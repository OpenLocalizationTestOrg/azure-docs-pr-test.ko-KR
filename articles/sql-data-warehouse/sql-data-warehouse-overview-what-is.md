---
title: "aaaWhat은 Azure SQL 데이터 웨어하우스 인지 확인 | Microsoft Docs"
description: "페타바이트 볼륨의 관계형 및 비관계형 데이터를 처리할 수 있는 엔터프라이즈급 분산 데이터베이스입니다. 확장 된 hello 업계 최초의 클라우드 데이터 웨어하우스로, 축소, 이며 초에서 일시 중지 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스란?
Azure SQL Data Warehouse는 거대한 양의 데이터를 처리할 수 있는 MPP(Massively Parallel Processing) 클라우드 기반 규모 확장 관계형 데이터베이스입니다. 

SQL 데이터 웨어하우스:

* Hello SQL Server 관계형 데이터베이스를 Azure의 클라우드 확장 기능을 결합합니다. 
* 계산에서 저장소를 분리합니다.
* 계산을 증가, 감소, 일시 중지 또는 다시 시작할 수 있습니다. 
* Hello Azure 플랫폼에서 통합 됩니다.
* SQL Server T-SQL(Transact-SQL) 및 도구를 활용합니다.
* SOC 및 ISO와 같은 다양한 법적 및 비즈니스 보안 요구 사항을 준수합니다.

이 문서에서는 SQL 데이터 웨어하우스의 hello 주요 기능을 설명 합니다.

## <a name="massively-parallel-processing-architecture"></a>대규모 병렬 처리 아키텍처
SQL 데이터 웨어하우스는 방대한 병렬 처리(MPP) 분산 데이터베이스 시스템입니다. Hello 백그라운드 SQL 데이터 웨어하우스에서는 많은 비공유 저장소 및 처리 단위를 통해 데이터를 분산합니다. hello 데이터를 기반으로 동적으로 연결 된 계산 노드는 쿼리를 실행 하는 프리미엄 로컬 중복 저장소 계층에 저장 됩니다. SQL 데이터 웨어하우스 사용 "구분 및 고정" 접근 방식 toorunning 로드 하 고 복잡 한 쿼리 합니다. 요청 제어 노드를 배포에 대 한 최적화 하 고 다음 병렬로 tooCompute 노드 toodo 작업 전달 받습니다.

분리된 저장소 및 계산을 사용하여 SQL Data Warehouse는 다음을 수행할 수 있습니다.

* 계산과 독립적으로 저장소를 확장 또는 축소합니다.
* 데이터를 이동하지 않고 계산을 확장 또는 축소합니다.
* 데이터를 그대로 유지하고 저장소에 대한 비용만 부담하면서 계산 용량을 일시 중지합니다.
* 운영 시간 동안 계산 용량을 다시 시작합니다.

hello 다음 다이어그램에서는 hello 아키텍처 자세히

![SQL 데이터 웨어하우스 아키텍처][1]

**제어 노드에:** hello 제어 노드를 관리 하 고 쿼리를 최적화 합니다. 모든 응용 프로그램 및 연결와 상호 작용 하는 hello 프런트 엔드는 SQL 데이터 웨어하우스에 hello 제어 노드에 연결 된 값을 SQL 데이터베이스 및 연결 tooit 찾아서 판단한 hello 동일 합니다. Hello 화면 아래에서 hello 제어 노드에 좌표 모든 hello 데이터 이동와 필요한 계산 분산된 데이터에 대해 toorun 병렬 쿼리 합니다. T-SQL 쿼리 tooSQL 데이터 웨어하우스를 제출 하면 hello 제어 노드에 동시에 각 계산 노드에서 실행 되는 별도 쿼리도 변환 합니다.

**계산 노드:** hello 계산 노드 SQL 데이터 웨어하우스 뒤 hello 전원으로 사용 합니다. 이들은 데이터를 저장하고 쿼리를 처리하는 SQL 데이터베이스입니다. 데이터를 추가 하면 SQL 데이터 웨어하우스 hello 행 tooyour 계산 노드를 배포 합니다. hello 계산 노드는 데이터에 대해 hello 병렬 쿼리를 실행 하는 hello 작업자입니다. 처리 후 hello 결과 백 toohello 제어 노드에 전달합니다. 반환 hello 최종 결과 toofinish hello 쿼리 hello 제어 노드 hello 결과 집계 합니다.

