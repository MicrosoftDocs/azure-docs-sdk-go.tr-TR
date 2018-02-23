---
title: "Go geliştiricileri için araçlar"
description: "Go için Azure SDK ve Azure hizmetleri ile çalışmaya ilişkin araçlar"
keywords: azure, go, golang, azure, visual studio, visual studio code
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 4753775e608b39c6da43d64fd08c1532e03d5810
ms.sourcegitcommit: aaa8c37880332625f858a38f5918e6cf581bf48d
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/15/2018
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="6cfa3-104">Go için Azure SDK’yı kullanan geliştiriciler için araçlar</span><span class="sxs-lookup"><span data-stu-id="6cfa3-104">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="6cfa3-105">Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-105">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="6cfa3-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6cfa3-106">Azure CLI 2.0</span></span>

<span data-ttu-id="6cfa3-107">Azure 2.0 CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-107">The Azure 2.0 CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="6cfa3-108">CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-108">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="6cfa3-109">CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-109">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="6cfa3-110">CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-110">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cfa3-111">Azure CLI 2.0’ı yükleme</span><span class="sxs-lookup"><span data-stu-id="6cfa3-111">Install the Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="6cfa3-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6cfa3-112">Visual Studio Code</span></span>

<span data-ttu-id="6cfa3-113">Visual Studio Code, uzantılar aracılığıyla Go dili için kapsamlı desteğe sahip basit bir düzenleyicidir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-113">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="6cfa3-114">Bu uzantılar, otomatik tamamlama, `impl` şablonları, yeniden düzenleme ve hata ayıklama gibi özelliklere yönelik destek içerir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-114">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="6cfa3-115">Visual Studio Code ayrıca kaynak denetimi gibi yaygın geliştirici araçları için birçok uzantı ve hatta Azure hizmetleriyle doğrudan etkileşim için uzantılar da sunar.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-115">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="6cfa3-116">Microsoft, Azure CLI için etkileşimli bir arabirim de dahil olmak üzere bu Azure uzantılarını içeren resmi bir meta uzantıyı korur.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-116">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="6cfa3-117">Visual Studio Code’u yükleyin</span><span class="sxs-lookup"><span data-stu-id="6cfa3-117">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="6cfa3-118">Visual Studio Code Go uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="6cfa3-118">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="6cfa3-119">Azure Araçları uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="6cfa3-119">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="6cfa3-120">dep ile bağımlılık yönetimi</span><span class="sxs-lookup"><span data-stu-id="6cfa3-120">Dependency management with dep</span></span>

<span data-ttu-id="6cfa3-121">Paket bağımlılıklarınızı yönetmenin ve Go ile satıcı dizinine taşıma işlemi yapmanın birçok yolu olsa da henüz resmi bir çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-121">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="6cfa3-122">Bu yönetimin, `dep` bağımlılık yöneticisi ile gerçekleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-122">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="6cfa3-123">Go için Azure SDK, satıcı dizinine taşıma işlemi için dep kullanır ve dep kullanan diğer projelere ilişkin bağımlılıkları doğru şekilde alacağı kesindir.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-123">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cfa3-124">dep bağımlılık yöneticisini edinin</span><span class="sxs-lookup"><span data-stu-id="6cfa3-124">Get the dep dependency manager</span></span>](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a><span data-ttu-id="6cfa3-125">Application Insights ile telemetri</span><span class="sxs-lookup"><span data-stu-id="6cfa3-125">Telemetry with Application Insights</span></span>

<span data-ttu-id="6cfa3-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/), uygulamalarınızdan telemetri bilgilerini kolayca toplamanıza olanak sağlayan ve Azure ekosistemi, Visual Studio Team Services ve GitHub ile tümleştirilen bir analiz ürünüdür.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) is an analytics product that allows you to easily collect telemetry information from your applications and integrates with the Azure ecosystem, Visual Studio Team Services, and GitHub.</span></span> <span data-ttu-id="6cfa3-127">Birçok uygulamada kullanılabilir ve Microsoft, Application Insights ile çalışmak için bir Go SDK sunar.</span><span class="sxs-lookup"><span data-stu-id="6cfa3-127">It can be used in many applications, and Microsoft offers a Go SDK for working with Application Insights.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cfa3-128">Go için Application Insights SDK’yı edinin</span><span class="sxs-lookup"><span data-stu-id="6cfa3-128">Get the Application Insights for Go SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Go) 
