---
title: "Azure Application Insights 원격 분석 데이터 모델 - 원격 분석 컨텍스트 | Microsoft Docs"
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
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="593bc-103">원격 분석 컨텍스트: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="593bc-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="593bc-104">모든 원격 분석 항목에는 강력한 형식의 컨텍스트 필드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="593bc-105">모든 필드는 특정 모니터링 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="593bc-106">사용자 지정 속성 컬렉션을 사용하여 사용자 지정 또는 응용 프로그램별 컨텍스트 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="593bc-107">응용 프로그램 버전</span><span class="sxs-lookup"><span data-stu-id="593bc-107">Application version</span></span>

<span data-ttu-id="593bc-108">응용 프로그램 컨텍스트 필드의 정보는 항상 원격 분석을 전송하는 응용 프로그램과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="593bc-109">응용 프로그램 버전은 응용 프로그램 동작 및 배포 상관 관계의 추세 변경을 분석하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="593bc-110">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="593bc-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="593bc-111">클라이언트 IP 주소</span><span class="sxs-lookup"><span data-stu-id="593bc-111">Client IP address</span></span>

<span data-ttu-id="593bc-112">클라이언트 장치의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-112">The IP address of the client device.</span></span> <span data-ttu-id="593bc-113">IPv4 및 IPv6이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="593bc-114">원격 분석이 서비스에서 전송되는 경우 위치 컨텍스트는 서비스에서 작업을 시작한 사용자와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="593bc-115">Application Insights는 클라이언트 IP에서 지리적 위치 정보를 추출한 다음 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="593bc-116">따라서 클라이언트 IP 자체는 최종 사용자가 식별할 수 있는 정보로 사용될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="593bc-117">최대 길이: 46</span><span class="sxs-lookup"><span data-stu-id="593bc-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="593bc-118">장치 유형</span><span class="sxs-lookup"><span data-stu-id="593bc-118">Device type</span></span>

<span data-ttu-id="593bc-119">원래 이 필드는 응용 프로그램의 최종 사용자가 사용하는 장치의 유형을 나타내는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="593bc-120">현재는 장치 유형이 'Browser'인 JavaScript 원격 분석을 장치 유형이 'PC'인 서버 쪽 원격 분석과 구별하는 데 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="593bc-121">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="593bc-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="593bc-122">작업 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-122">Operation id</span></span>

<span data-ttu-id="593bc-123">루트 작업의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="593bc-124">이 식별자를 사용하여 여러 구성 요소에서 원격 분석을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="593bc-125">자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="593bc-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="593bc-126">작업 ID는 요청 또는 페이지 보기에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="593bc-127">다른 모든 원격 분석은 이 필드를 포함 요청 또는 페이지 보기의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="593bc-128">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="593bc-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="593bc-129">부모 작업 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-129">Parent operation ID</span></span>

