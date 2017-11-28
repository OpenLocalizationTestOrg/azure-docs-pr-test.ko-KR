---
title: "aaaAzure CDN 실시간 경고 | Microsoft Docs"
description: "Microsoft Azure CDN의 실시간 경고입니다. 실시간 경고 hello 끝점에서 CDN 프로필의 hello 성능에 대 한 알림을 제공합니다."
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
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a><span data-ttu-id="c0497-104">Microsoft Azure CDN의 실시간 경고</span><span class="sxs-lookup"><span data-stu-id="c0497-104">Real-time alerts in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c0497-105">개요</span><span class="sxs-lookup"><span data-stu-id="c0497-105">Overview</span></span>
<span data-ttu-id="c0497-106">이 문서에서는 Microsoft Azure CDN의 실시간 경고에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-106">This document explains real-time alerts in Microsoft Azure CDN.</span></span> <span data-ttu-id="c0497-107">이 기능은 CDN 프로필의 hello 끝점 hello 성능에 대 한 실시간 알림을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-107">This functionality provides real-time notifications about hello performance of hello endpoints in your CDN profile.</span></span>  <span data-ttu-id="c0497-108">다음을 기반으로 전자 메일 또는 HTTP 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-108">You can set up email or HTTP alerts based on:</span></span>

* <span data-ttu-id="c0497-109">대역폭</span><span class="sxs-lookup"><span data-stu-id="c0497-109">Bandwidth</span></span>
* <span data-ttu-id="c0497-110">상태 코드</span><span class="sxs-lookup"><span data-stu-id="c0497-110">Status Codes</span></span>
* <span data-ttu-id="c0497-111">캐시 상태</span><span class="sxs-lookup"><span data-stu-id="c0497-111">Cache Statuses</span></span>
* <span data-ttu-id="c0497-112">연결</span><span class="sxs-lookup"><span data-stu-id="c0497-112">Connections</span></span>

