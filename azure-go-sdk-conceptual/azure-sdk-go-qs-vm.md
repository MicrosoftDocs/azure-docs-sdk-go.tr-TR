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
ms.openlocfilehash: e530d944deca40e9e6c29b6c2768e2367822714e
ms.sourcegitcommit: aaa8c37880332625f858a38f5918e6cf581bf48d
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/15/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a>Hızlı başlangıç: Go için Azure SDK ile bir şablondan Azure sanal makinesi dağıtma

Bu hızlı başlangıç, Go için Azure SDK ile bir şablondan kaynakları dağıtmaya odaklanır. Şablonlar, [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) içinde bulunan tüm kaynakların anlık görüntüleridir. İlerledikçe, kullanışlı bir görevi gerçekleştirirken SDK’nın işlevlerini ve kurallarını öğreneceksiniz.

Bu hızlı başlangıcın sonunda, bir kullanıcı adı ve parola ile oturum açtığınız çalışan bir sanal makineniz olacaktır.

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

Azure CLI’nın yerel bir yüklemesini kullanıyorsanız bu hızlı başlangıç, 2.0.24 veya sonraki sürümleri gerektirir. CLI yüklemenizin bu gereksinimi karşıladığından emin olmak için `az --version` çalıştırın. Yükleme veya yükseltme yapmanız gerekirse [Azure CLI 2.0’ı yükleyin](/cli/azure/install-azure-cli).

## <a name="install-the-azure-sdk-for-go"></a>Go için Azure SDK’yı yükleme 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma

Bir uygulamada etkileşimli olmadan oturum açmak için hizmet sorumlusu gerekir. Hizmet sorumluları, benzersiz bir kullanıcı kimliği oluşturan Rol Tabanlı Kimlik Doğrulaması’nın (RBAC) parçasıdır. CLI ile yeni bir hizmet sorumlusu oluşturmak için aşağıdaki komutu çalıştırın:

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

Çıkıştaki `appId`, `password` ve `tenant` değerlerini kaydettiğinizden __emin olun__. Bu değerler uygulama tarafından Azure kimlik doğrulaması yapmak için kullanılır.

Azure CLI 2.0 ile Hizmet Sorumluları oluşturma ve bunları yönetme hakkında daha fazla bilgi için bkz. [Azure CLI 2.0 ile Azure hizmet sorumlusu oluşturma](/cli/azure/create-an-azure-service-principal-azure-cli).

## <a name="get-the-code"></a>Kodu alma

`go get` ile hızlı başlangıç kodunu ve tüm bağımlılıklarını edinin.

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

Bu kod derlenir, ancak siz Azure hesabınızla ve oluşturulan hizmet sorumlusuyla ilgili bilgileri sağlayıncaya kadar düzgün çalışmaz. `main.go` içinde, bir `authInfo` yapısı içeren `config` değişkeni vardır. Bu yapının düzgün şekilde kimlik doğrulaması yapması için alan değerlerinin değiştirilmesi gerekir.

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* `SubscriptionID`: CLI komutundan alınabilen abonelik kimliğiniz

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* `TenantID`: Hizmet sorumlusu oluşturulurken kaydedilen `tenant` değeri olan kiracı kimliğiniz
* `ServicePrincipalID`: Hizmet sorumlusu oluşturulurken kaydedilen `appId` değeri
* `ServicePrincipalSecret`: Hizmet sorumlusu oluşturulurken kaydedilen `password` değeri

`vm-quickstart-params.json` dosyasındaki bir değeri de düzenlemeniz gerekir.

```json
    "vm_password": {
        "value": "_"
    }
```

* `vm_password`: VM kullanıcı hesabı için parola. 6-72 karakter uzunluğunda olmalı ve şu karakterlerden üçünü içermelidir:
  * Bir küçük harf
  * Bir büyük harf
  * Bir rakam
  * Bir sembol

## <a name="running-the-code"></a>Kodu çalıştırma

`go run` komutu ile hızlı başlangıcı çalıştırın.

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

Dağıtımda bir hata varsa bir sorun olduğunu belirten ancak özel ayrıntıları içermeyen bir ileti alırsınız. Azure CLI’yı kullanarak aşağıdaki komut ile dağıtım hatasının ayrıntılarını alın:

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

