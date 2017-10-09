---
title: "aaaConnect tooan 온-프레미스 SAP 시스템에 Azure 논리 앱 | Microsoft Docs"
description: "Hello 온-프레미스 데이터 게이트웨이 통해 논리 앱 워크플로에서 tooan 온-프레미스 SAP 시스템에 연결"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Hello SAP connector 사용 하 여 논리 앱에서 tooan 온-프레미스 SAP 시스템에 연결 

hello 온-프레미스 데이터 게이트웨이 toomanage 데이터 있으며는 온-프레미스 리소스에 안전 하 게 액세스 합니다. 이 항목에서는 논리 앱 tooan 온-프레미스 SAP 시스템을 연결 하는 방법을 보여 줍니다. 이 예제에서는 논리 앱 HTTP를 통한 IDOC를 요청 하 고 hello 응답을 다시 보냅니다.    

> [!NOTE]
> 현재 제한 사항: 
> - Hello 응답에 필요한 모든 단계 hello 내에 완료 하지 않는 경우 논리 앱 시간 초과 [요청 시간 제한](./logic-apps-limits-and-config.md)합니다. 이 시나리오에서는 요청이 차단될 수 있습니다. 
> - hello 파일 선택기는 hello 사용 가능한 모든 필드를 표시 하지 않습니다. 이 시나리오에서는 경로를 수동으로 추가할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

- 설치 하 고 최신 hello 구성 [온-프레미스 데이터 게이트웨이](https://www.microsoft.com/download/details.aspx?id=53127) 1.15.6150.1 버전 이상. [어떻게 tooconnect toohello 온-프레미스 데이터 게이트웨이 논리 앱에서](http://aka.ms/logicapps-gateway) 목록 hello 단계입니다. hello 게이트웨이 계속 하려면 먼저 온-프레미스 컴퓨터에 설치 되어야 합니다.

- 다운로드 및 설치 hello 최신 SAP 클라이언트 라이브러리에 hello hello 데이터 게이트웨이 설치한 컴퓨터 동일 합니다. Hello SAP 버전을 다음 중 하나를 사용 합니다. 
    - SAP Server
        - SAP 서버는 지원 hello.NET 커넥터 (NCo) 3.0
 
    - SAP Client
        - SAP .NET Connector(NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>트리거 및 tooyour SAP 시스템 연결에 대 한 작업 추가

hello SAP connector에 동작을 있지만 트리거 되지 않습니다. 따라서는 toouse 다른 트리거 hello 워크플로의 hello 시작 부분에 있습니다. 

1. Hello 요청/응답 트리거를 추가 하 고 다음 선택 **새 단계**합니다.

2. 선택 **동작 추가**, 다음을 입력 하 여 hello SAP 커넥터를 선택 하 고 `SAP` hello 검색 필드에:    

     ![SAP 응용 프로그램 서버 또는 SAP 메시지 서버 선택](media/logic-apps-using-sap-connector/sap-action.png)

3. SAP 설치 프로그램에 따라 [**SAP 응용 프로그램 서버**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) 또는 [**SAP 메시지 서버**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm)를 선택합니다. 기존 연결 되지 않은 경우 하나 toocreate 메시지 표시 됩니다.

   1. 선택 **온-프레미스 데이터 게이트웨이 통해 연결**, SAP 시스템에 대 한 hello 세부 정보를 입력 합니다.   

       ![연결 문자열 tooSAP 추가](media/logic-apps-using-sap-connector/picture2.png)  

   2. 아래 **게이트웨이**, 기존 게이트웨이 또는 tooinstall 새 게이트웨이 선택, 선택 **게이트웨이 설치**합니다.

        ![새 게이트웨이 설치](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Hello에 대 한 세부 정보를 모두 입력 한 후 선택 **만들기**합니다. 
   논리 앱 구성 및 hello 연결이 제대로 작동 하는지 확인 하는 hello 연결을 테스트 합니다.

4. SAP 연결의 이름을 입력합니다.

5. hello 다른 SAP 옵션을 사용할 수 있습니다. toofind IDOC 범주를 hello 목록에서 선택 합니다. Hello 경로 및 hello에 대 한 선택 hello HTTP 응답에 수동으로 입력 하거나 **본문** 필드:

     ![SAP 작업](media/logic-apps-using-sap-connector/picture3.png)

6. Hello 동작을 만들기 위한 추가 **HTTP 응답**합니다. hello 응답 메시지의 hello SAP 출력 해야 합니다.

7. 논리 앱을 저장합니다. IDOC hello HTTP 트리거 URL 통해 전송 하 여 테스트 하십시오. IDOC 보내집니다 hello, 후 hello 논리 앱에서 hello 응답을 기다립니다.   

     > [!TIP]
     > 방법에 대해 너무 확인[논리 앱 모니터링](../logic-apps/logic-apps-monitor-your-logic-apps.md)합니다.

Hello SAP connector는 tooyour 논리 앱을 추가 하는 다른 기능과 탐색을 시작 합니다.

- BAPI
- RFC

## <a name="get-help"></a>도움말 보기

tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

- 자세한 내용은 방법 toovalidate, 변환 및 다른 BizTalk와 비슷한 함수 hello에서 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다. 
- [Tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md) 논리 앱에서
