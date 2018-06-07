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
ms.openlocfilehash: 8423b3fedd89e57662bf96f777a5b30926914da9
ms.sourcegitcommit: b81b17cbb934399c195bfdcb87137aee935f5234
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34755524"
---
# <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="d9741-103">Go için Azure SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="d9741-103">Install the Azure SDK for Go</span></span>

<span data-ttu-id="d9741-104">Go için Azure SDK’ya hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="d9741-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="d9741-105">Bu SDK, Go uygulamalarınızdan Azure hizmetlerini yönetmenize ve bu hizmetlerle etkileşim kurmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9741-105">The SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="d9741-106">Go için Azure SDK’yı edinin</span><span class="sxs-lookup"><span data-stu-id="d9741-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="d9741-107">Bazı Azure hizmetlerinin kendi Go SDK’sı bulunur ve bu hizmetler Go için Azure SDK’sı çekirdek paketinde yer almaz.</span><span class="sxs-lookup"><span data-stu-id="d9741-107">Some Azure services have their own Go SDK and aren't included in the core Azure SDK for Go package.</span></span> <span data-ttu-id="d9741-108">Aşağıdaki tabloda kendi SDK’larına ve paket adlarına sahip hizmetler listelenir.</span><span class="sxs-lookup"><span data-stu-id="d9741-108">The following table lists the services with their own SDKs and their package names.</span></span> <span data-ttu-id="d9741-109">Bu paketlerinin tamamının önizlemede olduğu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-109">These packages are all considered to be in preview.</span></span>

