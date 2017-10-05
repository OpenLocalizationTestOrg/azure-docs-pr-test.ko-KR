---
title: "사용자 지정 정책의 문제를 해결하기 위한 Application Insights - Azure AD B2C | Microsoft Docs"
description: "Application Insights를 설정하여 사용자 지정 정책의 실행을 추적하는 방법"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="e864c-103">Azure Active Directory B2C: 로그 수집</span><span class="sxs-lookup"><span data-stu-id="e864c-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="e864c-104">이 문서에서는 사용자 지정 정책을 사용하여 문제를 진단할 수 있도록 Azure AD B2C에서 로그를 수집하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="e864c-105">현재 여기에 설명된 자세한 활동 로그는 **오직** 사용자 지정 정책 개발에 도움이 되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="e864c-106">프로덕션에서 개발 모드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="e864c-107">로그는 개발 중에 ID 공급자 간에 전송된 모든 클레임을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="e864c-108">프로덕션에서 사용하는 경우 개발자는 소유한 App Insights 로그에서 수집된 PII(개인적으로 식별 가능한 정보)에 대한 책임이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="e864c-109">이러한 자세한 로그는 정책이 **개발 모드**인 경우에만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="e864c-110">Application Insights 사용</span><span class="sxs-lookup"><span data-stu-id="e864c-110">Use Application Insights</span></span>

<span data-ttu-id="e864c-111">Azure AD B2C는 Application Insights로 데이터를 보내는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="e864c-112">Application Insights는 예외를 진단하고 응용 프로그램 성능 문제를 시각화하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="e864c-113">Application Insights 설정</span><span class="sxs-lookup"><span data-stu-id="e864c-113">Setup Application Insights</span></span>

1. <span data-ttu-id="e864c-114">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e864c-115">Azure 구독(Azure AD B2C 테넌트가 아님)을 사용하여 테넌트에 위치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="e864c-116">왼쪽 탐색 메뉴에서 **+ 새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="e864c-117">**Application Insights**를 검색하고 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="e864c-118">양식을 완료하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="e864c-119">**응용 프로그램 형식**에서 **일반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="e864c-120">리소스를 만들게 되면 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="e864c-121">왼쪽 메뉴에서 **속성**을 찾고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="e864c-122">**계측 키**를 복사하고 다음 섹션에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="e864c-123">사용자 지정 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e864c-123">Set up the custom policy</span></span>

1. <span data-ttu-id="e864c-124">RP 파일(예: SignUpOrSignin.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="e864c-125">다음 속성을 `<TrustFrameworkPolicy>` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="e864c-126">이미 존재하지 않는 경우 자식 노드 `<UserJourneyBehaviors>`을 `<RelyingParty>` 노드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="e864c-127">`<DefaultUserJourney ReferenceId="YourPolicyName" />`의 바로 다음에 위치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="e864c-128">다음 노드를 `<UserJourneyBehaviors>` 요소의 자식으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="e864c-129">`{Your Application Insights Key}`를 이전 섹션의 Application Insights에서 가져온 **계측 키**로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="e864c-130">`DeveloperMode="true"`은 ApplicationInsights가 프로세스 파이프라인을 통해 원격 분석 데이터를 신속하게 처리하도록 지시하여 개발에는 적합하지만 높은 볼륨에서 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="e864c-131">`ClientEnabled="true"`은 페이지 보기 및 클라이언트 쪽 오류(필요 없음)을 추적하는 ApplicationInsights 클라이언트 쪽 스크립트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="e864c-132">`ServerEnabled="true"`는 Application Insights에 기존 UserJourneyRecorder JSON을 사용자 지정 이벤트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="e864c-133">샘플:</span><span class="sxs-lookup"><span data-stu-id="e864c-133">Sample:</span></span>

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

3. <span data-ttu-id="e864c-134">정책을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="e864c-135">Application Insights에서 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e864c-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="e864c-136">Application Insights에서 새 로그가 표시되기까지 짧은 지연 시간이 발생합니다(5분 미만).</span><span class="sxs-lookup"><span data-stu-id="e864c-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="e864c-137">[Azure Portal](https://portal.azure.com)에서 만든 Application Insights 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="e864c-138">**개요** 메뉴에서 **분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="e864c-139">Application Insights에서 새 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="e864c-140">로그를 참조하는 데 사용할 수는 쿼리 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="e864c-141">쿼리</span><span class="sxs-lookup"><span data-stu-id="e864c-141">Query</span></span> | <span data-ttu-id="e864c-142">설명</span><span class="sxs-lookup"><span data-stu-id="e864c-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="e864c-143">traces</span><span class="sxs-lookup"><span data-stu-id="e864c-143">traces</span></span> | <span data-ttu-id="e864c-144">Azure AD B2C에서 생성된 모든 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e864c-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="e864c-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="e864c-145">traces \\</span></span>| <span data-ttu-id="e864c-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="e864c-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="e864c-147">마지막 날에 Azure AD B2C에서 생성된 모든 로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e864c-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="e864c-148">항목이 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-148">The entries may be long.</span></span>  <span data-ttu-id="e864c-149">자세히 보기 위해 CSV로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="e864c-150">분석 도구에 대한 자세한 내용은 [여기](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)에서 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="e864c-151">커뮤니티는 ID 개발자에게 도움을 주는 사용자 경험 뷰어를 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="e864c-152">Microsoft에서 지원되지 않고 엄격하게 그대로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="e864c-153">Application Insights 인스턴스에서 읽고 사용자 경험 이벤트의 올바른 구조 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="e864c-154">소스 코드를 가져오고 고유한 솔루션에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="e864c-155">현재 여기에 설명된 자세한 활동 로그는 **오직** 사용자 지정 정책 개발에 도움이 되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="e864c-156">프로덕션에서 개발 모드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-156">Do not use development mode in production.</span></span>  <span data-ttu-id="e864c-157">로그는 개발 중에 ID 공급자 간에 전송된 모든 클레임을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="e864c-158">프로덕션에서 사용하는 경우 개발자는 소유한 App Insights 로그에서 수집된 PII(개인적으로 식별 가능한 정보)에 대한 책임이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="e864c-159">이러한 자세한 로그는 정책이 **개발 모드**인 경우에만 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="e864c-160">지원되지 않는 사용자 지정 정책 샘플 및 관련된 도구에 대한 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="e864c-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="e864c-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e864c-161">Next Steps</span></span>

<span data-ttu-id="e864c-162">Application Insights에서 데이터를 탐색하여 고유한 ID 환경을 제공하기 위해 ID 경험 프레임워크 기본 B2C가 작동하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e864c-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