**저장소:** 데이터는 Azure Blob 저장소에 저장됩니다. 계산 노드 데이터를 조작할 때 쓰기은 및 blob 저장소에서 직접 tooand 읽기입니다. SQL 데이터 웨어하우스 수행할 수 있는 Azure 저장소에 투명 하 고 크게 확장, 하므로 hello 동일 합니다. 계산 및 저장소는 독립적이므로 SQL 데이터 웨어하우스는 저장소 크기를 계산 확장과 별도로 자동으로 조정할 수 있으며 그 반대도 마찬가지 입니다. Azure Blob 저장소 완벽 하 게 결함 허용 되며 간소화 hello 백업 및 복원 프로세스입니다.

**데이터 이동 서비스:** 데이터 이동 서비스 (DMS) hello 노드 간에 데이터를 이동 합니다. DMS는 hello 계산 노드 액세스 toodata 조인 및 집계에 대 한 필요한를 제공 합니다. DMS는 Azure 서비스가 아닙니다. SQL 데이터베이스와 함께 모든 hello 노드에서 실행 되는 Windows 서비스인 경우 DMS는 직접 상호 작용할 수 없는 백그라운드 프로세스입니다. 그러나 볼 수 있습니다 쿼리 계획 toosee 데이터 이동에 필요한 toorun 이므로 DMS 작업을 수행 하면 동시에 각 쿼리 합니다.

## <a name="optimized-for-data-warehouse-workloads"></a>데이터 웨어하우스 워크로드에 최적화
여러 데이터 웨어하우징 특정 성능 최적화를 포함 하 여 hello MPP 접근 하는 데 도움이:

* 모든 데이터 전반에 대한 분산 쿼리 최적화 프로그램 및 복잡한 통계 집합. Hello 서비스 특정 분산된 쿼리 작업의 hello 비용을 평가 하 여 수 toooptimize 쿼리는 데이터 크기와 배포에 정보를 사용 합니다.
* 고급 알고리즘 및 기술을 통합 hello 데이터에 필요한 tooperform hello 쿼리로 컴퓨팅 리소스 간에 이동 tooefficiently 이동 데이터를 처리 합니다. 이러한 데이터 이동 작업을 빌드되고 모든 최적화 toohello 데이터 이동 서비스가 자동으로 발생 합니다.
* 기본적으로 클러스터형 **columnstore** 인덱스. SQL 데이터 웨어하우스 열 기반 저장소를 사용 하 여 기존 행 기반 저장소 보다 및 too10x 드릴업 평균 5 x 압축 향상 되거나 더 많은 쿼리 성능 향상을 가져옵니다. Tooscan를 필요로 하는 분석 쿼리는 많은 수의 행을 columnstore 인덱스와 더 잘 작동 합니다.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>데이터 웨어하우스 단위를 사용한 예측 가능하고 확장 가능한 성능
SQL Data Warehouse는 사용자가 분석 쿼리에 대해 일관적이고 예측 가능한 성능을 예상할 수 있도록 SQL Database와 유사한 기술로 빌드됩니다. 사용자가 추가 하거나 뺄 계산 노드 선형 toosee 성능 배율을 예상 해야 합니다. SQL 데이터 웨어하우스 리소스 tooyour 할당 데이터 웨어하우스 단위 (Dwu) 단위로 측정 됩니다. Dwu로 CPU, 메모리, SQL 데이터 웨어하우스 tooyour 할당 되는 IOPS와 같은 기본 리소스의 측정값입니다. Dwu hello 수를 늘리면 리소스와 성능 증가 합니다. 특히, DWU는 다음을 보장합니다.

* 데이터 웨어하우스에서 hello 기본 하드웨어 또는 소프트웨어에 대 한 걱정 없이 수 tooscale 됩니다.
* 데이터 웨어하우스의 hello 계산을 변경 하기 전에 DWU 수준에 대 한 성능 향상을 예측할 수 있습니다.
* hello 기본 하드웨어와 소프트웨어 인스턴스 수 변경 하거나 워크 로드 성능에 영향을 주지 않고 이동 합니다.
* Microsoft 워크 로드의 hello 성능 영향을 주지 않고 hello 서비스의 아키텍처를 기본 hello 향상 시킬 수 있습니다.
* Microsoft SQL 데이터 웨어하우스에 확장할 수 있는 방식으로 성능이 향상 신속 하 게 및 효과 시스템 hello 균등 하 게 합니다.

