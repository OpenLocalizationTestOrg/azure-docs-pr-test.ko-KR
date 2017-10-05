---
title: "여러 NIC를 사용하여 Azure에서 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 또는 Resource Manager 템플릿을 사용하여 여러 NIC가 연결된 Linux VM을 만드는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="43ef9-103">Azure CLI 1.0을 사용하여 다중 NIC가 있는 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="43ef9-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="43ef9-104">Azure에서 여러 가상 NIC(네트워크 인터페이스)가 연결된 VM(가상 컴퓨터)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="43ef9-105">일반적인 시나리오는 프런트 엔드 및 백 엔드 연결에 다른 서브넷을 사용하거나 모니터링 또는 백업 솔루션 전용 네트워크를 두는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="43ef9-106">이 문서에서는 여러 NIC가 연결된 VM을 만드는 빠른 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="43ef9-107">자체 Bash 스크립트 내에서 여러 NIC를 만드는 방법을 비롯한 자세한 내용은 [다중 NIC VM 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="43ef9-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="43ef9-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="43ef9-109">VM을 만들 때 여러 NIC를 연결해야 합니다. Azure CLI 1.0을 사용하여 기존 VM에 NIC를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="43ef9-110">[Azure CLI 2.0을 사용해서 기존 VM에 NIC를 추가](multiple-nics.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="43ef9-111">또한 [가상 디스크에 따라 VM을 만들고](copy-vm.md) VM을 배포할 때 여러 NIC를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="43ef9-112">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="43ef9-112">CLI versions to complete the task</span></span>
<span data-ttu-id="43ef9-113">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="43ef9-114">[Azure CLI 1.0](#create-supporting-resources) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="43ef9-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="43ef9-115">[Azure CLI 2.0](multiple-nics.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="43ef9-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="43ef9-116">지원 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="43ef9-116">Create supporting resources</span></span>
<span data-ttu-id="43ef9-117">[Azure CLI](../../cli-install-nodejs.md)에 로그인되어 있고 리소스 관리자 모드를 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="43ef9-118">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="43ef9-119">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="43ef9-120">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-120">First, create a resource group.</span></span> <span data-ttu-id="43ef9-121">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="43ef9-122">VM을 보유할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="43ef9-123">다음 예제에서는 *mystorageaccount*라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="43ef9-124">VM을 연결할 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="43ef9-125">다음 예제는 주소 접두사 *192.168.0.0/16*으로 *myVnet*이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="43ef9-126">두 개의 가상 네트워크 서브넷(프런트 엔드 트래픽용 및 백 엔드 트래픽용)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="43ef9-127">다음 예제에서는 두 서브넷 *mySubnetFrontEnd* 및 *mySubnetBackEnd*를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="43ef9-128">여러 NIC 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="43ef9-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="43ef9-129">모든 NIC 생성을 반복하는 프로세스 스크립팅을 포함하여 [Azure CLI를 사용하여 여러 NIC 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)에 대한 자세한 정보를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="43ef9-130">다음 예제에서는 *myNic1* 및 *myNic2*라는 2개의 NIC를 만들며 하나의 NIC가 각 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="43ef9-131">또한 일반적으로 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 또는 [부하 분산 장치](../../load-balancer/load-balancer-overview.md)를 만들어 VM에서 트래픽을 관리하고 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="43ef9-132">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="43ef9-133">`azure network nic set`을 사용하여 NIC를 네트워크 보안 그룹에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="43ef9-134">다음 예제에서는 *myNic1* 및 *myNic2*를 *myNetworkSecurityGroup*에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="43ef9-135">VM 만들기 및 NIC 연결</span><span class="sxs-lookup"><span data-stu-id="43ef9-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="43ef9-136">VM을 만들 때 이제 여러 NIC를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="43ef9-137">`--nic-name`을 사용하여 단일 NIC를 제공하는 대신, `--nic-names`를 사용하고 쉼표로 구분된 NIC 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="43ef9-138">또한 VM 크기를 선택할 때도 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="43ef9-139">VM에 추가할 수 있는 NIC 총수가 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="43ef9-140">[Linux VM 크기](sizes.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="43ef9-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="43ef9-141">다음 예제에서는 여러 NIC를 지정하는 방법과 여러 NIC의 사용을 지원하는 VM 크기를 보여 줍니다(*Standard_DS2_v2*).</span><span class="sxs-lookup"><span data-stu-id="43ef9-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="43ef9-142">Resource Manager 템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="43ef9-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="43ef9-143">Azure Resource Manager 템플릿은 선언적 JSON 파일을 사용하여 환경을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="43ef9-144">[Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)에 대해 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="43ef9-145">Resource Manager 템플릿은 여러 NIC를 만드는 것과 같이 배포하는 동안 리소스의 여러 인스턴스를 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="43ef9-146">*복사* 를 사용하여 만들 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="43ef9-147">[*복사*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="43ef9-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="43ef9-148">`copyIndex()`를 사용하여 리소스 이름에 번호를 추가할 수도 있습니다. 이와 같이 `myNic1`, `myNic2` 등을 만들 수 있습니다. 다음은 인덱스 값을 추가하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="43ef9-149">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43ef9-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43ef9-150">Next steps</span></span>
<span data-ttu-id="43ef9-151">여러 NIC를 사용하여 VM을 만들려고 할 때 [Linux VM 크기](sizes.md) 를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="43ef9-152">각 VM 크기가 지원하는 NIC의 최대 수에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="43ef9-153">기존 VM에 NIC를 더 추가할 수 없으므로 VM을 배포할 때 모든 NIC를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="43ef9-154">배포를 계획할 때 처음부터 필요한 모든 네트워크 연결이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="43ef9-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

