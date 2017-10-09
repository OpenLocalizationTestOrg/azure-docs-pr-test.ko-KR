---
title: "OMS 로그 분석에서 경고 작업 샘플 aaaWebhook | Microsoft Docs"
description: "로그 분석 경고는 응답 tooa에서 실행할 수 있는 hello 작업 중 하나는 * tooinvoke 단일 HTTP 요청을 통해 외부 프로세스 수 있는 webhook * 합니다. 이 문서에서는 Slack을 사용하여 Log Analytics 경고에 웹후크 작업을 만드는 예제를 연습합니다."
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
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="5f6ef-104">OMS 로그 분석 toosend 메시지 tooSlack에서 경고 webhook 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="5f6ef-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="5f6ef-105">응답 tooa에서 실행할 수 있는 hello 작업 중 하나 [로그 분석 경고](log-analytics-alerts.md) 는 *webhook*, tooinvoke 단일 HTTP 요청을 통해 외부 프로세스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="5f6ef-106">[Log Analytics의 경고](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="5f6ef-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="5f6ef-107">이 문서에서는 메시지 서비스인 Slack을 사용하여 Log Analytics 경고에 웹후크 작업을 만드는 예를 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="5f6ef-108">이 샘플 Slack 계정이 toocomplete 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="5f6ef-109">[slack.com](http://slack.com)에서 무료 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="5f6ef-110">1단계 - Slack에서 웹후크를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5f6ef-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="5f6ef-111">tooSlack 로그인 [slack.com](http://slack.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="5f6ef-112">Hello에 채널을 선택 **채널** hello 왼쪽된 창에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="5f6ef-113">이 hello 채널 hello 메시지에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="5f6ef-114">와 같은 hello 기본 채널 중 하나를 선택할 수 **일반** 또는 **임의**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="5f6ef-115">프로덕션 시나리오에서는 **criticalservicealerts**와 같은 특수 채널을 만들 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="5f6ef-117">클릭 **응용 프로그램 또는 사용자 지정 통합 추가** tooopen hello 응용 프로그램 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="5f6ef-118">형식 *webhook* hello 검색 상자 선택한 후에 **들어오는 Webhook**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="5f6ef-120">클릭 **설치** 다음 tooyour 팀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="5f6ef-121">**구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="5f6ef-122">예를 들어 toouse 거 하 고을 클릭 한 다음 선택 hello hello 채널 **들어오는 Webhook 추가 통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="5f6ef-123">복사 hello **Webhook URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="5f6ef-124">붙일이 hello 경고 구성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Slack 채널](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="5f6ef-126">2 단계 - Log Analytics에서 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5f6ef-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="5f6ef-127">[경고 규칙 만들기](log-analytics-alerts.md) 설정을 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="5f6ef-128">쿼리: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="5f6ef-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="5f6ef-129">이 경고 확인 간격: 5 분</span><span class="sxs-lookup"><span data-stu-id="5f6ef-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="5f6ef-130">결과 수가 hello: 10 보다 큰</span><span class="sxs-lookup"><span data-stu-id="5f6ef-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="5f6ef-131">이 기간 동안: 60 분</span><span class="sxs-lookup"><span data-stu-id="5f6ef-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="5f6ef-132">선택 **예** 에 대 한 **Webhook** 및 **아니요** hello 다른 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="5f6ef-133">Hello에 대 한 여유 URL 붙여넣기 hello **Webhook URL** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="5f6ef-134">Hello 옵션을 너무 선택**사용자 지정 JSON 페이로드 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="5f6ef-135">Slack은 *text*라는 매개 변수를 사용하여 JSON 형식으로 설정된 페이로드를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="5f6ef-136">이 hello 텍스트를 생성 하는 hello 메시지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="5f6ef-137">Hello를 사용 하 여 hello 경고 매개 변수 중 하나 이상을 사용할 수 있습니다  *#*  hello 다음 예제와 같이 이러한 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![예제 JSON 페이로드](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="5f6ef-139">클릭 **저장** toosave hello 경고 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="5f6ef-140">충분 한 시간을 생성 하는 경고 toobe 기다린 비슷한 toohello 다음 될 메시지에 대 한 여유 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![Slack의 예제 웹후크](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="5f6ef-142">Slack을 위한 고급 웹후크 페이로드</span><span class="sxs-lookup"><span data-stu-id="5f6ef-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="5f6ef-143">Slack을 사용하여 인바운드 메시지를 광범위하게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="5f6ef-144">자세한 내용은 참조 [들어오는 Webhook](https://api.slack.com/incoming-webhooks) hello Slack 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="5f6ef-145">다음은 더 복잡 한 페이로드 toocreate 서식을 사용 하 여 서식 있는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
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


<span data-ttu-id="5f6ef-146">메시지를 생성이 Slack toohello 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-146">This would generate a message in Slack similar toohello following.</span></span>

![Slack의 예제 메시지](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="5f6ef-148">요약</span><span class="sxs-lookup"><span data-stu-id="5f6ef-148">Summary</span></span>
<span data-ttu-id="5f6ef-149">위치에이 경고 규칙을 사용 하면 해야 보낸 메시지 tooSlack hello 조건이 충족 될 때마다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="5f6ef-150">응답 tooan 경고에서 만들 수 있는 동작의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="5f6ef-151">메일 tooyourself 또는 다른 받는 사람이 다른 외부 서비스, runbook 작업 toostart 전자 메일 작업 toosend 또는 Azure 자동화에서 runbook을 호출 하는 webhook 매크로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="5f6ef-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f6ef-152">Next Steps</span></span>
* <span data-ttu-id="5f6ef-153">다른 작업을 포함하여 [Log Analytics의 경고 작업](log-analytics-alerts-actions.md)에 관하여 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f6ef-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