Dağıtım başarılı olursa yeni oluşturulan sanal makinede oturum açmak için kullanıcı adını, IP adresini ve parolayı sunan bir ileti görürsünüz. Çalışır durumda olduğunu onaylamak için bu makinede SSH işlemi yapın.

## <a name="cleaning-up"></a>Temizleme

CLI ile kaynak grubunu silerek bu hızlı başlangıç sırasında oluşturulan kaynakları temizleyin.

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a>Kod ayrıntıları

Hızlı başlangıç kodunun yaptığı işlem bir değişken öbeğine ve birçok küçük işleve ayrılmış ve her biri burada incelenmiştir.

### <a name="variable-assignments-and-structs"></a>Değişken atamaları ve yapıları

Hızlı başlangıç kendi içinde bulunduğundan, komut satırı seçenekleri veya ortam değişkenleri yerine genel değişkenleri kullanır.

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

Azure hizmetlerinde kimlik doğrulaması yapmak için gerekli tüm bilgileri kapsüllemek için `authInfo` yapısı bildirilir.

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

Oluşturulan kaynakların adlarını veren değerler bildirilir. Burada konum da belirtilir; dağıtımların diğer veri merkezlerinde nasıl davrandığını görmek için konumu değiştirebilirsiniz. Her veri merkezinde tüm gerekli kaynaklar mevcut değildir.

