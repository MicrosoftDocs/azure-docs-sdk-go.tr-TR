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
ms.openlocfilehash: 013a771345d96f0fa8dbece3218a01650744f70b
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059195"
---
# <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="c8d7f-103">Go için Azure SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="c8d7f-103">Install the Azure SDK for Go</span></span>

<span data-ttu-id="c8d7f-104">Go için Azure SDK’ya hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="c8d7f-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="c8d7f-105">Bu SDK, Go uygulamalarınızdan Azure hizmetlerini yönetmenize ve bu hizmetlerle etkileşim kurmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-105">The SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="c8d7f-106">Go için Azure SDK’yı edinin</span><span class="sxs-lookup"><span data-stu-id="c8d7f-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="c8d7f-107">Bazı Azure hizmetlerinin kendi Go SDK’sı bulunur ve bu hizmetler Go için Azure SDK’sı çekirdek paketinde yer almaz.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-107">Some Azure services have their own Go SDK and aren't included in the core Azure SDK for Go package.</span></span> <span data-ttu-id="c8d7f-108">Aşağıdaki tabloda kendi SDK’larına ve paket adlarına sahip hizmetler listelenir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-108">The following table lists the services with their own SDKs and their package names.</span></span> <span data-ttu-id="c8d7f-109">Bu paketlerinin tamamının önizlemede olduğu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-109">These packages are all considered to be in preview.</span></span>

