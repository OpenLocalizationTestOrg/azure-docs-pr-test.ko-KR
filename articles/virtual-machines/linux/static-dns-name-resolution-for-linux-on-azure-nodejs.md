---
title: "Azure에서 VM 이름 확인을 위해 내부 DNS 사용 | Microsoft Docs"
description: "Azure에서 VM 이름 확인을 위해 내부 DNS 사용"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="12156-103">Azure에서 VM 이름 확인을 위해 내부 DNS 사용</span><span class="sxs-lookup"><span data-stu-id="12156-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="12156-104">이 문서에서는 가상 NIC 카드(VNic) 및 DNS 레이블 이름을 사용하여 Linux VM에 대해 정적 내부 DNS 이름을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12156-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="12156-105">정적 DNS 이름은 이 문서에서 사용되는 Jenkins 빌드 서버 또는 Git 서버와 같은 영구 인프라 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="12156-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="12156-106">요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-106">The requirements are:</span></span>

* [<span data-ttu-id="12156-107">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="12156-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="12156-108">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="12156-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="12156-109">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="12156-109">CLI versions to complete the task</span></span>
<span data-ttu-id="12156-110">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="12156-111">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="12156-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="12156-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="12156-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="12156-113">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="12156-113">Quick commands</span></span>

<span data-ttu-id="12156-114">태스크를 빠르게 완료해야 하는 경우 다음 섹션에서 필요한 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="12156-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="12156-115">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#detailed-walkthrough) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12156-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="12156-116">사전 요구 사항: SSH 인바운드를 사용하는 NSG, 리소스 그룹, VNet, 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="12156-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="12156-117">정적 내부 DNS 이름으로 VNic 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="12156-118">`-r` cli 플래그는 VNic에 대한 정적 DNS 이름을 제공하는 DNS 레이블을 설정하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12156-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="12156-119">VNet, NSG에 VM 배포 및 VNic 연결</span><span class="sxs-lookup"><span data-stu-id="12156-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="12156-120">`-N`은 Azure에 배포하는 동안 새 VM에 VNic를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="12156-121">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="12156-121">Detailed walkthrough</span></span>

<span data-ttu-id="12156-122">Azure에서 전체 CiCd(지속적인 통합 및 지속적인 배포) 인프라는 특정 서버가 정적이거나 서버의 수명이 길어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="12156-123">VNet(Virtual Network) 및 NSG(네트워크 보안 그룹)와 같은 Azure 자산이 정적이고 거의 배포되지 않은 수명이 긴 리소스인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="12156-124">VNet을 배포하면 인프라에 어떤 부정적인 영향을 주지 않고 새 배포에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="12156-125">이 정적 네트워크에 Git 리포지토리 서버 및 Jenkins 자동화 서버를 추가하면 개발 또는 테스트 환경에 CiCd를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="12156-126">내부 DNS 이름은 Azure Virtual Network 내에서만 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="12156-127">DNS 이름은 내부용이므로 외부 인터넷에서 확인할 수 없으며 인프라에 대한 추가 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="12156-128">_모든 예제를 고유한 이름으로 바꿉니다._</span><span class="sxs-lookup"><span data-stu-id="12156-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="12156-129">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-129">Create the Resource group</span></span>

<span data-ttu-id="12156-130">리소스 그룹은 이 연습에서 만드는 모든 항목을 구성하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="12156-131">Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12156-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="12156-132">VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-132">Create the VNet</span></span>

<span data-ttu-id="12156-133">첫 번째 단계는 VM을 시작할 VNet을 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12156-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="12156-134">VNet은 이 연습을 위한 서브넷을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="12156-135">Azure VNet에 대한 자세한 내용은 [Azure CLI를 사용하여 가상 네트워크 만들기](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12156-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="12156-136">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-136">Create the NSG</span></span>

<span data-ttu-id="12156-137">서브넷은 기존 네트워크 보안 그룹을 기초로 빌드되므로 서브넷 전에 NSG를 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="12156-138">Azure NSG는 네트워크 계층에서 방화벽과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="12156-139">Azure NSG에 대한 자세한 내용은 [Azure CLI에서 NSG를 만드는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12156-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="12156-140">인바운드 SSH 허용 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="12156-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="12156-141">Linux VM은 인터넷에서 액세스를 해야 하므로 인바운드 포트 22 트래픽이 Linux VM의 포트 22에 대한 네트워크를 통해 전달되도록 허용하는 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="12156-142">VNet에 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="12156-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="12156-143">VNet 내의 VM은 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="12156-144">각 VNet에는 여러 개의 서브넷이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="12156-145">서브넷을 만들고 서브넷을 NSG와 연결하여 서브넷에 방화벽을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="12156-146">이제 서브넷은 VNet 내에 추가되고 NSG와 NSG 규칙과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="12156-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="12156-147">정적 DNS 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-147">Creating static DNS names</span></span>

<span data-ttu-id="12156-148">Azure는 매우 유연하지만 VM 이름 확인을 위해 DNS 이름을 사용하려면 DNS 레이블 지정을 사용하여 VNic(가상 네트워크 카드)로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="12156-149">VNic는 다른 VM에 연결하여 다시 사용할 수 있으므로 중요합니다. 그렇기 때문에 VM이 임시일 수 있는 반면 VNic는 고정 리소스로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="12156-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="12156-150">VNic에 DNS 레이블 지정을 사용하여 VNet의 다른 VM에서 간단한 이름 확인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="12156-151">확인 가능한 이름을 사용하면 다른 VM에서 DNS 이름 `Jenkins`로 자동화 서버에 액세스하거나 `gitrepo`로 Git 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="12156-152">VNic를 만들고 이전 단계에서 만든 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="12156-153">VNet 및 NSG에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="12156-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="12156-154">이제 VNet, 해당 VNet 내부의 서브넷 및 NSG가 SSH에 대한 포트 22를 제외한 모든 인바운드 트래픽을 차단하여 서브넷을 보호하는 방화벽의 역할을 하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12156-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="12156-155">이제 이 기존 네트워크 인프라 내에 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="12156-156">Azure CLI 및 `azure vm create` 명령을 사용하여 기존 Azure 리소스 그룹, VNet, 서브넷 및 VNic에 Linux VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="12156-157">전체 VM을 배포하기 위해 CLI를 사용하는 방법에 대한 자세한 내용은 [Azure CLI를 사용하여 전체 Linux 환경 만들기](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12156-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="12156-158">기존 리소스를 호출하기 위해 CLI 플래그를 사용하여 Azure에서 기존 네트워크 내에 VM을 배포하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="12156-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="12156-159">다시 말해, VNet 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12156-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="12156-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12156-160">Next steps</span></span>
* [<span data-ttu-id="12156-161">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="12156-162">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="12156-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
