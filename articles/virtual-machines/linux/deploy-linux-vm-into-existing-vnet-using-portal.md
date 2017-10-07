---
title: "Linux Vm의 경우 Azure 포털의 기존 네트워크에 aaaDeploy | Microsoft Docs"
description: "Hello 포털을 사용 하는 기존 Azure 가상 네트워크로 Linux VM을 배포 합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="ffb80-103">어떻게 toodeploy hello Azure 포털으로 기존 Azure 가상 네트워크로 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ffb80-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="ffb80-104">이 문서에서는 어떻게 toodeploy 기존 가상 네트워크 (VNet)로 가상 컴퓨터 (VM).</span><span class="sxs-lookup"><span data-stu-id="ffb80-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="ffb80-105">VNet 및 네트워크 보안 그룹과 같은 Azure 자산은 정적이고 거의 배포되지 않는 수명이 긴 리소스인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="ffb80-106">VNet에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 상수 재배포가 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="ffb80-107">기존의 행사로 VNet에 대해 생각 하드웨어 네트워크 스위치-필요는 없습니다 tooconfigure 각 배포와 새로운 하드웨어 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="ffb80-108">올바르게 구성 된 VNet에 계속할 수 있습니다 toodeploy 새 서버 해당 VNet에 반복 해 hello VNet의 hello 수명 기간 동안 필요한 경우에 자주 변경.</span><span class="sxs-lookup"><span data-stu-id="ffb80-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="ffb80-109">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb80-109">Create hello resource group</span></span>

<span data-ttu-id="ffb80-110">먼저 만듭니다 리소스 그룹 tooorganize이이 연습에서 만드는 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="ffb80-111">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffb80-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="ffb80-113">Hello VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb80-113">Create hello VNet</span></span>

<span data-ttu-id="ffb80-114">다음으로 VNet toolaunch hello를 Vm으로 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffb80-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="ffb80-115">hello VNet 서브넷 1 개를 포함 하 고 이후 단계에서이 서브넷 hello 네트워크 보안 그룹과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="ffb80-117">VNic toohello 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="ffb80-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="ffb80-118">가상 네트워크 카드 (VNics)은 중요 toodifferent Vm 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="ffb80-119">이 방법은 hello Vm 말할 수 하는 동안 정적 리소스로 hello VNic를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="ffb80-120">VNic 만들고 hello 이전 단계에서 만든 hello 서브넷과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="ffb80-122">Hello 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb80-122">Create hello network security group</span></span>

<span data-ttu-id="ffb80-123">Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="ffb80-124">Azure 네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffb80-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="ffb80-126">인바운드 SSH 허용 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="ffb80-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="ffb80-127">hello에서 액세스를 해야 하는 hello VM 인터넷, 인바운드 포트 22 트래픽 toobe 허용 하는 규칙이 VM이 생성 하는 hello hello 네트워크 tooport 22 통해 전달 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="ffb80-129">Hello 서브넷과 hello NSG 연결</span><span class="sxs-lookup"><span data-stu-id="ffb80-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="ffb80-130">VNet hello와 작성 hello 서브넷을 네트워크 보안 그룹을 hello hello 서브넷 연관 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="ffb80-131">네트워크 보안 그룹은 전체 서브넷 또는 개별 VNic와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="ffb80-132">Hello 방화벽 hello 서브넷 수준에서 트래픽을 필터링으로 모든 VNics 및 hello 서브넷 내에서 Vm hello hello 네트워크 보안 그룹에 의해 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="ffb80-133">hello 방법이 hello 네트워크 보안 그룹 되 고 단일 VNic 방금와 연결 된 하 고 하나의 VM을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="ffb80-135">Hello VNet에 VM hello 및 NSG를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="ffb80-136">Hello Linux VM에 기존 Azure 리소스 그룹, VNet, 서브넷 및 VNic 배포 toohello는 hello Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="ffb80-138">Hello 포털 toochoose 기존 리소스를 사용 하 여 hello 기존 네트워크 내부 Azure toodeploy hello VM 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="ffb80-139">VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffb80-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ffb80-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffb80-140">Next steps</span></span>

* [<span data-ttu-id="ffb80-141">Azure 리소스 관리자 템플릿 toocreate 특정 배포를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ffb80-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="ffb80-142">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb80-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="ffb80-143">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ffb80-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
