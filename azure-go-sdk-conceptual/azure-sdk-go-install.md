---
title: "Go için Azure SDK’yı yükleme"
description: "Go için Azure SDK’yı yükleme, satıcı dizinine taşıma ve yapılandırma."
keywords: azure, sdk, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 7fc0a3ff71b0b06f616ae43cff311352fe873345
ms.sourcegitcommit: 890f5f01a70e7e376e6bb98a2030afbfc016f538
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2018
---
# <a name="installing-the-azure-sdk-for-go"></a>Go için Azure SDK’yı yükleme

Go için Azure SDK’ya hoş geldiniz! Bu SDK, Go uygulamalarınızdan Azure hizmetlerini yönetmenize ve bu hizmetlerle etkileşim kurmanıza olanak sağlar.

## <a name="get-the-azure-sdk-for-go"></a>Go için Azure SDK’yı edinin

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

Azure Depolama Blobları ile çalışmak için ayrı bir SDK gerekir.

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a>Go için Azure SDK’yı satıcı dizinine taşıma

Go için Azure SDK, [dep](https://github.com/golang/dep) üzerinden satıcı dizinine taşınabilir. Kararlılık nedeniyle satıcı dizinine taşınması önerilir. `dep` desteğini kullanmak amacıyla `Gopkg.toml` için `[[constraint]]` bölümüne `github.com/Azure/azure-sdk-for-go` ekleyin. Örneğin, `14.0.0` sürümünde satıcı dizinine taşımak için şu girişi ekleyin:

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a>Projenize Go için Azure SDK’yı dahil etme

Go kodunuzdan Azure hizmetlerini kullanmak için, etkileşim kurduğunuz hizmetleri ve gerekli `autorest` modüllerini içeri aktarın.
[AutoRest paketleri](https://godoc.org/github.com/Azure/go-autorest) ve [kullanılabilir hizmetler](https://godoc.org/github.com/Azure/azure-sdk-for-go) için GoDoc’tan kullanılabilir modüllerin tam listesini alın. `go-autorest` içinde ihtiyaç duyduğunuz en yaygın paketler:

| Paket | Açıklama |
|---------|-------------|
| [github.com/Azure/go-autorest/autorest][autorest] | Hizmet istemcisi kimlik doğrulamasını işlemek için nesneler |
| [github.com/Azure/go-autorest/autorest/azure][autorest/azure] | Azure hizmetleri ile etkileşim için sabitler |
| [github.com/Azure/go-autorest/autorest/adal][autorest/adal] | Azure hizmetlerine erişmek için kimlik doğrulaması mekanizmaları |
| [github.com/Azure/go-autorest/autorest/to][autorest/to] | Azure SDK veri yapıları ile çalışmaya ilişkin tür onaylama yardımcıları |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

Azure hizmetlerine ilişkin modüllerin, kendi SDK API’lerinden bağımsız olarak sürümü oluşturulur. Bu sürümler, modül içeri aktarma yolunun parçasıdır ve bir _hizmet sürümünden_ veya bir _profilden_ gelir. Şu anda geliştirme ve yayınlama için belirli bir hizmet sürümünü kullanmanız önerilir. Hizmetler, `services` modülünün altında bulunur. İçeri aktarmanın tam yolu, hizmetin adını takip eden `YYYY-MM-DD` biçiminde sürüm ve tekrar hizmet adından oluşur. Örneğin, İşlem hizmetinin `2017-03-30` sürümünü dahil etmek için:

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

Şu anda, aksini yapmak için bir nedeniniz yoksa, bir hizmetin en son sürümünü kullanmanız önerilir.

Hizmetlerin toplu bir anlık görüntüsüne ihtiyacınız varsa tek bir profil sürümünü de seçebilirsiniz. Şu anda tek kilitli profil olan `2017-03-30` sürümü, hizmetin en son özelliklerini içermeyebilir. Profiller, `profiles` modülünün altında bulunur ve sürümü `YYYY-MM-DD` biçimindedir. Hizmetler, kendi profil sürümleri altında gruplanır. Örneğin, `2017-03-09` profilinden Azure Kaynakları yönetim modülünü içeri aktarmak için:

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> `preview` ve `latest` profilleri de kullanılabilir. Bunların kullanılması önerilmez. Bu profiller, sıralı sürümlerdir ve hizmet davranışı herhangi bir anda değişebilir.

## <a name="next-steps"></a>Sonraki adımlar

Go için Azure SDK’yı kullanmaya başlamak için hızlı başlangıcı deneyin.

* [Bir şablondan sanal makineyi dağıtma](azure-sdk-go-qs-vm.md)
* [Go için Azure Blob SDK ile nesneleri Azure Blob Depolama’ya aktarma](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [PostgreSQL için Azure Veritabanı’na bağlanma](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

Go SDK’daki diğer hizmetleri hemen kullanmaya başlamak isterseniz kullanılabilir örnek kodlardan bazılarına göz atın.

* [Azure hizmetleri ile kimlik doğrulaması](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [SSH kimlik doğrulaması ile yeni sanal makineleri dağıtma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [Azure Container Instances’a kapsayıcı görüntüsü dağıtma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [Azure Kubernetes Hizmeti’nde küme oluşturma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [Azure Depolama hizmetleri ile çalışma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [Go için Azure SDK’ya ilişkin tüm örnekler](https://github.com/azure-samples/azure-sdk-for-go-samples)