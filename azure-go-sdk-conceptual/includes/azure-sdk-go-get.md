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
<span data-ttu-id="35c8e-101">[Go için Azure SDK](https://github.com/Azure/azure-sdk-for-go), Go 1.8 ve sonraki sürümlerle uyumludur.</span><span class="sxs-lookup"><span data-stu-id="35c8e-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and later.</span></span> <span data-ttu-id="35c8e-102">[Azure Stack Profilleri](https://docs.microsoft.com/azure/azure-stack/azure-stack-version-profiles) kullanan ortamlar için en az Go 1.9 sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="35c8e-102">For environments using [Azure Stack Profiles](https://docs.microsoft.com/azure/azure-stack/azure-stack-version-profiles), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="35c8e-103">Sisteminizde Go yoksa [Go yükleme yönergelerini](https://golang.org/doc/install) izleyin.</span><span class="sxs-lookup"><span data-stu-id="35c8e-103">If you do not have Go available on your system, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="35c8e-104">Go için Azure SDK ve bağımlılıklarını `go get` üzerinden edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35c8e-104">You can obtain the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="35c8e-105">URL’de `Azure` kısmını büyük harfle yazdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="35c8e-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="35c8e-106">Aksi takdirde bu, SDK ile çalışırken büyük/küçük harfle ilgili içeri aktarma sorunlarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="35c8e-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="35c8e-107">İçeri aktarma deyimlerinizde de `Azure` kısmını büyük harfle yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35c8e-107">You also need to capitalize `Azure` in your import statements.</span></span>
