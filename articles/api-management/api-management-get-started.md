---
title: "Azure API Management에서 첫 번째 API 관리 | Microsoft Docs"
description: "API를 만들고, 작업을 추가하고, API 관리를 시작하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="cbfa1-103">Azure API 관리에서 첫 번째 API 관리</span><span class="sxs-lookup"><span data-stu-id="cbfa1-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="cbfa1-104"><a name="overview"> </a>개요</span><span class="sxs-lookup"><span data-stu-id="cbfa1-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="cbfa1-105">이 가이드에서는 빠르게 Azure API 관리를 사용하기 시작하고 첫 번째 API 호출을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="cbfa1-106"><a name="concepts"> </a>Azure API 관리란?</span><span class="sxs-lookup"><span data-stu-id="cbfa1-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="cbfa1-107">Azure API 관리를 통해 원하는 백 엔드를 사용하고 해당 백 엔드에 따라 모든 기능을 갖춘 API 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="cbfa1-108">일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-108">Common scenarios include:</span></span>

* <span data-ttu-id="cbfa1-109">**모바일 인프라 보안** </span><span class="sxs-lookup"><span data-stu-id="cbfa1-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="cbfa1-110">**ISV 파트너 시스템 사용** </span><span class="sxs-lookup"><span data-stu-id="cbfa1-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="cbfa1-111">**내부 API 프로그램 실행** </span><span class="sxs-lookup"><span data-stu-id="cbfa1-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="cbfa1-112">시스템은 다음 구성 요소로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="cbfa1-113">**API 게이트웨이** 는 다음 작업을 수행하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="cbfa1-114">API 호출 수락 후 백 엔드로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="cbfa1-115">API 키, JWT 토큰, 인증서 및 기타 자격 증명을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="cbfa1-116">사용 할당량 및 속도 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="cbfa1-117">코드 수정 없이 즉석에서 API를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="cbfa1-118">설정된 위치에 백 엔드 응답을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="cbfa1-119">분석용으로 호출 메타데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="cbfa1-120">**게시자 포털** 은 API 프로그램이 설치되는 관리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="cbfa1-121">다음 작업을 수행하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-121">Use it to:</span></span>
  
  * <span data-ttu-id="cbfa1-122">API 스키마를 정의하거나 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-122">Define or import API schema.</span></span>
  * <span data-ttu-id="cbfa1-123">제품에 API를 패키징합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-123">Package APIs into products.</span></span>
  * <span data-ttu-id="cbfa1-124">API에서 할당량 또는 변환 등의 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="cbfa1-125">분석의 정보를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="cbfa1-126">사용자를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-126">Manage users.</span></span>
* <span data-ttu-id="cbfa1-127">**개발자 포털** 은 개발자를 위한 기본 웹 서비스 역할을 하며, 여기서 개발자는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="cbfa1-128">API 설명서를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-128">Read API documentation.</span></span>
  * <span data-ttu-id="cbfa1-129">대화형 콘솔을 통해 API를 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="cbfa1-130">계정을 만들고 구독하여 API 키를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="cbfa1-131">자신의 사용량에 대한 분석에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="cbfa1-132"><a name="create-service-instance"> </a>API 관리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="cbfa1-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="cbfa1-133">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="cbfa1-134">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="cbfa1-135">자세한 내용은 [Azure 무료 평가판][Azure Free Trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="cbfa1-136">API 관리 작업의 첫 번째 단계는 서비스 인스턴스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="cbfa1-137">[Azure Portal][Azure Portal]에 로그인하고 **새로 만들기**, **웹 + 모바일**, **API Management**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API 관리 새 인스턴스][api-management-create-instance-menu]

<span data-ttu-id="cbfa1-139">**이름**에서 서비스 URL에 사용할 고유한 하위 도메인 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="cbfa1-140">서비스 인스턴스에 대해 원하는 **구독**, **리소스 그룹** 및 **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="cbfa1-141">입력 **Contoso ltd.**</span><span class="sxs-lookup"><span data-stu-id="cbfa1-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="cbfa1-142">에 대 한는 **조직 이름**에 전자 메일 주소를 입력 하 고는 **관리자 전자 메일** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="cbfa1-143">이 전자 메일 주소는 API 관리 시스템에서 알림을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="cbfa1-144">자세한 내용은 [Azure API Management에서 알림 및 전자 메일 템플릿을 구성하는 방법][How to configure notifications and email templates in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![새 API 관리 서비스][api-management-create-instance-step1]

