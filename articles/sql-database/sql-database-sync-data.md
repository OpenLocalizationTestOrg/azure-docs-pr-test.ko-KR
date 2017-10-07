---
title: "aaaSync 데이터 (미리 보기) | Microsoft Docs"
description: "이 개요에서는 Azure SQL 데이터 동기화(미리 보기)를 소개합니다."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>SQL 데이터 동기화를 사용하여 여러 클라우드 및 온-프레미스 데이터베이스의 데이터 동기화

SQL 데이터 동기화는 여러 SQL 데이터베이스 및 SQL Server 인스턴스 간에 양방향으로 선택 하는 hello 데이터를 동기화 할 수 있는 Azure SQL 데이터베이스는 서비스입니다.

데이터 동기화가 기반 하 여 동기화 그룹의 hello 개념으로 합니다. 동기화 그룹은 toosynchronize 데이터베이스의 그룹입니다.

동기화 그룹에는 다음과 같은 속성 hello:

-   hello **동기화 스키마** 어떤 데이터를 동기화에 대해 설명 합니다.

-   hello **동기화 방향** 양방향 수도 있고 한 방향 으로만 전달 될 수 있습니다. 동기화 방향 수 hello 즉, *허브 tooMember* 또는 *멤버 tooHub*, 또는 둘 다 합니다.

-   hello **동기화 간격** 계획 하는 동기화가 발생 합니다.

-   hello **충돌 해결 정책** 될 수 있는 그룹 수준 정책이 *허브 wins* 또는 *멤버 wins*합니다.

데이터 동기화는 허브 및 스포크 토폴로지 toosynchronize 데이터를 사용합니다. Hello 데이터베이스 중 하나에서 정의한 hello 그룹 허브 데이터베이스 hello로 합니다. hello 데이터베이스 hello 나머지는 멤버 데이터베이스입니다. 동기화 허브 hello 및 개별 멤버 사이만 발생합니다.
-   hello **허브 데이터베이스** Azure SQL 데이터베이스 여야 합니다.
-   hello **멤버 데이터베이스** SQL 데이터베이스, 온-프레미스 SQL Server 데이터베이스 또는 Azure 가상 컴퓨터에 SQL Server 인스턴스 수 있습니다.
-   hello **동기화 데이터베이스** hello 메타 데이터 및 로그 포함 데이터 동기화. hello 동기화 데이터베이스에 toobe hello에 Azure SQL 데이터베이스에 대 한 hello 허브 데이터베이스와 동일한 영역입니다. hello 동기화 데이터베이스 만든 고객 및 고객 소유 됩니다.

