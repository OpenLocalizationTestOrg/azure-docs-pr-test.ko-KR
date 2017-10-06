---
title: "Azure 논리 앱에서 aaaAdd hello Oracle 데이터베이스 커넥터 | Microsoft Docs"
description: "Hello Oracle 데이터베이스 커넥터를 사용 하 여 논리 앱"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Hello Oracle 데이터베이스 커넥터와 함께 시작

기존 데이터베이스의 데이터를 사용 하는 조직 구성 워크플로 만들 hello Oracle 데이터베이스 커넥터를 사용 하 여 있습니다. 이 커넥터는 온-프레미스 Oracle 데이터베이스 또는 Oracle 데이터베이스와 Azure 가상 컴퓨터에 설치 된 tooan을 연결할 수 있습니다. 이 커넥터를 사용하여 다음을 수행할 수 있습니다.

* 새 고객 tooa 고객 데이터베이스를 추가 하거나 orders 데이터베이스에 순서를 업데이트 하 여 워크플로 작성 합니다.
* 동작 tooget 데이터 행을 사용 하 고, 새 행을 삽입 하 고 및 삭제할 수도 있습니다. 예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Oracle 데이터베이스에 행을 삽입합니다(작업). 

이 항목에서는 toouse 논리 앱에서 Oracle 데이터베이스 커넥터 hello 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

* 지원되는 Oracle 버전: 
    * Oracle 9 이상
    * Oracle 클라이언트 소프트웨어 8.1.7 이상

* Hello 온-프레미스 데이터 게이트웨이 설치 합니다. [논리 앱에서 tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md) 목록 hello 단계입니다. hello 게이트웨이 온-프레미스 Oracle 데이터베이스 또는 Oracle DB 설치는 Azure VM에 필요한 tooconnect tooan입니다. 

    > [!NOTE]
    > hello 온-프레미스 데이터 게이트웨이 브리지 역할을 하 고 온-프레미스 데이터 (클라우드 hello에에서 없는 데이터) 및 논리 앱 간에 안전한 데이터 전송을 제공 합니다. hello 여러 서비스와 여러 데이터 원본이 동일한 게이트웨이에 사용할 수 있습니다. 따라서만 해야 tooinstall hello 게이트웨이 한 번만 합니다.

