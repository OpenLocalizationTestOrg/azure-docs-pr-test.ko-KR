---
title: "ExpressRoute 회로 만들기 및 수정: PowerShell: Azure 클래식 | Microsoft Docs"
description: "이 문서에서는 Express 경로 회로를 만들고 프로비전하는 단계를 안내합니다. 또한 상태 확인, 업데이트 또는 삭제 및 프로비전 해제 방법을 보여 줍니다."
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
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="2025f-104">PowerShell을 사용하여 ExpressRoute 회로 만들기 및 수정(클래식)</span><span class="sxs-lookup"><span data-stu-id="2025f-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2025f-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2025f-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="2025f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2025f-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="2025f-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2025f-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="2025f-108">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2025f-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="2025f-109">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="2025f-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="2025f-110">이 문서에서는 PowerShell cmdlet 및 일반 배포 모델을 사용하여 Azure Express 경로 회로를 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="2025f-111">이 문서는 ExpressRoute 회로의 상태 확인, 업데이트 또는 삭제 및 프로비전 해제를 수행하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="2025f-112">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="2025f-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="2025f-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2025f-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="2025f-114">1단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-114">Step 1.</span></span> <span data-ttu-id="2025f-115">필수 조건 및 워크플로 문서에 대한 검토</span><span class="sxs-lookup"><span data-stu-id="2025f-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="2025f-116">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md)를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="2025f-117">2단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-117">Step 2.</span></span> <span data-ttu-id="2025f-118">최신 버전의 Azure SM(서비스 관리) PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="2025f-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="2025f-119">Azure PowerShell 모듈을 사용하도록 컴퓨터를 구성하는 방법에 대한 단계별 지침은 [Azure PowerShell cmdlet 시작](/powershell/azure/overview)에 나온 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="2025f-120">3단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-120">Step 3.</span></span> <span data-ttu-id="2025f-121">Azure 계정에 로그인 및 구독 선택</span><span class="sxs-lookup"><span data-stu-id="2025f-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="2025f-122">상승된 권한으로 PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="2025f-123">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="2025f-124">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="2025f-125">둘 이상의 구독이 있는 경우 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="2025f-126">다음 cmdlet을 사용하여 클래식 배포 모델용 PowerShell에 Azure 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="2025f-127">Express 경로 회로 만들기 및 프로비전</span><span class="sxs-lookup"><span data-stu-id="2025f-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="2025f-128">1단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-128">Step 1.</span></span> <span data-ttu-id="2025f-129">Express 경로에 대한 PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="2025f-130">먼저 ExpressRoute cmdlet을 사용할 수 있도록 Azure와 ExpressRoute 모듈을 PowerShell 세션으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="2025f-131">로컬 컴퓨터에 설치된 위치에 있는 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="2025f-132">이 위치는 모듈 설치에 사용한 방법에 따라 다음 예제와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="2025f-133">따라서 필요한 경우 예제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="2025f-134">2단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-134">Step 2.</span></span> <span data-ttu-id="2025f-135">지원되는 공급자, 위치 및 대역폭 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="2025f-136">Express 경로 회로를 만들기 전에 지원되는 연결 공급자, 위치 및 대역폭 옵션 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="2025f-137">PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` 은(는) 이후 단계에서 사용할 이 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="2025f-138">연결 공급자가 여기에 나열되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="2025f-139">다음 정보는 나중에 회로를 만들 때 필요하므로 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="2025f-140">이름</span><span class="sxs-lookup"><span data-stu-id="2025f-140">Name</span></span>
* <span data-ttu-id="2025f-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="2025f-141">PeeringLocations</span></span>
* <span data-ttu-id="2025f-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="2025f-142">BandwidthsOffered</span></span>

