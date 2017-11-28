---
title: "선호도 그룹에서 지역으로 Azure Virtual Network(클래식) 마이그레이션 | Microsoft Docs"
description: "선호도 그룹에서 지역으로 가상 네트워크(클래식)를 마이그레이션하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: b9b3bd0f2184ac85261166d5fe2ab67e1bf319d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-to-a-region"></a><span data-ttu-id="1548e-103">선호도 그룹에서 지역으로 가상 네트워크(클래식) 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1548e-103">Migrate a virtual network (classic) from an affinity group to a region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1548e-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1548e-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="1548e-106">새로운 배포는 대부분 Resource Manager 배포 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="1548e-107">선호도 그룹을 사용하면 동일한 선호도 그룹 내에서 만든 리소스가 서로 가까이 있는 서버에서 물리적으로 호스트되도록 할 수 있으며, 이러한 리소스는 더욱 빠르게 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-107">Affinity groups ensure that resources created within the same affinity group are physically hosted by servers that are close together, enabling these resources to communicate quicker.</span></span> <span data-ttu-id="1548e-108">과거에는 선호도 그룹이 가상 네트워크(클래식)를 만들기 위한 요구 사항이었습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-108">In the past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="1548e-109">동시에 가상 네트워크(클래식)를 관리한 네트워크 관리자 서비스는 실제 서버 집합 또는 배율 단위 내에서만 작동할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-109">At that time, the network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="1548e-110">아키텍처 개선을 통해 네트워크 관리 범위가 하위 지역까지 증가했습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-110">Architectural improvements have increased the scope of network management to a region.</span></span>

<span data-ttu-id="1548e-111">이러한 아키텍처 개선의 결과, 선호도 그룹이 더 이상 권장 사항이 아니며 가상 네트워크(클래식)에 필수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="1548e-112">가상 네트워크(클래식)에 대해 선호도 그룹을 사용하던 것이 지역으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-112">The use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="1548e-113">지역과 연결된 가상 네트워크(클래식)를 지역 가상 네트워크라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="1548e-114">일반적으로 선호도 그룹을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="1548e-115">가상 네트워크 요구 사항 외에도, 선호도 그룹은 계산(클래식) 및 저장소(클래식)와 같은 리소스가 서로 가까이 있게 하려고 사용하는 것이 중요했습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-115">Aside from the virtual network requirement, affinity groups were also important to use to ensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="1548e-116">그러나 최신 Azure 네트워크 아키텍처를 통해 이러한 배치 요구 사항이 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-116">However, with the current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1548e-117">선호도 그룹과 연결된 가상 네트워크를 만드는 것이 여전히 기술적으로 가능하지만 그렇게 할 만큼 설득력 있는 이유가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-117">Although it is still technically possible to create a virtual network that is associated with an affinity group, there is no compelling reason to do so.</span></span> <span data-ttu-id="1548e-118">네트워크 보안 그룹과 같은 다양한 가상 네트워크 기능은 지역 가상 네트워크를 사용하는 경우에만 사용할 수 있으며, 선호도 그룹과 연결된 가상 네트워크에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-the-network-configuration-file"></a><span data-ttu-id="1548e-119">네트워크 구성 파일 편집</span><span class="sxs-lookup"><span data-stu-id="1548e-119">Edit the network configuration file</span></span>

1. <span data-ttu-id="1548e-120">네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-120">Export the network configuration file.</span></span> <span data-ttu-id="1548e-121">PowerShell 또는 Azure CLI(명령줄 인터페이스) 1.0을 사용하여 네트워크 구성 파일을 내보내는 방법을 알아보려면 [네트워크 구성 파일을 사용하여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md#export)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1548e-121">To learn how to export a network configuration file using PowerShell or the Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="1548e-122">네트워크 구성 파일을 편집하여 **AffinityGroup**을 **Location**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-122">Edit the network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="1548e-123">**Location**에 Azure [지역](https://azure.microsoft.com/regions)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1548e-124">**Location**은 가상 네트워크(클래식)와 연결된 선호도 그룹에 대해 지정한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-124">The **Location** is the region that you specified for the affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="1548e-125">예를 들어 가상 네트워크가 미국 서부에 위치한 선호도 그룹과 연결된 경우 마이그레이션할 때 **Location**이 미국 서부를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point to West US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="1548e-126">네트워크 구성 파일에서 값을 고유한 값으로 바꿔 다음 줄을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-126">Edit the following lines in your network configuration file, replacing the values with your own:</span></span> 
   
    <span data-ttu-id="1548e-127">**이전 값:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="1548e-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="1548e-128">**새 값:** \<VirtualNetworkSitename="VNetUSWest" 위치 = "미국 서부"\></span><span class="sxs-lookup"><span data-stu-id="1548e-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="1548e-129">변경 내용을 저장하고 Azure에 네트워크 구성을 [가져옵니다](virtual-networks-using-network-configuration-file.md#import) .</span><span class="sxs-lookup"><span data-stu-id="1548e-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) the network configuration to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1548e-130">이 마이그레이션에서는 서비스 가동 중지 시간이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-130">This migration does NOT cause any downtime to your services.</span></span>
> 
> 

## <a name="what-to-do-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="1548e-131">선호도 그룹에 VM(클래식)이 있는 경우 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="1548e-131">What to do if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="1548e-132">현재 선호도 그룹에 있는 VM(클래식)을 선호도 그룹에서 제거할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-132">VMs (classic) that are currently in an affinity group do not need to be removed from the affinity group.</span></span> <span data-ttu-id="1548e-133">VM을 배포하면 단일 배율 단위에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-133">Once a VM is deployed, it is deployed to a single scale unit.</span></span> <span data-ttu-id="1548e-134">선호도 그룹이 새 VM 배포에 대해 사용 가능한 VM 크기의 집합을 제한할 수 있지만 배포된 모든 기존 VM은 VM이 배포되는 배율 단위에서 사용 가능한 VM 크기의 집합으로 이미 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-134">Affinity groups can restrict the set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted to the set of VM sizes available in the scale unit in which the VM is deployed.</span></span> <span data-ttu-id="1548e-135">배율 단위에 VM을 이미 배포했기 때문에, 선호도 그룹에서 VM을 제거해도 VM에 미치는 영향은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1548e-135">Because the VM is already deployed to a scale unit, removing a VM from an affinity group has no effect on the VM.</span></span>
