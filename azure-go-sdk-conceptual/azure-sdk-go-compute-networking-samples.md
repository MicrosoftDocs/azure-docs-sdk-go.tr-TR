---
title: İşlem ve ağa yönelik Go için Azure SDK örnekleri
description: VM’ler ve sanal ağlar gibi işlem kaynaklarıyla çalışmak için Go için Azure SDK’dan seçilen örnekler.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 03/21/2018
ms.topic: sample
ms.prod: azure
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: 3b31716ee42c638bab4a6dd99b9eb0d7c07e51a4
ms.sourcegitcommit: 0f581979216f7c9d4913681a6d9f6fe09af26e43
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39475798"
---
# <a name="azure-sdk-for-go-samples-for-compute-and-networking"></a><span data-ttu-id="985f2-103">İşlem ve ağa yönelik Go için Azure SDK örnekleri</span><span class="sxs-lookup"><span data-stu-id="985f2-103">Azure SDK for Go samples for compute and networking</span></span>

<span data-ttu-id="985f2-104">Aşağıdaki tablo Azure’daki sanal ağları ve alt ağları yönetmek üzere kullanabileceğiniz, seçili Go kaynak kodu örnekleriyle ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="985f2-104">The following table links to selected samples of Go source code that you can use to manage VMs, virtual networks, and subnets in Azure.</span></span> 

<span data-ttu-id="985f2-105">Go için Azure SDK’ya ilişkin tüm örnekler [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples)’da bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="985f2-105">All samples for the Azure SDK for Go are available on [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span></span>

| <span data-ttu-id="985f2-106">Adı</span><span class="sxs-lookup"><span data-stu-id="985f2-106">Name</span></span> | <span data-ttu-id="985f2-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="985f2-107">Description</span></span> |
|------|-------------|
| [<span data-ttu-id="985f2-108">network/network</span><span class="sxs-lookup"><span data-stu-id="985f2-108">network/network</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/network/network.go) | <span data-ttu-id="985f2-109">Sanal ağlar, alt ağlar, ağ güvenliği grupları gibi ağ kaynaklarını oluşturun, güncelleştirin, silin ve sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="985f2-109">Create, update, delete, and query network resources including virtual networks, subnets, and network security groups.</span></span> |
| [<span data-ttu-id="985f2-110">compute/vm_disk</span><span class="sxs-lookup"><span data-stu-id="985f2-110">compute/vm_disk</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_disk.go) | <span data-ttu-id="985f2-111">Bir VM’de veri diskleri oluşturun, kullanıma açın, kullanıma kapatın, güncelleştirin ve şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="985f2-111">Create, attach, detatch, update, and encrypt data disks for a VM.</span></span> |
| [<span data-ttu-id="985f2-112">compute/vm</span><span class="sxs-lookup"><span data-stu-id="985f2-112">compute/vm</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm.go) | <span data-ttu-id="985f2-113">VM’leri oluşturun, güncelleştirin, devre dışı bırakın ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="985f2-113">Create, update, deactivate, and manage VMs.</span></span> |
| [<span data-ttu-id="985f2-114">compute/vm_with_availabilityset</span><span class="sxs-lookup"><span data-stu-id="985f2-114">compute/vm_with_availabilityset</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_availabilityset.go) | <span data-ttu-id="985f2-115">VM’ler için kullanılabilirlik kümeleri ve yük dengeleyicileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="985f2-115">Create availability sets and load balancers for VMs.</span></span> |
| [<span data-ttu-id="985f2-116">compute/vm_with_identity</span><span class="sxs-lookup"><span data-stu-id="985f2-116">compute/vm_with_identity</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_identity.go) | <span data-ttu-id="985f2-117">VM’ler için Yönetilen Hizmet Kimlikleri (MSI’ler) oluşturun ve bunları yönetin.</span><span class="sxs-lookup"><span data-stu-id="985f2-117">Create and manage Managed Service Identities (MSIs) for VMs.</span></span> |