| <span data-ttu-id="d9741-110">Hizmet</span><span class="sxs-lookup"><span data-stu-id="d9741-110">Service</span></span> | <span data-ttu-id="d9741-111">Paket</span><span class="sxs-lookup"><span data-stu-id="d9741-111">Package</span></span> |
|---------|---------|
| <span data-ttu-id="d9741-112">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="d9741-112">Blob Storage</span></span> | [<span data-ttu-id="d9741-113">github.com/Azure/azure-storage-blob-go</span><span class="sxs-lookup"><span data-stu-id="d9741-113">github.com/Azure/azure-storage-blob-go</span></span>](https://github.com/Azure/azure-storage-blob-go) |
| <span data-ttu-id="d9741-114">Dosya Depolama</span><span class="sxs-lookup"><span data-stu-id="d9741-114">File Storage</span></span> | [<span data-ttu-id="d9741-115">github.com/Azure/azure-storage-file-go</span><span class="sxs-lookup"><span data-stu-id="d9741-115">github.com/Azure/azure-storage-file-go</span></span>](https://github.com/Azure/azure-storage-file-go) |
| <span data-ttu-id="d9741-116">Olay Hub'ı</span><span class="sxs-lookup"><span data-stu-id="d9741-116">Event Hub</span></span> | [<span data-ttu-id="d9741-117">github.com/Azure/azure-event-hubs-go</span><span class="sxs-lookup"><span data-stu-id="d9741-117">github.com/Azure/azure-event-hubs-go</span></span>](https://github.com/Azure/azure-event-hubs-go) |
| <span data-ttu-id="d9741-118">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d9741-118">Application Insights</span></span> | [<span data-ttu-id="d9741-119">github.com/Microsoft/ApplicationInsights-go</span><span class="sxs-lookup"><span data-stu-id="d9741-119">github.com/Microsoft/ApplicationInsights-go</span></span>](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a><span data-ttu-id="d9741-120">Go için Azure SDK’yı satıcı dizinine taşıma</span><span class="sxs-lookup"><span data-stu-id="d9741-120">Vendor the Azure SDK for Go</span></span>

<span data-ttu-id="d9741-121">Go için Azure SDK, [dep](https://github.com/golang/dep) üzerinden satıcı dizinine taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-121">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="d9741-122">Kararlılık nedeniyle satıcı dizinine taşınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-122">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="d9741-123">`dep` desteğini kullanmak amacıyla `Gopkg.toml` için `[[constraint]]` bölümüne `github.com/Azure/azure-sdk-for-go` ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d9741-123">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="d9741-124">Örneğin, `14.0.0` sürümünde satıcı dizinine taşımak için şu girişi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d9741-124">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="d9741-125">Projenize Go için Azure SDK’yı dahil etme</span><span class="sxs-lookup"><span data-stu-id="d9741-125">Include the Azure SDK for Go in your project</span></span>

<span data-ttu-id="d9741-126">Go kodunuzdan Azure hizmetlerini kullanmak için, etkileşim kurduğunuz hizmetleri ve gerekli `autorest` modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="d9741-126">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="d9741-127">[AutoRest paketleri](https://godoc.org/github.com/Azure/go-autorest) ve [kullanılabilir hizmetler](https://godoc.org/github.com/Azure/azure-sdk-for-go) için GoDoc’tan kullanılabilir modüllerin tam listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d9741-127">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="d9741-128">`go-autorest` içinde ihtiyaç duyduğunuz en yaygın paketler:</span><span class="sxs-lookup"><span data-stu-id="d9741-128">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="d9741-129">Paket</span><span class="sxs-lookup"><span data-stu-id="d9741-129">Package</span></span> | <span data-ttu-id="d9741-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9741-130">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="d9741-131">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="d9741-131">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="d9741-132">Hizmet istemcisi kimlik doğrulamasını işlemek için nesneler</span><span class="sxs-lookup"><span data-stu-id="d9741-132">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="d9741-133">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="d9741-133">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="d9741-134">Azure hizmetleri ile etkileşim için sabitler</span><span class="sxs-lookup"><span data-stu-id="d9741-134">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="d9741-135">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="d9741-135">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="d9741-136">Azure hizmetlerine erişmek için kimlik doğrulaması mekanizmaları</span><span class="sxs-lookup"><span data-stu-id="d9741-136">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="d9741-137">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="d9741-137">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="d9741-138">Azure SDK veri yapıları ile çalışmaya ilişkin tür onaylama yardımcıları</span><span class="sxs-lookup"><span data-stu-id="d9741-138">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="d9741-139">Azure hizmetlerine ilişkin modüllerin, kendi SDK API’lerinden bağımsız olarak sürümü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d9741-139">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="d9741-140">Bu sürümler, modül içeri aktarma yolunun parçasıdır ve bir _hizmet sürümünden_ veya bir _profilden_ gelir.</span><span class="sxs-lookup"><span data-stu-id="d9741-140">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="d9741-141">Şu anda geliştirme ve yayınlama için belirli bir hizmet sürümünü kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-141">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="d9741-142">Hizmetler, `services` modülünün altında bulunur.</span><span class="sxs-lookup"><span data-stu-id="d9741-142">Services are located under the `services` module.</span></span> <span data-ttu-id="d9741-143">İçeri aktarmanın tam yolu, hizmetin adını takip eden `YYYY-MM-DD` biçiminde sürüm ve tekrar hizmet adından oluşur.</span><span class="sxs-lookup"><span data-stu-id="d9741-143">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="d9741-144">Örneğin, İşlem hizmetinin `2017-03-30` sürümünü dahil etmek için:</span><span class="sxs-lookup"><span data-stu-id="d9741-144">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="d9741-145">Şu anda, aksini yapmak için bir nedeniniz yoksa, bir hizmetin en son sürümünü kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-145">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="d9741-146">Hizmetlerin toplu bir anlık görüntüsüne ihtiyacınız varsa tek bir profil sürümünü de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9741-146">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="d9741-147">Şu anda tek kilitli profil olan `2017-03-09` sürümü, hizmetin en son özelliklerini içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-147">Right now, the only locked profile is version `2017-03-09`, which may not have the latest features of services.</span></span> <span data-ttu-id="d9741-148">Profiller, `profiles` modülünün altında bulunur ve sürümü `YYYY-MM-DD` biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d9741-148">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="d9741-149">Hizmetler, kendi profil sürümleri altında gruplanır.</span><span class="sxs-lookup"><span data-stu-id="d9741-149">Services are grouped under their profile version.</span></span> <span data-ttu-id="d9741-150">Örneğin, `2017-03-09` profilinden Azure Kaynakları yönetim modülünü içeri aktarmak için:</span><span class="sxs-lookup"><span data-stu-id="d9741-150">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="d9741-151">`preview` ve `latest` profilleri de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-151">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="d9741-152">Bunların kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="d9741-152">Using them is not recommended.</span></span> <span data-ttu-id="d9741-153">Bu profiller, sıralı sürümlerdir ve hizmet davranışı herhangi bir anda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="d9741-153">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9741-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9741-154">Next steps</span></span>

<span data-ttu-id="d9741-155">Go için Azure SDK’yı kullanmaya başlamak için hızlı başlangıcı deneyin.</span><span class="sxs-lookup"><span data-stu-id="d9741-155">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="d9741-156">Bir şablondan sanal makineyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="d9741-156">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="d9741-157">Go için Azure Blob SDK ile nesneleri Azure Blob Depolama’ya aktarma</span><span class="sxs-lookup"><span data-stu-id="d9741-157">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="d9741-158">PostgreSQL için Azure Veritabanı’na bağlanma</span><span class="sxs-lookup"><span data-stu-id="d9741-158">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="d9741-159">Go SDK’daki diğer hizmetleri hemen kullanmaya başlamak isterseniz kullanılabilir örnek kodlardan bazılarına göz atın.</span><span class="sxs-lookup"><span data-stu-id="d9741-159">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="d9741-160">Azure hizmetleri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d9741-160">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="d9741-161">SSH kimlik doğrulaması ile yeni sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="d9741-161">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="d9741-162">Azure Container Instances’a kapsayıcı görüntüsü dağıtma</span><span class="sxs-lookup"><span data-stu-id="d9741-162">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="d9741-163">Azure Kubernetes Hizmeti’nde küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9741-163">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="d9741-164">Azure Depolama hizmetleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="d9741-164">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="d9741-165">Go için Azure SDK’ya ilişkin tüm örnekler</span><span class="sxs-lookup"><span data-stu-id="d9741-165">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
