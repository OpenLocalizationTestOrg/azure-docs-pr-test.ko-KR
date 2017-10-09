---
title: "Azure에서 Linux Vm에 대 한 자습서를 설정 하는 aaaAvailability | Microsoft Docs"
description: "Azure에서 Linux Vm에 대 한 hello 가용성 집합에 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="9d519-103">Toouse 가용성 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9d519-103">How toouse availability sets</span></span>


<span data-ttu-id="9d519-104">이 자습서에서는 tooincrease hello 가용성 및 안정성 기능을 사용 하 여 Azure에서 가상 컴퓨터 솔루션의 가용성 집합을 호출 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="9d519-105">가용성 집합에 Vm을 Azure에 배포 하면 여러 개의 분리 된 하드웨어 클러스터에 분산 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="9d519-106">이렇게 있도록 Azure 내에서 하드웨어 또는 소프트웨어 오류가 발생 하는, 하위 집합이 Vm에 영향을 받음 및 사용 가능 하 고 사용 하 여 고객의 hello 관점에서 operational 전체 솔루션 유지 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="9d519-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d519-108">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-108">Create an availability set</span></span>
> * <span data-ttu-id="9d519-109">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="9d519-110">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="9d519-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9d519-111">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="9d519-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9d519-112">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9d519-113">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="9d519-114">가용성 집합 개요</span><span class="sxs-lookup"><span data-stu-id="9d519-114">Availability set overview</span></span>

<span data-ttu-id="9d519-115">가용성 집합 Azure tooensure Azure 데이터 센터 내에서 배포 하는 경우 그 안에 배치 hello VM 리소스를 서로 격리 되어 있는지에 사용할 수 있는 논리 그룹 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="9d519-116">Azure는 hello Vm 여러 물리적 서버에서 실행 되는 가용성 집합 내에서 배치 되도록 하, 랙, 저장 장치 및 네트워크 스위치를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="9d519-117">이렇게 하면 하드웨어 또는 소프트웨어 Azure 실패 hello 이벤트에서 Vm의 하위 집합만 영향을 주지 전반적인 응용 프로그램에서 가동 상태 유지 하 고 toobe tooyour 사용할 수 있는 고객을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="9d519-118">가용성 집합을 사용 하는 필수 기능 tooleverage 때 toobuild 신뢰할 수 있는 클라우드 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="9d519-119">4개의 프런트 엔드 웹 서버가 있고 데이터베이스를 호스팅하는 2개의 백 엔드 VM을 사용하는 일반적인 VM 기반 솔루션을 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="9d519-120">Azure를 원할 toodefine 두 가용성 집합에 Vm을 배포 하기 전에: hello "웹" 계층 및 하나의 가용성 hello "database" 계층에 대 한 설정에 대 한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="9d519-121">그런 다음 매개 변수 toohello az vm 명령을 만들고 Azure 해당 hello hello 사용할 수 있는 내부에서 만든 Vm에 자동으로 확인 됩니다 설정 hello 가용성을 지정할 수는 새 VM을 만들 때 집합에서 여러 물리적 하드웨어 리소스 간의 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="9d519-122">즉, 웹 서버 또는 데이터베이스 서버 Vm 중 하나에서 실행 되는 hello 물리적 하드웨어에 문제가 있는 경우 해당 hello을 파악 하는 웹 서버 및 데이터베이스 Vm의 다른 인스턴스는 계속 실행 제대로 다른 하드웨어에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="9d519-123">Azure 내에서 신뢰할 수 있는 VM 기반 솔루션 toodeploy 하려는 경우에 항상 가용성 집합을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="9d519-124">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-124">Create an availability set</span></span>

