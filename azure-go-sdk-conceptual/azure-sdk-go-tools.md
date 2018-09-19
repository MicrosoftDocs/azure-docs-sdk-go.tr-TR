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
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Go için Azure SDK’yı kullanan geliştiriciler için araçlar

Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.

## <a name="azure-cli"></a>Azure CLI

Azure CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar. CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir. CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz. CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.

> [!div class="nextstepaction"]
> [Azure CLI'yı yükleme](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code, Go desteği sunan basit bir düzenleyicidir. Bu uzantı otomatik tamamlama, `impl` şablonları, yeniden düzenleme ve hata ayıklama gibi özellikler sunar. Visual Studio Code ayrıca kaynak denetimine düzenleyici içinden erişim desteği ve Azure hizmetleriyle çalışmak için kullanılabilecek uzantılar sunar.

* [Visual Studio Code’u yükleyin](https://code.visualstudio.com/Download)
* [Visual Studio Code Go uzantısını edinin](https://code.visualstudio.com/docs/languages/go)
* [Visual Studio Code Azure Araçları uzantısını edinin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a>Azure DevOps Projesi ile CI/CD

Azure DevOps Projesi işlem hatları, Go uygulamalarınız için sürekli tümleştirme sistemi ayarlamanızı sağlar. İhtiyacınız olan tek şey bir git deposudur ve doğrudan Azure üzerinde dağıtma ve test gerçekleştirebilirsiniz.

> [!div class="nextstepaction"]
> [Azure DevOps Projesi ile CI/CD işlem hattı oluşturmayı öğrenin](/azure/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a>dep ile bağımlılık yönetimi

Go için Azure SDK, bağımlılık yönetimi için dep kullanır. dep komutu Go uygulamanız için satıcı gereksinimlerini çekmenizi ve çakışmalardan kaçınarak projenizin doğru bir şekilde çalıştığından emin olmanızı sağlar.

> [!div class="nextstepaction"]
> [dep bağımlılık yöneticisini edinin](https://github.com/golang/dep)
