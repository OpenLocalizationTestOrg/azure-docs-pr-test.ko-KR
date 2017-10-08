---
title: "SQL 데이터베이스-메모리 내 기술 aaaAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스-메모리 내 기술 hello 성능을 트랜잭션 및 분석 워크 로드에 크게 향상 시킬 합니다. 자세한 내용은 방법 tootake 이러한 기술 활용 합니다."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>SQL Database에서 메모리 내 기술을 사용하여 성능 최적화

Azure SQL Database의 메모리 내 기술을 사용하여 트랜잭션(OLTP(온라인 트랜잭션 처리)), 분석(OLAP(온라인 분석 처리)), 혼합(HTAP(하이브리드 트랜잭션/분석 처리))과 같은 다양한 워크로드의 성능을 향상할 수 있습니다. 때문에 더 효율적인 쿼리 및 트랜잭션 처리 hello, 메모리 내 기술 수 있도록 도와 드릴 tooreduce 비용입니다. 일반적으로 가격 책정 계층 hello 데이터베이스 tooachieve 성능 향상의 tooupgrade hello가 필요는 없습니다. 일부 경우에도 수 있습니다 hello 그래도 메모리 내 기술을 통한 성능 향상을 표시 하는 동안 가격 책정 계층을 줄입니다.

다음은 메모리 내 OLTP toosignificantly 성능 향상을 작업 하는 방법의 두 가지 예입니다.

- 메모리 내 OLTP를 사용 하 여 [쿼럼 비즈니스 솔루션 70 %Dtu 개선 하는 동안 수 toodouble 프로그램 작업 했습니다](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)합니다.
    - 여기서 DTU는 *데이터베이스 처리량 단위*를 의미하며 리소스 소비량의 측정값을 포함합니다.
