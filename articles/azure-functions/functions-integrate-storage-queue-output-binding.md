---
title: "azure 큐 메시지에 의해 트리거되는 함수 aaaCreate | Microsoft Docs"
description: "메시지에서 호출 하는 서버가 없는 함수를 사용 하 여 Azure 함수 toocreate tooan Azure 저장소 큐를 제출 합니다."
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
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>함수를 사용 하 여 메시지 tooan Azure 저장소 큐를 추가 합니다.

Azure 기능 입력 및 출력 바인딩은 함수에서 선언적으로 tooconnect tooexternal 서비스 데이터를 제공합니다. 이 항목에서는 tooupdate 바인딩에 출력을 추가 하 여 기존 함수에서 보내는 방법을 메시지 tooAzure 큐 저장소를 설명 합니다.  

![Hello 로그 보기 메시지입니다.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>필수 조건 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Hello 설치 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

## <a name="add-binding"></a>출력 바인딩 추가
 
1. 함수 앱과 함수를 모두 확장합니다.

2. **통합** 및 **+ 새 출력**을 선택한 다음 **Azure Queue Storage**, **선택**을 차례로 선택합니다.
    
    ![큐 저장소 출력 바인딩 tooa 함수 hello Azure 포털에에서 추가 합니다.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Hello 테이블에 지정 된 hello 설정을 사용 합니다. 

    ![큐 저장소 출력 바인딩 tooa 함수 hello Azure 포털에에서 추가 합니다.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | 설정      |  제안 값   | 설명                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **큐 이름**   | myqueue-items    | hello의 hello 이름 tooconnect tooin을 저장소 계정의 큐입니다. |
    | **Storage 계정 연결** | AzureWebJobStorage | Hello 함수 응용 프로그램에서 이미 사용 되는 저장소 계정 연결을 사용 하거나 새로 만들 수 있습니다.  |
    | **메시지 매개 변수 이름** | outputQueueItem | 바인딩 매개 변수를 출력 하는 hello 이름 hello입니다. | 

4. 클릭 **저장** tooadd hello 바인딩.
 
출력 바인딩 정의가지고 tooupdate hello 코드 toouse hello 바인딩 tooadd 메시지 tooa 큐가 있어야 합니다.  

## <a name="update-hello-function-code"></a>Hello 함수 코드를 업데이트 합니다.

1. Hello 편집기 함수 toodisplay hello 함수 코드를 선택 합니다. 

2. C# 함수에 대 한 업데이트 tooadd hello를 다음과 같이 함수 정의 **outputQueueItem** 저장소 바인딩 매개 변수입니다. JavaScript 함수에 대해서는 이 단계를 건너뜁니다.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Hello hello 메서드 반환 전에 코드 toohello 함수를 다음을 추가 합니다. 함수의 hello 언어에 대 한 적절 한 코드 조각을 hello를 사용 합니다.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. 선택 **저장** toosave 변경 합니다.

toohello HTTP 트리거 전달 된 값이 hello 메시지 추가 toohello 큐에 포함 됩니다.
 
## <a name="test-hello-function"></a>테스트 hello 함수 

1. Hello 코드 변경 내용이 저장 된 후 선택 **실행**합니다. 

    ![큐 저장소 출력 바인딩 tooa 함수 hello Azure 포털에에서 추가 합니다.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Hello 로그 toomake hello 함수 성공 확인을 확인 합니다. 명명 된 새 큐 **outqueue** hello 함수 런타임 hello 출력 바인딩이 때 처음으로 사용 하 여 저장소 계정에 만들어집니다.

다음으로 tooyour 저장소 계정 tooverify hello 새 큐와 tooit 추가한 hello 메시지를 연결할 수 있습니다. 

## <a name="connect-toohello-queue"></a>Toohello 큐 연결

Skip 이미 저장소 탐색기를 설치 하 고 tooyour 저장소 계정을 연결 하는 경우 처음 3 단계를 hello 합니다.    

1. 함수에서 선택 **통합** 및 새 hello **Azure 큐 저장소** 바인딩 출력 한 다음 확장 **설명서**합니다. **계정 이름** 및 **계정 키**를 모두 복사합니다. 이러한 자격 증명 tooconnect toohello 저장소 계정을 사용합니다.
 
    ![Hello 저장소 계정 연결 자격 증명을 가져옵니다.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Hello 실행 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/) 도구, 선택 hello 연결 hello 왼쪽에 있는 아이콘을 선택 **저장소 계정 이름과 키를 사용 하 여**를 선택 하 고 **다음**합니다.

    ![Hello 저장소 계정 탐색기 도구를 실행 합니다.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. 붙여넣기 hello **계정 이름** 및 **계정 키** 의 해당 필드에 1 단계에서 선택한 다음 선택 **다음**, 및 **연결**합니다. 
  
    ![붙여 hello 저장소 자격 증명을 연결 합니다.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Hello 연결 된 저장소 계정, **큐** 큐 이름이 있는지 확인 하 고 **myqueue 항목** 존재 합니다. 또한 메시지 hello 큐에 이미 나타납니다.  
 
    ![저장소 큐 만들기.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>다음 단계

출력 바인딩 tooan 기존 함수를 추가 했습니다. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

바인딩 tooQueue 저장소에 대 한 자세한 내용은 참조 [Azure 함수 저장소 큐 바인딩](functions-bindings-storage-queue.md)합니다. 