| <span data-ttu-id="c8d7f-110">Hizmet</span><span class="sxs-lookup"><span data-stu-id="c8d7f-110">Service</span></span> | <span data-ttu-id="c8d7f-111">Paket</span><span class="sxs-lookup"><span data-stu-id="c8d7f-111">Package</span></span> |
|---------|---------|
| <span data-ttu-id="c8d7f-112">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="c8d7f-112">Blob Storage</span></span> | [<span data-ttu-id="c8d7f-113">github.com/Azure/azure-storage-blob-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-113">github.com/Azure/azure-storage-blob-go</span></span>](https://github.com/Azure/azure-storage-blob-go) |
| <span data-ttu-id="c8d7f-114">Dosya Depolama</span><span class="sxs-lookup"><span data-stu-id="c8d7f-114">File Storage</span></span> | [<span data-ttu-id="c8d7f-115">github.com/Azure/azure-storage-file-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-115">github.com/Azure/azure-storage-file-go</span></span>](https://github.com/Azure/azure-storage-file-go) |
| <span data-ttu-id="c8d7f-116">Depolama Kuyruğu</span><span class="sxs-lookup"><span data-stu-id="c8d7f-116">Storage Queue</span></span> | [<span data-ttu-id="c8d7f-117">github.com/Azure/azure-storage-queue-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-117">github.com/Azure/azure-storage-queue-go</span></span>](https://github.com/Azure/azure-storage-queue-go) |
| <span data-ttu-id="c8d7f-118">Olay Hub'ı</span><span class="sxs-lookup"><span data-stu-id="c8d7f-118">Event Hub</span></span> | [<span data-ttu-id="c8d7f-119">github.com/Azure/azure-event-hubs-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-119">github.com/Azure/azure-event-hubs-go</span></span>](https://github.com/Azure/azure-event-hubs-go) |
| <span data-ttu-id="c8d7f-120">Service Bus</span><span class="sxs-lookup"><span data-stu-id="c8d7f-120">Service Bus</span></span> | [<span data-ttu-id="c8d7f-121">github.com/Azure/azure-service-bus-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-121">github.com/Azure/azure-service-bus-go</span></span>](https://github.com/Azure/azure-service-bus-go) |
| <span data-ttu-id="c8d7f-122">Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8d7f-122">Application Insights</span></span> | [<span data-ttu-id="c8d7f-123">github.com/Microsoft/ApplicationInsights-go</span><span class="sxs-lookup"><span data-stu-id="c8d7f-123">github.com/Microsoft/ApplicationInsights-go</span></span>](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a><span data-ttu-id="c8d7f-124">Go için Azure SDK’yı satıcı dizinine taşıma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-124">Vendor the Azure SDK for Go</span></span>

<span data-ttu-id="c8d7f-125">Go için Azure SDK, [dep](https://github.com/golang/dep) üzerinden satıcı dizinine taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-125">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="c8d7f-126">Kararlılık nedeniyle satıcı dizinine taşınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-126">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="c8d7f-127">Projenizde `dep` kullanmak için `github.com/Azure/azure-sdk-for-go` nesnesini `Gopkg.toml` öğenizdeki `[[constraint]]` bölümlerinden birine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-127">To use `dep` in your own project, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="c8d7f-128">Örneğin, `14.0.0` sürümünde satıcı dizinine taşımak için şu girişi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8d7f-128">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```toml
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="c8d7f-129">Projenize Go için Azure SDK’yı dahil etme</span><span class="sxs-lookup"><span data-stu-id="c8d7f-129">Include the Azure SDK for Go in your project</span></span>

<span data-ttu-id="c8d7f-130">Go kodunuzdan Azure hizmetlerini kullanmak için, etkileşim kurduğunuz hizmetleri ve gerekli `autorest` modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-130">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="c8d7f-131">[AutoRest paketleri](https://godoc.org/github.com/Azure/go-autorest) ve [kullanılabilir hizmetler](https://godoc.org/github.com/Azure/azure-sdk-for-go) için GoDoc’tan kullanılabilir modüllerin tam listesini alın.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-131">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="c8d7f-132">`go-autorest` içinde ihtiyaç duyduğunuz en yaygın paketler:</span><span class="sxs-lookup"><span data-stu-id="c8d7f-132">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="c8d7f-133">Paket</span><span class="sxs-lookup"><span data-stu-id="c8d7f-133">Package</span></span> | <span data-ttu-id="c8d7f-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8d7f-134">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="c8d7f-135">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="c8d7f-135">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="c8d7f-136">Hizmet istemcisi kimlik doğrulamasını işlemek için nesneler</span><span class="sxs-lookup"><span data-stu-id="c8d7f-136">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="c8d7f-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="c8d7f-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="c8d7f-138">Azure hizmetleri ile etkileşim için sabitler</span><span class="sxs-lookup"><span data-stu-id="c8d7f-138">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="c8d7f-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="c8d7f-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="c8d7f-140">Azure hizmetlerine erişmek için kimlik doğrulaması mekanizmaları</span><span class="sxs-lookup"><span data-stu-id="c8d7f-140">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="c8d7f-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="c8d7f-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="c8d7f-142">Azure SDK veri yapıları ile çalışmaya ilişkin tür onaylama yardımcıları</span><span class="sxs-lookup"><span data-stu-id="c8d7f-142">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="c8d7f-143">Go paketlerinin ve Azure hizmetlerinin sürümleri ayrı tutulur.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-143">Go packages and Azure services are versioned independently.</span></span> <span data-ttu-id="c8d7f-144">Hizmet sürümleri `services` modülünün altında bulunan modül içeri aktarma yolunun bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-144">The service versions are part of the module import path, underneath the `services` module.</span></span> <span data-ttu-id="c8d7f-145">Modülün tam yolu, hizmetin adını takip eden `YYYY-MM-DD` biçiminde sürüm ve tekrar hizmet adından oluşur.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-145">The full path for the module is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="c8d7f-146">Örneğin, İşlem hizmetinin `2017-03-30` sürümünü içeri aktarmak için:</span><span class="sxs-lookup"><span data-stu-id="c8d7f-146">For example, to import the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="c8d7f-147">Geliştirmeye başlarken hizmetin son sürümünü kullanmanız ve tutarlılık sağlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-147">It's recommended that you use the latest version of a service when starting development and keep it consistent.</span></span>
<span data-ttu-id="c8d7f-148">Sürümler arasında ortaya çıkan hizmet gereksinimi değişiklikleri Go SDK güncelleştirmesi olmasa da kodunuzda hataya neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-148">Service requirements may change between versions that could break your code, even if there are no Go SDK updates during that time.</span></span>

<span data-ttu-id="c8d7f-149">Hizmetlerin toplu bir anlık görüntüsüne ihtiyacınız varsa tek bir profil sürümünü de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-149">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="c8d7f-150">Şu anda tek kilitli profil olan `2017-03-09` sürümü, hizmetin en son özelliklerini içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-150">Right now, the only locked profile is version `2017-03-09`, which may not have the latest features of services.</span></span> <span data-ttu-id="c8d7f-151">Profiller, `profiles` modülünün altında bulunur ve sürümü `YYYY-MM-DD` biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-151">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="c8d7f-152">Hizmetler, kendi profil sürümleri altında gruplanır.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-152">Services are grouped under their profile version.</span></span> <span data-ttu-id="c8d7f-153">Örneğin, `2017-03-09` profilinden Azure Kaynakları yönetim modülünü içeri aktarmak için:</span><span class="sxs-lookup"><span data-stu-id="c8d7f-153">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="c8d7f-154">`preview` ve `latest` profilleri de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-154">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="c8d7f-155">Bunların kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-155">Using them is not recommended.</span></span> <span data-ttu-id="c8d7f-156">Bu profiller, sıralı sürümlerdir ve hizmet davranışı herhangi bir anda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-156">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8d7f-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8d7f-157">Next steps</span></span>

<span data-ttu-id="c8d7f-158">Go için Azure SDK’yı kullanmaya başlamak için hızlı başlangıcı deneyin.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-158">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="c8d7f-159">Bir şablondan sanal makineyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-159">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="c8d7f-160">Go için Azure Blob SDK ile nesneleri Azure Blob Depolama’ya aktarma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-160">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="c8d7f-161">PostgreSQL için Azure Veritabanı’na bağlanma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-161">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="c8d7f-162">Go SDK’daki diğer hizmetleri hemen kullanmaya başlamak isterseniz kullanılabilir örnek kodlardan bazılarına göz atın.</span><span class="sxs-lookup"><span data-stu-id="c8d7f-162">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="c8d7f-163">Azure hizmetleri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c8d7f-163">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="c8d7f-164">SSH kimlik doğrulaması ile yeni sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-164">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="c8d7f-165">Azure Container Instances’a kapsayıcı görüntüsü dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-165">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="c8d7f-166">Azure Kubernetes Hizmeti’nde küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-166">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="c8d7f-167">Azure Depolama hizmetleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="c8d7f-167">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="c8d7f-168">Go için Azure SDK’ya ilişkin tüm örnekler</span><span class="sxs-lookup"><span data-stu-id="c8d7f-168">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