데이터 웨어하우스 단위는 데이터 웨어하우징 워크로드 성능과 연관성이 높은 세 가지 측정 메트릭에 대한 단위를 제공합니다. hello 선형 hello dwu로 사용 하는 작업 부하 메트릭을 배율의 주요 합니다.

**검색/집계:** 대량의 행을 검색한 후 복잡한 집계를 수행하는 표준 데이터 웨어하우징 쿼리입니다. 이것은 I/O와 CPU를 많이 사용하는 연산입니다.

**로드:** hello 서비스로 기능 tooingest 데이터 hello 합니다. 로드는 Azure Data Lake 또는 Azure Storage Blob의 PolyBase를 통해 가장 잘 수행됩니다. 이 메트릭은 디자인 된 toostress 네트워크 및 hello 서비스의 CPU 측면입니다.

**테이블 선택 (CTAS) 만들기:** CTAS에는 hello 기능 toocopy 테이블을 측정 합니다. 이 저장소, hello 어플라이언스의 hello 노드 간에 배포 및 toostorage를 다시 작성에서 데이터를 읽고 작업 합니다. 이것은 CPU, IO 및 네트워크를 많이 사용하는 연산입니다.

## <a name="built-on-sql-server"></a>SQL Server 기반
SQL 데이터 웨어하우스 hello SQL Server 관계형 데이터베이스 엔진을 기반으로 하며 다양 한 엔터프라이즈 데이터 웨어하우스에서 기대 하는 hello 기능을 포함 합니다. T-SQL을 이미 알고 있는 경우 쉽게 tootransfer 프로그램 기술 tooSQL 데이터 웨어하우스 합니다. 고급 여부 또는 시작, 시작 hello 예제 hello 설명서에서 도움이 됩니다. 전반적으로 생각해볼 수 있겠습니다 hello 방식에서는 SQL 데이터 웨어하우스의 hello 언어 요소를 다음과 같이 구성 했습니다.

* SQL 데이터 웨어하우스는 많은 연산에 T-SQL 구문을 사용합니다. 또한 저장 프로시저, 사용자 정의 함수, 테이블 파티션, 인덱스, 데이터 정렬을 비롯한 기존의 SQL 구문을 폭넓게 지원합니다.
* SQL Data Warehouse에는 클러스터형 **Columnstore** 인덱스, PolyBase 통합 및 데이터 감사(위협 평가와 함께 완성되는)를 비롯한 새로운 SQL Server 기능이 많이 포함되어 있습니다.
* 데이터 웨어하우징 워크 로드에 대 한 일반적이 지 않거나 최신 tooSQL 서버에 있는 특정 T-SQL 언어 요소는 현재 사용할 수 있는 일 수 없습니다. 자세한 내용은 참조 hello [마이그레이션 설명서][Migration documentation]합니다.

Transact SQL hello와 SQL Server, SQL 데이터 웨어하우스, SQL 데이터베이스 및 분석 플랫폼 시스템 간의 기능 공통점을 데이터 요구 사항에 맞는 솔루션을 개발할 수 있습니다. 결정할 수 있는 tookeep 데이터를 기반으로 성능, 보안 및 크기 조정 요구 사항 및 다음 서로 다른 시스템 간의 필요에 따라 데이터를 전송 합니다.

## <a name="data-protection"></a>데이터 보호
SQL 데이터 웨어하우스는 Azure 프리미엄 로컬 중복 저장소에 모든 데이터를 저장합니다. 지역화 된 오류에 대 한 hello 로컬 데이터 센터 tooguarantee 투명 한 데이터 보호에 hello 데이터의 여러 동기 복사본이 유지 됩니다. 또한 SQL Data Warehouse는 Azure Storage 스냅숏을 사용하여 일정한 간격으로 자동으로 (일시 중지 해제된) 활성 데이터베이스를 백업합니다. 백업 및 복원, 작동 방법에 대 한 자세한 toolearn 참조 hello [백업 및 복원 개요][Backup and restore overview]합니다.

