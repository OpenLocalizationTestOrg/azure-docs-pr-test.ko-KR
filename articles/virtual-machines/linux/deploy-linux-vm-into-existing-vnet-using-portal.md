---
title: "Azure Portal을 사용하여 기존 네트워크에 Linux VM 배포 | Microsoft Docs"
description: "포털을 사용하여 기존 Azure Virtual Network에 Linux VM을 배포합니다."
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
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="04922-103">Azure Portal을 사용하여 기존 Azure Virtual Network에 Linux 가상 컴퓨터를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="04922-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="04922-104">이 문서에서는 기존 VNet(가상 네트워크)에 VM(가상 컴퓨터)을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04922-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="04922-105">VNet 및 네트워크 보안 그룹과 같은 Azure 자산은 정적이고 거의 배포되지 않는 수명이 긴 리소스인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="04922-106">VNet을 배포하면 인프라에 어떤 부정적인 영향을 주지 않고 상수 재배포에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="04922-107">VNet을 기존 하드웨어 네트워크 스위치라고 생각하면 배포할 때마다 새로운 하드웨어 스위치를 구성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04922-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="04922-108">올바르게 구성된 VNet으로 VNet에 반복하여 VNet의 수명 동안 필요한 변경 사항을 포함하는 새 서버를 계속 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="04922-109">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-109">Create the resource group</span></span>

<span data-ttu-id="04922-110">먼저 리소스 그룹을 만들어서 연습에서 만드는 모든 항목을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="04922-111">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04922-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="04922-113">VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-113">Create the VNet</span></span>

<span data-ttu-id="04922-114">다음으로 VM을 시작할 VNet을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="04922-115">VNet은 서브넷 1개를 포함하며, 이후 단계에서 이 서브넷이 포함된 네트워크 보안 그룹에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="04922-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="04922-117">서브넷에 VNic 추가</span><span class="sxs-lookup"><span data-stu-id="04922-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="04922-118">가상 네트워크 카드(VNic)는 다른 VM에 연결할 수 있으므로 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="04922-119">이 방법을 통해 VM이 임시 리소스가 되는 동안 vNic를 정적 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="04922-120">VNic를 만들고 이전 단계에서 만든 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="04922-122">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-122">Create the network security group</span></span>

<span data-ttu-id="04922-123">Azure 네트워크 보안 그룹은 네트워크 계층에서 방화벽과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="04922-124">Azure 네트워크 보안 그룹에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04922-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="04922-126">인바운드 SSH 허용 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="04922-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="04922-127">VM은 인터넷에서 액세스를 해야 하므로 인바운드 포트 22 트래픽이 VM의 포트 22에 대한 네트워크를 통해 전달되도록 허용하는 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="04922-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="04922-129">서브넷과 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="04922-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="04922-130">VNet 및 서브넷이 만들어졌다면 네트워크 보안 그룹을 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="04922-131">네트워크 보안 그룹은 전체 서브넷 또는 개별 VNic와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="04922-132">서브넷 수준에서 방화벽 필터링 트래픽을 사용할 경우 서브넷 내의 모든 VNic 및 VM이 네트워크 보안 그룹에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="04922-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="04922-133">다른 방법은 네트워크 보안 그룹이 단일 VNic와만 연결되어 하나의 VM만 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04922-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="04922-135">VNet 및 NSG에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="04922-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="04922-136">Azure Portal을 사용하여 기존 Azure 리소스 그룹, VNet, 서브넷 및 VNic에 Linux VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="04922-138">기존 리소스를 선택하려면 포털을 사용하여 Azure에서 기존 네트워크 내에 VM을 배포하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="04922-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="04922-139">VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04922-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="04922-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04922-140">Next steps</span></span>

* [<span data-ttu-id="04922-141">Azure Resource Manager 템플릿을 사용하여 특정 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="04922-142">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="04922-143">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="04922-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
