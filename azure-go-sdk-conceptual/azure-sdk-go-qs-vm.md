---
title: Go’dan bir Azure sanal makinesini dağıtma
description: Go için Azure SDK’yı kullanarak bir sanal makine dağıtın.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: quickstart
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: a7970be0857fd414d776241b033af0c23457790c
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059144"
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="51db5-103">Hızlı başlangıç: Go için Azure SDK ile bir şablondan Azure sanal makinesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="51db5-103">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="51db5-104">Bu hızlı başlangıçta Go için Azure SDK'yı kullanarak Azure Resource Manager şablonundan kaynak dağıtma adımları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="51db5-104">This quickstart shows you how to deploy resources from an Azure Resource Manager template, using the Azure SDK for Go.</span></span> <span data-ttu-id="51db5-105">Şablonlar, bir [Azure kaynak grubu](/azure/azure-resource-manager/resource-group-overview) içindeki tüm kaynakların anlık görüntüleridir.</span><span class="sxs-lookup"><span data-stu-id="51db5-105">Templates are snapshots of all of the resources within an [Azure resource group](/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="51db5-106">İlerledikçe SDK’nın işlevlerini ve kurallarını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="51db5-106">Along the way, you'll become familiar with the functionality and conventions of the SDK.</span></span>

<span data-ttu-id="51db5-107">Bu hızlı başlangıcın sonunda, bir kullanıcı adı ve parola ile oturum açtığınız çalışan bir sanal makineniz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="51db5-107">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

