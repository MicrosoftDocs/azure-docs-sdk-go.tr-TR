---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: 5df14f939efdd0550b49261c88c8dc6518ada459
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059280"
---
[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur. [Azure Stack Profilleri](/azure/azure-stack/user/azure-stack-version-profiles-go) kullanan ortamlar için en az Go 1.9 sürümü gerekir.
Go'yu yüklemeniz gerekiyorsa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.

Go için Azure SDK ve bağımlılıklarını `go get` üzerinden indirebilirsiniz.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun. Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir. İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.
