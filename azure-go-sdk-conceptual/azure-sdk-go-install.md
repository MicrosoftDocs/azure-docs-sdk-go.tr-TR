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
# <a name="installing-the-azure-sdk-for-go"></a><span data-ttu-id="cdcab-104">Go için Azure SDK’yı yükleme</span><span class="sxs-lookup"><span data-stu-id="cdcab-104">Installing the Azure SDK for Go</span></span>

<span data-ttu-id="cdcab-105">Go için Azure SDK’ya hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="cdcab-105">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="cdcab-106">Bu SDK, Go uygulamalarınızdan Azure hizmetlerini yönetmenize ve bu hizmetlerle etkileşim kurmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdcab-106">This SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="cdcab-107">Go için Azure SDK’yı edinin</span><span class="sxs-lookup"><span data-stu-id="cdcab-107">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="cdcab-108">Azure Depolama Blobları ile çalışmak için ayrı bir SDK gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-108">Working with Azure Storage Blobs requires a separate SDK.</span></span>

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a><span data-ttu-id="cdcab-109">Go için Azure SDK’yı satıcı dizinine taşıma</span><span class="sxs-lookup"><span data-stu-id="cdcab-109">Vendoring the Azure SDK for Go</span></span>

<span data-ttu-id="cdcab-110">Go için Azure SDK, [dep](https://github.com/golang/dep) üzerinden satıcı dizinine taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-110">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="cdcab-111">Kararlılık nedeniyle satıcı dizinine taşınması önerilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-111">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="cdcab-112">`dep` desteğini kullanmak amacıyla `Gopkg.toml` için `[[constraint]]` bölümüne `github.com/Azure/azure-sdk-for-go` ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdcab-112">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="cdcab-113">Örneğin, `14.0.0` sürümünde satıcı dizinine taşımak için şu girişi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cdcab-113">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="cdcab-114">Projenize Go için Azure SDK’yı dahil etme</span><span class="sxs-lookup"><span data-stu-id="cdcab-114">Including the Azure SDK for Go in your project</span></span>

<span data-ttu-id="cdcab-115">Go kodunuzdan Azure hizmetlerini kullanmak için, etkileşim kurduğunuz hizmetleri ve gerekli `autorest` modüllerini içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="cdcab-115">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="cdcab-116">[AutoRest paketleri](https://godoc.org/github.com/Azure/go-autorest) ve [kullanılabilir hizmetler](https://godoc.org/github.com/Azure/azure-sdk-for-go) için GoDoc’tan kullanılabilir modüllerin tam listesini alın.</span><span class="sxs-lookup"><span data-stu-id="cdcab-116">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="cdcab-117">`go-autorest` içinde ihtiyaç duyduğunuz en yaygın paketler:</span><span class="sxs-lookup"><span data-stu-id="cdcab-117">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="cdcab-118">Paket</span><span class="sxs-lookup"><span data-stu-id="cdcab-118">Package</span></span> | <span data-ttu-id="cdcab-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cdcab-119">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="cdcab-120">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="cdcab-120">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="cdcab-121">Hizmet istemcisi kimlik doğrulamasını işlemek için nesneler</span><span class="sxs-lookup"><span data-stu-id="cdcab-121">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="cdcab-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="cdcab-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="cdcab-123">Azure hizmetleri ile etkileşim için sabitler</span><span class="sxs-lookup"><span data-stu-id="cdcab-123">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="cdcab-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="cdcab-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="cdcab-125">Azure hizmetlerine erişmek için kimlik doğrulaması mekanizmaları</span><span class="sxs-lookup"><span data-stu-id="cdcab-125">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="cdcab-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="cdcab-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="cdcab-127">Azure SDK veri yapıları ile çalışmaya ilişkin tür onaylama yardımcıları</span><span class="sxs-lookup"><span data-stu-id="cdcab-127">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="cdcab-128">Azure hizmetlerine ilişkin modüllerin, kendi SDK API’lerinden bağımsız olarak sürümü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cdcab-128">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="cdcab-129">Bu sürümler, modül içeri aktarma yolunun parçasıdır ve bir _hizmet sürümünden_ veya bir _profilden_ gelir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-129">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="cdcab-130">Şu anda geliştirme ve yayınlama için belirli bir hizmet sürümünü kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-130">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="cdcab-131">Hizmetler, `services` modülünün altında bulunur.</span><span class="sxs-lookup"><span data-stu-id="cdcab-131">Services are located under the `services` module.</span></span> <span data-ttu-id="cdcab-132">İçeri aktarmanın tam yolu, hizmetin adını takip eden `YYYY-MM-DD` biçiminde sürüm ve tekrar hizmet adından oluşur.</span><span class="sxs-lookup"><span data-stu-id="cdcab-132">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="cdcab-133">Örneğin, İşlem hizmetinin `2017-03-30` sürümünü dahil etmek için:</span><span class="sxs-lookup"><span data-stu-id="cdcab-133">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="cdcab-134">Şu anda, aksini yapmak için bir nedeniniz yoksa, bir hizmetin en son sürümünü kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-134">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="cdcab-135">Hizmetlerin toplu bir anlık görüntüsüne ihtiyacınız varsa tek bir profil sürümünü de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdcab-135">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="cdcab-136">Şu anda tek kilitli profil olan `2017-03-30` sürümü, hizmetin en son özelliklerini içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-136">Right now, the only locked profile is version `2017-03-30`, which may not have the latest features of services.</span></span> <span data-ttu-id="cdcab-137">Profiller, `profiles` modülünün altında bulunur ve sürümü `YYYY-MM-DD` biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-137">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="cdcab-138">Hizmetler, kendi profil sürümleri altında gruplanır.</span><span class="sxs-lookup"><span data-stu-id="cdcab-138">Services are grouped under their profile version.</span></span> <span data-ttu-id="cdcab-139">Örneğin, `2017-03-09` profilinden Azure Kaynakları yönetim modülünü içeri aktarmak için:</span><span class="sxs-lookup"><span data-stu-id="cdcab-139">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="cdcab-140">`preview` ve `latest` profilleri de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-140">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="cdcab-141">Bunların kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="cdcab-141">Using them is not recommended.</span></span> <span data-ttu-id="cdcab-142">Bu profiller, sıralı sürümlerdir ve hizmet davranışı herhangi bir anda değişebilir.</span><span class="sxs-lookup"><span data-stu-id="cdcab-142">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdcab-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdcab-143">Next steps</span></span>

<span data-ttu-id="cdcab-144">Go için Azure SDK’yı kullanmaya başlamak için hızlı başlangıcı deneyin.</span><span class="sxs-lookup"><span data-stu-id="cdcab-144">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="cdcab-145">Bir şablondan sanal makineyi dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdcab-145">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="cdcab-146">Go için Azure Blob SDK ile nesneleri Azure Blob Depolama’ya aktarma</span><span class="sxs-lookup"><span data-stu-id="cdcab-146">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="cdcab-147">PostgreSQL için Azure Veritabanı’na bağlanma</span><span class="sxs-lookup"><span data-stu-id="cdcab-147">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="cdcab-148">Go SDK’daki diğer hizmetleri hemen kullanmaya başlamak isterseniz kullanılabilir örnek kodlardan bazılarına göz atın.</span><span class="sxs-lookup"><span data-stu-id="cdcab-148">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="cdcab-149">Azure hizmetleri ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="cdcab-149">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="cdcab-150">SSH kimlik doğrulaması ile yeni sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdcab-150">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="cdcab-151">Azure Container Instances’a kapsayıcı görüntüsü dağıtma</span><span class="sxs-lookup"><span data-stu-id="cdcab-151">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="cdcab-152">Azure Kubernetes Hizmeti’nde küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdcab-152">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="cdcab-153">Azure Depolama hizmetleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="cdcab-153">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="cdcab-154">Go için Azure SDK’ya ilişkin tüm örnekler</span><span class="sxs-lookup"><span data-stu-id="cdcab-154">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
