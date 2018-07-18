---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 02/14/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: d021dd8ef4744b7c50b296b231bf63481f92411a
ms.sourcegitcommit: 2a3bd491e087a1d0e7d269bed896c029357d62a6
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38988083"
---
[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur. [Azure Stack Profilleri](https://docs.microsoft.com/azure/azure-stack/azure-stack-version-profiles) kullanan ortamlar için en az Go 1.9 sürümü gerekir.
Sisteminizde Go yoksa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.

Go için Azure SDK ve bağımlılıklarını `go get` üzerinden edinebilirsiniz.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun. Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir. İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.
