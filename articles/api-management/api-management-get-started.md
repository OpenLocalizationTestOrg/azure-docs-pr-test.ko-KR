---
title: "aaaManage Azure API 관리에서 첫 번째 API | Microsoft Docs"
description: "Toocreate Api, 작업을 추가 하 고 API 관리 시작 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="e9709-103">Azure API 관리에서 첫 번째 API 관리</span><span class="sxs-lookup"><span data-stu-id="e9709-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="e9709-104"><a name="overview"> </a>개요</span><span class="sxs-lookup"><span data-stu-id="e9709-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="e9709-105">이 가이드에는 tooquickly Azure API 관리를 사용 하 여 시작 하 고 첫 번째 API 호출을 확인 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="e9709-106"><a name="concepts"> </a>Azure API 관리란?</span><span class="sxs-lookup"><span data-stu-id="e9709-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="e9709-107">Azure API 관리 tootake 원하는 백 엔드를 사용할 수 있으며 그에 따라 기능을 갖춘 API 프로그램을 시작.</span><span class="sxs-lookup"><span data-stu-id="e9709-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="e9709-108">일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-108">Common scenarios include:</span></span>

* <span data-ttu-id="e9709-109">**모바일 인프라 보안** </span><span class="sxs-lookup"><span data-stu-id="e9709-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="e9709-110">**ISV 파트너 에코 시스템을 사용 하도록 설정** hello 개발자 통해 빠른 파트너 온 보 딩을 제공 하 여 포털 하는 API 외관 toodecouple 구현 내부에서 작성 되며 없습니다 서식 파일을 파트너 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="e9709-111">**내부 API 프로그램을 실행** hello 가용성 및 최신 버전에 대 한 hello 조직 toocommunicate tooAPIs 변경에 대 한 중앙된 위치를 제공 하 여 조직 계정 기반 액세스 제어 모두 기반 간의 보안된 채널 hello API 게이트웨이 및 hello 백 엔드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="e9709-112">hello 시스템 hello 다음과 같은 구성 요소가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="e9709-113">hello **API 게이트웨이** 는 hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="e9709-114">API를 호출 하 고 라우팅하 tooyour 백 엔드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="e9709-115">API 키, JWT 토큰, 인증서 및 기타 자격 증명을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="e9709-116">사용 할당량 및 속도 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="e9709-117">코드를 수정 하지 않고 hello 즉석에서 API를 변형합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="e9709-118">설정된 위치에 백 엔드 응답을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="e9709-119">분석용으로 호출 메타데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="e9709-120">hello **게시자 포털** API 프로그램을 설정한 hello 관리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="e9709-121">다음 작업을 수행하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-121">Use it to:</span></span>
  
  * <span data-ttu-id="e9709-122">API 스키마를 정의하거나 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-122">Define or import API schema.</span></span>
  * <span data-ttu-id="e9709-123">제품에 API를 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-123">Package APIs into products.</span></span>
  * <span data-ttu-id="e9709-124">할당량 또는 hello Api에 대 한 변형 같은 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="e9709-125">분석의 정보를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="e9709-126">사용자를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-126">Manage users.</span></span>
* <span data-ttu-id="e9709-127">hello **개발자 포털** 역할을 hello 기본 웹 사이트는 개발자를 위한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="e9709-128">API 설명서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-128">Read API documentation.</span></span>
  * <span data-ttu-id="e9709-129">Hello 대화형 콘솔을 통해 API를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="e9709-130">계정을 만들고 tooget API 키를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="e9709-131">자신의 사용량에 대한 분석에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="e9709-132"><a name="create-service-instance"> </a>API 관리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e9709-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="e9709-133">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e9709-134">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="e9709-135">자세한 내용은 [Azure 무료 평가판][Azure Free Trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9709-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="e9709-136">hello 첫 번째 작업의 단계에서는 API 관리 toocreate 서비스 인스턴스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="e9709-137">Toohello 로그인 [Azure 포털] [ Azure Portal] 클릭 **새로**, **웹 + 모바일**, **API 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API 관리 새 인스턴스][api-management-create-instance-menu]

<span data-ttu-id="e9709-139">에 대 한 **이름**, hello 서비스 URL에 대 한 고유한 하위 도메인 이름을 toouse를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="e9709-140">원하는 hello 선택 **구독**, **리소스 그룹** 및 **위치** 서비스 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="e9709-141">입력 **Contoso ltd.** hello에 대 한 **조직 이름**, hello에 전자 메일 주소를 입력 하 고 **관리자 전자 메일** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="e9709-142">이 전자 메일 주소는 hello API 관리 시스템에서에서 알림에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="e9709-143">자세한 내용은 참조 [어떻게 tooconfigure 알림 하 고 Azure API 관리에서 서식 파일을 전자 메일로][How tooconfigure notifications and email templates in Azure API Management]합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![새 API 관리 서비스][api-management-create-instance-step1]

