---
title: "논리 앱에서 aaaAdd hello DB2 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 DB2 커넥터 개요"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Hello DB2 커넥터와 함께 시작
D b 2 용 Microsoft connector 연결 논리 앱 tooresources IBM DB2 데이터베이스에 저장 합니다. 이 커넥터는 TCP/IP 네트워크를 통해 원격 DB2 서버 컴퓨터와 Microsoft 클라이언트 toocommunicate를 포함합니다. 이 클라우드 데이터베이스 IBM Bluemix dashDB 등 Azure 가상화에서 실행 되는 Windows 용 IBM DB2 및 온-프레미스 hello 온-프레미스 데이터 게이트웨이 사용 하 여 데이터베이스입니다. Hello 참조 [목록 지원](connectors-create-api-db2.md#supported-db2-platforms-and-versions) IBM DB2 플랫폼 및이 항목의 버전입니다.

hello DB2 커넥터 데이터베이스 작업을 수행 하는 hello를 지원 합니다.

* 데이터베이스 테이블 목록 표시
* SELECT를 사용하여 단일 행 읽기
* SELECT를 사용하여 전체 행 읽기
* INSERT를 사용하여 단일 행 추가
* UPDATE를 사용하여 단일 행 변경
* DELETE를 사용하여 단일 행 삭제

이 항목에서는 toouse hello 커넥터 논리 앱 tooprocess에서 데이터베이스 작업 하는 방법을 보여 줍니다.

논리 앱에 대해 자세히 toolearn 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="available-actions"></a>사용 가능한 작업
hello DB2 커넥터 논리 앱 작업을 수행 하는 hello를 지원 합니다.

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>테이블 나열
모든 작업에 대 한 논리 앱을 만들어 hello Microsoft Azure 포털을 통해 수행 하는 여러 단계 중 구성 됩니다.

Hello 논리 앱 내에서 DB2 데이터베이스에서 작업 toolist 테이블을 추가할 수 있습니다. hello 동작 지시 hello 커넥터 tooprocess DB2 schema 문와 같은 `CALL SYSIBM.SQLTABLES`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `Db2getTables`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 설정한 다음 hello **간격** tootype **7**합니다.  
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 `db2` hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-Get 테이블 (미리 보기)**합니다.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. Hello에 **DB2-Get 테이블** 구성 창 **확인란** tooenable **온-프레미스 데이터 게이트웨이 통해 연결**합니다. 클라우드 tooon 온-프레미스에서 변경 hello 설정을 확인 합니다.
   
   * 에 대 한 값을 입력 **서버**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `ibmserver01:50000`을(를) 입력합니다.
   * **데이터베이스**에 대한 값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
   * **인증**값을 선택합니다. 예를 들어 **기본**을 선택합니다.
   * **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `db2admin`을(를) 입력합니다.
   * **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
   * **게이트웨이**에 대한 값을 선택합니다. 예를 들어 **datagateway01**을 선택합니다.
7. **만들기**를 선택한 다음 **저장**을 선택합니다. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. Hello에 **Db2getTables** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
9. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_tables**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 테이블의 목록을 포함 해야 합니다.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Hello 연결 만들기
다음 연결 속성이 hello를 사용 하 여 hello 클라우드 및이 커넥터는 연결 호스트 toodatabases 온-프레미스를 지원 합니다. 

| 속성 | 설명 |
| --- | --- |
| 서버 |필수입니다. 콜론으로 구분된 TCP/IP 포트 번호가 뒤에 붙는 IPv4 또는 IPv6 형식 중 하나로 구성되어 TCP/IP 주소 또는 별칭을 나타내는 문자열 값이 허용됩니다. |
| 데이터베이스 |필수입니다. DRDA 관계형 데이터베이스 이름(RDBNAM)을 나타내는 문자열 값이 허용됩니다. z/OS용 IBM DB2 위치로 인식되는 데이터베이스인 z/OS용 DB2에는 16바이트 문자열이 허용됩니다. i 관계형 데이터베이스용 IBM DB2 데이터베이스로 인식되는 데이터베이스인 i5/OS용 DB2에는 18바이트 문자열이 허용됩니다. LUW용 DB2에는 8바이트 문자열이 허용됩니다. |
| 인증 |선택 사항입니다. 목록 항목 값, 즉 기본 또는 Windows (kerberos)가 허용됩니다. |
| 사용자 이름 |필수입니다. 문자열 값을 허용합니다. z/OS용 DB2에는 8바이트 문자열이 허용됩니다. i용 DB2에는 10바이트 문자열이 허용됩니다. Linux 또는 UNIX용 DB2에는 8바이트 문자열이 허용됩니다. Windows용 DB2에는 30바이트 문자열이 허용됩니다. |
| 암호 |필수입니다. 문자열 값을 허용합니다. |
| 게이트웨이 |필수입니다. Hello 저장소 그룹 내 hello 온-프레미스 데이터 게이트웨이 정의 tooLogic 응용 프로그램을 나타내는 목록 항목 값을 허용 합니다. |

## <a name="create-hello-on-premises-gateway-connection"></a>Hello 온-프레미스 게이트웨이 연결을 만듭니다.
이 커넥터는 온-프레미스 DB2 데이터베이스 hello 온-프레미스 게이트웨이 사용 하 여 액세스할 수 있습니다. 자세한 내용은 게이트웨이 항목을 참조하세요. 

1. Hello에 **게이트웨이** 구성 창 **확인란** tooenable **게이트웨이 통해 연결**합니다. 클라우드 tooon 온-프레미스에서 변경 hello 설정을 확인 합니다.
2. 에 대 한 값을 입력 **서버**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `ibmserver01:50000`을(를) 입력합니다.
3. **데이터베이스**에 대한 값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
4. **인증**값을 선택합니다. 예를 들어 **기본**을 선택합니다.
5. **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `db2admin`을(를) 입력합니다.
6. **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
7. **게이트웨이**에 대한 값을 선택합니다. 예를 들어 **datagateway01**을 선택합니다.
8. 선택 **만들기** toocontinue 합니다. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Hello 클라우드 연결 만들기
이 커넥터는 클라우드 DB2 데이터베이스에 액세스할 수 있습니다. 

1. Hello에 **게이트웨이** 구성 창, leave hello **확인란** 사용 안 함 (클릭된) **게이트웨이 통해 연결**합니다. 
2. **연결 이름**에 대한 값을 입력합니다. 예를 들어 `hisdemo2`을(를) 입력합니다.
3. 에 대 한 값을 입력 **DB2 서버 이름**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `hisdemo2.cloudapp.net:50000`을(를) 입력합니다.
4. **DB2 데이터베이스 이름**값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
5. **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `db2admin`을(를) 입력합니다.
6. **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
7. 선택 **만들기** toocontinue 합니다. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>SELECT를 사용하여 전체 행 가져오기
논리 앱 작업 toofetch 모든 행은 DB2 테이블에 정의할 수 있습니다. 와 같은 hello 커넥터 tooprocess DB2 SELECT 문을 한 이렇게 하면 `SELECT * FROM AREA`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `Db2getRows`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 `db2` hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-Get 행 (미리 보기)**합니다.
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다.
7. Hello에 **연결** 구성 창 **새로 만들기**합니다. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. Hello에 **게이트웨이** 구성 창, leave hello **확인란** 사용 안 함 (클릭된) **게이트웨이 통해 연결**합니다.
   
   * **연결 이름**에 대한 값을 입력합니다. 예를 들어 `HISDEMO2`을(를) 입력합니다.
   * 에 대 한 값을 입력 **DB2 서버 이름**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `HISDEMO2.cloudapp.net:50000`을(를) 입력합니다.
   * **DB2 데이터베이스 이름**값을 입력합니다. 예를 들어 `NWIND`을(를) 입력합니다.
   * **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `db2admin`을(를) 입력합니다.
   * **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
9. 선택 **만들기** toocontinue 합니다.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
11. 필요에 따라 선택 **고급 옵션 표시** toospecify 쿼리 옵션입니다.
12. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. Hello에 **Db2getRows** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
14. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 행 목록이 포함 되어야 합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>INSERT를 사용하여 단일 행 추가
DB2 테이블에는 논리 앱 작업 tooadd 하나의 행을 정의할 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess DB2 INSERT 문 같은 `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `Db2insertRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **db2** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-행 삽입 (미리 보기)**합니다.
6. Hello에 **DB2-행 삽입 (미리 보기)** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 연결을 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 `Area 99999` 유형의 **AREAID**에는 `99999`을(를) 입력하고 **REGIONID**에는 `102`을(를) 입력합니다. 
10. **저장**을 선택합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. Hello에 **Db2insertRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 새 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>SELECT를 사용하여 단일 행 가져오기
DB2 테이블에는 논리 앱 작업 toofetch 하나의 행을 정의할 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess DB2 위치 선택 문 같은 `SELECT FROM AREA WHERE AREAID = '99999'`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름** (예: "**Db2getRow**"), **구독**, **리소스 그룹**, **위치** 및 **앱 서비스 계획**을 입력합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다. 
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **db2** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-Get 행 (미리 보기)**합니다.
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결을 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 **AREAID**에는 `99999`을(를) 입력합니다. 
10. 필요에 따라 선택 **고급 옵션 표시** toospecify 쿼리 옵션입니다.
11. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. Hello에 **Db2getRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
13. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>UPDATE를 사용하여 단일 행 변경
DB2 테이블에는 논리 앱 작업 toochange 하나의 행을 정의할 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess DB2 UPDATE 문을 같은 `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `Db2updateRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **db2** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-행 업데이트 (미리 보기)**합니다.
6. Hello에 **DB2-행 업데이트 (미리 보기)** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결 tooselect 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 `Updated 99999` 유형의 **AREAID**에는 `99999`을(를) 입력하고 **REGIONID**에는 `102`을(를) 입력합니다. 
10. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. Hello에 **Db2updateRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 새 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>DELETE를 사용하여 단일 행 삭제
DB2 테이블에는 논리 앱 작업 tooremove 하나의 행을 정의할 수 있습니다. 와 같은 hello 커넥터 tooprocess DB2 삭제 문을이 작업에 지시 `DELETE FROM AREA WHERE AREAID = '99999'`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `Db2deleteRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다. 
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에서 **db2** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **DB2-행 삭제 (미리 보기)**합니다.
6. Hello에 **DB2-행 삭제 (미리 보기)** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결을 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 **AREAID**에는 `99999`을(를) 입력합니다. 
10. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. Hello에 **Db2deleteRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 삭제 된 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>지원되는 DB2 플랫폼 및 버전
이 커넥터 hello를 지 원하는 DRDA 분산 관계형 데이터베이스 아키텍처 () SQL 액세스 관리자 (SQLAM) 버전 10과 11 IBM DB2 호환 제품 (예: IBM Bluemix dashDB) 뿐만 아니라 IBM DB2 플랫폼 및 버전에서 다음을 지원 합니다.

* z/OS용 IBM DB2 11.1
* z/OS용 IBM DB2 10.1
* i용 IBM DB2 7.3
* i용 IBM DB2 7.2
* i용 IBM DB2 7.1
* LUW용 IBM DB2 11
* LUW용 IBM DB2 10.5

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/db2/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