`templateFile` ve `parametersFile` sabitleri, dağıtım için gerekli dosyaları işaret eder. Hizmet sorumlusu belirteci daha sonra ele alınacaktır. `ctx` değişkeni, ağ işlemleri için [Go bağlamıdır](https://blog.golang.org/context).

### <a name="init-and-authorization"></a>init() ve yetkilendirme

Kod için `init()` yöntemi, yetkilendirmeyi ayarlar. Yetkilendirme, hızlı başlangıçtaki her şey için önkoşul olduğundan, başlatmanın parçası olması mantıklıdır. 

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

Bu kod, yetkilendirme için iki adımı tamamlar:

* `TenantID` için OAuth yapılandırma bilgileri, Azure Active Directory ile arabirim oluşturularak alınır. [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) nesnesi, standart Azure yapılandırmasında kullanılan uç noktaları içerir.
* [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken) işlevi çağrılır. Bu işlev, hangi Azure yönetimi stilinin kullanılmakta olduğu bilgisinin yanı sıra, hizmet sorumlusu oturum açma adı ile birlikte OAuth bilgilerini alır. Belirli gereksinimlere sahip değilseniz ve ne yaptığınızı bilmiyorsanız bu değer her zaman `.ResourceManagerEndpoint` olmalıdır.

### <a name="flow-of-operations-in-main"></a>main() içindeki işlem akışı

`main()` işlevi basittir, yalnızca işlem akışını belirtir ve hata denetimi gerçekleştirir.

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

Kodun çalıştırılma adımları sırayla şöyledir:

* (`createGroup()`) hedefine dağıtılacak kaynak grubunu oluşturma
* Bu grup (`createDeployment()`) içinde dağıtımı oluşturma
* Dağıtılan VM (`getLogin()`) için oturum açma bilgilerini alma ve görüntüleme

### <a name="creating-the-resource-group"></a>Kaynak grubunu oluşturma

`createGroup()` işlevi, kaynak grubunu oluşturur. Çağrı akışına ve bağımsız değişkenlere bakılarak, SDK’da hizmet etkileşimlerinin yapılandırılma şekli görülebilir.

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

Bir Azure hizmetiyle etkileşim kurmanın genel akışı şöyledir:

* `service.NewXClient()` yöntemini kullanarak istemciyi oluşturun; burada `X`, etkileşim kurmak istediğiniz `service` öğesinin kaynak türüdür. Bu işlev her zaman bir abonelik kimliği alır.
* İstemci için yetkilendirme yöntemini ayarlayarak istemcinin uzak API ile etkileşim kurmasını sağlayın.
* Yöntem çağrısını uzak API’ye karşılık gelen istemcide yapın. Hizmet istemcisi yöntemleri genellikle kaynağın adını ve bir meta veri nesnesini alır.

[`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) işlevi burada bir tür dönüştürmesi gerçekleştirmek için kullanılır. SDK’nın yöntemleri için parametre yapıları hemen her zaman işaretçiler aldığından, bu yöntemler tür dönüştürmelerini kolaylaştırmak için sağlanır. Kolaylık dönüştürücülerinin tam listesi ve davranışları için [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) modülüne ilişkin belgelere bakın.

`groupsClient.CreateOrUpdate()` işlemi, kaynak grubunu temsil eden bir veri yapısına işaretçiyi döndürür. Bu tür bir doğrudan dönüş değeri, zaman uyumlu olacak şekilde tasarlanmış kısa süreli bir işlemi belirtir. Sonraki bölümde, uzun süreli bir işlem örneğini ve bunlarla nasıl etkileşim kurulacağını göreceksiniz.

### <a name="performing-the-deployment"></a>Dağıtımı gerçekleştirme

Kaynaklarını içerecek grup oluşturulduktan sonra sıra dağıtımı çalıştırmaya gelir. Bu kod, mantığının farklı kısımlarını vurgulamak için daha küçük bölümlere ayrılmıştır.


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

Dağıtım dosyaları `readJSON` tarafından yüklenir; bunun ayrıntıları burada atlanmıştır. Bu işlev, kaynak dağıtım çağrısı için meta verilerin oluşturulmasında kullanılan `*map[string]interface{}` türünü döndürür.

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

Bu kod, kaynak grubunun oluşturulmasıyla aynı deseni izler. Azure kimlik doğrulaması sayesinde yeni bir istemci oluşturulur ve sonra bir yöntem çağrılır. Yöntemin adı (`CreateOrUpdate`) bile kaynak grupları için karşılık gelen yöntemin adıyla aynıdır. Bu desen, SDK’da tekrar tekrar görünür. Benzer işi gerçekleştiren yöntemler normalde aynı ada sahiptir.

En büyük fark, `deploymentsClient.CreateOrUpdate()` yönteminin dönüş değerindedir. Bu değer, [vadeli işlem tasarım desenini](https://en.wikipedia.org/wiki/Futures_and_promises) izleyen bir `Future` nesnesidir. Vadeli işlemler, Azure’da başka iş yaparken ara sıra yoklamak isteyebileceğiniz uzun süreli bir işlemdir.

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

Bu örnek için yapılacak en iyi şey, işlemin tamamlanmasını beklemektir. Vadeli işlemin beklenmesi için hem bir [bağlam nesnesi](https://blog.golang.org/context) hem de Future nesnesini oluşturan istemci gerekir. Burada iki olası hata kaynağı vardır: Yöntem çağrılmaya çalışılırken istemci tarafında bir hataya yol açılmıştır ve sunucudan bir hata yanıtı alınmıştır. İkinci durum, `deploymentFuture.Result()` çağrısının parçası olarak döndürülür.

### <a name="obtaining-the-assigned-ip-address"></a>Atanan IP adresini alma

Yeni oluşturulan VM ile herhangi bir şey yapmak için atanan IP adresi gerekir. IP adresleri, Ağ Arabirim Denetleyicisi (NIC) kaynaklarına bağlı olan kendi ayrı Azure kaynaklarıdır.

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

Bu yöntem, parametreler dosyasında depolanan bilgileri kullanır. Bu kod, NIC’sini almak için doğrudan VM’yi sorgulayabilir, IP kaynağını almak için NIC’yi sorgulayabilir ve sonra doğrudan IP kaynağını sorgulayabilir. Çözümlenecek uzun bir bağımlılıklar ve işlemler zincirinin olması, bunu pahalı kılar. JSON bilgileri yerel olduğundan, bunun yerine yüklenebilir.

VM kullanıcı adı ve parola değerleri de benzer şekilde JSON’dan yüklenir.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta, mevcut bir şablonu alıp Go aracılığıyla dağıttınız. Sonra, çalıştığından emin olmak için yeni oluşturulan sanal makineye SSH aracılığıyla bağlandınız.

Go ile Azure ortamında sanal makinelerle çalışma hakkında bilgi edinmeye devam etmek için [Go için Azure bilgi işlem örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) veya [Go için Azure kaynak yönetimi örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources) bölümüne bakın.