## <a name="creating-a-real-time-alert"></a><span data-ttu-id="c0497-113">실시간 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="c0497-113">Creating a real-time alert</span></span>
1. <span data-ttu-id="c0497-114">Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. <span data-ttu-id="c0497-116">Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    <span data-ttu-id="c0497-118">hello CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="c0497-119">마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **실시간 통계** 플라이 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c0497-120">**실시간 경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-120">Click on **Real-Time Alerts**.</span></span>
   
    ![CDN 관리 포털](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    <span data-ttu-id="c0497-122">기존 경고 구성 (있는 경우)의 hello 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-122">hello list of existing alert configurations (if any) is displayed.</span></span>
4. <span data-ttu-id="c0497-123">Hello 클릭 **경고 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-123">Click hello **Add Alert** button.</span></span>
   
    ![경고 추가 단추](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    <span data-ttu-id="c0497-125">새 경고를 만드는 양식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-125">A form for creating a new alert is displayed.</span></span>
   
    ![새 경고 양식](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. <span data-ttu-id="c0497-127">이 경고 toobe 활성 하려면 클릭할 때 **저장**, hello 확인 **경고가 활성화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-127">If you want this alert toobe active when you click **Save**, check hello **Alert Enabled** checkbox.</span></span>
6. <span data-ttu-id="c0497-128">Hello에 따라 경고에 대 한 설명이 포함 된 이름을 입력 **이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-128">Enter a descriptive name for your alert in hello **Name** field.</span></span>
7. <span data-ttu-id="c0497-129">Hello에 **미디어 유형** 드롭다운 **HTTP 대형 개체**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-129">In hello **Media Type** dropdown, select **HTTP Large Object**.</span></span>
   
    ![HTTP LOB(Large Object)를 선택한 미디어 유형](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="c0497-131">선택 해야 **HTTP 대형 개체** hello로 **미디어 유형**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-131">You must select **HTTP Large Object** as hello **Media Type**.</span></span>  <span data-ttu-id="c0497-132">hello 다른 선택 항목에서 사용 하지 않는 **Verizon에서 Azure CDN**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-132">hello other choices are not used by **Azure CDN from Verizon**.</span></span>  <span data-ttu-id="c0497-133">오류 tooselect **HTTP 대형 개체** 결제 경고가 발생 합니다 toonever 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-133">Failure tooselect **HTTP Large Object** will cause your alert toonever be triggered.</span></span>
   > 
   > 
8. <span data-ttu-id="c0497-134">만들기는 **식** 선택 하 여 toomonitor는 **메트릭을**, **연산자**, 및 **값 트리거할**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-134">Create an **Expression** toomonitor by selecting a **Metric**, **Operator**, and **Trigger value**.</span></span>
   
   * <span data-ttu-id="c0497-135">에 대 한 **메트릭을**를 모니터링할 조건의 hello 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-135">For **Metric**, select hello type of condition you want monitored.</span></span>  <span data-ttu-id="c0497-136">**대역폭 Mbps** hello 양의 초당 메가 비트에서 대역폭 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-136">**Bandwidth Mbps** is hello amount of bandwidth usage in megabits per second.</span></span>  <span data-ttu-id="c0497-137">**총 연결** 동시 HTTP 연결 tooour hello 수에 지 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-137">**Total Connections** is hello number of concurrent HTTP connections tooour edge servers.</span></span>  <span data-ttu-id="c0497-138">다양 한 캐시 상태 및 상태 코드 참조에 대 한 hello 정의 [Azure CDN 캐시 상태 코드](https://msdn.microsoft.com/library/mt759237.aspx) 및 [Azure CDN HTTP 상태 코드](https://msdn.microsoft.com/library/mt759238.aspx)</span><span class="sxs-lookup"><span data-stu-id="c0497-138">For definitions of hello various cache statuses and status codes, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) and [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)</span></span>
   * <span data-ttu-id="c0497-139">**연산자** hello 메트릭 및 hello 트리거 값 간에 hello 관계를 설정 하는 hello 수학 연산자.</span><span class="sxs-lookup"><span data-stu-id="c0497-139">**Operator** is hello mathematical operator that establishes hello relationship between hello metric and hello trigger value.</span></span>
   * <span data-ttu-id="c0497-140">**트리거 값** hello 알림이 전송 하기 위해 충족 되어야 하는 것이 임계값은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-140">**Trigger Value** is hello threshold value that must be met before a notification will be sent out.</span></span>
     
     <span data-ttu-id="c0497-141">아래 예제는 hello, 만든 hello 식 404 상태 코드의 hello 수는 25 보다 큰 경우 알림을 받는 toobe 싶습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-141">In hello below example, hello expression I have created indicates that I would like toobe notified when hello number of 404 status codes is greater than 25.</span></span>
     
     ![실시간 경고 샘플 식](./media/cdn-real-time-alerts/cdn-expression.png)
9. <span data-ttu-id="c0497-143">에 대 한 **간격**를 얼마나 자주 원하는 hello 식이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-143">For **Interval**, enter how frequently you would like hello expression evaluated.</span></span>
10. <span data-ttu-id="c0497-144">Hello에 **알림** 드롭다운을 toobe 때 알림을 받으려면 hello 식이 true 인 경우 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-144">In hello **Notify on** dropdown, select when you would like toobe notified when hello expression is true.</span></span>
    
    * <span data-ttu-id="c0497-145">**시작 조건** hello를 지정 된 조건이 처음 감지 된 경우 알림이 전송 되지 않음을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-145">**Condition Start** indicates that a notification will be sent when hello specified condition is first detected.</span></span>
    * <span data-ttu-id="c0497-146">**끝 조건을** hello를 지정 된 조건이 더 이상 검색 하는 경우 알림이 전송 되지 않음을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-146">**Condition End** indicates that a notification will be sent when hello specified condition is no longer detected.</span></span> <span data-ttu-id="c0497-147">모니터링 시스템이 네트워크에 지정 된 해당 hello 검색 된 후에이 알림 메시지를 트리거할 수 조건이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-147">This notification can only be triggered after our network monitoring system detected that hello specified condition occurred.</span></span>
    * <span data-ttu-id="c0497-148">**연속** 네트워크 모니터링 시스템 hello 때마다 지정 된 hello 검색으로 알림을 보낼 수 나타냅니다 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-148">**Continuous** indicates that a notification will be sent each time that hello network monitoring system detects hello specified condition.</span></span> <span data-ttu-id="c0497-149">모니터링 시스템을 검사 한 번 hello에 대 한 간격 마다 지정 조건에만 해당 hello 네트워크를 명심 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c0497-149">Keep in mind that hello network monitoring system will only check once per interval for hello specified condition.</span></span>
    * <span data-ttu-id="c0497-150">**조건 시작 및 끝** hello hello 지정 된 조건이 처음으로 검색 되 고 다시 한 번 hello 조건이 감지 되 면 더 이상으로 알림이 전송 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-150">**Condition Start and End** indicates that a notification will be sent hello first time that hello specified condition is detected and once again when hello condition is no longer detected.</span></span>
11. <span data-ttu-id="c0497-151">전자 메일을 통해 tooreceive 알림을 원하는 경우 확인 hello **알림 전자 메일을 통해** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-151">If you want tooreceive notifications by email, check hello **Notify by Email** checkbox.</span></span>  
    
    ![전자 메일로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    <span data-ttu-id="c0497-153">Hello에 **를** 필드 알림을 원하는 보낸 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-153">In hello **To** field, enter hello email address you where you want notifications sent.</span></span> <span data-ttu-id="c0497-154">에 대 한 **주체** 및 **본문**hello 기본 수준은 낮아질 수 있습니다, 또는 hello를 사용 하 여 hello 메시지를 사용자 지정할 수 있습니다 **사용할 수 있는 키워드** 목록 toodynamically 경고 데이터를 삽입할 때 hello 메시지가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-154">For **Subject** and **Body**, you may leave hello default, or you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c0497-155">Hello를 클릭 하 여 hello 전자 메일 알림을 테스트할 수 있습니다 **테스트 알림** 단추만 hello 경고 구성을 저장 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-155">You can test hello email notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
12. <span data-ttu-id="c0497-156">알림 toobe tooa 웹 서버에 게시 하려는 경우 확인 hello **HTTP Post로 알림** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-156">If you want notifications toobe posted tooa web server, check hello **Notify by HTTP Post** checkbox.</span></span>
    
    ![HTTP 게시로 알림 양식](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    <span data-ttu-id="c0497-158">Hello에 **Url** 필드 hello URL을 게시 하려는 HTTP hello 메시지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-158">In hello **Url** field, enter hello URL you where you want hello HTTP message posted.</span></span> <span data-ttu-id="c0497-159">Hello에 **헤더** textbox hello 요청에서 전송 하는 hello HTTP 헤더 toobe를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-159">In hello **Headers** textbox, enter hello HTTP headers toobe sent in hello request.</span></span>  <span data-ttu-id="c0497-160">에 대 한 **본문** hello를 사용 하 여 hello 메시지를 사용자 지정할 수 있습니다 **사용할 수 있는 키워드** 목록 toodynamically hello 메시지를 보낼 때 경고 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-160">For **Body** you may customize hello message using hello **Available keywords** list toodynamically insert alert data when hello message is sent.</span></span>  <span data-ttu-id="c0497-161">**헤더** 및 **본문** tooan XML 페이로드 아래 예제와 비슷한 toohello 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-161">**Headers** and **Body** default tooan XML payload similar toohello below example.</span></span>
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > <span data-ttu-id="c0497-162">Hello를 클릭 하 여 HTTP Post 알림 hello를 테스트할 수 있습니다 **테스트 알림** 단추만 hello 경고 구성을 저장 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-162">You can test hello HTTP Post notification by clicking hello **Test Notification** button, but only after hello alert configuration has been saved.</span></span>
    > 
    > 
13. <span data-ttu-id="c0497-163">Hello 클릭 **저장** 단추 toosave 경고 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-163">Click hello **Save** button toosave your alert configuration.</span></span>  <span data-ttu-id="c0497-164">5단계에서 **경고 사용** 을 선택한 경우 경고는 지금 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0497-164">If you checked **Alert Enabled** in step 5, your alert is now active.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0497-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0497-165">Next Steps</span></span>
* <span data-ttu-id="c0497-166">[Azure CDN의 실시간 통계](cdn-real-time-stats.md)</span><span class="sxs-lookup"><span data-stu-id="c0497-166">Analyze [Real-time stats in Azure CDN](cdn-real-time-stats.md)</span></span>
* <span data-ttu-id="c0497-167">[고급 HTTP 보고서](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="c0497-167">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c0497-168">[사용 패턴](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="c0497-168">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

