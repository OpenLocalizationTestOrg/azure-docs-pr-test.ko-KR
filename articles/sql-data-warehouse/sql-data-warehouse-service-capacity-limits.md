---
title: "데이터 웨어하우스 용량 제한을 aaaSQL | Microsoft Docs"
description: "SQL 데이터 웨어하우스의 연결, 데이터베이스, 테이블 및 쿼리에 대한 최대값입니다."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>SQL 데이터 웨어하우스 용량 제한
hello 다음 표에 나와 hello Azure SQL 데이터 웨어하우스의 다양 한 구성 요소에 허용 되는 최대 값입니다.

## <a name="workload-management"></a>워크로드 관리
| Category | 설명 | 최대 |
|:--- |:--- |:--- |
| [DWU(데이터 웨어하우스 단위)][Data Warehouse Units (DWU)] |단일 SQL 데이터 웨어하우스에 대한 최대 DWU |6000 |
| [DWU(데이터 웨어하우스 단위)][Data Warehouse Units (DWU)] |단일 SQL Server에 대한 최대 DWU |기본값 6000<br/><br/> 기본적으로 각 SQL server (예: myserver.database.windows.net) too6000 DWU를 수 있는 45,000의 DTU 할당량에 있습니다. 이 할당량은 안전을 위한 제한일 뿐입니다. 하 여 할당량을 늘릴 수 [지원 티켓을 만드는] [ creating a support ticket] 선택 하 고 *할당량* hello 요청 형식으로.  프로그램 DTU, 곱하기 toocalculate DWU 필요한 hello 합계 7.5를 hello 합니다. SQL server 블레이드 hello에서에서 현재 DTU 사용에 hello 포털에서 볼 수 있습니다. 일시 중지 및 일시 중지 되지 않은 데이터베이스 hello DTU 할당량을 차지 합니다. |
| 데이터베이스 연결 |열린 동시 세션 |1024<br/><br/>Hello에 요청 tooa SQL 데이터 웨어하우스 데이터베이스를 전송할 수 있으며 각 1024 활성 연결의 최대 지원 한 번입니다. Note hello 실제로 동시에 실행할 수 있는 쿼리 수가 제한 됩니다. Hello 동시성 제한을 초과 하는 hello 요청으로 갑니다 내부 큐 toobe 처리 될 때까지 대기입니다. |
| 데이터베이스 연결 |준비된 문에 대한 최대 메모리 |20MB |
| [워크로드 관리][Workload management] |최대 동시 쿼리 수 |32<br/><br/> 기본적으로 SQL Data Warehouse는 최대 32개의 동시 쿼리 및 큐에 대기 중인 남은 쿼리를 실행할 수 있습니다.<br/><br/>사용자에 게 할당 tooa 더 높은 리소스 클래스 또는 낮은 DWU로 SQL 데이터 웨어하우스를 구성 하는 hello 동시성 수준을 줄일 수 있습니다. DMV 쿼리 수와 같은 일부 쿼리 toorun 항상 허용 됩니다. |
| [Tempdb][Tempdb] |Tempdb의 최대 크기 |DW100당 399GB입니다. 따라서 DWU1000 Tempdb에는 크기의 too3.99 TB |

## <a name="database-objects"></a>데이터베이스 개체
| Category | 설명 | 최대 |
|:--- |:--- |:--- |
| 데이터베이스 |최대 크기 |디스크에서 압축된 240TB<br/><br/>이 공간 tempdb 또는 로그 공간의 독립적 이며 따라서이 공간을 전용된 toopermanent 테이블입니다.  클러스터형 columnstore의 압축에 따른 예상 크기 증가 비율은 5배입니다.  이러한 압축 모든 테이블은 클러스터형된 columnstore (hello 기본 테이블 형식) hello 데이터베이스 toogrow tooapproximately 1 PB을 수행할 수 있습니다. |
| 테이블 |최대 크기 |디스크에서 압축된 60TB |
| 테이블 |데이터베이스 당 테이블 |20억 |
| 테이블 |테이블 당 열 |1024열 |
| 테이블 |열 당 바이트 |열 [데이터 형식][data type]에 따라 다릅니다.  char 데이터 형식의 경우 8,000자, nvarchar의 경우 4,000자, MAX 데이터 형식의 경우 2GB로 제한됩니다. |
| 테이블 |행 당 바이트, 정의된 크기 |8,060바이트<br/><br/>행당 바이트 수 hello hello에 계산 페이지 압축을 사용한 것과 같은 방식으로 SQL Server입니다. SQL 데이터 웨어하우스 SQL Server와 마찬가지로 있는 행 오버플로 저장소를 지 원하는 **가변 길이 열** toobe 행 외부로 밀어넣을 합니다. 가변 길이 행 행 외부로 밀어넣은, 24 바이트의 루트만 hello 주 레코드에 저장 됩니다. 자세한 내용은 참조 hello [행 오버플로 데이터 초과 8 KB] [ Row-Overflow Data Exceeding 8 KB] MSDN 문서. |
| 테이블 |테이블 당 파티션 |15,000<br/><br/>성능을 향상 시키려면 hello 수를 최소화 권장 파티션 있습니다 필요 하지만 비즈니스 요구 사항을 지원 합니다. Hello로 파티션 수가 증가 hello 오버 헤드에 대 한 데이터 정의 언어 (DDL) 하 고 데이터 조작 언어 (DML) 작업 증가 하 고 성능이 저하 발생 합니다. |
| 테이블 |파티션 경계 값 당 문자. |4000 |
| 인덱스 |테이블 당 비클러스터형 인덱스. |999<br/><br/>Toorowstore 테이블에만 적용 됩니다. |
| 인덱스 |테이블 당 클러스터형 인덱스. |1<br><br/>Tooboth rowstore와 columnstore 테이블에 적용 됩니다. |
| 인덱스 |인덱스 키 크기. |900바이트.<br/><br/>Toorowstore 인덱스에만 적용 됩니다.<br/><br/>Hello 인덱스를 만들 때 hello 열에 hello 기존 데이터가 900 바이트를 초과 하지 않도록 하는 경우 최대 크기인 900 바이트 이상의 varchar 열에 인덱스를 만들 수 있습니다. 그러나 나중에 넣거나 hello 총 크기 tooexceed 900 바이트를 발생 시키는 hello 열에 대해 업데이트 동작이 실패 합니다. |
| 인덱스 |인덱스 당 키 열. |16<br/><br/>Toorowstore 인덱스에만 적용 됩니다. 클러스터형 columnstore 인덱스는 모든 열을 포함합니다. |
| 통계 |Hello의 크기는 열 값을 결합합니다. |900바이트. |
| 통계 |통계 개체 당 열. |32 |
| 통계 |테이블 당 열에 만든 통계. |30,000 |
| 저장 프로시저 |최대 수준의 중첩. |8 |
| 보기 |보기 당 열 |1,024 |

