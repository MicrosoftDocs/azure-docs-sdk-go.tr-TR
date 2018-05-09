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
<span data-ttu-id="7868d-101">[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="7868d-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and later.</span></span> <span data-ttu-id="7868d-102">[Azure Stack Profilleri](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles) kullanan ortamlar için en az Go 1.9 sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="7868d-102">For environments using [Azure Stack Profiles](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="7868d-103">Sisteminizde Go yoksa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.</span><span class="sxs-lookup"><span data-stu-id="7868d-103">If you do not have Go available on your system, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="7868d-104">Go için Azure SDK ve bağımlılıklarını `go get` üzerinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7868d-104">You can obtain the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="7868d-105">URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7868d-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="7868d-106">Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7868d-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="7868d-107">İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7868d-107">You also need to capitalize `Azure` in your import statements.</span></span>

