---
title: "aaaLearn 어떻게 toouse hello Azure 논리 앱에 대 한 MQ 커넥터 | Microsoft Docs"
description: "프로그램 논리 앱 워크플로 toobrowse에서 tooan 온-프레미스 또는 Azure MQ 서버를 연결, 수신, 및 메시지 tooWebSphere MQ 보내기"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Hello MQ 커넥터를 사용 하 여 논리 앱에서 tooan IBM MQ 서버 연결 

MQ용 Microsoft 커넥터는 MQ 서버 온-프레미스 또는 Azure에 저장된 메시지를 전송하고 검색합니다. 이 커넥터는 TCP/IP 네트워크를 통해 원격 IBM MQ 서버와 통신하는 Microsoft MQ 클라이언트를 포함합니다. 이 문서는 시작 가이드 toouse hello MQ 커넥터입니다. 큐에서 단일 메시지를 검색 하 여 시작 하 고 다른 작업을 hello 보는 것이 좋습니다.    

hello MQ 커넥터 hello 다음 작업을 포함 합니다. 트리거는 없습니다.

-   Hello IBM MQ Server에서에서 hello 메시지를 삭제 하지 않고 단일 메시지 찾아보기
-   Hello IBM MQ Server에서에서 hello 메시지를 삭제 하지 않고 일괄 처리 메시지 찾아보기
-   단일 메시지를 수신 하 고 hello IBM MQ Server에서에서 hello 메시지를 삭제 합니다.
-   일괄 처리 메시지를 수신 하 고 hello IBM MQ Server에서에서 hello 메시지 삭제
-   단일 메시지 toohello IBM MQ Server 보내기 

## <a name="prerequisites"></a>필수 조건

* 온-프레미스 MQ 서버를 사용 하는 경우 [hello 온-프레미스 데이터 게이트웨이 설치](../logic-apps/logic-apps-gateway-install.md) 네트워크 내의 서버에 있습니다. MQ 서버 hello 공개적으로 Azure 내에서 제공 하거나, 사용할 수 있으면 다음 hello 데이터 게이트웨이 사용 되지 않거나 필요 합니다.

    > [!NOTE]
    > hello 서버에 온-프레미스 데이터 게이트웨이가 설치 된 hello도 있어야.Net Framework 4.6이 MQ 커넥터 toofunction hello에 대 한 설치 합니다.

* Hello hello 온-프레미스 데이터 게이트웨이-에 대 한 Azure 리소스 만들기 [hello 데이터 게이트웨이 연결을 설정](../logic-apps/logic-apps-gateway-connection.md)합니다.

* 공식적으로 지원되는 IBM WebSphere MQ 버전:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>논리 앱 만들기