<span data-ttu-id="9d519-125">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 가용성 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="9d519-126">이 예제에서 업데이트 및 오류 도메인의 hello 번호가 모두 설정 *2* hello 가용성 명명 된 집합에 대 한 *myAvailabilitySet* hello에 *myResourceGroupAvailability*리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="9d519-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="9d519-128">가용성 집합에서 "오류 도메인" 및 "업데이트 도메인" tooisolate 리소스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="9d519-129">**장애 도메인**은 서버 + 네트워크 + 저장소 리소스의 격리된 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="9d519-130">앞 예제는 hello에서 가용성 집합 두 개 이상의 오류 도메인에이 Vm이 배포 된 경우 분산 toobe 한다고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="9d519-131">또한 가용성 집합이 두 개의 **업데이트 도메인**에도 분산되도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="9d519-132">두 개의 업데이트 도메인 Azure 소프트웨어 업데이트를 수행 하는 경우 VM 우리는 격리 되어 있는지 확인, hello에서 업데이트할 VM이 실행 되는 모든 hello 소프트웨어 방지 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="9d519-133">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="9d519-133">Configure virtual network</span></span>
<span data-ttu-id="9d519-134">일부 Vm을 배포 하 여 분산 장치를 테스트할 수 전에 가상 네트워크 리소스를 지 원하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="9d519-135">가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 관리](tutorial-virtual-network.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="9d519-136">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-136">Create network resources</span></span>
<span data-ttu-id="9d519-137">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="9d519-138">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 이라는 서브넷과 *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="9d519-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="9d519-139">가상 NIC는 [az network nic create](/cli/azure/network/nic#create)를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="9d519-140">hello 다음 예제에서는 세 개의 가상 Nic</span><span class="sxs-lookup"><span data-stu-id="9d519-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="9d519-141">(각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="9d519-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="9d519-142">언제 든 지 가상 Nic를 추가 하 고 Vm을 만들 수 있고 toohello 부하 분산 장치를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="9d519-143">가용성 집합에 포함된 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="9d519-144">Hello 가용성 집합 toomake hello 하드웨어 올바르게 분할 되어 있는지 내에서 Vm은 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="9d519-145">기존 VM tooan 가용성 집합을 만든 후 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="9d519-146">사용 하 여 VM을 만들 때 [az vm 만들기](/cli/azure/vm#create) hello를 사용 하 여 설정 하는 hello 가용성 지정 `--availability-set` 매개 변수 toospecify hello hello 가용성 집합 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="9d519-147">이제 새로 만든 가용성 집합에는 두 개의 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="9d519-148">에 포함 되어 있으므로 hello 동일한 가용성 집합 Azure 방법을 사용 하면 해당 hello Vm과 해당 리소스 (데이터 디스크가 포함) 격리 된 실제 하드웨어에 분산 되어 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="9d519-149">이렇게 분산되면 전체 VM 솔루션의 가용성을 훨씬 높여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="9d519-150">Vm을 추가할 때 발생할 수 있는 한 가지 특정 VM 크기 가용성 집합 내에서 사용할 수 있는 toouse 더 이상 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="9d519-151">이 문제를 더 이상 적용 hello 격리 규칙 hello 가용성 집합을 유지 하면서 용량 tooadd 충분 한 경우에 발생할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="9d519-152">어떤 VM 크기는 기존 가용성 hello를 사용 하 여 설정 내에서 사용할 수 있는 toouse toosee 확인할 수 있습니다 `--availability-set list-sizes` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="9d519-153">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="9d519-153">Check for available VM sizes</span></span> 

<span data-ttu-id="9d519-154">더 많은 Vm toohello 가용성을 설정 하 고, 나중에 추가할 수 있지만 어떤 VM 크기 hello 하드웨어에서 사용할 수 있는 tooknow 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="9d519-155">사용 하 여 [az vm 가용성 집합 목록 크기](/cli/azure/availability-set#list-sizes) toolist hello 가용성 집합에 대 한 클러스터 hello 하드웨어에서 모든 hello 사용 가능한 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="9d519-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d519-156">Next steps</span></span>

<span data-ttu-id="9d519-157">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d519-158">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-158">Create an availability set</span></span>
> * <span data-ttu-id="9d519-159">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="9d519-160">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="9d519-160">Check available VM sizes</span></span>

<span data-ttu-id="9d519-161">가상 컴퓨터 크기 집합에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d519-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d519-162">VM Scale Set 만들기</span><span class="sxs-lookup"><span data-stu-id="9d519-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

