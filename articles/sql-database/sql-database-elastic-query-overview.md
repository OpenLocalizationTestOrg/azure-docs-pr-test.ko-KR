---
title: "aaaAzure SQL 데이터베이스 탄력적 쿼리 개요 | Microsoft Docs"
description: "Hello 탄력적 쿼리 기능 개요"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Azure SQL Database 탄력적 쿼리 개요(미리 보기)
(미리 보기)에서 hello 탄력적 쿼리 기능을 toorun Azure SQL 데이터베이스에서 여러 데이터베이스에 걸쳐 있는 Transact SQL 쿼리를 사용 합니다. 있습니다 tooperform 데이터베이스 간 쿼리 tooaccess 원격 테이블 및 tooconnect Microsoft 및 타사 도구 (Excel, PowerBI, Tableau, 등) tooquery 여러 데이터베이스가 있는 데이터 계층에 걸쳐 있습니다. 이 기능을 사용 하 여 SQL 데이터베이스에서 쿼리 toolarge 데이터 계층을 확장할 수 있으며 비즈니스 인텔리전스 (BI) 보고서에서 hello 결과 시각화 수도 있습니다.


## <a name="why-use-elastic-queries"></a>탄력적 쿼리를 사용하는 이유

**Azure SQL 데이터베이스**

완전히 T-SQL로 Azure SQL 데이터베이스에서 쿼리합니다. 이렇게 하면 원격 데이터베이스의 읽기 전용 쿼리가 가능합니다. SQL Server 고객 toomigrate 응용 프로그램 3-및 4 부분으로 구성 이름 또는 연결 된 서버 tooSQL DB 사용 하 여 현재 온-프레미스에 대 한 옵션 제공 합니다.

**표준 계층에서 사용가능**

탄력적 쿼리는 또한 toohello 프리미엄 성능 계층에 있는 hello 표준 성능 계층에 지원 됩니다. 더 낮은 성능 계층에 대 한 성능 제한에 아래 미리 보기 제한 사항에 hello 섹션을 참조 합니다.

**푸시 tooremote 데이터베이스**

탄력적 쿼리 실행에 대 한 SQL 매개 변수 toohello 원격 데이터베이스를 푸시할 이제 수 있습니다.

**저장 프로시저 실행**

[sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)를 사용하여 원격 저장된 프로시저 호출 또는 원격 함수를 실행합니다.

**유연성**

외부 테이블을 탄력적 쿼리 tooremote 테이블과 다른 스키마 또는 테이블 이름을 참조할 이제 수 있습니다.

## <a name="elastic-query-scenarios"></a>탄력적 쿼리 시나리오

hello 목표 toofacilitate 쿼리 하는 여러 데이터베이스에는 하나의 전체 결과 행을 제공 하는 시나리오입니다. hello 쿼리 중 하나를 구성할 수 hello 사용자 또는 응용 프로그램에서 직접 또는 직접 도구를 통해 되지 않은 연결 된 toohello 데이터베이스입니다. 이것은 보고서를 만들거나, 유료 BI 또는 데이터 통합 도구나 변경할 수 없는 모든 소프트웨어를 사용할 때 특히 유용합니다. 유연한 쿼리를 Excel, PowerBI, Tableau, 또는 cognos와 같은 도구에서 SQL Server 연결 경험을 친숙 한 hello를 사용 하 여 여러 데이터베이스에 걸쳐 쿼리할 수 있습니다.
탄력적 쿼리 쉽게 액세스할 수 있도록 SQL Server Management Studio 또는 Visual Studio에서 발급 하는 쿼리를 통해 데이터베이스의 전체 컬렉션 tooan 있으며이 Entity Framework 또는 기타 ORM 환경에서 데이터베이스 간 쿼리를 용이 하 게 합니다. 그림 1에 나와 있는 응용 프로그램을 클라우드를 기존 시나리오 (hello를 사용 하 여 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)) 하며 확장 데이터에 빌드 계층 및 데이터베이스 간 보고용 사용 되는 탄력적 쿼리 합니다.

**그림 1** 수평 확장된 데이터 계층에서 사용하는 탄력적 쿼리

![수평 확장된 데이터 계층에서 사용하는 탄력적 쿼리][1]

탄력적 쿼리에 대 한 고객 시나리오는 토폴로지에 따라 hello 특징이 있습니다.

