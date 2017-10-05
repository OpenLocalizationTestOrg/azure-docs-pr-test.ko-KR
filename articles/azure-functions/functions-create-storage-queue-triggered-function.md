---
title: "Azure에서 큐 메시지에 의해 트리거되는 함수 만들기 | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure Storage 큐에 제출된 메시지에 의해 호출되는 서버를 사용하지 않는 함수를 만듭니다."
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="449de-103">Azure Queue Storage에 의해 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="449de-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="449de-104">Azure Storage 큐에 메시지가 제출될 때 트리거되는 함수를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="449de-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![로그에서 메시지 보기.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="449de-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="449de-106">Prerequisites</span></span>

- <span data-ttu-id="449de-107">[Microsoft Azure Storage 탐색기](http://storageexplorer.com/)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="449de-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="449de-108">An Azure subscription.</span></span> <span data-ttu-id="449de-109">구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="449de-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="449de-110">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="449de-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="449de-112">다음으로 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="449de-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="449de-113">큐 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="449de-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="449de-114">함수 앱을 확장한 후 **함수** 옆의 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="449de-115">함수 앱에서 첫 번째 함수이면 **사용자 지정 함수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="449de-116">그러면 함수 템플릿의 전체 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="449de-116">This displays the complete set of function templates.</span></span>

    ![Azure Portal에서 함수 빨리 시작하기 페이지](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="449de-118">원하는 언어에 해당하는 **QueueTrigger** 템플릿을 선택하고 테이블에 지정된 대로 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![저장소 큐 트리거 함수 만들기.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="449de-120">설정</span><span class="sxs-lookup"><span data-stu-id="449de-120">Setting</span></span> | <span data-ttu-id="449de-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="449de-121">Suggested value</span></span> | <span data-ttu-id="449de-122">설명</span><span class="sxs-lookup"><span data-stu-id="449de-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="449de-123">**큐 이름**</span><span class="sxs-lookup"><span data-stu-id="449de-123">**Queue name**</span></span>   | <span data-ttu-id="449de-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="449de-124">myqueue-items</span></span>    | <span data-ttu-id="449de-125">저장소 계정에서 연결할 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="449de-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="449de-126">**저장소 계정 연결**</span><span class="sxs-lookup"><span data-stu-id="449de-126">**Storage account connection**</span></span> | <span data-ttu-id="449de-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="449de-127">AzureWebJobStorage</span></span> | <span data-ttu-id="449de-128">함수 앱에 이미 사용된 저장소 계정 연결을 사용하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="449de-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="449de-129">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="449de-129">**Name your function**</span></span> | <span data-ttu-id="449de-130">함수 앱에서 고유</span><span class="sxs-lookup"><span data-stu-id="449de-130">Unique in your function app</span></span> | <span data-ttu-id="449de-131">큐 트리거 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="449de-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="449de-132">**만들기**를 클릭하여 사용자의 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="449de-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="449de-133">다음으로 Azure Storage 계정에 연결하고 **myqueue-items** 저장소 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="449de-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="449de-134">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="449de-134">Create the queue</span></span>

1. <span data-ttu-id="449de-135">함수에서 **통합**을 클릭하고 **설명서**를 확장하여 **계정 이름** 및 **계정 키**를 모두 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="449de-136">이러한 자격 증명을 사용하여 저장소 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="449de-137">저장소 계정에 이미 연결된 경우 4단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="449de-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![저장소 계정 연결 자격 증명 가져오기.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="449de-139">v</span><span class="sxs-lookup"><span data-stu-id="449de-139">v</span></span>

1. <span data-ttu-id="449de-140">[Microsoft Azure Storage 탐색기](http://storageexplorer.com/) 도구를 실행하고 왼쪽의 연결 아이콘을 클릭하고 **저장소 계정 이름 및 키 사용**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![저장소 계정 탐색기 도구 실행.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="449de-142">1단계에서 **계정 이름** 및 **계정 키**를 입력하고 **다음**을 클릭한 후 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![저장소 자격 증명 입력 및 연결.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="449de-144">연결된 저장소 계정을 확장하고 **큐**를 마우스 오른쪽 단추로 클릭하고 **큐 만들기**를 클릭하고 `myqueue-items`를 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="449de-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![저장소 큐 만들기.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="449de-146">이제 저장소 큐가 있고 메시지를 큐에 추가하여 함수를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="449de-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="449de-147">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="449de-147">Test the function</span></span>

1. <span data-ttu-id="449de-148">Azure Portal로 돌아가서 함수를 찾은 후 페이지 맨 아래에 있는 **로그**를 확장하고 로그 스트리밍이 일시 중지되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="449de-149">Storage 탐색기에서 저장소 계정, **큐** 및 **myqueue-items**를 확장한 후 **메시지 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![큐에 메시지 추가.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="449de-151">"Hello World!"</span><span class="sxs-lookup"><span data-stu-id="449de-151">Type your "Hello World!"</span></span> <span data-ttu-id="449de-152">메시지를 **메시지 텍스트**에 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="449de-153">몇 초 동안 기다린 다음 함수 로그로 돌아가서 새 메시지를 큐에서 읽었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![로그에서 메시지 보기.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="449de-155">Storage 탐색기로 돌아가 **새로 고침**을 클릭하고 메시지가 처리되고 더 이상 큐에 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="449de-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="449de-156">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="449de-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="449de-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="449de-157">Next steps</span></span>

<span data-ttu-id="449de-158">저장소 큐에 메시지가 추가될 때 실행되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="449de-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="449de-159">Queue Storage 트리거에 대한 자세한 내용은 [Azure Functions Storage 큐 바인딩](functions-bindings-storage-queue.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="449de-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>