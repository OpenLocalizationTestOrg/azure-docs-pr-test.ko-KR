---
title: "Azure ExpressRoute Microsoft 피어링에 대한 경로 필터 구성: PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용 하 여 Microsoft 피어 링에 대 한 tooconfigure 경로 필터 하는 방법을 설명합니다"
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
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="41af4-103">Microsoft 피어링에 대한 경로 필터 구성</span><span class="sxs-lookup"><span data-stu-id="41af4-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="41af4-104">경로 필터는 방식으로 tooconsume Microsoft 피어 링을 통해 지원 되는 서비스의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="41af4-105">이 문서 도움말 구성 하 고 ExpressRoute 회로 대 한 경로 필터 관리에 hello 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="41af4-106">Dynamics 365 서비스 및 비즈니스에 대 한 Exchange Online, SharePoint Online 및 Skype와 같은 Office 365 서비스는 hello Microsoft 피어 링을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="41af4-107">Microsoft 피어 링 express 경로 회로에 구성 되 면 모든 접두사 관련된 toothese 서비스는 설정 된 hello BGP 세션을 통해 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="41af4-108">BGP 커뮤니티 값은 연결 된 tooevery 접두사 tooidentify hello 서비스 hello 접두사를 통해 제공 된입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="41af4-109">Hello BGP 커뮤니티 값과 매핑되는 hello 서비스의 목록에 대 한 참조 [BGP 커뮤니티](expressroute-routing.md#bgp)합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="41af4-110">연결 tooall 서비스를 필요로 하는 경우 많은 수의 접두사는 BGP를 통해 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="41af4-111">이 네트워크 라우터에서 관리 hello 경로 테이블의 hello 크기 크게 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="41af4-112">Microsoft 피어 링을 통해 제공 되는 서비스의 하위 집합만 tooconsume 하려는 경우 두 가지 방법으로 경로 테이블의 hello 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="41af4-113">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-113">You can:</span></span>