* **수직 분할에서 데이터베이스 간 쿼리** (토폴로지 1): hello 데이터는 많은 데이터 계층의 데이터베이스 간에 수직 분할 됩니다. 일반적으로 서로 다른 테이블 집합이 서로 다른 데이터베이스에 상주합니다. 즉, 해당 hello 스키마는 다른 데이터베이스에서 다릅니다. 예를 들어, 재고의 모든 테이블은 한 데이터베이스 안에 있지만 모든 회계 관련 테이블은 보조 데이터베이스에 있습니다. 이 토폴로지를 사용 하는 일반적인 사용 사례는 하나의 간에 tooquery 또는 toocompile 보고서 테이블 여러 데이터베이스에 대해 필요합니다.
* **가로 Partitioning-분할** (토폴로지 2): 데이터를 수평으로 분할 되 수평 확장 된 데이터에서 toodistribute 행 계층입니다. 이 접근 방식 hello 스키마는 참여 하는 모든 데이터베이스에 동일 합니다. 이 방법을 "분할"이라고도 합니다. 분할을 수행할 수 있습니다 및 (1) hello 탄력적 데이터베이스 도구 라이브러리 또는 (2) 자체 분할을 사용 하 여 관리 합니다. 탄력적 쿼리는 여러 분할 영역에 걸쳐 사용 되는 tooquery 또는 컴파일 reports입니다.

