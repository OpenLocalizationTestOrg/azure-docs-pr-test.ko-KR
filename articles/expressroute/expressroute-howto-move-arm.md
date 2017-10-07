---
title: "클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동: PowerShell: Azure | Microsoft Docs"
description: "이 페이지에서는 PowerShell을 사용 하 여 클래식 회로 toohello 리소스 관리자 배포 toomove을 모델링 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="9b0a0-103">PowerShell을 사용 하 여 hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="9b0a0-104">리소스 관리자 배포 모델 및 클래식 hello에 대 한 ExpressRoute 회로 toouse hello 회로 toohello 리소스 관리자 배포 모델을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="9b0a0-105">hello 다음 섹션에서는 PowerShell을 사용 하 여 회로 이동 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b0a0-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9b0a0-106">Before you begin</span></span>

* <span data-ttu-id="9b0a0-107">Hello Azure PowerShell 모듈의 최신 버전 hello 있는지 확인 하십시오 (이상 버전 1.0).</span><span class="sxs-lookup"><span data-stu-id="9b0a0-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="9b0a0-108">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9b0a0-109">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="9b0a0-110">제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="9b0a0-111">완전히 이해 하는 hello 제한 및 제한 사항이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="9b0a0-112">Hello 회로 hello 클래식 배포 모델에서 완전 하 게 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="9b0a0-113">Hello 리소스 관리자 배포 모델에서 만든 리소스 그룹 가졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="9b0a0-114">ExpressRoute 회로 이동</span><span class="sxs-lookup"><span data-stu-id="9b0a0-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="9b0a0-115">1 단계: hello 클래식 배포 모델에서 회로 세부 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="9b0a0-116">Azure 클래식 환경 toohello에 로그인 하 고 hello 서비스 키를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="9b0a0-117">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="9b0a0-118">Hello 적절 한 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="9b0a0-119">Azure 및 express 경로 대 한 hello PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="9b0a0-120">모든 ExpressRoute 회로 대 한 tooget hello 서비스 키 아래의 hello cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="9b0a0-121">Hello 키를 검색 한 후 복사 hello **서비스 키** toomove toohello 리소스 관리자 배포 모델을 사용 하지 않겠다고 hello 회로의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="9b0a0-122">2단계: 로그인하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9b0a0-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="9b0a0-123">리소스 관리자 환경을 toohello 하 고 새 리소스 그룹 만들기 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="9b0a0-124">Tooyour Azure Resource Manager 환경에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="9b0a0-125">Hello 적절 한 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="9b0a0-126">리소스 그룹을 아직 없는 경우 hello 조각 toocreate 새 리소스 그룹을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="9b0a0-127">3 단계: hello ExpressRoute 회로 toohello 리소스 관리자 배포 모델을 이동</span><span class="sxs-lookup"><span data-stu-id="9b0a0-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="9b0a0-128">사용자는 이제 준비 toomove hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 express 경로 회로입니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="9b0a0-129">계속 하기 전에 제공 하는 hello 정보를 검토 [hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="9b0a0-130">toomove 회로 수정 하 고 다음 코드 조각 hello 실행:</span><span class="sxs-lookup"><span data-stu-id="9b0a0-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="9b0a0-131">Hello 이동 완료 되 면 hello 이전 cmdlet에 나열 된 hello 새 이름을 사용 하는 tooaddress hello 리소스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="9b0a0-132">hello 회로 기본적으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="9b0a0-133">회로 액세스 수정</span><span class="sxs-lookup"><span data-stu-id="9b0a0-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="9b0a0-134">두 가지 경우 모두에 대 한 express 경로 회로 액세스 tooenable</span><span class="sxs-lookup"><span data-stu-id="9b0a0-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="9b0a0-135">클래식 express 경로 회로 toohello 리소스 관리자 배포 모델을 이동한 후 액세스 tooboth 배포 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="9b0a0-136">Hello cmdlet tooenable 액세스 tooboth 배포 모델을 따라를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="9b0a0-137">Hello 회로 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="9b0a0-138">"클래식 작업 허용" tooTRUE를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="9b0a0-139">Hello 회로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-139">Update hello circuit.</span></span> <span data-ttu-id="9b0a0-140">이 작업을 성공적으로 완료 되 면 hello 클래식 배포 모델에서 수 tooview hello 회로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="9b0a0-141">다음 cmdlet tooget hello ExpressRoute 회로의 세부 정보 hello hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="9b0a0-142">나열 된 수 toosee hello 서비스 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="9b0a0-143">이제 클래식 Vnet 및 hello 리소스 관리자 명령에 대 한 hello 클래식 배포 모델 명령을 사용 하 여 리소스 관리자 Vnet에 대 한 링크 toohello ExpressRoute 회로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="9b0a0-144">hello 다음 문서는 데 도움이 링크 toohello ExpressRoute 회로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="9b0a0-145">가상 네트워크 tooyour hello 리소스 관리자 배포 모델에서 ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="9b0a0-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="9b0a0-146">가상 네트워크 tooyour hello 클래식 배포 모델의 ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="9b0a0-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="9b0a0-147">toodisable ExpressRoute 회로 액세스 toohello 클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="9b0a0-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="9b0a0-148">Hello cmdlet toodisable 액세스 toohello 클래식 배포 모델을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="9b0a0-149">Hello ExpressRoute 회로의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="9b0a0-150">"클래식 작업 허용" tooFALSE를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="9b0a0-151">Hello 회로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-151">Update hello circuit.</span></span> <span data-ttu-id="9b0a0-152">이 작업을 성공적으로 완료 되 면 hello 클래식 배포 모델에서 수 tooview hello 회로 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b0a0-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="9b0a0-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b0a0-153">Next steps</span></span>

* [<span data-ttu-id="9b0a0-154">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="9b0a0-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="9b0a0-155">가상 네트워크 tooyour ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="9b0a0-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
