---
title: "Azure에서 Windows용 가상 컴퓨터 확장 집합 만들기 | Microsoft Docs"
description: "가상 컴퓨터 확장 집합을 사용하여 고가용성 응용 프로그램을 만들고 Windows VM에 배포"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6600d3b401495f6c291249935b16bcc36c9b8f4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="7ad8b-103">가상 컴퓨터 확장 집합을 만들고 Windows에 고가용성 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7ad8b-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="7ad8b-104">가상 컴퓨터 확장 집합을 사용하면 동일한 자동 크기 조정 가상 컴퓨터 집합을 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="7ad8b-105">확장 집합의 VM 수를 수동으로 조정하거나 CPU 사용률, 메모리 요구량 또는 네트워크 트래픽을 기반으로 자동으로 크기를 조정하는 규칙을 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="7ad8b-106">이 자습서에서는 Azure에서 가상 컴퓨터 확장 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="7ad8b-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ad8b-108">사용자 지정 스크립트 확장을 사용하여 크기를 조정하는 IIS 사이트를 정의</span><span class="sxs-lookup"><span data-stu-id="7ad8b-108">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="7ad8b-109">확장 집합에 대한 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="7ad8b-110">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="7ad8b-111">확장 집합의 인스턴스 수 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="7ad8b-111">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="7ad8b-112">자동 크기 조정 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-112">Create autoscale rules</span></span>

