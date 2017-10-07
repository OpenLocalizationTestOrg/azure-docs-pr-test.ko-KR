---
title: "API 관리 개요 및 키 개념 aaaAzure | Microsoft Docs"
description: "API, 제품, 역할, 그룹 및 기타 API 관리의 주요 개념에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a><span data-ttu-id="05bee-103">API 관리란?</span><span class="sxs-lookup"><span data-stu-id="05bee-103">What is API Management?</span></span>
<span data-ttu-id="05bee-104">API 관리 Api tooexternal, 파트너 및 해당 데이터 및 서비스의 내부 개발자 toounlock hello 잠재력을 게시 하는 조직은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-104">API Management helps organizations publish APIs tooexternal, partner and internal developers toounlock hello potential of their data and services.</span></span> <span data-ttu-id="05bee-105">기업 everywhere는 디지털 플랫폼으로 tooextend 자신의 작업을 찾고, 새 채널 만들기, 신규 고객을 찾고 기존 값과 업무 강화 운전 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-105">Businesses everywhere are looking tooextend their operations as a digital platform, creating new channels, finding new customers and driving deeper engagement with existing ones.</span></span> <span data-ttu-id="05bee-106">API 관리 개발자 참여, 비즈니스 통찰력, 분석, 보안 및 보호를 통해 성공적인 API 프로그램 hello 코어 능력 tooensure를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-106">API Management provides hello core competencies tooensure a successful API program through developer engagement, business insights, analytics, security and protection.</span></span>

<span data-ttu-id="05bee-107">Azure API 관리에 대 한 개요 비디오를 따라 hello를 감시 하 고 toouse API 관리 tooadd 많은 기능 tooyour 액세스 제어를 포함 하 여 API를 평가해 제한, 모니터링, 이벤트 로깅 및 응답을 위해 별도의 최소한의 노력으로 캐시에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-107">Watch hello following video for an overview of Azure API Management and learn how toouse API Management tooadd many features tooyour API, including access control, rate limiting, monitoring, event logging, and response caching, with minimal work on your part.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

<span data-ttu-id="05bee-108">API 관리 toouse 관리자 Api를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-108">toouse API Management, administrators create APIs.</span></span> <span data-ttu-id="05bee-109">각 API 하나 이상의 작업 구성 되며 tooone 개 이상의 제품에는 각 API를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-109">Each API consists of one or more operations, and each API can be added tooone or more products.</span></span> <span data-ttu-id="05bee-110">toouse API를 개발자가 해당 API를 포함 하는 tooa 제품 구독 및 다음 hello API의 작업을 적용 될 수 있는 제목 tooany 사용 정책을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-110">toouse an API, developers subscribe tooa product that contains that API, and then they can call hello API's operation, subject tooany usage policies that may be in effect.</span></span>

<span data-ttu-id="05bee-111">이 항목에서는 API 관리의 주요 개념을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-111">This topic provides an overview of API Management key concepts.</span></span>

