---
title: İşlem ve ağa yönelik Go için Azure SDK örnekleri
description: VM’ler ve sanal ağlar gibi işlem kaynaklarıyla çalışmak için Go için Azure SDK’dan seçilen örnekler.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: sample
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: d570ad8598ae06633d0010245c207641161ee446
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059093"
---
# <a name="azure-sdk-for-go-samples-for-compute-and-networking"></a><span data-ttu-id="bc699-103">İşlem ve ağa yönelik Go için Azure SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="bc699-103">Azure SDK for Go samples for compute and networking</span></span>

<span data-ttu-id="bc699-104">Aşağıdaki tabloda Go için Azure SDK'da işlem ve sanal ağ kaynaklarının yönetimini gösteren seçilmiş örneklerin bağlantıları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bc699-104">The following table links to selected samples that demonstrate the management of compute and virtual network resources in the Azure SDK for Go.</span></span>

<span data-ttu-id="bc699-105">Go için Azure SDK’ya ilişkin tüm örnekler [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples)’da bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="bc699-105">All samples for the Azure SDK for Go are available on [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span></span>

| <span data-ttu-id="bc699-106">Adı</span><span class="sxs-lookup"><span data-stu-id="bc699-106">Name</span></span> | <span data-ttu-id="bc699-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bc699-107">Description</span></span> |
|------|-------------|
| [<span data-ttu-id="bc699-108">network/network</span><span class="sxs-lookup"><span data-stu-id="bc699-108">network/network</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/network/network.go) | <span data-ttu-id="bc699-109">Sanal ağlar, alt ağlar, ağ güvenliği grupları gibi ağ kaynaklarını oluşturun, güncelleştirin, silin ve sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="bc699-109">Create, update, delete, and query network resources including virtual networks, subnets, and network security groups.</span></span> |
| [<span data-ttu-id="bc699-110">compute/vm_disk</span><span class="sxs-lookup"><span data-stu-id="bc699-110">compute/vm_disk</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_disk.go) | <span data-ttu-id="bc699-111">Bir VM’de veri diskleri oluşturun, kullanıma açın, kullanıma kapatın, güncelleştirin ve şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="bc699-111">Create, attach, detach, update, and encrypt data disks for a VM.</span></span> |
| [<span data-ttu-id="bc699-112">compute/vm</span><span class="sxs-lookup"><span data-stu-id="bc699-112">compute/vm</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm.go) | <span data-ttu-id="bc699-113">VM’leri oluşturun, güncelleştirin, devre dışı bırakın ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc699-113">Create, update, deactivate, and manage VMs.</span></span> |
| [<span data-ttu-id="bc699-114">compute/vm_with_availabilityset</span><span class="sxs-lookup"><span data-stu-id="bc699-114">compute/vm_with_availabilityset</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_availabilityset.go) | <span data-ttu-id="bc699-115">VM’ler için kullanılabilirlik kümeleri ve yük dengeleyicileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc699-115">Create availability sets and load balancers for VMs.</span></span> |
| [<span data-ttu-id="bc699-116">compute/vm_with_identity</span><span class="sxs-lookup"><span data-stu-id="bc699-116">compute/vm_with_identity</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_identity.go) | <span data-ttu-id="bc699-117">VM’ler için Yönetilen Hizmet Kimlikleri (MSI’ler) oluşturun ve bunları yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc699-117">Create and manage Managed Service Identities (MSIs) for VMs.</span></span> |
