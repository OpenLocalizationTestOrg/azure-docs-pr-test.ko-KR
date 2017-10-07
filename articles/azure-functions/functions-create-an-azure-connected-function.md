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
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Azure 함수 toocreate tooother Azure에 연결 하는 함수를 사용 하 여 서비스

이 항목에서는 toocreate toomessages Azure 저장소 큐 및 복사본 hello에서 수신 대기 하는 Azure 함수에서 함수는 Azure 저장소 테이블에 toorows 메시지 하는 방법을 보여 줍니다. 타이머 트리거 함수 hello 큐에 사용 되는 tooload 메시지입니다. 두 번째 함수는 hello 큐에서 읽고 메시지 toohello 테이블을 씁니다. Hello 큐와 hello 테이블 모두 드립니다 hello 바인딩 정의에 따라 Azure 함수에 의해 생성 됩니다. 

더 흥미로운 toomake 항목을 하나의 함수는 JavaScript로 작성 된 및 다른 hello C# 스크립트에 기록 됩니다. 여기서는 함수 앱이 다양한 언어로 된 함수를 포함하는 방식을 보여 줍니다. 

[채널 9의 비디오](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)에서 설명된 이 시나리오를 볼 수 있습니다.

## <a name="create-a-function-that-writes-toohello-queue"></a>Toohello 큐에 기록 하는 함수를 만듭니다