> [!NOTE]
> <span data-ttu-id="51db5-108">Go içinde Resource Manager şablonu kullanılmadan VM oluşturma adımlarını görmek için SDK ile VM kaynağı oluşturma ve yapılandırma süreçlerini gösteren bu [kesinlik temelli örneği](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm.go) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="51db5-108">To see the creation of a VM in Go without the use of a Resource Manager template, there is an [imperative sample](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm.go) demonstrating how to build and configure all VM resources with the SDK.</span></span> <span data-ttu-id="51db5-109">Bu örnekte şablon kullanılmasının nedeni, Azure hizmet mimarisinin ayrıntılarına fazla girmeden SDK kurallarına odaklanmaktır.</span><span class="sxs-lookup"><span data-stu-id="51db5-109">Using a template in this sample allows a focus on SDK conventions without getting into too many details about Azure service architecture.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="51db5-110">Azure CLI’nın yerel bir yüklemesini kullanıyorsanız bu hızlı başlangıç, __2.0.28__ veya sonraki CLI sürümlerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="51db5-110">If you use a local install of the Azure CLI, this quickstart requires CLI version __2.0.28__ or later.</span></span> <span data-ttu-id="51db5-111">CLI yüklemenizin bu gereksinimi karşıladığından emin olmak için `az --version` çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="51db5-111">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="51db5-112">Yükleme veya yükseltme yapmanız gerekirse bkz. [Azure CLI’yı yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="51db5-112">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="51db5-113">Go için Azure SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="51db5-113">Install the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="51db5-114">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="51db5-114">Create a service principal</span></span>

<span data-ttu-id="51db5-115">Bir uygulama ile Azure’da etkileşimli olmadan oturum açmak için hizmet sorumlusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="51db5-115">To sign in non-interactively to Azure with an application, you need a service principal.</span></span> <span data-ttu-id="51db5-116">Hizmet sorumluları, benzersiz bir kullanıcı kimliği oluşturan rol tabanlı erişim denetiminin (RBAC) parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="51db5-116">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="51db5-117">CLI ile yeni bir hizmet sorumlusu oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="51db5-117">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth > quickstart.auth
```

<span data-ttu-id="51db5-118">`AZURE_AUTH_LOCATION` ortam değişkenini bu dosyaya giden tam yol olacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="51db5-118">Set the environment variable `AZURE_AUTH_LOCATION` to be the full path to this file.</span></span> <span data-ttu-id="51db5-119">Daha sonra hizmet sorumlusundan herhangi bir değişiklik yapmanıza veya bilgi kaydetmenize gerek kalmadan SDK kimlik bilgilerini bulur ve doğrudan bu dosyadan okur.</span><span class="sxs-lookup"><span data-stu-id="51db5-119">Then the SDK locates and reads the credentials directly from this file, without you having to make any changes or record information from the service principal.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="51db5-120">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="51db5-120">Get the code</span></span>

<span data-ttu-id="51db5-121">`go get` ile hızlı başlangıç kodunu ve tüm bağımlılıklarını edinin.</span><span class="sxs-lookup"><span data-stu-id="51db5-121">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm/...
```

<span data-ttu-id="51db5-122">`AZURE_AUTH_LOCATION` değişkeni düzgün şekilde ayarlanmışsa kaynak kodunda herhangi bir değişiklik yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="51db5-122">You don't need to make any source code modifications if the `AZURE_AUTH_LOCATION` variable is properly set.</span></span> <span data-ttu-id="51db5-123">Program çalıştığında, gerekli olan tüm kimlik doğrulama bilgilerini buradan yükler.</span><span class="sxs-lookup"><span data-stu-id="51db5-123">When the program runs, it loads all the necessary authentication information from there.</span></span>

## <a name="running-the-code"></a><span data-ttu-id="51db5-124">Kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="51db5-124">Running the code</span></span>

<span data-ttu-id="51db5-125">`go run` komutu ile hızlı başlangıcı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="51db5-125">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm
go run main.go
```

<span data-ttu-id="51db5-126">Dağıtım başarılı olursa yeni oluşturulan sanal makinede oturum açmak için kullanıcı adını, IP adresini ve parolayı sunan bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="51db5-126">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="51db5-127">Makineye SSH ile bağlanarak çalışır durumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="51db5-127">SSH into this machine to see if it's up and running.</span></span> 

## <a name="cleaning-up"></a><span data-ttu-id="51db5-128">Temizleme</span><span class="sxs-lookup"><span data-stu-id="51db5-128">Cleaning up</span></span>

<span data-ttu-id="51db5-129">CLI ile kaynak grubunu silerek bu hızlı başlangıç sırasında oluşturulan kaynakları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="51db5-129">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

<span data-ttu-id="51db5-130">Ayrıca oluşturulmuşsa hizmet sorumlusunu silin.</span><span class="sxs-lookup"><span data-stu-id="51db5-130">Also delete the service principal that was created.</span></span> <span data-ttu-id="51db5-131">`quickstart.auth` dosyasında `clientId` için bir JSON anahtarı bulunur.</span><span class="sxs-lookup"><span data-stu-id="51db5-131">In the `quickstart.auth` file, there's a JSON key for `clientId`.</span></span> <span data-ttu-id="51db5-132">Bu değeri `CLIENT_ID_VALUE` ortam değişkenine kopyalayın ve aşağıdaki Azure CLI komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="51db5-132">Copy this value to the `CLIENT_ID_VALUE` environment variable and run the following Azure CLI command:</span></span>

```azurecli-interactive
az ad sp delete --id ${CLIENT_ID_VALUE}
```

<span data-ttu-id="51db5-133">Burada `quickstart.auth` ile alınan `CLIENT_ID_VALUE` değerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51db5-133">Where you supply the value for `CLIENT_ID_VALUE` from `quickstart.auth`.</span></span>

> [!WARNING]
> <span data-ttu-id="51db5-134">Bu uygulamanın hizmet sorumlusunu silmezseniz Azure Active Directory kiracınızda etkin bir şekilde bırakılır.</span><span class="sxs-lookup"><span data-stu-id="51db5-134">Failing to delete the service principal for this application leaves it active in your Azure Active Directory tenant.</span></span>
> <span data-ttu-id="51db5-135">Hizmet sorumlusunun adı ve parolası UUID olarak oluşturuluyor olsa da kullanılmayan hizmet sorumlularını ve Azure Active Directory uygulamalarını silerek güvenlik açısından sorun yaratmalarını önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51db5-135">While both the name and password for the service principal are generated as UUIDs, make sure that you follow good security practices by deleting any unused service principals and Azure Active Directory Applications.</span></span>

## <a name="code-in-depth"></a><span data-ttu-id="51db5-136">Kod ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="51db5-136">Code in depth</span></span>

<span data-ttu-id="51db5-137">Hızlı başlangıç kodunun yaptığı işlem bir değişken öbeğine ve birçok küçük işleve ayrılmış ve her biri burada incelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="51db5-137">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variables-constants-and-types"></a><span data-ttu-id="51db5-138">Değişkenler, sabitler ve türler</span><span class="sxs-lookup"><span data-stu-id="51db5-138">Variables, constants, and types</span></span>

<span data-ttu-id="51db5-139">Hızlı başlangıç kendi içinde olduğundan, genel sabitleri ve değişkenleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="51db5-139">Since quickstart is self-contained, it uses global constants and variables.</span></span>

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

// Information loaded from the authorization file to identify the client
type clientInfo struct {
    SubscriptionID string
    VMPassword     string
}

var (
    ctx        = context.Background()
    clientData clientInfo
    authorizer autorest.Authorizer
)
```

<span data-ttu-id="51db5-140">Oluşturulan kaynakların adlarını veren değerler bildirilir.</span><span class="sxs-lookup"><span data-stu-id="51db5-140">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="51db5-141">Burada konum da belirtilir; dağıtımların diğer veri merkezlerinde nasıl davrandığını görmek için konumu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51db5-141">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="51db5-142">Her veri merkezinde tüm gerekli kaynaklar mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="51db5-142">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="51db5-143">`clientInfo` türü, SDK’da istemcileri ve VM parolasını ayarlamak üzere kimlik doğrulama dosyasından yüklenen bilgileri barındırır.</span><span class="sxs-lookup"><span data-stu-id="51db5-143">The `clientInfo` type holds the information loaded from the authentication file to set up clients in the SDK and set the VM password.</span></span>

<span data-ttu-id="51db5-144">`templateFile` ve `parametersFile` sabitleri, dağıtım için gerekli dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="51db5-144">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="51db5-145">`authorizer` değişkeni kimlik doğrulaması için Go SDK’sı tarafından yapılandırılır ve `ctx` değişkeni ise ağ işlemleri için bir [Go bağlamıdır](https://blog.golang.org/context).</span><span class="sxs-lookup"><span data-stu-id="51db5-145">The `authorizer` will be configured by the Go SDK for authentication, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="authentication-and-initialization"></a><span data-ttu-id="51db5-146">Kimlik doğrulama ve başlatma</span><span class="sxs-lookup"><span data-stu-id="51db5-146">Authentication and initialization</span></span>

<span data-ttu-id="51db5-147">`init` işlevi kimlik doğrulamayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="51db5-147">The `init` function sets up authentication.</span></span> <span data-ttu-id="51db5-148">Yetkilendirme, hızlı başlangıçtaki her şey için önkoşul olduğundan, başlatmanın parçası olması mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="51db5-148">Since authentication is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> <span data-ttu-id="51db5-149">Ayrıca istemcileri ve VM’yi yapılandırmak için kimlik doğrulama dosyasından gerekli olan bazı bilgileri yükler.</span><span class="sxs-lookup"><span data-stu-id="51db5-149">It also loads some information needed from the authentication file to configure clients and the VM.</span></span>

```go
func init() {
    var err error
    authorizer, err = auth.NewAuthorizerFromFile(azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v", err)
    }

    authInfo, err := readJSON(os.Getenv("AZURE_AUTH_LOCATION"))
    clientData.SubscriptionID = (*authInfo)["subscriptionId"].(string)
    clientData.VMPassword = (*authInfo)["clientSecret"].(string)
}
```

<span data-ttu-id="51db5-150">İlk olarak, `AZURE_AUTH_LOCATION` konumunda bulunan dosyadan kimlik doğrulama bilgilerini yüklemek için [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) çağrılır.</span><span class="sxs-lookup"><span data-stu-id="51db5-150">First, [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) is called to load the authentication information from the file located at `AZURE_AUTH_LOCATION`.</span></span> <span data-ttu-id="51db5-151">Ardından dosya `readJSON` işlevi tarafından el ile yüklenerek (burada göz ardı edilir), programın geri kalanını çalıştırmak için gereken iki değerin çekilmesi sağlanır: İstemcinin abonelik kimliği ve VM’nin parolası için de kullanılan hizmet sorumlusunun gizli dizisi.</span><span class="sxs-lookup"><span data-stu-id="51db5-151">Next, this file is loaded manually by the `readJSON` function (omitted here) to pull the two values needed to run the rest of the program: The subscription ID of the client, and the service principal's secret, which is also used for the VM's password.</span></span>

> [!WARNING]
> <span data-ttu-id="51db5-152">Hızlı başlangıcı basit tutmak için hizmet sorumlusu parolası yeniden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51db5-152">To keep the quickstart simple, the service principal password is reused.</span></span> <span data-ttu-id="51db5-153">Üretimdeyken Azure kaynaklarınıza erişim sağlayan bir parolayı __asla__ yeniden kullanmamaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="51db5-153">In production, take care to __never__ reuse a password which gives access to your Azure resources.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="51db5-154">main() içindeki işlem akışı</span><span class="sxs-lookup"><span data-stu-id="51db5-154">Flow of operations in main()</span></span>

<span data-ttu-id="51db5-155">`main` işlevi basittir, yalnızca işlem akışını belirtir ve hata denetimi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="51db5-155">The `main` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("Created group: %v", *group.Name)

    log.Printf("Starting deployment: %s", deploymentName)
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy: %v", err)
    }
    if result.Name != nil {
        log.Printf("Completed deployment %v: %v", deploymentName, *result.Properties.ProvisioningState)
    } else {
        log.Printf("Completed deployment %v (no data returned to SDK)", deploymentName)
    }
    getLogin()
}
```

<span data-ttu-id="51db5-156">Kodun çalıştırılma adımları sırayla şöyledir:</span><span class="sxs-lookup"><span data-stu-id="51db5-156">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="51db5-157">(`createGroup`) hedefine dağıtılacak kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="51db5-157">Create the resource group to deploy to (`createGroup`)</span></span>
* <span data-ttu-id="51db5-158">Bu grup (`createDeployment`) içinde dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51db5-158">Create the deployment within this group (`createDeployment`)</span></span>
* <span data-ttu-id="51db5-159">Dağıtılan VM (`getLogin`) için oturum açma bilgilerini alma ve görüntüleme</span><span class="sxs-lookup"><span data-stu-id="51db5-159">Get and display login information for the deployed VM (`getLogin`)</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="51db5-160">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="51db5-160">Create the resource group</span></span>

<span data-ttu-id="51db5-161">`createGroup` işlevi, kaynak grubunu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="51db5-161">The `createGroup` function creates the resource group.</span></span> <span data-ttu-id="51db5-162">Çağrı akışına ve bağımsız değişkenlere bakılarak, SDK’da hizmet etkileşimlerinin yapılandırılma şekli görülebilir.</span><span class="sxs-lookup"><span data-stu-id="51db5-162">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

```go
func createGroup() (group resources.Group, err error) {
    groupsClient := resources.NewGroupsClient(clientData.SubscriptionID)
    groupsClient.Authorizer = authorizer

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

<span data-ttu-id="51db5-163">Bir Azure hizmetiyle etkileşim kurmanın genel akışı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="51db5-163">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="51db5-164">`service.New*Client()` yöntemini kullanarak istemciyi oluşturun; burada `*`, etkileşim kurmak istediğiniz `service` öğesinin kaynak türüdür.</span><span class="sxs-lookup"><span data-stu-id="51db5-164">Create the client using the `service.New*Client()` method, where `*` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="51db5-165">Bu işlev her zaman bir abonelik kimliği alır.</span><span class="sxs-lookup"><span data-stu-id="51db5-165">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="51db5-166">İstemci için yetkilendirme yöntemini ayarlayarak istemcinin uzak API ile etkileşim kurmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="51db5-166">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="51db5-167">Yöntem çağrısını uzak API’ye karşılık gelen istemcide yapın.</span><span class="sxs-lookup"><span data-stu-id="51db5-167">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="51db5-168">Hizmet istemcisi yöntemleri genellikle kaynağın adını ve bir meta veri nesnesini alır.</span><span class="sxs-lookup"><span data-stu-id="51db5-168">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="51db5-169">[`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) işlevi burada bir tür dönüştürmesi gerçekleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51db5-169">The [`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="51db5-170">SDK’nın yöntemleri için parametre yapıları hemen her zaman işaretçiler aldığından, bu yöntemler tür dönüştürmelerini kolaylaştırmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="51db5-170">The parameters for SDK methods almost exclusively take pointers, so convenience methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="51db5-171">Kolaylık dönüştürücülerinin tam listesi ve davranışları için [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) modülüne ilişkin belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="51db5-171">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list of convenience converters and their behavior.</span></span>

<span data-ttu-id="51db5-172">`groupsClient.CreateOrUpdate` yöntemi, kaynak grubunu temsil eden bir veri türüne işaretçiyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="51db5-172">The `groupsClient.CreateOrUpdate` method returns a pointer to a data type representing the resource group.</span></span> <span data-ttu-id="51db5-173">Bu tür bir doğrudan dönüş değeri, zaman uyumlu olacak şekilde tasarlanmış kısa süreli bir işlemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="51db5-173">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="51db5-174">Sonraki bölümde, uzun süreli bir işlem örneğini ve bunlarla nasıl etkileşim kurulacağını göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="51db5-174">In the next section, you'll see an example of a long-running operation and how to interact with it.</span></span>

### <a name="perform-the-deployment"></a><span data-ttu-id="51db5-175">Dağıtımı gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="51db5-175">Perform the deployment</span></span>

<span data-ttu-id="51db5-176">Kaynak grubu oluşturulduktan sonra sıra dağıtımı çalıştırmaya gelir.</span><span class="sxs-lookup"><span data-stu-id="51db5-176">Once the resource group is created, it's time to run the deployment.</span></span> <span data-ttu-id="51db5-177">Bu kod, mantığının farklı kısımlarını vurgulamak için daha küçük bölümlere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="51db5-177">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>

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
    (*params)["vm_password"] = map[string]string{
        "value": clientData.VMPassword,
    }
        // ...
```

<span data-ttu-id="51db5-178">Dağıtım dosyaları `readJSON` tarafından yüklenir; bunun ayrıntıları burada atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51db5-178">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="51db5-179">Bu işlev, kaynak dağıtım çağrısı için meta verilerin oluşturulmasında kullanılan `*map[string]interface{}` türünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="51db5-179">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span> <span data-ttu-id="51db5-180">VM’nin parolası ayrıca dağıtım parametrelerinde el ile ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51db5-180">The VM's password is also set manually on the deployment parameters.</span></span>

```go
        // ...

    deploymentsClient := resources.NewDeploymentsClient(clientData.SubscriptionID)
    deploymentsClient.Authorizer = authorizer

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
        return
    }
```

<span data-ttu-id="51db5-181">Bu kod, kaynak grubunun oluşturulmasıyla aynı deseni izler.</span><span class="sxs-lookup"><span data-stu-id="51db5-181">This code follows the same pattern as creating the resource group.</span></span> <span data-ttu-id="51db5-182">Azure kimlik doğrulaması sayesinde yeni bir istemci oluşturulur ve sonra bir yöntem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="51db5-182">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span>
<span data-ttu-id="51db5-183">Yöntemin adı (`CreateOrUpdate`) bile kaynak grupları için karşılık gelen yöntemin adıyla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="51db5-183">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="51db5-184">Bu desen SDK boyunca görülür.</span><span class="sxs-lookup"><span data-stu-id="51db5-184">This pattern is seen throughout the SDK.</span></span>
<span data-ttu-id="51db5-185">Benzer işi gerçekleştiren yöntemler normalde aynı ada sahiptir.</span><span class="sxs-lookup"><span data-stu-id="51db5-185">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="51db5-186">En büyük fark, `deploymentsClient.CreateOrUpdate` yönteminin dönüş değerindedir.</span><span class="sxs-lookup"><span data-stu-id="51db5-186">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate` method.</span></span> <span data-ttu-id="51db5-187">Bu değer, [vadeli işlem tasarım desenini](https://en.wikipedia.org/wiki/Futures_and_promises) izleyen bir [Vadeli işlem](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future) türüdür.</span><span class="sxs-lookup"><span data-stu-id="51db5-187">This value is of the [Future](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future) type, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="51db5-188">Vadeli işlemler, tamamlanması üzerine yoklama yapabileceğiniz, iptal edeceğiniz veya engelleyebileceğiniz Azure’daki uzun süreli bir işlemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="51db5-188">Futures represent a long-running operation in Azure that you can poll, cancel, or block on their completion.</span></span>

```go
        //...
    err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
    if err != nil {
        return
    }
    return deploymentFuture.Result(deploymentsClient)
}
```

<span data-ttu-id="51db5-189">Bu örnek için yapılacak en iyi şey, işlemin tamamlanmasını beklemektir.</span><span class="sxs-lookup"><span data-stu-id="51db5-189">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="51db5-190">Vadeli işlemin beklenmesi için hem bir [bağlam nesnesi](https://blog.golang.org/context) hem de `Future` nesnesini oluşturan istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="51db5-190">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the `Future`.</span></span> <span data-ttu-id="51db5-191">Burada iki olası hata kaynağı vardır: Yöntem çağrılmaya çalışılırken istemci tarafında bir hataya yol açılmıştır ve sunucudan bir hata yanıtı alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="51db5-191">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="51db5-192">İkinci durum, `deploymentFuture.Result` çağrısının parçası olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="51db5-192">The latter is returned as part of the `deploymentFuture.Result` call.</span></span>

### <a name="get-the-assigned-ip-address"></a><span data-ttu-id="51db5-193">Atanan IP adresini alma</span><span class="sxs-lookup"><span data-stu-id="51db5-193">Get the assigned IP address</span></span>

<span data-ttu-id="51db5-194">Yeni oluşturulan VM ile herhangi bir şey yapmak için atanan IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="51db5-194">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="51db5-195">IP adresleri, Ağ Arabirim Denetleyicisi (NIC) kaynaklarına bağlı olan kendi ayrı Azure kaynaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="51db5-195">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

```go
func getLogin() {
    params, err := readJSON(parametersFile)
    if err != nil {
        log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
    }

    addressClient := network.NewPublicIPAddressesClient(clientData.SubscriptionID)
    addressClient.Authorizer = authorizer
    ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
    ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
    if err != nil {
        log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
    }

    vmUser := (*params)["vm_user"].(map[string]interface{})

    log.Printf("Log in with ssh: %s@%s, password: %s",
        vmUser["value"].(string),
        *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
        clientData.VMPassword)
}
```

<span data-ttu-id="51db5-196">Bu yöntem, parametreler dosyasında depolanan bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="51db5-196">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="51db5-197">Bu kod, NIC’sini almak için doğrudan VM’yi sorgulayabilir, IP kaynağını almak için NIC’yi sorgulayabilir ve sonra doğrudan IP kaynağını sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="51db5-197">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="51db5-198">Çözümlenecek uzun bir bağımlılıklar ve işlemler zincirinin olması, bunu pahalı kılar.</span><span class="sxs-lookup"><span data-stu-id="51db5-198">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="51db5-199">JSON bilgileri yerel olduğundan, bunun yerine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="51db5-199">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="51db5-200">VM kullanıcısının değeri de ayrıca JSON’dan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="51db5-200">The value for the VM user is also loaded from the JSON.</span></span> <span data-ttu-id="51db5-201">VM parolası, kimlik doğrulama dosyasından önceden yüklendi.</span><span class="sxs-lookup"><span data-stu-id="51db5-201">The VM password was loaded earlier from the authentication file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51db5-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51db5-202">Next steps</span></span>

<span data-ttu-id="51db5-203">Bu hızlı başlangıçta, mevcut bir şablonu alıp Go aracılığıyla dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="51db5-203">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="51db5-204">Sonra, yeni oluşturulan sanal makineye SSH aracılığıyla bağlandınız.</span><span class="sxs-lookup"><span data-stu-id="51db5-204">Then you connected to the newly created VM via SSH.</span></span>

<span data-ttu-id="51db5-205">Go ile Azure ortamında sanal makinelerle çalışma hakkında bilgi edinmeye devam etmek için [Go için Azure bilgi işlem örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) veya [Go için Azure kaynak yönetimi örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="51db5-205">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>

<span data-ttu-id="51db5-206">SDK’daki kullanılabilir kimlik doğrulama yöntemleri ve destekledikleri kimlik doğrulama türleri hakkında daha fazla bilgi edinmek için bkz. [Go için Azure SDK ile kimlik doğrulama](azure-sdk-go-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="51db5-206">To learn more about the available authentication methods in the SDK, and which authentication types they support, see [Authentication with the Azure SDK for Go](azure-sdk-go-authorization.md).</span></span>
