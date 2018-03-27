---
title: İşlem ve ağa yönelik Go için Azure SDK örnekleri
description: VM’ler ve sanal ağlar gibi işlem kaynaklarıyla çalışmak için Go için Azure SDK’dan seçilen örnekler.
author: sptramer
ms.author: sttramer
ms.date: 03/21/2018
ms.topic: article
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 1e6f9d848213f0f70ab59d5e0bcc5c52127e97c5
ms.sourcegitcommit: fcc1786d59d2e32c97a9a8e0748e06f564a961bd
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2018
---
# <a name="azure-sdk-for-go-samples-for-compute-and-networking"></a><span data-ttu-id="a5c5e-103">İşlem ve ağa yönelik Go için Azure SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="a5c5e-103">Azure SDK for Go samples for compute and networking</span></span>

<span data-ttu-id="a5c5e-104">Aşağıdaki tablo Azure’daki sanal ağları ve alt ağları yönetmek üzere kullanabileceğiniz, seçili Go kaynak kodu örnekleriyle ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-104">The following table links to selected samples of Go source code that you can use to manage VMs, virtual networks, and subnets in Azure.</span></span> 

<span data-ttu-id="a5c5e-105">Go için Azure SDK’ya ilişkin tüm örnekler [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples)’da bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-105">All samples for the Azure SDK for Go are available on [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span></span>

| <span data-ttu-id="a5c5e-106">Adı</span><span class="sxs-lookup"><span data-stu-id="a5c5e-106">Name</span></span> | <span data-ttu-id="a5c5e-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a5c5e-107">Description</span></span> |
|------|-------------|
| [<span data-ttu-id="a5c5e-108">network/network</span><span class="sxs-lookup"><span data-stu-id="a5c5e-108">network/network</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/network/network.go) | <span data-ttu-id="a5c5e-109">Sanal ağlar, alt ağlar, ağ güvenliği grupları gibi ağ kaynaklarını oluşturun, güncelleştirin, silin ve sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-109">Create, update, delete, and query network resources including virtual networks, subnets, and network security groups.</span></span> |
| [<span data-ttu-id="a5c5e-110">compute/loadbalancer</span><span class="sxs-lookup"><span data-stu-id="a5c5e-110">compute/loadbalancer</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/loadbalancer.go) | <span data-ttu-id="a5c5e-111">Bir yük dengeleyicisi ile kullanılabilirlik gruplarını oluşturup sorgulayın ve VM’ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-111">Create and query availability groups, and create VMs with a load balancer.</span></span> |
| [<span data-ttu-id="a5c5e-112">compute/compute</span><span class="sxs-lookup"><span data-stu-id="a5c5e-112">compute/compute</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/compute.go) | <span data-ttu-id="a5c5e-113">VM’ler oluşturun, silin, güncelleştirin ve bunların güç yönetimini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-113">Create, delete, update, and power-manage VMs.</span></span> <span data-ttu-id="a5c5e-114">Veri diskleriyle çalışın ve VM’nin işletim sistemi diskini yönetin.</span><span class="sxs-lookup"><span data-stu-id="a5c5e-114">Work with data disks and managing the OS disk of the VM.</span></span> |
