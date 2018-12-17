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
<span data-ttu-id="4c388-101">[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="4c388-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and higher.</span></span> <span data-ttu-id="4c388-102">[Azure Stack Profilleri](/azure/azure-stack/user/azure-stack-version-profiles-go) kullanan ortamlar için en az Go 1.9 sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c388-102">For environments using [Azure Stack Profiles](/azure/azure-stack/user/azure-stack-version-profiles-go), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="4c388-103">Go'yu yüklemeniz gerekiyorsa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.</span><span class="sxs-lookup"><span data-stu-id="4c388-103">If you need to install Go, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="4c388-104">Go için Azure SDK ve bağımlılıklarını `go get` üzerinden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c388-104">You can download the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="4c388-105">URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4c388-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="4c388-106">Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="4c388-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="4c388-107">İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c388-107">You also need to capitalize `Azure` in your import statements.</span></span>
