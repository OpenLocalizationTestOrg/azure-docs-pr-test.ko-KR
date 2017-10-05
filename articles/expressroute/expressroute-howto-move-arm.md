---
title: "클래식에서 Resource Manager로 ExpressRoute 회로 이동: PowerShell: Azure | Microsoft Docs"
description: "이 페이지는 PowerShell을 사용하여 클래식 회로를 Resource Manager 배포 모델로 이동하는 방법을 설명합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="6f406-103">PowerShell을 사용하여 클래식에서 Resource Manager 배포 모델로 ExpressRoute 회로 이동</span><span class="sxs-lookup"><span data-stu-id="6f406-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="6f406-104">클래식 및 Resource Manager 배포 모델 모두에서 사용할 수 있도록 ExpressRoute 회로를 사용하려면 회로를 Resource Manager 배포 모델로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="6f406-105">다음 섹션에서는 PowerShell을 사용하여 회로를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f406-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6f406-106">Before you begin</span></span>

* <span data-ttu-id="6f406-107">Azure PowerShell 모듈의 최신 버전(버전 1.0 이상)이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="6f406-108">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f406-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="6f406-109">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md) 및 [워크플로](expressroute-workflows.md)를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="6f406-110">[클래식에서 Resource Manager로 ExpressRoute 회로 이동](expressroute-move.md)에서 제공되는 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="6f406-111">제한 및 제한 사항을 완전히 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="6f406-112">클래식 배포 모델에서 회로가 완벽하게 작동되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="6f406-113">리소스 관리자 배포 모델에 만든 리소스 그룹이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="6f406-114">ExpressRoute 회로 이동</span><span class="sxs-lookup"><span data-stu-id="6f406-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="6f406-115">1단계: 클래식 배포 모델에서 회로 세부 정보 수집</span><span class="sxs-lookup"><span data-stu-id="6f406-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="6f406-116">Azure 클래식 환경에 로그인하고 서비스 키를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="6f406-117">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="6f406-118">적절한 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="6f406-119">Azure 및 ExpressRoute에 대한 PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="6f406-120">아래 cmdlet을 사용하여 모든 ExpressRoute 회로에 대한 서비스 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="6f406-121">키를 가져온 후에 Resource Manager 배포 모델로 이동하려는 회로의 **서비스 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="6f406-122">2단계: 로그인하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6f406-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="6f406-123">Resource Manager 환경에 로그인하고 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="6f406-124">Azure Resource Manager 환경으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="6f406-125">적절한 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="6f406-126">리소스 그룹이 아직 없는 경우 아래 코드 조각을 수정하여 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="6f406-127">3단계: 리소스 관리자 배포 모델로 Express 경로 회로 이동</span><span class="sxs-lookup"><span data-stu-id="6f406-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="6f406-128">이제 클래식 배포 모델에서 Resource Manager 배포 모델로 ExpressRoute 회로를 이동할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="6f406-129">계속 진행하기 전에 [클래식에서 Resource Manager 배포 모델로 ExpressRoute 회로 이동](expressroute-move.md)에서 제공되는 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="6f406-130">회로를 이동하려면 다음 코드 조각을 수정한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="6f406-131">이동이 완료되면 이전 cmdlet에 나열된 새 이름을 사용하여 리소스 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="6f406-132">회로는 기본적으로 이름이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="6f406-133">회로 액세스 수정</span><span class="sxs-lookup"><span data-stu-id="6f406-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="6f406-134">두 배포 모델에 대한 ExpressRoute 회로 액세스를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="6f406-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="6f406-135">클래식 ExpressRoute 회로를 Resource Manager 배포 모델로 이동한 후에 두 배포 모델에 모두 액세스할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="6f406-136">두 배포 모델에 모두 액세스하려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="6f406-137">회로 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="6f406-138">"Allow Classic Operations"을 TRUE로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="6f406-139">회로를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-139">Update the circuit.</span></span> <span data-ttu-id="6f406-140">이 작업이 성공적으로 완료되면 클래식 배포 모델의 회로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="6f406-141">ExpressRoute 회로의 세부 정보를 가져오려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="6f406-142">나열된 서비스 키를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="6f406-143">이제 클래식 VNet에 대한 클래식 배포 모델 명령 및 Resource Manager VNet에 대한 Resource Manager 명령을 사용하여 ExpressRoute 회로에 대한 링크를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="6f406-144">다음 문서에서는 ExpressRoute 회로에 대한 링크를 관리하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="6f406-145">리소스 관리자 배포 모델에서 가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="6f406-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="6f406-146">클래식 배포 모델에서 가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="6f406-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="6f406-147">클래식 배포 모델에 대한 ExpressRoute 회로 액세스를 사용하지 않도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="6f406-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="6f406-148">클래식 배포 모델에 대한 액세스를 사용하지 않도록 설정하려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="6f406-149">ExpressRoute 회로의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="6f406-150">"Allow Classic Operations"을 FALSE로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="6f406-151">회로를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-151">Update the circuit.</span></span> <span data-ttu-id="6f406-152">이 작업이 성공적으로 완료되면 클래식 배포 모델의 회로를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f406-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="6f406-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f406-153">Next steps</span></span>

* [<span data-ttu-id="6f406-154">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="6f406-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="6f406-155">가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="6f406-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)