---
title: "GitHub webhook에 의해 트리거되는 Azure에서 함수 aaaCreate | Microsoft Docs"
description: "Azure 함수 toocreate GitHub webhook 호출 하는 서버가 없는 함수를 사용 합니다."
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
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="35d82-103">GitHub webhook를 통해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="35d82-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="35d82-104">자세한 내용은 방법 toocreate GitHub 특정 페이로드를 사용한 HTTP webhook 요청에 의해 트리거되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook hello Azure 포털에서에서 함수를 트리거](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="35d82-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="35d82-106">Prerequisites</span></span>

+ <span data-ttu-id="35d82-107">하나 이상의 프로젝트와 함께 GitHub 계정.</span><span class="sxs-lookup"><span data-stu-id="35d82-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="35d82-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="35d82-108">An Azure subscription.</span></span> <span data-ttu-id="35d82-109">구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="35d82-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="35d82-110">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="35d82-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="35d82-112">다음으로 hello 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="35d82-113">GitHub 웹후크 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="35d82-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="35d82-114">함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="35d82-115">Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="35d82-116">이 함수 템플릿의 hello 전체 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-116">This displays hello complete set of function templates.</span></span>

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="35d82-118">선택 hello **GitHub WebHook** 원하는 언어에 대 한 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="35d82-119">**함수 이름을 지정한** 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-119">**Name your function**, then select **Create**.</span></span>

     ![Hello Azure 포털에서에서 새 GitHub 트리거되는 webhook 함수 만들기](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="35d82-121">클릭 하 여 새 함수에 **<> / Get 함수 URL**, 복사 및 hello 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="35d82-122">동일한 작업에 대 한 hello 마십시오 **<> / 가져오기 GitHub 비밀**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="35d82-123">GitHub에서 이러한 값 tooconfigure hello webhook을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Hello 함수 코드를 검토 합니다.](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="35d82-125">다음으로 GitHub 리포지토리에 webhook를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="35d82-126">Hello webhook 구성</span><span class="sxs-lookup"><span data-stu-id="35d82-126">Configure hello webhook</span></span>

1. <span data-ttu-id="35d82-127">Github를 소유 하 고 있는 tooa 저장소를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="35d82-128">분기된 모든 리포지토리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="35d82-129">사용 하 여 저장소 toofork 해야 할 경우 <https://github.com/Azure-Samples/functions-quickstart>합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="35d82-130">**설정**, **Webhooks**, **webhook 추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![GitHub 웹후크를 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="35d82-132">Hello 테이블에 지정 된 설정을 사용 하 고 클릭 **webhook 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Webhook URL에 hello 및 암호를 설정 합니다.](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="35d82-134">설정</span><span class="sxs-lookup"><span data-stu-id="35d82-134">Setting</span></span> | <span data-ttu-id="35d82-135">제안 값</span><span class="sxs-lookup"><span data-stu-id="35d82-135">Suggested value</span></span> | <span data-ttu-id="35d82-136">설명</span><span class="sxs-lookup"><span data-stu-id="35d82-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="35d82-137">**페이로드 URL**</span><span class="sxs-lookup"><span data-stu-id="35d82-137">**Payload URL**</span></span> | <span data-ttu-id="35d82-138">복사된 값</span><span class="sxs-lookup"><span data-stu-id="35d82-138">Copied value</span></span> | <span data-ttu-id="35d82-139">반환 하는 hello 값을 사용 하 여 **<> / Get 함수 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="35d82-140">**비밀**</span><span class="sxs-lookup"><span data-stu-id="35d82-140">**Secret**</span></span>   | <span data-ttu-id="35d82-141">복사된 값</span><span class="sxs-lookup"><span data-stu-id="35d82-141">Copied value</span></span> | <span data-ttu-id="35d82-142">반환 하는 hello 값을 사용 하 여 **<> / 가져오기 GitHub 비밀**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="35d82-143">**콘텐츠 형식**</span><span class="sxs-lookup"><span data-stu-id="35d82-143">**Content type**</span></span> | <span data-ttu-id="35d82-144">application/json</span><span class="sxs-lookup"><span data-stu-id="35d82-144">application/json</span></span> | <span data-ttu-id="35d82-145">hello 함수는 JSON 페이로드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="35d82-146">이벤트 트리거</span><span class="sxs-lookup"><span data-stu-id="35d82-146">Event triggers</span></span> | <span data-ttu-id="35d82-147">개별 이벤트를 선택하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-147">Let me select individual events</span></span> | <span data-ttu-id="35d82-148">Tootrigger 문제 메모 이벤트에만 포함 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="35d82-149">문제 주석</span><span class="sxs-lookup"><span data-stu-id="35d82-149">Issue comment</span></span> |  |

<span data-ttu-id="35d82-150">이제 webhook hello 새 문제 메모 추가 될 때 구성 된 tootrigger 함수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="35d82-151">테스트 hello 함수</span><span class="sxs-lookup"><span data-stu-id="35d82-151">Test hello function</span></span>

1. <span data-ttu-id="35d82-152">GitHub 리포지토리에 hello를 열고 **문제** 새 브라우저 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="35d82-153">Hello 새 창에서 클릭 **새 문제**, 제목을 입력 하 고 클릭 **새 문제를 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="35d82-154">Hello 문제에서 설명을 입력 하 고 클릭 **주석**합니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![GitHub 문제 주석을 추가합니다.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="35d82-156">Toohello 포털 돌아가서 hello 로그를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="35d82-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="35d82-157">Hello 새 주석 텍스트와 함께 추적 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-157">You should see a trace entry with hello new comment text.</span></span>

     ![Hello 로그에 hello 주석 텍스트를 봅니다.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="35d82-159">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="35d82-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="35d82-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35d82-160">Next steps</span></span>

<span data-ttu-id="35d82-161">GitHub 웹후크에서 요청을 수신할 때 실행되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="35d82-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="35d82-162">웹후크 트리거에 대한 자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](functions-bindings-http-webhook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35d82-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
