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
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Go için Azure SDK’yı kullanan geliştiriciler için araçlar

Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.

## <a name="azure-cli-20"></a>Azure CLI 2.0

Azure 2.0 CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar. CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir. CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz. CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.

> [!div class="nextstepaction"]
> [Azure CLI 2.0’ı yükleme](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code, uzantılar aracılığıyla Go dili için kapsamlı desteğe sahip basit bir düzenleyicidir. Bu uzantılar, otomatik tamamlama, `impl` şablonları, yeniden düzenleme ve hata ayıklama gibi özelliklere yönelik destek içerir. Visual Studio Code ayrıca kaynak denetimi gibi yaygın geliştirici araçları için birçok uzantı ve hatta Azure hizmetleriyle doğrudan etkileşim için uzantılar da sunar. Microsoft, Azure CLI için etkileşimli bir arabirim de dahil olmak üzere bu Azure uzantılarını içeren resmi bir meta uzantıyı korur.

* [Visual Studio Code’u yükleyin](https://code.visualstudio.com/Download)
* [Visual Studio Code Go uzantısını edinin](https://code.visualstudio.com/docs/languages/go)
* [Azure Araçları uzantısını edinin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a>dep ile bağımlılık yönetimi

Paket bağımlılıklarınızı yönetmenin ve Go ile satıcı dizinine taşıma işlemi yapmanın birçok yolu olsa da henüz resmi bir çözüm yoktur. Bu yönetimin, `dep` bağımlılık yöneticisi ile gerçekleştirilmesi önerilir. Go için Azure SDK, satıcı dizinine taşıma işlemi için dep kullanır ve dep kullanan diğer projelere ilişkin bağımlılıkları doğru şekilde alacağı kesindir.

> [!div class="nextstepaction"]
> [dep bağımlılık yöneticisini edinin](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a>Application Insights ile telemetri

[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/), uygulamalarınızdan telemetri bilgilerini kolayca toplamanıza olanak sağlayan ve Azure ekosistemi, Visual Studio Team Services ve GitHub ile tümleştirilen bir analiz ürünüdür. Birçok uygulamada kullanılabilir ve Microsoft, Application Insights ile çalışmak için bir Go SDK sunar.

> [!div class="nextstepaction"]
> [Go için Application Insights SDK’yı edinin](https://github.com/Microsoft/ApplicationInsights-Go) 
