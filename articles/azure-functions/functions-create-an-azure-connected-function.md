---
title: "aaaCreate tooAzure 서비스를 연결 하는 함수 | Microsoft Docs"
description: "Azure 함수 toocreate tooother Azure에 연결 하는 서버가 없는 응용 프로그램을 사용 하 여 서비스입니다."
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
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="90529-104">Azure 함수 toocreate tooother Azure에 연결 하는 함수를 사용 하 여 서비스</span><span class="sxs-lookup"><span data-stu-id="90529-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="90529-105">이 항목에서는 toocreate toomessages Azure 저장소 큐 및 복사본 hello에서 수신 대기 하는 Azure 함수에서 함수는 Azure 저장소 테이블에 toorows 메시지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90529-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="90529-106">타이머 트리거 함수 hello 큐에 사용 되는 tooload 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="90529-107">두 번째 함수는 hello 큐에서 읽고 메시지 toohello 테이블을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="90529-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="90529-108">Hello 큐와 hello 테이블 모두 드립니다 hello 바인딩 정의에 따라 Azure 함수에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90529-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="90529-109">더 흥미로운 toomake 항목을 하나의 함수는 JavaScript로 작성 된 및 다른 hello C# 스크립트에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90529-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="90529-110">여기서는 함수 앱이 다양한 언어로 된 함수를 포함하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90529-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="90529-111">[채널 9의 비디오](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)에서 설명된 이 시나리오를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="90529-112">Toohello 큐에 기록 하는 함수를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="90529-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="90529-113">Tooa 저장소 큐를 연결할 수 있습니다, 전에 toocreate hello 메시지 큐를 로드 하는 함수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="90529-114">이 JavaScript 함수 메시지 toohello 큐를 10 초 마다 기록 하는 타이머 트리거를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="90529-115">Azure 계정이 없는 경우 hello를 확인해 [Azure 함수 시도](https://functions.azure.com/try) 하세요 또는 [무료 Azure 계정 만들기](https://azure.microsoft.com/free/)합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="90529-116">Azure 포털 toohello 이동한 함수 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="90529-117">**새 함수** > **TimerTrigger-JavaScript**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="90529-118">Hello 함수 이름을 **FunctionsBindingsDemo1**, cron 식 값을 입력 `0/10 * * * * *` 에 대 한 **일정**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![타이머 트리거 함수 추가](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="90529-120">이제 10초마다 실행되는 타이머 트리거 함수가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="90529-121">Hello에 **개발** 탭을 클릭 **로그** hello 로그의 hello 활동을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="90529-122">10초마다 기록된 로그 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90529-122">You see a log entry written every 10 seconds.</span></span>
   
    ![보기 hello 로그 tooverify hello 함수 작동](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="90529-124">메시지 큐 출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="90529-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="90529-125">Hello에 **통합** 탭에서 선택 **새 출력** > **Azure 큐 저장소** > **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![트리거 타이머 함수 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="90529-127">입력 `myQueueItem` 에 대 한 **메시지 매개 변수 이름** 및 `functions-bindings` 에 대 한 **큐 이름**, 기존 선택 **저장소 계정 연결** 키를누르거나**새** toocreate 저장소 계정 연결을 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Hello 출력 바인딩 toohello 저장소 큐 만들기](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="90529-129">Hello에 다시 **개발** 탭, 코드 toohello 함수 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="90529-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="90529-130">Hello 찾을 *경우* 문을 약 9 hello 함수를 입력 하 고 해당 문 다음에 삽입 hello 다음 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="90529-131">이 코드에서는 **myQueueItem** 설정 하 고 해당 **시간** 속성 toohello 현재 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="90529-132">그런 다음 hello 새 큐 항목 toohello 컨텍스트의 추가 **myQueueItem** 바인딩.</span><span class="sxs-lookup"><span data-stu-id="90529-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="90529-133">**저장 및 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="90529-134">Storage 탐색기를 사용하여 저장소 업데이트 보기</span><span class="sxs-lookup"><span data-stu-id="90529-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="90529-135">함수가 만든 hello 큐에 메시지를 확인 하 여 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="90529-136">Visual Studio에서 클라우드 탐색기를 사용 하 여 tooyour 저장소 큐를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="90529-137">그러나 hello 포털 사용 하면 쉽게 tooconnect tooyour 저장소 계정을 Microsoft Azure 저장소 탐색기를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="90529-138">Hello에 **통합** 탭을 클릭 하 여 큐 출력 바인딩이 > **설명서**다음 저장소 계정에 대 한 연결 문자열 hello 숨기기를 취소 하 고 hello 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="90529-139">이 값 tooconnect tooyour 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Azure Storage 탐색기 다운로드](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="90529-141">아직 설치하지 않은 경우 [Microsoft Azure Storage 탐색기](http://storageexplorer.com)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="90529-142">저장소 탐색기를 클릭 hello 연결 tooAzure 저장소 아이콘 hello 연결 문자열 hello 필드에 붙여넣고 hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Storage 탐색기에서 연결 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="90529-144">**로컬 및 연결 된**를 확장 하 고 **저장소 계정은** > 저장소 계정 > **큐** > **함수-바인딩**toohello 큐 메시지 내용이 기록 되도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Hello 큐의 메시지 뷰](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="90529-146">Hello 큐 존재 하지 않는 비어 경우 대개는 문제가 있습니다 함수 바인딩 또는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="90529-147">Hello 큐에서 읽는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="90529-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="90529-148">Toohello 큐에 추가 되는 메시지를가지고 hello 큐에서 읽을 수 있는 다른 함수를 만들 수 있습니다 및 쓰기 hello 메시지를 영구적으로 tooan Azure 저장소 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="90529-149">**새 함수** > **QueueTrigger-CSharp**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="90529-150">Hello 함수 이름을 `FunctionsBindingsDemo2`, 입력 **함수 바인딩** hello에 **큐 이름** 필드를 기존 저장소 계정을 선택 하거나 하나를 만들고 클릭 **만들기**.</span><span class="sxs-lookup"><span data-stu-id="90529-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![출력 큐 타이머 함수 추가](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="90529-152">(선택 사항) 새 함수 hello 하기 전에 저장소 탐색기에 hello 새 큐를 확인 하 여 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="90529-153">또한 Visual Studio에서 클라우드 탐색기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="90529-154">(선택 사항) Hello 새로 고침 **함수 바인딩** 큐를 항목 hello 큐에서 제거 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="90529-155">hello 제거 하기 때문에 발생 hello 함수는 바인딩된 toohello **함수 바인딩** 입력된 트리거와 hello 함수 hello 큐를 읽고 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="90529-156">테이블 출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="90529-156">Add a table output binding</span></span>

1. <span data-ttu-id="90529-157">FunctionsBindingsDemo2에서 **통합** > **새 출력** > **Azure Table Storage** > **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![바인딩 tooan Azure 저장소 테이블 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="90529-159">**테이블 이름**으로 `functionbindings`을, **테이블 매개 변수 이름**으로 `myTable`를 입력하고 **Storage 계정 연결**을 선택하거나 새로 만든 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Hello 저장소 테이블 바인딩 구성](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="90529-161">Hello에 **개발** 탭에서 함수 코드를 기존 hello hello 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90529-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
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
        
        // Add hello item toohello table binding collection.
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
    <span data-ttu-id="90529-162">hello **TableItem** 클래스 hello 저장소 테이블의 행을 나타내며 hello 항목 toohello 추가 `myTable` 컬렉션 **TableItem** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="90529-163">Hello를 설정 해야 **PartitionKey** 및 **RowKey** hello 테이블로 toobe 수 tooinsert 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="90529-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-164">Click **Save**.</span></span>  <span data-ttu-id="90529-165">마지막으로, 저장소 탐색기 또는 Visual Studio 클라우드 탐색기에 hello 테이블을 확인 하 여 hello 함수 작동을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90529-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="90529-166">(선택 사항) 저장소 탐색기에서 저장소 계정에서 확장 **테이블** > **functionsbindings** 행 toohello 테이블을 추가 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="90529-167">할 수 있는 Visual Studio에서 클라우드 탐색기에서 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Hello 테이블의 행 보기](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="90529-169">Hello 테이블이 존재 하지 않는 비어 경우 대개는 문제가 있습니다 함수 바인딩 또는 코드.</span><span class="sxs-lookup"><span data-stu-id="90529-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="90529-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90529-170">Next steps</span></span>
<span data-ttu-id="90529-171">Azure 함수에 대 한 자세한 내용은 다음 항목 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="90529-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="90529-172">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="90529-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="90529-173">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="90529-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="90529-174">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="90529-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="90529-175">함수를 테스트하는 다양한 도구와 기법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="90529-176">어떻게 tooscale Azure 함수</span><span class="sxs-lookup"><span data-stu-id="90529-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="90529-177">Hello 소비 호스팅 계획 및 toochoose 오른쪽 계획 hello 하는 방법을 비롯 한 Azure 기능을 사용할 수 있는 서비스 계획에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90529-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

