---
title: "Azure 가상 네트워크 (클래식)에서 선호도 그룹 tooa 지역 aaaMigrate | Microsoft Docs"
description: "가상 네트워크 (클래식)에서 선호도 toomigrate tooa 영역을 그룹화 하는 방법을 알아봅니다."
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
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="7b667-103">선호도 그룹 tooa 영역에서 가상 네트워크 (클래식)를 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7b667-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b667-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="7b667-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7b667-106">대부분의 새로운 배포 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="7b667-107">선호도 그룹 리소스 hello 동일한 선호도 그룹 물리적으로 서로 가까이 더욱 빠르게 이러한 리소스 toocommunicate를 사용 하도록 설정 하는 서버에서 호스트 내에서 생성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="7b667-108">지난 hello, 선호도 그룹과 가상 네트워크 (클래식)를 만들기 위한 요구 사항 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="7b667-109">그 당시 hello 네트워크 관리자 관리 서비스를 가상 네트워크 (클래식) 집합 물리적 서버 또는 배율 단위 내 에서만 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="7b667-110">아키텍처 향상으로 인해 네트워크 관리 tooa 영역의 hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="7b667-111">이러한 아키텍처 개선의 결과, 선호도 그룹이 더 이상 권장 사항이 아니며 가상 네트워크(클래식)에 필수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="7b667-112">가상 네트워크 (클래식)에 대 한 선호도 그룹의 hello 사용 지역으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="7b667-113">지역과 연결된 가상 네트워크(클래식)를 지역 가상 네트워크라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="7b667-114">일반적으로 선호도 그룹을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="7b667-115">Hello 가상 네트워크 요구 사항 외에도 선호도 그룹 했는데도 중요 한 toouse tooensure 리소스 (클래식)를 계산 및 저장소 (클래식) 등, 서로 가까이 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="7b667-116">그러나 현재 Azure 네트워크 아키텍처 hello와 이러한 배치 요구 사항을 더 이상 필요 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b667-117">여전히 기술적으로 가능 toocreate 가상 네트워크를 선호도 그룹과 연결 된 경우에 방법이 없는 매력적인 이유가 toodo 하므로.</span><span class="sxs-lookup"><span data-stu-id="7b667-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="7b667-118">네트워크 보안 그룹과 같은 다양한 가상 네트워크 기능은 지역 가상 네트워크를 사용하는 경우에만 사용할 수 있으며, 선호도 그룹과 연결된 가상 네트워크에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="7b667-119">Hello 네트워크 구성 파일 편집</span><span class="sxs-lookup"><span data-stu-id="7b667-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="7b667-120">Hello 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-120">Export hello network configuration file.</span></span> <span data-ttu-id="7b667-121">toolearn tooexport 네트워크 구성의 PowerShell을 사용 하 여 파일 또는 Azure CLI (명령줄 인터페이스) 1.0 hello 어떻게 참조 [네트워크 구성 파일을 사용 하 여 가상 네트워크 구성](virtual-networks-using-network-configuration-file.md#export)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="7b667-122">Hello 네트워크 구성 파일을 편집 대체 **AffinityGroup** 와 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="7b667-123">**Location**에 Azure [지역](https://azure.microsoft.com/regions)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7b667-124">hello **위치** 가상 네트워크 (클래식)와 연결 된 hello 선호도 그룹에 대해 지정한 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="7b667-125">예를 들어, 가상 네트워크 (클래식)를 마이그레이션할 때 West US에 있는 선호도 그룹과 연결 된 경우 프로그램 **위치** tooWest 미국 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="7b667-126">네트워크 구성 파일에 있는 줄을 다음, 사용자의 정보로 hello 값 대체 hello를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="7b667-127">**이전 값:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="7b667-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="7b667-128">**새 값:** \<VirtualNetworkSitename="VNetUSWest" 위치 = "미국 서부"\></span><span class="sxs-lookup"><span data-stu-id="7b667-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="7b667-129">변경 내용을 저장 하 고 [가져올](virtual-networks-using-network-configuration-file.md#import) 네트워크 구성 tooAzure hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="7b667-130">이 마이그레이션 가동 중지 시간 tooyour 서비스 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="7b667-131">선호도 그룹에 VM (클래식)이 있는 경우 어떤 toodo</span><span class="sxs-lookup"><span data-stu-id="7b667-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="7b667-132">현재 선호도 그룹에 있는 Vm (클래식) toobe hello 선호도 그룹에서 제거 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="7b667-133">VM을 배포한 후 배포 tooa 단일 배율 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="7b667-134">선호도 그룹에 새 VM 배포에 대 한 사용 가능한 VM 크기 집합이 hello 제한할 수 있지만 배포 된 모든 기존 VM 이미 제한 되어 toohello 집합이 VM 크기는 hello VM을 배포 하는 hello 배율 단위에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="7b667-135">VM은 이미 hello tooa 배율 단위 배포 때문에 hello VM에 영향을 주지에 선호도 그룹에서 VM을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b667-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
