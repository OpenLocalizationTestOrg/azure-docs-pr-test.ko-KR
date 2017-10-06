---
title: "azure 큐 메시지에 의해 트리거되는 함수 aaaCreate | Microsoft Docs"
description: "메시지에서 호출 하는 서버가 없는 함수를 사용 하 여 Azure 함수 toocreate tooan Azure 저장소 큐를 제출 합니다."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="4eb2b-103">Azure Queue Storage에 의해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb2b-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="4eb2b-104">메시지는 경우에 발생 하는 함수 toocreate tooan Azure 저장소 큐를 전송 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="4eb2b-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4eb2b-106">Prerequisites</span></span>

- <span data-ttu-id="4eb2b-107">다운로드 및 설치 hello [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="4eb2b-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-108">An Azure subscription.</span></span> <span data-ttu-id="4eb2b-109">구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="4eb2b-110">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb2b-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="4eb2b-112">다음으로 hello 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="4eb2b-113">큐 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb2b-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="4eb2b-114">함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="4eb2b-115">Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="4eb2b-116">이 함수 템플릿의 hello 전체 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-116">This displays hello complete set of function templates.</span></span>

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="4eb2b-118">선택 hello **QueueTrigger** 원하는 언어 및 hello 테이블에 지정 된 hello 설정 사용에 대 한 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Hello 저장소 큐 트리거된 함수를 만듭니다.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="4eb2b-120">설정</span><span class="sxs-lookup"><span data-stu-id="4eb2b-120">Setting</span></span> | <span data-ttu-id="4eb2b-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="4eb2b-121">Suggested value</span></span> | <span data-ttu-id="4eb2b-122">설명</span><span class="sxs-lookup"><span data-stu-id="4eb2b-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="4eb2b-123">**큐 이름**</span><span class="sxs-lookup"><span data-stu-id="4eb2b-123">**Queue name**</span></span>   | <span data-ttu-id="4eb2b-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="4eb2b-124">myqueue-items</span></span>    | <span data-ttu-id="4eb2b-125">Tooconnect tooin 저장소 계정의 큐 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="4eb2b-126">**Storage 계정 연결**</span><span class="sxs-lookup"><span data-stu-id="4eb2b-126">**Storage account connection**</span></span> | <span data-ttu-id="4eb2b-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="4eb2b-127">AzureWebJobStorage</span></span> | <span data-ttu-id="4eb2b-128">Hello 함수 응용 프로그램에서 이미 사용 되는 저장소 계정 연결을 사용 하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="4eb2b-129">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="4eb2b-129">**Name your function**</span></span> | <span data-ttu-id="4eb2b-130">함수 앱에서 고유</span><span class="sxs-lookup"><span data-stu-id="4eb2b-130">Unique in your function app</span></span> | <span data-ttu-id="4eb2b-131">큐 트리거 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="4eb2b-132">클릭 **만들기** toocreate 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="4eb2b-133">다음으로 tooyour Azure 저장소 계정을 연결 하 고 hello 만들 **myqueue 항목** 저장소 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="4eb2b-134">Hello 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="4eb2b-134">Create hello queue</span></span>

1. <span data-ttu-id="4eb2b-135">함수에서 **통합**을 클릭하고 **설명서**를 확장하여 **계정 이름** 및 **계정 키**를 모두 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="4eb2b-136">이러한 자격 증명 tooconnect toohello 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="4eb2b-137">저장소 계정에 이미 연결한 경우 toostep 4를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Hello 저장소 계정 연결 자격 증명을 가져옵니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="4eb2b-139">v</span><span class="sxs-lookup"><span data-stu-id="4eb2b-139">v</span></span>

1. <span data-ttu-id="4eb2b-140">Hello 실행 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/) 도구를 hello 클릭 연결 hello 왼쪽에 있는 아이콘을 선택 **저장소 계정 이름과 키를 사용 하 여**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Hello 저장소 계정 탐색기 도구를 실행 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="4eb2b-142">Hello 입력 **계정 이름** 및 **계정 키** 1 단계에서 클릭 **다음** 차례로 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Hello 저장소 자격 증명을 입력 하 고 연결 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="4eb2b-144">Hello 연결 된 저장소 계정, 마우스 오른쪽 단추로 클릭 **큐**, 클릭 **만들기 큐**, 형식 `myqueue-items`, enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![저장소 큐 만들기.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="4eb2b-146">저장소 큐를가지고 메시지 toohello 큐를 추가 하 여 hello 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="4eb2b-147">테스트 hello 함수</span><span class="sxs-lookup"><span data-stu-id="4eb2b-147">Test hello function</span></span>

1. <span data-ttu-id="4eb2b-148">Hello Azure 포털에 다시 찾아보기 tooyour 함수 확장 hello **로그** hello 있는지 확인 하 고 hello 페이지 맨 아래에 해당 로그 스트리밍 없는 일시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="4eb2b-149">Storage 탐색기에서 저장소 계정, **큐** 및 **myqueue-items**를 확장한 후 **메시지 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![메시지 toohello 큐를 추가 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="4eb2b-151">"Hello World!"</span><span class="sxs-lookup"><span data-stu-id="4eb2b-151">Type your "Hello World!"</span></span> <span data-ttu-id="4eb2b-152">메시지를 **메시지 텍스트**에 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="4eb2b-153">몇 초 동안 기다립니다 다음 tooyour 기능 로그를 다시 이동 하 고 hello 큐에서 읽은 hello 새 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="4eb2b-155">저장소 탐색기에서 다시 클릭 **새로 고침** 처리가 hello 메시지를 확인 하는 더 이상 hello 큐에 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4eb2b-156">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="4eb2b-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="4eb2b-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4eb2b-157">Next steps</span></span>

<span data-ttu-id="4eb2b-158">메시지가 tooa 저장소 큐 추가 될 때 실행 되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="4eb2b-159">Queue Storage 트리거에 대한 자세한 내용은 [Azure Functions Storage 큐 바인딩](functions-bindings-storage-queue.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4eb2b-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>