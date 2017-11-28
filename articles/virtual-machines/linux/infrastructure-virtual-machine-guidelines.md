---
title: "Azure Linux 가상 컴퓨터 지침 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 배포하기 위한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 2d886795b301ab79272cae10a53831fd44c18f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a><span data-ttu-id="4c93f-103">Linux용 Azure 가상 컴퓨터 지침</span><span class="sxs-lookup"><span data-stu-id="4c93f-103">Azure virtual machines guidelines for Linux</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="4c93f-104">이 문서에서는 Azure 환경 내에서 VM(가상 컴퓨터)을 만들고 관리하는 데 필요한 계획 단계를 이해하는 데 주안점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-104">This article focuses on understanding the required planning steps for creating and managing virtual machines (VMs) within your Azure environment.</span></span>

## <a name="implementation-guidelines-for-vms"></a><span data-ttu-id="4c93f-105">VM에 대한 구현 지침</span><span class="sxs-lookup"><span data-stu-id="4c93f-105">Implementation guidelines for VMs</span></span>
<span data-ttu-id="4c93f-106">의사 결정:</span><span class="sxs-lookup"><span data-stu-id="4c93f-106">Decisions:</span></span>

* <span data-ttu-id="4c93f-107">인프라의 다양한 응용 프로그램 계층 및 구성 요소를 위해 몇 개의 VM이 필요한가?</span><span class="sxs-lookup"><span data-stu-id="4c93f-107">How many VMs do you require for your various application tiers and components of your infrastructure?</span></span>
* <span data-ttu-id="4c93f-108">각 VM에 어떤 CPU 및 메모리 리소스가 필요하며 저장소 요구 사항은 무엇인가?</span><span class="sxs-lookup"><span data-stu-id="4c93f-108">What CPU and memory resources does each VM need, and what are the storage requirements?</span></span>

<span data-ttu-id="4c93f-109">작업:</span><span class="sxs-lookup"><span data-stu-id="4c93f-109">Tasks:</span></span>

* <span data-ttu-id="4c93f-110">응용 프로그램의 워크로드와 VM에 필요한 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-110">Define the workloads for your application and the resources the VMs require.</span></span>
* <span data-ttu-id="4c93f-111">해당 VM 크기 및 저장소 형식에 따라 각 VM의 리소스 요구를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-111">Align the resource demands for each VM with the appropriate VM size and storage type.</span></span>
* <span data-ttu-id="4c93f-112">인프라의 다양한 계층 및 구성 요소에 대한 리소스 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-112">Define your resource groups for the different tiers and components of your infrastructure.</span></span>
* <span data-ttu-id="4c93f-113">VM 명명 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-113">Define your VM naming convention.</span></span>
* <span data-ttu-id="4c93f-114">Azure CLI, 웹 포털 또는 Resource Manager 템플릿을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-114">Create your VMs using the Azure CLI, web portal, or with Resource Manager templates.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="4c93f-115">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="4c93f-115">Virtual machines</span></span>
<span data-ttu-id="4c93f-116">Azure 환경 내의 주요 구성 리소스 중 하나가 VM일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-116">One of the main resources within your Azure environment is likely VMs.</span></span> <span data-ttu-id="4c93f-117">이 리소스에서 응용 프로그램, 데이터베이스, 인증, 서비스 등을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-117">This resource is where you run your applications, databases, authentication services, etc.</span></span>

<span data-ttu-id="4c93f-118">성능 및 비용 측면에서 환경 규모를 올바르게 조정하려면 [다양한 VM 크기](sizes.md) 를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-118">It is important to understand the [different VM sizes](sizes.md) to correctly size your environment from a performance and cost perspective.</span></span> <span data-ttu-id="4c93f-119">VM에 충분한 CPU 코어 또는 메모리가 없으면 디자인 및 개발 품질과 관계없이 응용 프로그램의 성능이 저하됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-119">If your VMs do not have enough CPU cores or memory, performance of your application suffers regardless of how well it is designed and developed.</span></span> <span data-ttu-id="4c93f-120">인프라의 각 구성 요소에 사용할 VM 크기를 결정할 때는 각 VM 시리즈에 대해 제안된 워크로드를 먼저 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-120">Review the suggested workloads for each VM series as a starting point as you decide which size VM to use for each component in your infrastructure.</span></span> <span data-ttu-id="4c93f-121">배포 후에 [VM의 크기를 변경](change-vm-size.md) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-121">You can [change the size of a VM](change-vm-size.md) after deployment.</span></span>

