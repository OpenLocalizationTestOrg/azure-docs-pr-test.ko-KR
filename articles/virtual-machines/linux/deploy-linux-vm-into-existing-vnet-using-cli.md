---
title: "Azure CLI 2.0으로 기존 네트워크에 Linux VM 배포 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 기존 가상 네트워크에 Linux 가상 컴퓨터를 배포하는 방법에 알아봅니다."
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="d4cac-103">Azure CLI를 사용하여 기존 Azure Virtual Network에 Linux 가상 컴퓨터를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4cac-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="d4cac-104">이 문서에서는 Azure CLI 2.0을 사용하여 기존 가상 네트워크에 VM(가상 컴퓨터)을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="d4cac-105">요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-105">The requirements are:</span></span>

- [<span data-ttu-id="d4cac-106">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="d4cac-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="d4cac-107">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="d4cac-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="d4cac-108">[Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="d4cac-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="d4cac-109">Quick Commands</span></span>
<span data-ttu-id="d4cac-110">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 필요한 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="d4cac-111">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#detailed-walkthrough) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="d4cac-112">이 사용자 지정 환경을 만들려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d4cac-113">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d4cac-114">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="d4cac-115">**사전 요구 사항:** Azure 리소스 그룹, 가상 네트워크 및 서브넷, 인바운드 SSH가 있는 네트워크 보안 그룹, 가상 네트워크 인터페이스 카드.</span><span class="sxs-lookup"><span data-stu-id="d4cac-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="d4cac-116">가상 네트워크 인프라에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="d4cac-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="d4cac-117">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="d4cac-117">Detailed walkthrough</span></span>

<span data-ttu-id="d4cac-118">가상 네트워크 및 네트워크 보안 그룹과 같은 Azure 자산이 정적이고 거의 배포되지 않은 수명이 긴 리소스인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="d4cac-119">가상 네트워크를 배포하면 인프라에 어떤 부정적인 영향을 주지 않고 새 배포에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="d4cac-120">가상 네트워크를 기존 하드웨어 네트워크 스위치라고 생각하면 배포할 때마다 새로운 하드웨어 스위치를 구성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="d4cac-121">올바르게 구성된 가상 네트워크로 가상 네트워크에 반복하여 가상 네트워크의 수명 동안 필요한 변경 사항을 포함하는 새 VM을 계속 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="d4cac-122">이 사용자 지정 환경을 만들려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d4cac-123">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d4cac-124">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="d4cac-125">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-125">Create the resource group</span></span>

<span data-ttu-id="d4cac-126">먼저 Azure 리소스 그룹을 만들어서 연습에서 만드는 모든 항목을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="d4cac-127">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d4cac-128">[az group create](/cli/azure/group#create)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d4cac-129">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="d4cac-130">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-130">Create the virtual network</span></span>

<span data-ttu-id="d4cac-131">VM가 Azure 가상 네트워크 내에서 시작되도록 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="d4cac-132">Azure 가상 네트워크에 대한 자세한 내용은 [Azure CLI를 사용하여 가상 네트워크 만들기](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="d4cac-133">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="d4cac-134">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="d4cac-135">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-135">Create the network security group</span></span>

<span data-ttu-id="d4cac-136">Azure 네트워크 보안 그룹은 네트워크 계층에서 방화벽과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="d4cac-137">네트워크 보안 그룹에 대한 자세한 내용은 [Azure CLI에서 네트워크 보안 그룹을 만드는 방법](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="d4cac-138">[az network nsg create](/cli/azure/network/nsg#create)를 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="d4cac-139">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="d4cac-140">인바운드 SSH 허용 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="d4cac-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="d4cac-141">VM은 인터넷에서 액세스를 해야 하므로 인바운드 포트 22 트래픽이 VM의 포트 22에 대한 네트워크를 통해 전달되도록 허용하는 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="d4cac-142">[az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 네트워크 보안 그룹에 대해 인바운드 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="d4cac-143">다음 예제에서는 *myNetworkSecurityGroupRuleSSH*이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="d4cac-144">네트워크 보안 그룹에 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="d4cac-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="d4cac-145">네트워크 보안 그룹 규칙을 서브넷 또는 특정 가상 네트워크 인터페이스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="d4cac-146">네트워크 보안 그룹을 서브넷에 연결하게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="d4cac-147">[az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update)로 서브넷을 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="d4cac-148">가상 네트워크 인터페이스 카드를 서브넷에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="d4cac-149">가상 네트워크 인터페이스 카드(VNic)는 다른 VM에 연결하여 다시 사용할 수 있기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="d4cac-150">이렇게 다시 사용하면 VM이 임시 리소스가 되는 동안 VNic를 정적 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="d4cac-151">VNic를 만들고 [az network nic create](/cli/azure/network/nic#create)로 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="d4cac-152">다음 예제는 *myNic*라는 VNic를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="d4cac-153">가상 네트워크 인프라에 VM 배포</span><span class="sxs-lookup"><span data-stu-id="d4cac-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="d4cac-154">이제 가상 네트워크, 서브넷 및 네트워크 보안 그룹이 SSH에 대한 포트 22를 제외한 모든 인바운드 트래픽을 차단하여 서브넷을 보호하는 역할을 하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="d4cac-155">이제 이 기존 네트워크 인프라 내에 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="d4cac-156">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d4cac-157">전체 VM을 배포하기 위해 Azure CLI 2.0과 함께 사용하는 플래그에 대한 자세한 내용은 [Azure CLI를 사용하여 전체 Linux 환경 만들기](create-cli-complete.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="d4cac-158">다음 예제는 Azure Managed Disks를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="d4cac-159">이들 디스크는 Azure 플랫폼을 통해 처리되며 디스크를 저장할 위치나 준비가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="d4cac-160">관리 디스크에 대한 자세한 내용은 [Azure Managed Disks 개요](../../storage/storage-managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="d4cac-161">관리되지 않는 디스크를 사용하려는 경우 아래의 추가 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="d4cac-162">관리 디스크를 사용하는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="d4cac-163">관리되지 않는 디스크를 사용하려는 경우 다음과 같은 추가 매개 변수를 진행 명령에 추가하여 `mystorageaccount`라는 저장소 계정에 관리되지 않는 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="d4cac-164">기존 리소스를 호출하기 위해 CLI 플래그를 사용하여 Azure에서 기존 네트워크 내에 VM을 배포하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="d4cac-165">가상 네트워크 및 서브넷이 배포되면 Azure 지역 내에서 정적 또는 영구적으로 리소스로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="d4cac-166">이 예제에서는 VNic에 공용 IP 주소를 만들어 할당하지 않았기 때문에 이 VM은 인터넷을 통해 공개적으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cac-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="d4cac-167">자세한 내용은 [Azure CLI을 사용하여 고정 공용 IP가 있는 VM 만들기](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4cac-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4cac-168">Next steps</span></span>
<span data-ttu-id="d4cac-169">Azure에서 가상 컴퓨터를 만드는 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cac-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="d4cac-170">Azure Resource Manager 템플릿을 사용하여 특정 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="d4cac-171">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="d4cac-172">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cac-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
