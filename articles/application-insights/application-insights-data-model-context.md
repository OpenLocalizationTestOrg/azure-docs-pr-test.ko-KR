---
title: "aaaAzure Insights 원격 분석 데이터 모델 응용 프로그램 원격 분석 컨텍스트 | Microsoft Docs"
description: "Application Insights 원격 분석 컨텍스트 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="e71ca-103">원격 분석 컨텍스트: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="e71ca-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="e71ca-104">모든 원격 분석 항목에는 강력한 형식의 컨텍스트 필드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="e71ca-105">모든 필드는 특정 모니터링 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="e71ca-106">Hello 사용자 지정 속성 컬렉션 toostore 사용자 지정 또는 응용 프로그램 관련 컨텍스트 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="e71ca-107">응용 프로그램 버전</span><span class="sxs-lookup"><span data-stu-id="e71ca-107">Application version</span></span>

<span data-ttu-id="e71ca-108">Hello 응용 프로그램 컨텍스트 필드의 정보는 항상 hello 원격 분석을 전송 하는 hello 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="e71ca-109">응용 프로그램 버전은 hello 응용 프로그램 동작 및 해당 상관 관계 toohello 배포에 사용 되는 tooanalyze 추세 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="e71ca-110">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="e71ca-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="e71ca-111">클라이언트 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e71ca-111">Client IP address</span></span>

<span data-ttu-id="e71ca-112">hello hello 클라이언트 장치의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-112">hello IP address of hello client device.</span></span> <span data-ttu-id="e71ca-113">IPv4 및 IPv6이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="e71ca-114">서비스에서 원격 분석을 보내면 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한 hello 위치 컨텍스트는입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="e71ca-115">Application Insights는 hello 클라이언트 IP에서 hello 지리적 위치 정보를 추출 하를 잘라 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="e71ca-116">따라서 클라이언트 IP 자체는 최종 사용자가 식별할 수 있는 정보로 사용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="e71ca-117">최대 길이: 46</span><span class="sxs-lookup"><span data-stu-id="e71ca-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="e71ca-118">장치 유형</span><span class="sxs-lookup"><span data-stu-id="e71ca-118">Device type</span></span>

<span data-ttu-id="e71ca-119">이 필드는 사용 된 원래 사용 하는 hello 응용 프로그램의 hello 장치 hello 최종 사용자의 tooindicate hello 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="e71ca-120">오늘날 주로 toodistinguish JavaScript 원격 분석 형식과 함께 사용 hello 장치 '브라우저'에서 서버 쪽 원격 분석 hello 장치 유형 'p C'으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="e71ca-121">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="e71ca-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="e71ca-122">작업 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-122">Operation id</span></span>

<span data-ttu-id="e71ca-123">Hello 루트 작업의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="e71ca-124">이 식별자는 여러 구성 요소에서 toogroup 원격 분석을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="e71ca-125">자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e71ca-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="e71ca-126">hello 작업 id는 요청 또는 페이지 보기에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="e71ca-127">다른 모든 원격 분석 요청이 나 페이지 뷰를 포함 하는 hello에 대 한이 필드 toohello 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="e71ca-128">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="e71ca-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="e71ca-129">부모 작업 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-129">Parent operation ID</span></span>

<span data-ttu-id="e71ca-130">안녕 hello 원격 분석 항목의 직계 부모의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="e71ca-131">자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e71ca-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="e71ca-132">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="e71ca-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="e71ca-133">작업 이름</span><span class="sxs-lookup"><span data-stu-id="e71ca-133">Operation name</span></span>

<span data-ttu-id="e71ca-134">hello 연산의 hello 이름 (그룹)입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="e71ca-135">요청 또는 페이지 보기 하 여 hello 작업 이름이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="e71ca-136">다른 모든 원격 분석 항목 요청 또는 페이지 뷰를 포함 하는 hello에 대 한이 필드 toohello 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="e71ca-137">작업 이름이 작업 (예를 들어 ' GET Home/Index ')의 그룹에 대 한 모든 hello 원격 분석 항목을 찾는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="e71ca-138">이 컨텍스트 속성은 사용 되는 tooanswer 같은 질문을 "hello이이 페이지에서 throw 되는 일반적인 예외 무엇 인가요."</span><span class="sxs-lookup"><span data-stu-id="e71ca-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="e71ca-139">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="e71ca-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="e71ca-140">Hello 작업의 합성 소스</span><span class="sxs-lookup"><span data-stu-id="e71ca-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="e71ca-141">가상 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-141">Name of synthetic source.</span></span> <span data-ttu-id="e71ca-142">Hello 응용 프로그램에서 일부 원격 분석 가상 트래픽을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="e71ca-143">웹 크롤러 인덱싱 hello 웹 사이트, 사이트 가용성 테스트 또는 자체 Application Insights SDK과 같은 진단 라이브러리에서 추적 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="e71ca-144">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="e71ca-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="e71ca-145">세션 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-145">Session id</span></span>