<span data-ttu-id="e9709-145">API 관리 서비스 인스턴스는 Developer, Standard, Premium의 세 가지 계층으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="e9709-146">hello 개발자 계층 개발, 테스트 및 파일럿 API 프로그램 고가용성은 문제가 되지입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="e9709-147">Hello 표준 및 프리미엄 계층에서는 예약된 단위 개수 toohandle 더 많은 트래픽을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="e9709-148">대부분의 처리 능력 및 성능을 hello Standard 및 Premium 계층 hello 사용 하 여 API 관리 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="e9709-149">임의 계층을 사용하여 이 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="e9709-150">API Management 계층에 대한 자세한 내용은 [API Management 가격][API Management pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9709-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="e9709-151">클릭 **만들기** toostart 서비스 인스턴스를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-151">Click **Create** toostart provisioning your service instance.</span></span>

![새 API 관리 서비스][api-management-instance-created]

<span data-ttu-id="e9709-153">Hello 서비스 인스턴스를 만든 후 hello 다음 단계는 toocreate 가져오거나 API.</span><span class="sxs-lookup"><span data-stu-id="e9709-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="e9709-154"><a name="create-api"> </a>API 가져오기</span><span class="sxs-lookup"><span data-stu-id="e9709-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="e9709-155">API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="e9709-156">API 작업은 웹 서비스 프록시 tooexisting입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="e9709-157">API를 만들고 작업을 수동으로 추가하거나 API를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="e9709-158">이 자습서에서는 Microsoft에서 제공 하 고 Azure에서 호스팅되는 샘플 계산기 웹 서비스에 대 한 API hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e9709-159">API를 만들고 수동으로 추가 하는 작업에 대 한 지침을 참조 하십시오. [어떻게 toocreate Api](api-management-howto-create-apis.md) 및 [어떻게 tooadd 작업 tooan API](api-management-howto-add-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="e9709-160">Api는 hello 게시자 포털에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="e9709-161">tooreach, 클릭 **게시자 포털** hello 서비스 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="e9709-163">tooimport hello 계산기 API 클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **가져오기 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![API 가져오기 단추][api-management-import-api]

<span data-ttu-id="e9709-165">Hello 단계 tooconfigure hello 계산기 API 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="e9709-166">클릭 **From URL**, 입력 **http://calcapi.cloudapp.net/calcapi.json** hello에 **사양 문서 URL** 텍스트 상자, 한 hello 클릭 **Swagger**  라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="e9709-167">형식 **calc** hello에 **웹 API URL 접미사** 입력란.</span><span class="sxs-lookup"><span data-stu-id="e9709-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="e9709-168">Hello에 클릭 **(선택 사항) 제품** 확인란을 선택한 **스타터**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="e9709-169">클릭 **저장** tooimport hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-169">Click **Save** tooimport hello API.</span></span>

![새 API 추가][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="e9709-171">**API 관리**는 현재 가져오기에 대한 Swagger 문서의 1.2 및 2.0 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="e9709-172">[Swagger 2.0 사양](http://swagger.io/specification)에서 `host`, `basePath` 및 `schemes` 속성이 선택 사항이라고 선언하더라도 Swagger 2.0 문서는 해당 속성을 **반드시** 포함해야 합니다. 그렇지 않으면 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="e9709-173">가져온 hello API는 hello hello API에 대 한 요약 페이지에에서 표시 됩니다 hello 게시자 포털.</span><span class="sxs-lookup"><span data-stu-id="e9709-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API 요약][api-management-imported-api-summary]

<span data-ttu-id="e9709-175">hello API 섹션에 여러 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-175">hello API section has several tabs.</span></span> <span data-ttu-id="e9709-176">hello **요약** 기본 메트릭 및 hello API에 대 한 정보 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="e9709-177">hello [설정을](api-management-howto-create-apis.md#configure-api-settings) 탭은 API에 대 한 사용 되는 tooview 및 편집 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="e9709-178">hello [작업](api-management-howto-add-operations.md) 탭은 사용 되는 toomanage hello API의 작업으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="e9709-179">hello **보안** 탭은 기본 인증을 사용 하 여 hello 백 엔드 서버에 대 한 사용된 tooconfigure 게이트웨이 인증 수 또는 [상호 인증서 인증](api-management-howto-mutual-certificates.md), 및 tooconfigure [ OAuth 2.0을 사용 하 여 사용자 권한 부여](api-management-howto-oauth2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="e9709-180">hello **문제** 탭은 Api를 사용 하는 hello 개발자 보고 사용 하는 tooview 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="e9709-181">hello **제품** 탭은이 API를 포함 하는 사용 되는 tooconfigure hello 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="e9709-182">기본적으로 각 API 관리 인스턴스는 두 개의 샘플 제품과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="e9709-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="e9709-183">**Starter**</span></span>
* <span data-ttu-id="e9709-184">**무제한**</span><span class="sxs-lookup"><span data-stu-id="e9709-184">**Unlimited**</span></span>

<span data-ttu-id="e9709-185">이 자습서에서는 API hello를 가져올 때 기본 계산기 API hello toohello Starter 제품에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="e9709-186">순서 toomake 호출 tooan api에서 개발자가 access tooit을 제공 하는 tooa 제품 먼저 구독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="e9709-187">개발자는 tooproducts hello 개발자 포털에서 구독할 수 있습니다 또는 관리자가 개발자 tooproducts hello 게시자 포털에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="e9709-188">Hello API 관리 인스턴스 hello에서 이전 단계에서에서 만든 hello 자습서 하므로 기본적으로 구독 된 tooevery 제품은 이미 하기 때문에 관리자를 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="e9709-189"><a name="call-operation"></a>Hello 개발자 포털에서 작업 호출</span><span class="sxs-lookup"><span data-stu-id="e9709-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="e9709-190">작업 편리 tooview 제공 하는 hello 개발자 포털에서 직접 호출할 수 있습니다 및 API의 hello 작동을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="e9709-191">이 자습서 단계에서는 hello 기본 계산기 API를 호출 합니다 **정수 두 개를 추가** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="e9709-192">클릭 **개발자 포털** hello에 hello 메뉴에서 hello 게시자 포털의 오른쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="e9709-194">클릭 **Api** hello 상단 메뉴에서 **기본 계산기** toosee hello 사용 가능한 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![개발자 포털][api-management-developer-portal-calc-api]

<span data-ttu-id="e9709-196">Note hello 샘플 설명과 함께 hello API 및이 작업을 사용 하는 hello 개발자에 대 한 설명서를 제공 하는 작업을 가져온 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="e9709-197">작업을 수동으로 추가하는 경우 이러한 설명을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="e9709-198">toocall hello **정수 두 개를 추가** 작업을 클릭 하 여 **실습**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![시도][api-management-developer-portal-calc-api-console]

<span data-ttu-id="e9709-200">Hello 매개 변수에 대 한 일부 값을 입력 하 또는 hello 기본값을 유지 하 고 클릭 수 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="e9709-202">작업이 호출 hello 개발자 포털 hello 표시 **응답 상태**, hello **응답 헤더**, 임의의 **응답 콘텐츠**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![응답][api-management-invoke-get-response]

## <span data-ttu-id="e9709-204"><a name="view-analytics"> </a>분석 보기</span><span class="sxs-lookup"><span data-stu-id="e9709-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="e9709-205">기본 계산기를 선택 하 여 스위치 백 toohello 게시자 포털에 대 한 tooview 분석 **관리** hello에 hello 메뉴에서 hello 개발자 포털의 오른쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![관리][api-management-manage-menu]

<span data-ttu-id="e9709-207">hello hello 게시자 포털에 대 한 기본 보기는 hello **대시보드**, 해당 API 관리 인스턴스에 대 한 개요를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![대시보드][api-management-dashboard]

<span data-ttu-id="e9709-209">에 대 한 hello 차트 위로 hello 마우스 호버 **기본 계산기** toosee hello 특정 메트릭을의 지정 된 기간에 대 한 API hello hello 사용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="e9709-210">모든 줄 보이지 않으면 차트에서 뒤로 toohello 개발자 포털 및 API hello 일부 호출, 몇 분 정도 전환한 다음 돌아와서 toohello 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="e9709-211">클릭 **세부 정보 보기** tooview hello 요약 페이지 API 표시 하는 hello 메트릭 중 더 큰 버전을 포함 하 여 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![분석][api-management-mouse-over]

![요약][api-management-api-summary-metrics]

<span data-ttu-id="e9709-214">자세한 메트릭 및 보고서에 대 한 클릭 **분석** hello에서 **API 관리** hello 왼쪽 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e9709-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![개요][api-management-analytics-overview]

<span data-ttu-id="e9709-216">hello **분석** 섹션에 다음 4 개의 탭 hello:</span><span class="sxs-lookup"><span data-stu-id="e9709-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="e9709-217">**한 눈에** 뿐만 아니라 상위 개발자, 상위 제품, 상위 Api 및 상위 작업 hello 전반적인 사용 현황 및 상태 메트릭을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="e9709-218">**사용량** 에서는 지리적 표현을 포함하여 API 호출 및 대역폭을 심도 있게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="e9709-219">**상태** 에서는 상태 코드, 캐시 성공률, 응답 시간, API 및 서비스 응답 시간을 위주로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="e9709-220">**활동** hello 개발자, 제품, API 및 작업에서 특정 활동에 드릴 다운 하는 보고서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="e9709-221"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9709-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="e9709-222">너무 방법에 대해 알아봅니다[속도 제한 된 API 보호](api-management-howto-product-with-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9709-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
