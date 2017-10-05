---
title: "Azure CDN 실시간 경고 | Microsoft Docs"
description: "Microsoft Azure CDN의 실시간 경고입니다. 실시간 경고는 CDN 프로필에서 끝점의 성능에 대한 알림을 제공합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6e66eb076ac7220823a848b5047f147d4101cd55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="9b618-104">Microsoft Azure CDN의 실시간 경고</span><span class="sxs-lookup"><span data-stu-id="9b618-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="9b618-105">개요</span><span class="sxs-lookup"><span data-stu-id="9b618-105">Overview</span></span>
<span data-ttu-id="9b618-106">이 문서에서는 Microsoft Azure CDN의 실시간 경고에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="9b618-107">이 기능은 CDN 프로필에서 끝점의 성능에 대한 실시간 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-107">This functionality provides real-time notifications about the performance of the endpoints in your CDN profile.</span></span>  <span data-ttu-id="9b618-108">다음을 기반으로 전자 메일 또는 HTTP 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="9b618-109">대역폭</span><span class="sxs-lookup"><span data-stu-id="9b618-109">Bandwidth</span></span>
* <span data-ttu-id="9b618-110">상태 코드</span><span class="sxs-lookup"><span data-stu-id="9b618-110">Status Codes</span></span>
* <span data-ttu-id="9b618-111">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="9b618-111">Cache Statuses</span></span>
* <span data-ttu-id="9b618-112">연결</span><span class="sxs-lookup"><span data-stu-id="9b618-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="9b618-113">실시간 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="9b618-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="9b618-114">[Azure 포털](https://portal.azure.com)에서 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="9b618-116">CDN 프로필 블레이드에서 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="9b618-118">CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="9b618-119">**분석** 탭을 마우스로 가리킨 후 **실시간 통계** 플라이아웃을 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="9b618-120">**실시간 경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN 관리 포털](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="9b618-122">기존 경고 구성(있는 경우)의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-122">The list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="9b618-123">**경고 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-123">Click the **Add Alert** button.</span></span>
   
    ![경고 추가 단추](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="9b618-125">새 경고를 만드는 양식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-125">A form for creating a new alert is displayed.</span></span>
   
    ![새 경고 양식](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="9b618-127">**저장**을 클릭할 때 이 경고를 활성화하려면 **경고 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-127">If you want this alert to be active when you click **Save**, check the **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="9b618-128">**이름** 필드에 경고에 대한 설명이 포함된 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-128">Enter a descriptive name for your alert in the **Name** field.</span></span>
7. <span data-ttu-id="9b618-129">**미디어 유형** 드롭다운에서 **HTTP LOB(Large Object)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-129">In the **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![HTTP LOB(Large Object)를 선택한 미디어 유형](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="9b618-131">**HTTP LOB(Large Object)**를 **미디어 형식**으로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-131">You must select **HTTP Large Object** as the **Media Type**.</span></span>  <span data-ttu-id="9b618-132">다른 옵션은 **Verizon의 Azure CDN**에서 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-132">The other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="9b618-133">**HTTP LOB(Large Object)** 를 선택하지 않으면 경고가 절대로 트리거되지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-133">Failure to select **HTTP Large Object** will cause your alert to never be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="9b618-134">**메트릭**, **연산자** 및 **트리거 값**을 선택하여 모니터링하기 위해 **식**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-134">Create an **Expression** to monitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="9b618-135">**메트릭**의 경우 모니터링하려는 조건의 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-135">For **Metric**, select the type of condition you want monitored.</span></span>  <span data-ttu-id="9b618-136">**대역폭 Mbps** 는 초당 메가비트인 대역폭 양입니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-136">**Bandwidth Mbps** is the amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="9b618-137">**총 연결** 은 에지 서버에 대한 동시 HTTP 연결의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-137">**Total Connections** is the number of concurrent HTTP connections to our edge servers.</span></span>  <span data-ttu-id="9b618-138">다양한 캐시 상태 및 상태 코드의 정의는 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx) 및 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b618-138">For definitions of the various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="9b618-139">**연산자** 는 메트릭과 트리거 값 간의 관계를 설정하는 수학 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-139">**Operator** is the mathematical operator that establishes the relationship between the metric and the trigger value.</span></span>
   * <span data-ttu-id="9b618-140">**트리거 값** 은 알림이 전송되기 전에 충족해야 하는 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-140">**Trigger Value** is the threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="9b618-141">아래 예제에서 만들어 놓은 식은 404 상태 코드의 수가 25보다 클 때 알림을 받게 된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-141">In the below example, the expression I have created indicates that I would like to be notified when the number of 404 status codes is greater than 25.</span></span>
     
     ![실시간 경고 샘플 식](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="9b618-143">**간격**에 식을 평가하려는 빈도를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-143">For **Interval**, enter how frequently you would like the expression evaluated.</span></span>
10. <span data-ttu-id="9b618-144">**알림 대상** 드롭다운에서 식이 true일 떼 알림을 받으려는 경우를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-144">In the **Notify on** dropdown, select when you would like to be notified when the expression is true.</span></span>
    
    * <span data-ttu-id="9b618-145">**조건 시작** 은 지정된 조건이 처음 감지될 때 알림이 전송되지 않는다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-145">**Condition Start** indicates that a notification will be sent when the specified condition is first detected.</span></span>
    * <span data-ttu-id="9b618-146">**조건 종료** 는 지정된 조건이 더 이상 감지되지 않을 때 알림이 전송되지 않는다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-146">**Condition End** indicates that a notification will be sent when the specified condition is no longer detected.</span></span> <span data-ttu-id="9b618-147">네트워크 모니터링 시스템이 지정된 조건이 발생했음을 감지한 후에만 이 알림이 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-147">This notification can only be triggered after our network monitoring system detected that the specified condition occurred.</span></span>
    * <span data-ttu-id="9b618-148">**연속** 은 네트워크 모니터링 시스템이 지정된 조건을 감지할 때마다 알림이 전송된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-148">**Continuous** indicates that a notification will be sent each time that the network monitoring system detects the specified condition.</span></span> <span data-ttu-id="9b618-149">네트워크 모니터링 시스템은 지정된 조건의 간격으로 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-149">Keep in mind that the network monitoring system will only check once per interval for the specified condition.</span></span>
    * <span data-ttu-id="9b618-150">**조건 시작 및 종료** 는 처음으로 지정된 상태가 감지된 때와 조건이 더 이상 감지되지 않을 때 다시 한 번 알림을 전송한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-150">**Condition Start and End** indicates that a notification will be sent the first time that the specified condition is detected and once again when the condition is no longer detected.</span></span>
11. <span data-ttu-id="9b618-151">전자 메일로 알림을 수신하려는 경우 **전자 메일 알림** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-151">If you want to receive notifications by email, check the **Notify by Email** checkbox.</span></span>  
    
    ![전자 메일로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="9b618-153">**받는 사람** 필드에 알림을 전송하려는 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-153">In the **To** field, enter the email address you where you want notifications sent.</span></span> <span data-ttu-id="9b618-154">**제목** 및 **본문**에 기본값을 그대로 두거나 메시지를 보낼 때 동적으로 경고 데이터를 삽입하려면 **사용할 수 있는 키워드** 목록을 사용하여 메시지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-154">For **Subject** and **Body**, you may leave the default, or you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9b618-155">**테스트 알림** 단추를 클릭하여 전자 메일 알림을 테스트할 수 있지만 경고 구성을 저장한 후에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-155">You can test the email notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="9b618-156">웹 서버에 알림을 게시하려면 **HTTP 게시로 알림** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-156">If you want notifications to be posted to a web server, check the **Notify by HTTP Post** checkbox.</span></span>
    
    ![HTTP 게시로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="9b618-158">**URL** 필드에 HTTP 메시지를 게시할 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-158">In the **Url** field, enter the URL you where you want the HTTP message posted.</span></span> <span data-ttu-id="9b618-159">**헤더** 텍스트 상자에 요청에서 보낼 HTTP 헤더를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-159">In the **Headers** textbox, enter the HTTP headers to be sent in the request.</span></span>  <span data-ttu-id="9b618-160">**본문**에 메시지를 보낼 때 동적으로 경고 데이터를 삽입하려면 **사용할 수 있는 키워드** 목록을 사용하여 메시지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-160">For **Body** you may customize the message using the **Available keywords** list to dynamically insert alert data when the message is sent.</span></span>  <span data-ttu-id="9b618-161">**헤더** 및 **본문**은 아래 예제와 유사한 XML 페이로드에 대한 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-161">**Headers** and **Body** default to an XML payload similar to the below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="9b618-162">**테스트 알림** 단추를 클릭하여 HTTP 게시 알림을 테스트할 수 있지만 경고 구성을 저장한 후에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-162">You can test the HTTP Post notification by clicking the **Test Notification** button, but only after the alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="9b618-163">**저장** 단추를 클릭하여 경고 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-163">Click the **Save** button to save your alert configuration.</span></span>  <span data-ttu-id="9b618-164">5단계에서 **경고 사용** 을 선택한 경우 경고는 지금 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b618-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b618-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b618-165">Next Steps</span></span>
* <span data-ttu-id="9b618-166">[Azure CDN의 실시간 통계](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="9b618-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="9b618-167">[고급 HTTP 보고서](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="9b618-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="9b618-168">[사용 패턴](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="9b618-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

