---
title: "aaaGeneric SQL 커넥터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooconfigure Microsoft 일반 SQL 커넥터입니다."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>일반 SQL 커넥터 기술 참조
이 문서에서는 hello 제네릭 SQL 커넥터를 설명 합니다. hello 문서 toohello 제품 다음이 적용 됩니다.

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 핫픽스 4.1.3671.0 이상 [KB3092178](https://support.microsoft.com/kb/3092178)을 사용해야 합니다.

Hello 커넥터 MIM2016 및 FIM2010R2 hello에서 다운로드할 수는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=717495)합니다.

toosee 작업에서이 커넥터 참조 hello [단계별 제네릭 SQL 커넥터](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) 문서.

## <a name="overview-of-hello-generic-sql-connector"></a>Hello 제네릭 SQL 커넥터 개요
일반 SQL 커넥터 hello는 ODBC 연결을 제공 하는 데이터베이스 시스템과 toointegrate hello 동기화 서비스를 수 있습니다.  

상위 수준 측면에서 같은 기능 hello hello hello 커넥터의 현재 버전에서 지원 됩니다.

| 기능 | 지원 |
| --- | --- |
| 연결된 데이터 원본 |hello 커넥터 모든 64 비트 ODBC 드라이버를 사용할 수 있습니다. Hello 다음으로 테스트 되었습니다. <li>Microsoft SQL Server 및 SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 및 11g</li><li>MySQL 5.x</li> |
| 시나리오 |<li>개체 수명 주기 관리</li><li>암호 관리</li> |
| 작업 |<li>전체 가져오기 및 델타 가져오기, 내보내기</li><li>내보내기: 추가, 삭제, 업데이트 및 바꾸기</li><li>암호 설정, 암호 변경</li> |
| 스키마 |<li>개체 및 특성의 동적 검색</li> |

### <a name="prerequisites"></a>필수 조건
Hello 커넥터를 사용 하기 전에 hello 동기화 서버에 hello 다음 있는지 확인 합니다.

* Microsoft.NET 4.5.2 Framework 이상
* 64비트 ODBC 클라이언트 드라이버

### <a name="permissions-in-connected-data-source"></a>연결된 데이터 원본의 사용 권한
toocreate 또는 일반 SQL 커넥터에서 지원 되는 hello 작업을 수행 해야 합니다.

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>포트 및 프로토콜
ODBC 드라이버 toowork hello에 필요한 hello 포트, hello 데이터베이스 공급 업체의 설명서를 참조 하십시오.

## <a name="create-a-new-connector"></a>새 커넥터 만들기
일반 SQL 커넥터 tooCreate에 **동기화 서비스** 선택 **관리 에이전트** 및 **만들기**합니다. 선택 hello **일반 SQL (Microsoft)** 커넥터입니다.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>연결
hello 커넥터 연결에 대 한 ODBC DSN 파일을 사용 합니다. 사용 하 여 hello DSN 파일 만들기 **ODBC 데이터 원본** hello 시작 메뉴에서 찾을 **관리 도구**합니다. 만들 hello 관리 도구에는 **파일 DSN** toohello 커넥터 제공할 수 있도록 합니다.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

hello 연결 화면은 hello 먼저 새 제네릭 SQL 커넥터를 만들 때입니다. 먼저 다음 정보는 tooprovide hello가 필요 합니다.

* DSN 파일 경로
* 인증
  * 사용자 이름
  * 암호

hello 데이터베이스는 다음 인증 방법 중 하나를 지원 해야 합니다.

