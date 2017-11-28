---
title: "Azure에서 Linux VM에 대한 가용성 집합 자습서 | Microsoft Docs"
description: "Azure에서 Linux VM에 대한 가용성 집합에 대해 알아봅니다."
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
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="c9e45-103">가용성 집합 사용 방법</span><span class="sxs-lookup"><span data-stu-id="c9e45-103">How to use availability sets</span></span>


<span data-ttu-id="c9e45-104">이 자습서에서는 가용성 집합이라는 기능을 사용하여 Azure에서 VM(가상 컴퓨터) 솔루션의 가용성과 안정성을 향상시키는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="c9e45-105">가용성 집합을 사용하면 Azure에 배포한 VM이 격리된 여러 하드웨어 클러스터에 분산되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="c9e45-106">이렇게 하면 Azure 내의 하드웨어 또는 소프트웨어 오류가 발생할 때 VM의 하위 집합에만 영향을 주며 전체 솔루션을 사용하는 고객의 관점에서 전체 솔루션을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="c9e45-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c9e45-108">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-108">Create an availability set</span></span>
> * <span data-ttu-id="c9e45-109">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c9e45-110">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="c9e45-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c9e45-111">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c9e45-112">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="c9e45-113">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9e45-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="c9e45-114">가용성 집합 개요</span><span class="sxs-lookup"><span data-stu-id="c9e45-114">Availability set overview</span></span>

<span data-ttu-id="c9e45-115">가용성 집합은 해당 집합에 배치한 VM 리소스가 Azure 데이터 센터에 배포될 때 서로 간에 격리되도록 하기 위해 Azure에서 사용할 수 있는 논리적 그룹화 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="c9e45-116">Azure는 가용성 집합 내에 배치한 VM을 여러 물리적 서버, 계산 랙, 저장 단위 및 네트워크 스위치에서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="c9e45-117">이렇게 하면 하드웨어 또는 Azure 소프트웨어 오류가 발생할 경우 VM의 하위 집합에만 영향을 주는 한편 전체 응용 프로그램은 계속 유지되어 고객이 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="c9e45-118">가용성 집합을 사용하는 것은 안정적인 클라우드 솔루션을 구축하려고 할 때 활용할 수 있는 필수적인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="c9e45-119">4개의 프런트 엔드 웹 서버가 있고 데이터베이스를 호스팅하는 2개의 백 엔드 VM을 사용하는 일반적인 VM 기반 솔루션을 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="c9e45-120">Azure를 사용하면 VM을 배포하기 전에 하나는 “웹” 계층, 다른 하나는 “데이터베이스” 계층에 대한 집합인 두 개의 가용성 집합을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="c9e45-121">새 VM을 만들 때 az vm create 명령에 대한 매개 변수로 가용성 집합을 지정할 수 있으며, Azure에서는 사용 가능한 집합 내에 만든 VM이 여러 물리적 하드웨어 리소스에서 자동으로 격리되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="c9e45-122">즉, 웹 서버 VM 또는 데이터베이스 서버 VM 중 하나가 실행 중인 물리적 하드웨어에 문제가 있는 경우 웹 서버 VM과 데이터베이스 VM의 다른 인스턴스가 다른 하드웨어에 있기 때문에 계속 실행된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="c9e45-123">Azure 내에서 신뢰할 수 있는 VM 기반 솔루션을 배포하려면 항상 가용성 집합을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="c9e45-124">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-124">Create an availability set</span></span>

<span data-ttu-id="c9e45-125">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 가용성 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="c9e45-126">이 예제에서는 *myResourceGroupAvailability* 리소스 그룹의 *myAvailabilitySet*라는 가용성 집합에 대해 업데이트 수와 장애 도메인 수를 모두 *2*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="c9e45-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-127">Create a resource group.</span></span>

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

<span data-ttu-id="c9e45-128">가용성 집합을 사용하면 "장애 도메인" 및 "업데이트 도메인"에서 리소스를 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="c9e45-129">**장애 도메인**은 서버 + 네트워크 + 저장소 리소스의 격리된 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="c9e45-130">위의 예제에서는 VM을 배포할 때 가용성 집합이 적어도 두 개의 장애 도메인에 분산되도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="c9e45-131">또한 가용성 집합이 두 개의 **업데이트 도메인**에도 분산되도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="c9e45-132">두 개의 업데이트 도메인은 Azure에서 소프트웨어 업데이트를 수행할 때 VM 리소스가 격리되어 해당 VM에서 실행되는 모든 소프트웨어가 동시에 업데이트되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="c9e45-133">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="c9e45-133">Configure virtual network</span></span>
<span data-ttu-id="c9e45-134">일부 VM을 배포하고 부하 분산 장치를 테스트하려면 지원하는 가상 네트워크 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="c9e45-135">가상 네트워크에 대한 자세한 내용은 [Azure Virtual Network 관리](tutorial-virtual-network.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9e45-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="c9e45-136">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-136">Create network resources</span></span>
<span data-ttu-id="c9e45-137">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c9e45-138">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="c9e45-139">가상 NIC는 [az network nic create](/cli/azure/network/nic#create)를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="c9e45-140">다음 예제에서는 3개의 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="c9e45-141">(다음 단계에서 앱에 대해 만드는 각 VM에 대해 가상 NIC 하나씩)</span><span class="sxs-lookup"><span data-stu-id="c9e45-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="c9e45-142">언제든지 추가 가상 NIC 및 VM을 만든 후 부하 분산 장치에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="c9e45-143">가용성 집합에 포함된 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="c9e45-144">하드웨어 전체에 올바르게 배포되도록 하려면 VM을 가용성 집합 내에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="c9e45-145">VM을 만든 후에는 가용성 집합에 기존 VM을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="c9e45-146">[az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 때 가용성 집합의 이름을 지정하는 `--availability-set` 매개 변수를 사용하여 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

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

<span data-ttu-id="c9e45-147">이제 새로 만든 가용성 집합에는 두 개의 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="c9e45-148">동일한 가용성 집합에 있기 때문에 Azure에서는 VM 및 관련된 모든 리소스(데이터 디스크 포함)가 격리된 물리적 하드웨어에 분산되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="c9e45-149">이렇게 분산되면 전체 VM 솔루션의 가용성을 훨씬 높여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="c9e45-150">VM을 추가할 때 발생할 수 있는 한 가지 문제는 특정 VM 크기를 가용성 집합 내에서 더 이상 사용할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="c9e45-151">가용성 집합에 적용되는 격리 규칙을 유지하면서 추가할 수 있는 용량이 더 이상 충분하지 않을 경우에 이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="c9e45-152">`--availability-set list-sizes` 매개 변수를 사용하여 기존 가용성 집합에서 사용할 수 있는 VM 크기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="c9e45-153">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="c9e45-153">Check for available VM sizes</span></span> 

<span data-ttu-id="c9e45-154">나중에 더 많은 VM을 가용성 집합에 추가할 수 있지만 하드웨어에서 사용 가능한 VM 크기를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="c9e45-155">[az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes)를 사용하여 하드웨어 클러스터에서 가용성 집합에 대한 사용 가능한 모든 크기를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="c9e45-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9e45-156">Next steps</span></span>

<span data-ttu-id="c9e45-157">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c9e45-158">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-158">Create an availability set</span></span>
> * <span data-ttu-id="c9e45-159">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c9e45-160">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="c9e45-160">Check available VM sizes</span></span>

<span data-ttu-id="c9e45-161">가상 컴퓨터 확장 집합에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9e45-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9e45-162">VM Scale Set 만들기</span><span class="sxs-lookup"><span data-stu-id="c9e45-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