> [!NOTE]
> 온-프레미스 데이터베이스를 사용 하는 경우 너무[로컬 에이전트를 구성 합니다.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![데이터베이스 간 데이터 동기화](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Toouse 데이터를 동기화 하는 경우

데이터 동기화 데이터 toobe 여러 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스에 걸쳐 toodate를 유지 해야 하는 경우에 유용 합니다. 데이터 동기화에 대 한 hello 주요 사용 사례는 다음과 같습니다.

-   **하이브리드 데이터 동기화:** 데이터 동기화 온-프레미스 데이터베이스와 Azure SQL 데이터베이스 tooenable 하이브리드 응용 프로그램 간에 동기화 된 데이터를 유지할 수 있습니다. 이 기능은 이동 toohello 클라우드를 고려 하는 고 tooput가 toocustomers 제기 될 수 있습니다 Azure에서 응용 프로그램의 일부입니다.

-   **분산된 응용 프로그램:** 대부분의 경우 것이 유용한 tooseparate 다양 한 작업이 다른 데이터베이스에 걸쳐 있습니다. 예를 들어 대형 프로덕션 데이터베이스 있는데 toorun 보고 또는 분석 워크 로드에이 데이터도 필요한 경우 유용한 toohave 이와 같은 추가 작업에 대 한 두 번째 데이터베이스입니다. 이 방법을 사용 하면 프로덕션 작업에 hello 성능에 영향을 최소화합니다. 데이터 동기화 tookeep이 두 데이터베이스 동기화를 사용할 수 있습니다.

-   **전역 분산 응용 프로그램:** 많은 비즈니스는 여러 지역 및 여러 국가 걸쳐 있습니다. 데이터 영역에 닫습니다 최상의 toohave는 toominimize 네트워크 대기 시간, tooyou 합니다. 데이터 동기화 동기화 hello 세계 지역에서 데이터베이스를 쉽게 유지할 수 있습니다.

다음 시나리오는 hello에 대 한 데이터 동기화 권장 됩니다.

-   재해 복구

-   읽기 크기 조정

-   ETL (OLTP tooOLAP)

-   온-프레미스 SQL Server tooAzure SQL 데이터베이스에서 마이그레이션

## <a name="how-does-data-sync-work"></a>데이터 동기화는 어떻게 작동하나요? 

-   **데이터 변경 내용 추적:** 데이터 동기화는 트리거 삽입, 업데이트 및 삭제를 사용하여 변경 내용을 추적합니다. hello 변경 hello 사용자 데이터베이스에 추가 테이블에 기록 됩니다.

-   **데이터 동기화:** 데이터 동기화는 허브 및 스포크 모델에서 설계됩니다. hello 허브에서 동기화 각 멤버와 함께 개별적으로 합니다. Hello 허브에서에서 변경 내용을 다운로드 한 toohello 회원인과 다음 hello 멤버에서 변경 내용을 업로드 toohello 허브입니다.

-   **충돌 해결:** 데이터 동기화는 충돌 해결을 위해 *허브 우선* 또는 *멤버 우선*이라는 두 가지 옵션을 제공합니다.
    -   선택 하는 경우 *허브 wins*, hello 허브에 변경 내용을 hello hello 멤버의 변경 내용을 덮어씁니다.
    -   선택 하는 경우 *멤버 wins*, hello hello 멤버 hello 허브에서 변경 내용 덮어쓰기 변경 합니다. 둘 이상의 멤버가 경우 hello 최종 값 멤버는 먼저 동기화 파일에 따라 달라 집니다.

## <a name="limitations-and-considerations"></a>제한 사항 및 고려 사항

### <a name="performance-impact"></a>성능에 미치는 영향
데이터 동기화 사용 하 여 삽입, 업데이트 및 삭제 트리거 tootrack 변경 합니다. 변경 내용 추적에 대 한 hello 사용자 데이터베이스에 테이블 생성 됩니다. 이러한 변경 내용 추적 작업은 데이터베이스 워크로드에 영향을 줍니다. 서비스 계층을 평가하고 필요한 경우 업그레이드합니다.

### <a name="eventual-consistency"></a>결과적 일관성
데이터 동기화가 트리거 기반이기 때문에 트랜잭션 일관성이 보장되지 않습니다. Microsoft는 결과적으로 모든 변경 내용을 적용하고 데이터 동기화가 데이터 손실을 발생하지 않도록 보장합니다.

### <a name="unsupported-data-types"></a>지원되지 않는 데이터 형식

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection(XML 지원)

-   Cursor, Timestamp, Hierarchyid

### <a name="requirements"></a>요구 사항

-   각 표에는 기본 키가 있어야 합니다.

-   테이블 기본 키 hello 없는 id 열을 가질 수 없습니다.

-   개체 (데이터베이스, 테이블 및 열)의 hello 이름을 hello 인쇄 가능한 문자 마침표 (.), 왼쪽 대괄호 (), 포함 또는 오른쪽 대괄호 (]) 수 없습니다.

### <a name="limitations-on-service-and-database-dimensions"></a>서비스 및 데이터베이스 차원에 대한 제한 사항

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **차원**                                                      | **제한**              | **해결 방법**              |
| 데이터베이스가 속할 수 있는 동기화 그룹의 최대 수입니다.       | 5                      |                             |
| 단일 동기화 그룹에서 끝점의 최대 수입니다.              | 30                     | 여러 동기화 그룹 만들기 |
| 단일 동기화 그룹에서 온-프레미스 끝점의 최대 수입니다. | 5                      | 여러 동기화 그룹 만들기 |
| 데이터베이스, 테이블, 스키마 및 열 이름                       | 이름당 50자 |                             |
| 동기화 그룹의 표                                          | 500                    | 여러 동기화 그룹 만들기 |
| 동기화 그룹에서 표의 열                              | 1000                   |                             |
| 표의 데이터 행 크기                                        | 24Mb                  |                             |
| 최소 동기화 간격                                           | 5분              |                             |

## <a name="common-questions"></a>일반적인 질문

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>데이터 동기화에서 데이터를 동기화하는 빈도는 어떻게 되나요? 
hello 최소 빈도 5 분 마다입니다.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>온-프레미스 데이터베이스에만 해당 SQL Server 간의 데이터 동기화 toosync를 사용할 수 있습니까? 
직접 끌 수는 없습니다. 하지만 동기화 할 수 있습니다 하지 온-프레미스 SQL Server 데이터베이스 간에 직접 Azure에서 허브 데이터베이스를 만들어 한 다음 hello 온-프레미스 데이터베이스 toohello 동기화 그룹을 추가 합니다.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>내 프로덕션 데이터베이스 tooan 빈 데이터베이스에서 데이터 동기화 tooseed 데이터를 사용 하 여을 동기화 한 다음 할 수 있습니까? 
예. 원래 hello에서 스크립팅 하 여 hello 새 데이터베이스에 수동으로 hello 스키마를 만듭니다. Hello 스키마를 만든 후 hello 테이블 tooa 동기화 그룹 toocopy hello 데이터를 추가 하 고 동기화 된 상태로 유지 합니다.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>내가 만들지 않은 테이블이 표시되는 이유는 무엇인가요?  
데이터 동기화는 변경 내용 추적을 위해 데이터베이스에 추가 테이블을 만듭니다. 해당 테이블을 삭제하지 마세요. 삭제하면 데이터 동기화의 작동이 중지됩니다.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>라고 하는 오류 메시지가 수신 됨 "hello 열에 NULL hello 값을 삽입할 수 없습니다 \<열\>합니다. 열에는 Null을 사용할 수 없습니다."라는 오류 메시지를 받았습니다. 그, 및 hello 오류 어떻게 해결할 수 있습니까? 
이 오류 메시지는 hello 두 다음 문제 중 하나를 나타냅니다.
1.  기본 키가 없는 테이블이 있을 수 있습니다. 기본 키 tooall hello 테이블 추가 toofix이 문제를 동기화 하는 합니다.
2.  CREATE INDEX 문에 WHERE 절이 있을 수 있습니다. 동기화에서는 이 조건이 처리되지 않습니다. toofix이이 문제를 hello WHERE 절을 제거 하거나 수동으로 변경할 hello tooall 데이터베이스. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>데이터 동기화에서는 어떻게 순환 참조가 처리되나요? 즉, hello 동일한 데이터를 여러 동기화 그룹 동기화 시점과 계속 결과적으로 변경?
데이터 동기화에서는 순환 참조가 처리되지 않습니다. 있는지 tooavoid 수 하 합니다. 

## <a name="next-steps"></a>다음 단계

SQL 데이터 동기화에 대한 자세한 내용은 다음을 참조하세요.

-   [SQL 데이터 동기화 시작](sql-database-get-started-sql-data-sync.md)

-   완전 한 보여 주는 PowerShell 예제 tooconfigure SQL 데이터 동기화 방법:
    -   [여러 Azure SQL 데이터베이스 간에 toosync PowerShell을 사용 하 여](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Azure SQL 데이터베이스와 SQL Server 온-프레미스 데이터베이스 간의 toosync PowerShell을 사용 하 여](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Hello 전체 SQL 데이터 동기화 기술 설명서를 다운로드 합니다.](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Hello SQL 데이터 동기화 REST API 설명서 다운로드](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

SQL Database에 대한 자세한 내용은 다음을 참조하세요.

-   [SQL 데이터베이스 개요](sql-database-technical-overview.md)

-   [데이터베이스 수명 주기 관리](https://msdn.microsoft.com/library/jj907294.aspx)
