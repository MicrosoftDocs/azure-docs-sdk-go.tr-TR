---
title: Go için Azure SDK’yı yükleme
description: Go için Azure SDK’yı yükleme, satıcı dizinine taşıma ve yapılandırma.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 03/14/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 2799e3a6c637036eeaf7b20adf8aa55a8a4ab400
ms.sourcegitcommit: 4db332f5e43a5b43032ff9017805d5fd5a650d86
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2019
ms.locfileid: "55145541"
---
# <a name="install-the-azure-sdk-for-go"></a>Go için Azure SDK’yı yükleme

Go için Azure SDK’ya hoş geldiniz! Bu SDK, Go uygulamalarınızdan Azure hizmetlerini yönetmenize ve bu hizmetlerle etkileşim kurmanıza olanak sağlar.

## <a name="get-the-azure-sdk-for-go"></a>Go için Azure SDK’yı edinin

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

Bazı Azure hizmetlerinin kendi Go SDK’sı bulunur ve bu hizmetler Go için Azure SDK’sı çekirdek paketinde yer almaz. Aşağıdaki tabloda kendi SDK’larına ve paket adlarına sahip hizmetler listelenir. Bu paketlerinin tamamının önizlemede olduğu kabul edilir.

| Hizmet | Paket |
|---------|---------|
| Blob Depolama | [github.com/Azure/azure-storage-blob-go](https://github.com/Azure/azure-storage-blob-go) |
| Dosya Depolama | [github.com/Azure/azure-storage-file-go](https://github.com/Azure/azure-storage-file-go) |
| Depolama Kuyruğu | [github.com/Azure/azure-storage-queue-go](https://github.com/Azure/azure-storage-queue-go) |
| Olay Hub'ı | [github.com/Azure/azure-event-hubs-go](https://github.com/Azure/azure-event-hubs-go) |
| Service Bus | [github.com/Azure/azure-service-bus-go](https://github.com/Azure/azure-service-bus-go) |
| Application Insights | [github.com/Microsoft/ApplicationInsights-go](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a>Go için Azure SDK’yı satıcı dizinine taşıma

Go için Azure SDK, [dep](https://github.com/golang/dep) üzerinden satıcı dizinine taşınabilir. Kararlılık nedeniyle satıcı dizinine taşınması önerilir. Projenizde `dep` kullanmak için `github.com/Azure/azure-sdk-for-go` nesnesini `Gopkg.toml` öğenizdeki `[[constraint]]` bölümlerinden birine ekleyin. Örneğin, `14.0.0` sürümünde satıcı dizinine taşımak için şu girişi ekleyin:

```toml
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a>Projenize Go için Azure SDK’yı dahil etme

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

Go paketlerinin ve Azure hizmetlerinin sürümleri ayrı tutulur. Hizmet sürümleri `services` modülünün altında bulunan modül içeri aktarma yolunun bir parçasıdır. Modülün tam yolu, hizmetin adını takip eden `YYYY-MM-DD` biçiminde sürüm ve tekrar hizmet adından oluşur. Örneğin, İşlem hizmetinin `2017-03-30` sürümünü içeri aktarmak için:

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

Geliştirmeye başlarken hizmetin son sürümünü kullanmanız ve tutarlılık sağlamanız önerilir.
Sürümler arasında ortaya çıkan hizmet gereksinimi değişiklikleri Go SDK güncelleştirmesi olmasa da kodunuzda hataya neden olabilir.

Hizmetlerin toplu bir anlık görüntüsüne ihtiyacınız varsa tek bir profil sürümünü de seçebilirsiniz. Şu anda tek kilitli profil olan `2017-03-09` sürümü, hizmetin en son özelliklerini içermeyebilir. Profiller, `profiles` modülünün altında bulunur ve sürümü `YYYY-MM-DD` biçimindedir. Hizmetler, kendi profil sürümleri altında gruplanır. Örneğin, `2017-03-09` profilinden Azure Kaynakları yönetim modülünü içeri aktarmak için:

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

* [Azure hizmetleri ile kimlik doğrulaması](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/internal/iam)
* [SSH kimlik doğrulaması ile yeni sanal makineleri dağıtma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [Azure Container Instances’a kapsayıcı görüntüsü dağıtma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [Azure Kubernetes Hizmeti’nde küme oluşturma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute)
* [Azure Depolama hizmetleri ile çalışma](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [Go için Azure SDK’ya ilişkin tüm örnekler](https://github.com/azure-samples/azure-sdk-for-go-samples)
