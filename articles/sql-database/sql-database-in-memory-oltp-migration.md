---
title: "aaaIn 메모리 내 OLTP SQL txn 성능 향상 | Microsoft Docs"
description: "기존 SQL 데이터베이스의 메모리 내 OLTP를 채택 tooimprove의 트랜잭션 성능입니다."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>메모리 내 OLTP를 사용 하 여 tooimprove SQL 데이터베이스에서 응용 프로그램 성능
[메모리 내 OLTP](sql-database-in-memory.md) 에 수 있는 트랜잭션 처리, 데이터 수집 및 임시 데이터 시나리오 사용된 tooimprove hello 성능을 [프리미엄](sql-database-service-tiers.md) 증가 하지 않고 Azure SQL 데이터베이스 가격 책정 계층을 hello 합니다. 

> [!NOTE] 
> [쿼럼이 SQL Database를 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)에 대해 알아보기


기존 데이터베이스에서 이러한 단계 tooadopt 메모리 내 OLTP를 따릅니다.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>1단계: 프리미엄 데이터베이스 사용 확인
메모리 내 OLTP는 프리미엄 데이터베이스에서만 지원됩니다. 메모리 내 hello 결과 1을 반환 하는 경우 지원 됩니다 (0 아님):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP*는 *고도의 트랜잭션 처리*의 약어입니다.



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>2 단계: 식별 개체 toomigrate tooIn 메모리 내 OLTP
SSMS는 활성 워크로드를 사용하여 데이터베이스에 대해 실행할 수 있는 **트랜잭션 성능 분석 개요** 보고서를 포함합니다. 테이블 및 저장된 프로시저에 적합 한 마이그레이션 hello 보고서 식별 tooIn 메모리 내 OLTP 합니다.

Ssms에서 toogenerate hello 보고서:

* Hello에 **개체 탐색기**, 데이터베이스 노드를 마우스 오른쪽 단추로 클릭 합니다.
* **보고서** > **표준 보고서** > **트랜잭션 성능 분석 개요**를 클릭합니다.

