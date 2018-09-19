---
title: Go için Azure SDK’yı kullanan geliştiriciler için araçlar
description: Go için Azure SDK ve Azure hizmetleri ile çalışmaya ilişkin araçlar
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 70cf7d645f47df29e8e42599a0acd75858144783
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059212"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="881d7-103">Go için Azure SDK’yı kullanan geliştiriciler için araçlar</span><span class="sxs-lookup"><span data-stu-id="881d7-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="881d7-104">Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="881d7-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="881d7-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="881d7-105">Azure CLI</span></span>

<span data-ttu-id="881d7-106">Azure CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="881d7-106">The Azure CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="881d7-107">CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="881d7-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="881d7-108">CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881d7-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="881d7-109">CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="881d7-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="881d7-110">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="881d7-110">Install the Azure CLI</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="881d7-111">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="881d7-111">Visual Studio Code</span></span>

<span data-ttu-id="881d7-112">Visual Studio Code, Go desteği sunan basit bir düzenleyicidir.</span><span class="sxs-lookup"><span data-stu-id="881d7-112">Visual Studio Code is a lightweight editor that offers Go support.</span></span> <span data-ttu-id="881d7-113">Bu uzantı otomatik tamamlama, `impl` şablonları, yeniden düzenleme ve hata ayıklama gibi özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="881d7-113">This extension offers features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="881d7-114">Visual Studio Code ayrıca kaynak denetimine düzenleyici içinden erişim desteği ve Azure hizmetleriyle çalışmak için kullanılabilecek uzantılar sunar.</span><span class="sxs-lookup"><span data-stu-id="881d7-114">Visual Studio Code also offers support for in-editor access to source control, and extensions for working with Azure services.</span></span>

* [<span data-ttu-id="881d7-115">Visual Studio Code’u yükleyin</span><span class="sxs-lookup"><span data-stu-id="881d7-115">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="881d7-116">Visual Studio Code Go uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="881d7-116">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="881d7-117">Visual Studio Code Azure Araçları uzantısını edinin</span><span class="sxs-lookup"><span data-stu-id="881d7-117">Get the Visual Studio Code Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a><span data-ttu-id="881d7-118">Azure DevOps Projesi ile CI/CD</span><span class="sxs-lookup"><span data-stu-id="881d7-118">CI/CD with Azure DevOps Project</span></span>

<span data-ttu-id="881d7-119">Azure DevOps Projesi işlem hatları, Go uygulamalarınız için sürekli tümleştirme sistemi ayarlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="881d7-119">Azure DevOps Project pipelines allow you to set up a continuous integration system for your Go applications.</span></span> <span data-ttu-id="881d7-120">İhtiyacınız olan tek şey bir git deposudur ve doğrudan Azure üzerinde dağıtma ve test gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881d7-120">All it takes is a git repo, and you can deploy and test directly on Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="881d7-121">Azure DevOps Projesi ile CI/CD işlem hattı oluşturmayı öğrenin</span><span class="sxs-lookup"><span data-stu-id="881d7-121">Learn how to create a CI/CD pipeline with Azure DevOps Project</span></span>](/azure/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="881d7-122">dep ile bağımlılık yönetimi</span><span class="sxs-lookup"><span data-stu-id="881d7-122">Dependency management with dep</span></span>

<span data-ttu-id="881d7-123">Go için Azure SDK, bağımlılık yönetimi için dep kullanır.</span><span class="sxs-lookup"><span data-stu-id="881d7-123">The Azure SDK for Go uses dep for dependency management.</span></span> <span data-ttu-id="881d7-124">dep komutu Go uygulamanız için satıcı gereksinimlerini çekmenizi ve çakışmalardan kaçınarak projenizin doğru bir şekilde çalıştığından emin olmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="881d7-124">The dep command allows you to pull and vendor requirements for your Go application, avoiding version conflicts and ensuring that your project works correctly.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="881d7-125">dep bağımlılık yöneticisini edinin</span><span class="sxs-lookup"><span data-stu-id="881d7-125">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