* **Windows 인증**: 데이터베이스를 인증 하는 hello hello Windows 자격 증명 tooverify hello 사용자를 사용 합니다. 지정 된 hello 사용자 이름과 암호는 hello 데이터베이스와 함께 사용 되는 tooauthenticate 합니다. 이 계정 사용 권한을 toohello 데이터베이스가 필요합니다.
* **SQL 인증**: hello 데이터베이스 사용 하 여 hello 사용자 이름/암호 인증 한 hello 연결 화면 tooconnect toohello 데이터베이스를 정의 합니다. Hello DSN 파일에서 hello 사용자 이름/암호를 저장 하는 경우 hello 자격 증명 hello 연결 화면에 제공 된 우선 순위를 가집니다.
* **Azure SQL 데이터베이스 인증**: 자세한 내용은 참조 [연결할 데이터베이스를 사용 하 여 Azure Active Directory 인증 여 tooSQL](../../sql-database/sql-database-aad-authentication.md)합니다.

**DN이 앵커**:이 옵션을 선택 하는 경우 hello DN hello 앵커 특성으로도 사용 됩니다. 이 간단한 구현에 사용할 수 있습니다 하지만 제한 다음 hello에:

* 커넥터는 하나의 개체 유형만 지원합니다. 따라서 특성 참조만 할 수 있는 참조 hello 동일한 개체 유형입니다.

**내보내기 형식: Replace 개체**: 내보내기 작업 중 일부 특성에만 변경 될 때 모든 특성을 가진 hello 전체 개체를 내보내고 대체 hello 기존 개체입니다.

### <a name="schema-1-detect-object-types"></a>스키마1(개체 형식 검색)
이 페이지에서는 tooconfigure 하려는 방법을 hello 커넥터는 hello 데이터베이스에서 진행 중인 toofind hello 다른 개체 형식입니다.

모든 개체 형식은 파티션으로 표시되며 **파티션 및 계층 구성**에서 자세히 구성됩니다.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**개체 유형 검색 방법**: hello 커넥터 이러한 개체 유형 검색 방법을 지원 합니다.

* **고정 값**: hello 쉼표로 구분 된 목록 사용 하 여 개체 유형 목록을 제공 합니다. 예: `User,Group,Department`  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **테이블/뷰/저장 프로시저**: hello hello 테이블/뷰/저장 프로시저의 이름과 다음 hello 개체 유형 목록을 제공 하는 hello 열 이름을 제공 합니다. 저장된 프로시저를 사용 하는 경우 다음도 매개 변수를 제공에 대 한 hello 형태로 표시 **[이름]: [방향]: [Value]**합니다. 별도 줄 (사용 하 여 Ctrl + Enter tooget 새 줄에) 각 매개 변수를 제공 합니다.  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **SQL 쿼리**:이 옵션을 사용 예를 들어 개체 유형의 단일 열을 반환 하는 SQL 쿼리 tooprovide 있습니다 `SELECT [Column Name] FROM TABLENAME`합니다. hello 반환 문자열 (varchar) 형식의 열 이어야 합니다.

### <a name="schema-2-detect-attribute-types"></a>스키마2(특성 형식 검색)
이 페이지에서는 보아야 tooconfigure 특성 이름을 어떻게 hello 및 형식 toobe 감지 하려고 합니다. hello 이전 페이지에서 검색 된 모든 개체 유형에 대해 hello 구성 옵션 나열 됩니다.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**특성 유형 검색 방법**: hello 커넥터 스키마 1 화면에서 검색 된 개체 형식별으로 이러한 특성 유형 검색 메서드를 지원 합니다.

* **테이블/뷰/저장 프로시저**: 사용된 toofind hello 특성 이름 이어야 하는 hello 테이블/뷰/저장 프로시저의 hello 이름을 제공 합니다. 저장된 프로시저를 사용 하는 경우 다음도 매개 변수를 제공에 대 한 hello 형태로 표시 **[이름]: [방향]: [Value]**합니다. 별도 줄 (사용 하 여 Ctrl + Enter tooget 새 줄에) 각 매개 변수를 제공 합니다. 다중 값된 특성에 toodetect hello 특성 이름은 쉼표로 구분 된 목록이 테이블 또는 뷰를 제공 합니다. 부모 및 자식 테이블에 동일한 열 이름이 있는 경우 다중값 시나리오가 지원되지 않습니다.
* **SQL 쿼리**:이 옵션을 사용 예를 들어 특성 이름 가진 단일 열을 반환 하는 SQL 쿼리 tooprovide 있습니다 `SELECT [Column Name] FROM TABLENAME`합니다. hello 반환 문자열 (varchar) 형식의 열 이어야 합니다.

