---
title: "Go’dan bir Azure sanal makinesini dağıtma"
description: "Go için Azure SDK’yı kullanarak bir sanal makineyi dağıtın."
keywords: azure, sanal makine, vm, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 02/08/2018
ms.topic: quickstart
ms.devlang: go
manager: routlaw
ms.openlocfilehash: ae460dbf21b13c40f3d564274f8b790afe005aae
ms.sourcegitcommit: af3473779cd7c2978f290fbdc51ee15eb1130840
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="7f486-104">Hızlı başlangıç: Go için Azure SDK ile bir şablondan Azure sanal makinesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="7f486-104">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="7f486-105">Bu hızlı başlangıç, Go için Azure SDK ile bir şablondan kaynakları dağıtmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="7f486-105">This quickstart focuses on deploying resources from a template with the Azure SDK for Go.</span></span> <span data-ttu-id="7f486-106">Şablonlar, [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) içinde bulunan tüm kaynakların anlık görüntüleridir.</span><span class="sxs-lookup"><span data-stu-id="7f486-106">Templates are snapshots of all of the resources contained within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="7f486-107">İlerledikçe, kullanışlı bir görevi gerçekleştirirken SDK’nın işlevlerini ve kurallarını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7f486-107">Along the way, you'll become familiar with the functionality and conventions of the SDK while performing a useful task.</span></span>

