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
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Azure Queue Storage에 의해 트리거되는 함수 만들기

메시지는 경우에 발생 하는 함수 toocreate tooan Azure 저장소 큐를 전송 하는 방법을 알아봅니다.

![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>필수 조건

- 다운로드 및 설치 hello [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)합니다.

- Azure 구독. 구독이 없으면 시작하기 전에 [계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만드세요.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure Function 앱 만들기

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

다음으로 hello 새 함수 앱에서 함수를 만듭니다.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>큐 트리거 함수 만들기

1. 함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다. Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다. 이 함수 템플릿의 hello 전체 집합을 표시합니다.

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. 선택 hello **QueueTrigger** 원하는 언어 및 hello 테이블에 지정 된 hello 설정 사용에 대 한 서식 파일입니다.

    ![Hello 저장소 큐 트리거된 함수를 만듭니다.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | 설정 | 제안 값 | 설명 |
    |---|---|---|
    | **큐 이름**   | myqueue-items    | Tooconnect tooin 저장소 계정의 큐 하는 hello의 이름입니다. |
    | **Storage 계정 연결** | AzureWebJobStorage | Hello 함수 응용 프로그램에서 이미 사용 되는 저장소 계정 연결을 사용 하거나 새로 만들 수 있습니다.  |
    | **함수 이름 지정** | 함수 앱에서 고유 | 큐 트리거 함수의 이름입니다. |

3. 클릭 **만들기** toocreate 함수입니다.

다음으로 tooyour Azure 저장소 계정을 연결 하 고 hello 만들 **myqueue 항목** 저장소 큐입니다.

## <a name="create-hello-queue"></a>Hello 큐 만들기

1. 함수에서 **통합**을 클릭하고 **설명서**를 확장하여 **계정 이름** 및 **계정 키**를 모두 복사합니다. 이러한 자격 증명 tooconnect toohello 저장소 계정을 사용합니다. 저장소 계정에 이미 연결한 경우 toostep 4를 건너뜁니다.

    ![Hello 저장소 계정 연결 자격 증명을 가져옵니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Hello 실행 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/) 도구를 hello 클릭 연결 hello 왼쪽에 있는 아이콘을 선택 **저장소 계정 이름과 키를 사용 하 여**를 클릭 하 고 **다음**합니다.

    ![Hello 저장소 계정 탐색기 도구를 실행 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Hello 입력 **계정 이름** 및 **계정 키** 1 단계에서 클릭 **다음** 차례로 **연결**합니다.

    ![Hello 저장소 자격 증명을 입력 하 고 연결 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Hello 연결 된 저장소 계정, 마우스 오른쪽 단추로 클릭 **큐**, 클릭 **만들기 큐**, 형식 `myqueue-items`, enter 키를 누릅니다.

    ![저장소 큐 만들기.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

저장소 큐를가지고 메시지 toohello 큐를 추가 하 여 hello 함수를 테스트할 수 있습니다.

## <a name="test-hello-function"></a>테스트 hello 함수

1. Hello Azure 포털에 다시 찾아보기 tooyour 함수 확장 hello **로그** hello 있는지 확인 하 고 hello 페이지 맨 아래에 해당 로그 스트리밍 없는 일시 중지 합니다.

1. Storage 탐색기에서 저장소 계정, **큐** 및 **myqueue-items**를 확장한 후 **메시지 추가**를 클릭합니다.

    ![메시지 toohello 큐를 추가 합니다.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. "Hello World!" 메시지를 **메시지 텍스트**에 입력하고 **확인**을 클릭합니다.

1. 몇 초 동안 기다립니다 다음 tooyour 기능 로그를 다시 이동 하 고 hello 큐에서 읽은 hello 새 메시지를 확인 합니다.

    ![Hello 로그 보기 메시지입니다.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. 저장소 탐색기에서 다시 클릭 **새로 고침** 처리가 hello 메시지를 확인 하는 더 이상 hello 큐에 들어갑니다.

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>다음 단계

메시지가 tooa 저장소 큐 추가 될 때 실행 되는 함수를 만들었습니다.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Queue Storage 트리거에 대한 자세한 내용은 [Azure Functions Storage 큐 바인딩](functions-bindings-storage-queue.md)을 참조하세요.