<span data-ttu-id="7ad8b-113">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7ad8b-114">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="7ad8b-115">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="7ad8b-116">확장 집합 개요</span><span class="sxs-lookup"><span data-stu-id="7ad8b-116">Scale Set overview</span></span>
<span data-ttu-id="7ad8b-117">확장 집합은 이전의 [고가용성 VM 만들기](tutorial-availability-sets.md) 자습서에서 배운 것과 비슷한 개념을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-117">Scale sets use similar concepts as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="7ad8b-118">확장 집합의 VM은 가용성 집합의 VM처럼 장애 도메인 및 업데이트 도메인에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="7ad8b-119">VM은 필요에 따라 확장 집합에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="7ad8b-120">사용자는 확장 집합에서 VM이 추가되거나 제거되는 방법 및 시기를 제어하는 자동 크기 조정 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-120">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="7ad8b-121">이러한 규칙은 메트릭(예: CPU 부하, 메모리 사용량 또는 네트워크 트래픽)을 기반으로 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="7ad8b-122">확장 집합은 Azure 플랫폼 이미지를 사용하는 경우 최대 1,000개의 VM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-122">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="7ad8b-123">중요한 설치 또는 VM 사용자 지정이 필요한 워크로드의 경우 [사용자 지정 VM 이미지를 만들 수 있습니다](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="7ad8b-123">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="7ad8b-124">사용자 지정 이미지를 사용하는 경우 확장 집합에 최대 100개의 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-124">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="7ad8b-125">크기를 조정하는 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-125">Create an app to scale</span></span>
<span data-ttu-id="7ad8b-126">확장 집합을 만들려면 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="7ad8b-127">다음 예제에서는 *EastUS* 위치에 *myResourceGroupAutomate*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-127">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="7ad8b-128">이전 자습서에서는 사용자 지정 스크립트 확장을 사용하여 [VM 구성을 자동화](tutorial-automate-vm-deployment.md)하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-128">In an earlier tutorial, you learned how to [Automate VM configuration](tutorial-automate-vm-deployment.md) using the Custom Script Extension.</span></span> <span data-ttu-id="7ad8b-129">확장 집합 구성을 만든 후 사용자 지정 스크립트 확장을 적용하여 IIS를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-129">Create a scale set configuration then apply a Custom Script Extension to install and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define the script for your Custom Script Extension to run
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension to install IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="7ad8b-130">규모 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-130">Create scale load balancer</span></span>
<span data-ttu-id="7ad8b-131">Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="7ad8b-132">부하 분산 장치 상태 프로브가 각 VM에서 지정된 포트를 모니터링하고 작동하는 VM으로만 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-132">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span> <span data-ttu-id="7ad8b-133">자세한 내용은 [Windows 가상 컴퓨터를 부하 분산하는 방법](tutorial-load-balancer.md)에 대한 다음 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-133">For more information, see the next tutorial on [How to load balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="7ad8b-134">공용 IP 주소를 갖고 있고 포트 80에서 웹 트래픽을 분산하는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create the load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule to distribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update the load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="7ad8b-135">확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-135">Create a scale set</span></span>
<span data-ttu-id="7ad8b-136">이제 [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm)를 사용하여 가상 컴퓨터 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="7ad8b-137">다음 예제는 *myScaleSet*이라는 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-137">The following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create the virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="7ad8b-138">확장 집합 리소스와 VM을 모두 만들고 구성하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-138">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="7ad8b-139">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="7ad8b-139">Test your app</span></span>
<span data-ttu-id="7ad8b-140">IIS 웹 사이트의 실제 동작을 확인하려면 [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-140">To see your IIS website in action, obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="7ad8b-141">다음 예제에서는 확장 집합의 일부로 만든 *myPublicIP*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-141">The following example obtains the IP address for *myPublicIP* created as part of the scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="7ad8b-142">웹 브라우저에 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-142">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="7ad8b-143">앱이 표시되고 부하 분산 장치가 트래픽을 분산한 VM의 호스트 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-143">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![실행 중인 IIS 사이트](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="7ad8b-145">확장 집합의 실제 동작을 확인하려면 웹 브라우저에서 새로 고침을 실행하여 부하 분산 장치가 앱이 실행되는 모든 VM으로 트래픽을 분산시키는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-145">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="7ad8b-146">관리 작업</span><span class="sxs-lookup"><span data-stu-id="7ad8b-146">Management tasks</span></span>
<span data-ttu-id="7ad8b-147">확장 집합의 수명 주기 내내 하나 이상의 관리 작업을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-147">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="7ad8b-148">또한 다양한 수명 주기 작업을 자동화하는 스크립트를 만들어야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-148">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="7ad8b-149">Azure PowerShell은 이러한 작업을 수행할 수 있는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-149">Azure PowerShell provides a quick way to do those tasks.</span></span> <span data-ttu-id="7ad8b-150">다음은 몇 가지 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="7ad8b-151">확장 집합의 VM 보기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-151">View VMs in a scale set</span></span>
<span data-ttu-id="7ad8b-152">확장 집합에서 실행 중인 VM 목록을 보려면 다음과 같이 [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-152">To view a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through the instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="7ad8b-153">VM 인스턴스 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="7ad8b-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="7ad8b-154">현재 확장 집합의 인스턴스 수를 보려면 [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss)를 사용하여 *sku.capacity*를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-154">To see the number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="7ad8b-155">그런 다음 [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)를 사용하여 확장 집합의 가상 컴퓨터 수를 수동으로 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-155">You can then manually increase or decrease the number of virtual machines in the scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="7ad8b-156">다음 예제는 확장 집합의 VM 수를 *5*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-156">The following example sets the number of VMs in your scale set to *5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update the capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="7ad8b-157">확장 집합에 지정된 인스턴스 수를 업데이트하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-157">If takes a few minutes to update the specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="7ad8b-158">자동 크기 조정 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="7ad8b-158">Configure autoscale rules</span></span>
<span data-ttu-id="7ad8b-159">확장 집합에서 인스턴스 수를 수동으로 확장하는 대신 자동 크기 조정 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-159">Rather than manually scaling the number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="7ad8b-160">이러한 규칙은 확장 집합의 인스턴스를 모니터링하고 사용자가 정의한 메트릭 및 임계값에 따라 적절하게 대응합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-160">These rules monitor the instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="7ad8b-161">다음은 평균 CPU 부하가 5분 넘게 60%를 초과하면 인스턴스 수를 하나 늘리는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-161">The following example scales out the number of instances by one when the average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="7ad8b-162">평균 CPU 부하가 5분 넘게 30% 미만이면 인스턴스 수를 하나 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-162">If the average CPU load then drops below 30% over a 5 minute period, the instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule to increase the number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule to decrease the number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply the autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="7ad8b-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ad8b-163">Next steps</span></span>
<span data-ttu-id="7ad8b-164">이 자습서에서는 가상 컴퓨터 확장 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="7ad8b-165">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ad8b-166">사용자 지정 스크립트 확장을 사용하여 크기를 조정하는 IIS 사이트를 정의</span><span class="sxs-lookup"><span data-stu-id="7ad8b-166">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="7ad8b-167">확장 집합에 대한 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="7ad8b-168">가상 컴퓨터 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="7ad8b-169">확장 집합의 인스턴스 수 증가 또는 감소</span><span class="sxs-lookup"><span data-stu-id="7ad8b-169">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="7ad8b-170">자동 크기 조정 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7ad8b-170">Create autoscale rules</span></span>

<span data-ttu-id="7ad8b-171">Virtual Machines의 부하 분산 개념에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ad8b-171">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ad8b-172">Virtual Machines 부하 분산</span><span class="sxs-lookup"><span data-stu-id="7ad8b-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