<span data-ttu-id="7f486-108">Bu hızlı başlangıcın sonunda, bir kullanıcı adı ve parola ile oturum açtığınız çalışan bir sanal makineniz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f486-108">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="7f486-109">Azure CLI’nın yerel bir yüklemesini kullanıyorsanız bu hızlı başlangıç, 2.0.24 veya sonraki sürümleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7f486-109">If you use a local install of the Azure CLI, this quickstart requires CLI version 2.0.24 or later.</span></span> <span data-ttu-id="7f486-110">CLI yüklemenizin bu gereksinimi karşıladığından emin olmak için `az --version` çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f486-110">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="7f486-111">Yükleme veya yükseltme yapmanız gerekirse [Azure CLI 2.0’ı yükleyin](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7f486-111">If you need to install or upgrade, see [Install the Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="7f486-112">Go için Azure SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="7f486-112">Install the Azure SDK for Go</span></span> 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="7f486-113">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f486-113">Create a service principal</span></span>

<span data-ttu-id="7f486-114">Bir uygulamada etkileşimli olmadan oturum açmak için hizmet sorumlusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f486-114">To log in non-interactively with an application, you need a service principal.</span></span> <span data-ttu-id="7f486-115">Hizmet sorumluları, benzersiz bir kullanıcı kimliği oluşturan rol tabanlı erişim denetiminin (RBAC) parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="7f486-115">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="7f486-116">CLI ile yeni bir hizmet sorumlusu oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7f486-116">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

<span data-ttu-id="7f486-117">Çıkıştaki `appId`, `password` ve `tenant` değerlerini kaydettiğinizden __emin olun__.</span><span class="sxs-lookup"><span data-stu-id="7f486-117">__Make sure__ to record the `appId`, `password`, and `tenant` values in the output.</span></span> <span data-ttu-id="7f486-118">Bu değerler uygulama tarafından Azure kimlik doğrulaması yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f486-118">These values are used by the application to authenticate with Azure.</span></span>

<span data-ttu-id="7f486-119">Azure CLI 2.0 ile hizmet sorumluları oluşturma ve bunları yönetme hakkında daha fazla bilgi için bkz. [Azure CLI 2.0 ile Azure hizmet sorumlusu oluşturma](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7f486-119">For more information on creating and managing service principals with the Azure CLI 2.0, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>

## <a name="get-the-code"></a><span data-ttu-id="7f486-120">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="7f486-120">Get the code</span></span>

<span data-ttu-id="7f486-121">`go get` ile hızlı başlangıç kodunu ve tüm bağımlılıklarını edinin.</span><span class="sxs-lookup"><span data-stu-id="7f486-121">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

<span data-ttu-id="7f486-122">Bu kod derlenir, ancak siz Azure hesabınızla ve oluşturulan hizmet sorumlusuyla ilgili bilgileri sağlayıncaya kadar düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="7f486-122">This code compiles, but doesn't run correctly until you provide it information about your Azure account and the created service principal.</span></span> <span data-ttu-id="7f486-123">`main.go` içinde, bir `authInfo` yapısı içeren `config` değişkeni vardır.</span><span class="sxs-lookup"><span data-stu-id="7f486-123">In `main.go` there is a variable, `config`, which contains an `authInfo` struct.</span></span> <span data-ttu-id="7f486-124">Bu yapının düzgün şekilde kimlik doğrulaması yapması için alan değerlerinin değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f486-124">This struct needs to have its field values replaced in order to authenticate correctly.</span></span>

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* <span data-ttu-id="7f486-125">`SubscriptionID`: CLI komutundan alınabilen abonelik kimliğiniz</span><span class="sxs-lookup"><span data-stu-id="7f486-125">`SubscriptionID`: Your subscription ID, which can be obtained from the CLI command</span></span>

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* <span data-ttu-id="7f486-126">`TenantID`: Hizmet sorumlusu oluşturulurken kaydedilen `tenant` değeri olan kiracı kimliğiniz</span><span class="sxs-lookup"><span data-stu-id="7f486-126">`TenantID`: Your tenant ID, the `tenant` value recorded when creating the service principal</span></span>
* <span data-ttu-id="7f486-127">`ServicePrincipalID`: Hizmet sorumlusu oluşturulurken kaydedilen `appId` değeri</span><span class="sxs-lookup"><span data-stu-id="7f486-127">`ServicePrincipalID`: The `appId` value recorded when creating the service principal</span></span>
* <span data-ttu-id="7f486-128">`ServicePrincipalSecret`: Hizmet sorumlusu oluşturulurken kaydedilen `password` değeri</span><span class="sxs-lookup"><span data-stu-id="7f486-128">`ServicePrincipalSecret`: The `password` value recorded when creating the service principal</span></span>

<span data-ttu-id="7f486-129">`vm-quickstart-params.json` dosyasındaki bir değeri de düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f486-129">You also need to edit a value in the `vm-quickstart-params.json` file.</span></span>

```json
    "vm_password": {
        "value": "_"
    }
```

* <span data-ttu-id="7f486-130">`vm_password`: VM kullanıcı hesabı için parola.</span><span class="sxs-lookup"><span data-stu-id="7f486-130">`vm_password`: The password for the VM user account.</span></span> <span data-ttu-id="7f486-131">12-72 karakter uzunluğunda olmalı ve şu karakterlerden üçünü içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7f486-131">It must be 12-72 characters in length and contain 3 of the following characters:</span></span>
  * <span data-ttu-id="7f486-132">Bir küçük harf</span><span class="sxs-lookup"><span data-stu-id="7f486-132">A lowercase letter</span></span>
  * <span data-ttu-id="7f486-133">Bir büyük harf</span><span class="sxs-lookup"><span data-stu-id="7f486-133">An uppercase letter</span></span>
  * <span data-ttu-id="7f486-134">Bir rakam</span><span class="sxs-lookup"><span data-stu-id="7f486-134">A number</span></span>
  * <span data-ttu-id="7f486-135">Bir sembol</span><span class="sxs-lookup"><span data-stu-id="7f486-135">A symbol</span></span>

## <a name="running-the-code"></a><span data-ttu-id="7f486-136">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7f486-136">Running the code</span></span>

<span data-ttu-id="7f486-137">`go run` komutu ile hızlı başlangıcı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f486-137">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

<span data-ttu-id="7f486-138">Dağıtımda bir hata varsa bir sorun olduğunu belirten ancak özel ayrıntıları içermeyen bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f486-138">If there is a failure in the deployment, you get a message indicating that there was an issue, but without any specific details.</span></span> <span data-ttu-id="7f486-139">Azure CLI’yı kullanarak aşağıdaki komut ile dağıtım hatasının ayrıntılarını alın:</span><span class="sxs-lookup"><span data-stu-id="7f486-139">Using the Azure CLI, get the details of the deployment failure with the following command:</span></span>

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

<span data-ttu-id="7f486-140">Dağıtım başarılı olursa yeni oluşturulan sanal makinede oturum açmak için kullanıcı adını, IP adresini ve parolayı sunan bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f486-140">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="7f486-141">Çalışır durumda olduğunu onaylamak için bu makinede SSH işlemi yapın.</span><span class="sxs-lookup"><span data-stu-id="7f486-141">SSH into this machine to confirm that it is up and running.</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="7f486-142">Temizleme</span><span class="sxs-lookup"><span data-stu-id="7f486-142">Cleaning up</span></span>

<span data-ttu-id="7f486-143">CLI ile kaynak grubunu silerek bu hızlı başlangıç sırasında oluşturulan kaynakları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="7f486-143">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a><span data-ttu-id="7f486-144">Kod ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="7f486-144">Code in depth</span></span>

<span data-ttu-id="7f486-145">Hızlı başlangıç kodunun yaptığı işlem bir değişken öbeğine ve birçok küçük işleve ayrılmış ve her biri burada incelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="7f486-145">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variable-assignments-and-structs"></a><span data-ttu-id="7f486-146">Değişken atamaları ve yapıları</span><span class="sxs-lookup"><span data-stu-id="7f486-146">Variable assignments and structs</span></span>

<span data-ttu-id="7f486-147">Hızlı başlangıç kendi içinde bulunduğundan, komut satırı seçenekleri veya ortam değişkenleri yerine genel değişkenleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="7f486-147">Since quickstart is self-contained, it uses global variables rather than command-line options or environment variables.</span></span>

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

<span data-ttu-id="7f486-148">Azure hizmetlerinde kimlik doğrulaması yapmak için gerekli tüm bilgileri kapsüllemek için `authInfo` yapısı bildirilir.</span><span class="sxs-lookup"><span data-stu-id="7f486-148">The `authInfo` struct is declared to encapsulate all of the information needed for authorization with Azure services.</span></span>

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

var (
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }

    ctx = context.Background()

    token *adal.ServicePrincipalToken
)
```

<span data-ttu-id="7f486-149">Oluşturulan kaynakların adlarını veren değerler bildirilir.</span><span class="sxs-lookup"><span data-stu-id="7f486-149">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="7f486-150">Burada konum da belirtilir; dağıtımların diğer veri merkezlerinde nasıl davrandığını görmek için konumu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f486-150">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="7f486-151">Her veri merkezinde tüm gerekli kaynaklar mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="7f486-151">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="7f486-152">`templateFile` ve `parametersFile` sabitleri, dağıtım için gerekli dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="7f486-152">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="7f486-153">Hizmet sorumlusu belirteci daha sonra ele alınacaktır. `ctx` değişkeni, ağ işlemleri için [Go bağlamıdır](https://blog.golang.org/context).</span><span class="sxs-lookup"><span data-stu-id="7f486-153">The service principal token is covered later, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="init-and-authorization"></a><span data-ttu-id="7f486-154">init() ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="7f486-154">init() and authorization</span></span>

<span data-ttu-id="7f486-155">Kod için `init()` yöntemi, yetkilendirmeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7f486-155">The `init()` method for the code sets up authorization.</span></span> <span data-ttu-id="7f486-156">Yetkilendirme, hızlı başlangıçtaki her şey için önkoşul olduğundan, başlatmanın parçası olması mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="7f486-156">Since authorization is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> 

```go
// Authenticate with the Azure services over OAuth, using a service principal.
func init() {
    oauthConfig, err := adal.NewOAuthConfig(azure.PublicCloud.ActiveDirectoryEndpoint, config.TenantID)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v\n", err)
    }
    token, err = adal.NewServicePrincipalToken(
        *oauthConfig,
        config.ServicePrincipalID,
        config.ServicePrincipalSecret,
        azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("faled to get token: %v\n", err)
    }
}
```

<span data-ttu-id="7f486-157">Bu kod, yetkilendirme için iki adımı tamamlar:</span><span class="sxs-lookup"><span data-stu-id="7f486-157">This code completes two steps for authorization:</span></span>

* <span data-ttu-id="7f486-158">`TenantID` için OAuth yapılandırma bilgileri, Azure Active Directory ile arabirim oluşturularak alınır.</span><span class="sxs-lookup"><span data-stu-id="7f486-158">OAuth configuration information for the `TenantID` is retrieved by interfacing with Azure Active Directory.</span></span> <span data-ttu-id="7f486-159">[`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) nesnesi, standart Azure yapılandırmasında kullanılan uç noktaları içerir.</span><span class="sxs-lookup"><span data-stu-id="7f486-159">The [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) object contains endpoints used in the standard Azure configuration.</span></span>
* <span data-ttu-id="7f486-160">[`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken) işlevi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7f486-160">The [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken) function is called.</span></span> <span data-ttu-id="7f486-161">Bu işlev, hangi Azure yönetimi stilinin kullanılmakta olduğu bilgisinin yanı sıra, hizmet sorumlusu oturum açma adı ile birlikte OAuth bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="7f486-161">This function takes the OAuth information along with the service principal login, as well as which style of Azure management is being used.</span></span> <span data-ttu-id="7f486-162">Belirli gereksinimlere sahip değilseniz ve ne yaptığınızı bilmiyorsanız bu değer her zaman `.ResourceManagerEndpoint` olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f486-162">Unless you have specific requirements and know what you're doing, this value should always be `.ResourceManagerEndpoint`.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="7f486-163">main() içindeki işlem akışı</span><span class="sxs-lookup"><span data-stu-id="7f486-163">Flow of operations in main()</span></span>

<span data-ttu-id="7f486-164">`main()` işlevi basittir, yalnızca işlem akışını belirtir ve hata denetimi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7f486-164">The `main()` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("created group: %v\n", *group.Name)

    log.Println("starting deployment")
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy correctly: %v", err)
    }
    log.Printf("Completed deployment: %v", *result.Name)
    getLogin()
}
```

<span data-ttu-id="7f486-165">Kodun çalıştırılma adımları sırayla şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7f486-165">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="7f486-166">(`createGroup()`) hedefine dağıtılacak kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f486-166">Create the resource group to deploy to (`createGroup()`)</span></span>
* <span data-ttu-id="7f486-167">Bu grup (`createDeployment()`) içinde dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f486-167">Create the deployment within this group (`createDeployment()`)</span></span>
* <span data-ttu-id="7f486-168">Dağıtılan VM (`getLogin()`) için oturum açma bilgilerini alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7f486-168">Obtain and display login information for the deployed VM (`getLogin()`)</span></span>

### <a name="creating-the-resource-group"></a><span data-ttu-id="7f486-169">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f486-169">Creating the resource group</span></span>

<span data-ttu-id="7f486-170">`createGroup()` işlevi, kaynak grubunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7f486-170">The `createGroup()` function creates the resource group.</span></span> <span data-ttu-id="7f486-171">Çağrı akışına ve bağımsız değişkenlere bakılarak, SDK’da hizmet etkileşimlerinin yapılandırılma şekli görülebilir.</span><span class="sxs-lookup"><span data-stu-id="7f486-171">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

```go
func createGroup() (group resources.Group, err error) {
        groupsClient := resources.NewGroupsClient(config.SubscriptionID)
        groupsClient.Authorizer = autorest.NewBearerAuthorizer(token)

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

<span data-ttu-id="7f486-172">Bir Azure hizmetiyle etkileşim kurmanın genel akışı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7f486-172">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="7f486-173">`service.NewXClient()` yöntemini kullanarak istemciyi oluşturun; burada `X`, etkileşim kurmak istediğiniz `service` öğesinin kaynak türüdür.</span><span class="sxs-lookup"><span data-stu-id="7f486-173">Create the client using the `service.NewXClient()` method, where `X` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="7f486-174">Bu işlev her zaman bir abonelik kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="7f486-174">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="7f486-175">İstemci için yetkilendirme yöntemini ayarlayarak istemcinin uzak API ile etkileşim kurmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7f486-175">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="7f486-176">Yöntem çağrısını uzak API’ye karşılık gelen istemcide yapın.</span><span class="sxs-lookup"><span data-stu-id="7f486-176">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="7f486-177">Hizmet istemcisi yöntemleri genellikle kaynağın adını ve bir meta veri nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="7f486-177">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="7f486-178">[`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) işlevi burada bir tür dönüştürmesi gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f486-178">The [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="7f486-179">SDK’nın yöntemleri için parametre yapıları hemen her zaman işaretçiler aldığından, bu yöntemler tür dönüştürmelerini kolaylaştırmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7f486-179">The parameters structs for methods of the SDK almost exclusively take pointers, so these methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="7f486-180">Kolaylık dönüştürücülerinin tam listesi ve davranışları için [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) modülüne ilişkin belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7f486-180">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list and behavior of convenience converters.</span></span>

