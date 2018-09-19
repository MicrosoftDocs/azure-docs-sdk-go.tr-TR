---
title: Go için Azure SDK ile kimlik doğrulaması
description: Go için Azure SDK’da bulabileceğiniz kimlik doğrulama yöntemlerini ve bu yöntemleri nasıl kullanacağınızı öğrenin.
services: azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: conceptual
ms.technology: azure-sdk-go
ms.devlang: go
ms.service: active-directory
ms.component: authentication
ms.openlocfilehash: 28fd4a4c0832ab19dcf52dc549d0ddc0d1eec6f1
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059110"
---
# <a name="authentication-methods-in-the-azure-sdk-for-go"></a>Go için Azure SDK’da kimlik doğrulama yöntemleri

Go için Azure SDK, Azure ile kimlik doğrulama gerçekleştirmek için birden fazla yöntem sunar. Bu kimlik doğrulama _türleri_ farklı kimlik doğrulama _yöntemleriyle_ çağrılır. Bu makalede kullanabileceğiniz tür ve yöntemlerin yanı sıra uygulamanıza en uygun seçeneği belirleme yollarına yer verilmiştir.

## <a name="available-authentication-types-and-methods"></a>Kullanılabilir kimlik doğrulama türleri ve yöntemleri

Go için Azure SDK, farklı kimlik bilgileri kümeleri kullanarak birkaç farklı türde kimlik doğrulaması sunar. Kimlik doğrulama türlerinden her biri, SDK’nın bu kimlik bilgilerini giriş olarak alması gibi, farklı kimlik doğrulama yöntemleri aracılığıyla kullanılabilir. Aşağıdaki tabloda uygulamanız tarafından kullanılması önerilen uygun kimlik doğrulama türleri açıklanmaktadır.

