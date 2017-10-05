---
title: "Azure ExpressRoute Microsoft 피어링에 대한 경로 필터 구성: PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용하여 Microsoft 피어링에 대한 경로 필터를 구성하는 방법을 설명합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: de3550c20439fa809869d98b8a57ea3be9c03e7c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="824f5-103">Microsoft 피어링에 대한 경로 필터 구성</span><span class="sxs-lookup"><span data-stu-id="824f5-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="824f5-104">경로 필터는 Microsoft 피어링을 통해 지원되는 서비스의 하위 집합을 사용하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="824f5-105">이 문서의 단계는 ExpressRoute 회로에 대한 경로 필터를 구성하고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="824f5-106">Dynamics 365 서비스 및 Exchange Online, SharePoint Online 및 비즈니스용 Skype와 같은 Office 365 서비스는 Microsoft 피어링을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="824f5-107">Microsoft 피어링이 ExpressRoute 회로에 구성되면 설정된 BGP 세션을 통해 이러한 서비스와 관련된 모든 접두사가 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="824f5-108">BGP 커뮤니티 값은 접두사를 통해 제공되는 서비스를 식별하는 모든 접두사에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="824f5-109">BGP 커뮤니티 값과 매핑되는 서비스의 목록은 [BGP 커뮤니티](expressroute-routing.md#bgp)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="824f5-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="824f5-110">모든 서비스에 연결해야 하는 경우 많은 수의 접두사가 BGP를 통해 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="824f5-111">그러면 네트워크 내의 라우터에서 유지 관리되는 경로 테이블의 크기가 상당히 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="824f5-112">Microsoft 피어링을 통해 제공되는 서비스의 하위 집합만 사용하려는 경우 두 가지 방법으로 경로 테이블의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="824f5-113">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-113">You can:</span></span>

- <span data-ttu-id="824f5-114">BGP 커뮤니티에 라우팅 필터를 적용하여 필요 없는 접두사를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="824f5-115">표준 네트워킹 방법은 많은 네트워크 내에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="824f5-116">경로 필터를 정의하고 ExpressRoute 회로에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="824f5-117">경로 필터는 Microsoft 피어링을 통해 사용하려는 서비스 목록을 선택할 수 있는 새 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="824f5-118">ExpressRoute 라우터는 경로 필터에서 식별된 서비스에 속하는 접두사 목록만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="824f5-119"><a name="about"></a>경로 필터 정보</span><span class="sxs-lookup"><span data-stu-id="824f5-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="824f5-120">Microsoft 피어링이 ExpressRoute 회로에 구성되면 Microsoft 에지 라우터는 에지 라우터(사용자 또는 연결 공급자 소유)를 사용하여 한 쌍의 BGP 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="824f5-121">경로는 네트워크에 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-121">No routes are advertised to your network.</span></span> <span data-ttu-id="824f5-122">네트워크에 경로 보급을 사용하려면 경로 필터를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="824f5-123">경로 필터를 사용하면 ExpressRoute 회로의 Microsoft 피어링을 통해 사용하려는 서비스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="824f5-124">특히 모든 BGP 커뮤니티 값의 허용 목록입니다</span><span class="sxs-lookup"><span data-stu-id="824f5-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="824f5-125">경로 필터 리소스가 정의되고 ExpressRoute 회로에 연결되면 BGP 커뮤니티 값에 매핑되는 모든 접두사는 네트워크에 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="824f5-126">경로 필터를 Office 365 서비스에 연결할 수 있으려면 ExpressRoute를 통해 Office 365 서비스를 사용할 수 있는 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="824f5-127">ExpressRoute를 통해 Office 365 서비스를 사용할 수 있는 권한이 없는 경우 경로 필터를 연결하는 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="824f5-128">권한 부여 프로세스에 대한 자세한 내용은 [Office 365용 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="824f5-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="824f5-129">Dynamics 365 서비스에 대한 연결에는 사전 권한 부여가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="824f5-130">경로 필터를 정의하지 않은 경우에도 2017년 8월 1일 이전에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 Microsoft 피어링을 통해 보급된 모든 서비스 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="824f5-131">2017년 8월 1일 이후에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 경로 필터가 회로에 연결될 때까지 접두사가 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="824f5-132"><a name="workflow"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="824f5-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="824f5-133">Microsoft 피어링을 통해 서비스에 성공적으로 연결할 수 있으려면 다음 구성 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="824f5-134">Microsoft 피어링을 프로비전하는 활성 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="824f5-135">다음 지침을 사용하여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="824f5-136">[ExpressRoute 회로를 만들고](expressroute-howto-circuit-arm.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="824f5-137">ExpressRoute 회로는 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="824f5-138">직접 BGP 세션을 관리하는 경우 [Microsoft 피어링을 만듭니다](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="824f5-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="824f5-139">또는 연결 공급자가 회로에 Microsoft 피어링을 프로비전하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="824f5-140">경로 필터를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="824f5-141">Microsoft 피어링을 통해 사용하려는 서비스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="824f5-142">서비스와 연결된 BGP 커뮤니티 값의 목록을 식별합니다</span><span class="sxs-lookup"><span data-stu-id="824f5-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="824f5-143">BGP 커뮤니티 값과 일치하는 접두사 목록을 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="824f5-144">경로 필터를 ExpressRoute 회로에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="824f5-145">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="824f5-145">Before you begin</span></span>

<span data-ttu-id="824f5-146">구성을 시작하기 전에 다음 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="824f5-147">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-147">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="824f5-148">자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/install-azurerm-ps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="824f5-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="824f5-149">설치 관리자를 사용하는 대신 PowerShell 갤러리에서 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-149">Download the latest version from the PowerShell Gallery, rather than using the Installer.</span></span> <span data-ttu-id="824f5-150">현재 설치 관리자는 필요한 cmdlet을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-150">The Installer currently does not support the required cmdlets.</span></span>
  > 

 - <span data-ttu-id="824f5-151">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="824f5-152">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="824f5-153">지침을 수행하여 [Express 경로 회로를 만들고](expressroute-howto-circuit-arm.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-153">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="824f5-154">ExpressRoute 회로는 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="824f5-155">활성 Microsoft 피어링이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="824f5-156">[피어링 구성 수정 및 만들기](expressroute-circuit-peerings.md)의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="824f5-157">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-157">Log in to your Azure account</span></span>

<span data-ttu-id="824f5-158">이 구성을 시작하기 전에 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-158">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="824f5-159">Cmdlet가 Azure 계정에 대한 로그인 자격 증명을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-159">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="824f5-160">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-160">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="824f5-161">상승된 권한으로 PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-161">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="824f5-162">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-162">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="824f5-163">Azure 구독이 여러 개인 경우 계정의 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-163">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="824f5-164">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-164">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="824f5-165"><a name="prefixes"></a>1단계.</span><span class="sxs-lookup"><span data-stu-id="824f5-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="824f5-166">접두사 및 BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="824f5-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="824f5-167">1. BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="824f5-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="824f5-168">다음 cmdlet을 사용하여 Microsoft 피어링을 통해 액세스할 수 있는 서비스와 관련된 BGP 커뮤니티 값의 목록 및 관련된 접두사 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-168">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="824f5-169">2. 사용하려는 값의 목록 확인</span><span class="sxs-lookup"><span data-stu-id="824f5-169">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="824f5-170">경로 필터에 사용하려는 BGP 커뮤니티 값 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-170">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="824f5-171">예를 들어, Dynamics 365 서비스의 BGP 커뮤니티 값은 12076:5040입니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-171">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="824f5-172"><a name="filter"></a>2단계.</span><span class="sxs-lookup"><span data-stu-id="824f5-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="824f5-173">경로 필터 및 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="824f5-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="824f5-174">경로 필터에는 하나의 규칙만이 있을 수 있고 규칙은 '허용' 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-174">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="824f5-175">이 규칙에는 관련된 BGP 커뮤니티 값의 목록이 있을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="824f5-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="824f5-176">1. 경로 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="824f5-176">1. Create a route filter</span></span>

<span data-ttu-id="824f5-177">먼저, 경로 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-177">First, create the route filter.</span></span> <span data-ttu-id="824f5-178">'New-AzureRmRouteFilter' 명령은 경로 필터 리소스만을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-178">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="824f5-179">리소스를 만든 후에 규칙을 만들고 경로 필터 개체에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-179">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="824f5-180">다음 명령을 실행하여 경로 필터 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-180">Run the following command to create a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="824f5-181">2. 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="824f5-181">2. Create a filter rule</span></span>

<span data-ttu-id="824f5-182">이 예제에 나와 있는 대로 BGP 커뮤니티의 집합을 쉼표로 구분된 목록으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-182">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span></span> <span data-ttu-id="824f5-183">다음 명령을 실행하여 새 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-183">Run the following command to create a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-the-rule-to-the-route-filter"></a><span data-ttu-id="824f5-184">3. 경로 필터에 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="824f5-184">3. Add the rule to the route filter</span></span>

<span data-ttu-id="824f5-185">다음 명령을 실행하여 필터 규칙을 경로 필터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-185">Run the following command to add the filter rule to the route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="824f5-186"><a name="attach"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="824f5-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="824f5-187">경로 필터를 ExpressRoute 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-187">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="824f5-188">Microsoft 피어링만 있다고 가정하고 다음 명령을 실행하여 경로 필터를 ExpressRoute 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-188">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="824f5-189"><a name="getproperties"></a>경로 필터의 속성을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="824f5-189"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="824f5-190">경로 필터의 속성을 가져오려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-190">To get the properties of a route filter, use the following steps:</span></span>

1. <span data-ttu-id="824f5-191">다음 명령을 실행하여 경로 필터 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-191">Run the following command to get the route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="824f5-192">다음 명령을 실행하여 경로 필터 리소스에 대한 경로 필터 규칙을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-192">Get the route filter rules for the route-filter resource by running the following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="824f5-193"><a name="updateproperties"></a>경로 필터의 속성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="824f5-193"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="824f5-194">경로 필터가 이미 회로에 연결된 경우 BGP 커뮤니티 목록에 대한 업데이트로 인해 설정된 BGP 세션을 통해 적절한 접두사 보급 변경 내용을 자동으로 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-194">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagates appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="824f5-195">다음 명령을 사용하여 경로 필터의 BGP 커뮤니티 목록을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-195">You can update the BGP community list of your route filter using the following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="824f5-196"><a name="detach"></a>ExpressRoute 회로에서 경로 필터를 분리하려면</span><span class="sxs-lookup"><span data-stu-id="824f5-196"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="824f5-197">경로 필터를 ExpressRoute 회로에서 분리하면 접두사가 BGP 세션을 통해 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-197">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="824f5-198">다음 명령을 사용하여 ExpressRoute 회로에서 경로 필터를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-198">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="824f5-199"><a name="delete"></a>경로 필터를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="824f5-199"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="824f5-200">회로에 연결되지 않은 경우에만 필터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-200">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="824f5-201">경로 필터를 삭제하기 전에 회로에 연결되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-201">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="824f5-202">다음 명령을 사용하여 경로 필터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="824f5-202">You can delete a route filter using the following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="824f5-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="824f5-203">Next steps</span></span>

<span data-ttu-id="824f5-204">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="824f5-204">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>