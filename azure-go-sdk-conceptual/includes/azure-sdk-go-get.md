---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 02/14/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: ddd58efdbc0c2d3ded068a9bebf2466db702566f
ms.sourcegitcommit: f08abf902b48f8173aa6e261084ff2cfc9043305
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/03/2018
---
[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur. [Azure Stack Profilleri](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles) kullanan ortamlar için en az Go 1.9 sürümü gerekir.
Sisteminizde Go yoksa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.

Go için Azure SDK ve bağımlılıklarını `go get` üzerinden edinebilirsiniz.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun. Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir. İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.

