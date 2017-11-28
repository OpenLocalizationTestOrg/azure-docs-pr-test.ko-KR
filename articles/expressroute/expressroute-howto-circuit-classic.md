---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure 클래식 | Microsoft Docs"
description: "이 문서를 만들고 ExpressRoute 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, 회로가 프로 비전 해제 알 수 있습니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="5ad85-104">PowerShell을 사용하여 ExpressRoute 회로 만들기 및 수정(클래식)</span><span class="sxs-lookup"><span data-stu-id="5ad85-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ad85-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5ad85-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="5ad85-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ad85-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="5ad85-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5ad85-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="5ad85-108">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5ad85-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="5ad85-109">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="5ad85-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="5ad85-110">이 문서를 안내해 hello 단계 toocreate Azure ExpressRoute 회로 PowerShell cmdlet 및 hello 클래식 배포 모델을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="5ad85-111">또한이 문서를 보면 어떻게 toocheck hello 상태 업데이트 또는 삭제 하 고, ExpressRoute 회로 프로 비전 해제 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="5ad85-112">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="5ad85-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="5ad85-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5ad85-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="5ad85-114">1단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-114">Step 1.</span></span> <span data-ttu-id="5ad85-115">Hello 필수 구성 요소 및 워크플로 기사를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="5ad85-116">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5ad85-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="5ad85-117">2단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-117">Step 2.</span></span> <span data-ttu-id="5ad85-118">Hello hello Azure 서비스 관리 (SM) PowerShell 모듈의 최신 버전 설치</span><span class="sxs-lookup"><span data-stu-id="5ad85-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="5ad85-119">Hello 지침에 따라 [Azure PowerShell cmdlet 시작](/powershell/azure/overview) 방법에 대 한 단계별 지침에 대 한 tooconfigure 컴퓨터 toouse hello Azure PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="5ad85-120">3단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-120">Step 3.</span></span> <span data-ttu-id="5ad85-121">Tooyour Azure 계정에에서 로그인을 구독 선택</span><span class="sxs-lookup"><span data-stu-id="5ad85-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="5ad85-122">관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="5ad85-123">다음 예제에서는 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="5ad85-124">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="5ad85-125">둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="5ad85-126">를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="5ad85-127">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="5ad85-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="5ad85-128">1단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-128">Step 1.</span></span> <span data-ttu-id="5ad85-129">ExpressRoute에 대 한 hello PowerShell 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ad85-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="5ad85-130">이미 수행 hello Azure 및 ExpressRoute 모듈에서 순서 toostart hello ExpressRoute cmdlet을 사용 하 여 hello PowerShell 세션으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="5ad85-131">Hello 모듈을 가져올 hello 있었던 위치 설치 tooon 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="5ad85-132">Tooinstall hello 모듈을 사용해 hello 방법에 따라, hello 위치 hello 다음 예제와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="5ad85-133">필요한 경우 hello 예제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="5ad85-134">2단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-134">Step 2.</span></span> <span data-ttu-id="5ad85-135">지원 되는 공급자, 위치 및 대역폭 hello 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="5ad85-136">ExpressRoute 회로 만들기 전에 hello 지원 되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="5ad85-137">PowerShell cmdlet을 hello `Get-AzureDedicatedCircuitServiceProvider` 이후 단계에서 사용 하는이 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="5ad85-138">연결 공급자가 여기에 나열 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="5ad85-139">Hello 회로 만들 때 나중에 필요 합니다 하기 때문에 다음 정보를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="5ad85-140">이름</span><span class="sxs-lookup"><span data-stu-id="5ad85-140">Name</span></span>
* <span data-ttu-id="5ad85-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="5ad85-141">PeeringLocations</span></span>
* <span data-ttu-id="5ad85-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="5ad85-142">BandwidthsOffered</span></span>