> [!NOTE]
> <span data-ttu-id="05bee-112">자세한 내용은 참조 hello [클라우드 기반 API 관리: Api 전원 hello을 활용 하 여](http://j.mp/ms-apim-whitepaper) PDF 백서입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-112">For more information, see hello [Cloud-based API Management: Harnessing hello Power of APIs](http://j.mp/ms-apim-whitepaper) PDF whitepaper.</span></span> <span data-ttu-id="05bee-113">CITO Research의 API 관리에 대한 이 소개 백서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-113">This introductory whitepaper on API Management by CITO Research covers:</span></span> 
> 
> * <span data-ttu-id="05bee-114">공통 API 요구 사항 및 특징</span><span class="sxs-lookup"><span data-stu-id="05bee-114">Common API requirements and challenges</span></span>
> * <span data-ttu-id="05bee-115">API 분리 및 외관 제공</span><span class="sxs-lookup"><span data-stu-id="05bee-115">Decoupling APIs and presenting facades</span></span>
> * <span data-ttu-id="05bee-116">개발자가 시작 및 신속하게 실행</span><span class="sxs-lookup"><span data-stu-id="05bee-116">Getting developers up and running quickly</span></span>
> * <span data-ttu-id="05bee-117">액세스 보안</span><span class="sxs-lookup"><span data-stu-id="05bee-117">Securing access</span></span>
> * <span data-ttu-id="05bee-118">분석 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="05bee-118">Analytics and metrics</span></span>
> * <span data-ttu-id="05bee-119">API 관리 플랫폼으로 제어 및 파악</span><span class="sxs-lookup"><span data-stu-id="05bee-119">Gaining control and insight with an API Management platform</span></span>
> * <span data-ttu-id="05bee-120">클라우드 대 온-프레미스 솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="05bee-120">Using cloud vs on-premises solutions</span></span>
> * <span data-ttu-id="05bee-121">Azure API 관리</span><span class="sxs-lookup"><span data-stu-id="05bee-121">Azure API Management</span></span>
> 
> 

## <span data-ttu-id="05bee-122"><a name="apis"> </a>API 및 작업</span><span class="sxs-lookup"><span data-stu-id="05bee-122"><a name="apis"> </a>APIs and operations</span></span>
<span data-ttu-id="05bee-123">Api는 API 관리 서비스 인스턴스 hello foundation입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-123">APIs are hello foundation of an API Management service instance.</span></span> <span data-ttu-id="05bee-124">각 API에는 사용 가능한 toodevelopers 작업의 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-124">Each API represents  a set of operations available toodevelopers.</span></span> <span data-ttu-id="05bee-125">Hello API를 구현 하는 참조 toohello 백 엔드 서비스를 포함 하는 각 API 및 작업 맵 toohello 작업 hello 백 엔드 서비스에서 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-125">Each API contains a reference toohello back-end service that implements hello API, and its operations map toohello operations implemented by hello back-end service.</span></span> <span data-ttu-id="05bee-126">API 관리의 작업은 매우 다양하게 구성할 수 있으며 URL 매핑, 쿼리 및 경로 매개 변수, 요청 및 응답 콘텐츠, 작업 응답 캐싱 등을 더 효율적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-126">Operations in API Management are highly configurable, with control over URL mapping, query and path parameters, request and response content, and operation response caching.</span></span> <span data-ttu-id="05bee-127">속도 제한, 할당량 및 제한 정책을 IP hello API 또는 개별 작업 수준에서 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-127">Rate limit, quotas, and IP restriction policies can also be implemented at hello API or individual operation level.</span></span>

<span data-ttu-id="05bee-128">자세한 내용은 참조 [어떻게 toocreate Api] [ How toocreate APIs] 및 [어떻게 tooadd 작업 tooan API][How tooadd operations tooan API]합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-128">For more information, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="05bee-129"><a name="products"> </a> 제품</span><span class="sxs-lookup"><span data-stu-id="05bee-129"><a name="products"> </a> Products</span></span>
<span data-ttu-id="05bee-130">제품이 어떻게 Api는 toodevelopers 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-130">Products are how APIs are surfaced toodevelopers.</span></span> <span data-ttu-id="05bee-131">API 관리에서 제품은 하나 이상의 API를 가지며 제목, 설명, 사용 약관 등으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-131">Products in API Management have one or more APIs, and are configured with a title, description, and terms of use.</span></span> <span data-ttu-id="05bee-132">제품은 **개방형** 또는 **보호된** 제품일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-132">Products can be **Open** or **Protected**.</span></span> <span data-ttu-id="05bee-133">보호 된 제품에 사용할 수 있습니다, 열려 있는 동안 구독된 toobefore 여야 합니다. 구독 없이 제품을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-133">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="05bee-134">제품을 개발자가 사용할 수 있게 되면 제품을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-134">When a product is ready for use by developers it can be published.</span></span> <span data-ttu-id="05bee-135">게시를 후 볼 수 있습니다 (hello 보호 된 제품의 대/소문자를 구독) 개발자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-135">Once it is published, it can be viewed (and in hello case of protected products subscribed to) by developers.</span></span> <span data-ttu-id="05bee-136">구독 승인이 hello 제품 수준에서 구성 및 관리자 승인 필요 하거나 자동으로 승인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-136">Subscription approval is configured at hello product level and can either require administrator approval, or be auto-approved.</span></span>

<span data-ttu-id="05bee-137">그룹은 제품 toodevelopers의 사용 되는 toomanage hello 표시 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-137">Groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="05bee-138">제품은 가시성 toogroups 부여 및 개발자가 보고 하 고는 속해 있는 표시 toohello 그룹 toohello 제품을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-138">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> 

<span data-ttu-id="05bee-139">자세한 내용은 참조 [어떻게 toocreate 및 제품 게시] [ How toocreate and publish a product] 비디오 다음 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-139">For more information, see [How toocreate and publish a product][How toocreate and publish a product] and hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <span data-ttu-id="05bee-140"><a name="groups"> </a> 그룹</span><span class="sxs-lookup"><span data-stu-id="05bee-140"><a name="groups"> </a> Groups</span></span>
<span data-ttu-id="05bee-141">그룹은 제품 toodevelopers의 사용 되는 toomanage hello 표시 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-141">Groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="05bee-142">API 관리 hello 변경할 수 없는 시스템 그룹 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-142">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="05bee-143">**관리자** - Azure 구독 관리자가 이 그룹의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-143">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="05bee-144">관리자 API 관리 서비스 인스턴스, 관리 Api, 작업 및 개발자가 사용 하는 제품 hello 만들기.</span><span class="sxs-lookup"><span data-stu-id="05bee-144">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="05bee-145">**개발자** - 인증된 개발자 포털 사용자가 이 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-145">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="05bee-146">개발자는 Api를 사용 하 여 응용 프로그램을 구축 하는 hello 고객 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-146">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="05bee-147">개발자는 toohello 개발자 포털 액세스 권한이 부여 된 하 고 API의 hello 작업을 호출 하는 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-147">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="05bee-148">**게스트** -예:이 그룹에는 API 관리 인스턴스 년의 hello 개발자 포털을 방문 하는 잠재 고객의 개발자 포털 사용자가 인증 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-148">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="05bee-149">Hello 기능 tooview Api와 같은 특정 읽기 전용 액세스를 부여할 수 되지만 호출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-149">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="05bee-150">관리자 추가 toothese 시스템 그룹에 사용자 지정 그룹을 만들 수 있습니다 또는 [연결 된 Azure Active Directory 테 넌 트의 외부 그룹을 활용 하 여](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group)합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-150">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group).</span></span> <span data-ttu-id="05bee-151">사용자 지정 그룹과 외부 그룹 개발자 가시성 제공 시스템 그룹과 함께 사용할 수 있으며 tooAPI 제품에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-151">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="05bee-152">예를 들어 특정와 개발자가 파트너 조직 및의 액세스 허용 사용자 지정 그룹 하나 만들 수 있습니다 관련 Api만 포함 된 제품에서 Api toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-152">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="05bee-153">사용자는 두 그룹 이상의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-153">A user can be a member of more than one group.</span></span>

<span data-ttu-id="05bee-154">자세한 내용은 참조 [어떻게 toocreate 및 사용 하 여 그룹][How toocreate and use groups]합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-154">For more information, see  [How toocreate and use groups][How toocreate and use groups].</span></span>

## <span data-ttu-id="05bee-155"><a name="developers"> </a> 개발자</span><span class="sxs-lookup"><span data-stu-id="05bee-155"><a name="developers"> </a> Developers</span></span>
<span data-ttu-id="05bee-156">개발자는 API 관리 서비스 인스턴스에 hello 사용자 계정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-156">Developers represent hello user accounts in an API Management service instance.</span></span> <span data-ttu-id="05bee-157">Hello에서 등록할 수 또는 개발자가 만들어질 수도 있고 관리자가 toojoin 초대 [개발자 포털][Developer portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-157">Developers can be created or invited toojoin by administrators, or they can sign up from hello [Developer portal][Developer portal].</span></span> <span data-ttu-id="05bee-158">각 개발자 하나 이상의 그룹의 구성원이 며 toohello 제품은 가시성 toothose 그룹 권한을 부여 하는 구독 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-158">Each developer is a member of one or more groups, and can be subscribe toohello products that grant visibility toothose groups.</span></span>

<span data-ttu-id="05bee-159">Tooa 제품을 구독 하는 개발자가 기본 및 보조 키를 hello 제품에 대 한 hello 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-159">When developers subscribe tooa product they are granted hello primary and secondary key for hello product.</span></span> <span data-ttu-id="05bee-160">이 키는 hello 제품의 Api 호출할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-160">This key is used when making calls into hello product's APIs.</span></span>

<span data-ttu-id="05bee-161">자세한 내용은 참조 [어떻게 toocreate 또는 초대 개발자] [ How toocreate or invite developers] 및 [tooassociate 개발자와 그룹화 하는 방법을][How tooassociate groups with developers]합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-161">For more information, see [How toocreate or invite developers][How toocreate or invite developers] and [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="05bee-162"><a name="policies"> </a> 정책</span><span class="sxs-lookup"><span data-stu-id="05bee-162"><a name="policies"> </a> Policies</span></span>
<span data-ttu-id="05bee-163">정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 API 관리의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-163">Policies are a powerful capability of API Management that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="05bee-164">정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-164">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="05bee-165">인기 있는 문에 포함 XML tooJSON 및 호출 속도 제한 toorestrict hello 양을 개발자 로부터 들어오는 호출에서 형식 변환 및 다른 많은 정책을 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-165">Popular statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer, and many other policies are available.</span></span>

<span data-ttu-id="05bee-166">정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-166">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="05bee-167">Hello와 같은 일부 정책은 [제어 흐름](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) 및 [변수 설정](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) 정책은 정책 식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-167">Some policies such as hello [Control flow](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) and [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="05bee-168">자세한 내용은 참조 [고급 정책](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [정책 식을](https://msdn.microsoft.com/library/azure/dn910913.aspx), 조사식 hello 다음 비디오.</span><span class="sxs-lookup"><span data-stu-id="05bee-168">For more information, see [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx), and watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

<span data-ttu-id="05bee-169">API Management 정책의 전체 목록을 보려면 [정책 참조][Policy reference]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05bee-169">For a complete list of API Management policies, see [Policy reference][Policy reference].</span></span> <span data-ttu-id="05bee-170">정책 사용 및 구성에 대한 자세한 내용은 [API Management 정책][API Management policies]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05bee-170">For more information on using and configuring policies, see [API Management policies][API Management policies].</span></span> <span data-ttu-id="05bee-171">속도 제한 및 할당량 정책을 사용하여 제품을 만드는 방법에 대한 자습서는 [고급 제품 설정을 만들고 구성하는 방법][How create and configure advanced product settings]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05bee-171">For a tutorial on creating a product with rate limit and quota policies, see [How create and configure advanced product settings][How create and configure advanced product settings].</span></span> <span data-ttu-id="05bee-172">데모 비디오를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="05bee-172">For a demo, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <span data-ttu-id="05bee-173"><a name="developer-portal"> </a> 개발자 포털</span><span class="sxs-lookup"><span data-stu-id="05bee-173"><a name="developer-portal"> </a> Developer portal</span></span>
<span data-ttu-id="05bee-174">hello 개발자 포털 개발자 수 Api, 보기 및 호출 작업을 확인 하 고 구독 tooproducts은입니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-174">hello developer portal is where developers can learn about your APIs, view and call operations, and subscribe tooproducts.</span></span> <span data-ttu-id="05bee-175">잠재 고객 hello 개발자 포털을 방문할 수 있는 Api 및 작업을 확인 하 고 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-175">Prospective customers can visit hello developer portal, view APIs and operations, and sign up.</span></span> <span data-ttu-id="05bee-176">개발자 포털에 대 한 hello URL은 API 관리 서비스 인스턴스에 대 한 hello Azure 클래식 포털에서에서 hello 대시보드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-176">hello URL for your developer portal is located on hello dashboard in hello Azure Classic Portal for your API Management service instance.</span></span>

<span data-ttu-id="05bee-177">사용자 지정 내용을 추가 스타일을 사용자 지정 하 고 브랜드를 추가 하 여 개발자 포털을 가리키도록의 hello 모양과 느낌을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-177">You can customize hello look and feel of your developer portal by adding custom content, customizing styles, and adding your branding.</span></span>

## <a name="api-management-and-hello-api-economy"></a><span data-ttu-id="05bee-178">API 관리 및 hello API 경제</span><span class="sxs-lookup"><span data-stu-id="05bee-178">API Management and hello API economy</span></span>
<span data-ttu-id="05bee-179">API 관리, Microsoft Ignite 2015 hello 컨퍼런스에서 프레젠테이션을 다음 조사식 hello에 대 한 자세한 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="05bee-179">toolearn more about API Management, watch hello following presentation from hello Microsoft Ignite 2015 conference.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




