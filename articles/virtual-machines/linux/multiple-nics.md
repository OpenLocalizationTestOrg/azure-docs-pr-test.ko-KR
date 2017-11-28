---
title: "여러 NIC를 사용하여 Azure에서 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 2.0 또는 Resource Manager 템플릿을 사용하여 여러 NIC가 있는 Linux VM을 만드는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="6ab3c-103">여러 네트워크 인터페이스 카드를 사용하여 Azure에서 Linux 가상 컴퓨터를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="6ab3c-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="6ab3c-104">Azure에서 여러 가상 NIC(네트워크 인터페이스)가 연결된 VM(가상 컴퓨터)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="6ab3c-105">일반적인 시나리오는 프런트 엔드 및 백 엔드 연결에 다른 서브넷을 사용하거나 모니터링 또는 백업 솔루션 전용 네트워크를 두는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="6ab3c-106">이 문서에서는 여러 NIC가 연결되어 있는 VM을 만드는 방법과 기존 VM에서 NIC를 추가 또는 제거하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="6ab3c-107">자체 Bash 스크립트 내에서 여러 NIC를 만드는 방법을 비롯한 자세한 내용은 [다중 NIC VM 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="6ab3c-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="6ab3c-109">이 문서에서는 Azure CLI 2.0을 사용하여 여러 NIC가 있는 VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="6ab3c-110">[Azure CLI 1.0](multiple-nics-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="6ab3c-111">지원 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab3c-111">Create supporting resources</span></span>
<span data-ttu-id="6ab3c-112">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6ab3c-113">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6ab3c-114">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="6ab3c-115">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6ab3c-116">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="6ab3c-117">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="6ab3c-118">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnetFrontEnd*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="6ab3c-119">[az network vnet subnet create](/cli/azure/network/vnet/subnet#create)를 사용하여 백 엔드 트래픽에 대한 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="6ab3c-120">다음 예제에서는 *mySubnetBackEnd*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="6ab3c-121">[az network nsg create](/cli/azure/network/nsg#create)를 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="6ab3c-122">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="6ab3c-123">여러 NIC 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="6ab3c-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="6ab3c-124">[az network nic create](/cli/azure/network/nic#create)를 사용하여 두 개의 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="6ab3c-125">다음 예제는 네트워크 보안 그룹에 연결된 *myNic1* 및 *myNic2*라는 2개의 NIC를 만들며 하나의 NIC가 각 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="6ab3c-126">VM 만들기 및 NIC 연결</span><span class="sxs-lookup"><span data-stu-id="6ab3c-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="6ab3c-127">VM을 만들 때 `--nics`로 만든 NIC를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="6ab3c-128">또한 VM 크기를 선택할 때도 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="6ab3c-129">VM에 추가할 수 있는 NIC 총수가 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="6ab3c-130">[Linux VM 크기](sizes.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="6ab3c-131">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6ab3c-132">다음 예제에서는 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-132">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="6ab3c-133">VM에 NIC 추가</span><span class="sxs-lookup"><span data-stu-id="6ab3c-133">Add a NIC to a VM</span></span>
<span data-ttu-id="6ab3c-134">이전 단계에서는 여러 NIC가 있는 VM을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="6ab3c-135">Azure CLI 2.0을 사용해서 기존 VM에 NIC를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="6ab3c-136">[az network nic create](/cli/azure/network/nic#create)를 사용하여 다른 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="6ab3c-137">다음 예제에서는 이전 단계에서 만든 백 엔드 서브넷 및 네트워크 보안 그룹에 연결된 *myNic3*라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="6ab3c-138">기존 VM에 NIC를 추가하려면 먼저 [az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="6ab3c-139">다음 예제에서는 *myVM*이라는 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6ab3c-140">[az vm nic add](/cli/azure/vm/nic#add)를 사용하여 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="6ab3c-141">다음 예제에서는 *myNic3*를 *myVM*에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="6ab3c-142">[az vm start](/cli/azure/vm#start)를 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="6ab3c-143">VM에서 NIC 제거</span><span class="sxs-lookup"><span data-stu-id="6ab3c-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="6ab3c-144">기존 VM에사 NIC를 제거하려면 먼저 [az vm deallocate](/cli/azure/vm#deallocate)를 사용하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="6ab3c-145">다음 예제에서는 *myVM*이라는 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6ab3c-146">[az vm nic remove](/cli/azure/vm/nic#remove)를 사용하여 NIC를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="6ab3c-147">다음 예제에서는 *myVM*에서 *myNic3*를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="6ab3c-148">[az vm start](/cli/azure/vm#start)를 사용하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="6ab3c-149">Resource Manager 템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab3c-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="6ab3c-150">Azure Resource Manager 템플릿은 선언적 JSON 파일을 사용하여 환경을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="6ab3c-151">[Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)에 대해 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6ab3c-152">Resource Manager 템플릿은 여러 NIC를 만드는 것과 같이 배포하는 동안 리소스의 여러 인스턴스를 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="6ab3c-153">*복사* 를 사용하여 만들 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="6ab3c-154">[*복사*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="6ab3c-155">`copyIndex()`를 사용하여 리소스 이름에 번호를 추가할 수도 있습니다. 이와 같이 `myNic1`, `myNic2` 등을 만들 수 있습니다. 다음은 인덱스 값을 추가하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="6ab3c-156">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ab3c-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ab3c-157">Next steps</span></span>
<span data-ttu-id="6ab3c-158">여러 NIC를 사용하여 VM을 만들려고 할 때 [Linux VM 크기](sizes.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="6ab3c-159">각 VM 크기가 지원하는 NIC의 최대 수에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab3c-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 