<span data-ttu-id="4c93f-122">저장소는 VM의 성능에 중요한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-122">Storage plays a key role in VM performance.</span></span> <span data-ttu-id="4c93f-123">일반 스핀 디스크를 사용하는 Standard 저장소를 사용할 수도 있고, I/O 워크로드가 높고 최고의 성능이 필요한 경우에는 SSD 디스크를 사용하는 Premium 저장소를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-123">You can use Standard storage, that uses regular spinning disks, or Premium storage for high I/O workloads and peak performance, that use SSD disks.</span></span> <span data-ttu-id="4c93f-124">VM 크기와 마찬가지로 저장 미디어를 선택하는 데 비용을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-124">As with the VM size, there are cost considerations to selecting the storage medium.</span></span> <span data-ttu-id="4c93f-125">최적의 VM 성능을 위해 적절한 저장소를 디자인하는 방법을 이해하려는 경우 [저장소 인프라 지침 문서](infrastructure-storage-solutions-guidelines.md) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4c93f-125">You can read the [storage infrastructure guidelines article](infrastructure-storage-solutions-guidelines.md) to understand how to design appropriate storage for optimum performance of your VMs.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="4c93f-126">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="4c93f-126">Resource groups</span></span>
<span data-ttu-id="4c93f-127">VM과 같은 구성 요소는 손쉬운 관리 및 유지 관리를 위해 [Azure 리소스 그룹](../../azure-resource-manager/resource-group-overview.md)을 사용하여 논리적으로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-127">Components such as VMs are logically grouped for ease of management and maintenance using [Azure Resource Groups](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="4c93f-128">리소스 그룹을 사용하여 지정된 응용 프로그램을 구성하는 모든 리소스를 만들고, 관리하고, 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-128">By using resource groups, you can create, manage, and monitor all the resources that make up a given application.</span></span> <span data-ttu-id="4c93f-129">[역할 기반 액세스 제어](../../active-directory/role-based-access-control-what-is.md) 를 구현하여 팀 내의 사람 사람들에게 필요한 리소스에 대한 액세스 권한만 부여할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-129">You can also implement [role-based access controls](../../active-directory/role-based-access-control-what-is.md) to grant access to others within your team to only the resources they require.</span></span> <span data-ttu-id="4c93f-130">시간을 투입하여 리소스 그룹 및 역할 할당을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-130">Take time to plan out your resource groups and role assignments.</span></span> <span data-ttu-id="4c93f-131">실제로 리소스 그룹을 디자인 및 구현하는 다양한 접근 방법이 있으므로 VM을 구축하는 최선의 방법을 이해하려면 [리소스 그룹 지침 문서](infrastructure-resource-groups-guidelines.md) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4c93f-131">There are different approaches to actually design and implement resource groups, so be sure to read the [resource groups guidelines article](infrastructure-resource-groups-guidelines.md) to understand how best to build out your VMs.</span></span>

## <a name="templates"></a><span data-ttu-id="4c93f-132">템플릿</span><span class="sxs-lookup"><span data-stu-id="4c93f-132">Templates</span></span>
<span data-ttu-id="4c93f-133">선언적 JSON 파일에 정의되는 템플릿을 작성하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-133">You can build templates, defined by declarative JSON files, to create your VMs.</span></span> <span data-ttu-id="4c93f-134">템플릿은 VM 자체는 물론, 일반적으로 필요한 저장소, 네트워킹, 네트워크 인터페이스, IP 주소 지정 등을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-134">Templates typically also build the required storage, networking, network interfaces, IP addressing, etc. along with the VMs themselves.</span></span> <span data-ttu-id="4c93f-135">템플릿을 통해 개발 및 테스트를 위한 일관되고 재현 가능한 환경을 만들어 프로덕션 환경에 쉽게 복제할 수도 있고 그 반대도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4c93f-135">You can use templates to create consistent, reproducible environments for development and testing purposes to easily replicate production environments and vice versa.</span></span> <span data-ttu-id="4c93f-136">VM을 만들어 배포하는 데 템플릿을 사용하는 방법을 이해하려면 [템플릿 작성 및 사용](../../azure-resource-manager/resource-group-overview.md#template-deployment)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4c93f-136">You can read more about [building and using templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) to understand how you can use them for creating and deploying your VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c93f-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c93f-137">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