<span data-ttu-id="7f486-181">`groupsClient.CreateOrUpdate()` işlemi, kaynak grubunu temsil eden bir veri yapısına işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7f486-181">The `groupsClient.CreateOrUpdate()` operation returns a pointer to a data struct representing the resource group.</span></span> <span data-ttu-id="7f486-182">Bu tür bir doğrudan dönüş değeri, zaman uyumlu olacak şekilde tasarlanmış kısa süreli bir işlemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="7f486-182">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="7f486-183">Sonraki bölümde, uzun süreli bir işlem örneğini ve bunlarla nasıl etkileşim kurulacağını göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7f486-183">In the next section, you'll see an example of a long-running operation and how to interact with them.</span></span>

### <a name="performing-the-deployment"></a><span data-ttu-id="7f486-184">Dağıtımı gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="7f486-184">Performing the deployment</span></span>

<span data-ttu-id="7f486-185">Kaynaklarını içerecek grup oluşturulduktan sonra sıra dağıtımı çalıştırmaya gelir.</span><span class="sxs-lookup"><span data-stu-id="7f486-185">Once the group to contain its resources is created, it's time to run the deployment.</span></span> <span data-ttu-id="7f486-186">Bu kod, mantığının farklı kısımlarını vurgulamak için daha küçük bölümlere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7f486-186">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>


