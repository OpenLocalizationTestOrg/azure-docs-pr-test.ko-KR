---
title: "여러 Nic 사용 하 여 Azure에서 Linux VM aaaCreate | Microsoft Docs"
description: "여러 Nic 사용 하 여 Linux VM toocreate tooit hello Azure CLI 또는 리소스 관리자 템플릿을 사용 하 여 연결 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="37ff5-103">여러 Nic hello Azure CLI 1.0을 사용 하 여 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="37ff5-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="37ff5-104">여러 가상 네트워크 인터페이스 (Nic) 연결 된 tooit가 Azure에서 가상 컴퓨터 (VM)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="37ff5-105">일반적인 시나리오는 toohave 프런트 엔드 및 백 엔드 연결에 대 한 서로 다른 서브넷 또는 네트워크를 전용 tooa 모니터링 또는 백업 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="37ff5-106">이 문서는 빠른 명령을 toocreate 여러 연결 된 Nic tooit 사용 하 여 VM을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="37ff5-107">자세한 정보에 대 한 방법을 toocreate 자신의 내에서 여러 Nic를 이용한 적 비롯 하 여 스크립트에 대해 자세히 알아보세요 [다중 NIC Vm을 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="37ff5-108">[VM 크기](sizes.md) 가 다르면 다양한 NIC가 지원되므로 그에 따라 VM 크기를 지정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="37ff5-109">Nic tooan hello Azure CLI 1.0 함께 존재 하는 VM을 추가할 수 없습니다-VM을 만들 때 여러 Nic를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="37ff5-110">있습니다 수 [hello Azure CLI 2.0 함께 존재 하는 VM Nic tooan 추가](multiple-nics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="37ff5-111">수도 있습니다 [hello 원래 가상 디스크에 따라 VM 만들기](copy-vm.md) hello VM을 배포 하는 경우 여러 Nic를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="37ff5-112">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="37ff5-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="37ff5-113">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="37ff5-114">[Azure CLI 1.0](#create-supporting-resources) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="37ff5-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="37ff5-115">[Azure CLI 2.0](multiple-nics.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="37ff5-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="37ff5-116">지원 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="37ff5-116">Create supporting resources</span></span>
<span data-ttu-id="37ff5-117">Hello 갖도록 [Azure CLI](../../cli-install-nodejs.md) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="37ff5-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="37ff5-118">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="37ff5-119">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="37ff5-120">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-120">First, create a resource group.</span></span> <span data-ttu-id="37ff5-121">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="37ff5-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="37ff5-122">저장소 계정 toohold Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="37ff5-123">hello 다음 예제에서는 저장소 계정인 *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="37ff5-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="37ff5-124">가상 네트워크 tooconnect Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="37ff5-125">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 의 주소 접두사가 *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="37ff5-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="37ff5-126">두 개의 가상 네트워크 서브넷(프런트 엔드 트래픽용 및 백 엔드 트래픽용)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="37ff5-127">hello 다음 예제에서는 명명 된, 두 서브넷 *mySubnetFrontEnd* 및 *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="37ff5-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="37ff5-128">여러 NIC 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="37ff5-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="37ff5-129">에 대 한 자세한 정보를 읽을 수 있습니다 [hello Azure CLI를 사용 하 여 여러 Nic를 배포](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), 스크립팅 모든 hello Nic toocreate 전체 반복의 hello 프로세스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="37ff5-130">hello 다음 예제에서는 라는 두 개의 nic가 *myNic1* 및 *myNic2*, tooeach 서브넷 연결 NIC 1 개 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

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

<span data-ttu-id="37ff5-131">또한 만들 일반적으로 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 또는 [부하 분산 장치](../../load-balancer/load-balancer-overview.md) toohelp 관리 하 고 Vm에 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="37ff5-132">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="37ff5-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="37ff5-133">Nic toohello 네트워크 보안 그룹을 사용 하 여 바인딩 `azure network nic set`합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="37ff5-134">hello 다음 예제에서는 *myNic1* 및 *myNic2* 와 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="37ff5-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="37ff5-135">VM을 만들고 hello Nic 연결</span><span class="sxs-lookup"><span data-stu-id="37ff5-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="37ff5-136">Hello VM을 만들 때 이제 여러 Nic를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="37ff5-137">대신 사용 하 여 `--nic-name` tooprovide 단일 NIC를 대신 사용 하 여 `--nic-names` Nic의 쉼표로 구분 된 목록에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="37ff5-138">또한 해야 tootake 주의 hello v M 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="37ff5-139">hello tooa VM을 추가할 수 있는 Nic의 총 수에 대 한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="37ff5-140">[Linux VM 크기](sizes.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="37ff5-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="37ff5-141">hello 다음 예제에서는 toospecify 여러 Nic 및 VM 크기를 정하는 사용 하 여 지 원하는 여러 Nic (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="37ff5-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="37ff5-142">Resource Manager 템플릿을 사용하여 여러 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="37ff5-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="37ff5-143">Azure 리소스 관리자 템플릿 선언적 JSON 파일 toodefine 환경의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="37ff5-144">[Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)에 대해 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="37ff5-145">리소스 관리자 템플릿을 여러 Nic를 만들 때 처럼 배포 하는 동안 방식으로 toocreate 리소스를 여러 개 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="37ff5-146">사용 하면 *복사* 인스턴스 toocreate toospecify hello 수:</span><span class="sxs-lookup"><span data-stu-id="37ff5-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="37ff5-147">[*복사*를 사용하여 여러 인스턴스 만들기](../../resource-group-create-multiple.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="37ff5-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="37ff5-148">사용할 수도 있습니다는 `copyIndex()` toothen toocreate 수 있는 숫자 tooa 자원 이름을 추가 `myNic1`, `myNic2`, 등 hello 다음 hello 인덱스 값을 추가 하는 모양의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="37ff5-149">[Resource Manager 템플릿을 사용하여 여러 NIC 만들기](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)의 전체 예제를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="37ff5-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37ff5-150">Next steps</span></span>
<span data-ttu-id="37ff5-151">있는지 tooreview 확인 [Linux VM 크기](sizes.md) toocreating 여러 Nic 사용 하 여 VM을 시도할 때.</span><span class="sxs-lookup"><span data-stu-id="37ff5-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="37ff5-152">각 VM 크기가 지원 Nic의 주의 기울여야 toohello 최대 수를 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="37ff5-153">추가 Nic tooan 기존 VM을 추가할 수 없습니다, hello VM을 배포할 때 모든 hello Nic에 만들어야 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="37ff5-154">프로그램 배포 toomake hello 처음부터 hello 필요한 네트워크 연결을 모두 갖도록를 계획할 때는 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37ff5-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

