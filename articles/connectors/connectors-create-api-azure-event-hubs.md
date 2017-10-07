---
title: "Azure 논리 앱에 대 한 Azure 이벤트 허브 이벤트 모니터를 aaaSet | Microsoft Docs"
description: "데이터 스트림을 tooreceive 이벤트를 모니터링 하 고 Azure 이벤트 허브를 사용 하 여 Azure 논리 앱에 대 한 이벤트를 전송 합니다."
services: logic-apps
keywords: "데이터 스트림, 이벤트 모니터, 이벤트 허브"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>모니터링, 수신, 및 hello 이벤트 허브 커넥터와 함께 이벤트 보내기

이벤트 모니터를 tooset 논리 앱 이벤트 검색, 이벤트를 수신 고, 이벤트를 보낼 수 있도록 연결 tooan [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs) 논리 앱에서 합니다. [Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md)에 대해 자세히 알아봅니다.

## <a name="requirements"></a>요구 사항

* Toohave 있는 [이벤트 허브 네임 스페이스 및 이벤트 허브](../event-hubs/event-hubs-create.md) Azure에서. 자세한 내용은 [어떻게 toocreate 이벤트 허브 네임 스페이스 및 이벤트 허브](../event-hubs/event-hubs-create.md)합니다. 

* toouse [커넥터](https://docs.microsoft.com/azure/connectors/apis-list) 논리 앱에서 앱이 있는 toocreate 논리 먼저 합니다. 자세한 내용은 [어떻게 toocreate 논리 앱](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>이벤트 허브 네임 스페이스 사용 권한을 확인 하 고 hello 연결 문자열을 찾을

모든 서비스에 대 한 논리 앱 tooaccess toocreate 있는 [ *연결* ](./connectors-overview.md) 논리 앱 및 hello 서비스에 아직 없는 경우 사이입니다. 이 연결에는 논리 앱 tooaccess 데이터 권한도 부여 됩니다.
논리 앱 tooaccess에 대 한 이벤트 허브에 있는 toohave **관리** 사용 권한 및 이벤트 허브 네임 스페이스에 대 한 hello 연결 문자열입니다.

toocheck 권한과 get hello 연결 문자열에서 다음이 단계를 수행 합니다.

1.  Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다. 

2.  Tooyour 이벤트 허브로 이동 *네임 스페이스*, 특정 이벤트 허브를 hello 되지 않습니다. Hello 네임 스페이스 블레이드에서 아래 **설정**, 선택 **공유 액세스 정책을**합니다. **클레임** 아래에서 해당 네임스페이스에 대한 **관리** 권한이 있는지 확인합니다.

    ![Event Hub 네임스페이스에 대한 관리 권한](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  toocopy hello 연결 문자열 hello 이벤트 허브 네임 스페이스에 대 한 선택 **RootManageSharedAccessKey**합니다. 다음 tooyour 기본 연결 문자열 키를 hello 복사 단추를 선택 합니다.

    ![Event Hubs 네임스페이스 연결 문자열 복사](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm 연결 문자열은 특정 이벤트 허브 또는 이벤트 허브 네임 스페이스와 연결 되어 있는지 여부를 확인 hello에 대 한 연결 문자열 hello `EntityPath` 매개 변수입니다. 이 매개 변수를 찾을 경우 hello 연결 문자열 "엔터티"은 특정 이벤트 허브에 대 한 이며 논리 앱과 함께 hello 올바른 문자열로 toouse 않습니다.

4.  이제 이벤트 허브 트리거나 작업 tooyour 논리 앱을 추가한 후 자격 증명에 대 한 메시지가 나타나면, tooyour 이벤트 허브 네임 스페이스를 연결할 수 있습니다. 연결 이름을 지정, 복사 하 고 선택 하는 hello 연결 문자열을 입력 **만들기**합니다.

    ![Event Hubs 네임스페이스에 대한 연결 문자열 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    연결을 만들 hello 연결 이름 hello 이벤트 허브 트리거 또는 작업에 표시 되어야 합니다. 
    그런 다음 계속 진행할 수 있습니다 hello 논리 앱의 다른 단계입니다.

    ![Event Hubs 네임스페이스 연결 생성됨](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Event Hub에서 새 이벤트를 수신하면 워크플로 시작

[*트리거*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)는 논리 앱에서 워크플로를 시작하는 이벤트입니다. 새 이벤트는 tooyour 이벤트 허브를 전송 하는 경우 워크플로 시작 하려면이 이벤트를 검색 하는 hello 트리거를 추가 하기 위한 다음이 단계를 수행 합니다.

1.  Hello에 [Azure 포털](https://portal.azure.com "Azure 포털"), tooyour 기존 논리 앱을 이동 하거나 빈 논리 앱을 만듭니다.

2.  Hello 논리가 응용 프로그램 디자이너에 대 한 hello 검색 상자에 입력 `event hubs` 필터에 대 한 합니다. 이 트리거 선택: **이벤트가 Event Hub에서 사용 가능한 경우**

    ![Event Hub에서 새 이벤트를 수신하는 경우에 대한 트리거 선택](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    연결 tooyour 이벤트 허브 네임 스페이스를 아직 없는 경우 메시지가 toocreate이 지금이 연결 합니다. 사용자 연결에 이름을 지정 하 고 사용자 이벤트 허브 네임 스페이스에 대 한 hello 연결 문자열을 입력 합니다. 
    필요한 경우에 대해 배울 [어떻게 toofind 연결 문자열](#permissions-connection-string)합니다.

    ![Event Hubs 네임스페이스에 대한 연결 문자열 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Hello 연결을 만든 후 hello hello에 대 한 설정을 **때 이벤트에 이벤트 허브에서 사용할 수 있는** 트리거 표시 합니다.

    ![Event Hub에서 새 이벤트를 수신하는 경우에 대한 트리거 설정](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  입력 하거나 hello toomonitor 이벤트 허브에 대 한 hello 이름을 선택 합니다. Hello 빈도 및 빈도 toocheck hello 이벤트 허브에 대 한 간격을 선택 합니다.

    > [!TIP]
    > toooptionally 이벤트 읽기에 대 한 소비자 그룹을 선택, 선택 **고급 옵션 표시**합니다. 

    ![Event Hub 또는 소비자 그룹 지정](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    이제 설정한 트리거 toostart 워크플로 논리 앱에 대 한 합니다. 
    논리 앱 hello 이벤트 허브 설정 하는 hello 일정에 따라 지정 된 것을 확인 합니다. 
    Hello 이벤트 허브에서에서 새 이벤트를 발견 하는 응용 프로그램, hello 트리거 논리 앱에서 다른 작업 또는 트리거 실행 됩니다.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>논리 앱에서 이벤트 허브 이벤트 tooyour 보내기

[*작업*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)은 논리 앱 워크플로에서 수행하는 태스크입니다. 트리거 tooyour 논리 앱을 추가 하면 해당 트리거에 의해 생성 된 데이터와 작업 tooperform 작업을 추가할 수 있습니다. toosend 이벤트 tooyour 이벤트 허브 논리 앱에서 다음이 단계를 수행 합니다.

1.  논리 앱 디자이너의 논리 앱 트리거 아래에서 **새 단계** > **작업 추가**를 선택합니다.

    ![[새 단계]를 선택한 후 [작업 추가]를 선택합니다.](./media/connectors-create-api-azure-event-hubs/add-action.png)

    이제 작업 tooperform를 선택 하 찾을 수 있습니다. 
    이 예제에 대 한 작업을 선택할 수 있지만 hello 이벤트 허브 작업 toosend 이벤트 합니다.

2.  Hello 검색 상자에 입력 `event hubs` 필터에 대 한 합니다.
이 작업 선택: **이벤트 보내기**

    ![[Event Hubs - 이벤트 보내기] 작업을 선택합니다.](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Hello toosend hello 이벤트를 원하는 이벤트 허브에 대 한 hello 이름과 같은 hello 이벤트에 대 한 hello 필요한 세부 정보를 입력 합니다. 예: 해당 이벤트에 대 한 콘텐츠 hello 이벤트에 대 한 다른 선택적 정보를 입력 합니다.

    > [!TIP]
    > toooptionally 지정 여기서 toosend hello 이벤트 hello 이벤트 허브 파티션 선택 **고급 옵션 표시**합니다. 

    ![Event Hub 이름 및 선택적 이벤트 정보 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  변경 내용을 저장합니다.

    ![논리 앱 저장](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    이제 논리 앱에서 동작 toosend 이벤트를 설정 했습니다. 

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/eventhubs/)합니다. 

## <a name="get-help"></a>도움말 보기

tooask 질문과 대답 질문 참조를 수행 하는 다른 Azure 논리 앱 사용자가 방문 hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

*  [Azure Logic Apps용 다른 커넥터 찾기](./apis-list.md)