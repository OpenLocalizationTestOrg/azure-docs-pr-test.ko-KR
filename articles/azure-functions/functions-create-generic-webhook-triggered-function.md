---
title: "Azure에서 제네릭 웹후크를 통해 트리거되는 함수 만들기 | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure의 웹후크에 의해 호출되는 서버 없는 함수를 만듭니다."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: f283f8d79c5ae5fb6a72c84c9e9edb7bb8de4a83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="e5b13-103">제네릭 웹후크를 통해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="e5b13-104">Azure Functions를 사용하면 먼저 VM을 만들거나 웹 응용 프로그램을 게시하지 않고도 서버를 사용하지 않는 환경에서 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="e5b13-105">예를 들어 Azure Monitor에서 발생된 경고에 의해 트리거되도록 함수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-105">For example, you can configure a function to be triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="e5b13-106">이 항목에서는 리소스 그룹이 구독에 추가될 때 C# 코드를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-106">This topic shows you how to execute C# code when a resource group is added to your subscription.</span></span>   

![Azure Portal에서 제네릭 웹후크를 통해 트리거되는 함수](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="e5b13-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e5b13-108">Prerequisites</span></span> 

<span data-ttu-id="e5b13-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-109">To complete this tutorial:</span></span>

+ <span data-ttu-id="e5b13-110">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="e5b13-111">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="e5b13-112">다음으로 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="e5b13-113"><a name="create-function"></a>제네릭 웹후크를 통해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="e5b13-114">함수 앱을 확장한 후 **함수** 옆의 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="e5b13-115">이 함수가 함수 앱의 첫 번째 함수이면 **사용자 지정 함수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-115">If this function is the first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="e5b13-116">그러면 함수 템플릿의 전체 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-116">This displays the complete set of function templates.</span></span>

    ![Azure Portal에서 함수 빨리 시작하기 페이지](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="e5b13-118">**제네릭 웹후크 - C#** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-118">Select the **Generic WebHook - C#** template.</span></span> <span data-ttu-id="e5b13-119">C# 함수의 이름을 입력하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Azure Portal에서 제네릭 웹후크를 통해 트리거되는 함수 만들기](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="e5b13-121">새 함수에서 **</> 함수 URL 가져오기**를 클릭한 다음 값을 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-121">In your new function, click **</> Get function URL**, then copy and save the value.</span></span> <span data-ttu-id="e5b13-122">이 값을 사용하여 웹후크를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-122">You use this value to configure the webhook.</span></span> 

    ![함수 코드 검토](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="e5b13-124">다음으로 Azure Monitor의 활동 로그 경고에서 웹후크 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="e5b13-125">활동 로그 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-125">Create an activity log alert</span></span>

1. <span data-ttu-id="e5b13-126">Azure Portal에서 **모니터** 서비스로 이동하고 **경고**를 선택한 후 **활동 로그 경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-126">In the Azure portal, navigate to the **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![모니터](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="e5b13-128">표에 지정된 대로 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-128">Use the settings as specified in the table:</span></span>

    ![활동 로그 경고 만들기](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="e5b13-130">설정</span><span class="sxs-lookup"><span data-stu-id="e5b13-130">Setting</span></span>      |  <span data-ttu-id="e5b13-131">제안 값</span><span class="sxs-lookup"><span data-stu-id="e5b13-131">Suggested value</span></span>   | <span data-ttu-id="e5b13-132">설명</span><span class="sxs-lookup"><span data-stu-id="e5b13-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="e5b13-133">**활동 로그 경고 이름**</span><span class="sxs-lookup"><span data-stu-id="e5b13-133">**Activity log alert name**</span></span> | <span data-ttu-id="e5b13-134">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="e5b13-134">resource-group-create-alert</span></span> | <span data-ttu-id="e5b13-135">활동 로그 경고의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-135">Name of the activity log alert.</span></span> |
    | <span data-ttu-id="e5b13-136">**구독**</span><span class="sxs-lookup"><span data-stu-id="e5b13-136">**Subscription**</span></span> | <span data-ttu-id="e5b13-137">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="e5b13-137">Your subscription</span></span> | <span data-ttu-id="e5b13-138">이 자습서를 위해 사용 중인 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-138">The subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="e5b13-139">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="e5b13-139">**Resource Group**</span></span> | <span data-ttu-id="e5b13-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e5b13-140">myResourceGroup</span></span> | <span data-ttu-id="e5b13-141">경고 리소스가 배포되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-141">The resource group that the alert resources are deployed to.</span></span> <span data-ttu-id="e5b13-142">함수 앱과 동일한 리소스 그룹을 사용하면 자습서를 완료한 후 보다 쉽게 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-142">Using the same resource group as your function app makes it easier to clean up after you complete the tutorial.</span></span> |
    | <span data-ttu-id="e5b13-143">**이벤트 범주**</span><span class="sxs-lookup"><span data-stu-id="e5b13-143">**Event category**</span></span> | <span data-ttu-id="e5b13-144">관리</span><span class="sxs-lookup"><span data-stu-id="e5b13-144">Administrative</span></span> | <span data-ttu-id="e5b13-145">이 범주에는 Azure 리소스에 대한 변경 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-145">This category includes changes made to Azure resources.</span></span>  |
    | <span data-ttu-id="e5b13-146">**리소스 종류**</span><span class="sxs-lookup"><span data-stu-id="e5b13-146">**Resource type**</span></span> | <span data-ttu-id="e5b13-147">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="e5b13-147">Resource groups</span></span> | <span data-ttu-id="e5b13-148">경고를 리소스 그룹 활동으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-148">Filters alerts to resource group activities.</span></span> |
    | <span data-ttu-id="e5b13-149">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="e5b13-149">**Resource Group**</span></span><br/><span data-ttu-id="e5b13-150">및 **리소스**</span><span class="sxs-lookup"><span data-stu-id="e5b13-150">and **Resource**</span></span> | <span data-ttu-id="e5b13-151">모두</span><span class="sxs-lookup"><span data-stu-id="e5b13-151">All</span></span> | <span data-ttu-id="e5b13-152">모든 리소스를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="e5b13-153">**작업 이름**</span><span class="sxs-lookup"><span data-stu-id="e5b13-153">**Operation name**</span></span> | <span data-ttu-id="e5b13-154">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-154">Create Resource Group</span></span> | <span data-ttu-id="e5b13-155">경고를 만들기 작업으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-155">Filters alerts to create operations.</span></span> |
    | <span data-ttu-id="e5b13-156">**Level**</span><span class="sxs-lookup"><span data-stu-id="e5b13-156">**Level**</span></span> | <span data-ttu-id="e5b13-157">정보 제공</span><span class="sxs-lookup"><span data-stu-id="e5b13-157">Informational</span></span> | <span data-ttu-id="e5b13-158">정보 수준 경고를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="e5b13-159">**상태**</span><span class="sxs-lookup"><span data-stu-id="e5b13-159">**Status**</span></span> | <span data-ttu-id="e5b13-160">Succeeded</span><span class="sxs-lookup"><span data-stu-id="e5b13-160">Succeeded</span></span> | <span data-ttu-id="e5b13-161">경고를 성공적으로 완료한 작업으로 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-161">Filters alerts to actions that have completed successfully.</span></span> |
    | <span data-ttu-id="e5b13-162">**작업 그룹**</span><span class="sxs-lookup"><span data-stu-id="e5b13-162">**Action group**</span></span> | <span data-ttu-id="e5b13-163">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="e5b13-163">New</span></span> | <span data-ttu-id="e5b13-164">경고가 발생하는 경우 수행하는 작업을 정의하는 새 작업 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-164">Create a new action group, which defines the action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="e5b13-165">**작업 그룹 이름**</span><span class="sxs-lookup"><span data-stu-id="e5b13-165">**Action group name**</span></span> | <span data-ttu-id="e5b13-166">function-webhook</span><span class="sxs-lookup"><span data-stu-id="e5b13-166">function-webhook</span></span> | <span data-ttu-id="e5b13-167">작업 그룹을 식별하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-167">A name to identify the action group.</span></span>  | 
    | <span data-ttu-id="e5b13-168">**짧은 이름**</span><span class="sxs-lookup"><span data-stu-id="e5b13-168">**Short name**</span></span> | <span data-ttu-id="e5b13-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="e5b13-169">funcwebhook</span></span> | <span data-ttu-id="e5b13-170">작업 그룹에 대한 짧은 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-170">A short name for the action group.</span></span> |  

3. <span data-ttu-id="e5b13-171">**작업**에서 표에 지정된 설정을 사용하여 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-171">In **Actions**, add an action using the settings as specified in the table:</span></span> 

    ![작업 그룹 추가](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="e5b13-173">설정</span><span class="sxs-lookup"><span data-stu-id="e5b13-173">Setting</span></span>      |  <span data-ttu-id="e5b13-174">제안 값</span><span class="sxs-lookup"><span data-stu-id="e5b13-174">Suggested value</span></span>   | <span data-ttu-id="e5b13-175">설명</span><span class="sxs-lookup"><span data-stu-id="e5b13-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="e5b13-176">**Name**</span><span class="sxs-lookup"><span data-stu-id="e5b13-176">**Name**</span></span> | <span data-ttu-id="e5b13-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="e5b13-177">CallFunctionWebhook</span></span> | <span data-ttu-id="e5b13-178">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-178">A name for the action.</span></span> |
    | <span data-ttu-id="e5b13-179">**작업 유형**</span><span class="sxs-lookup"><span data-stu-id="e5b13-179">**Action type**</span></span> | <span data-ttu-id="e5b13-180">웹후크</span><span class="sxs-lookup"><span data-stu-id="e5b13-180">Webhook</span></span> | <span data-ttu-id="e5b13-181">경고에 대한 응답은 웹후크 URL이 호출되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-181">The response to the alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="e5b13-182">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="e5b13-182">**Details**</span></span> | <span data-ttu-id="e5b13-183">함수 URL</span><span class="sxs-lookup"><span data-stu-id="e5b13-183">Function URL</span></span> | <span data-ttu-id="e5b13-184">앞에서 복사한 함수의 웹후크 URL에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-184">Paste in the webhook URL of the function that you copied earlier.</span></span> |<span data-ttu-id="e5b13-185">v</span><span class="sxs-lookup"><span data-stu-id="e5b13-185">v</span></span>

4. <span data-ttu-id="e5b13-186">**확인**을 클릭하여 경고 및 작업 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-186">Click **OK** to create the alert and action group.</span></span>  

<span data-ttu-id="e5b13-187">이제 구독에서 리소스 그룹을 만들 때 웹후크가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-187">The webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="e5b13-188">다음으로, 요청 본문의 JSON 로그 데이터를 처리하도록 함수의 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-188">Next, you update the code in your function to handle the JSON log data in the body of the request.</span></span>   

## <a name="update-the-function-code"></a><span data-ttu-id="e5b13-189">함수 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="e5b13-189">Update the function code</span></span>

1. <span data-ttu-id="e5b13-190">포털의 함수 앱으로 돌아간 후 함수를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-190">Navigate back to your function app in the portal, and expand your function.</span></span> 

2. <span data-ttu-id="e5b13-191">포털에서 함수의 C# 스크립트 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-191">Replace the C# script code in the function in the portal with the following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get the activityLog object from the JSON in the message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if the resource in the activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about the created resource group to the streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="e5b13-192">이제 구독에 새 리소스 그룹을 만들어 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-192">Now you can test the function by creating a new resource group in your subscription.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="e5b13-193">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="e5b13-193">Test the function</span></span>

1. <span data-ttu-id="e5b13-194">Azure Portal 왼쪽에 있는 리소스 그룹 아이콘을 클릭하고 **+추가**를 선택한 후 **리소스 그룹 이름**을 입력하고 **만들기**를 선택하여 빈 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-194">Click the resource group icon in the left of the Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** to create an empty resource group.</span></span>
    
    ![리소스 그룹을 만듭니다.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="e5b13-196">함수도 돌아가서 **로그** 창을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-196">Go back to your function and expand the **Logs** window.</span></span> <span data-ttu-id="e5b13-197">리소스 그룹이 만들어지면 활동 로그 경고가 웹후크를 트리거하고 함수가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-197">After the resource group is created, the activity log alert triggers the webhook and the function executes.</span></span> <span data-ttu-id="e5b13-198">로그에 기록된 새 리소스 그룹의 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-198">You see the name of the new resource group written to the logs.</span></span>  

    ![테스트 응용 프로그램 설정을 추가합니다.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="e5b13-200">(선택 사항) 뒤로 돌아가 만든 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-200">(Optional) Go back and delete the resource group that you created.</span></span> <span data-ttu-id="e5b13-201">이 활동은 함수를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-201">Note that this activity doesn't trigger the function.</span></span> <span data-ttu-id="e5b13-202">삭제 작업이 경고에 의해 필터링되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-202">This is because delete operations are filtered out by the alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="e5b13-203">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="e5b13-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="e5b13-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5b13-204">Next steps</span></span>

<span data-ttu-id="e5b13-205">제네릭 웹후크에서 요청을 수신할 때 실행되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5b13-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="e5b13-206">웹후크 트리거에 대한 자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](functions-bindings-http-webhook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5b13-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="e5b13-207">C#으로 함수를 개발하는 방법에 대한 자세한 내용은 [Azure Functions C# 스크립트 개발자 참조](functions-reference-csharp.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5b13-207">To learn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