1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다. 
2. Hello 입력 **이름**, MQTestApp, 같은 **구독**, **리소스 그룹**, 및 **위치** (여기서 hello hello 위치 사용 온-프레미스 데이터 게이트웨이 연결 구성 됨). 선택 **Pin toodashboard**를 선택 하 고 **만들기**합니다.  
![논리 앱 만들기](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>트리거 추가

> [!NOTE]
> hello MQ 커넥터는 모든 트리거는 없습니다. 따라서 사용 하 여 다른 트리거 toostart hello와 같은 논리 앱 **되풀이** 트리거. 

1. hello **논리 앱 디자이너** 열립니다, **되풀이** 일반적인 트리거의 hello 목록의 합니다.
2. 선택 **편집** hello 되풀이 트리거 내에서. 
3. 집합 hello **주파수** 너무**일**, 및 집합 hello **간격** 너무**7**합니다. 

## <a name="browse-a-single-message"></a>단일 메시지 찾아보기
1. **+ 새 단계**를 선택한 다음 **작업 추가**를 선택합니다.
2. Hello 검색 상자에 입력 `mq`를 선택한 후 **MQ-찾아보기 메시지**합니다.  
![메시지 찾아보기](media/connectors-create-api-mq/Browse_message.png)

3. 기존 MQ 연결 없으면 다음 hello 연결을 만듭니다.  

    1. 선택 **온-프레미스 데이터 게이트웨이 통해 연결**, 한 MQ 서버의 hello 속성을 입력 합니다.  
    에 대 한 **서버**, hello MQ 서버 이름을 입력 하거나 뒤에 콜론과 hello 포트 번호로 hello IP 주소를 입력 합니다. 
    2. hello **게이트웨이** 구성 된 모든 기존 게이트웨이 연결을 나열 하는 드롭다운입니다. 게이트웨이를 선택합니다.
    3. 작업을 완료하면 **만들기**를 선택합니다. 연결에는 비슷한 toohello 다음 표시 됩니다.   
    ![연결 속성](media/connectors-create-api-mq/Connection_Properties.png)

4. Hello 작업 속성에서 다음을 수행할 수 있습니다.  

    * 사용 하 여 hello **큐** 속성 tooaccess hello 연결에 정의 된 것 보다 다른 큐 이름
    * 사용 하 여 hello **MessageId**, **CorrelationId**, **GroupId**, 및 기타 속성 toobrowse hello 다른 MQ 메시지 속성에 따라 메시지에 대 한
    * 설정 **IncludeInfo** 너무**True** hello 출력의 tooinclude 추가 메시지 정보입니다. 너무 설정 또는**False** toonot hello 출력에 추가 메시지 정보를 포함 합니다.
    * 입력 한 **제한 시간** 값 toodetermine 비어 있는 큐에서 메시지 tooarrive에 대 한 시간 toowait 합니다. 아무 것도 입력 되지 hello 큐의 첫 번째 메시지 hello이 검색 되 고 메시지 tooappear 기다리는 데 걸린 시간이 합니다.  
    ![메시지 속성 찾아보기](media/connectors-create-api-mq/Browse_message_Props.png)

5. 변경 내용을 **저장**한 다음 논리 앱을 **실행**합니다.  
![저장 및 실행](media/connectors-create-api-mq/Save_Run.png)

6. 몇 초 후 실행 하는 hello hello 단계 표시 되어 있으며, hello 출력 볼 수 있습니다. 각 단계의 hello 녹색 확인 표시가 toosee 세부 정보를 선택 합니다. 선택 **원시 출력 참조** toosee hello에 대 한 추가 세부 정보 데이터를 출력 합니다.  
![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_message_output.png)  

    원시 출력:  
    ![메시지 원시 출력 찾아보기](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Hello 때 **IncludeInfo** tootrue 옵션 설정, hello 출력 뒤에 표시 됩니다.  
![메시지 포함 정보 찾아보기](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>여러 메시지 찾아보기
hello **메시지 찾아보기** 액션에 포함 된 **BatchSize** 옵션 tooindicate hello 큐에서 메시지 반환 되어야 합니다.  **BatchSize**에 항목이 없는 경우 모든 메시지가 반환됩니다. hello 출력은 메시지의 배열을 반환 합니다.

1. Hello를 추가할 때 **메시지 찾아보기** hello 첫 번째 연결을 구성 된 작업은 기본적으로 선택 합니다. 선택 **연결 변경** toocreate 새 연결 하거나 다른 연결을 선택 합니다.

2. 찾아보기의 hello 출력 메시지를 보여 줍니다.  
![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>단일 메시지 수신
hello **메시지 받기** 동작 hello로 동일한 입력 및 출력을 hello에 **찾아보기 메시지** 동작 합니다. 사용 하는 경우 **메시지 받기**, hello 메시지 hello 큐에서 삭제 됩니다.

## <a name="receive-multiple-messages"></a>여러 메시지 수신
hello **메시지를 받을** 동작 hello로 동일한 입력 및 출력을 hello에 **메시지 찾아보기** 동작 합니다. 사용 하는 경우 **메시지를 받을**, hello 메시지 hello 큐에서 삭제 됩니다.

메시지가 없는 hello 큐에는 찾아보기 또는 receive를 수행 하는 경우, 다음 출력 hello로 hello 단계가 실패 합니다.  
![MQ 메시지 오류 없음](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>메시지 보내기
1. Hello를 추가할 때 **메시지 보내기** hello 첫 번째 연결을 구성 된 작업은 기본적으로 선택 합니다. 선택 **연결 변경** toocreate 새 연결 하거나 다른 연결을 선택 합니다. 유효한 hello **메시지 유형** 는 **데이터 그램**, **회신**, 또는 **요청**합니다.  
![메시지 속성 전송](media/connectors-create-api-mq/Send_Msg_Props.png)

2. hello 메시지 보내기의 출력 hello 다음과 같습니다.  
![메시지 출력 전송](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/mq/)합니다.

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.