### <a name="schema-3-define-anchor-and-dn"></a>스키마3(앵커 및 DN 정의)
이 페이지에 각 검색 된 개체 유형에 대해 tooconfigure 앵커 및 DN 특성 수 있습니다. 여러 특성 hello 앵커 toomake 템플릿 고유한 선택할 수 있습니다.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* 다중값 및 부울 특성은 나열되지 않습니다.
* 하지 않는 한 앵커 및 DN 특성과 동일한 특성을 사용할 수 없습니다 **DN이 앵커** hello 연결 페이지에서 선택 합니다.
* 경우 **DN이 앵커** 선택 hello 연결 페이지에서이 페이지는 유일한 hello DN 특성 필요 합니다. 이 특성은 hello 앵커 특성으로도 사용 합니다.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>스키마4(특성 형식, 참조 및 방향 정의)
이 페이지에서는 정수, 이진 또는 부울, 및 각 특성에 대 한 방향을 같은 tooconfigure hello 특성 형식이 있습니다. **스키마2** 페이지에서 모든 특성은 다중값 특성을 포함하여 나열됩니다.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **데이터 형식**: toomap hello 특성 유형 toothose 형식은 hello 동기화 엔진에 알려진를 사용 합니다. hello 기본 toouse hello hello SQL 스키마에서 검색 하는 대로 동일한 형식 이지만 날짜/시간 및 참조는 쉽게 감지 되지 않습니다. Toospecify, 해야 **DateTime** 또는 **참조**합니다.
* **방향**: hello 특성 방향 tooImport, 내보내기, 또는 ImportExport 설정할 수 있습니다. ImportExport는 기본값입니다.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

참고:

* 특성 유형을 hello 커넥터에서 검색 되지 않는, hello 문자열 데이터 형식이 사용 됩니다.
* **중첩 테이블** 은 열이 하나인 데이터베이스 테이블을 고려할 수 있습니다. Oracle는 임의의 순서로 중첩된 테이블의 hello 행을 저장합니다. 그러나 PL/SQL 변수로 hello 중첩된 테이블을 검색 하는 경우 hello 행 1부터 시작 하는 연속 아래 첨자 제공 됩니다. 배열 유사 액세스 tooindividual 행을 제공합니다.
* **VARRYS** hello 커넥터에서 지원 되지 않습니다.

### <a name="schema-5-define-partition-for-reference-attributes"></a>스키마5(참조 특성에 대한 파티션 정의)
이 페이지에서는 모든 참조 특성에 대해 특성이 참조하는 파티션(개체 형식)을 구성합니다.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

사용 하는 경우 **DN이 앵커**, hello 하나에서 참조 하 고 동일한 개체 유형 hello를 사용 해야 합니다. 다른 개체 형식을 참조할 수 없습니다.

>[!NOTE]
에 대 한 옵션은 이제 hello 2017 년 3 월 업데이트 부터는 "*"이이 옵션을 선택한 다음 모든 가능한 멤버 유형은 가져오게 됩니다.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 2017 년 5 월을 기준으로 hello "*" 즉, **옵션** 변경한 toosupport 가져오거나 내보내고 흐름. Toouse이이 옵션을 사용할 경우 다중 값된 테이블/뷰 hello 개체 유형을 포함 하는 특성이 있어야 합니다.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> 경우 "*" hello 개체 형식과 hello 열의 hello 이름을 지정 해야 하는 다음을 선택 합니다.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

가져온 후 다음, 다음과 유사한 toohello 이미지를 표시 됩니다.

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>글로벌 매개 변수
hello 글로벌 매개 변수 페이지를 사용 하는 tooconfigure 델타 가져오기 암호 방법과 날짜/시간 형식.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



일반 SQL 커넥터 hello hello 델타 가져오기에 대 한 메서드를 다음을 지원 합니다.