- <span data-ttu-id="41af4-114">BGP 커뮤니티에 라우팅 필터를 적용하여 필요 없는 접두사를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="41af4-115">표준 네트워킹 방법은 많은 네트워크 내에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="41af4-116">경로 필터를 정의 하 고 tooyour ExpressRoute 회로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="41af4-117">경로 필터는 새 리소스의 hello 목록을 선택할 수 있습니다 서비스를 Microsoft 피어 링을 통해 tooconsume 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="41af4-118">ExpressRoute 라우터는만 hello hello 경로 필터에서 식별 된 toohello 서비스에 속하는 접두사 목록을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="41af4-119"><a name="about"></a>경로 필터 정보</span><span class="sxs-lookup"><span data-stu-id="41af4-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="41af4-120">Microsoft 피어 링 express 경로 회로에 구성 되 면 hello Microsoft에 지 라우터는 한 쌍의 BGP 세션을 원하는 대로 이동해 왔거나 연결 공급자의에 지 라우터를 hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="41af4-121">경로가 보급된 tooyour 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="41af4-122">tooenable 경로 광고 tooyour 네트워크 경로 필터를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="41af4-123">경로 필터를 사용 하면 ExpressRoute 회로 Microsoft 피어 링을 통해 tooconsume 서비스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="41af4-124">모든 hello BGP 커뮤니티 값의 허용 목록을 경우합니다</span><span class="sxs-lookup"><span data-stu-id="41af4-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="41af4-125">경로 필터 리소스 정의 tooan ExpressRoute 회로 연결 되 면 toohello BGP 커뮤니티 값에 매핑되는 모든 접두사는 보급된 tooyour 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="41af4-126">Office 365 서비스에 toobe 수 tooattach 경로 필터, ExpressRoute 통해 권한 부여 tooconsume Office 365 서비스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="41af4-127">ExpressRoute 통해 권한 있는 tooconsume Office 365 서비스에 없으면 hello 작업 tooattach 경로 필터 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="41af4-128">Hello 권한 부여 프로세스에 대 한 자세한 내용은 참조 [Office 365에 대 한 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="41af4-129">연결 tooDynamics 365 서비스에 모든 권한을 가지 지 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41af4-130">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="41af4-131">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="41af4-132"><a name="workflow"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="41af4-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="41af4-133">toobe 수 toosuccessfully Microsoft 피어 링을 통해 tooservices 연결, hello 다음 구성 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="41af4-134">Microsoft 피어링을 프로비전하는 활성 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="41af4-135">이러한 작업 지침 tooaccomplish 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="41af4-136">[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="41af4-137">ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="41af4-138">[Microsoft 피어 링 만들기](expressroute-circuit-peerings.md) 직접 hello BGP 세션을 관리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="41af4-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="41af4-139">또는 연결 공급자가 회로에 Microsoft 피어링을 프로비전하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="41af4-140">경로 필터를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="41af4-141">식별 hello tooconsume Microsoft 피어 링을 통해 서비스</span><span class="sxs-lookup"><span data-stu-id="41af4-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="41af4-142">Hello 서비스와 관련 된 BGP 커뮤니티 값의 hello 목록 확인</span><span class="sxs-lookup"><span data-stu-id="41af4-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="41af4-143">한 규칙 tooallow hello 접두사 목록 일치 하는 hello BGP 커뮤니티 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="41af4-144">Hello 경로 필터 toohello ExpressRoute 회로 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="41af4-145">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="41af4-145">Before you begin</span></span>

<span data-ttu-id="41af4-146">구성을 시작 하기 전에 hello 다음 조건을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="41af4-147">Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="41af4-148">자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/install-azurerm-ps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41af4-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="41af4-149">Hello 설치 관리자를 사용 하 여 보다는 hello PowerShell 갤러리에서 hello 최신 버전을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="41af4-150">현재 설치 관리자 hello hello 필요한 cmdlet을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="41af4-151">검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="41af4-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="41af4-152">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="41af4-153">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="41af4-154">ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="41af4-155">활성 Microsoft 피어링이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="41af4-156">[피어링 구성 수정 및 만들기](expressroute-circuit-peerings.md)의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="41af4-157">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="41af4-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="41af4-158">이 구성을 시작 하기 전에 tooyour Azure 계정에에서 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="41af4-159">hello cmdlet Azure 계정에 대 한 hello 로그인 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="41af4-160">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="41af4-161">상승 된 권한으로 PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="41af4-162">다음 예제에서는 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="41af4-163">여러 Azure 구독이 있는 경우 hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="41af4-164">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="41af4-165"><a name="prefixes"></a>1단계.</span><span class="sxs-lookup"><span data-stu-id="41af4-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="41af4-166">접두사 및 BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="41af4-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="41af4-167">1. BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="41af4-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="41af4-168">관련 된 접두사 목록을 hello 및 hello Microsoft 피어 링을 통해 액세스할 수 있는 서비스와 관련 된 BGP 커뮤니티 값 목록이 tooget hello cmdlet을 다음 사용:</span><span class="sxs-lookup"><span data-stu-id="41af4-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="41af4-169">2. 원하는 toouse hello 값 목록을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="41af4-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="41af4-170">Hello 경로 필터에 원하는 BGP 커뮤니티 값 목록이 toouse을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="41af4-171">예를 들어 hello Dynamics 365 서비스에 대 한 BGP 커뮤니티 값 12076:5040 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="41af4-172"><a name="filter"></a>2단계.</span><span class="sxs-lookup"><span data-stu-id="41af4-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="41af4-173">경로 필터 및 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="41af4-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="41af4-174">경로 필터 규칙을 하나만 가질 수 있습니다 및 hello 규칙 '허용' 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="41af4-175">이 규칙에는 관련된 BGP 커뮤니티 값의 목록이 있을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="41af4-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="41af4-176">1. 경로 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="41af4-176">1. Create a route filter</span></span>

<span data-ttu-id="41af4-177">먼저 hello 경로 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-177">First, create hello route filter.</span></span> <span data-ttu-id="41af4-178">hello 명령 ' 새로 만들기-AzureRmRouteFilter'만 경로 필터 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="41af4-179">Hello 리소스를 만든 후 다음 규칙을 만들고 해야 toohello 경로 필터 개체를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="41af4-180">경로 필터 리소스 hello 명령 toocreate 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="41af4-181">2. 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="41af4-181">2. Create a filter rule</span></span>

<span data-ttu-id="41af4-182">Hello 예제와 같이 쉼표로 구분 된 목록으로 BGP 커뮤니티의 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="41af4-183">다음 명령은 toocreate hello 새 규칙을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="41af4-184">3. Hello 규칙 toohello 경로 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="41af4-185">다음 명령 tooadd hello 필터 규칙 toohello 경로 필터 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="41af4-186"><a name="attach"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="41af4-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="41af4-187">Hello 경로 필터 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="41af4-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="41af4-188">Hello 명령 tooattach hello 경로 필터 toohello ExpressRoute 회로 유일한 Microsoft 피어 링 했 고 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="41af4-189"><a name="getproperties"></a>경로 필터의 tooget hello 속성</span><span class="sxs-lookup"><span data-stu-id="41af4-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="41af4-190">경로 필터의 tooget hello 속성 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="41af4-191">다음 명령은 tooget hello 경로 필터 리소스 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="41af4-192">Hello 다음 명령을 실행 하 여 hello 경로 필터 리소스에 대 한 hello 경로 필터 규칙을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="41af4-193"><a name="updateproperties"></a>경로 필터의 tooupdate hello 속성</span><span class="sxs-lookup"><span data-stu-id="41af4-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="41af4-194">Hello 경로 필터는 이미 연결 되어 있는 경우 회로 tooa 업데이트 toohello BGP 커뮤니티 목록을 자동으로 설정 하는 hello BGP 세션을 통해 적절 한 접두사 광고 변경 내용을 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="41af4-195">다음 명령을 hello를 사용 하 여 경로 필터 목록이 BGP 커뮤니티 hello를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="41af4-196"><a name="detach"></a>ExpressRoute 회로에서 경로 필터 toodetach</span><span class="sxs-lookup"><span data-stu-id="41af4-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="41af4-197">경로 필터 hello ExpressRoute 회로에서 분리 되 면 접두사가 hello BGP 세션을 통해 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="41af4-198">필터에서 다음 명령을 hello를 사용 하 여 ExpressRoute 회로 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="41af4-199"><a name="delete"></a>경로 필터 toodelete</span><span class="sxs-lookup"><span data-stu-id="41af4-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="41af4-200">삭제 되지 않았으면 경로 필터 tooany 회로 연결에 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="41af4-201">해당 hello 경로 필터 되지 않도록 tooany 회로 toodelete 시도 하기 전에 연결 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="41af4-202">다음 명령을 hello를 사용 하 여 필터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="41af4-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41af4-203">Next steps</span></span>

<span data-ttu-id="41af4-204">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41af4-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
