---
title: "Cosmos DB aaaConnect tooAzure BI 분석 도구를 사용 하 여 | Microsoft Docs"
description: "어떻게 toouse hello Azure Cosmos DB ODBC 드라이버 toocreate 테이블 및 뷰 데이터와 BI 분석 소프트웨어에 정규화 된 데이터를 볼 수 있도록에 대해 알아봅니다."
keywords: "odbc, odbc 드라이버"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Cosmos DB tooAzure 연결 hello ODBC 드라이버와 BI 분석 도구를 사용 하 여

hello tooconnect tooAzure 분석 하 고 있는 Azure Cosmos DB 데이터 시각화를 만들 수 있도록 Cosmos DB BI 분석을 사용 하 여 SQL Server Integration Services, Power BI Desktop 및 Tableau와 같은 도구는 Azure Cosmos DB ODBC 드라이버 사용 솔루션입니다.

hello Azure Cosmos DB ODBC 드라이버 호환 ODBC 3.8 이며 ANSI SQL 92 구문을 지원 합니다. 드라이버는 다양 한 기능 toohelp Azure Cosmos DB의 데이터를 renormalize hello 합니다. Hello 드라이버를 사용 하 여 Azure Cosmos DB에서 데이터 테이블 및 뷰를 나타낼 수 있습니다. hello 드라이버에서는 hello 테이블 및 뷰를 쿼리, 삽입, 업데이트 및 삭제 하 여 그룹을 포함 하 여에 대 한 tooperform SQL 작업 있습니다.

## <a name="why-do-i-need-toonormalize-my-data"></a>Toonormalize 내 데이터도 필요한 이유
Azure Cosmos DB schemaless 데이터베이스, tooiterate 응용 프로그램을 사용 하 여 응용 프로그램을 신속 하 게 개발할 수 있게 되므로 데이터 hello 신속 하 게 모델링 하지 tooa 엄격한 스키마 제한 합니다. 단일 Azure Cosmos DB 데이터베이스에 다양한 구조의 JSON 문서가 포함될 수 있습니다. 이 빠른 응용 프로그램 개발에 매우 유용 하지만 tooanalyze 원하는 하 고 데이터 분석 및 BI 도구를 사용 하 여 데이터의 보고서를 만들 hello 데이터 종종 toobe 결합 해야 하 고 tooa 특정 스키마를 준수 합니다.

이 경우에 hello ODBC 드라이버. Hello ODBC 드라이버를 사용 하 여 있습니다 수 이제 구하고 다시 정규화 된 테이블 및 뷰 tooyour 데이터 분석 및 보고를 맞추는 방식으로 Azure Cosmos DB에서 데이터 필요 합니다. hello 구하고 다시 정규화 된 스키마 hello 내부 데이터에 영향을 미치지와 개발자가 tooadhere toothem를 제한 하지 않습니다, 그리고은 사용 하도록 설정 하기만 하면 tooleverage ODBC 호환 도구 tooaccess hello 데이터. 이제 Azure Cosmos DB 데이터베이스는 개발 팀에서 선호될 뿐 아니라 데이터 분석에서도 많이 사용될 것입니다.

이제 있습니다 hello ODBC 드라이버를 시작 하세요.

## <a id="install"></a>1 단계: hello Azure Cosmos DB ODBC 드라이버를 설치 합니다.

1. 사용자 환경에 대 한 hello 드라이버를 다운로드 합니다.

    * Windows 64비트용 [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64)
    * Windows 32비트 또는 64비트용 [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64)
    * Windows 32비트용 [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32)

    실행된 hello msi 파일을 로컬, 어떤 시작 hello **Microsoft Azure Cosmos DB ODBC 드라이버 설치 마법사**합니다. 