Tooa 저장소 큐를 연결할 수 있습니다, 전에 toocreate hello 메시지 큐를 로드 하는 함수 해야 합니다. 이 JavaScript 함수 메시지 toohello 큐를 10 초 마다 기록 하는 타이머 트리거를 사용 합니다. Azure 계정이 없는 경우 hello를 확인해 [Azure 함수 시도](https://functions.azure.com/try) 하세요 또는 [무료 Azure 계정 만들기](https://azure.microsoft.com/free/)합니다.

1. Azure 포털 toohello 이동한 함수 응용 프로그램을 찾습니다.

2. **새 함수** > **TimerTrigger-JavaScript**를 클릭합니다. 

3. Hello 함수 이름을 **FunctionsBindingsDemo1**, cron 식 값을 입력 `0/10 * * * * *` 에 대 한 **일정**, 클릭 하 고 **만들기**합니다.
   
    ![타이머 트리거 함수 추가](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    이제 10초마다 실행되는 타이머 트리거 함수가 생성되었습니다.

5. Hello에 **개발** 탭을 클릭 **로그** hello 로그의 hello 활동을 표시 합니다. 10초마다 기록된 로그 항목이 표시됩니다.
   
    ![보기 hello 로그 tooverify hello 함수 작동](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>메시지 큐 출력 바인딩 추가

1. Hello에 **통합** 탭에서 선택 **새 출력** > **Azure 큐 저장소** > **선택**합니다.

    ![트리거 타이머 함수 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. 입력 `myQueueItem` 에 대 한 **메시지 매개 변수 이름** 및 `functions-bindings` 에 대 한 **큐 이름**, 기존 선택 **저장소 계정 연결** 키를누르거나**새** toocreate 저장소 계정 연결을 하 고 클릭 **저장**합니다.  

    ![Hello 출력 바인딩 toohello 저장소 큐 만들기](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Hello에 다시 **개발** 탭, 코드 toohello 함수 다음 hello 추가:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Hello 찾을 *경우* 문을 약 9 hello 함수를 입력 하 고 해당 문 다음에 삽입 hello 다음 코드입니다.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    이 코드에서는 **myQueueItem** 설정 하 고 해당 **시간** 속성 toohello 현재 타임 스탬프입니다. 그런 다음 hello 새 큐 항목 toohello 컨텍스트의 추가 **myQueueItem** 바인딩.

3. **저장 및 실행**을 클릭합니다.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Storage 탐색기를 사용하여 저장소 업데이트 보기
함수가 만든 hello 큐에 메시지를 확인 하 여 작동 하는지 확인할 수 있습니다.  Visual Studio에서 클라우드 탐색기를 사용 하 여 tooyour 저장소 큐를 연결할 수 있습니다. 그러나 hello 포털 사용 하면 쉽게 tooconnect tooyour 저장소 계정을 Microsoft Azure 저장소 탐색기를 사용 하 여 합니다.

1. Hello에 **통합** 탭을 클릭 하 여 큐 출력 바인딩이 > **설명서**다음 저장소 계정에 대 한 연결 문자열 hello 숨기기를 취소 하 고 hello 값을 복사 합니다. 이 값 tooconnect tooyour 저장소 계정을 사용합니다.

    ![Azure Storage 탐색기 다운로드](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. 아직 설치하지 않은 경우 [Microsoft Azure Storage 탐색기](http://storageexplorer.com)를 다운로드하여 설치합니다. 
 
3. 저장소 탐색기를 클릭 hello 연결 tooAzure 저장소 아이콘 hello 연결 문자열 hello 필드에 붙여넣고 hello 마법사를 완료 합니다.

    ![Storage 탐색기에서 연결 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. **로컬 및 연결 된**를 확장 하 고 **저장소 계정은** > 저장소 계정 > **큐** > **함수-바인딩**toohello 큐 메시지 내용이 기록 되도록 확인 합니다.

    ![Hello 큐의 메시지 뷰](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Hello 큐 존재 하지 않는 비어 경우 대개는 문제가 있습니다 함수 바인딩 또는 코드입니다.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Hello 큐에서 읽는 함수 만들기

Toohello 큐에 추가 되는 메시지를가지고 hello 큐에서 읽을 수 있는 다른 함수를 만들 수 있습니다 및 쓰기 hello 메시지를 영구적으로 tooan Azure 저장소 테이블입니다.

1. **새 함수** > **QueueTrigger-CSharp**를 클릭합니다. 
 
2. Hello 함수 이름을 `FunctionsBindingsDemo2`, 입력 **함수 바인딩** hello에 **큐 이름** 필드를 기존 저장소 계정을 선택 하거나 하나를 만들고 클릭 **만들기**.

    ![출력 큐 타이머 함수 추가](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (선택 사항) 새 함수 hello 하기 전에 저장소 탐색기에 hello 새 큐를 확인 하 여 작동 하는지 확인할 수 있습니다. 또한 Visual Studio에서 클라우드 탐색기를 사용할 수도 있습니다.  

4. (선택 사항) Hello 새로 고침 **함수 바인딩** 큐를 항목 hello 큐에서 제거 했습니다. hello 제거 하기 때문에 발생 hello 함수는 바인딩된 toohello **함수 바인딩** 입력된 트리거와 hello 함수 hello 큐를 읽고 큐에 대기 합니다. 
 
## <a name="add-a-table-output-binding"></a>테이블 출력 바인딩 추가

1. FunctionsBindingsDemo2에서 **통합** > **새 출력** > **Azure Table Storage** > **선택**을 클릭합니다.

    ![바인딩 tooan Azure 저장소 테이블 추가](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. **테이블 이름**으로 `functionbindings`을, **테이블 매개 변수 이름**으로 `myTable`를 입력하고 **Storage 계정 연결**을 선택하거나 새로 만든 후 **저장**을 클릭합니다.

    ![Hello 저장소 테이블 바인딩 구성](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. Hello에 **개발** 탭에서 함수 코드를 기존 hello hello 다음 코드로 바꿉니다.
   
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
    hello **TableItem** 클래스 hello 저장소 테이블의 행을 나타내며 hello 항목 toohello 추가 `myTable` 컬렉션 **TableItem** 개체입니다. Hello를 설정 해야 **PartitionKey** 및 **RowKey** hello 테이블로 toobe 수 tooinsert 속성입니다.

4. **Save**를 클릭합니다.  마지막으로, 저장소 탐색기 또는 Visual Studio 클라우드 탐색기에 hello 테이블을 확인 하 여 hello 함수 작동을 확인할 수 있습니다.

5. (선택 사항) 저장소 탐색기에서 저장소 계정에서 확장 **테이블** > **functionsbindings** 행 toohello 테이블을 추가 하 고 있는지 확인 합니다. 할 수 있는 Visual Studio에서 클라우드 탐색기에서 hello 동일 합니다.

    ![Hello 테이블의 행 보기](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Hello 테이블이 존재 하지 않는 비어 경우 대개는 문제가 있습니다 함수 바인딩 또는 코드. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>다음 단계
Azure 함수에 대 한 자세한 내용은 다음 항목 hello를 참조 하세요.

* [Azure Functions 개발자 참조](functions-reference.md)  
  함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.
* [Azure Functions 테스트](functions-test-a-function.md)  
  함수를 테스트하는 다양한 도구와 기법을 설명합니다.
* [어떻게 tooscale Azure 함수](functions-scale.md)  
  Hello 소비 호스팅 계획 및 toochoose 오른쪽 계획 hello 하는 방법을 비롯 한 Azure 기능을 사용할 수 있는 서비스 계획에 설명 합니다. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

