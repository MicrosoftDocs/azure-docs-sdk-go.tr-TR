---
title: Go’dan bir Azure sanal makinesini dağıtma
description: Go için Azure SDK’yı kullanarak bir sanal makineyi dağıtın.
author: sptramer
ms.author: sttramer
ms.date: 04/03/2018
ms.topic: quickstart
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 565580e9e6c6ced543bd00bbaa01383834d9a41c
ms.sourcegitcommit: 2b2884ea7673c95ba45b3d6eec647200e75bfc5b
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/19/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a>Hızlı başlangıç: Go için Azure SDK ile bir şablondan Azure sanal makinesi dağıtma

Bu hızlı başlangıç, Go için Azure SDK ile bir şablondan kaynakları dağıtmaya odaklanır. Şablonlar, [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) içinde bulunan tüm kaynakların anlık görüntüleridir. İlerledikçe, kullanışlı bir görevi gerçekleştirirken SDK’nın işlevlerini ve kurallarını öğreneceksiniz.

Bu hızlı başlangıcın sonunda, bir kullanıcı adı ve parola ile oturum açtığınız çalışan bir sanal makineniz olacaktır.

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

Azure CLI’nın yerel bir yüklemesini kullanıyorsanız bu hızlı başlangıç, __2.0.28__ veya sonraki CLI sürümlerini gerektirir. CLI yüklemenizin bu gereksinimi karşıladığından emin olmak için `az --version` çalıştırın. Yükleme veya yükseltme yapmanız gerekirse [Azure CLI 2.0’ı yükleyin](/cli/azure/install-azure-cli).

## <a name="install-the-azure-sdk-for-go"></a>Go için Azure SDK’yı yükleme 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma


Bir uygulamada etkileşimli olmadan oturum açmak için hizmet sorumlusu gerekir. Hizmet sorumluları, benzersiz bir kullanıcı kimliği oluşturan rol tabanlı erişim denetiminin (RBAC) parçasıdır. CLI ile yeni bir hizmet sorumlusu oluşturmak için aşağıdaki komutu çalıştırın:

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart --sdk-auth > quickstart.auth
```

`AZURE_AUTH_LOCATION` ortam değişkenini bu dosyaya giden tam yol olacak şekilde ayarlayın. Daha sonra hizmet sorumlusundan herhangi bir değişiklik yapmanıza veya bilgi kaydetmenize gerek kalmadan SDK kimlik bilgilerini bulur ve doğrudan bu dosyadan okur.

## <a name="get-the-code"></a>Kodu alma

`go get` ile hızlı başlangıç kodunu ve tüm bağımlılıklarını edinin.

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm/...
```

`AZURE_AUTH_LOCATION` değişkeni düzgün şekilde ayarlanmışsa kaynak kodunda herhangi bir değişiklik yapmanız gerekmez. Program çalıştığında, gerekli olan tüm kimlik doğrulama bilgilerini buradan yükler.

## <a name="running-the-code"></a>Kodu çalıştırma