| Kimlik doğrulaması türü | Şunlar olduğunda önerilir... |
|---------------------|---------------------|
| Sertifika tabanlı kimlik doğrulaması | Azure Active Directory (AAD) kullanıcısı veya hizmet sorumlusu için yapılandırılmış bir X509 sertifikasına sahipsiniz. Daha fazla bilgi için bkz. [Azure Active Directory’de sertifika tabanlı kimlik doğrulamayı kullanmaya başlama]. |
| İstemci kimlik bilgileri | Bu uygulamaya veya ait olduğu uygulama sınıfına ayarlı yapılandırılmış bir hizmet sorumlusuna sahipsiniz. Daha fazla bilgi için bkz. [Azure CLI ile hizmet sorumlusu oluşturma]. |
| Yönetilen Hizmet Kimliği (MSI) | Uygulamanız, Yönetilen Hizmet Kimliği (MSI) ile yapılandırılmış bir Azure kaynak üzerinde çalışıyor. Daha fazla bilgi için bkz. [Azure kaynakları için Yönetilen Hizmet Kimliği (MSI)]. |
| Cihaz belirteci | Uygulamanız __yalnızca__ etkileşimli olarak kullanılacak şekilde tasarlanmıştır. Kullanıcılarda çok faktörlü kimlik doğrulaması etkin olabilir. Kullanıcıların oturum açmak için bir web tarayıcısına erişimi olur. Daha fazla bilgi için bkz. [Cihaz belirteci kimlik doğrulaması kullanma](#use-device-token-authentication).|
| Kullanıcı adı/parola | Başka herhangi bir kimlik doğrulama yöntemi kullanamayan etkileşimli bir uygulamaya sahipsiniz. Kullanıcılarınızın çok faktörlü kimlik doğrulaması özelliği AAD oturum açma işlemleri için etkinleştirilmemiş. |

> [!IMPORTANT]
> İstemci kimlik bilgileri dışında bir kimlik doğrulama türü kullanıyorsanız, uygulamanız Azure Active Directory'de kayıtlı olmalıdır. Bunu nasıl yapacağınızı öğrenmek için bkz. [Uygulamaları Azure Active Directory ile tümleştirme](/azure/active-directory/develop/active-directory-integrating-applications).
>
> [!NOTE]
> Özel gereksinimleriniz yoksa, kullanıcı adı/parola kimlik doğrulamasından kaçının. Kullanıcı tabanlı oturum açmanın uygun olduğu durumlarda, genellikle bunun yerine cihaz belirteci kimlik doğrulaması kullanılabilir.

[Azure Active Directory’de sertifika tabanlı kimlik doğrulamayı kullanmaya başlama]: /azure/active-directory/active-directory-certificate-based-authentication-get-started
[Azure CLI ile hizmet sorumlusu oluşturma]: /cli/azure/create-an-azure-service-principal-azure-cli
[Azure kaynakları için Yönetilen Hizmet Kimliği (MSI)]: /azure/active-directory/managed-service-identity/overview

Bu kimlik doğrulama türleri farklı yöntemler üzerinden kullanılabilir.

* [_Ortam tabanlı kimlik doğrulama_](#use-environment-based-authentication) kimlik bilgilerini doğrudan programın ortamından okur.
* [_Dosya tabanlı kimlik doğrulama_](#use-file-based-authentication) hizmet sorumlusu kimlik bilgilerini içeren bir dosya yükler.
* [_İstemci tabanlı kimlik doğrulama_](#use-an-authentication-client), kodda bir nesne kullanır ve program yürütme sırasında sizi kimlik bilgilerini sağlama görevinden sorumlu hale getirir.
* [_Cihaz belirteci kimlik doğrulama_](#use-device-token-authentication), kullanıcının bir web tarayıcısından etkileşimli olarak oturum açmasını gerektirir.

Tüm kimlik doğrulama işlevleri ve türleri `github.com/Azure/go-autorest/autorest/azure/auth` paketinde kullanılabilir.

> [!NOTE]
> Özel gereksinimleriniz yoksa, istemci tabanlı kimlik doğrulamadan kaçının. Bu kimlik doğrulama yöntemi hatalı uygulamalara sevk eder. Özellikle, istemci tabanlı kimlik doğrulama kullanmak kimlik bilgilerini doğrudan yazmayı cazip kılar. Kimlik doğrulama için özel kod yazmak da ayrıca kimlik doğrulama değişiklik gerektirdiğinde gelecek SDK sürümlerinde başarısız olabilir.

## <a name="use-environment-based-authentication"></a>Ortam tabanlı kimlik doğrulama kullanma

Uygulamanızı denetimli bir ortamda çalıştırıyorsanız, ortam tabanlı kimlik doğrulama doğal bir tercihtir. Bu kimlik doğrulama yöntemiyle uygulamanızı çalıştırmadan önce kabuk ortamını yapılandırırsınız. Çalışma zamanında Go SDK'sı bu ortam değişkenlerini okuyarak Azure ile kimlik doğrulama gerçekleştirir.

Ortam tabanlı kimlik doğrulamanın, cihaz belirteçleri hariç şu sırayla değerlendirilmiş tüm kimlik doğrulama yöntemleri için desteği vardır:

* İstemci kimlik bilgileri
* X509 sertifikaları
* Kullanıcı adı/parola
* Yönetilen Hizmet Kimliği (MSI)

Bir kimlik doğrulama türü ayarlanmamış değerlere sahipse veya reddedilirse SDK otomatik olarak bir sonraki kimlik doğrulama türünü dener. Denenecek tür kalmadığında SDK bir hata döndürür.

Aşağıdaki tabloda ortam tabanlı kimlik doğrulama tarafından desteklenen her bir kimlik doğrulama türüne ayarlanması gereken ortam değişkenlerinin ayrıntıları verilmektedir.

| Kimlik doğrulaması türü | Ortam değişkeni | Açıklama |
| ------------------- | -------------------- | ----------- |
| __İstemci kimlik bilgileri__ | `AZURE_TENANT_ID` | Hizmet sorumlusunun ait olduğu Active Directory kiracısının kimliği. |
| | `AZURE_CLIENT_ID` | Hizmet sorumlusunun adı veya kimliği. |
| | `AZURE_CLIENT_SECRET` | Hizmet sorumlusuyla ilişkili gizli dizi. |
| __Sertifika__ | `AZURE_TENANT_ID` | Sertifikanın birlikte kayıtlı olduğu Active Directory kiracısının kimliği. |
| | `AZURE_CLIENT_ID` | Sertifikayla ilişkili uygulama istemci kimliği. |
| | `AZURE_CERTIFICATE_PATH` | İstemci sertifikası dosyası yolu. |
| | `AZURE_CERTIFICATE_PASSWORD` | İstemci sertifikası için parola. |
| __Kullanıcı Adı/Parola__ | `AZURE_TENANT_ID` | Kullanıcının ait olduğu Active Directory kiracısının kimliği. |
| | `AZURE_CLIENT_ID` | Uygulama istemci kimliği. |
| | `AZURE_USERNAME` | Oturum açmada kullanılan kullanıcı adı. |
| | `AZURE_PASSWORD` | Oturum açmada kullanılan parola. |
| __MSI__ | | MSI kimlik doğrulama için kimlik bilgilerine ihtiyaç duyulmaz. Uygulama, MSI kullanmak üzere yapılandırılmış bir Azure kaynağında çalışıyor olmalıdır. Ayrıntılı bilgi için bkz. [Azure kaynakları için Yönetilen Hizmet Kimliği (MSI)]. |

Varsayılan Azure genel bulut dışında başka bir bulut ya da yönetim uç noktasına bağlanmak için aşağıdaki ortam değişkenlerini ayarlayın. En yaygın nedenler, Azure Stack, farklı bir coğrafi bölgede bulut veya klasik dağıtım modeli kullanmaktır.

| Ortam değişkeni | Açıklama  |
|----------------------|--------------|
| `AZURE_ENVIRONMENT` | Bağlanılacak bulut ortamı adı. |
| `AZURE_AD_RESOURCE` | Bağlantı için kullanılacak Active Directory kaynak kimliği, yönetim uç noktanızın URI'si olarak. |

Ortam tabanlı kimlik doğrulaması kullanırken, yetkilendirici nesnenizi almak için [NewAuthorizerFromEnvironment](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromEnvironment) işlevini çağırın. Bu nesne daha sonra Azure’a erişmesine izin vermek için istemcilerin `Authorizer` özelliğinde ayarlanır.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
authorizer, err := auth.NewAuthorizerFromEnvironment()
```

### <a name="authentication-on-azure-stack"></a>Azure Stack’te Kimlik Doğrulaması

Azure Stack’te kimlik doğrulaması yapmak için aşağıdaki değişkenleri ayarlamanız gerekir:

| Ortam değişkeni | Açıklama  |
|----------------------|--------------|
| `AZURE_AD_ENDPOINT` | Active Directory uç noktası. |
| `AZURE_AD_RESOURCE` | Active Directory kaynak kimliği. |

Bu değişkenler Azure Stack meta data verilerinden alınabilir. Meta verileri almak için Azure Stack ortamınızda bir web tarayıcısı açıp şu URL’yi kullanın: `(ResourceManagerURL)/metadata/endpoints?api-version=1.0`

`ResourceManagerURL` Azure Stack dağıtımınızın bölge adı, makine adı ve dış tam etki alanı adına (FQDN) göre değişiklik gösterebilir:

| Ortam | ResourceManagerURL |
|----------------------|--------------|
| Geliştirme Seti | `https://management.local.azurestack.external/` |
| Tümleşik Sistemler | `https://management.(region).ext-(machine-name).(FQDN)` |

Azure Stack üzerinde Go için Azure SDK’sını kullanma hakkında daha fazla bilgi için bkz. [Azure Stack’te GO ile API sürümü profillerini kullanma](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-version-profiles-go)

## <a name="use-file-based-authentication"></a>Dosya tabanlı kimlik doğrulama kullanma

Dosya tabanlı kimlik doğrulama yönteminde [Azure CLI](/cli/azure) tarafından oluşturulan bir dosya biçimi kullanılır. Bu dosyayı `--sdk-auth` parametresiyle yeni bir hizmet sorumlusu oluştururken kolaylıkla oluşturabilirsiniz. Dosya tabanlı kimlik doğrulama kullanmayı planlıyorsanız, hizmet sorumlusu oluştururken bu bağımsız değişkenin sağlandığından emin olun. CLI çıktıyı `stdout` öğesine yazdırdığından, çıktıyı bir dosyaya yeniden yönlendirin.

```azurecli
az ad sp create-for-rbac --sdk-auth > azure.auth
```

`AZURE_AUTH_LOCATION` ortam değişkenini yetkilendirme dosyasının bulunduğu konuma ayarlayın. Ortam değişkeni uygulama tarafından okunur ve içindeki kimlik bilgileriyse ayrıştırılır. Yetkilendirme dosyasını çalışma zamanında seçmeniz gerekiyorsa, [os.Setenv](https://golang.org/pkg/os/#Setenv) işlevini kullanarak programın ortamını işleyin.

Kimlik doğrulama bilgilerini yüklemek için [NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) işlevini çağırın. Ortam tabanlı yetkilendirmeden farklı olarak, dosya tabanlı yetkilendirme bir kaynak uç noktası gerektirir.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
authorizer, err := NewAuthorizerFromFile(azure.PublicCloud.ResourceManagerEndpoint)
```

Hizmet sorumlularını kullanma ve erişim izinlerini yönetmeyle ilgili daha fazla bilgi için bkz. [Azure CLI ile hizmet sorumlusu oluşturma].

## <a name="use-device-token-authentication"></a>Cihaz belirteci kimlik doğrulaması kullanma

Kullanıcıların etkileşimli olarak oturum açmasını istiyorsanız, en iyi yol cihaz belirteci kimlik doğrulamasıdır. Bu kimlik doğrulama akışı, bir Microsoft oturum açma sitesine yapıştırmak üzere kullanıcıya bir belirteç geçirir. Kullanıcı daha sonra bu sitede bir Azure Active Directory (AAD) hesabıyla kimlik doğrulaması yapar. Bu kimlik doğrulama yöntemi, standart kullanıcı adı/parola kimlik doğrulamasının aksine, çok faktörlü kimlik doğrulamasının etkinleştirildiği hesapları destekler.

Cihaz belirteci kimlik doğrulamasını kullanmak için, [NewDeviceFlowConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewDeviceFlowConfig) işleviyle bir [DeviceFlowConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig) yetkilendiricisi oluşturun. Kimlik doğrulama işlemini başlatmak için sonuç nesnesinin üzerinde [Authorizer](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig.Authorizer) işlevini çağırın. Cihaz akışı kimlik doğrulaması, tüm kimlik doğrulama akışı tamamlanana kadar program yürütmesini engeller.

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
deviceConfig := auth.NewDeviceFlowConfig(applicationID, tenantID)
authorizer, err := deviceConfig.Authorizer()
```

## <a name="use-an-authentication-client"></a>Kimlik doğrulama istemcisini kullanma

Belirli bir türde kimlik doğrulama gerekiyorsa ve programınızın kullanıcıdan kimlik doğrulama bilgilerini yükleme işini yapmasını kabul ediyorsanız, [auth.AuthorizerConfig](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#AuthorizerConfig) arabirimiyle uyumlu olan herhangi bir istemciyi kullanabilirsiniz. Aşağıdaki durumlarda bu arabirimi uygulayan bir tür kullanabilirsiniz:

* Etkileşimli program yazma
* Özel yapılandırma dosyaları kullanma
* Yerleşik kimlik doğrulama yöntemini kullanmanızı engelleyen bir gereksinime sahip olma

> [!WARNING]
> Azure kimlik bilgilerini asla bir uygulamaya doğrudan yazmayın. Uygulama ikili dosyasına gizli diziler koymak, uygulama çalışsa da çalışmasa da saldırganın bu gizli dizileri ayıklamasını kolaylaştırır. Bu kimlik bilgilerinin yetkilendirildiği tüm Azure kaynaklarını tehlikeye atar!

Aşağıdaki tabloda SDK’da `AuthorizerConfig` arabirimiyle uyumlu olan türler listelenmiştir.

| Kimlik doğrulaması türü | Yetkilendirici türü |
|---------------------|-----------------------|
| Sertifika tabanlı kimlik doğrulaması | [ClientCertificateConfig] |
| İstemci kimlik bilgileri | [ClientCredentialsConfig] |
| Yönetilen Hizmet Kimliği (MSI) | [MSIConfig] |
| Kullanıcı adı/parola | [UsernamePasswordConfig] |

[ClientCertificateConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#ClientCertificateConfig
[ClientCredentialsConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#ClientCredentialsConfig
[MSIConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#MSIConfig
[DeviceFlowConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#DeviceFlowConfig
[UsernamePasswordConfig]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#UsernamePasswordConfig

İlişkili olduğu `New` işleviyle birlikte bir doğrulayıcı oluşturun ve ardından kimlik doğrulama için sonuç nesnesi üzerinde `Authorize` işlevini çağırın. Örneğin, sertifika tabanlı kimlik doğrulaması kullanmak için:

```go
import "github.com/Azure/go-autorest/autorest/azure/auth"
certificateAuthorizer := auth.NewClientCertificateConfig(certificatePath, certificatePassword, clientID, tenantID)
authorizerToken, err := certificateAuthorizer.Authorize()
```