자세한 내용은 참조 [테이블 또는 tooIn 메모리 내 OLTP 저장 프로시저를 이식 해야 하는지 확인](http://msdn.microsoft.com/library/dn205133.aspx)합니다.

## <a name="step-3-create-a-comparable-test-database"></a>3단계: 비교할 수 있는 테스트 데이터베이스 만들기
hello 보고서 데이터베이스를 나타냅니다. 가정 되 고 이익이 되는 테이블 변환 tooa 메모리 액세스에 최적화 된 테이블. 테스트 하 여 tooconfirm hello 표시 먼저 테스트 하는 것이 좋습니다.

프로덕션 데이터베이스의 테스트 복사본이 필요합니다. hello 테스트 데이터베이스 있어야 hello에 동일한 서비스 계층 수준 프로덕션 데이터베이스로 합니다.

tooease 테스트, 테스트 데이터베이스를 다음과 같이 수정할.

1. SSMS를 사용 하 여 toohello 테스트 데이터베이스를 연결 합니다.
2. tooavoid 쿼리에서 WITH (SNAPSHOT) 옵션 hello, hello T-SQL 문 다음에 표시 된 대로 hello 데이터베이스 옵션을 설정 해야 합니다.
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>4단계: 테이블 마이그레이션
만들고 메모리 액세스에 최적화 된 복사본을 채우는 해야 원하는 tootest hello 테이블의 합니다. 다음 중 하나를 사용하여 만들 수 있습니다.

* hello SSMS에서 메모리 최적화 마법사에 유용 합니다.
* 수동 T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>SSMS의 메모리 최적화 마법사.
toouse이 마이그레이션 옵션:

1. SSMS로 toohello 테스트 데이터베이스를 연결 합니다.
2. Hello에 **개체 탐색기**hello 테이블을 마우스 오른쪽 단추로 클릭 하 고 클릭 **메모리 최적화 관리자**합니다.
   
   * hello **테이블 메모리 최적화 관리자** 마법사가 표시 됩니다.
3. Hello 마법사에서 **마이그레이션 유효성 검사** (또는 hello **다음** 단추) toosee hello 테이블에 있는 경우 지원 되지 않는 메모리 액세스에 최적화 된 테이블에서 지원 되지 않는 기능입니다. 자세한 내용은 다음을 참조하세요.
   
   * hello *메모리 최적화 검사 목록이* 에 [메모리 최적화 관리자](http://msdn.microsoft.com/library/dn284308.aspx)합니다.
   * [메모리 내 OLTP에서 지원되지 않는 TRANSACT-SQL 항목](http://msdn.microsoft.com/library/dn246937.aspx).
   * [마이그레이션 tooIn 메모리 내 OLTP](http://msdn.microsoft.com/library/dn247639.aspx)합니다.
4. Hello 테이블에 지원 되지 않는 기능이 없습니다, hello 관리자는 사용자에 대 한 hello 실제 스키마 및 데이터 마이그레이션을 수행할 수 있습니다.

#### <a name="manual-t-sql"></a>수동 T-SQL
toouse이 마이그레이션 옵션:

1. SSMS (또는 이와 유사한 유틸리티)을 사용 하 여 tooyour 테스트 데이터베이스를 연결 합니다.
2. 테이블 및 인덱스에 대 한 hello 전체 T-SQL 스크립트를 가져옵니다.
   
   * SSMS에서 테이블 노드를 마우스 오른쪽 단추로 클릭합니다.
   * **테이블 스크립팅** > **CREATE** > **새 쿼리 창**을 클릭합니다.
3. Hello 스크립트 창에서 추가 WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE 문의 합니다.
4. 클러스터형 인덱스가 있으면 tooNONCLUSTERED 변경 합니다.
5. SP_RENAME을 사용 하 여 hello 기존 테이블을 이름을 바꿉니다.
6. 편집 된 CREATE TABLE 스크립트를 실행 하 여 hello 테이블의 새 메모리 액세스에 최적화 된 복사본을 hello를 만듭니다.
7. INSERT를 사용 하 여 hello 데이터 tooyour 메모리 액세스에 최적화 된 테이블을 복사 중... 선택 *로:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>5단계(선택 사항): 저장 프로시저 마이그레이션
hello 메모리 내 기능 성능 향상된을 위해 저장된 프로시저를 수정할 수도 있습니다.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저를 사용할 때 고려 사항
고유 하 게 컴파일된 저장된 프로시저 hello 다음 옵션은 T-SQL WITH 절에 있어야 합니다.

* NATIVE_COMPILATION
* SCHEMABINDING: 저장된 프로시저를 hello 의미 테이블 hello 저장 프로시저를 삭제 하지 않는 한 hello 저장 프로시저에 영향을 주므로 어떤 식으로든 변경할 열 정의 가질 수 없습니다.

네이티브 모듈은 트랜잭션 관리에 하나의 큰 [ATOMIC 블록](http://msdn.microsoft.com/library/dn452281.aspx) 을 사용해야 합니다. 명시적 BEGIN TRANSACTION 또는 ROLLBACK TRANSACTION에 대한 역할이 없습니다. 비즈니스 규칙의 위반을 검색 하는 코드를 hello atomic 블록을 종료할 수는 [THROW](http://msdn.microsoft.com/library/ee677615.aspx) 문.

### <a name="typical-create-procedure-for-natively-compiled"></a>고유하게 컴파일된 일반적인 만들기 프로시저
일반적으로 hello T-SQL toocreate 고유 하 게 컴파일된 저장된 프로시저는 서식 파일을 다음 유사한 toohello.

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* TRANSACTION_ISOLATION_LEVEL hello에 대 한 스냅숏은 hello 가장 일반적인 고유 하 게 컴파일된 hello에 대 한 값을 저장 프로시저입니다. 그러나의 하위 집합 hello 다른 값도 지원 됩니다.
  
  * 반복 가능한 읽기
  * 직렬화 가능
* hello sys.languages 뷰에서 hello 언어 값이 있어야 합니다.

### <a name="how-toomigrate-a-stored-procedure"></a>어떻게 toomigrate 저장된 프로시저
hello 마이그레이션 단계입니다.

1. Hello CREATE PROCEDURE 스크립트 toohello 일반 해석 된 저장된 프로시저를 가져옵니다.
2. 해당 헤더 toomatch hello 이전 서식 파일을 다시 작성 합니다.
3. T-SQL 코드 hello 저장 프로시저가 고유 하 게 컴파일된 저장된 프로시저에 지원 되지 않는 기능이 사용 되는지 여부를 확인 합니다. 필요한 경우 해결 방법을 구현합니다.
   
   * 자세한 내용은 [고유하게 컴파일된 저장 프로시저에 대한 마이그레이션 문제](http://msdn.microsoft.com/library/dn296678.aspx)를 참조하세요.
4. SP_RENAME을 사용 하 여 hello 이전 저장된 프로시저를 이름을 바꿉니다. 또는 단순히 삭제합니다.
5. 편집된 프로시저 T-SQL 만들기 스크립트를 실행합니다.

## <a name="step-6-run-your-workload-in-test"></a>6단계: 테스트에서 워크로드 실행
프로덕션 데이터베이스에서 실행 되는 비슷한 toohello 작업 하는 테스트 데이터베이스에서 작업을 실행 합니다. 이 테이블 및 저장된 프로시저에 대 한 hello 메모리 내 기능을 사용 하 여 달성 hello 성능 향상에 도움이 알아낼 수 있습니다.

Hello 워크 로드의 주요 특성은 합니다.

* 동시 연결 수.
* 읽기/쓰기 비율.

tootailor 실행된 hello 테스트 작업 사용해봅니다에 나와 있는 hello 편리한 ostress.exe 도구 [여기](sql-database-in-memory.md)합니다.

hello에서 테스트를 실행 toominimize 네트워크 대기 시간이 동일한 Azure 지역 hello 데이터베이스가 있는 위치입니다.

## <a name="step-7-post-implementation-monitoring"></a>7단계: 사후 실현 모니터링
프로덕션 환경에서 메모리 내에 구현의 hello 성능 효과 모니터링 하는 것이 좋습니다.

* [메모리 내 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).
* [동적 관리 뷰를 사용하여 Azure SQL 데이터베이스 모니터링](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>관련 링크
* [메모리 내 OLTP(메모리 내 최적화)](http://msdn.microsoft.com/library/dn133186.aspx)
* [소개 tooNatively 컴파일 저장 프로시저](http://msdn.microsoft.com/library/dn133184.aspx)
* [메모리 최적화 관리자](http://msdn.microsoft.com/library/dn284308.aspx)