`go run` komutu ile hızlı başlangıcı çalıştırın.

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm
go run main.go
```

Dağıtımda bir hata varsa bir sorun olduğunu belirten ancak yeterli ayrıntıları içermemiş olabilen bir ileti alırsınız. Azure CLI’yı kullanarak aşağıdaki komut ile dağıtım hatasının tam ayrıntılarını alın:

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

### <a name="variables-constants-and-types"></a>Değişkenler, sabitler ve türler

Hızlı başlangıç kendi içinde olduğundan, genel sabitleri ve değişkenleri kullanır.

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

Oluşturulan kaynakların adlarını veren değerler bildirilir. Burada konum da belirtilir; dağıtımların diğer veri merkezlerinde nasıl davrandığını görmek için konumu değiştirebilirsiniz. Her veri merkezinde tüm gerekli kaynaklar mevcut değildir.

`clientInfo` türü, SDK’da istemcileri ve VM parolasını ayarlamak üzere kimlik doğrulama dosyasından bağımsız olarak yüklenmesi gereken bilgileri kapsayacak şekilde bildirilmiştir.

`templateFile` ve `parametersFile` sabitleri, dağıtım için gerekli dosyaları işaret eder. `authorizer` değişkeni kimlik doğrulaması için Go SDK’sı tarafından yapılandırılır ve `ctx` değişkeni ise ağ işlemleri için bir [Go bağlamıdır](https://blog.golang.org/context).

### <a name="authentication-and-initialization"></a>Kimlik doğrulama ve başlatma

`init` işlevi kimlik doğrulamayı ayarlar. Yetkilendirme, hızlı başlangıçtaki her şey için önkoşul olduğundan, başlatmanın parçası olması mantıklıdır. Ayrıca istemcileri ve VM’yi yapılandırmak için kimlik doğrulama dosyasından gerekli olan bazı bilgileri yükler.

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

İlk olarak, `AZURE_AUTH_LOCATION` konumunda bulunan dosyadan kimlik doğrulama bilgilerini yüklemek için [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) çağrılır. Ardından dosya `readJSON` işlevi tarafından el ile yüklenerek (burada göz ardı edilir), programın geri kalanını çalıştırmak için gereken iki değerin çekilmesi sağlanır: İstemcinin abonelik kimliği ve VM’nin parolası için de kullanılan hizmet sorumlusunun gizli dizisi.

> [!WARNING]
> Hızlı başlangıcı basit tutmak için hizmet sorumlusu parolası yeniden kullanılır. Üretimdeyken Azure kaynaklarınıza erişim sağlayan bir parolayı __asla__ yeniden kullanmamaya dikkat edin.

### <a name="flow-of-operations-in-main"></a>main() içindeki işlem akışı

`main` işlevi basittir, yalnızca işlem akışını belirtir ve hata denetimi gerçekleştirir.

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

Kodun çalıştırılma adımları sırayla şöyledir:

* (`createGroup`) hedefine dağıtılacak kaynak grubunu oluşturma
* Bu grup (`createDeployment`) içinde dağıtımı oluşturma
* Dağıtılan VM (`getLogin`) için oturum açma bilgilerini alma ve görüntüleme

### <a name="creating-the-resource-group"></a>Kaynak grubunu oluşturma

`createGroup` işlevi, kaynak grubunu oluşturur. Çağrı akışına ve bağımsız değişkenlere bakılarak, SDK’da hizmet etkileşimlerinin yapılandırılma şekli görülebilir.

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

Bir Azure hizmetiyle etkileşim kurmanın genel akışı şöyledir:

* `service.New*Client()` yöntemini kullanarak istemciyi oluşturun; burada `*`, etkileşim kurmak istediğiniz `service` öğesinin kaynak türüdür. Bu işlev her zaman bir abonelik kimliği alır.
* İstemci için yetkilendirme yöntemini ayarlayarak istemcinin uzak API ile etkileşim kurmasını sağlayın.
* Yöntem çağrısını uzak API’ye karşılık gelen istemcide yapın. Hizmet istemcisi yöntemleri genellikle kaynağın adını ve bir meta veri nesnesini alır.

[`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) işlevi burada bir tür dönüştürmesi gerçekleştirmek için kullanılır. SDK’nın yöntemleri için parametre yapıları hemen her zaman işaretçiler aldığından, bu yöntemler tür dönüştürmelerini kolaylaştırmak için sağlanır. Kolaylık dönüştürücülerinin tam listesi ve davranışları için [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) modülüne ilişkin belgelere bakın.

`groupsClient.CreateOrUpdate` yöntemi, kaynak grubunu temsil eden bir veri türüne işaretçiyi döndürür. Bu tür bir doğrudan dönüş değeri, zaman uyumlu olacak şekilde tasarlanmış kısa süreli bir işlemi belirtir. Sonraki bölümde, uzun süreli bir işlem örneğini ve bunlarla nasıl etkileşim kurulacağını göreceksiniz.

### <a name="performing-the-deployment"></a>Dağıtımı gerçekleştirme

Kaynak grubu oluşturulduktan sonra sıra dağıtımı çalıştırmaya gelir. Bu kod, mantığının farklı kısımlarını vurgulamak için daha küçük bölümlere ayrılmıştır.

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