* Oracle 클라이언트 hello hello 온-프레미스 데이터 게이트웨이 설치한 hello 컴퓨터에 설치 합니다. Tooinstall는 64 비트 Oracle Data Provider for Oracle에서.NET hello 해야 합니다.  

  [Windows x64용 64비트 ODAC 12c 릴리스 4(12.1.0.2.4)](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Hello Oracle 클라이언트가 설치 되지 않은 경우 toocreate 시도 하거나 hello 연결을 사용할 때 오류가 발생 합니다. 이 항목의 일반적인 오류 hello를 참조 하십시오.


## <a name="add-hello-connector"></a>Hello 커넥터를 추가 합니다.

> [!IMPORTANT]
> 이 연결에는 트리거가 필요하지 않습니다. 작업만 있습니다. 따라서 논리 앱을 만들 때 다른 트리거 toostart 논리 앱와 같은 추가 **되풀이 일정을 예약**, 또는 **요청 / 응답-응답**합니다. 

1. Hello에 [Azure 포털](https://portal.azure.com), 빈 논리 앱을 만듭니다.

2. 논리 앱을 hello 시작 시 hello 선택 **요청 / 응답-요청** 트리거: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. **저장**을 선택합니다. 저장하면 요청 URL이 자동으로 생성됩니다. 

4. **새 단계**를 선택한 다음 **작업 추가**를 선택합니다. 에 입력 `oracle` toosee hello 사용 가능한 작업: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > 이 가장 빠른 방법은 toosee hello도 hello 트리거 및 모든 커넥터에 대해 사용할 수 있는 작업입니다. 와 같은 일부 hello 커넥터 이름에서에서 입력 `oracle`합니다. hello 디자이너는 트리거 및 작업을 나열합니다. 

5. 과 같은 hello 작업 중 하나를 선택 **Oracle 데이터베이스-Get 행**합니다. **온-프레미스 데이터 게이트웨이를 통해 연결**을 선택합니다. Hello Oracle 서버 이름, 인증 방법, 사용자 이름, 암호 및 선택 hello 게이트웨이 입력 합니다.

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. 연결 되 면 hello 목록에서 테이블을 선택 하 고 hello 행 ID tooyour 테이블을 입력 합니다. Tooknow hello 식별자 toohello 테이블이 필요합니다. Oracle DB 관리자에 게 문의 하 고에서 hello 출력을 가져올 알지 못하는 경우 `select * from yourTableName`합니다. 이렇게 하면 tooproceed 필요한 식별이 가능한 정보 hello 됩니다.

    다음 예제는 hello, 인사 관리 데이터베이스에서 작업 데이터를 반환 되 고 됩니다. 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. 다음이 단계에서 사용할 수 있습니다 hello의 다른 커넥터가 toobuild 워크플로에 합니다. Oracle에서 데이터를 가져오지 tootest 원하는 다음 사용자가 직접 hello 중 하나를 사용 하 여 hello Oracle 데이터와 전자 메일 보내기에 해당 하는 Office 365 또는 Gmail 메일 커넥터 보냅니다. Hello Oracle 테이블 toobuild hello의 hello 동적 토큰을 사용 하 여 `Subject` 및 `Body` 전자 메일:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. 논리 앱을 **저장**한 후 **실행**을 선택합니다. Hello 디자이너를 닫고 hello 상태에 대 한 실행 기록을 hello 합니다. 실패 한 경우 hello 메시지 실패 한 행을 선택 합니다. hello 디자이너가 열리고 오류 정보를 hello 및 실패 단계 된 방법을 보여 줍니다.도 보여 줍니다. 성공 하면 추가한 hello 정보로 메일을 받을 해야 있습니다.


### <a name="workflow-ideas"></a>워크플로 아이디어

* Toomonitor hello #oracle hashtag 원하는 쿼리 및 다른 응용 프로그램 내에서 사용할 수 있도록 데이터베이스의 hello 트 윗을 저장 합니다. 논리 앱에서 추가 hello `Twitter - When a new tweet is posted` 트리거되며 hello 입력 **#oracle** hashtag 합니다. Hello을 추가 합니다 `Oracle Database - Insert row` 동작을 사용자 테이블을 선택 합니다.

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Tooa 서비스 버스 큐를 다시 전송 됩니다. Tooget 이러한 메시지를 한 데이터베이스에 저장 합니다. 논리 앱에서 추가 hello `Service Bus - when a message is received in a queue` 트리거와 선택 hello 큐입니다. Hello을 추가 합니다 `Oracle Database - Insert row` 동작을 사용자 테이블을 선택 합니다.

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>일반 오류

#### <a name="error-cannot-reach-hello-gateway"></a>**오류**: hello 게이트웨이 연결할 수 없습니다

**원인**: hello 온-프레미스 데이터 게이트웨이 수 tooconnect toohello 클라우드가 아닙니다. 

**완화**: 게이트웨이 설치 하 고 한다는 toohello 연결할 수 있는 hello 온-프레미스 컴퓨터에서 실행 되 고 있는지 확인 인터넷 합니다.  해제 되어 있는 컴퓨터 또는 절전 모드를 hello 게이트웨이 설치 하지 않는 것이 좋습니다. Hello 온-프레미스 데이터 게이트웨이 서비스 (PBIEgwService)를 다시 시작할 수도 있습니다.

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**오류**: 사용 중인 hello 공급자는 사용 되지 않습니다: ' System.Data.OracleClient 필요 Oracle 클라이언트 소프트웨어 버전 8.1.7 이상입니다.'. 방문 하세요 [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello 공식 공급자입니다.

**원인**: hello Oracle 클라이언트 SDK에 설치 되어 있지 hello 컴퓨터 위치 hello 온-프레미스 데이터 게이트웨이가 실행 되 고 있습니다.  

**해결 방법**:에 다운로드 및 설치 hello Oracle 클라이언트 SDK hello hello 온-프레미스 데이터 게이트웨이와 동일한 컴퓨터.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**오류**: 테이블 '[Tablename]'에 키 열이 정의되어 있지 않습니다.

**원인**: hello 테이블의 모든 기본 키가 없습니다.  

**해결 방법**: hello Oracle 데이터베이스 커넥터는 기본 키 열에 있는 테이블을 사용 해야 합니다.

#### <a name="currently-not-supported"></a>현재 지원되지 않음

* 뷰 및 저장 프로시저 
* 복합 키가 있는 모든 테이블
* 테이블의 중첩된 개체 유형
 
## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/oracle/)합니다. 

## <a name="get-some-help"></a>도움 받기

hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) 는 좋은 tooask 질문 배치 질문에 답변 하 고 다른 논리 앱 사용자가 수행 하는 작업을 참조 합니다. 

[http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출해 주시면 Logic Apps 및 커넥터를 개선하는 데 도움이 될 수 있습니다. 


## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md), hello에서 논리 앱에서 사용할 수 있는 커넥터를 탐색 하 고 우리의 [Api 목록](apis-list.md)합니다.
