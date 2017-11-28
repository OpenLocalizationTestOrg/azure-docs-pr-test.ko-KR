---
title: "응용 프로그램 통찰력 tootroubleshoot 사용자 지정 정책-Azure AD B2C | Microsoft Docs"
description: "어떻게 toosetup Application Insights tootrace hello 사용자 지정 정책 실행"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="29cb0-103">Azure Active Directory B2C: 로그 수집</span><span class="sxs-lookup"><span data-stu-id="29cb0-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="29cb0-104">이 문서에서는 사용자 지정 정책을 사용하여 문제를 진단할 수 있도록 Azure AD B2C에서 로그를 수집하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="29cb0-105">현재 hello 여기에 설명 된 자세한 활동 로그 만들어진 **전용** tooaid 사용자 지정 정책 개발에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="29cb0-106">프로덕션에서 개발 모드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="29cb0-107">로그를 개발 하는 동안 tooand hello id 공급자에서 보내는 클레임을 모두 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="29cb0-108">프로덕션 환경에서 사용 하는 경우 hello 개발자는 각자 소유한 hello App Insights 로그에서 수집 된 PII (개인적으로 식별이 가능한 정보)에 대 한 책임을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="29cb0-109">Hello 정책에 배치 되 면 이러한 자세한 로그만 수집 됩니다 **개발 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="29cb0-110">Application Insights 사용</span><span class="sxs-lookup"><span data-stu-id="29cb0-110">Use Application Insights</span></span>

<span data-ttu-id="29cb0-111">Azure AD B2C 데이터 tooApplication Insights 보내기 위한 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="29cb0-112">Application Insights 방법을 toodiagnose 예외를 제공 하 고 응용 프로그램 성능 문제를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="29cb0-113">Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="29cb0-113">Setup Application Insights</span></span>

1. <span data-ttu-id="29cb0-114">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="29cb0-115">사용자가 hello 테 넌 트의 Azure 구독 (하지 Azure AD B2C 테 넌 트)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="29cb0-116">클릭 **+ 새로 만들기** hello 왼쪽 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="29cb0-117">**Application Insights**를 검색하고 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="29cb0-118">Hello 양식을 작성 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="29cb0-119">선택 **일반** hello에 대 한 **응용 프로그램 종류**합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="29cb0-120">Hello 리소스를 만든 후에 hello Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="29cb0-121">찾을 **속성** hello 왼쪽 메뉴에서 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="29cb0-122">복사 hello **계측 키** hello 다음 섹션에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="29cb0-123">Hello 사용자 지정 정책 설정</span><span class="sxs-lookup"><span data-stu-id="29cb0-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="29cb0-124">Hello RP 파일 (예를 들어 SignUpOrSignin.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="29cb0-125">다음 특성 toohello hello 추가 `<TrustFrameworkPolicy>` 요소:</span><span class="sxs-lookup"><span data-stu-id="29cb0-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="29cb0-126">이미 존재 하지 않으면 자식 노드를 추가 `<UserJourneyBehaviors>` toohello `<RelyingParty>` 노드.</span><span class="sxs-lookup"><span data-stu-id="29cb0-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="29cb0-127">Hello 직후 위치 여야 합니다.`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="29cb0-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="29cb0-128">Hello 노드 다음에 오는 hello의 자식으로 추가 `<UserJourneyBehaviors>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="29cb0-129">있는지 tooreplace 확인 `{Your Application Insights Key}` hello로 **계측 키** hello 이전 섹션에서 Application Insights에서 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="29cb0-130">`DeveloperMode="true"`양호 하지만 높은 볼륨에서 제한 된 개발에 대 한 hello 처리 파이프라인을 통해 ApplicationInsights tooexpedite hello 원격 분석을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="29cb0-131">`ClientEnabled="true"`페이지 보기 및 클라이언트 쪽 오류 (필요 없음)을 추적 하기 위한 hello ApplicationInsights 클라이언트 쪽 스크립트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="29cb0-132">`ServerEnabled="true"`사용자 지정 이벤트 tooApplication 통찰력으로 기존 UserJourneyRecorder JSON hello 하는 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="29cb0-133">샘플:</span><span class="sxs-lookup"><span data-stu-id="29cb0-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="29cb0-134">Hello 정책을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="29cb0-135">Hello Application Insights에서 로그를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="29cb0-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="29cb0-136">Application Insights에서 새 로그가 표시되기까지 짧은 지연 시간이 발생합니다(5분 미만).</span><span class="sxs-lookup"><span data-stu-id="29cb0-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="29cb0-137">Hello에서 만든 hello Application Insights 리소스를 열고 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="29cb0-138">Hello에 **개요** 메뉴를 클릭 **분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="29cb0-139">Application Insights에서 새 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="29cb0-140">다음은 toosee hello 로그를 사용할 수 있습니다 쿼리 목록</span><span class="sxs-lookup"><span data-stu-id="29cb0-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="29cb0-141">쿼리</span><span class="sxs-lookup"><span data-stu-id="29cb0-141">Query</span></span> | <span data-ttu-id="29cb0-142">설명</span><span class="sxs-lookup"><span data-stu-id="29cb0-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="29cb0-143">traces</span><span class="sxs-lookup"><span data-stu-id="29cb0-143">traces</span></span> | <span data-ttu-id="29cb0-144">모든 Azure AD B2C에 의해 생성 된 hello 로그 참조</span><span class="sxs-lookup"><span data-stu-id="29cb0-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="29cb0-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="29cb0-145">traces \\</span></span>| <span data-ttu-id="29cb0-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="29cb0-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="29cb0-147">참조 하는 모든 hello 로그에서 생성 된 Azure AD B2C hello에 대 한 마지막 날</span><span class="sxs-lookup"><span data-stu-id="29cb0-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="29cb0-148">hello 항목 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-148">hello entries may be long.</span></span>  <span data-ttu-id="29cb0-149">자세히 보기에 대 한 tooCSV 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="29cb0-150">Hello 분석 도구에 대 한 자세히 알아볼 수 있습니다 [여기](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="29cb0-151">hello 커뮤니티에는 사용자의 여행 뷰어 toohelp identity 개발자가 개발 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="29cb0-152">Microsoft에서 지원되지 않고 엄격하게 그대로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="29cb0-153">Application Insights 인스턴스에서 읽고 hello 사용자 여행 이벤트의 올바른 구조 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="29cb0-154">Hello 소스 코드를 받으며 사용자 고유의 솔루션에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="29cb0-155">현재 hello 여기에 설명 된 자세한 활동 로그 만들어진 **전용** tooaid 사용자 지정 정책 개발에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="29cb0-156">프로덕션에서 개발 모드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-156">Do not use development mode in production.</span></span>  <span data-ttu-id="29cb0-157">로그를 개발 하는 동안 tooand hello id 공급자에서 보내는 클레임을 모두 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="29cb0-158">프로덕션 환경에서 사용 하는 경우 hello 개발자는 각자 소유한 hello App Insights 로그에서 수집 된 PII (개인적으로 식별이 가능한 정보)에 대 한 책임을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="29cb0-159">Hello 정책에 배치 되 면 이러한 자세한 로그만 수집 됩니다 **개발 모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="29cb0-160">지원되지 않는 사용자 지정 정책 샘플 및 관련된 도구에 대한 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="29cb0-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="29cb0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29cb0-161">Next Steps</span></span>

<span data-ttu-id="29cb0-162">Hello 데이터를 이해 하는 Application Insights toohelp 탐색 방법을 toodeliver 고유한 identity 환경을 작동 하는 기본 B2C Id 경험 프레임 워크를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="29cb0-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