## <a name="loads"></a>로드
| Category | 설명 | 최대 |
|:--- |:--- |:--- |
| Polybase 로드 |행당 MB |1<br/><br/>Polybase 부하는 제한 된 tooloading 행이 1 MB 보다 작은 및 tooVARCHR(MAX)를 로드할 수 없습니다 nvarchar (max) 또는 varbinary (max).<br/><br/> |

## <a name="queries"></a>쿼리
| Category | 설명 | 최대 |
|:--- |:--- |:--- |
| 쿼리 |사용자 테이블에서 쿼리된 쿼리입니다. |1000 |
| 쿼리 |시스템 뷰에서 동시 쿼리입니다. |100 |
| 쿼리 |시스템 뷰에서 쿼리된 쿼리입니다. |1000 |
| 쿼리 |최대 매개 변수 |2098 |
| 배치 |최대 크기 |65,536*4096 |
| 결과 선택 |행 당 열 |4096<br/><br/>하지 결과 선택 hello에서 행 마다 4096 개 이상의 열을 포함할 수 있습니다. 항상 4096이 있다고 보장할 수 없습니다. Hello 쿼리 계획에서 임시 테이블을 필요한 경우 각 테이블에 최대 1024 개의 열 hello 적용할 수 있습니다. |
| SELECT |중첩된 하위 쿼리 |32<br/><br/>SELECT 문에는 32개 보다 많은 중첩된 하위 쿼리가 있어서는 안 됩니다. 항상 32가 있다고 보장할 수 없습니다. 예를 들어 조인을 hello 쿼리 계획으로 하위 쿼리를 제공할 수 있습니다. hello 수 만큼 하위 쿼리 사용 가능한 메모리로 제한 될 수도 있습니다. |
| SELECT |조인 당 열 |1024열<br/><br/>하지 hello 조인에에서 1024 개 이상 있을 수 있습니다. 항상 1024가 있다고 보장할 수 없습니다. Hello 조인 계획 hello 조인 결과 보다 더 많은 열이 있는 임시 테이블을 필요한 경우 hello 1024 제한은 toohello 임시 테이블을 적용 됩니다. |
| SELECT |그룹화 기준 열 당 바이트. |8060<br/><br/>hello GROUP BY 절에 열이 hello 최대 8060 바이트 있을 수 있습니다. |
| SELECT |정렬 기준 열 당 바이트 |8060 바이트.<br/><br/>hello ORDER BY 절에 열이 hello 최대 8060 바이트 있을 수 있습니다. |
| 식별자 및 문 당 상수 |참조된 식별자 및 상수의 수. |65,535<br/><br/>SQL 데이터 웨어하우스 hello 식별자 및 쿼리를 하나의 식에 포함 될 수 있는 상수 수를 제한 합니다. 이 제한은 65,535입니다. 이 숫자를 초과하면 SQL Server 오류 8632가 발생합니다. 자세한 내용은 [내부 오류: 식 서비스 제한에 도달했습니다.][Internal error: An expression services limit has been reached]를 참조하세요. |

## <a name="metadata"></a>Metadata
| 시스템 뷰 | 최대 행 |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |가장 최근 1000 hello에 대 한 DMS 작업자의 총 SQL 요청합니다. |
| sys.dm_pdw_errors |10000 |
| sys.dm_pdw_exec_requests |10000 |
| sys.dm_pdw_exec_sessions |10000 |
| sys.dm_pdw_request_steps |단계 sys.dm_pdw_exec_requests에 저장 된 가장 최근 1000 hello SQL 요청에 대 한 총 수입니다. |
| sys.dm_pdw_os_event_logs |10000 |
| sys.dm_pdw_sql_requests |hello 가장 최근 1000 SQL 요청 sys.dm_pdw_exec_requests에 저장 됩니다. |

## <a name="next-steps"></a>다음 단계
자세한 참조 정보는 [SQL Data Warehouse 참조 개요][SQL Data Warehouse reference overview]를 참조하세요.

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
