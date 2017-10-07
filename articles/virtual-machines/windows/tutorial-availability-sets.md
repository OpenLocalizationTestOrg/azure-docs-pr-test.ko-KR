---
title: "Azure의 Windows Vm에 대 한 자습서를 설정 하는 aaaAvailability | Microsoft Docs"
description: "Hello 가용성 집합에 대 한 Windows Azure에서 Vm에 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="d2707-103">Toouse 가용성 설정 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2707-103">How toouse availability sets</span></span>

<span data-ttu-id="d2707-104">이 자습서에서는 tooincrease hello 가용성 및 안정성 기능을 사용 하 여 Azure에서 가상 컴퓨터 솔루션의 가용성 집합을 호출 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="d2707-105">가용성 집합에 Vm을 Azure에 배포 하면 여러 개의 분리 된 하드웨어 클러스터에 분산 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="d2707-106">이렇게 있도록 Azure 내에서 하드웨어 또는 소프트웨어 오류가 발생 하는, 하위 집합이 Vm에 영향을 받음 및 사용 가능 하 고 사용 하 여 고객의 hello 관점에서 operational 전체 솔루션 유지 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="d2707-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2707-108">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-108">Create an availability set</span></span>
> * <span data-ttu-id="d2707-109">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="d2707-110">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="d2707-110">Check available VM sizes</span></span>

<span data-ttu-id="d2707-111">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d2707-112">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d2707-113">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="d2707-114">가용성 집합 개요</span><span class="sxs-lookup"><span data-stu-id="d2707-114">Availability set overview</span></span>

<span data-ttu-id="d2707-115">가용성 집합 Azure tooensure Azure 데이터 센터 내에서 배포 하는 경우 그 안에 배치 hello VM 리소스를 서로 격리 되어 있는지에 사용할 수 있는 논리 그룹 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="d2707-116">Azure는 hello Vm 여러 물리적 서버에서 실행 되는 가용성 집합 내에서 배치 되도록 하, 랙, 저장 장치 및 네트워크 스위치를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="d2707-117">이렇게 하면 하드웨어 또는 소프트웨어 Azure 실패 hello 이벤트에서 Vm의 하위 집합만 영향을 주지 전반적인 응용 프로그램에서 가동 상태 유지 하 고 toobe tooyour 사용할 수 있는 고객을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="d2707-118">가용성 집합을 사용 하는 필수 기능 tooleverage 때 toobuild 신뢰할 수 있는 클라우드 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="d2707-119">4개의 프런트 엔드 웹 서버가 있고 데이터베이스를 호스팅하는 2개의 백 엔드 VM을 사용하는 일반적인 VM 기반 솔루션을 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="d2707-120">Azure를 원할 toodefine 두 가용성 집합에 Vm을 배포 하기 전에: hello "웹" 계층 및 하나의 가용성 hello "database" 계층에 대 한 설정에 대 한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="d2707-121">그런 다음 매개 변수 toohello az vm 명령을 만들고 Azure 해당 hello hello 사용할 수 있는 내부에서 만든 Vm에 자동으로 확인 됩니다 설정 hello 가용성을 지정할 수는 새 VM을 만들 때 집합에서 여러 물리적 하드웨어 리소스 간의 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="d2707-122">즉, 웹 서버 또는 데이터베이스 서버 Vm 중 하나에서 실행 되는 hello 물리적 하드웨어에 문제가 있는 경우 해당 hello을 파악 하는 웹 서버 및 데이터베이스 Vm의 다른 인스턴스는 계속 실행 제대로 다른 하드웨어에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="d2707-123">Azure 내에서 신뢰할 수 있는 VM 기반 솔루션 toodeploy 하려는 경우에 항상 가용성 집합을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="d2707-124">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-124">Create an availability set</span></span>

<span data-ttu-id="d2707-125">[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="d2707-126">이 예제에서 업데이트 및 오류 도메인의 hello 번호가 모두 설정 *2* hello 가용성 명명 된 집합에 대 한 *myAvailabilitySet* hello에 *myResourceGroupAvailability*리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="d2707-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="d2707-128">가용성 집합에 포함된 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="d2707-129">Vm은 hello 가용성 집합 toomake hello 하드웨어 올바르게 분할 되어 있는지 내에서 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="d2707-130">기존 VM tooan 가용성 집합을 만든 후 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="d2707-131">위치에 hello 하드웨어 toomultiple 업데이트 도메인과 오류 도메인에 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="d2707-132">**업데이트 도메인** Vm 및 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어의 그룹은 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="d2707-133">Vm에 동일 hello **장애 도메인** 공통 저장소 뿐만 아니라 일반적인 전원 원본과 네트워크 스위치를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="d2707-134">사용 하 여 구성을 사용 하는 VM을 만들 때 [새로 AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) hello를 사용 하 여 설정 하는 hello 가용성 지정 `-AvailabilitySetId` hello 가용성 집합의 매개 변수 toospecify hello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="d2707-135">와 2 개의 Vm을 만들 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) hello 가용성 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="d2707-136">몇 분 toocreate 걸리고 두 Vm을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="d2707-137">완료 되 면 hello 기반 하드웨어를 분산 하는 가상 컴퓨터 2 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="d2707-138">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="d2707-138">Check for available VM sizes</span></span> 

<span data-ttu-id="d2707-139">더 많은 Vm toohello 가용성을 설정 하 고, 나중에 추가할 수 있지만 어떤 VM 크기 hello 하드웨어에서 사용할 수 있는 tooknow 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="d2707-140">사용 하 여 [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist hello 가용성 집합에 대 한 클러스터 hello 하드웨어에서 모든 hello 사용 가능한 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="d2707-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2707-141">Next steps</span></span>

<span data-ttu-id="d2707-142">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2707-143">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-143">Create an availability set</span></span>
> * <span data-ttu-id="d2707-144">가용성 집합에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="d2707-145">사용 가능한 VM 크기 확인</span><span class="sxs-lookup"><span data-stu-id="d2707-145">Check available VM sizes</span></span>

<span data-ttu-id="d2707-146">가상 컴퓨터 크기 집합에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2707-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2707-147">VM Scale Set 만들기</span><span class="sxs-lookup"><span data-stu-id="d2707-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


