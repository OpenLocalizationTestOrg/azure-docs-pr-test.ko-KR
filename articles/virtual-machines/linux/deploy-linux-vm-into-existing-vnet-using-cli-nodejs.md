---
title: "Azure CLI 1.0으로 기존 네트워크에 Linux VM 배포 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 기존 가상 네트워크에 Linux VM을 배포하는 방법"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="91f27-103">Azure CLI 1.0을 사용하여 기존 Azure Virtual Network에 Linux 가상 컴퓨터를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="91f27-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="91f27-104">이 문서에서는 Azure CLI 1.0을 사용하여 기존 VNet(가상 네트워크)에 VM(가상 컴퓨터)을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="91f27-105">요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-105">The requirements are:</span></span>

- [<span data-ttu-id="91f27-106">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="91f27-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="91f27-107">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="91f27-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="91f27-108">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="91f27-108">CLI versions to complete the task</span></span>
<span data-ttu-id="91f27-109">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="91f27-110">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="91f27-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="91f27-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="91f27-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="91f27-112">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="91f27-112">Quick Commands</span></span>

<span data-ttu-id="91f27-113">태스크를 빠르게 완료해야 하는 경우 다음 섹션에서 필요한 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="91f27-114">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="91f27-115">필수 구성 요소: SSH 인바운드를 사용하는 NSG, 리소스 그룹, VNet, 서브넷.</span><span class="sxs-lookup"><span data-stu-id="91f27-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="91f27-116">모든 예제를 고유한 설정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="91f27-117">가상 네트워크 인프라에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="91f27-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="91f27-118">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="91f27-118">Detailed walkthrough</span></span>

<span data-ttu-id="91f27-119">VNet 및 네트워크 보안 그룹과 같은 Azure 자산은 정적이고 거의 배포되지 않는 수명이 긴 리소스인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="91f27-120">VNet을 배포하면 인프라에 어떤 부정적인 영향을 주지 않고 새 배포에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="91f27-121">VNet를 기존 하드웨어 네트워크 스위치로 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="91f27-122">각 배포에 대해 새로운 하드웨어 스위치를 구성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="91f27-123">올바르게 구성된 VNet으로 VNet에 반복하여 VNet의 수명 동안 필요한 변경 사항을 포함하는 새 서버를 계속 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="91f27-124">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-124">Create the resource group</span></span>

<span data-ttu-id="91f27-125">먼저 리소스 그룹을 만들어서 연습에서 만드는 모든 항목을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="91f27-126">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="91f27-127">VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-127">Create the VNet</span></span>

<span data-ttu-id="91f27-128">첫 번째 단계는 VM을 시작할 VNet을 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="91f27-129">VNet은 이 연습을 위한 서브넷을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="91f27-130">Azure VNet에 대한 자세한 내용은 [Azure CLI를 사용하여 가상 네트워크 만들기](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="91f27-131">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-131">Create the network security group</span></span>

<span data-ttu-id="91f27-132">서브넷은 기존 네트워크 보안 그룹을 기초로 빌드되므로 서브넷 전에 네트워크 보안 그룹을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="91f27-133">Azure 네트워크 보안 그룹은 네트워크 계층에서 방화벽과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="91f27-134">Azure 네트워크 보안 그룹에 대한 자세한 내용은 [Azure CLI에서 네트워크 보안 그룹을 만드는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="91f27-135">인바운드 SSH 허용 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="91f27-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="91f27-136">VM은 인터넷에서 액세스를 해야 하므로 인바운드 포트 22 트래픽이 VM의 포트 22에 대한 네트워크를 통해 전달되도록 허용하는 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="91f27-137">VNet에 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="91f27-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="91f27-138">VNet 내의 VM은 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="91f27-139">각 VNet에는 여러 개의 서브넷이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="91f27-140">서브넷을 만들고 네트워크 보안 그룹과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="91f27-141">이제 서브넷은 VNet 내에 추가되고 네트워크 보안 그룹 및 규칙과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="91f27-142">서브넷에 VNic 추가</span><span class="sxs-lookup"><span data-stu-id="91f27-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="91f27-143">가상 네트워크 카드(VNic)는 다른 VM에 연결하여 다시 사용할 수 있기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="91f27-144">이 방법을 통해 VM이 임시 리소스가 되는 동안 vNic를 정적 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="91f27-145">VNic를 만들고 이전 단계에서 만든 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="91f27-146">VNet 및 NSG에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="91f27-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="91f27-147">이제 VNet, VNet 내부의 서브넷 및 네트워크 보안 그룹이 SSH에 대한 포트 22를 제외한 모든 인바운드 트래픽을 차단하여 서브넷을 보호하는 역할을 하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="91f27-148">이제 이 기존 네트워크 인프라 내에 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="91f27-149">Azure CLI 및 `azure vm create` 명령을 사용하여 기존 Azure 리소스 그룹, VNet, 서브넷 및 VNic에 Linux VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="91f27-150">전체 VM을 배포하기 위해 CLI를 사용하는 방법에 대한 자세한 내용은 [Azure CLI를 사용하여 전체 Linux 환경 만들기](create-cli-complete.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91f27-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="91f27-151">기존 리소스를 호출하기 위해 CLI 플래그를 사용하여 Azure에서 기존 네트워크 내에 VM을 배포하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="91f27-152">VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91f27-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="91f27-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91f27-153">Next steps</span></span>

* [<span data-ttu-id="91f27-154">Azure Resource Manager 템플릿을 사용하여 특정 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="91f27-155">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="91f27-156">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="91f27-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
