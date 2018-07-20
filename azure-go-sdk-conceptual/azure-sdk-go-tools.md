---
title: Go geliştiricileri için araçlar
description: Go için Azure SDK ve Azure hizmetleri ile çalışmaya ilişkin araçlar
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 07/13/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: dfa3912ac13e6f6d52d607f9dcc150f3a5b57602
ms.sourcegitcommit: d1790b317a8fcb4d672c654dac2a925a976589d4
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/14/2018
ms.locfileid: "39039514"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="1b97b-103">Go için Azure SDK’yı kullanan geliştiriciler için araçlar</span><span class="sxs-lookup"><span data-stu-id="1b97b-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="1b97b-104">Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1b97b-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="1b97b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b97b-105">Azure CLI</span></span>

<span data-ttu-id="1b97b-106">Azure CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b97b-106">The Azure CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="1b97b-107">CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="1b97b-108">CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b97b-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="1b97b-109">CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b97b-110">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="1b97b-110">Install the Azure CLI</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="1b97b-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="1b97b-111">Visual Studio Code</span></span>

<span data-ttu-id="1b97b-112">Visual Studio Code, uzantılar aracılığıyla Go dili için kapsamlı desteğe sahip basit bir düzenleyicidir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-112">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="1b97b-113">Bu uzantılar, otomatik tamamlama, `impl` şablonları, yeniden düzenleme ve hata ayıklama gibi özelliklere yönelik destek içerir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-113">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="1b97b-114">Visual Studio Code ayrıca kaynak denetimi gibi yaygın geliştirici araçları için birçok uzantı ve hatta Azure hizmetleriyle doğrudan etkileşim için uzantılar da sunar.</span><span class="sxs-lookup"><span data-stu-id="1b97b-114">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="1b97b-115">Microsoft, Azure CLI için etkileşimli bir arabirim de dahil olmak üzere bu Azure uzantılarını içeren resmi bir meta uzantıyı korur.</span><span class="sxs-lookup"><span data-stu-id="1b97b-115">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="1b97b-116">Visual Studio Code’u yükleyin</span><span class="sxs-lookup"><span data-stu-id="1b97b-116">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="1b97b-117">Visual Studio Code Go uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="1b97b-117">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="1b97b-118">Azure Araçları uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="1b97b-118">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a><span data-ttu-id="1b97b-119">Azure DevOps Projesi ile CI/CD</span><span class="sxs-lookup"><span data-stu-id="1b97b-119">CI/CD with Azure DevOps Project</span></span>

<span data-ttu-id="1b97b-120">Azure DevOps Projesi işlem hattı ile Go uygulamalarınız için sürekli derleme ve dağıtım ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b97b-120">With the Azure DevOps Project pipeline, you can set up a continuous build and deploy for your Go applications.</span></span> <span data-ttu-id="1b97b-121">Azure kaynaklarınıza dağıtım ve doğrudan bunlar üzerinde test için gerekli kurulumu yapabilmeniz için yalnızca mevcut bir git deposu yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-121">All you need is an available git repo, and you can set up to deploy and test directly on your Azure resources.</span></span> <span data-ttu-id="1b97b-122">Kolayca oluşturulup yönetilebilen yapılandırma işlem hattı doğrudan Azure'da sağlandığından, bunu da diğer Azure kaynaklarınızla aynı şekilde denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b97b-122">The configuration pipeline is easy to create and manage, and since it's provisioned directly on Azure, you can control it in the same way that you handle your other Azure resources.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b97b-123">Azure DevOps Projesi ile CI/CD işlem hattı oluşturmayı öğrenin</span><span class="sxs-lookup"><span data-stu-id="1b97b-123">Learn how to create a CI/CD pipeline with Azure DevOps Project</span></span>](/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="1b97b-124">dep ile bağımlılık yönetimi</span><span class="sxs-lookup"><span data-stu-id="1b97b-124">Dependency management with dep</span></span>

<span data-ttu-id="1b97b-125">Paket bağımlılıklarınızı yönetmenin ve Go ile satıcı dizinine taşıma işlemi yapmanın birçok yolu olsa da henüz resmi bir çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="1b97b-125">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="1b97b-126">Bu yönetimin, `dep` bağımlılık yöneticisi ile gerçekleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-126">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="1b97b-127">Go için Azure SDK, satıcı dizinine taşıma işlemi için dep kullanır ve dep kullanan diğer projelere ilişkin bağımlılıkları doğru şekilde alacağı kesindir.</span><span class="sxs-lookup"><span data-stu-id="1b97b-127">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b97b-128">dep bağımlılık yöneticisini edinin</span><span class="sxs-lookup"><span data-stu-id="1b97b-128">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