<span data-ttu-id="2025f-143">이제 Express 경로 회로를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="2025f-144">3단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-144">Step 3.</span></span> <span data-ttu-id="2025f-145">Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="2025f-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="2025f-146">아래 예제에서는 Equinix 실리콘밸리를 통해 200Mbps Express 경로 회로를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="2025f-147">다른 공급자와 다른 설정을 사용하는 경우, 요청을 수행할 때 해당 정보를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2025f-148">Express 경로 회로는 서비스 키가 발급된 순간부터 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="2025f-149">연결 공급자가 회로를 프로비전할 준비가 된 후에 이 작업을 수행하도록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2025f-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="2025f-150">다음은 새 서비스 키에 대한 예제 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="2025f-151">또는 프리미엄 추가 기능을 통해 Express 경로 회로를 만들려면 다음 예를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="2025f-152">프리미엄 추가 기능에 대한 자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="2025f-153">응답에 서비스 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-153">The response will contain the service key.</span></span> <span data-ttu-id="2025f-154">다음을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="2025f-155">4단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-155">Step 4.</span></span> <span data-ttu-id="2025f-156">모든 Express 경로 회로 나열</span><span class="sxs-lookup"><span data-stu-id="2025f-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="2025f-157">만들어 놓은 모든 Express 경로 회로 목록을 가져오려면 `Get-AzureDedicatedCircuit` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="2025f-158">응답은 다음 예와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="2025f-159">`Get-AzureDedicatedCircuit` cmdlet을 사용하여 이 정보를 언제든지 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="2025f-160">매개 변수 없이 호출을 수행하면 모든 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="2025f-161">서비스 키는 *ServiceKey* 필드에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="2025f-162">다음을 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="2025f-163">5단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-163">Step 5.</span></span> <span data-ttu-id="2025f-164">프로비전을 위해 연결 공급자에 서비스 키 보내기</span><span class="sxs-lookup"><span data-stu-id="2025f-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="2025f-165">*ServiceProviderProvisioningState* 는 서비스 공급자 측의 현재 프로비전 상태에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="2025f-166">*Status* 는 Microsoft 측의 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="2025f-167">회로 프로비전 상태에 대한 자세한 내용은 [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="2025f-168">새 Express 경로 회로를 만들면 회로는 다음 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="2025f-169">연결 공급자가 사용자에 대해 활성화를 처리 중이면 다음 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="2025f-170">Express 경로 회로를 사용하려면 다음 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="2025f-171">6단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-171">Step 6.</span></span> <span data-ttu-id="2025f-172">회로 키의 상태를 주기적으로 확인</span><span class="sxs-lookup"><span data-stu-id="2025f-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="2025f-173">이를 통해 공급자가 회로 활성화를 마치면 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="2025f-174">회로가 구성된 후에는 *ServiceProviderProvisioningState*가 아래 예에서처럼 *Provisioned*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="2025f-175">7단계.</span><span class="sxs-lookup"><span data-stu-id="2025f-175">Step 7.</span></span> <span data-ttu-id="2025f-176">라우팅 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="2025f-176">Create your routing configuration</span></span>
<span data-ttu-id="2025f-177">단계별 지침은 [Express 경로 회로 라우팅 구성(회로 피어링 만들기 및 수정)](expressroute-howto-routing-classic.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2025f-178">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="2025f-179">관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="2025f-180">8단계:</span><span class="sxs-lookup"><span data-stu-id="2025f-180">Step 8.</span></span> <span data-ttu-id="2025f-181">가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="2025f-182">그 다음 가상 네트워크를 Express 경로 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="2025f-183">단계별 지침은 [Express 경로 회로에 가상 네트워크 연결](expressroute-howto-linkvnet-classic.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="2025f-184">ExpressRoute에 클래식 배포 모델을 사용하여 가상 네트워크를 만들어야 하는 경우 [ExpressRoute에 대해 가상 네트워크 만들기](expressroute-howto-vnet-portal-classic.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="2025f-185">Express 경로 회로의 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="2025f-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="2025f-186">`Get-AzureCircuit` cmdlet을 사용하여 이 정보를 언제든지 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="2025f-187">매개 변수 없이 호출을 수행하면 모든 회로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-187">Making the call without any parameters lists all the circuits.</span></span>

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

<span data-ttu-id="2025f-188">서비스 키를 매개 변수 형태로 호출에 전달하면 특정 Express 경로 회로에 대한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="2025f-189">다음 예제를 실행하여 모든 매개 변수에 대한 자세한 설명을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="2025f-190">Express 경로 회로 수정</span><span class="sxs-lookup"><span data-stu-id="2025f-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="2025f-191">연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="2025f-192">가동 중지 시간 없이 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="2025f-193">Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="2025f-194">포트에 사용 가능한 용량이 있는 경우 ExpressRoute 회로의 대역폭을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="2025f-195">회로 대역폭 다운그레이드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="2025f-196">요금제를 데이터 요금에서 무제한 데이터 요금으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="2025f-197">요금제를 무제한 데이터 요금에서 데이터 요금으로 변경하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="2025f-198">*Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="2025f-199">제한 및 제한 사항에 대한 자세한 내용은 [Express 경로 FAQ](expressroute-faqs.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="2025f-200">Express 경로 Premium 추가 기능을 활성화하려면</span><span class="sxs-lookup"><span data-stu-id="2025f-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="2025f-201">다음 PowerShell cmdlet을 사용하여 기존 회로에 대해 Express 경로 프리미엄 추가 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="2025f-202">이제 Express 경로 프리미엄 추가 기능을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="2025f-203">명령이 성공적으로 실행되는 즉시 프리미엄 추가 기능에 대한 청구가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="2025f-204">Express 경로 Premium 추가 기능을 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="2025f-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2025f-205">표준 회로에 허용된 것보다 많은 리소스를 사용할 경우 이 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="2025f-206">고려 사항</span><span class="sxs-lookup"><span data-stu-id="2025f-206">Considerations</span></span>

* <span data-ttu-id="2025f-207">프리미엄을 표준으로 다운그레이드하기 전에 회로에 연결된 가상 네트워크 수가 10개 미만인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="2025f-208">그렇지 않으면 업데이트 요청이 실패하고 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="2025f-209">다른 지리적 위치의 모든 가상 네트워크를 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="2025f-210">그렇지 않으면 업데이트 요청이 실패하고 프리미엄 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="2025f-211">사설 피어링을 위해서는 경로 테이블의 경로가 4000개 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="2025f-212">경로 테이블 크기가 4000개 경로 이상이면 BGP 세션이 폐기되고 게시된 프리픽스 수가 4000개 미만이 될 때까지 다시 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="2025f-213">Premium 추가 기능 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="2025f-213">Disable the premium add-on</span></span>
<span data-ttu-id="2025f-214">다음 PowerShell cmdlet을 사용하여 기존 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="2025f-215">Express 경로 회로 대역폭을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="2025f-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="2025f-216">공급자에 대해 지원되는 대역폭 옵션은 [Express 경로 FAQ](expressroute-faqs.md) 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="2025f-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="2025f-217">물리적 포트(회로가 생성되어 있는)에 허용되는 한 기존 회로보다 크다면 어떤 크기든 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2025f-218">기존 포트에 적절한 용량이 없는 경우 ExpressRoute 회로를 다시 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="2025f-219">해당 위치에서 사용 가능한 추가 용량이 없는 경우 해당 회로를 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="2025f-220">그러나 중단 없이 Express 경로 회로의 대역폭을 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="2025f-221">대역폭을 다운그레이드하려면 Express 경로 회로의 프로비전을 해제하고 새 Express 경로 회로를 다시 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="2025f-222">회로 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2025f-222">Resize a circuit</span></span>

<span data-ttu-id="2025f-223">필요한 크기를 선택한 후에, 다음 명령을 사용하여 회로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="2025f-224">회로의 크기는 Microsoft 쪽에서 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="2025f-225">변경에 부합하게 구성을 업데이트하려면 해당 공급자에게 연락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="2025f-226">이 지점에서 업데이트된 대역폭 옵션에 대한 요금을 청구하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="2025f-227">회로 대역폭을 증가시킬 때 다음과 같은 오류가 표시되면 기존 회로가 생성된 물리적 포트에 남아있는 대역폭이 충분하지 않다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="2025f-228">이 회로를 삭제하고 필요한 크기의 회로를 새로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="2025f-229">Express 경로 회로 프로비전 해제 및 삭제</span><span class="sxs-lookup"><span data-stu-id="2025f-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="2025f-230">고려 사항</span><span class="sxs-lookup"><span data-stu-id="2025f-230">Considerations</span></span>

* <span data-ttu-id="2025f-231">이 작업이 성공하려면 모든 가상 네트워크를 Express 경로 회로에서 연결 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="2025f-232">이 작업이 실패할 경우 회로에 연결된 가상 네트워크가 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="2025f-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="2025f-233">ExpressRoute 회로 서비스 공급자 프로비전 상태가 **프로비전 중** 또는 **프로비전됨**인 경우에는 서비스 공급자에게 회로 프로비전 해제를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="2025f-234">서비스 공급자가 회로의 프로비전을 해제한 다음 통지를 보낼 때까지 리소스가 계속 예약되며 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="2025f-235">서비스 공급자가 회로 프로비전을 해제하여 서비스 공급자 프로비전 상태가 **프로비전되지 않음**이 되면 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="2025f-236">그러면 회로에 대한 요금 청구가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="2025f-237">회로 삭제</span><span class="sxs-lookup"><span data-stu-id="2025f-237">Delete a circuit</span></span>

<span data-ttu-id="2025f-238">다음 명령을 실행하여 Express 경로 회로를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="2025f-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2025f-239">Next steps</span></span>
<span data-ttu-id="2025f-240">회로를 만든 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2025f-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="2025f-241">Express 경로 회로의 라우팅 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="2025f-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="2025f-242">가상 네트워크를 Express 경로 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="2025f-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