```go
func createDeployment() (deployment resources.DeploymentExtended, err error) {
    template, err := readJSON(templateFile)
    if err != nil {
        return
    }
    params, err := readJSON(parametersFile)
    if err != nil {
        return
    }

        // ...
```

<span data-ttu-id="7f486-187">Dağıtım dosyaları `readJSON` tarafından yüklenir; bunun ayrıntıları burada atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7f486-187">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="7f486-188">Bu işlev, kaynak dağıtım çağrısı için meta verilerin oluşturulmasında kullanılan `*map[string]interface{}` türünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="7f486-188">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span>

```go
        // ...
        
        deploymentsClient := resources.NewDeploymentsClient(config.SubscriptionID)
        deploymentsClient.Authorizer = autorest.NewBearerAuthorizer(token)

        deploymentFuture, err := deploymentsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                deploymentName,
                resources.Deployment{
                        Properties: &resources.DeploymentProperties{
                                Template:   template,
                                Parameters: params,
                                Mode:       resources.Incremental,
                        },
                },
        )
        if err != nil {
                log.Fatalf("Failed to create deployment: %v", err)
        }
        //...
```

<span data-ttu-id="7f486-189">Bu kod, kaynak grubunun oluşturulmasıyla aynı deseni izler.</span><span class="sxs-lookup"><span data-stu-id="7f486-189">This code follows the same pattern as with creating the resource group.</span></span> <span data-ttu-id="7f486-190">Azure kimlik doğrulaması sayesinde yeni bir istemci oluşturulur ve sonra bir yöntem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7f486-190">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span> <span data-ttu-id="7f486-191">Yöntemin adı (`CreateOrUpdate`) bile kaynak grupları için karşılık gelen yöntemin adıyla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7f486-191">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="7f486-192">Bu desen, SDK’da tekrar tekrar görünür.</span><span class="sxs-lookup"><span data-stu-id="7f486-192">This pattern is seen again and again in the SDK.</span></span> <span data-ttu-id="7f486-193">Benzer işi gerçekleştiren yöntemler normalde aynı ada sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7f486-193">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="7f486-194">En büyük fark, `deploymentsClient.CreateOrUpdate()` yönteminin dönüş değerindedir.</span><span class="sxs-lookup"><span data-stu-id="7f486-194">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate()` method.</span></span> <span data-ttu-id="7f486-195">Bu değer, [vadeli işlem tasarım desenini](https://en.wikipedia.org/wiki/Futures_and_promises) izleyen bir `Future` nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="7f486-195">This value is a `Future` object, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="7f486-196">Vadeli işlemler, Azure’da başka iş yaparken ara sıra yoklamak isteyebileceğiniz uzun süreli bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="7f486-196">Futures represent a long-running operation in Azure that you may want to occasionally poll while performing other work.</span></span>

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

