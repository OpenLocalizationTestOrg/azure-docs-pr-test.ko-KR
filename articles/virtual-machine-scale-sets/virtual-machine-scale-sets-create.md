---
title: "aaaCreate Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "Azure CLI, PowerShell, 템플릿 또는 Visual Studio를 사용하여 Linux 또는 Microsoft Azure 가상 컴퓨터 확장 집합을 만들고 배포합니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="f5589-103">가상 컴퓨터 확장 집합 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="f5589-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="f5589-104">가상 컴퓨터 크기 집합에 더 쉽게 있습니다 toodeploy 고 집합으로 동일한 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="f5589-105">규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="f5589-106">확장 집합에 대한 자세한 내용은 [가상 컴퓨터 확장 집합](virtual-machine-scale-sets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5589-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="f5589-107">이 자습서에서는 가상 컴퓨터 크기 집합 하는 toocreate 어떻게 **없이** Azure 포털 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="f5589-108">어떻게 toouse hello Azure 포털에 대 한 정보를 참조 하십시오. [어떻게 toocreate 가상 컴퓨터 크기는 Azure 포털 hello로을 집합](virtual-machine-scale-sets-portal-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="f5589-109">Azure Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5589-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="f5589-110">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="f5589-110">Sign in tooAzure</span></span>

<span data-ttu-id="f5589-111">Azure CLI 2.0 또는 Azure PowerShell toocreate 소수 자릿수를 사용 하 여 설정, 먼저 toosign tooyour 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="f5589-112">설정, tooinstall 및 로그인 tooAzure Azure CLI 또는 PowerShell을 참조 하는 방법에 대 한 자세한 내용은 [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli.md) 또는 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f5589-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-113">Create a resource group</span></span>

<span data-ttu-id="f5589-114">먼저 hello 가상 컴퓨터 크기 집합는 리소스 그룹은 연결 된 toocreate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="f5589-115">Azure CLI에서 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-115">Create from Azure CLI</span></span>

<span data-ttu-id="f5589-116">Azure CLI를 사용하여 적은 노력으로 가상 컴퓨터 확장 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="f5589-117">기본값을 생략한 경우 기본값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="f5589-118">예를 들어 가상 네트워크 정보를 지정하지 않는 경우 가상 네트워크가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="f5589-119">Hello 부분 뒤를 생략 하면 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="f5589-120">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="f5589-120">A load balancer</span></span>
- <span data-ttu-id="f5589-121">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="f5589-121">A virtual network</span></span>
- <span data-ttu-id="f5589-122">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="f5589-122">A public IP address</span></span>

<span data-ttu-id="f5589-123">Toouse hello 가상 컴퓨터 크기 집합에 가상 컴퓨터 이미지를 hello 선택 때 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="f5589-124">URN</span><span class="sxs-lookup"><span data-stu-id="f5589-124">URN</span></span>  
<span data-ttu-id="f5589-125">리소스의 hello 식별자:</span><span class="sxs-lookup"><span data-stu-id="f5589-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="f5589-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="f5589-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="f5589-127">URN 별칭</span><span class="sxs-lookup"><span data-stu-id="f5589-127">URN alias</span></span>  
<span data-ttu-id="f5589-128">hello URN의 식별 이름:</span><span class="sxs-lookup"><span data-stu-id="f5589-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="f5589-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="f5589-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="f5589-130">사용자 지정 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="f5589-130">Custom resource id</span></span>  
<span data-ttu-id="f5589-131">hello 경로 tooan Azure 리소스:</span><span class="sxs-lookup"><span data-stu-id="f5589-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="f5589-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="f5589-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="f5589-133">웹 리소스</span><span class="sxs-lookup"><span data-stu-id="f5589-133">Web resource</span></span>  
<span data-ttu-id="f5589-134">hello 경로 tooan HTTP URI:</span><span class="sxs-lookup"><span data-stu-id="f5589-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="f5589-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="f5589-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="f5589-136">`az vm image list`을 사용하여 사용 가능한 이미지 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="f5589-137">toocreate 가상 컴퓨터 크기 집합, hello 다음을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="f5589-138">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="f5589-138">Resource group</span></span> 
- <span data-ttu-id="f5589-139">이름</span><span class="sxs-lookup"><span data-stu-id="f5589-139">Name</span></span>
- <span data-ttu-id="f5589-140">운영 체제 이미지</span><span class="sxs-lookup"><span data-stu-id="f5589-140">Operating system image</span></span>
- <span data-ttu-id="f5589-141">인증 정보</span><span class="sxs-lookup"><span data-stu-id="f5589-141">Authentication information</span></span> 
 
