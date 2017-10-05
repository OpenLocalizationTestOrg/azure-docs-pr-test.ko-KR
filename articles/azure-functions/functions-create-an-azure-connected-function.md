---
title: "Azure 서비스에 연결하는 함수 만들기 | Microsoft Docs"
description: "다른 Azure 서비스에 연결하는 서버가 없는 응용 프로그램을 만들려면 Azure Functions를 사용합니다."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="b65d6-104">다른 Azure 서비스에 연결하는 함수를 만들려면 Azure Functions를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="b65d6-105">이 항목에서는 Azure Storage 큐의 메시지를 수신 대기하고 Azure Storage 테이블에 그 메시지를 복사하는 Azure Functions에서 함수 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="b65d6-106">메시지를 큐에 로드하는 데 타이머 트리거 함수가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="b65d6-107">두 번째 함수는 큐에서 메시지를 읽어 와서 테이블에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="b65d6-108">바인딩 정의를 기반으로 Azure Functions가 사용자에 대한 큐와 테이블을 모두 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="b65d6-109">좀더 흥미로운 학습을 위해 한 함수는 JavaScript로 다른 함수는 C# 스크립트로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="b65d6-110">여기서는 함수 앱이 다양한 언어로 된 함수를 포함하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="b65d6-111">[채널 9의 비디오](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)에서 설명된 이 시나리오를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="b65d6-112">큐에 기록할 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="b65d6-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="b65d6-113">저장소 큐에 연결하려면 먼저 메시지 큐를 로드하는 함수를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="b65d6-114">이 JavaScript 함수는 10초마다 메시지를 큐에 기록하는 타이머 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="b65d6-115">Azure 계정이 없는 경우 [Azure Functions 사용](https://functions.azure.com/try) 환경을 확인하거나 [무료 Azure 계정을 만드세요](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b65d6-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="b65d6-116">Azure Portal로 이동하여 함수 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="b65d6-117">**새 함수** > **TimerTrigger-JavaScript**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="b65d6-118">함수의 이름을 **FunctionsBindingsDemo1**로 지정하고 **일정**에 대한 `0/10 * * * * *` 식 값을 입력한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![타이머 트리거 함수 추가](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="b65d6-120">이제 10초마다 실행되는 타이머 트리거 함수가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="b65d6-121">**개발** 탭에서 **로그**를 클릭하고 로그에 있는 활동을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="b65d6-122">10초마다 기록된 로그 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-122">You see a log entry written every 10 seconds.</span></span>
   
    ![로그를 확인하여 함수가 작동하는지 확인](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="b65d6-124">메시지 큐 출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="b65d6-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="b65d6-125">**통합** 탭에서 **새 출력** > **Azure Queue Storage** > **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![트리거 타이머 함수 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="b65d6-127">**메시지 매개 변수 이름**에 대해 `myQueueItem`을, **큐 이름**에 대해 `functions-bindings`를 입력하고 기존 **Storage 계정 연결**을 선택하거나 **새로 만들기**를 클릭하여 저장소 계정 연결을 만든 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![저장소 큐에 출력 바인딩 만들기](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="b65d6-129">다시 **개발** 탭으로 돌아가 함수에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="b65d6-130">함수의 줄 9 주위에서 *if* 문을 찾고 해당 문 뒤에 다음 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="b65d6-131">이 코드는 **myQueueItem**을 만들고 **시간** 속성을 현재 timeStamp로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="b65d6-132">그런 다음 새 큐 항목을 컨텍스트의 **myQueueItem** 바인딩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="b65d6-133">**저장 및 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="b65d6-134">Storage 탐색기를 사용하여 저장소 업데이트 보기</span><span class="sxs-lookup"><span data-stu-id="b65d6-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="b65d6-135">생성한 큐에서 메시지를 확인하여 함수가 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="b65d6-136">Visual Studio에서 클라우드 탐색기를 사용하여 저장소 큐에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="b65d6-137">그러나 포털에서 Microsoft Azure Storage 탐색기를 사용하면 저장소 계정에 쉽게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="b65d6-138">**통합** 탭에서 큐 출력 바인딩 > **설명서**를 클릭한 후 저장소 계정에 대한 연결 문자열을 표시하고 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="b65d6-139">이 값을 사용하여 저장소 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-139">You use this value to connect to your storage account.</span></span>

    ![Azure Storage 탐색기 다운로드](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="b65d6-141">아직 설치하지 않은 경우 [Microsoft Azure Storage 탐색기](http://storageexplorer.com)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="b65d6-142">Storage 탐색기에서 Azure Storage에 연결 아이콘을 클릭하고 필드에 연결 문자열을 붙여 넣고 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Storage 탐색기에서 연결 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="b65d6-144">**로컬 및 연결된** 아래에서 **Storage 계정** > 저장소 계정 > **큐** > **functions-bindings**를 확장하고 해당 메시지가 큐에 기록되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![큐에서 메시지 보기](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="b65d6-146">큐가 존재하지 않거나 비어 있는 경우 함수 바인딩 또는 코드에 문제가 있을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="b65d6-147">큐에서 읽어 오는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="b65d6-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="b65d6-148">이제 큐에 메시지가 추가되었고 큐에서 읽어 오는 다른 함수를 만들어 메시지를 Azure Storage 테이블에 영구적으로 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="b65d6-149">**새 함수** > **QueueTrigger-CSharp**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="b65d6-150">함수의 이름을 `FunctionsBindingsDemo2`로 지정하고 **큐 이름** 필드에 **functions-bindings**를 입력하고 기존의 저장소 계정을 선택하거나 만든 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![출력 큐 타이머 함수 추가](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="b65d6-152">(선택 사항) 이전처럼 Storage 탐색기에서 새로운 큐를 확인하여 새 함수가 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="b65d6-153">또한 Visual Studio에서 클라우드 탐색기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="b65d6-154">(선택 사항) **functions-bindings** 큐를 새로 고치고 큐에서 해당 항목이 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="b65d6-155">입력 트리거 및 함수가 큐를 읽어 오면서 함수가 **functions-bindings** 큐에 바인딩되므로 제거가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="b65d6-156">테이블 출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="b65d6-156">Add a table output binding</span></span>

1. <span data-ttu-id="b65d6-157">FunctionsBindingsDemo2에서 **통합** > **새 출력** > **Azure Table Storage** > **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![바인딩을 Azure Storage 테이블에 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="b65d6-159">**테이블 이름**으로 `functionbindings`을, **테이블 매개 변수 이름**으로 `myTable`를 입력하고 **Storage 계정 연결**을 선택하거나 새로 만든 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Storage 테이블 바인딩 구성](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="b65d6-161">**개발** 탭에서 기존 함수 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="b65d6-162">**TableItem** 클래스는 저장소 테이블에서 행을 나타내며 **TableItem** 개체의 `myTable` 컬렉션에 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="b65d6-163">테이블에 삽입할 수 있도록 **PartitionKey** 및 **RowKey** 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="b65d6-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-164">Click **Save**.</span></span>  <span data-ttu-id="b65d6-165">마지막으로, Storage 탐색기 또는 Visual Studio 클라우드 탐색기에서 테이블을 확인하여 함수가 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="b65d6-166">(선택 사항) 저장소 탐색기의 저장소 계정에서 **테이블** > **functionsbindings**를 확장하고 테이블에 행이 추가된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="b65d6-167">Visual Studio의 클라우드 탐색기에서 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![테이블의 행 보기](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="b65d6-169">테이블이 존재하지 않거나 비어 있는 경우 함수 바인딩 또는 코드에 문제가 있을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="b65d6-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b65d6-170">Next steps</span></span>
<span data-ttu-id="b65d6-171">Azure Functions에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b65d6-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="b65d6-172">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="b65d6-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="b65d6-173">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="b65d6-174">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="b65d6-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="b65d6-175">함수를 테스트하는 다양한 도구와 기법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="b65d6-176">Azure Functions 크기 조정 방법</span><span class="sxs-lookup"><span data-stu-id="b65d6-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="b65d6-177">소비 호스팅 요금제, 올바른 요금제 선택 방법을 포함하여 Azure Functions에서 사용 가능한 서비스 요금제에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b65d6-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