<span data-ttu-id="5ad85-143">이제 준비 toocreate ExpressRoute 회로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="5ad85-144">3단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-144">Step 3.</span></span> <span data-ttu-id="5ad85-145">Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="5ad85-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="5ad85-146">다음 예제는 hello Silicon Valley에 Equinix 통해 toocreate 200 50mbps ExpressRoute 회로 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="5ad85-147">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ad85-148">ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="5ad85-149">Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="5ad85-150">hello 다음 새 서비스 키에 대 한 예제 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="5ad85-151">또는 다음 예제를 사용 하 여 hello toocreate hello premium 추가 기능으로 ExpressRoute 회로 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="5ad85-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="5ad85-152">Toohello 참조 [express 경로 FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="5ad85-153">hello 응답 hello 서비스 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-153">hello response will contain hello service key.</span></span> <span data-ttu-id="5ad85-154">Hello 다음을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="5ad85-155">4단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-155">Step 4.</span></span> <span data-ttu-id="5ad85-156">모든 hello ExpressRoute 회로 나열</span><span class="sxs-lookup"><span data-stu-id="5ad85-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="5ad85-157">Hello를 실행할 수 있습니다 `Get-AzureDedicatedCircuit` tooget 모든 목록이 만든 ExpressRoute 회로 hello 명령:</span><span class="sxs-lookup"><span data-stu-id="5ad85-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="5ad85-158">hello 응답에는 다음 예제는 다음과 유사한 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5ad85-159">Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ad85-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="5ad85-160">Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="5ad85-161">서비스 키 hello에 나열 될 *ServiceKey* 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5ad85-162">Hello 다음을 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="5ad85-163">5단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-163">Step 5.</span></span> <span data-ttu-id="5ad85-164">Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기</span><span class="sxs-lookup"><span data-stu-id="5ad85-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="5ad85-165">*ServiceProviderProvisioningState* hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="5ad85-166">*상태* Microsoft의 hello에 hello 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="5ad85-167">상태를 프로 비전 하는 회로 대 한 자세한 내용은 참조 hello [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서.</span><span class="sxs-lookup"><span data-stu-id="5ad85-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="5ad85-168">새 ExpressRoute 회로 만들 때 다음 상태 hello hello 회로가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="5ad85-169">hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 상태 뒤에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="5ad85-170">ExpressRoute 회로에 있어야 하면 toobe 수 toouse에 대 한 상태에 따라 hello 것:</span><span class="sxs-lookup"><span data-stu-id="5ad85-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="5ad85-171">6단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-171">Step 6.</span></span> <span data-ttu-id="5ad85-172">Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="5ad85-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="5ad85-173">이를 통해 공급자가 회로 활성화를 마치면 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="5ad85-174">Hello 회로 구성한 후 *ServiceProviderProvisioningState* 모양으로 표시 됩니다 *프로 비전 됨* hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="5ad85-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="5ad85-175">7단계.</span><span class="sxs-lookup"><span data-stu-id="5ad85-175">Step 7.</span></span> <span data-ttu-id="5ad85-176">라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="5ad85-176">Create your routing configuration</span></span>
<span data-ttu-id="5ad85-177">Toohello 참조 [ExpressRoute 회로 라우팅 구성 (만들고 회로 피어 링 수정)](expressroute-howto-routing-classic.md) 단계별 지침에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ad85-178">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="5ad85-179">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="5ad85-180">8단계:</span><span class="sxs-lookup"><span data-stu-id="5ad85-180">Step 8.</span></span> <span data-ttu-id="5ad85-181">가상 네트워크 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="5ad85-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="5ad85-182">다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="5ad85-183">너무 참조[연결 ExpressRoute 회로 toovirtual 네트워크](expressroute-howto-linkvnet-classic.md) 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="5ad85-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="5ad85-184">ExpressRoute에 대 한 hello 클래식 배포 모델을 사용 하 여 가상 네트워크 toocreate 해야 할 경우 참조 [ExpressRoute에 대 한 가상 네트워크 만들기](expressroute-howto-vnet-portal-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="5ad85-185">ExpressRoute 회로의 hello 상태를 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ad85-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="5ad85-186">Hello를 사용 하 여 언제 든 지가이 정보를 검색할 수 `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ad85-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="5ad85-187">Hello 매개 변수 없이 호출을 만드는 모든 hello 회로 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5ad85-188">Hello 서비스 키 매개 변수 toohello 호출으로 전달 하 여 특정 ExpressRoute 회로 대 한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="5ad85-189">다음 예제는 hello를 실행 하 여 모든 hello 매개 변수에 대 한 자세한 설명을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="5ad85-190">Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="5ad85-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="5ad85-191">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="5ad85-192">할 수 있는 가동 중지 시간 없이 사용 다음과 같습니다. hello:</span><span class="sxs-lookup"><span data-stu-id="5ad85-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="5ad85-193">Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="5ad85-194">증가 hello 대역폭의 ExpressRoute 회로 제공 된 hello 포트에서 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="5ad85-195">참고는 회로의 대역폭 hello 다운 그레이드는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="5ad85-196">데이터 요금 tooUnlimited 데이터에서에서 계획을 계량 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="5ad85-197">Note 변경 hello 계량 계획에서 무제한 데이터 요금 tooMetered 데이터가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="5ad85-198">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="5ad85-199">Toohello 참조 [express 경로 FAQ](expressroute-faqs.md) 제한 및 제한 사항에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="5ad85-200">tooenable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="5ad85-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="5ad85-201">Hello 다음 PowerShell cmdlet을 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="5ad85-202">지금 회로 사용 하도록 설정 하는 hello ExpressRoute premium 추가 기능을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="5ad85-203">Note hello 명령이 성공적으로 실행 되는 즉시 hello premium 추가 기능에 대 한 청구 먼저 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="5ad85-204">toodisable hello ExpressRoute premium 추가 기능</span><span class="sxs-lookup"><span data-stu-id="5ad85-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ad85-205">이 작업은 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 하는 경우 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="5ad85-206">고려 사항</span><span class="sxs-lookup"><span data-stu-id="5ad85-206">Considerations</span></span>

* <span data-ttu-id="5ad85-207">Toostandard premium에서에서 다운 그레이드 하기 전에 가상 네트워크 연결 된 toohello 회로 hello 수는 10 보다 작은 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="5ad85-208">이렇게 하지 않으면 업데이트 요청이 못하며, 프리미엄 요금이 청구 된 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="5ad85-209">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="5ad85-210">이렇게 하지 않으면 업데이트 요청이 못하며, 프리미엄 요금이 청구 된 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="5ad85-211">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="5ad85-212">경로 테이블 크기가 4, 000 경로 보다 큰 경우 hello BGP 세션 삭제 됩니다 하 고 보급된 된 접두사의 hello 수가 4, 000 하위 메뉴를 클릭 될 때까지 했다가 다시 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="5ad85-213">Hello premium 추가 기능을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="5ad85-213">Disable hello premium add-on</span></span>
<span data-ttu-id="5ad85-214">Hello 다음 PowerShell cmdlet을 사용 하 여 기존 회로 대 한 hello ExpressRoute premium 추가 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="5ad85-215">tooupdate hello ExpressRoute 회로 대역폭</span><span class="sxs-lookup"><span data-stu-id="5ad85-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="5ad85-216">Hello 확인 [express 경로 FAQ](expressroute-faqs.md) 지원 공급자에 대 한 대역폭 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="5ad85-217">기존 회로 hello 크기 보다 큰는 상태로 유지 됩니다 (회로 생성 되) hello 실제 포트를 사용 하면 모든 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ad85-218">Hello 기존 포트에서 부적절 한 용량이 있으면 toorecreate hello ExpressRoute 회로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="5ad85-219">해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="5ad85-220">Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="5ad85-221">대역폭을 다운 그레이드 toodeprovision hello ExpressRoute 회로 해야 하 고 새 ExpressRoute 회로 다시 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="5ad85-222">회로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="5ad85-222">Resize a circuit</span></span>

<span data-ttu-id="5ad85-223">필요한 크기를 결정 한 다음 회로 명령 tooresize 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5ad85-224">회로는 hello Microsoft 쪽 조정 된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="5ad85-225">이러한 변경의 쪽 toomatch 사용자 연결 공급자 tooupdate 구성을 게 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="5ad85-226">이 시점에서 대역폭 옵션에서 업데이트 하는 참고는 먼저 hello에 대 한 청구 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="5ad85-227">Hello hello 회로 대역폭을 늘릴 때 다음 오류가 표시 되 면 것 의미 합니다. 기존 회로 만들 위치 hello 실제 포트에 남아 있는 충분 한 대역폭 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="5ad85-228">이 회로 toodelete 있고 필요한 hello 크기의 새 회로 만들기.</span><span class="sxs-lookup"><span data-stu-id="5ad85-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="5ad85-229">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="5ad85-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="5ad85-230">고려 사항</span><span class="sxs-lookup"><span data-stu-id="5ad85-230">Considerations</span></span>

* <span data-ttu-id="5ad85-231">이 작업 toosucceed에 대 한 express 경로 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="5ad85-232">확인 toosee 있는 모든 가상 네트워크가 있는 경우이 작업이 실패 하면 toohello 회로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="5ad85-233">Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨** 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="5ad85-234">Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="5ad85-235">Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 (hello 서비스 공급자 프로 비전 상태가 너무 설정 되어**프로 비전 되지**) hello 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="5ad85-236">Hello 회로 대 한 요금 청구를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="5ad85-237">회로 삭제</span><span class="sxs-lookup"><span data-stu-id="5ad85-237">Delete a circuit</span></span>

<span data-ttu-id="5ad85-238">Hello 다음 명령을 실행 하 여 ExpressRoute 회로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="5ad85-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ad85-239">Next steps</span></span>
<span data-ttu-id="5ad85-240">회로 만든 후 다음 hello 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad85-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="5ad85-241">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="5ad85-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="5ad85-242">가상 네트워크 tooyour ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="5ad85-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

