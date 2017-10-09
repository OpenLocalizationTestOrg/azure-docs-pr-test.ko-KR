---
title: "여러 Nic 사용 하 여 Azure에서 Linux VM aaaCreate | Microsoft Docs"
description: "여러 Nic 사용 하 여 Linux VM toocreate tooit hello Azure CLI 2.0 또는 리소스 관리자 템플릿을 사용 하 여 연결 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="a2ab6-103">여러 네트워크와 Azure에서 Linux 가상 컴퓨터를 toocreate 인터페이스 카드 방법</span><span class="sxs-lookup"><span data-stu-id="a2ab6-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="a2ab6-104">여러 가상 네트워크 인터페이스 (Nic) 연결 된 tooit가 Azure에서 가상 컴퓨터 (VM)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="a2ab6-105">일반적인 시나리오는 toohave 프런트 엔드 및 백 엔드 연결에 대 한 서로 다른 서브넷 또는 네트워크를 전용 tooa 모니터링 또는 백업 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="a2ab6-106">이 문서에 설명 하 고 여러 Nic 사용 하 여 VM toocreate tooit 연결 방법 기존 VM에서 Nic tooadd 또는 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="a2ab6-107">자세한 정보에 대 한 방법을 toocreate 자신의 내에서 여러 Nic를 이용한 적 비롯 하 여 스크립트에 대해 자세히 알아보세요 [다중 NIC Vm을 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="a2ab6-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="a2ab6-109">이 문서와 여러 Nic 사용 하 여 VM a toocreate Azure CLI 2.0 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="a2ab6-110">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](multiple-nics-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="a2ab6-111">지원 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="a2ab6-111">Create supporting resources</span></span>
<span data-ttu-id="a2ab6-112">최신 설치 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a2ab6-113">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a2ab6-114">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="a2ab6-115">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a2ab6-116">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a2ab6-117">Hello 가상 네트워크를 만듭니다 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a2ab6-118">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 와 명명 된 서브넷 *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="a2ab6-119">사용 하 여 백 엔드 트래픽 hello에 대 한 서브넷을 만든 [만드는 az 네트워크 vnet 서브넷](/cli/azure/network/vnet/subnet#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="a2ab6-120">hello 다음 예제에서는 서브넷을 만듭니다. 명명 된 *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="a2ab6-121">[az network nsg create](/cli/azure/network/nsg#create)를 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="a2ab6-122">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="a2ab6-123">여러 NIC 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="a2ab6-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="a2ab6-124">[az network nic create](/cli/azure/network/nic#create)를 사용하여 두 개의 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="a2ab6-125">hello 다음 예제에서는 라는 두 개의 nic가 *myNic1* 및 *myNic2*관계, hello 네트워크 보안 그룹을 tooeach 서브넷 연결 NIC 1 개:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

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

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="a2ab6-126">VM을 만들고 hello Nic 연결</span><span class="sxs-lookup"><span data-stu-id="a2ab6-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="a2ab6-127">Hello Nic 지정 hello VM을 만들 때 사용 하 여 만든 `--nics`합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="a2ab6-128">또한 해야 tootake 주의 hello v M 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="a2ab6-129">hello tooa VM을 추가할 수 있는 Nic의 총 수에 대 한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="a2ab6-130">[Linux VM 크기](sizes.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="a2ab6-131">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a2ab6-132">hello 다음 예제에서는 V *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-132">hello following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="a2ab6-133">NIC tooa VM 추가</span><span class="sxs-lookup"><span data-stu-id="a2ab6-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="a2ab6-134">여러 Nic를 사용 하 여 VM을 만든 hello 이전 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="a2ab6-135">또한 Nic tooan hello Azure CLI 2.0 함께 존재 하는 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="a2ab6-136">[az network nic create](/cli/azure/network/nic#create)를 사용하여 다른 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="a2ab6-137">hello 다음 예제에서는 명명 된 NIC *myNic3* toohello 백 엔드 서브넷과 hello 이전 단계에서 만든 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="a2ab6-138">NIC tooan tooadd 기존의 VM에 할당을 먼저 해제의 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="a2ab6-139">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a2ab6-140">추가 인 NIC와 hello [az vm nic 추가](/cli/azure/vm/nic#add)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="a2ab6-141">hello 다음 예제에서는 추가 *myNic3* 너무*myVM*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="a2ab6-142">시작의 VM hello [az vm 시작](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="a2ab6-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="a2ab6-143">VM에서 NIC 제거</span><span class="sxs-lookup"><span data-stu-id="a2ab6-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="a2ab6-144">기존 VM에서 NIC tooremove 할당 hello VM을 먼저 해제와 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="a2ab6-145">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a2ab6-146">제거 인 NIC와 hello [az vm nic 제거](/cli/azure/vm/nic#remove)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="a2ab6-147">hello 다음 예제에서는 제거 *myNic3* 에서 *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="a2ab6-148">시작의 VM hello [az vm 시작](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="a2ab6-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="a2ab6-149">Resource Manager 템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="a2ab6-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="a2ab6-150">Azure 리소스 관리자 템플릿 선언적 JSON 파일 toodefine 환경의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="a2ab6-151">[Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)에 대해 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a2ab6-152">리소스 관리자 템플릿을 여러 Nic를 만들 때 처럼 배포 하는 동안 방식으로 toocreate 리소스를 여러 개 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="a2ab6-153">사용 하면 *복사* 인스턴스 toocreate toospecify hello 수:</span><span class="sxs-lookup"><span data-stu-id="a2ab6-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="a2ab6-154">[*복사*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="a2ab6-155">사용할 수도 있습니다는 `copyIndex()` toothen toocreate 수 있는 숫자 tooa 자원 이름을 추가 `myNic1`, `myNic2`, 등 hello 다음 hello 인덱스 값을 추가 하는 모양의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="a2ab6-156">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2ab6-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2ab6-157">Next steps</span></span>
<span data-ttu-id="a2ab6-158">검토 [Linux VM 크기](sizes.md) toocreating 여러 Nic 사용 하 여 VM을 시도할 때.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="a2ab6-159">각 VM 크기가 지원 Nic의 주의 기울여야 toohello 최대 수를 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2ab6-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