> [!NOTE]
> 탄력적 쿼리 대부분 hello 처리의 hello 데이터 계층에서 수행 될 수 있는 비 정기적인 보고 시나리오에 가장 적합 합니다. 쿼리가 보다 복잡한 과도한 보고 작업 부하 또는 데이터 웨어하우징 시나리오의 경우, [Azure SQL 데이터 웨어하우스](https://azure.microsoft.com/services/sql-data-warehouse/)사용을 고려합니다.
>  

## <a name="vertical-partitioning---cross-database-queries"></a>수직 분할 – 데이터베이스 간 쿼리

코딩, toobegin 참조 [데이터베이스 간 쿼리 (수직 분할) 시작](sql-database-elastic-query-getting-started-vertical.md)합니다.

탄력적 쿼리는 SQL 데이터베이스 사용 가능한 tooother SQL 데이터베이스에 있는 데이터에 사용 되는 toomake 수 있습니다. 따라서 다른 원격 SQL 데이터베이스에서 쿼리를를 하나의 데이터베이스 toorefer tootables 수 있습니다. hello 첫 번째 단계는 toodefine 각 원격 데이터베이스에 대 한 외부 데이터 원본입니다. hello 외부 데이터 원본이 toogain 액세스 tootables hello 원격 데이터베이스에 있는 원하는 hello 로컬 데이터베이스에 정의 되었습니다. 변경이 hello 원격 데이터베이스에 필요 하지 않으면 합니다. 시나리오에 대 한 일반적인 수직 분할 서로 다른 데이터베이스는 서로 다른 스키마를 탄력적 쿼리 수 사용된 tooimplement tooreference 데이터 액세스 등의 일반적인 사용 사례 수 및 데이터베이스 간 쿼리 합니다.

> [!IMPORTANT]
> 사용자는 모든 외부 데이터 원본 ALTER 권한이 있어야 합니다. 이 사용 권한은 hello ALTER DATABASE 권한이 포함 되어 있습니다. ALTER ANY EXTERNAL DATA SOURCE 권한은 필요한 toorefer toohello 데이터 원본으로 사용 합니다.
>

**참조 데이터**: hello 토폴로지 참조 데이터 관리에 사용 됩니다. 아래 hello 그림에서 두 개의 테이블 (t 1과 t 2)에 참조 데이터는 전용된 데이터베이스에 저장 됩니다. 유연한 쿼리를 사용 하면 이제 액세스할 수 있습니다 테이블 t 1과 T2 원격으로 다른 데이터베이스에서 hello 그림에 나와 있는 것 처럼 합니다. 참조 테이블이 작거나 참조 테이블에 대한 원격 쿼리에 선택적 조건자가 있으면 토폴로지 1을 사용합니다.

**그림 2** 수직으로 분할-탄력적 쿼리 tooquery 참조 데이터 사용

![수직 분할-탄력적 쿼리 tooquery 참조 데이터 사용][3]

**데이터베이스 간 쿼리**: 탄력적 쿼리를 사용하면 여러 SQL 데이터베이스 간 쿼리가 필요한 사용 사례를 구현할 수 있습니다. 그림 3에는 CRM, 재고, HR 및 제품 등, 서로 다른 4가지 데이터베이스가 있습니다. Hello 데이터베이스 중 하나에서 수행 하는 쿼리도 필요한 액세스 tooone 또는 다른 데이터베이스 hello 모두. 탄력적 쿼리를 사용 하면 각 hello 4 개의 데이터베이스에 몇 가지 간단한 DDL 문을 실행 하 여이 위한 데이터베이스를 구성할 수 있습니다. 이 일회성 구성 후 액세스 tooa 원격 테이블은을 T-SQL 쿼리 또는 BI 도구에서 tooa 로컬 테이블을 참조 합니다. 이 방법은 hello 원격 쿼리가 큰 결과 반환 하지 않는 경우에 권장 됩니다.

**그림 3** 수직으로 분할-탄력적 쿼리 tooquery를 사용 하 여 다양 한 데이터베이스에 걸쳐

![수직 분할-탄력적 쿼리 tooquery를 사용 하 여 다양 한 데이터베이스에 걸쳐][4]

hello 다음 단계 탄력적 데이터베이스 쿼리 구성 hello로 원격 SQL 데이터베이스에 액세스 tooa 테이블 있는 동일 해야 하는 수직 분할 시나리오에 대 한 스키마:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource of type **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

DDL 문 hello를 실행 한 후 로컬 테이블 것 처럼 "mytable" hello 원격 테이블에 액세스할 수 있습니다. Azure SQL 데이터베이스 자동으로 연결 toohello 원격 데이터베이스를 열고, hello 원격 데이터베이스에 사용자 요청을 처리 하 고 hello 결과 반환 합니다.

## <a name="horizontal-partitioning---sharding"></a>행 분할 - 분할
탄력적 쿼리 tooperform는 분할 된, 즉, 수평 분할을 통해 보고 작업을 사용 하 여 데이터 계층 필요는 [탄력적 데이터베이스 분할 맵은](sql-database-elastic-scale-shard-map-management.md) hello 데이터 계층의 toorepresent hello 데이터베이스. 일반적으로 단일 분할 맵은는이 시나리오에서 사용 하 고 탄력적 쿼리 기능 (헤드 노드)를 사용 하 여 전용된 데이터베이스 역할 hello 보고 쿼리에 대 한 진입점을 합니다. 이 전용된 데이터베이스에만 액세스 toohello 분할 맵이 필요합니다. 그림 4에는이 토폴로지 및 hello 탄력적 쿼리 데이터베이스 및 분할 맵 사용 하 여 해당 구성을 보여 줍니다. hello 데이터베이스 hello 데이터 계층의 모든 Azure SQL 데이터베이스 버전 또는 에디션에 될 수 있습니다. Hello 탄력적 데이터베이스 클라이언트 라이브러리 및 분할 맵 만들기에 대 한 자세한 내용은 참조 [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md)합니다.

**그림 4** 행 분할 - 탄력적 쿼리를 사용하여 분할된 데이터 계층에 대해 보고

![행 분할 - 탄력적 쿼리를 사용하여 분할된 데이터 계층에 대해 보고][5]

> [!NOTE]
> 데이터베이스 탄력적 쿼리 (헤드 노드) 별도 데이터베이스 이거나 hello 수 해당 호스트 hello 분할 맵을 데이터베이스 동일 합니다. 을 선택 하면 모든 구성 해야 해당 데이터베이스의 해당 서비스, 성능 계층은 충분 한 상위 수준 toohandle 예상 hello 양의 로그인/쿼리 요청 합니다.

hello 다음 단계 탄력적 데이터베이스 쿼리 구성에 대 한 수평 분할 해야 하는 시나리오 액세스 tooa 집합이 테이블에 있는 일반적으로 여러 개의 원격 SQL 데이터베이스에:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* 만들기는 [분할 맵은](sql-database-elastic-scale-shard-map-management.md) hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 데이터 계층을 나타내는입니다.   
* [CREATE/DROP EXTERNA DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)**SHARD_MAP_MANAGER** 형식의 mydatasource
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

다음이 단계를 수행한 후 로컬 테이블 것 처럼 "mytable" hello 수평 분할 된 테이블을 액세스할 수 있습니다. Azure SQL 데이터베이스 자동으로 여러 병렬 연결 toohello 원격 데이터베이스 hello 테이블은 물리적으로 저장 위치, hello 원격 데이터베이스의 hello 요청을 처리을 열고 hello 결과 반환 합니다.
Hello 수평 분할 시나리오에서 확인할 수 있습니다에 필요한 hello 단계에 대 한 자세한 내용은 [수평 분할에 쿼리를 탄력적](sql-database-elastic-query-horizontal-partitioning.md)합니다.

코딩, toobegin 참조 [탄력적 쿼리 행 (분할) 분할에 대 한 시작](sql-database-elastic-query-getting-started.md)합니다.

## <a name="t-sql-querying"></a>T-SQL 쿼리
외부 데이터 원본 및 외부 테이블을 정의 외부 테이블 정의 되어 있는 일반 SQL Server 연결 문자열 tooconnect toohello 데이터베이스 사용할 수 있습니다. 실행할 수 있습니다 다음 T-SQL 문을 외부 테이블을 통해 해당 연결에서 아래에 설명 된 hello 같은 제한 사항이 있습니다. 에 대 한 hello 설명서 항목에서 자세한 내용 및 T-SQL 쿼리 예제를 찾을 수 있습니다 [수평 분할](sql-database-elastic-query-horizontal-partitioning.md) 및 [수직 분할](sql-database-elastic-query-vertical-partitioning.md)합니다.

## <a name="connectivity-for-tools"></a>도구에 대한 연결
응용 프로그램 및 외부 테이블을가지고 있는 BI 또는 데이터 통합 도구 toodatabases 일반 SQL Server 연결 문자열 tooconnect를 사용할 수 있습니다. SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다. 연결 되 면 toohello 탄력적 데이터베이스와 hello 외부 테이블 쿼리 해당 데이터베이스에 있는 것 처럼 작업할 때와 다른 SQL Server 데이터베이스 연결 toowith 도구 참조 합니다.

> [!IMPORTANT]
> 탄력적 쿼리를 통해 Azure Active Directory를 사용한 인증은 현재 지원되지 않습니다.
> 
> 

## <a name="cost"></a>비용
탄력적 쿼리는 Azure SQL 데이터베이스는 데이터베이스의 hello 비용에 포함 되어 있습니다. 원격 데이터베이스에에서 있는 다른 데이터 센터 탄력적 쿼리 끝점 hello 보다 토폴로지는 지원 되지만 원격 데이터베이스의 데이터 유출 일반 요금이 청구 됩니다는 [Azure 속도](https://azure.microsoft.com/pricing/details/data-transfers/)합니다.

## <a name="preview-limitations"></a>미리 보기 제한 사항
* 첫 번째 탄력적 쿼리를 실행 차지 tooa hello 표준 성능 계층에 몇 분입니다. 이 시간은 필요한 tooload hello 탄력적 쿼리 기능입니다. 더 높은 성능 계층을 사용 하 여 로드 성능을 향상 시킵니다.
* 외부 데이터 원본이나, SSMS 또는 SSDT에서의 외부 테이블 스크립팅은 아직 지원되지 않습니다.
* SQL DB 가져오기/내보내기는 외부 데이터 원본 및 외부 테이블을 아직 지원하지 않습니다. 가져오기/내보내기 toouse 해야 할 경우 내보내기 전에 이러한 개체를 삭제 한 다음 가져온 후 다시 만듭니다.
* 탄력적 쿼리 현재만 읽기 전용 액세스 tooexternal 테이블 지원합니다. 하지만 사용할 수 있습니다 전체 T-SQL 기능 hello 데이터베이스에서 hello 외부 테이블 정의 됩니다. 이 예를 들어, 임시 결과 유지 하려면을 선택 하 여 예: < 열 > _ 목록 < local_table >에 유용한 방법 tooexternal 테이블 참조는 hello 탄력적 쿼리 데이터베이스에서 저장 프로시저 toodefine 수 있습니다.
* nvarchar(max)를 제외하고 LOB 형식은 외부 테이블 정의에서 지원되지 않습니다. 이 문제를 해결 hello LOB 형식을 nvarchar (max)로 캐스팅 하는 hello 원격 데이터베이스에 뷰를 만들, hello 기본 테이블 대신 hello 보기를 통해 외부 테이블을 정의 및 쿼리에 hello 원래 LOB 형식으로 다시 캐스팅 수 있습니다.
* 외부 테이블에 대한 열 통계는 현재 지원되지 않습니다. 테이블 통계는 지원 되기는 하지만 toobe 수동으로 만든 필요 합니다.

## <a name="feedback"></a>사용자 의견
하십시오 경험에 대 한 피드백 탄력적 쿼리로 공유 Stackoverflow 컴퓨터나 Disqus 아래 hello MSDN 포럼에 있습니다. 우리는 모든 종류의 hello 서비스 (결함, 스럽게, 기능 간격)에 대 한 사용자 의견 수집 합니다.

## <a name="next-steps"></a>다음 단계

* 수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.
* 수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.
* 행 분할(분할) 자습서는 [행 분할(분할)을 위한 탄력적 데이터베이스 쿼리 시작하기](sql-database-elastic-query-getting-started.md)를 참조하세요.
* 행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.
* 단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