<span data-ttu-id="f5589-142">다음 예제는 hello (이 단계는 몇 분 정도 걸릴 수 있습니다) 하는 기본적인 가상 컴퓨터 크기 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="f5589-143">Hello 명령이 완료 된 후에 가상 컴퓨터 크기 집합 만든 이제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="f5589-144">Tooget hello 가상 컴퓨터의 IP 주소를 hello tooit 연결할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="f5589-145">다음 명령을 hello로 많은 hello 가상 컴퓨터 (IP 주소 hello 포함)에 대 한 다른 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="f5589-146">PowerShell에서 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-146">Create from PowerShell</span></span>

<span data-ttu-id="f5589-147">PowerShell은 Azure CLI 보다 더 복잡 한 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="f5589-148">Azure CLI는 네트워킹 관련 리소스(부하 분산 장치, IP 주소, 가상 네트워크 등)의 기본값을 제공하는 반면 PowerShell은 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="f5589-149">PowerShell을 사용하여 이미지를 참조하는 작업은 약간 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="f5589-150">Cmdlet을 다음 hello로 이미지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="f5589-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5589-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="f5589-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="f5589-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="f5589-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="f5589-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="f5589-154">hello cmdlet 작업 순서에 파이프 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="f5589-155">Hello에 대 한 모든 tooget 이미지 하는 방법의 예로 **미국 서 부 2** hello 이름이 있는 게시자를 사용 하 여 영역 **microsoft** 에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="f5589-156">가상 컴퓨터 크기 집합을 만들기 위한 hello 워크플로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="f5589-157">Hello 크기 집합에 대 한 정보를 포함 하는 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="f5589-158">참조 hello 기본 OS 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="f5589-159">Hello 운영 체제 설정을 구성: 인증, VM 이름 접두사 및 사용자/통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="f5589-160">네트워킹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-160">Configure networking.</span></span>
5. <span data-ttu-id="f5589-161">Hello 크기 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-161">Create hello scale set.</span></span>

<span data-ttu-id="f5589-162">이 예제에서는 Windows Server 2016이 설치된 컴퓨터에 2개의 인스턴스로 된 기본 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="f5589-163">사용자 지정 가상 컴퓨터 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="f5589-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="f5589-164">크기 hello 갤러리에서 가상 컴퓨터 이미지를 참조 하는 대신 사용자 지정 이미지에서 집합을 만드는 경우 hello _집합 AzureRmVmssStorageProfile_ 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="f5589-165">템플릿에서 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-165">Create from a template</span></span>

<span data-ttu-id="f5589-166">Azure Resource Manager 템플릿을 사용하여 가상 컴퓨터 확장 집합을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="f5589-167">Hello에서 하나를 사용 하거나 사용자 고유의 템플릿을 만들 수 있습니다 [템플릿 리포지토리](https://azure.microsoft.com/resources/templates/?term=vmss)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="f5589-168">이러한 템플릿을 배포할 수 있으며 직접 tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f5589-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="f5589-169">toocreate JSON 텍스트 파일을 만들면 사용자 지정 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="f5589-170">방법에 대 한 일반적인 내용은 toocreate 템플릿을 사용자 지정 하 고, 참조 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f5589-171">[GitHub에서](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set) 샘플 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="f5589-172">샘플을 사용 하 고 toocreate 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [최소 실행 가능한 크기 집합](.\virtual-machine-scale-sets-mvss-start.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="f5589-173">Visual Studio에서 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-173">Create from Visual Studio</span></span>

<span data-ttu-id="f5589-174">Visual Studio와 함께 Azure 리소스 그룹 프로젝트 만들고는 가상 컴퓨터 크기 집합 tooit 서식 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="f5589-175">Tooimport 사용할지를 선택할 수 있습니다 GitHub 또는 hello Azure 웹 응용 프로그램 갤러리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="f5589-176">PowerShell 배포 스크립트도 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="f5589-177">자세한 내용은 참조 [어떻게 toocreate 가상 컴퓨터 크기는 Visual Studio와 함께 집합](virtual-machine-scale-sets-vs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="f5589-178">Hello Azure 포털에서 만들기</span><span class="sxs-lookup"><span data-stu-id="f5589-178">Create from hello Azure portal</span></span>

<span data-ttu-id="f5589-179">hello Azure 포털 tooquickly 크기 집합을 만들기는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="f5589-180">자세한 내용은 참조 [어떻게 toocreate 가상 컴퓨터 크기는 Azure 포털 hello로을 집합](virtual-machine-scale-sets-portal-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5589-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5589-181">Next steps</span></span>

<span data-ttu-id="f5589-182">[데이터 디스크](virtual-machine-scale-sets-attached-disks.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="f5589-183">너무 방법에 대해 알아봅니다[앱 관리](virtual-machine-scale-sets-deploy-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5589-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
