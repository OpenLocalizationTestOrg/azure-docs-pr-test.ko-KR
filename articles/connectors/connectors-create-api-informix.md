---
title: "논리 앱에서 aaaAdd hello Informix 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Informix 커넥터 개요"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Hello Informix 커넥터와 함께 시작
Informix 용 Microsoft connector 연결 논리 앱 tooresources IBM Informix 데이터베이스에 저장 합니다. TCP/IP 네트워크를 통해 hello Informix 커넥터에는 Microsoft 클라이언트 toocommunicate tooremote Informix 서버 컴퓨터가 포함 됩니다. 이 Azure의 가상화를 실행 하는 Windows 용 IBM Informix 같은 클라우드 데이터베이스 및 온-프레미스 hello 온-프레미스 데이터 게이트웨이 사용 하 여 데이터베이스입니다. Hello 참조 [목록 지원](connectors-create-api-informix.md#supported-informix-platforms-and-versions) IBM Informix 플랫폼 및이 항목의 버전입니다.

hello 커넥터 데이터베이스 작업을 수행 하는 hello를 지원 합니다.

* 데이터베이스 테이블 목록 표시
* SELECT를 사용하여 단일 행 읽기
* SELECT를 사용하여 전체 행 읽기
* INSERT를 사용하여 단일 행 추가
* UPDATE를 사용하여 단일 행 변경
* DELETE를 사용하여 단일 행 삭제

이 항목에서는 toouse hello 커넥터 논리 앱 tooprocess에서 데이터베이스 작업 하는 방법을 보여 줍니다.

논리 앱에 대해 자세히 toolearn 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="available-actions"></a>사용 가능한 작업
이 커넥터는 논리 앱 작업을 수행 하는 hello를 지원 합니다.

* Getables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>테이블 나열
모든 작업에 대 한 논리 앱을 만들어 hello Microsoft Azure 포털을 통해 수행 하는 여러 단계 중 구성 됩니다.

Hello 논리 앱 내에서 작업 toolist 테이블 Informix 데이터베이스에 추가할 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess Informix schema 문와 같은 `CALL SYSIBM.SQLTABLES`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `InformixgetTables`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다.  
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-Get 테이블 (미리 보기)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. Hello에 **Informix-Get 테이블** 구성 창 **확인란** tooenable **온-프레미스 데이터 게이트웨이 통해 연결**합니다. 클라우드 tooon 온-프레미스에서 변경 hello 설정을 확인 합니다.
   
   * 에 대 한 값을 입력 **서버**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `ibmserver01:9089`을(를) 입력합니다.
   * **데이터베이스**에 대한 값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
   * **인증**값을 선택합니다. 예를 들어 **기본**을 선택합니다.
   * **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `informix`을(를) 입력합니다.
   * **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
   * **게이트웨이**에 대한 값을 선택합니다. 예를 들어 **datagateway01**을 선택합니다.
7. **만들기**를 선택한 다음 **저장**을 선택합니다. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. Hello에 **InformixgetTables** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
9. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_tables**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 테이블의 목록을 포함 해야 합니다.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Hello 연결 만들기
다음 연결 속성이 hello를 사용 하 여 hello 클라우드 및이 커넥터는 연결 toodatabase 온-프레미스를 지원 합니다. 

| 속성 | 설명 |
| --- | --- |
| 서버 |필수입니다. 콜론으로 구분된 TCP/IP 포트 번호가 뒤에 붙는 IPv4 또는 IPv6 형식 중 하나로 구성되어 TCP/IP 주소 또는 별칭을 나타내는 문자열 값이 허용됩니다. |
| 데이터베이스 |필수입니다. DRDA 관계형 데이터베이스 이름(RDBNAM)을 나타내는 문자열 값이 허용됩니다. IBM Informix 데이터베이스 이름(dbname)으로 인식되는 데이터베이스인 Informix에는 128바이트 문자열이 허용됩니다. |
| 인증 |선택 사항입니다. 목록 항목 값, 즉 기본 또는 Windows (kerberos)가 허용됩니다. |
| 사용자 이름 |필수입니다. 문자열 값을 허용합니다. |
| 암호 |필수입니다. 문자열 값을 허용합니다. |
| 게이트웨이 |필수입니다. Hello 저장소 그룹 내 hello 온-프레미스 데이터 게이트웨이 정의 tooLogic 응용 프로그램을 나타내는 목록 항목 값을 허용 합니다. |

## <a name="create-hello-on-premises-gateway-connection"></a>Hello 온-프레미스 게이트웨이 연결을 만듭니다.
이 커넥터 hello 온-프레미스 데이터 게이트웨이 사용 하 여 온-프레미스 Informix 데이터베이스에 액세스할 수 있습니다. 자세한 내용은 게이트웨이 항목을 참조하세요. 

1. Hello에 **게이트웨이** 구성 창 **확인란** tooenable **게이트웨이 통해 연결**합니다. 클라우드 tooon 온-프레미스에서 설정을 변경 하는 hello를 참조 하십시오.
2. 에 대 한 값을 입력 **서버**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `ibmserver01:9089`을(를) 입력합니다.
3. **데이터베이스**에 대한 값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
4. **인증**값을 선택합니다. 예를 들어 **기본**을 선택합니다.
5. **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `informix`을(를) 입력합니다.
6. **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
7. **게이트웨이**에 대한 값을 선택합니다. 예를 들어 **datagateway01**을 선택합니다.
8. 선택 **만들기** toocontinue 합니다. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Hello 클라우드 연결 만들기
이 커넥터는 클라우드 Informix 데이터베이스에 액세스할 수 있습니다. 

1. Hello에 **게이트웨이** 구성 창, leave hello **확인란** 사용 안 함 (클릭된) **게이트웨이 통해 연결**합니다. 
2. **연결 이름**에 대한 값을 입력합니다. 예를 들어 `hisdemo2`을(를) 입력합니다.
3. 에 대 한 값을 입력 **Informix 서버 이름**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `hisdemo2.cloudapp.net:9089`을(를) 입력합니다.
4. **Informix 데이터베이스 이름**값을 입력합니다. 예를 들어 `nwind`을(를) 입력합니다.
5. **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `informix`을(를) 입력합니다.
6. **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
7. 선택 **만들기** toocontinue 합니다. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>SELECT를 사용하여 전체 행 가져오기
논리 앱 작업 toofetch 모든 행은 hello Informix 테이블에서 만들 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess Informix SELECT 문에 같은 `SELECT * FROM AREA`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름** (예: "**InformixgetRows**"), **구독**, **리소스 그룹**, **위치** 및 **앱 서비스 계획**을 입력합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-Get 행 (미리 보기)** .
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다.
7. Hello에 **연결** 구성 창 **새로 만들기**합니다. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. Hello에 **게이트웨이** 구성 창, leave hello **확인란** 사용 안 함 (클릭된) **게이트웨이 통해 연결**합니다.
   
   * **연결 이름**에 대한 값을 입력합니다. 예를 들어 `HISDEMO2`을(를) 입력합니다.
   * 에 대 한 값을 입력 **Informix 서버 이름**, 주소 또는 별칭으로 포트 번호의 hello 형태로 합니다. 예를 들어 `HISDEMO2.cloudapp.net:9089`을(를) 입력합니다.
   * **Informix 데이터베이스 이름**값을 입력합니다. 예를 들어 `NWIND`을(를) 입력합니다.
   * **사용자 이름**에 대한 값을 입력합니다. 예를 들어 `informix`을(를) 입력합니다.
   * **암호**에 대한 값을 입력합니다. 예를 들어 `Password1`을(를) 입력합니다.
9. 선택 **만들기** toocontinue 합니다.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
11. 필요에 따라 선택 **고급 옵션 표시** toospecify 쿼리 옵션입니다.
12. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. Hello에 **InformixgetRows** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
14. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 행 목록이 포함 되어야 합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>INSERT를 사용하여 단일 행 추가
Informix 테이블에서 논리 앱 작업 tooadd 하나의 행을 만들 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess Informix INSERT 문 같은 `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `InformixinsertRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-행 삽입 (미리 보기)**.
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 연결 프로그램 tooselect 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 `Area 99999` 유형의 **AREAID**에는 `99999`을(를) 입력하고 **REGIONID**에는 `102`을(를) 입력합니다. 
10. **저장**을 선택합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. Hello에 **InformixinsertRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 새 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>SELECT를 사용하여 단일 행 가져오기
Informix 테이블에서 논리 앱 작업 toofetch 하나의 행을 만들 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess Informix 위치 선택 문 같은 `SELECT FROM AREA WHERE AREAID = '99999'`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `InformixgetRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-Get 행 (미리 보기)** .
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결 tooselect 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 **AREAID**에는 `99999`을(를) 입력합니다. 
10. 필요에 따라 선택 **고급 옵션 표시** toospecify 쿼리 옵션입니다.
11. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. Hello에 **InformixgetRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
13. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력; 있는 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>UPDATE를 사용하여 단일 행 변경
Informix 테이블에서 논리 앱 작업 toochange 하나의 행을 만들 수 있습니다. 이 작업 지시 hello 커넥터 tooprocess Informix UPDATE 문을 같은 `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `InformixupdateRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-행 업데이트 (미리 보기)**.
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결 tooselect 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 `Updated 99999` 유형의 **AREAID**에는 `99999`을(를) 입력하고 **REGIONID**에는 `102`을(를) 입력합니다. 
10. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. Hello에 **InformixupdateRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 새 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>DELETE를 사용하여 단일 행 삭제
Informix 테이블에서 논리 앱 작업 tooremove 하나의 행을 만들 수 있습니다. 와 같은 hello 커넥터 tooprocess Informix 삭제 문을이 작업에 지시 `DELETE FROM AREA WHERE AREAID = '99999'`합니다.

### <a name="create-a-logic-app"></a>논리 앱 만들기
1. Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.
2. Hello 입력 **이름**와 같은 `InformixdeleteRow`, **구독**, **리소스 그룹**, **위치**, 및 **응용 프로그램 계획 서비스**합니다. 선택 **Pin toodashboard**를 선택한 후 **만들기**합니다.

### <a name="add-a-trigger-and-action"></a>트리거 및 작업 추가
1. Hello에 **논리 앱 디자이너**선택, **빈 LogicApp** hello에 **템플릿** 목록입니다.
2. Hello에 **트리거** 목록에서 **되풀이**합니다. 
3. Hello에 **되풀이** 트리거를 **편집**선택, **주파수** 드롭 다운 tooselect **일**를 선택한 후  **간격** tootype **7**합니다. 
4. 선택 hello **+ 새 단계** 상자를 선택한 후 **동작 추가**합니다.
5. Hello에 **동작** 목록에 입력 **informix** hello에 **추가 작업에 대 한 검색** 편집 상자를 선택한 후 **Informix-행 삭제 (미리 보기)**.
6. Hello에 **행 (미리 보기)을 가져오려면** 동작을 **연결 변경**합니다. 
7. Hello에 **연결** 구성 창에서 기존 연결을 선택 합니다. 예를 들어 **hisdemo2**를 선택합니다.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. Hello에 **테이블 이름** 목록, 선택 hello **아래쪽 화살표**를 선택한 후 **영역**합니다.
9. 모든 필수 열(빨간색 별표 참조) 값을 입력합니다. 예를 들어 **AREAID**에는 `99999`을(를) 입력합니다. 
10. **저장**을 선택합니다. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. Hello에 **InformixdeleteRow** hello 내 블레이드 **모든 실행** 목록에서 **요약**, 선택 hello 첫 번째 나열 된 항목 (가장 최근 실행).
12. Hello에 **실행 논리 앱** 블레이드를 **실행 세부 정보**합니다. Hello 내 **동작** 목록에서 **Get_rows**합니다. Hello 값에 대 한 참조 **상태**, 해야 **Succeeded**합니다. 선택 hello **입력 링크** tooview hello 입력 합니다. 선택 hello **출력 링크**, 및 보기 hello 출력;는 hello 삭제 된 행을 포함 해야 합니다.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>지원되는 Informix 플랫폼 및 버전
이 커넥터는 구성 시 IBM Informix 버전을 다음과 같습니다. hello 지원 toosupport DRDA 분산 관계형 데이터베이스 아키텍처 () 클라이언트 연결 합니다.

* IBM Informix 12.1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/informix/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md) 탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

