---
title: "Azure에서 큐 메시지에 의해 트리거되는 함수 만들기 | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure Storage 큐에 제출된 메시지에 의해 호출되는 서버를 사용하지 않는 함수를 만듭니다."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 57c59273a9da55f3e357764c522b444ae2d73cb5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a><span data-ttu-id="336ce-103">Functions를 사용하여 Azure Storage 큐에 메시지 추가</span><span class="sxs-lookup"><span data-stu-id="336ce-103">Add messages to an Azure Storage queue using Functions</span></span>

<span data-ttu-id="336ce-104">Azure Functions에서 입력 및 출력 바인딩은 함수에서 외부 서비스 데이터로 연결하기 위한 선언적 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-104">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="336ce-105">이 항목에서는 메시지를 Azure Queue Storage로 보내는 출력 바인딩을 추가하여 기존 함수를 업데이트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-105">In this topic, learn how to update an existing function by adding an output binding that sends messages to Azure Queue storage.</span></span>  

![로그에서 메시지 보기.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="336ce-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="336ce-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="336ce-108">[Microsoft Azure Storage Explorer](http://storageexplorer.com/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-108">Install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="336ce-109"><a name="add-binding"></a>출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="336ce-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="336ce-110">함수 앱과 함수를 모두 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="336ce-111">**통합** 및 **+ 새 출력**을 선택한 다음 **Azure Queue Storage**, **선택**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Queue Storage 출력 바인딩을 Azure Portal의 함수에 추가합니다.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="336ce-113">표에 지정된 대로 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-113">Use the settings as specified in the table:</span></span> 

    ![Queue Storage 출력 바인딩을 Azure Portal의 함수에 추가합니다.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="336ce-115">설정</span><span class="sxs-lookup"><span data-stu-id="336ce-115">Setting</span></span>      |  <span data-ttu-id="336ce-116">제안 값</span><span class="sxs-lookup"><span data-stu-id="336ce-116">Suggested value</span></span>   | <span data-ttu-id="336ce-117">설명</span><span class="sxs-lookup"><span data-stu-id="336ce-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="336ce-118">**큐 이름**</span><span class="sxs-lookup"><span data-stu-id="336ce-118">**Queue name**</span></span>   | <span data-ttu-id="336ce-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="336ce-119">myqueue-items</span></span>    | <span data-ttu-id="336ce-120">Storage 계정에서 연결할 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-120">The name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="336ce-121">**Storage 계정 연결**</span><span class="sxs-lookup"><span data-stu-id="336ce-121">**Storage account connection**</span></span> | <span data-ttu-id="336ce-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="336ce-122">AzureWebJobStorage</span></span> | <span data-ttu-id="336ce-123">함수 앱에 이미 사용된 저장소 계정 연결을 사용하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-123">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="336ce-124">**메시지 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="336ce-124">**Message parameter name**</span></span> | <span data-ttu-id="336ce-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="336ce-125">outputQueueItem</span></span> | <span data-ttu-id="336ce-126">출력 바인딩 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-126">The name of the output binding parameter.</span></span> | 

4. <span data-ttu-id="336ce-127">**저장**을 클릭하여 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-127">Click **Save** to add the binding.</span></span>
 
<span data-ttu-id="336ce-128">이제 출력 바인딩이 정의되었고 큐에 메시지를 추가할 바인딩을 사용하도록 코드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-128">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span></span>  

## <a name="update-the-function-code"></a><span data-ttu-id="336ce-129">함수 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="336ce-129">Update the function code</span></span>

1. <span data-ttu-id="336ce-130">편집기에서 함수 코드를 표시할 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-130">Select your function to display the function code in the editor.</span></span> 

2. <span data-ttu-id="336ce-131">C# 함수의 경우 **outputQueueItem** 저장소 바인딩 매개 변수를 추가하기 위해 함수 정의를 다음과 같이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-131">For a C# function, update your function definition as follows to add the **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="336ce-132">JavaScript 함수에 대해서는 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="336ce-133">메서드가 반환하기 직전에 함수에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-133">Add the following code to the function just before the method returns.</span></span> <span data-ttu-id="336ce-134">함수의 언어에 대해 적절한 코드 조각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-134">Use the appropriate snippet for the language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed to the function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed to the function: " + name);     
    ```

4. <span data-ttu-id="336ce-135">**저장**을 선택하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-135">Select **Save** to save changes.</span></span>

<span data-ttu-id="336ce-136">HTTP 트리거에 전달된 값은 큐에 추가된 메시지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-136">The value passed to the HTTP trigger is included in a message added to the queue.</span></span>
 
## <a name="test-the-function"></a><span data-ttu-id="336ce-137">함수 테스트</span><span class="sxs-lookup"><span data-stu-id="336ce-137">Test the function</span></span> 

1. <span data-ttu-id="336ce-138">코드 변경 내용이 저장된 후 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-138">After the code changes are saved, select **Run**.</span></span> 

    ![Queue Storage 출력 바인딩을 Azure Portal의 함수에 추가합니다.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="336ce-140">로그에서 함수가 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-140">Check the logs to make sure that the function succeeded.</span></span> <span data-ttu-id="336ce-141">**outqueue**라는 새 큐는 출력 바인딩이 처음 사용될 때 함수 런타임에 의해 Storage 계정에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-141">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span></span>

<span data-ttu-id="336ce-142">다음으로 새 큐와 여기에 추가한 메시지를 확인하기 위해 저장소 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-142">Next, you can connect to your storage account to verify the new queue and the message you added to it.</span></span> 

## <a name="connect-to-the-queue"></a><span data-ttu-id="336ce-143">큐에 연결</span><span class="sxs-lookup"><span data-stu-id="336ce-143">Connect to the queue</span></span>

<span data-ttu-id="336ce-144">Storage 탐색기를 이미 설치했고 저장소 계정에 연결한 경우 처음 세 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-144">Skip the first three steps if you have already installed Storage Explorer and connected it to your storage account.</span></span>    

1. <span data-ttu-id="336ce-145">함수에서 **통합** 및 새 **Azure Queue Storage** 출력 바인딩을 선택한 후 **설명서**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-145">In your function, choose **Integrate** and the new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="336ce-146">**계정 이름** 및 **계정 키**를 모두 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="336ce-147">이러한 자격 증명을 사용하여 저장소 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-147">You use these credentials to connect to the storage account.</span></span>
 
    ![Storage 계정 연결 자격 증명 가져오기.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="336ce-149">[Microsoft Azure Storage Explorer](http://storageexplorer.com/) 도구를 실행하고 왼쪽의 연결 아이콘을 선택하고 **저장소 계정 이름 및 키 사용**을 선택하고 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-149">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Storage 계정 탐색기 도구 실행.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="336ce-151">1단계에서 복사한 **계정 이름** 및 **계정 키**를 해당 필드에 붙여 넣은 다음, **다음**, **연결**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-151">Paste the **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![저장소 자격 증명을 붙여 넣고 연결합니다.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="336ce-153">연결된 저장소 계정을 확장하고 **큐**를 확장하고 **myqueue-items**라는 큐가 존재하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-153">Expand the attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="336ce-154">큐에 이미 있는 메시지도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-154">You should also see a message already in the queue.</span></span>  
 
    ![저장소 큐 만들기.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="336ce-156">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="336ce-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="336ce-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="336ce-157">Next steps</span></span>

<span data-ttu-id="336ce-158">기존 함수에 출력 바인딩을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="336ce-158">You have added an output binding to an existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="336ce-159">Queue Storage에 바인딩에 대한 자세한 내용은 [Azure Functions Storage 큐 바인딩](functions-bindings-storage-queue.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="336ce-159">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



