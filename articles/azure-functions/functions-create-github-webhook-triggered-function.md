---
title: "Azure에서 GitHub webhook를 통해 트리거되는 함수 만들기 | Microsoft 문서"
description: "Azure Functions를 사용하여 GitHub webhook를 통해 호출되는 서버 없는 함수를 만듭니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="37f2c-103">GitHub webhook를 통해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="37f2c-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="37f2c-104">GitHub별 페이로드와 함께 HTTP 웹후크 요청에 의해 트리거되는 함수를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Azure Portal에서 Github 웹후크를 통해 트리거되는 함수](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="37f2c-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="37f2c-106">Prerequisites</span></span>

+ <span data-ttu-id="37f2c-107">하나 이상의 프로젝트와 함께 GitHub 계정.</span><span class="sxs-lookup"><span data-stu-id="37f2c-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="37f2c-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="37f2c-108">An Azure subscription.</span></span> <span data-ttu-id="37f2c-109">구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="37f2c-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="37f2c-110">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="37f2c-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="37f2c-112">다음으로 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="37f2c-113">GitHub 웹후크 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="37f2c-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="37f2c-114">함수 앱을 확장한 후 **함수** 옆의 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="37f2c-115">함수 앱에서 첫 번째 함수이면 **사용자 지정 함수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="37f2c-116">그러면 함수 템플릿의 전체 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-116">This displays the complete set of function templates.</span></span>

    ![Azure Portal에서 함수 빨리 시작하기 페이지](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="37f2c-118">원하는 언어에 해당하는 **GitHub WebHook** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="37f2c-119">**함수 이름을 지정한** 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-119">**Name your function**, then select **Create**.</span></span>

     ![Azure Portal에서 GitHub 웹후크를 통해 트리거되는 함수를 만듭니다.](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="37f2c-121">새 함수에서 **</> 함수 URL 가져오기**를 클릭한 다음 값을 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="37f2c-122">**</> GitHub 비밀 가져오기**에 대해 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="37f2c-123">이러한 값은 GitHub에서 webhook를 구성할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-123">You use these values to configure the webhook in GitHub.</span></span>

    ![함수 코드 검토](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="37f2c-125">다음으로 GitHub 리포지토리에 webhook를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="37f2c-126">웹후크 구성</span><span class="sxs-lookup"><span data-stu-id="37f2c-126">Configure the webhook</span></span>

1. <span data-ttu-id="37f2c-127">GitHub에서 소유한 리포지토리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="37f2c-128">분기된 모든 리포지토리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="37f2c-129">리포지토리를 분기해야 하는 경우 <https://github.com/Azure-Samples/functions-quickstart>를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="37f2c-130">**설정**, **Webhooks**, **webhook 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![GitHub 웹후크를 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="37f2c-132">표에 지정된 것처럼 설정을 사용한 후 **웹후크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![웹후크 URL 및 암호를 설정합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="37f2c-134">설정</span><span class="sxs-lookup"><span data-stu-id="37f2c-134">Setting</span></span> | <span data-ttu-id="37f2c-135">제안 값</span><span class="sxs-lookup"><span data-stu-id="37f2c-135">Suggested value</span></span> | <span data-ttu-id="37f2c-136">설명</span><span class="sxs-lookup"><span data-stu-id="37f2c-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="37f2c-137">**페이로드 URL**</span><span class="sxs-lookup"><span data-stu-id="37f2c-137">**Payload URL**</span></span> | <span data-ttu-id="37f2c-138">복사된 값</span><span class="sxs-lookup"><span data-stu-id="37f2c-138">Copied value</span></span> | <span data-ttu-id="37f2c-139">**</> 함수 URL 가져오기**에서 반환된 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="37f2c-140">**비밀**</span><span class="sxs-lookup"><span data-stu-id="37f2c-140">**Secret**</span></span>   | <span data-ttu-id="37f2c-141">복사된 값</span><span class="sxs-lookup"><span data-stu-id="37f2c-141">Copied value</span></span> | <span data-ttu-id="37f2c-142">**</> GitHub 비밀 가져오기**에서 반환된 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="37f2c-143">**콘텐츠 형식**</span><span class="sxs-lookup"><span data-stu-id="37f2c-143">**Content type**</span></span> | <span data-ttu-id="37f2c-144">application/json</span><span class="sxs-lookup"><span data-stu-id="37f2c-144">application/json</span></span> | <span data-ttu-id="37f2c-145">함수에는 JSON 페이로드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="37f2c-146">이벤트 트리거</span><span class="sxs-lookup"><span data-stu-id="37f2c-146">Event triggers</span></span> | <span data-ttu-id="37f2c-147">개별 이벤트를 선택하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-147">Let me select individual events</span></span> | <span data-ttu-id="37f2c-148">문제 주석 이벤트만 트리거하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="37f2c-149">문제 주석</span><span class="sxs-lookup"><span data-stu-id="37f2c-149">Issue comment</span></span> |  |

<span data-ttu-id="37f2c-150">이제 새로운 문제 주석이 추가되면 함수를 트리거하도록 webhook가 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="37f2c-151">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="37f2c-151">Test the function</span></span>

1. <span data-ttu-id="37f2c-152">GitHub 리포지토리에서 **문제** 탭을 새 브라우저 창에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="37f2c-153">새 창에서 **새 문제**를 클릭하고 제목을 입력한 다음 **새 문제 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="37f2c-154">문제에 주석을 입력하고 **주석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-154">In the issue, type a comment and click **Comment**.</span></span>

    ![GitHub 문제 주석을 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="37f2c-156">포털로 돌아가 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="37f2c-157">새 주석 텍스트와 함께 추적 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-157">You should see a trace entry with the new comment text.</span></span>

     ![로그에서 주석 텍스트 보기.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="37f2c-159">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="37f2c-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="37f2c-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37f2c-160">Next steps</span></span>

<span data-ttu-id="37f2c-161">GitHub 웹후크에서 요청을 수신할 때 실행되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="37f2c-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="37f2c-162">웹후크 트리거에 대한 자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](functions-bindings-http-webhook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37f2c-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