* **트리거**: [트리거를 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc708665.aspx)을 참조하세요.
* **워터 마크**: 모든 데이터베이스에 사용할 수 있는 일반적인 방법입니다. 미리 hello 데이터베이스 공급 업체에 따라 hello 워터 마크 쿼리가 채워집니다. 워터 마크 열은 사용되는 모든 테이블/보기에 있어야 합니다. 이 열으로 삽입 및 업데이트 toohello 테이블 및 해당 종속 추적 해야 합니다 (다중 값 또는 하위) 테이블입니다. hello 시계 동기화 서비스와 hello 데이터베이스 서버 간 동기화 되어야 합니다. 그렇지 않은 경우 hello 델타 가져오기에 일부 항목을 생략 될 수 있습니다.  
  제한 사항:
  * 워터 마크 전략은 삭제된 개체를 지원하지 않습니다.
* **스냅숏**: (Microsoft SQL Server로만 작동) [스냅숏을 사용하여 델타 뷰 생성](https://technet.microsoft.com/library/cc720640.aspx)
* **변경 내용 추적**: (Microsoft SQL Server로만 작동) [About 변경 내용 추적](https://msdn.microsoft.com/library/bb933875.aspx)  
  제한 사항:
  * 앵커 및 DN 특성 hello hello 테이블에서 선택한 개체에 대 한 기본 키의 일부 여야 합니다.
  * 변경 내용 추적을 사용하여 가져오기 및 내보내기를 수행하는 동안 SQL 쿼리가 지원되지 않습니다.

**추가 매개 변수**: hello 데이터베이스 서버에 있는 위치를 나타내는 데이터베이스 서버 표준 시간대를 지정 합니다. 이 값은 사용 toosupport hello 날짜 및 시간 특성의 다양 한 형식입니다.

hello 커넥터 UTC 형식으로 날짜와 날짜 및 시간을 항상 저장합니다. hello 날짜 및 시간 toobe 수 toocorrectly 변환할 hello 데이터베이스 서버 및 사용 하는 hello 형식을 hello 표준 시간대를 지정 해야 합니다. hello 형식.Net 형식을 표현 되어야 합니다.

내보내기 중 모든 날짜 시간 특성 toohello 커넥터 UTC 시간 형식으로 제공 되어야 합니다.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**암호 구성**: 암호 동기화 기능을 제공 하는 hello 커넥터 및 지원 설정 하 고 암호를 변경 합니다.

hello 커넥터 toosupport 암호 동기화를 두 가지 방법을 제공 합니다.

* **저장 프로시저**:이 방법은 두 개의 저장된 프로시저 toosupport 집합 및 암호를 변경 해야 합니다. 추가 대 한 모든 매개 변수를 입력 하 고 hello 암호 작업에서 변경 **암호 SP 설정** 및 **암호 SP 변경** 아래 예제에서는 각각 기준으로 매개 변수입니다.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **암호 확장**:이 메서드를 사용 하려면 암호 확장 DLL (tooprovide hello hello를 구현 하는 확장 DLL 이름 필요한 [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) 인터페이스). 암호 확장 어셈블리 hello 커넥터 런타임 시 hello DLL을 로드할 수 있도록 확장 폴더에 배치 되어야 합니다.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

Hello에 대 한 암호 관리 tooenable hello 있습니다 **확장 구성** 페이지.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>파티션 및 계층 구조 구성
Hello 파티션 및 계층 구조 페이지에서 모든 개체 유형을 선택 합니다. 각 개체 형식은 고유한 파티션입니다.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

Hello에 정의 된 hello 값을 재정의할 수도 있습니다 **연결** 또는 **글로벌 매개 변수** 페이지.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>앵커 구성
이 페이지는 hello 앵커 이미 정의 되어 있으므로 읽기 전용입니다. hello 선택한 앵커 특성은 항상 추가 hello 개체 유형 tooensure와 것에서으로 유지 고유 개체 유형입니다.

![anchors](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>실행 단계 매개 변수 구성
이러한 단계는 hello hello 커넥터에서 실행 프로필에서 구성 됩니다. 이러한 구성 데이터 가져오기 및 내보내기의 실제 작업을 hello지 않습니다.

### <a name="full-and-delta-import"></a>전체 및 델타 가져오기
일반 SQL 커넥터는 다음의 메서드를 사용하여 전체 및 델타 가져오기를 지원합니다.

* 테이블
* 보기
* 저장 프로시저
* SQL 쿼리

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**테이블/뷰**  
tooimport 다중 값된 속성 개체에 대해 tooprovide hello 쉼표로 구분 된 테이블/뷰 이름에 있으면 **다중값 이름 테이블/뷰** 및 각 조인 조건 hello에 **Join 조건**hello 부모 테이블입니다.

예: tooimport hello Employee 개체 및 해당 모든 다중 값된 특성 원하는합니다. 직원(주 테이블) 및 부서(다중값)라는 두 개의 테이블이 있습니다.
다음 hello지 않습니다.

* **테이블/뷰/SP**에서 **직원**을 입력합니다.
* **다중값 테이블/뷰 이름**에서 부서를 입력합니다.
* 직원 및 부서 간 hello 조인 조건을 입력 **조인 조건**, 예를 들어 `Employee.DEPTID=Department.DepartmentID`합니다.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**저장 프로시저**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* 많은 데이터를 설정한 경우이 저장 프로시저와 tooimplement 페이지 매김을 좋습니다.
* 저장 프로시저 toosupport 페이지 매김 tooprovide 시작 인덱스와 끝 인덱스 필요합니다. 참고: [많은 양의 데이터를 효율적으로 페이징](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndex 및 @EndIndex은(는) 실행 시 **구성 단계** 페이지에 구성된 해당 페이지 크기 값으로 바꿉니다. 예를 들어 hello 커넥터 첫 페이지와 hello 페이지 크기를 검색 하는 경우 설정 되어 500으로 이러한 상황에서 @StartIndex 1 것 및 @EndIndex 500 합니다. 이러한 값의 후속 페이지를 검색 하는 커넥터 늘린 hello 변경 @StartIndex & @EndIndex 값입니다.
* hello 매개 변수를 제공, tooexecute 저장 프로시저에 매개 변수가 `[Name]:[Direction]:[Value]` 형식입니다. (사용 하 여 Ctrl + Enter tooget 새 줄) 별도 줄에 각 매개 변수를 입력 합니다.
* 또한 일반 SQL 커넥터는 Microsoft SQL Server의 연결된 서버에서 가져오기 작업을 지원합니다. 연결 된 서버에 테이블에서 정보를 검색, 테이블 hello 형식으로 제공 해야:`[ServerName].[Database].[Schema].[TableName]`
* 일반 SQL 커넥터는 실행 단계 정보와 스키마 탐색 간에 구조가 비슷한(모두 별칭 이름 및 데이터 형식) 개체만 지원합니다. Hello 선택한 경우에 스키마 및 실행된 단계에서 제공 된 정보 로부터 개체 다르면 SQL 커넥터는 없습니다 toosupport 이러한 유형의 시나리오입니다.

**SQL 쿼리**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* 여러 결과 집합 쿼리는 지원되지 않습니다.
* SQL 쿼리 지원 페이지 매김 hello 설명과 시작 인덱스와 끝 인덱스 변수 toosupport 페이지 매김으로 합니다.

### <a name="delta-import"></a>델타 가져오기
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

델타 가져오기 구성은 전체 가져오기에 비해 몇 가지 추가 구성이 필요합니다.

* Hello 트리거 또는 스냅숏 방법을 tootrack 델타 변경 내용을 선택 하는 경우 데이터베이스에 스냅숏 또는 기록 테이블을 제공 합니다 **스냅숏 또는 기록 테이블에 해당 하는 데이터베이스의 이름** 상자입니다.
* 또한 해야 기록 테이블과 부모 테이블 간의 조인 조건을 tooprovide 예`Employee.ID=History.EmployeeID`
* hello 기록 테이블에서 hello 부모 테이블에서 tootrack hello 트랜잭션 hello 작업 정보 (추가/업데이트/삭제)를 포함 하는 hello 열 이름을 제공 해야 합니다.
* 워터 마크 tootrack 델타 변경 내용을 선택 하면 다음에 hello 작업 정보를 포함 하는 hello 열 이름을 제공 **수 위 표시 열 이름**합니다.
* hello **변경 유형 특성** 종류를 변경 하는 hello에 열이 필요 합니다. 이 열이 매핑되는 hello 기본 테이블에서 발생 하는 변경 또는 다중 값 테이블 tooa hello 델타 보기 형식을 변경 합니다. 이 열에는 특성-수준 변경 또는 추가, 수정, hello Modify_Attribute 변경 유형을 포함 될 수 있습니다 또는 삭제 변경 개체 수준 변경 형식에 대 한 유형입니다. Hello 기본값 추가, 수정가 하거나 삭제 하면이 옵션을 사용 하 여 해당 값을 정의할 수 있습니다.

### <a name="export"></a>내보내기
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

일반 SQL 커넥터는 다음과 같이 네 가지 지원된 방법을 사용하여 내보내기를 지원합니다.

* 테이블
* 보기
* 저장 프로시저
* SQL 쿼리

**테이블/뷰**  
Hello 테이블/뷰 옵션을 선택 하면 hello 커넥터 hello 각각의 쿼리 toodo hello 내보내기를 생성 합니다.

**저장 프로시저**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Hello 저장 프로시저 옵션을 선택 하면 세 가지 서로 다른 저장 프로시저 tooperform Insert/Update/Delete 작업 내보내기에 필요 합니다.

* **SP 이름을 추가**: 모든 개체에 hello 해당 테이블에서 삽입을 위한 tooconnector 제공 하는 경우이 SP 실행 합니다.
* **SP 이름을 업데이트**: 개체 업데이트 hello 해당 테이블에 대 한 tooconnector 상태가 된 경우이 SP 실행 합니다.
* **SP 이름을 삭제**: 임의의 개체 제공 tooconnector hello 해당 테이블에서 삭제 되 면이 SP 실행 합니다.
* 매개 변수 값 toohello 저장 프로시저를 사용 하는 hello 스키마에서 선택한 특성입니다. 예를 들어 `EmployeeName: INPUT: @EmployeeName` (EmployeeName hello 커넥터 스키마에서 선택 및 내보내기 수행 하는 동안 hello 해당 값을 대체 하는 hello 커넥터)
* toorun 저장된 프로시저 매개 변수가 있는, 매개 변수에서 제공 `[Name]:[Direction]:[Value]` 형식입니다. (사용 하 여 Ctrl + Enter tooget 새 줄) 별도 줄에 각 매개 변수를 입력 합니다.

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Hello SQL 쿼리 옵션을 선택 하면 세 가지 tooperform 삽입/업데이트/삭제 작업을 쿼리하여 내보내기 필요 합니다.

* **삽입 쿼리**: 개체 tooconnector hello 해당 테이블에 삽입을 위해 제공 하는 경우이 쿼리를 실행 합니다.
* **업데이트 쿼리**: 개체 업데이트 hello 해당 테이블에 대 한 tooconnector 상태가 된 경우이 쿼리가 실행 됩니다.
* **삭제 쿼리**: 개체 상태가 tooconnector hello 해당 테이블에서 삭제 된 경우이 쿼리를 실행 합니다.
* 예를 들어 매개 변수 값 toohello 쿼리를 사용 하는 hello 스키마에서 선택한 특성`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>문제 해결
* 참조 hello tooenable 로깅 tootroubleshoot 커넥터 hello 하는 방법에 대 한 내용은 [어떻게 커넥터에 대 한 ETW 추적 tooEnable](http://go.microsoft.com/fwlink/?LinkId=335731)합니다.