## <a name="integrated-with-microsoft-tools"></a>Microsoft 도구와 통합
SQL 데이터 웨어하우스 또한 통합 hello 도구는 대부분 사용자에 잘 알고 수 있으므로 SQL Server를 합니다. 이러한 도구로는 다음이 있습니다.

**기존 SQL Server 도구:** SQL 데이터 웨어하우스는 SQL Server Analysis Services, Integration Services 및 Reporting Services와 완전히 통합됩니다.

**클라우드 기반 도구:** SQL Data Warehouse는 데이터 팩터리, Stream Analytics, Machine Learning 및 Power BI를 포함하여 Azure의 수많은 신규 도구와 통합할 수 있습니다. 자세한 전체 목록은 [통합된 도구 개요][Integrated tools overview]를 참조하세요.

**타사 도구:** 많은 타사 도구 공급자들이 자사의 도구와 SQL Data Warehouse의 통합을 보증하였습니다. 전체 목록은 [SQL Data Warehouse 솔루션 파트너][SQL Data Warehouse solution partners](영문)를 참조하세요.

## <a name="hybrid-data-sources-scenarios"></a>하이브리드 데이터 원본 시나리오
Polybase tooleverage을 사용 하면 친숙 한 T-SQL 명령을 사용 하 여 서로 다른 원본의 데이터입니다. Polybase는 tooquery 비관계형 데이터를 일반 테이블 처럼 Azure Blob 저장소에 보관 있습니다. SQL 데이터 웨어하우스로 Polybase tooquery 비관계형 데이터 또는 tooimport 비관계형 데이터를 사용 합니다.

* PolyBase는 외부 테이블 tooaccess 비관계형 데이터를 사용합니다. hello 테이블 정의에 SQL 데이터 웨어하우스에 저장 됩니다 및 SQL을 사용 하 여 액세스할 수 있습니다 및 도구를 일반 관계형 데이터 액세스 하는 것입니다.
* Polybase는 통합 시 중립적입니다. 이 지 원하는 기능 tooall hello 소스와 같은 기능 노출 hello 합니다. Polybase에서 읽은 hello 데이터 구분 기호로 분리 된 파일 또는 ORC 파일을 비롯 한 다양 한 형식 될 수 있습니다.
* PolyBase는 HDInsight 클러스터에 대 한 저장소로도 사용 되는 사용 되는 tooaccess blob 저장소를 수 있습니다. 이 액세스할 수 있도록 toohello 관계형 및 비관계형 도구를 사용 하 여 동일한 데이터입니다.

## <a name="sla"></a>SLA
SQL Data Warehouse는 Microsoft 온라인 서비스 SLA의 일부로 제품 수준 SLA(서비스 수준 계약)를 제공합니다. 자세한 내용은 [SQL Data Warehouse에 대한 SLA][SLA for SQL Data Warehouse]를 방문하세요. Hello를 방문할 수 있는 다른 모든 제품에 대 한 SLA 정보에 대 한 [서비스 수준 계약] Azure 페이지 또는 hello에 [볼륨 라이선스] [ Volume Licensing] 페이지. 

## <a name="next-steps"></a>다음 단계
SQL 데이터 웨어하우스에 대 한 비트를 파악 했으므로 자세한 방법을 tooquickly [SQL 데이터 웨어하우스를 만들] [ create a SQL Data Warehouse] 및 [샘플 데이터를 로드][load sample data]합니다. 새 tooAzure 인 경우 사용할 수 있습니다 hello [Azure 용어집] [ Azure glossary] 새 용어를 발견할 때 유용 합니다. 또는 그 밖의 SQL Data Warehouse 리소스를 살펴봅니다.  

* [고객 성공 사례]
* [블로그]
* [기능 요청]
* [비디오]
* [고객 자문 팀 블로그]
* [지원 티켓 만들기]
* [MSDN 포럼]
* [Stack Overflow 포럼]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[지원 티켓 만들기]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[고객 성공 사례]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[블로그]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[고객 자문 팀 블로그]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[기능 요청]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN 포럼]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Stack Overflow 포럼]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[비디오]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[서비스 수준 계약]: https://azure.microsoft.com/en-us/support/legal/sla/