<span data-ttu-id="cbfa1-146">API 관리 서비스 인스턴스는 Developer, Standard, Premium의 세 가지 계층으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="cbfa1-147">개발자 계층은 고가용성이 문제가 되지 않는 개발, 테스트 및 파일럿 API 프로그램용입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="cbfa1-148">Standard 및 Premium 계층에서는 예약 단위 수를 확장하여 더 많은 트래픽을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="cbfa1-149">Standard 및 Premium 계층은 API 관리 서비스에 가장 많은 처리 능력과 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="cbfa1-150">임의 계층을 사용하여 이 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="cbfa1-151">API Management 계층에 대한 자세한 내용은 [API Management 가격][API Management pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="cbfa1-152">**만들기**를 클릭하여 서비스 인스턴스를 프로비전하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-152">Click **Create** to start provisioning your service instance.</span></span>

![새 API 관리 서비스][api-management-instance-created]

<span data-ttu-id="cbfa1-154">서비스 인스턴스를 만든 후 다음 단계는 API를 만들거나 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="cbfa1-155"><a name="create-api"> </a>API 가져오기</span><span class="sxs-lookup"><span data-stu-id="cbfa1-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="cbfa1-156">API는 클라이언트 응용 프로그램에서 호출할 수 있는 작업 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="cbfa1-157">API 작업은 기존 웹 서비스로 프록시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="cbfa1-158">API를 만들고 작업을 수동으로 추가하거나 API를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="cbfa1-159">이 자습서에서는 Microsoft에서 제공하고 Azure에서 호스트하는 샘플 계산기 웹 서비스에 대한 API를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cbfa1-160">API를 만들고 작업을 수동으로 추가하는 방법에 대해서는 [API를 만드는 방법](api-management-howto-create-apis.md) 및 [API에 작업을 추가하는 방법](api-management-howto-add-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="cbfa1-161">API는 게시자 포털에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="cbfa1-162">여기에 도달하려면 서비스 도구 모음에서 **게시자 포털**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="cbfa1-164">계산기 API를 가져오려면 왼쪽의 **API 관리** 메뉴에서 **API**를 클릭한 다음 **API 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![API 가져오기 단추][api-management-import-api]

<span data-ttu-id="cbfa1-166">다음 단계를 수행하여 계산기 API를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="cbfa1-167">**URL에서**를 클릭하고 **사양 문서 URL** 텍스트 상자에 **http://calcapi.cloudapp.net/calcapi.json**을 입력하고 **Swagger** 라디오 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="cbfa1-168">**웹 API URL 접미사** 텍스트 상자에 **calc**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="cbfa1-169">**제품(선택 사항)** 상자를 클릭하고 **시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="cbfa1-170">**저장** 을 클릭하여 API를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-170">Click **Save** to import the API.</span></span>

![새 API 추가][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="cbfa1-172">**API 관리**는 현재 가져오기에 대한 Swagger 문서의 1.2 및 2.0 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="cbfa1-173">[Swagger 2.0 사양](http://swagger.io/specification)에서 `host`, `basePath` 및 `schemes` 속성이 선택 사항이라고 선언하더라도 Swagger 2.0 문서는 해당 속성을 **반드시** 포함해야 합니다. 그렇지 않으면 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="cbfa1-174">API를 가져오면 API에 대한 요약 페이지가 게시자 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![API 요약][api-management-imported-api-summary]

<span data-ttu-id="cbfa1-176">API 섹션에는 여러 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-176">The API section has several tabs.</span></span> <span data-ttu-id="cbfa1-177">**요약** 탭은 API에 대한 기본 메트릭과 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="cbfa1-178">[설정](api-management-howto-create-apis.md#configure-api-settings) 탭은 API에 대한 구성을 보고 편집하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="cbfa1-179">[작업](api-management-howto-add-operations.md) 탭은 API의 작업을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="cbfa1-180">**보안** 탭은 기본 인증 또는 [상호 인증서 인증](api-management-howto-mutual-certificates.md)을 사용하여 백엔드 서버에 대한 게이트웨이 인증을 구성하고 [OAuth 2.0을 사용하여 사용자 권한 부여](api-management-howto-oauth2.md)를 구성하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="cbfa1-181">**문제** 탭은 API를 사용하는 개발자가 보고한 문제를 보는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="cbfa1-182">**제품** 탭은 이 API를 포함하는 제품을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="cbfa1-183">기본적으로 각 API 관리 인스턴스는 두 개의 샘플 제품과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="cbfa1-184">**Starter**</span><span class="sxs-lookup"><span data-stu-id="cbfa1-184">**Starter**</span></span>
* <span data-ttu-id="cbfa1-185">**무제한**</span><span class="sxs-lookup"><span data-stu-id="cbfa1-185">**Unlimited**</span></span>

<span data-ttu-id="cbfa1-186">이 자습서에서는 기본 계산기 API를 가져온 경우 해당 API를 Starter 제품에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="cbfa1-187">API를 호출하려면 개발자는 먼저 제품에 대한 액세스 권한을 주는 제품을 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="cbfa1-188">개발자가 개발자 포털에서 제품을 구독할 수 있습니다. 또는 관리자가 게시자 포털에서 개발자가 제품에 구독하도록 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="cbfa1-189">이 자습서의 이전 단계에서 API 관리 인스턴스를 만들었기 때문에 현재 관리자이므로 기본적으로 모든 제품에 구독되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="cbfa1-190"><a name="call-operation"> </a>개발자 포털에서 작업 호출</span><span class="sxs-lookup"><span data-stu-id="cbfa1-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="cbfa1-191">개발자 포털에서 직접 작업을 호출할 수 있으며, 이 포털을 사용하면 편리한 방법으로 API의 작업을 보고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="cbfa1-192">이 자습서에서는 기본 계산기 API의 **두 정수 추가** 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="cbfa1-193">게시자 포털의 오른쪽 위에 있는 메뉴에서 **개발자 포털** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="cbfa1-195">맨 위 메뉴에서 **API**를 클릭하고 **기본 계산기**를 클릭하여 사용할 수 있는 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![개발자 포털][api-management-developer-portal-calc-api]

<span data-ttu-id="cbfa1-197">API 및 작업과 함께 가져온 매개 변수와 샘플 설명을 참고하세요. 이는 본 작업을 사용하는 개발자에게 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="cbfa1-198">작업을 수동으로 추가하는 경우 이러한 설명을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="cbfa1-199">**두 정수 추가** 작업을 호출하려면 **시도**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![시도][api-management-developer-portal-calc-api-console]

<span data-ttu-id="cbfa1-201">매개 변수에 대한 값을 입력하거나 기본값을 유지한 다음 **보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="cbfa1-203">작업 호출 후에는 개발자 포털에 **응답 상태**, **응답 헤더**, **응답 콘텐츠**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![응답][api-management-invoke-get-response]

## <span data-ttu-id="cbfa1-205"><a name="view-analytics"> </a>분석 보기</span><span class="sxs-lookup"><span data-stu-id="cbfa1-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="cbfa1-206">기본 계산기에 대한 분석을 보려면 개발자 포털의 오른쪽 위에 있는 메뉴에서 **관리** 를 선택하여 게시자 포털로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![관리][api-management-manage-menu]

<span data-ttu-id="cbfa1-208">게시자 포털의 기본 보기는 **대시보드**이며 여기서 API 관리 인스턴스의 개요를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![대시보드][api-management-dashboard]

<span data-ttu-id="cbfa1-210">**기본 계산기** 차트 위로 마우스를 가져가서 주어진 기간의 API 사용 관련 특정 메트릭을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="cbfa1-211">차트에 아무런 줄도 표시되지 않는 경우 개발자 포털로 다시 전환하여 API를 호출한 후 몇 분 정도 기다렸다가 대시보드로 다시 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="cbfa1-212">**자세히 보기**를 클릭하여 API에 대한 요약 페이지를 표시합니다. 여기에는 더 크게 표시되는 메트릭 버전도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![분석][api-management-mouse-over]

![요약][api-management-api-summary-metrics]

<span data-ttu-id="cbfa1-215">자세한 메트릭과 보고서를 보려면 왼쪽의 **API 관리** 메뉴에서 **분석**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![개요][api-management-analytics-overview]

<span data-ttu-id="cbfa1-217">**분석** 섹션에는 다음과 같은 네 개의 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="cbfa1-218">**개요** 에서는 전체적인 사용 및 상태 메트릭뿐만 아니라 상위 개발자, 상위 제품, 상위 API 및 상위 작업도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="cbfa1-219">**사용량** 에서는 지리적 표현을 포함하여 API 호출 및 대역폭을 심도 있게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="cbfa1-220">**상태** 에서는 상태 코드, 캐시 성공률, 응답 시간, API 및 서비스 응답 시간을 위주로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="cbfa1-221">**활동** 에서는 개발자의 특정 작업, 제품, API 및 작업에 대한 자세한 내용을 보여 주는 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="cbfa1-222"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="cbfa1-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="cbfa1-223">[비율 제한으로 API를 보호](api-management-howto-product-with-rules.md)하는 방법 알아보기.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
