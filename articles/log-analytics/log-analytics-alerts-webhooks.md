---
title: "OMS Log Analytics에서 웹후크 경고 작업 샘플 | Microsoft Docs"
description: "Log Analytics 경고에 응답하여 실행할 수 있는 작업 중 하나는 단일 HTTP 요청을 통해 외부 프로세스를 호출할 수 있는 *웹후크*입니다. 이 문서에서는 Slack을 사용하여 Log Analytics 경고에 웹후크 작업을 만드는 예제를 연습합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="f5e8c-104">OMS Log Analytics에서 Slack에 메시지를 보내는 경고 웹후크 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="f5e8c-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="f5e8c-105">[Log Analytics 경고](log-analytics-alerts.md) 에 응답하여 실행할 수 있는 작업 중 하나는 단일 HTTP 요청을 통해 외부 프로세스를 호출할 수 있는 *웹후크*입니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="f5e8c-106">[Log Analytics의 경고](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f5e8c-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="f5e8c-107">이 문서에서는 메시지 서비스인 Slack을 사용하여 Log Analytics 경고에 웹후크 작업을 만드는 예를 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="f5e8c-108">이 샘플을 완료하려면 Slack 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="f5e8c-109">[slack.com](http://slack.com)에서 무료 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="f5e8c-110">1단계 - Slack에서 웹후크를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f5e8c-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="f5e8c-111">[slack.com](http://slack.com)에서 Slack에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="f5e8c-112">왼쪽 창의 **채널** 섹션에서 채널을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="f5e8c-113">메시지를 받게 될 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="f5e8c-114">**일반** 또는 **임의**와 같은 기본 채널 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="f5e8c-115">프로덕션 시나리오에서는 **criticalservicealerts**와 같은 특수 채널을 만들 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="f5e8c-117">**앱 또는 사용자 지정 통합 추가** 를 클릭하여 앱 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="f5e8c-118">검색 상자에 *웹후크* 를 입력하고 **들어오는 웹후크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="f5e8c-120">팀 이름 옆의 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="f5e8c-121">**구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="f5e8c-122">이 예제에 사용할 채널을 선택한 다음 **들어오는 웹후크 통합 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="f5e8c-123">**웹후크 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="f5e8c-124">복사한 내용을 경고 구성에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="f5e8c-126">2 단계 - Log Analytics에서 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="f5e8c-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="f5e8c-127">[경고 규칙을 만듭니다](log-analytics-alerts.md) .</span><span class="sxs-lookup"><span data-stu-id="f5e8c-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="f5e8c-128">쿼리: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="f5e8c-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="f5e8c-129">이 경고 확인 간격: 5 분</span><span class="sxs-lookup"><span data-stu-id="f5e8c-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="f5e8c-130">결과 수: 10보다 큼</span><span class="sxs-lookup"><span data-stu-id="f5e8c-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="f5e8c-131">이 기간 동안: 60 분</span><span class="sxs-lookup"><span data-stu-id="f5e8c-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="f5e8c-132">**웹후크**에 대해 **예**를 선택하고 다른 작업에 대해 **아니오**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="f5e8c-133">**웹후크 URL** 필드에 Slack URL을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="f5e8c-134">**사용자 지정 JSON 페이로드를 포함할**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="f5e8c-135">Slack은 *text*라는 매개 변수를 사용하여 JSON 형식으로 설정된 페이로드를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="f5e8c-136">이는 생성하는 메시지에 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="f5e8c-137">다음 예와 같이 *#* 기호를 사용하여 경고 매개 변수 중 하나 이상을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![예제 JSON 페이로드](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="f5e8c-139">**저장** 을 클릭하여 경고 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="f5e8c-140">경고가 생성될 때까지 충분한 시간 동안 기다린 다음 다음과 유사한 메시지에 대해 Slack을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![Slack의 예제 웹후크](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="f5e8c-142">Slack을 위한 고급 웹후크 페이로드</span><span class="sxs-lookup"><span data-stu-id="f5e8c-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="f5e8c-143">Slack을 사용하여 인바운드 메시지를 광범위하게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="f5e8c-144">자세한 내용은 Slack 웹 사이트의 [들어오는 웹후크](https://api.slack.com/incoming-webhooks) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="f5e8c-145">다음은 서식을 가진 풍부한 메시지를 만들기 위한 더 복잡한 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="f5e8c-146">이는 Slack에 다음과 유사한 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-146">This would generate a message in Slack similar to the following.</span></span>

![Slack의 예제 메시지](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="f5e8c-148">요약</span><span class="sxs-lookup"><span data-stu-id="f5e8c-148">Summary</span></span>
<span data-ttu-id="f5e8c-149">이 경고 규칙이 적용되는 상태에서 조건을 만족할 때마다 메시지를 Slack에 보내도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="f5e8c-150">이는 경고에 응답하여 만들 수 있는 작업의 한 예일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="f5e8c-151">다른 외부 서비스를 호출하는 웹후크 작업, Azure 자동화에서 Runbook을 시작하는 Runbook 작업 또는 본인과 다른 받는 사람에게 메일을 보내는 전자 메일 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="f5e8c-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5e8c-152">Next Steps</span></span>
* <span data-ttu-id="f5e8c-153">다른 작업을 포함하여 [Log Analytics의 경고 작업](log-analytics-alerts-actions.md)에 관하여 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f5e8c-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