<span data-ttu-id="7f486-197">Bu örnek için yapılacak en iyi şey, işlemin tamamlanmasını beklemektir.</span><span class="sxs-lookup"><span data-stu-id="7f486-197">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="7f486-198">Vadeli işlemin beklenmesi için hem bir [bağlam nesnesi](https://blog.golang.org/context) hem de Future nesnesini oluşturan istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f486-198">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the Future object.</span></span> <span data-ttu-id="7f486-199">Burada iki olası hata kaynağı vardır: Yöntem çağrılmaya çalışılırken istemci tarafında bir hataya yol açılmıştır ve sunucudan bir hata yanıtı alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="7f486-199">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="7f486-200">İkinci durum, `deploymentFuture.Result()` çağrısının parçası olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="7f486-200">The latter is returned as part of the `deploymentFuture.Result()` call.</span></span>

### <a name="obtaining-the-assigned-ip-address"></a><span data-ttu-id="7f486-201">Atanan IP adresini alma</span><span class="sxs-lookup"><span data-stu-id="7f486-201">Obtaining the assigned IP address</span></span>

<span data-ttu-id="7f486-202">Yeni oluşturulan VM ile herhangi bir şey yapmak için atanan IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f486-202">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="7f486-203">IP adresleri, Ağ Arabirim Denetleyicisi (NIC) kaynaklarına bağlı olan kendi ayrı Azure kaynaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="7f486-203">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

```go
func getLogin() {
        params, err := readJSON(parametersFile)
        if err != nil {
                log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
        }

        addressClient := network.NewPublicIPAddressesClient(config.SubscriptionID)
        addressClient.Authorizer = autorest.NewBearerAuthorizer(token)
        ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
        ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
        if err != nil {
                log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
        }

        vmUser := (*params)["vm_user"].(map[string]interface{})
        vmPass := (*params)["vm_password"].(map[string]interface{})

        log.Printf("Log in with ssh: %s@%s, password: %s",
                vmUser["value"].(string),
                *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
                vmPass["value"].(string))
}
```

<span data-ttu-id="7f486-204">Bu yöntem, parametreler dosyasında depolanan bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="7f486-204">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="7f486-205">Bu kod, NIC’sini almak için doğrudan VM’yi sorgulayabilir, IP kaynağını almak için NIC’yi sorgulayabilir ve sonra doğrudan IP kaynağını sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="7f486-205">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="7f486-206">Çözümlenecek uzun bir bağımlılıklar ve işlemler zincirinin olması, bunu pahalı kılar.</span><span class="sxs-lookup"><span data-stu-id="7f486-206">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="7f486-207">JSON bilgileri yerel olduğundan, bunun yerine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7f486-207">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="7f486-208">VM kullanıcı adı ve parola değerleri de benzer şekilde JSON’dan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7f486-208">The values for the VM user and password are likewise loaded from the JSON.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f486-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f486-209">Next steps</span></span>

<span data-ttu-id="7f486-210">Bu hızlı başlangıçta, mevcut bir şablonu alıp Go aracılığıyla dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="7f486-210">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="7f486-211">Sonra, çalıştığından emin olmak için yeni oluşturulan sanal makineye SSH aracılığıyla bağlandınız.</span><span class="sxs-lookup"><span data-stu-id="7f486-211">Then you connected to the newly created VM via SSH to ensure that it's running.</span></span>

<span data-ttu-id="7f486-212">Go ile Azure ortamında sanal makinelerle çalışma hakkında bilgi edinmeye devam etmek için [Go için Azure bilgi işlem örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) veya [Go için Azure kaynak yönetimi örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="7f486-212">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>