Dağıtım dosyaları `readJSON` tarafından yüklenir; bunun ayrıntıları burada atlanmıştır. Bu işlev, kaynak dağıtım çağrısı için meta verilerin oluşturulmasında kullanılan `*map[string]interface{}` türünü döndürür. VM’nin parolası ayrıca dağıtım parametrelerinde el ile ayarlanmıştır.

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

Bu kod, kaynak grubunun oluşturulmasıyla aynı deseni izler. Azure kimlik doğrulaması sayesinde yeni bir istemci oluşturulur ve sonra bir yöntem çağrılır. Yöntemin adı (`CreateOrUpdate`) bile kaynak grupları için karşılık gelen yöntemin adıyla aynıdır. Bu desen SDK boyunca görülür. Benzer işi gerçekleştiren yöntemler normalde aynı ada sahiptir.

En büyük fark, `deploymentsClient.CreateOrUpdate` yönteminin dönüş değerindedir. Bu değer, [vadeli işlem tasarım desenini](https://en.wikipedia.org/wiki/Futures_and_promises) izleyen bir [Vadeli işlem](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future) türüdür. Vadeli işlemler, tamamlanması üzerine yoklama yapabileceğiniz, iptal edeceğiniz veya engelleyebileceğiniz Azure’daki uzun süreli bir işlemi temsil eder.

```go
        //...
    err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
    if err != nil {
        return
    }
    deployment, err = deploymentFuture.Result(deploymentsClient)

    // Work around possible bugs or late-stage failures
    if deployment.Name == nil || err != nil {
        deployment, _ = deploymentsClient.Get(ctx, resourceGroupName, deploymentName)
    }
    return
```

Bu örnek için yapılacak en iyi şey, işlemin tamamlanmasını beklemektir. Vadeli işlemin beklenmesi için hem bir [bağlam nesnesi](https://blog.golang.org/context) hem de `Future` nesnesini oluşturan istemci gerekir. Burada iki olası hata kaynağı vardır: Yöntem çağrılmaya çalışılırken istemci tarafında bir hataya yol açılmıştır ve sunucudan bir hata yanıtı alınmıştır. İkinci durum, `deploymentFuture.Result` çağrısının parçası olarak döndürülür.

Dağıtım bilgileri alındıktan sonra, verilerin doldurulduğundan emin olmak için `deploymentsClient.Get` işlevine yönelik el ile bir çağrıyla dağıtım bilgilerinin boş olduğu olası hatalar için geçici bir çözüm bulunur.

### <a name="obtaining-the-assigned-ip-address"></a>Atanan IP adresini alma

Yeni oluşturulan VM ile herhangi bir şey yapmak için atanan IP adresi gerekir. IP adresleri, Ağ Arabirim Denetleyicisi (NIC) kaynaklarına bağlı olan kendi ayrı Azure kaynaklarıdır.

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

Bu yöntem, parametreler dosyasında depolanan bilgileri kullanır. Bu kod, NIC’sini almak için doğrudan VM’yi sorgulayabilir, IP kaynağını almak için NIC’yi sorgulayabilir ve sonra doğrudan IP kaynağını sorgulayabilir. Çözümlenecek uzun bir bağımlılıklar ve işlemler zincirinin olması, bunu pahalı kılar. JSON bilgileri yerel olduğundan, bunun yerine yüklenebilir.

VM kullanıcısının değeri de ayrıca JSON’dan yüklenir. VM parolası, kimlik doğrulama dosyasından önceden yüklendi.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta, mevcut bir şablonu alıp Go aracılığıyla dağıttınız. Sonra, çalıştığından emin olmak için yeni oluşturulan sanal makineye SSH aracılığıyla bağlandınız.

Go ile Azure ortamında sanal makinelerle çalışma hakkında bilgi edinmeye devam etmek için [Go için Azure bilgi işlem örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) veya [Go için Azure kaynak yönetimi örnekleri](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources) bölümüne bakın.

SDK’daki kullanılabilir kimlik doğrulama yöntemleri ve destekledikleri kimlik doğrulama türleri hakkında daha fazla bilgi edinmek için bkz. [Go için Azure SDK ile kimlik doğrulama](azure-sdk-go-authorization.md).