<span data-ttu-id="e71ca-146">세션 ID-hello 인스턴스의 hello 사용자의 상호 hello 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="e71ca-147">Hello 세션 컨텍스트 필드의 정보는 항상 hello 최종 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="e71ca-148">서비스에서 원격 분석을 보내면 hello 세션 컨텍스트가 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="e71ca-149">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="e71ca-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="e71ca-150">익명 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-150">Anonymous user id</span></span>

<span data-ttu-id="e71ca-151">익명 사용자 ID입니다. Hello 응용 프로그램의 hello 최종 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="e71ca-152">서비스에서 원격 분석을 보내면 hello 사용자 컨텍스트가 hello 작업 hello 서비스에서 시작한 hello 사용자에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="e71ca-153">[샘플링](app-insights-sampling.md) hello 기술 toominimize hello 양의 원격 분석 수집된 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="e71ca-154">알고리즘 시도 tooeither 샘플링 샘플 또는 모든 hello 축소 상관 관계가 지정 된 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="e71ca-155">익명 사용자 ID는 샘플링 점수 생성에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="e71ca-156">따라서 익명 사용자 ID는 충분히 임의의 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="e71ca-157">익명 사용자 id toostore 사용자 이름을 사용 하는 hello 필드의 오용입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="e71ca-158">인증된 사용자 ID를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e71ca-158">Use Authenticated user id.</span></span>

<span data-ttu-id="e71ca-159">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="e71ca-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="e71ca-160">인증된 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-160">Authenticated user id</span></span>

<span data-ttu-id="e71ca-161">인증 된 사용자 id입니다. 익명 사용자 id,이 필드의 반대 hello 라는 이름으로 hello 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="e71ca-162">PII 정보이므로 기본적으로 대부분의 SDK에서 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="e71ca-163">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="e71ca-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="e71ca-164">계정 ID</span><span class="sxs-lookup"><span data-stu-id="e71ca-164">Account id</span></span>

<span data-ttu-id="e71ca-165">다중 테 넌 트 응용 프로그램에서 hello 계정 ID 또는 hello 사용자와 작동 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="e71ca-166">예를 들어 Azure Portal의 구독 ID 또는 플랫폼을 블로깅하는 블로그 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="e71ca-167">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="e71ca-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="e71ca-168">클라우드 역할</span><span class="sxs-lookup"><span data-stu-id="e71ca-168">Cloud role</span></span>

<span data-ttu-id="e71ca-169">일부인 hello 역할 hello 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="e71ca-170">Azure에서 역할 이름을 toohello를 직접 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="e71ca-171">사용 되는 toodistinguish 단일 응용 프로그램의 구성 요소인 마이크로 서비스 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="e71ca-172">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="e71ca-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="e71ca-173">클라우드 역할 인스턴스</span><span class="sxs-lookup"><span data-stu-id="e71ca-173">Cloud role instance</span></span>

<span data-ttu-id="e71ca-174">Hello 응용 프로그램이 실행 중인 hello 인스턴스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="e71ca-175">온-프레미스의 경우 컴퓨터 이름, Azure의 경우 인스턴스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="e71ca-176">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="e71ca-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="e71ca-177">내부: SDK 버전</span><span class="sxs-lookup"><span data-stu-id="e71ca-177">Internal: SDK version</span></span>

<span data-ttu-id="e71ca-178">SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-178">SDK version.</span></span> <span data-ttu-id="e71ca-179">자세한 내용은 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e71ca-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="e71ca-180">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="e71ca-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="e71ca-181">내부: 노드 이름</span><span class="sxs-lookup"><span data-stu-id="e71ca-181">Internal: Node name</span></span>

<span data-ttu-id="e71ca-182">이 필드는 요금 청구를 위해 사용 되는 hello 노드 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="e71ca-183">노드 toooverride hello 표준 검색 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="e71ca-184">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="e71ca-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="e71ca-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e71ca-185">Next steps</span></span>

- <span data-ttu-id="e71ca-186">너무 방법에 대해 알아봅니다[확장 하 고 원격 분석 필터링](app-insights-api-filtering-sampling.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="e71ca-187">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e71ca-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="e71ca-188">표준 컨텍스트 속성 컬렉션 [구성](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e71ca-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
