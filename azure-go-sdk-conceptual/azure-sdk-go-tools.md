---
title: Go geliştiricileri için araçlar
description: Go için Azure SDK ve Azure hizmetleri ile çalışmaya ilişkin araçlar
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 006d140bffb66fdd769a14511232d4ea5081811d
ms.sourcegitcommit: 181d4e0b164cf39b3feac346f559596bd19c94db
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38066991"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Go için Azure SDK’yı kullanan geliştiriciler için araçlar

Go kodunu etkili bir şekilde yazmaya ve Go kodunun Azure hizmetleri ile sorunsuz şekilde çalışmasını sağlamaya yönelik önerilen araçlardan bazıları burada açıklanmıştır.

## <a name="azure-cli-20"></a>Azure CLI 2.0

Azure 2.0 CLI, aboneliklerinizde Azure kaynaklarını oluşturmak ve yapılandırmak için bir komut satırı arabirimi sağlar. CLI, daha karmaşık hizmet kullanımına odaklanabilmeniz için genel ve paylaşılan Azure kaynaklarını hızlı bir şekilde oluşturmaya başlamanıza yardımcı olabilir. CLI, sorgulama ve filtreleme özelliklerine sahiptir; böylece çıkışı doğrudan sık kullandığınız komut satırı araçlarına kanalize edebilirsiniz. CLI, bir Docker görüntüsü olarak veya [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) aracılığıyla yerel sisteminize yüklenebilir.

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
> [dep bağımlılık yöneticisini edinin](https://github.com/golang/dep)