- hello 다음 비디오에서 보여 주는 샘플 작업과 리소스 소비량에서 향상: [Azure SQL 데이터베이스 비디오에서 메모리 내 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)합니다.
    - 자세한 내용은 hello 블로그 게시물을 참조 하십시오.: [Azure SQL 데이터베이스 블로그 게시물에서 메모리 내 OLTP](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

메모리 내 기술 hello 프리미엄 계층에서는 프리미엄 탄력적 풀에서 데이터베이스를 비롯 한 모든 데이터베이스에서 사용할 수 있는 합니다.

hello 다음 비디오에서는 설명 잠재적인 성능 향상 이점을 얻으려면 Azure SQL 데이터베이스의 메모리 내 기술 사용 합니다. 항상 볼 수 있는 hello 성능 향상 hello 작업 부하 및 데이터를 hello 데이터베이스의 액세스 패턴의 hello 특성 등의 많은 요인에 따라 집니다 등에입니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Azure SQL 데이터베이스의 메모리 내 기술 다음 hello 사용:

- *메모리 내 OLTP*은 처리량을 증가시키고 트랜잭션 처리에 대한 대기 시간을 감소시킵니다. 메모리 내 OLTP를 활용하는 시나리오는 거래와 게임, 이벤트 또는 IoT 장치의 데이터 수집, 캐싱, 데이터 부하 및 임시 테이블과 테이블 변수 시나리오와 같은 처리량 많은 트랜잭션을 처리하는 경우입니다.
- *클러스터형 columnstore 인덱스* (too10 시간)을 사용 하면 저장소 공간을 줄이는 및 보고 및 분석 쿼리의 성능을 향상 합니다. 팩트 테이블을 데이터 마트 toofit에 더 많은 데이터에서에서 사용할 데이터베이스 수 있으며 성능을 향상 시킬 수 있습니다. 또한 운영 데이터베이스 tooarchive에서 기록 데이터와 사용할 수 있으며 too10 시간 수 tooquery 더 많은 데이터를 사용할 수 있습니다.
- *비클러스터형 columnstore 인덱스* HTAP 도움말에 대 한 비용이 많이 드는 추출, 변환 및 로드 (ETL) 프로세스 hello 필요 toorun 하지 않고 직접 데이터베이스 있습니다 toogain 실시간으로 파악할 hello 작동 쿼리를 통해 비즈니스 및이 대기 에 대 한 데이터 웨어하우스 toobe hello 채워집니다. 비클러스터형 columnstore 인덱스는 hello 운영 워크 로드에 hello 미치는 영향을 줄이면서 hello OLTP 데이터베이스에서 분석 쿼리 실행 속도가 매우 빠르지만 허용 합니다.
- Columnstore 인덱스가 있는 메모리 액세스에 최적화 된 테이블의 hello 조합을 할 수도 있습니다. 이 조합 tooperform 매우 빠른 트랜잭션 처리, 수 및 너무*동시에* 실행된 분석 쿼리를 매우 신속 하 게 hello에 동일 데이터입니다.

Columnstore 인덱스와 메모리 내 OLTP 일부일 hello SQL Server 제품의 2012 및 2014 년 이후 각각. Azure SQL 데이터베이스 및 SQL Server 공유 hello 동일한 메모리 내 기술 구현 합니다. 앞으로 이러한 기술에 대한 새로운 기능을 SQL Server에 배포하기 전에 Azure SQL Database에서 먼저 릴리스합니다.

이 항목에 메모리 내 OLTP와 columnstore 인덱스를 특정 tooAzure SQL 데이터베이스의 측면에 설명 하 고 예제도 포함 되어:
- 저장소 및 데이터 크기 제한에 이러한 기술의 hello 영향을 볼 수 있습니다.
- Toomanage hello 다른 가격대 간의 이러한 기술을 사용 하는 데이터베이스의 이동을 hello 하는 방법을 확인할 수 있습니다.
- 메모리 내 OLTP와 Azure SQL 데이터베이스에서 columnstore 인덱스의 hello 사용을 보여 주는 두 개의 샘플이 표시 됩니다.

Hello 리소스에 대 한 자세한 내용은 다음을 참조 하십시오.

Hello 기술에 대 한 자세한 정보:

- [메모리 내 OLTP 개요 및 사용 시나리오](https://msdn.microsoft.com/library/mt774593.aspx) (참조 toocustomer 사례 연구 및 시작 정보 tooget 포함)
- [메모리 내 OLTP에 대한 설명서](http://msdn.microsoft.com/library/dn133186.aspx)
- [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)
- HTAP(하이브리드 트랜잭션/분석 처리) 즉, [실시간 운영 분석](https://msdn.microsoft.com/library/dn817827.aspx)

메모리 내 oltp는 빠른 입문: [빠른 시작 1: 더 빠르게 T-SQL 성능을 위한 메모리 내 OLTP 기술](http://msdn.microsoft.com/library/mt694156.aspx) (다른 문서 toohelp 시작 하는 데)

Hello 기술에 대 한 심층 분석 비디오:

- [Azure SQL 데이터베이스에서 메모리 내 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (성능의 데모 포함 된 이점 및 단계 tooreproduce 이러한 결과 사용자가 직접)
- [메모리 내 OLTP 비디오: 무엇 인지 및/하는 경우 어떻게 toouse 것](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Columnstore 인덱스: Ignite 2016의 메모리 내 분석 비디오](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>저장소 및 데이터 크기

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>메모리 내 OLTP의 데이터 크기 및 저장 제한

메모리 내 OLTP는 사용자 데이터를 저장하는 데 사용되는 메모리에 최적화된 테이블을 포함합니다. 이러한 테이블은 메모리에 필요한 toofit입니다. 메모리 hello SQL 데이터베이스 서비스에서 직접 관리 하기 때문에 사용자 데이터에 대 한 할당량의 hello 개념을 했습니다. 이 개념은 참조 tooas *메모리 내 OLTP 저장소*합니다.

지원되는 독립 실행형 데이터베이스 가격 책정 계층 및 탄력적 풀 가격 책정 계층은 각각 일정량의 메모리 내 OLTP 저장소를 포함합니다. 작성 hello 시 얻게 저장소는 기가바이트 모든 125 개의 데이터베이스 트랜잭션 단위 (DTUs) 또는 탄력적 데이터베이스에 대해 트랜잭션 Edtu (단위).

hello [SQL 데이터베이스 서비스 계층](sql-database-service-tiers.md) 기술 자료 문서에 지원 되는 각 독립 실행형 데이터베이스 및 가격 책정 계층 탄력적 풀에 사용할 수 있는 hello 메모리 내 OLTP 저장소의 hello 공식 목록입니다.

메모리 내 OLTP 저장소 캡을 향해 항목 수가 다음 hello:

- 메모리 최적화된 테이블 및 테이블 변수의 활성 사용자 데이터 행입니다. 오래 된 행 버전 hello 캡을 차지 하지 않습니다는 참고 사항
- 메모리 최적화된 테이블에 대한 인덱스입니다.
- ALTER TABLE 작업의 작업 오버헤드입니다.

Hello cap 발생 하면 할당량 초과 오류를 표시 하 고 수 tooinsert 또는 update 데이터는 더 이상. toomitigate이이 오류 데이터를 삭제 하거나 hello 가격 책정 계층 hello 데이터베이스 또는 풀을 늘리십시오.

메모리 내 OLTP 저장소 사용을 모니터링 하 고 hello 단면에 거의 도달 하면 경고를 구성 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터에서 메모리 내 저장소](sql-database-in-memory-oltp-monitoring.md)합니다.

#### <a name="about-elastic-pools"></a>탄력적 풀에 대한 정보

탄력적 풀과 메모리 내 OLTP 저장소 hello hello 풀의 모든 데이터베이스에서 공유 됩니다. 따라서 한 데이터베이스의 hello 사용 다른 데이터베이스에 영향을 줄 수 있습니다. 두 가지 해결 방법이 있습니다.

- 최대-eDTU 데이터베이스에 대 한 전체 hello 풀에 대 한 hello eDTU 수 보다 낮은 구성 합니다. 이 최대 풀 hello toohello eDTU 수입니다. 해당 하는 toohello 크기에에서 모든 데이터베이스에서 hello 메모리 내 OLTP 저장소 사용률, 대문자입니다.
- 최소 eDTU를 0보다 크게 구성합니다. 이 최소 보장 hello toohello 해당 하는 사용 가능한 메모리 내 OLTP 저장소 양을 hello 풀의 각 데이터베이스에 최소 eDTU를 구성 합니다.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>columnstore 인덱스의 데이터 크기 및 저장소

Columnstore 인덱스는 메모리에 필요한 toofit 되지 않습니다. 따라서 hello 인덱스의 hello 크기는 hello에 설명 되어 있는 hello 최대 전체 데이터베이스 크기에만 hello [SQL 데이터베이스 서비스 계층](sql-database-service-tiers.md) 문서.

클러스터형된 columnstore 인덱스를 사용할 때는 칼럼 형식 압축 hello 기본 테이블 저장소에 사용 됩니다. 이러한 압축 hello 데이터베이스에 더 많은 데이터를 표시할 수 있습니다는 사용자 데이터의 hello 저장소 공간을 상당히 줄일 수 있습니다. Hello 압축으로 더 높아질 수 있습니다 및 [보관 칼럼 형식 압축](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)합니다. hello 압축량 얻을 수 있는 hello 데이터의 hello 특성에 따라 달라 집니다 하지만 10 번 hello 압축도 드물지 않습니다.

예를 들어 최대 크기인 1tb (테라바이트)를 사용 하 여 데이터베이스 있고 columnstore 인덱스를 사용 하 여 10 회 hello 압축을 얻을 경우 hello 데이터베이스의 10TB의 사용자 데이터의 합계를 넣을 수 있습니다.

비클러스터형 columnstore 인덱스를 사용할 때는 hello 기본 테이블은 여전히 hello 일반적인 행 저장소 형식으로 저장 됩니다. 따라서 hello 저장소 분량이 절약 크기가 클러스터형된 columnstore 인덱스와 되지 않습니다. 그러나 기존의 비클러스터형 인덱스의 수를 단일 columnstore 인덱스로 대체 하는 경우에 여전히 hello 테이블에 대 한 hello 저장소 공간에는 전반적인 절감을 볼 수 있습니다.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>가격 책정 계층 간의 메모리 내 기술을 사용하여 데이터베이스 이동

존재 하지 않습니다 비 호환성 문제 또는 기타 문제 tooa 더 높은 가격 책정 계층을와 같은 표준 tooPremium에서 업그레이드 하는 경우. hello 사용할 수 있는 기능 및 리소스만 증가 합니다.

하지만 가격 책정 계층으로 다운 그레이드 hello 데이터베이스 저하 될 수 있습니다. hello 영향 때 특히 tooStandard Premium에서에서 다운 그레이드 하면 명백한 또는 기본 데이터베이스에 메모리 내 OLTP 개체를 포함 합니다. 메모리 액세스에 최적화 된 테이블 및 columnstore 인덱스를 사용할 수 없는 hello 다운 그레이드 한 후 (경우에 계속 표시)입니다. hello hello 가격 책정 계층 탄력적 풀의 또는 데이터베이스 이동 In-memory 기술과 함께 사용 하는 표준 또는 기본 탄력적인 풀을 낮추면 하는 경우 동일한 고려 사항이 적용 됩니다.

### <a name="in-memory-oltp"></a>메모리 내 OLTP

*TooBasic/표준 다운 그레이드*: 메모리 내 OLTP는 hello Standard 또는 Basic 계층에 있는 데이터베이스에서 지원 되지 않습니다. 또한 가능한 toomove 모든 메모리 내 OLTP 개체 toohello Standard 또는 Basic 계층에 있는 데이터베이스는 없습니다.

Hello 데이터베이스 tooStandard/Basic를 다운 그레이드 하기 전에 모든 메모리 액세스에 최적화 된 테이블 및 테이블 형식 뿐 아니라 모든 고유 하 게 컴파일된 T-SQL 모듈을 제거 합니다.

지정된 된 데이터베이스는 메모리 내 OLTP를 지원 하는지 여부를 프로그래밍 방식으로 toounderstand가 있습니다. Hello 다음 TRANSACT-SQL 쿼리를 실행할 수 있습니다.

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Hello 쿼리가 반환 하는 경우 **1**은이 데이터베이스에서 메모리 내 OLTP를 지원 합니다.


*Tooa 낮은 Premium 계층을 다운 그레이드*: 가격 책정 계층 hello 데이터베이스의 hello와 관련 된 또는 hello 탄력적 풀에서 사용할 수 있는 hello 메모리 내 OLTP 저장소 안에 메모리 액세스에 최적화 된 테이블의 데이터에에서 맞아야 합니다. 가격 책정 계층 toolower hello를 시도 하거나 hello 데이터베이스를 이동 하는 경우 사용할 수 있는 충분 한 메모리 내 OLTP 저장소 풀에 없는, hello 작업이 실패 합니다.

### <a name="columnstore-indexes"></a>Columnstore 인덱스

*TooBasic 또는 표준 다운 그레이드*: Standard 또는 Basic 계층을 hello Columnstore 인덱스는 고 아닌 hello 프리미엄 가격 책정 계층 에서만 지원 됩니다. 데이터베이스 tooStandard 또는 Basic를 다운 그레이드 하면 columnstore 인덱스가 사용할 수 없습니다. hello 시스템 columnstore 인덱스를 유지 하지만 hello 인덱스를 활용 하지 않습니다. 나중에 다시 tooPremium으로 업그레이드할 경우 columnstore 인덱스는 즉시 toobe 다시 활용 합니다.

있는 경우는 **클러스터 된** columnstore 인덱스 계층 다운 그레이드 한 후 hello 전체 테이블 사용할 수 없게 됩니다. 모든 삭제 권장 따라서 *클러스터형* hello Premium 계층 아래 데이터베이스를 다운 그레이드 하기 전에 columnstore 인덱스입니다.

*Tooa 낮은 Premium 계층을 다운 그레이드*: hello 전체 데이터베이스 또는 hello hello 탄력적 풀에서 사용 가능한 저장소 가격 책정 계층을 hello 대상에 대 한 hello 최대 데이터베이스 크기 내에 포함 되 면이 다운 그레이드 성공 합니다. Hello columnstore 인덱스에서 특정 영향은 없습니다.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Hello 메모리 내 OLTP 예제 설치

Hello에 몇 번의 클릭 hello AdventureWorksLT 샘플 데이터베이스를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 그런 다음 hello이 섹션의 단계에 설명 AdventureWorksLT 데이터베이스를 메모리 내 OLTP 개체와 보강 성능 이점을 설명 하는 방법입니다.

메모리 내 OLTP의 경우 더 간단하지만 시각적으로 뛰어난 성능 데모는 다음을 참조하세요.

- 릴리스: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- 소스 코드: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>설치 단계

1. Hello에 [Azure 포털](https://portal.azure.com/)를 서버에 Premium 데이터베이스를 만듭니다. 집합 hello **소스** toohello AdventureWorksLT 샘플 데이터베이스. 자세한 지침은 [첫 번째 Azure SQL Database 만들기](sql-database-get-started-portal.md)를 참조하세요.

2. SQL Server Management Studio를 사용 하 여 toohello 데이터베이스 연결 [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)합니다.

3. 복사 hello [메모리 내 OLTP Transact SQL 스크립트](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour 클립보드 합니다. T-SQL 스크립트 hello 1 단계에서 만든 hello AdventureWorksLT 샘플 데이터베이스의 hello 메모리에 필요한 개체를 만듭니다.

4. SSMS에 hello T-SQL 스크립트를 붙여 하 고 hello 스크립트를 실행 합니다. hello `MEMORY_OPTIMIZED = ON` 절 CREATE TABLE 문에는 매우 중요 합니다. 예:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>오류 40536


Hello T-SQL 스크립트를 실행할 때 40536 오류가 발생할 경우 hello hello 데이터베이스에서 메모리를 지원 하는지 여부를 T-SQL 스크립트 tooverify 다음를 실행 합니다.


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


**0**이라는 결과는 메모리 내가 지원되지 않음을 나타내고 **1**은 지원됨을 나타냅니다. toodiagnose hello 문제 hello Premium 서비스 계층에서 해당 hello 데이터베이스를 확인 합니다.


#### <a name="about-hello-created-memory-optimized-items"></a>메모리 액세스에 최적화 된 항목을 만든 hello에 대 한

**테이블**: hello 샘플 hello 다음 메모리 액세스에 최적화 된 테이블에 포함 되어 있습니다.

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Hello 통해 메모리 액세스에 최적화 된 테이블을 검사할 수 **개체 탐색기** SSMS에서 합니다. **테이블** > **필터** > **필터 설정** > **메모리 액세스에 최적화됨**을 마우스 오른쪽 단추로 클릭합니다. hello 값 1을 같습니다.


또는 같은 hello 카탈로그 뷰를 쿼리할 수 있습니다.


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**고유하게 컴파일된 저장 프로시저**: 카탈로그 뷰 쿼리를 통해 SalesLT.usp_InsertSalesOrder_inmem을 검사할 수 있습니다.


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Hello 샘플 OLTP 워크 로드를 실행 합니다.

다음 두 개의 hello 간의 차이 hello *저장 프로시저* hello 테이블의 메모리 액세스에 최적화 된 버전을 사용 하 여 hello 첫 번째 프로시저, hello 하는 동안 두 번째 절차는 hello 일반 디스크에 테이블 사용:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


이 섹션에서는 toouse hello 편리한 방법을 표시 **ostress.exe** 유틸리티 tooexecute hello 스트레스가 수준에서 두 개의 저장된 프로시저입니다. Hello 두 스트레스 실행 toofinish에 걸리는 시간을 비교할 수 있습니다.


Ostress.exe를 실행 하면 hello 다음 둘 다에 대해 설계 된 매개 변수 값을 전달 하는 것이 좋습니다.

- -n100을 사용하여 많은 수의 동시 연결을 실행합니다.
- -r500을 사용하여 각 연결 루프를 수백 번 가집니다.


그러나 모든 기능이 작동 하는 n10 및-r50 tooensure 같은 값이 훨씬 작은 toostart를 할 수 있습니다.


### <a name="script-for-ostressexe"></a>ostress.exe에 대한 스크립트


이 섹션은 우리의 ostress.exe 명령줄에 포함 된 hello T-SQL 스크립트를 표시 합니다. hello 스크립트 hello 이전에 설치 하는 T-SQL 스크립트에서 생성 된 항목을 사용 합니다.


hello 다음 스크립트는 샘플에 판매 주문을 삽입 품목이 5 개인 메모리 액세스에 최적화 된 hello 다음 *테이블*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


toomake hello *_ondisk* 버전의 hello ostress.exe에 대 한 이전 T-SQL 스크립트, hello의 두 항목 바꿨을 것 *_inmem* 와 substring *_ondisk*합니다. 이러한 대체 hello 이름을 테이블 및 저장된 프로시저의 영향을 줍니다.


### <a name="install-rml-utilities-and-ostress"></a>RML 유틸리티 및 ostress 설치


이상적으로 Azure 가상 컴퓨터 (VM)에서 toorun ostress.exe를 계획 합니다. 만듭니다는 [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello에 동일한 Azure 지역 AdventureWorksLT 데이터베이스가 상주 합니다. 하지만 대신 노트북에서 ostress.exe를 실행할 수 있습니다.


Hello, VM 또는 호스트 무엇이 든 선택 hello 재생 Markup Language (RML) 유틸리티를 설치 합니다. hello 유틸리티 ostress.exe를 포함합니다.

자세한 내용은 다음을 참조하세요.
- ostress.exe 토론 hello [메모리 내 OLTP에 대 한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)합니다.
- [메모리 내 OLTP에 대한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)
- hello [ostress.exe를 설치 하기 위한 블로그](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)합니다.



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Hello 실행 *_inmem* 작업 부하를 먼저 스트레스


사용할 수는 *RML Cmd Prompt* 창 toorun ostress.exe 명령줄 취급 합니다. hello 명령줄 매개 변수를 ostress 직접:

- 동시에 100개의 연결(-n100)을 실행하도록 합니다.
- 50 회 hello T-SQL 스크립트를 실행 하는 각 연결 (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


앞에 ostress.exe 명령줄 toorun hello:


1. 모든 이전 실행 하 여 삽입 된 모든 hello 데이터 hello 다음 toodelete SSMS에서 명령을 실행 하 여 hello 데이터베이스 데이터 콘텐츠를 다시 설정 하십시오.

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Hello ostress.exe 명령줄 tooyour 클립보드 앞의 hello 텍스트를 복사 합니다.

3. Hello 대체 `<placeholders>` hello 매개 변수-S-U-P-d hello로에 대 한 실제 값을 수정 합니다.

4. 편집한 명령줄을 RML Cmd 창에서 실행합니다.


#### <a name="result-is-a-duration"></a>결과는 기간입니다


Ostress.exe 완료 되 면 실행 지속 시간 hello RML Cmd 창에서 출력의 마지막 줄으로 된 hello를 기록 됩니다. 예를 들어 짧은 테스트 실행은 약 1.5분 동안 지속됩니다.

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>*_ondisk*에 대해 다시 설정하고 편집한 다음 다시 실행합니다.


Hello hello 결과 구성한 후 *_inmem* 실행 hello hello에 대 한 단계를 수행 하십시오 *_ondisk* 실행:


1. Hello 이전을 실행 하 여 삽입 된 모든 hello 데이터 hello 다음 SSMS toodelete에서 명령을 실행 하 여 hello 데이터베이스를 다시 설정 하십시오.
```
EXECUTE Demo.usp_DemoReset;
```

2. Hello ostress.exe 명령줄 tooreplace 모든 편집 *_inmem* 와 *_ondisk*합니다.

3. Hello에 대 한 ostress.exe를 두 번째로 다시 실행 하 고 hello 기간 결과 캡처하십시오.

4. 다시 (삭제에 대 한 책임감 있게 많은 양의 테스트 데이터를 지정할 수 있는 대상) hello 데이터베이스를 다시 설정 합니다.


#### <a name="expected-comparison-results"></a>예상된 비교 결과

메모리에이 테스트 해당 성능 향상을 이루었습니다 **9 번** 이 단순한 작업에 대 한 ostress와의 Azure VM에서 실행 중인 hello 동일 hello 데이터베이스와 Azure 지역입니다.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Hello 메모리 내 분석 샘플을 설치 합니다.


이 섹션에서는 기존의 b-트리 인덱스와 columnstore 인덱스를 사용할 때 있습니다 hello IO 및 통계 결과 비교 합니다.


OLTP 워크 로드에서 실시간 분석에 대 한 것이 가장 좋은 toouse 비클러스터형 columnstore 인덱스입니다. 자세한 내용은 [설명한 Columnstore 인덱스](http://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.



### <a name="prepare-hello-columnstore-analytics-test"></a>Hello columnstore 분석 테스트 준비


1. Azure 포털 toocreate hello 샘플에 포함 하 여 새 AdventureWorksLT 데이터베이스 hello를 사용 합니다.
 - 정확한 이름을 사용합니다.
 - Premium 서비스 계층을 선택합니다.

2. 복사 hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour 클립보드 합니다.
 - T-SQL 스크립트 hello 1 단계에서 만든 hello AdventureWorksLT 샘플 데이터베이스의 hello 메모리에 필요한 개체를 만듭니다.
 - hello 스크립트 hello 차원 테이블 두 개와 팩트 테이블을 만듭니다. hello 팩트 테이블은 각각 3.5 백만 행으로 채워집니다.
 - hello 스크립트 toocomplete 15 분 걸릴 수 있습니다.

3. SSMS에 hello T-SQL 스크립트를 붙여 하 고 hello 스크립트를 실행 합니다. hello **COLUMNSTORE** hello 키워드 **CREATE INDEX** 문에에서 같이 매우 중요 합니다.<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. AdventureWorksLT toocompatibility 수준 130을 설정 합니다.<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    수준 130 직접적인 관련된은 tooIn 메모리 내 기능 않습니다. 하지만 수준 130은 일반적으로 120이 제공하는 것보다 빠른 쿼리 성능을 제공합니다.


#### <a name="key-tables-and-columnstore-indexes"></a>핵심 테이블 및 columnstore 인덱스


- dbo입니다. 에서는 고급 hello에 압축 클러스터형된 columnstore 인덱스를 가진 테이블인 FactResellerSalesXL_CCI *데이터* 수준입니다.

- dbo입니다. FactResellerSalesXL_PageCompressed는 해당 하는 일반 클러스터형된 인덱스는 hello에만 압축 된 테이블은 *페이지* 수준입니다.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>키는 toocompare hello columnstore 인덱스를 쿼리합니다.


[실행할 수 있는 여러 T-SQL 쿼리 형식이](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee 성능 향상. Hello T-SQL 스크립트의에서 2 단계에서 주의 기울여야 toothis 쌍 쿼리 비용을 지불 합니다. 두 쿼리는 한 줄만 다릅니다.


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


클러스터형된 columnstore 인덱스는 hello FactResellerSalesXL에에서\_CCI 테이블입니다.

hello T-SQL 스크립트 발췌 한 다음 통계에 대 한 인쇄 IO와 각 테이블의 hello 쿼리에 대 한 시간입니다.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

Hello P2 가격 책정 계층을 사용 하 여 데이터베이스를 hello 기존 인덱스와 비교 하는 hello 클러스터형된 columnstore 인덱스를 사용 하 여이 쿼리에 대 한 약 9 번 hello 성능 향상을 기대할 수 있습니다. P15와 hello columnstore 인덱스를 사용 하 여 57 배 정도 hello 성능 향상을 기대할 수 있습니다.



## <a name="next-steps"></a>다음 단계

- [빠른 시작 1: 더 빠른 T-SQL 성능을 위한 메모리 내 OLTP 기술](http://msdn.microsoft.com/library/mt694156.aspx)

- [기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용](sql-database-in-memory-oltp-migration.md)

- 메모리 내 OLTP에 대한 [메모리 내 OLTP 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).


## <a name="additional-resources"></a>추가 리소스

#### <a name="deeper-information"></a>자세한 정보

- [쿼럼이 SQL Database의 메모리 내 OLTP을 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법에 대해 알아보기](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [Azure SQL Database의 메모리 내 OLTP 블로그 게시물](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [메모리 내 OLTP에 대해 알아보기](http://msdn.microsoft.com/library/dn133186.aspx)

- [columnstore 인덱스에 대해 알아보기](https://msdn.microsoft.com/library/gg492088.aspx)

- [실시간 운영 성과 분석에 대해 알아보기](http://msdn.microsoft.com/library/dn817827.aspx)

- [일반적인 워크로드 패턴 및 마이그레이션 고려 사항에 대한 백서](http://msdn.microsoft.com/library/dn673538.aspx)를 참조하세요. 여기에서 메모리 내 OLTP가 일반적으로 상당한 성능 향상을 제공하는 워크로드 패턴을 설명합니다.

#### <a name="application-design"></a>응용 프로그램 설계

- [메모리 내 OLTP(메모리 내 최적화)](http://msdn.microsoft.com/library/dn133186.aspx)

- [기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>도구

- [Azure Portal](https://portal.azure.com/)

- [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SSDT(SQL Server Data Tools)](http://msdn.microsoft.com/library/mt204009.aspx)