<span data-ttu-id="593bc-130">원격 분석 항목의 직계 부모의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="593bc-131">자세한 내용은 [원격 분석 상관 관계](application-insights-correlation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="593bc-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="593bc-132">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="593bc-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="593bc-133">작업 이름</span><span class="sxs-lookup"><span data-stu-id="593bc-133">Operation name</span></span>

<span data-ttu-id="593bc-134">작업의 이름(그룹)입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-134">The name (group) of the operation.</span></span> <span data-ttu-id="593bc-135">작업 이름은 요청 또는 페이지 보기에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="593bc-136">다른 모든 원격 분석 항목은 이 필드를 포함 요청 또는 페이지 보기의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="593bc-137">작업 이름은 작업 그룹(예를 들어 'GET Home/Index')에 대한 모든 원격 분석 항목을 찾는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="593bc-138">이 컨텍스트 속성은 "이 페이지에서 발생하는 일반적인 예외"와 같은 질문에 답변하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="593bc-139">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="593bc-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="593bc-140">작업의 가상 원본</span><span class="sxs-lookup"><span data-stu-id="593bc-140">Synthetic source of the operation</span></span>

<span data-ttu-id="593bc-141">가상 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-141">Name of synthetic source.</span></span> <span data-ttu-id="593bc-142">응용 프로그램의 일부 원격 분석은 가상 트래픽을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="593bc-143">이는 Application Insights SDK 자체와 같은 진단 라이브러리에서 웹 사이트, 사이트 가용성 테스트 또는 추적을 인덱싱하는 웹 크롤러일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="593bc-144">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="593bc-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="593bc-145">세션 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-145">Session id</span></span>

<span data-ttu-id="593bc-146">세션 ID - 응용 프로그램과의 사용자 상호 작용 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="593bc-147">세션 컨텍스트 필드의 정보는 항상 최종 사용자와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="593bc-148">원격 분석이 서비스에서 전송되는 경우 서비스 컨텍스트는 서비스에서 작업을 시작한 사용자와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="593bc-149">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="593bc-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="593bc-150">익명 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-150">Anonymous user id</span></span>

<span data-ttu-id="593bc-151">익명 사용자 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-151">Anonymous user id.</span></span> <span data-ttu-id="593bc-152">응용 프로그램의 최종 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-152">Represents the end user of the application.</span></span> <span data-ttu-id="593bc-153">원격 분석이 서비스에서 전송되는 경우 사용자 컨텍스트는 서비스에서 작업을 시작한 사용자와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="593bc-154">[샘플링](app-insights-sampling.md)은 수집된 원격 분석의 양을 최소화하는 기술 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="593bc-155">샘플링 알고리즘은 상관 관계가 지정된 모든 원격 분석을 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="593bc-156">익명 사용자 ID는 샘플링 점수 생성에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="593bc-157">따라서 익명 사용자 ID는 충분히 임의의 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="593bc-158">익명 사용자 ID를 사용하여 사용자 이름을 저장하는 것은 이 필드의 오용입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="593bc-159">인증된 사용자 ID를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="593bc-159">Use Authenticated user id.</span></span>

<span data-ttu-id="593bc-160">최대 길이: 128</span><span class="sxs-lookup"><span data-stu-id="593bc-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="593bc-161">인증된 사용자 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-161">Authenticated user id</span></span>

<span data-ttu-id="593bc-162">인증된 사용자 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-162">Authenticated user id.</span></span> <span data-ttu-id="593bc-163">익명 사용자 ID와 반대되는 이 필드는 표시 이름으로 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="593bc-164">PII 정보이므로 기본적으로 대부분의 SDK에서 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="593bc-165">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="593bc-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="593bc-166">계정 ID</span><span class="sxs-lookup"><span data-stu-id="593bc-166">Account id</span></span>

<span data-ttu-id="593bc-167">다중 테넌트 응용 프로그램에서 이는 사용자가 작업하는 데 사용하는 계정 ID 또는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="593bc-168">예를 들어 Azure Portal의 구독 ID 또는 플랫폼을 블로깅하는 블로그 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="593bc-169">최대 길이: 1024</span><span class="sxs-lookup"><span data-stu-id="593bc-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="593bc-170">클라우드 역할</span><span class="sxs-lookup"><span data-stu-id="593bc-170">Cloud role</span></span>

<span data-ttu-id="593bc-171">응용 프로그램이 속해 있는 역할의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="593bc-172">Azure에서 역할 이름에 직접 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="593bc-173">단일 응용 프로그램의 일부인 마이크로 서비스를 구별하는 데 사용될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="593bc-174">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="593bc-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="593bc-175">클라우드 역할 인스턴스</span><span class="sxs-lookup"><span data-stu-id="593bc-175">Cloud role instance</span></span>

<span data-ttu-id="593bc-176">응용 프로그램이 실행되고 있는 인스턴스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="593bc-177">온-프레미스의 경우 컴퓨터 이름, Azure의 경우 인스턴스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="593bc-178">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="593bc-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="593bc-179">내부: SDK 버전</span><span class="sxs-lookup"><span data-stu-id="593bc-179">Internal: SDK version</span></span>

<span data-ttu-id="593bc-180">SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-180">SDK version.</span></span> <span data-ttu-id="593bc-181">자세한 내용은 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="593bc-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="593bc-182">최대 길이: 64</span><span class="sxs-lookup"><span data-stu-id="593bc-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="593bc-183">내부: 노드 이름</span><span class="sxs-lookup"><span data-stu-id="593bc-183">Internal: Node name</span></span>

<span data-ttu-id="593bc-184">이 필드는 요금 청구에 사용되는 노드 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="593bc-185">이를 사용하여 노드의 표준 검색을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="593bc-186">최대 길이: 256</span><span class="sxs-lookup"><span data-stu-id="593bc-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="593bc-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="593bc-187">Next steps</span></span>

- <span data-ttu-id="593bc-188">[원격 분석을 확장 및 필터링](app-insights-api-filtering-sampling.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="593bc-189">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="593bc-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="593bc-190">표준 컨텍스트 속성 컬렉션 [구성](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="593bc-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