2. Hello 기본 입력된 tooinstall hello ODBC 드라이버를 사용 하 여 hello 설치 마법사를 완료 합니다.
3. 열기 hello **ODBC 데이터 원본 관리자** 컴퓨터에 앱을 할 수 있는이 하 여 입력 **ODBC 데이터 원본** Windows hello에서에서 검색 상자입니다. 
    Hello 드라이버 hello를 클릭 하 여 설치 된 것을 확인할 수 있습니다 **드라이버** 탭 하 고, 보장 **Microsoft Azure Cosmos DB ODBC Driver** 나열 됩니다.

    ![Azure Cosmos DB ODBC 데이터 원본 관리자](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>2 단계: tooyour Azure Cosmos DB 데이터베이스 연결

1. 후 [hello Azure Cosmos DB ODBC 드라이버 설치](#install), hello에 **ODBC 데이터 원본 관리자** 창 클릭 **추가**합니다. 사용자 또는 시스템 DSN을 만들 수 있습니다. 이 예제에서는 사용자 DSN을 만듭니다.
2. Hello에 **새 데이터 원본 만들기** 창에서 **Microsoft Azure Cosmos DB ODBC Driver**, 클릭 하 고 **마침**합니다.
3. Hello에 **Azure Cosmos DB ODBC 드라이버 SDN 설정** 창 hello 다음을 입력 합니다. 

    ![Azure Cosmos DB ODBC 드라이버 DSN 설정 창](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **데이터 원본 이름**: hello ODBC DSN에 대 한 고유한 이름입니다. 이 이름은 고유 tooyour Azure Cosmos DB 계정을 하므로 적절 한 이름을 계정이 여러 개인 경우 합니다.
    - **설명**: hello 데이터 원본에 대 한 간략 한 설명을 합니다.
    - **호스트**: Azure Cosmos DB 계정에 대한 URI입니다. 다음 스크린 샷에서 hello와 같이 hello Azure Cosmos DB 키 블레이드에서 hello Azure 포털에서에서이 검색할 수 있습니다. 
    - **선택 키**: hello 스크린 샷 다음 그림과 같이 hello Azure Cosmos DB 키 블레이드에서 hello Azure 포털에서에서 기본 또는 보조, 읽기 / 쓰기 또는 읽기 전용 키 hello 합니다. Hello DSN 읽기 전용 데이터 처리 및 보고에 사용 되 면 hello 읽기 전용 키를 사용 하는 것이 좋습니다.
    ![Azure Cosmos DB 키 블레이드](./media/odbc-driver/odbc-driver-keys.png)
    - **에 대 한 액세스 키를 암호화**: hello 최선의 선택이이 컴퓨터의 hello 사용자를 기반으로 선택 합니다. 
4. Hello 클릭 **테스트** 단추 toomake tooyour Azure Cosmos DB 계정을 연결할 수 있는지 합니다. 
5. 클릭 **고급 옵션** 집합 hello 값에 따라:
    - **일관성 쿼리**: 선택 hello [일관성 수준이](consistency-levels.md) 운영을 위한 합니다. hello 기본값은 세션입니다.
    - **재시도 횟수**: hello 몇 번 tooretry tooservice 제한 인해 hello 초기 요청이 완료 되지 않은 경우에 작업입니다.
    - **스키마 파일**: 다양한 옵션이 있습니다.
        - 기본적으로이 항목으로 (비어 있음)는 그대로 두고 hello 드라이버 hello 각 컬렉션의 모든 컬렉션 toodetermine hello 스키마에 대 한 첫 번째 페이지 데이터를 검색 합니다. 이 작업을 컬렉션 매핑이라고 합니다. 정의 된 스키마 파일 없이 hello 드라이버 각 드라이버 세션에 대 한 tooperform hello 검색이 개이고 a 더 높은 hello DSN을 사용 하 여 응용 프로그램의 시간 시작 될 수 있습니다. 따라서 DSN에 대한 스키마 파일을 항상 연결하는 것이 좋습니다.
        - 스키마 파일을 이미 있는 경우 (사용 하 여 만든 수 있는 하나 hello [스키마 편집기](#schema-editor))를 클릭할 수 있는 **찾아보기**을 tooyour 파일을 이동한 다음 클릭 **저장**, 클릭 하 고 **확인**합니다.
        - 새 스키마 toocreate 클릭 **확인**, 클릭 하 고 **스키마 편집기** hello 주 창에 있습니다. 설정한 다음 toohello [스키마 편집기](#schema-editor) 정보입니다. 새 스키마 파일 hello를 만들면 해야 toogo 백 toohello **고급 옵션** 창 tooinclude hello 새로 만든 스키마 파일입니다.

6. 완료 하 고 hello를 닫으면 **Azure Cosmos DB ODBC 드라이버가 DSN 설정** 창에서 새 사용자 DSN은 hello toohello 사용자 DSN 탭을 추가 합니다.

    ![Hello 사용자 DSN 탭에서 새 Azure Cosmos DB ODBC DSN](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>3 단계: hello 컬렉션 매핑 메서드를 사용 하 여 스키마 정을 만듭니다.

**컬렉션 매핑** 또는 **테이블 구분 기호**의 두 가지 유형의 샘플링 방법을 사용할 수 있습니다. 샘플링 세션은 두 가지 샘플링 방법을 모두 사용할 수 있지만 각 컬렉션은 특정 샘플링 방법만 사용할 수 있습니다. 다음 hello 단계 hello 컬렉션 매핑 방법을 사용 하 여 하나 이상의 컬렉션에 hello 데이터에 대 한 스키마를 만듭니다. 이 샘플링 방법을 hello 데이터의 컬렉션 toodetermine hello 구조의 hello 페이지의 hello 데이터를 검색합니다. Hello ODBC 쪽에 있는 컬렉션 tooa 테이블을 바꿉니다. 이 샘플링 메서드는 효율적이 고 빠른 hello 데이터 컬렉션에는 유형이 같은 경우입니다. 컬렉션 형식이 다른 형식의 데이터가 들어 있으면 hello를 사용 하는 것이 좋습니다 [테이블 구분 기호 메서드 매핑할](#table-mapping) toodetermine hello 데이터 구조 hello 컬렉션에는 보다 강력한 샘플링 방법을 제공 합니다. 

1. 1-4 단계에서 완료 한 후 [연결 tooyour Azure Cosmos DB 데이터베이스](#connect), 클릭 **스키마 편집기** hello에 **Azure Cosmos DB ODBC 드라이버가 DSN 설정** 창.

    ![Hello Azure Cosmos DB ODBC 드라이버가 DSN 설정 창에서 스키마 편집기 단추](./media/odbc-driver/odbc-driver-schema-editor.png)
2. Hello에 **스키마 편집기** 창 클릭 **새로 만들기**합니다.
    hello **스키마 생성** hello Azure Cosmos DB 계정에서에서 모든 hello 컬렉션 창에 표시 됩니다. 
3. 하나 이상의 컬렉션 toosample를 선택한 다음 클릭 **샘플**합니다. 
4. Hello에 **디자인 보기** 탭, hello 데이터베이스, 스키마 및 테이블에 표시 됩니다. Hello 테이블 뷰에서 hello 검색에는 hello hello 열 이름 (SQL 이름, 원본 이름 등)와 관련 된 속성 집합이 표시 됩니다.
    각 열에 대 한 hello 열 SQL 이름, hello SQL 유형, SQL 길이 (있는 경우), 수정할 수 있습니다 (있는 경우) 소수 자릿수, 전체 자릿수 (있는 경우) 및 null을 허용 합니다.
    - 설정할 수 있습니다 **열 숨기기** 너무**true** tooexclude 쿼리 결과에서 해당 열을 선택 합니다. 열 표시 열 숨기기 = true는 여전히 hello 스키마의 일부가 아니지만 선택 및 프로젝션에 대 한 반환 되지 않습니다. 예를 들어 "_"로 시작 하는 hello Azure Cosmos DB 필요한 시스템 속성을 모두 숨길 수 있습니다.
    - hello **id** 열은 hello 유일한 필드는 hello hello 정규화 된 스키마의 기본 키로 사용 될 때 숨길 수 없습니다. 
5. Hello 스키마 정의 완료 한 후 클릭 **파일** | **저장**toohello 디렉터리 toosave hello 스키마를 탐색 한 다음 클릭, **저장**합니다.

    Toouse hello 나중에 원하는 경우이 스키마 DSN을 사용 hello Azure Cosmos DB ODBC 드라이버가 DSN 설정 창을 열고 (ODBC 데이터 원본 관리자 hello)를 통해 고급 옵션을 클릭 한 다음 hello 스키마 파일 상자에서 스키마 저장 toohello를 이동 합니다. 스키마 파일 tooan 저장 기존 DSN hello DSN 연결 tooscope toohello 데이터와 스키마에서 정의 된 구조를 수정 합니다.

## <a id="table-mapping"></a>4 단계: hello 테이블 구분 기호를 사용 하 여 스키마 정의 만드는 메서드를 매핑

**컬렉션 매핑** 또는 **테이블 구분 기호**의 두 가지 유형의 샘플링 방법을 사용할 수 있습니다. 샘플링 세션은 두 가지 샘플링 방법을 모두 사용할 수 있지만 각 컬렉션은 특정 샘플링 방법만 사용할 수 있습니다. 

hello 다음 단계에에서 스키마를 만들 hello 데이터에 대 한 hello를 사용 하 여 하나 이상의 컬렉션 **테이블 구분 기호** 메서드 매핑할 합니다. 컬렉션에 형식이 다른 데이터가 포함되어 있으면 이 샘플링 방법을 사용하는 것이 좋습니다. 이 메서드 tooscope hello tooa 집합의 특성 및 해당 값을 샘플링을 사용할 수 있습니다. 예를 들어 문서에 "Type" 속성을 포함 하는 경우이 속성의 hello 샘플링 toohello 값 범위 수 있습니다. hello 샘플링의 hello 최종 결과 집합의 각 사용자가 지정한 형식에 대 한 hello 값에 대 한 테이블을 것입니다. 예를 들어, Type = Car를 지정하면 Car 테이블이 생성되지만 Type = Plane을 지정하면 Plane 테이블이 생성됩니다.

1. 1-4 단계에서 완료 한 후 [연결 tooyour Azure Cosmos DB 데이터베이스](#connect), 클릭 **스키마 편집기** hello Azure Cosmos DB ODBC 드라이버가 DSN 설치 창에서.
2. Hello에 **스키마 편집기** 창 클릭 **새로 만들기**합니다.
    hello **스키마 생성** hello Azure Cosmos DB 계정에서에서 모든 hello 컬렉션 창에 표시 됩니다. 
3. Hello에 대 한 컬렉션 선택 **샘플 보기** 탭 hello **매핑 정의** hello 컬렉션에 대 한 열을 클릭 **편집**합니다. 그런 다음 hello **매핑 정의** 창에서 **테이블 구분 기호** 메서드. 그런 다음 않습니다 다음 hello:

    a. Hello에 **특성** 상자 구분 기호 속성의 hello 이름을 입력 합니다. 이 속성은 사용자 문서를 tooscope hello 샘플링, 예를 들어 도시에 속성 및 enter 키를 누릅니다. 

    b. 방금 입력 한 hello 특성에 대 한 tooscope hello 샘플링 toocertain 값만 하려는 경우 hello 특성 hello 선택 상자에서 선택 하 고 hello에 값을 입력 **값** 상자 예를 들어 시애틀 enter 키를 누릅니다. 특성에 대 한 여러 값 tooadd를 계속할 수 있습니다. 특성 선택 값을 입력할 때 올바른 해당 hello 바로 확인 합니다.

    예를 들어, 포함 하는 경우는 **특성** 값의 City, 원하는 toolimit 테이블 tooonly 뉴욕과 두바이 도시 값 행, hello에hello특성상자및뉴욕및두바이City를입력합니다 **값** 상자입니다.
4. **확인**을 클릭합니다. 
5. Hello에 toosample hello 컬렉션에 대 한 hello 매핑 정의 완료 한 후 원하는 **스키마 편집기** 창 클릭 **샘플**합니다.
     각 열에 대 한 hello 열 SQL 이름, hello SQL 유형, SQL 길이 (있는 경우), 수정할 수 있습니다 (있는 경우) 소수 자릿수, 전체 자릿수 (있는 경우) 및 null을 허용 합니다.
    - 설정할 수 있습니다 **열 숨기기** 너무**true** tooexclude 쿼리 결과에서 해당 열을 선택 합니다. 열 표시 열 숨기기 = true는 여전히 hello 스키마의 일부가 아니지만 선택 및 프로젝션에 대 한 반환 되지 않습니다. 예를 들어 "_"로 시작 하 여 모든 hello Azure Cosmos DB 필요한 시스템 속성을 숨길 수 있습니다.
    - hello **id** 열은 hello 유일한 필드는 hello hello 정규화 된 스키마의 기본 키로 사용 될 때 숨길 수 없습니다. 
6. Hello 스키마 정의 완료 한 후 클릭 **파일** | **저장**toohello 디렉터리 toosave hello 스키마를 탐색 한 다음 클릭, **저장**합니다.
7. Hello에 다시 **Azure Cosmos DB ODBC 드라이버가 DSN 설정** 창 클릭 * * 옵션 * * 고급 합니다. 그런 다음, hello **스키마 파일** 상자 저장 toohello 스키마 파일을 이동 하 고 클릭 **확인**합니다. 클릭 **확인** 다시 toosave hello DSN입니다. 이 저장 hello 만든 스키마를 toohello DSN입니다. 

## <a name="optional-creating-views"></a>(선택 사항) 뷰 만들기
정의 하 고 hello 샘플링 프로세스의 일환으로 보기를 만들 수 있습니다. 이러한 뷰는 해당 tooSQL 뷰입니다. 읽기 전용으로 설정 되며 범위 hello 선택 내용 및 hello Azure Cosmos DB SQL 정의의 프로젝션 됩니다. 

toocreate hello에서 데이터에 대 한 보기 **스키마 편집기** 창의 hello에서 **뷰 정의** 열을 클릭 하 여 **추가** hello 컬렉션 toosample의 hello 행에 있습니다. 그런 다음 hello **뷰 정의** 창 다음 hello지 않습니다:
1. 클릭 **새로**EmployeesfromSeattleView 예를 들어, hello 보기의 이름을 입력 하 고 클릭 **확인**합니다.
2. Hello에 **보기 편집** 창 Azure Cosmos DB 쿼리를 입력 합니다. Azure Cosmos DB SQL 쿼리(예: `SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`)여야 합니다. 그런 후 **확인**을 클릭합니다.

원하는 수만큼 뷰를 만들 수 있습니다. Hello 뷰 정의 완료 하면 다음 hello 데이터를 샘플링할 수 있습니다. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>5단계: Power BI Desktop과 같은 BI 도구에서 데이터 보기

이 단계 단순히 표시 하는 ODBC 호환 도구로-새 사용자 DSN tooconnect DocumentADB을 사용할 수 있습니다 tooconnect tooPower BI Desktop 및 Power BI 시각화를 만듭니다.

1. Power BI Desktop을 엽니다.
2. **데이터 가져오기**를 클릭합니다.
3. Hello에 **데이터 가져오기** 창 클릭 **다른** | **ODBC** | **연결**합니다.
4. Hello에 **에서 ODBC** 창, 선택 hello 데이터 원본 이름을 생성 하 고 클릭 **확인**합니다. Hello에 두면 **고급 옵션** 빈 항목입니다.
5. Hello에 **ODBC 드라이버를 사용 하 여 데이터 원본에 액세스** 창에서 **기본값 또는 사용자 지정** 클릭 하 고 **연결**합니다. Tooinclude hello 않아도 **연결 문자열 속성을 자격 증명**합니다.
6. Hello에 **탐색기** hello 데이터베이스, hello 스키마 및 선택 hello 테이블 창의 hello 왼쪽된 창에서를 확장 합니다. hello 결과 창에는 만든 hello 스키마를 사용 하 여 hello 데이터 포함 되어 있습니다.
7. Power BI desktop에서 toovisualize hello 데이터 hello 테이블 이름 앞에 hello 상자를 확인 하 고 클릭 **부하**합니다.
8. Power BI Desktop에서 맨 왼쪽 hello 선택 hello 데이터 탭 ![Power BI Desktop의 데이터 탭](./media/odbc-driver/odbc-driver-data-tab.png) 데이터를 가져온 tooconfirm 합니다.
9. 이제 Power BI를 사용 하 여 hello 보고서 탭을 클릭 하 여 시각적 개체를 만들 수 있습니다 ![Power BI Desktop의 보고서 탭](./media/odbc-driver/odbc-driver-report-tab.png), **새 시각적**, 타일 사용자 지정 하 고 있습니다. Power BI Desktop에서 시각화를 만드는 방법에 대한 자세한 내용은 [Power BI의 시각화 유형](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/)을 참조하세요.

## <a name="troubleshooting"></a>문제 해결

Hello 다음 오류가 표시 되 면 확인 hello **호스트** 및 **선택 키** 복사한 값에서 Azure 포털 hello [2 단계](#connect) 올바른지, 그리고 다시 시도 하십시오. Hello 복사 단추 toohello hello의 오른쪽을 사용 하 여 **호스트** 및 **선택 키** hello Azure 포털 toocopy hello 값 오류 없이의 값입니다.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>다음 단계

Azure Cosmos DB에 대해 자세히 toolearn 참조 [Azure Cosmos DB 이란?](introduction.md)합니다.
