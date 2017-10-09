---
title: "SQL 데이터 웨어하우스 서비스에 대 한 aaaAll 항목 | Microsoft Docs"
description: "Hello Azure 서비스에 대 한 모든 항목의 테이블 이름이 http://azure.microsoft.com/documentation/articles/, 제목 및 설명에 존재 하는 SQL 데이터 웨어하우스입니다."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Azure SQL 데이터 웨어하우스 서비스에 대한 모든 항목
이 항목에서는 toohello 직접 적용 되는 모든 항목 나열 **SQL 데이터 웨어하우스** Azure의 서비스입니다. 키워드에 대 한이 웹 페이지를 사용 하 여 검색할 수 있습니다 **Ctrl + F**, 현재 관심 toofind hello 항목입니다.

## <a name="new"></a>새로 만들기
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 1 |[SQL Data Warehouse 백업](sql-data-warehouse-backups.md) |Azure SQL 데이터 웨어하우스 tooa 복원 지점 또는 다른 지리적 지역 toorestore 수 있도록 하는 SQL 데이터 웨어하우스 기본 제공 데이터베이스 백업에 알아봅니다. |

## <a name="updated-articles-sql-data-warehouse"></a>업데이트된 문서, SQL Data Warehouse
이 섹션에서는 최근에 업데이트 된 문서를 나열, big 또는 중요 한 된 hello를 업데이트 합니다. 업데이트 된 각 아티클당 hello의 대략적인 코드 조각을 추가 markdown 텍스트가 표시 됩니다. hello 문서의 hello 날짜 범위 내에서 업데이트 된 **2016-08-22** 너무**2016-10-05**합니다.

| &nbsp; | 문서 | 업데이트된 텍스트, 코드 조각 | 업데이트 시기 |
| ---:|:--- |:--- |:--- |
| 2 |[Azure blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드합니다(PolyBase).](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |/ tootrack 바이트와 파일 r.command, s.request_id, r.status, count (distinct input_name) nbr_files로 선택, 합계 (s.bytes_processed) / 1024/1024 r.request_id에 대 한 sys.dm_pdw_exec_requests r 내부 조인 sys.dm_pdw_dms_external_work s에서 gb_processed로 s.request_id = WHERE r 합니다. label  = 'CTAS : Load  cso . DimProduct  '  OR r. label  = 'CTAS : Load  cso . FactOnlineSales  ' GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |2016-09-07 |
| 3 |[SQL Data Warehouse 복원](sql-data-warehouse-restore-database-overview.md) |* * 일시 중지 된 데이터 웨어하우스 복원할 수 있습니까? * * 필요한는 일시 중지 된 데이터 웨어하우스 toorestore toofirst 다시 온라인으로 전환 합니다. Hello 데이터 웨어하우스를 다시 온라인 상태가 되 면에서 복원 지점 toochoose의 7 일 해야 합니다. * * 복원 tooa 지리적 중복 지역 * * hello 지역 중복 저장소를 사용 하는 다른 지리적 지역에 hello 데이터 웨어하우스 tooyour 쌍 이룬된 데이터 센터를 복원할 수 있습니다. 데이터 웨어하우스 hello hello 마지막 매일 백업에서 복원 됩니다. * * 복원 시간 표시 막대 * * hello 내에서 데이터베이스 tooany 복원 지점을 지난 7 일을 복원할 수 있습니다. 스냅숏은은 tooeight 매 4 시간 마다 시작 하며 7 일 동안 사용할 수 있는 합니다. 7일보다 오래된 스냅숏은 만료되고 해당 복원 지점을 더 이상 사용할 수 없게 됩니다. * * 복원을 비용 * * hello 저장소 요금 데이터 웨어하우스를 복원 하는 hello hello Azure 프리미엄 저장소 요금이 청구 됩니다. 복원 된 데이터 웨어하우스를 일시 중지 하면 hello Azure 프리미엄 저장소 속도로 저장소에 대 한 요금이 청구 됩니다. 일시 중지 hello 장점은 충전 없는입니다. |2016-09-29 |

## <a name="get-started"></a>시작
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 4 |[인증 tooAzure SQL 데이터 웨어하우스](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) 및 SQL Server 인증 tooAzure SQL 데이터 웨어하우스 합니다. |
| 5 |[Azure SQL 데이터 웨어하우스에 대한 모범 사례](sql-data-warehouse-best-practices.md) |Azure SQL 데이터 웨어하우스에 대한 솔루션을 개발하면서 알아야 할 권장 사항 및 모범 사례입니다. 이 내용은 성공적인 개발에 도움이 됩니다. |
| 6 |[Azure SQL 데이터 웨어하우스용 드라이버](sql-data-warehouse-connection-strings.md) |SQL 데이터 웨어하우스용 드라이버 및 연결 문자열 |
| 7 |[SQL 데이터 웨어하우스 tooAzure 연결](sql-data-warehouse-connect-overview.md) |SQL 데이터 웨어하우스를 tooAzure 프로그램에 대 한 문자열 toofind hello 서버 이름 및 연결 |
| 8 |[Azure 기계 학습을 사용하여 데이터 분석](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Azure 기계 학습 toobuild 예측 기계 학습 Azure SQL 데이터 웨어하우스에 저장 된 데이터를 기반으로 모델을 사용 합니다. |
| 9 |[Azure SQL 데이터 웨어하우스 쿼리(sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Hello sqlcmd 명령줄 유틸리티를 사용 하 여 Azure SQL 데이터 웨어하우스를 쿼리 합니다. |
| 10 |[TRANSACT-SQL(TSQL)를 사용하여 SQL 데이터 웨어하우스 데이터베이스 만들기](sql-data-warehouse-get-started-create-database-tsql.md) |어떻게 toocreate는 Azure SQL 데이터는 t s q l을 웨어하우스에 대해 알아봅니다 |
| 11 |[SQL 데이터 웨어하우스에 대 한 toocreate 지원 티켓 하는 방법](sql-data-warehouse-get-started-create-support-ticket.md) |어떻게 Azure SQL 데이터 웨어하우스에 toocreate 지원 티켓 합니다. |
| 12 |[Azure Data Factory를 사용하여 데이터 로드](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Azure 데이터 팩터리를 사용 하 여 tooload 데이터에 알아봅니다 |
| 13 |[SQL 데이터 웨어하우스에서 PolyBase를 사용하여 데이터 로드](sql-data-warehouse-get-started-load-with-polybase.md) |PolyBase 무엇 인지 알아보고 방법과 toouse 데이터 웨어하우징 시나리오에 대 한 것입니다. |
| 14 |[Azure SQL 데이터 웨어하우스 만들기](sql-data-warehouse-get-started-provision.md) |Toocreate에 Azure SQL 데이터 웨어하우스는 Azure 포털을 hello 하는 방법에 대해 알아봅니다 |
| 15 |[PowerShell을 사용하여 SQL 데이터 웨어하우스 만들기](sql-data-warehouse-get-started-provision-powershell.md) |PowerShell을 사용하여 SQL 데이터 웨어하우스 만들기 |
| 16 |[Power BI를 사용하여 데이터 시각화](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Power BI로 SQL 데이터 웨어하우스 데이터 시각화 |
| 17 |[Azure SQL 데이터 웨어하우스 쿼리(Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Visual Studio를 사용하여 SQL 데이터 웨어하우스를 쿼리합니다. |

## <a name="develop"></a>개발
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 18 |[SQL 데이터 웨어하우스에 대해 트랜잭션 최적화](sql-data-warehouse-develop-best-practices-transactions.md) |Azure SQL 데이터 웨어하우스에서 효율적인 트랜잭션 업데이트를 작성하는 모범 사례 가이드 |
| 19 |[SQL 데이터 웨어하우스의 동시성 및 워크로드 관리](sql-data-warehouse-develop-concurrency.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 동시성 및 워크로드 관리를 이해합니다. |
| 20 |[SQL 데이터 웨어하우스의 CTAS(Create Table As Select)](sql-data-warehouse-develop-ctas.md) |Hello를 사용 하 여 코딩 하기 위한 팁 솔루션 개발을 위한 Azure SQL 데이터 웨어하우스에 (CTAS) 문을 선택 하는 테이블을 만듭니다. |
| 21 |[SQL 데이터 웨어하우스의 동적 SQL](sql-data-warehouse-develop-dynamic-sql.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 동적 SQL 사용 팁. |
| 22 |[SQL 데이터 웨어하우스의 GROUP BY 옵션](sql-data-warehouse-develop-group-by-options.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 GROUP BY 옵션 구현을 위한 팁. |
| 23 |[SQL 데이터 웨어하우스에 레이블을 tooinstrument 쿼리를 사용 하 여](sql-data-warehouse-develop-label.md) |Azure SQL 데이터 웨어하우스 레이블을 tooinstrument 쿼리를 사용 하 여 솔루션을 개발 하기 위한 팁입니다. |
| 24 |[SQL 데이터 웨어하우스의 루프](sql-data-warehouse-develop-loops.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 루프 및 커서 대체를 위한 팁. |
| 25 |[SQL 데이터 웨어하우스의 저장된 프로시저](sql-data-warehouse-develop-stored-procedures.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 저장 프로시저 구현을 위한 팁 |
| 26 |[SQL 데이터 웨어하우스의 트랜잭션](sql-data-warehouse-develop-transactions.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 트랜잭션 구현을 위한 팁 |
| 27 |[SQL 데이터 웨어하우스의 사용자 정의 스키마](sql-data-warehouse-develop-user-defined-schemas.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 스키마 사용을 위한 팁 |
| 28 |[SQL 데이터 웨어하우스의 변수 할당](sql-data-warehouse-develop-variable-assignment.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 변수 할당을 위한 팁 |
| 29 |[SQL 데이터 웨어하우스의 뷰](sql-data-warehouse-develop-views.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Transact-SQL 뷰 사용을 위한 팁 |
| 30 |[SQL 데이터 웨어하우스에 대한 디자인 결정 및 코딩 기술](sql-data-warehouse-overview-develop.md) |SQL 데이터 웨어하우스에 대한 개발 개념, 디자인 결정, 권장 사항 및 코딩 기술입니다. |

## <a name="manage"></a>관리
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 31 |[Azure SQL 데이터 웨어하우스의 계산 능력 관리(개요)](sql-data-warehouse-manage-compute-overview.md) |Azure SQL 데이터 웨어하우스의 성능 확장 기능입니다. Dwu로 조정 하 여 수평 확장 또는 일시 중지 하 고 계산 리소스 toosave 비용이 다시 시작 합니다. |
| 32 |[Azure SQL 데이터 웨어하우스의 계산 능력 관리(Azure 포털)](sql-data-warehouse-manage-compute-portal.md) |Azure 포털 작업 toomanage 전원을 계산 합니다. DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 일시 중지 및 재개 자원 toosave 비용을 계산 합니다. |
| 33 |[Azure SQL 데이터 웨어하우스의 계산 능력 관리(PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |PowerShell 작업 toomanage 전원을 계산 합니다. DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 일시 중지 및 재개 자원 toosave 비용을 계산 합니다. |
| 34 |[Azure SQL 데이터 웨어하우스의 계산 능력 관리(REST)](sql-data-warehouse-manage-compute-rest-api.md) |PowerShell 작업 toomanage 전원을 계산 합니다. DWU를 조정하여 계산 리소스 크기를 조정합니다. 또는 일시 중지 및 재개 자원 toosave 비용을 계산 합니다. |
| 35 |[Azure SQL 데이터 웨어하우스의 계산 능력 관리(T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Dwu로 조정 하 여 작업 tooscale 아웃 성능 TRANSACT-SQL (T-SQL)입니다. 사용량이 많지 않은 시간 동안 다시 조정하여 비용을 절감합니다. |
| 36 |[DMV를 사용하여 작업 모니터링](sql-data-warehouse-manage-monitor.md) |자세한 내용은 방법 toomonitor Dmv를 사용 하 여 작업 합니다. |
| 37 |[Azure SQL 데이터 웨어하우스의 데이터베이스 관리](sql-data-warehouse-overview-manage.md) |SQL 데이터 웨어하우스 데이터베이스 관리 개요. 관리 도구, DWU 및 성능 확장, 쿼리 성능 문제 해결, 보안 정책 설정, 데이터 손상 또는 지역적 중단으로부터 데이터베이스 복원 등이 포함되어 있습니다. |
| 38 |[Azure SQL 데이터 웨어하우스의 사용자 쿼리 모니터링](sql-data-warehouse-overview-manage-user-queries.md) |Hello 고려 사항, 모범 사례 및 Azure SQL 데이터 웨어하우스에 사용자 쿼리를 모니터링 하는 것에 대 한 작업의 개요 |
| 39 |[SQL Data Warehouse 복원](sql-data-warehouse-restore-database-overview.md) |Azure SQL 데이터 웨어하우스 데이터베이스를 복구 하기 위한 hello 데이터베이스 복원 옵션의 개요입니다. |
| 40 |[Azure SQL 데이터 웨어하우스 복원(포털)](sql-data-warehouse-restore-database-portal.md) |Azure SQL 데이터 웨어하우스 복원을 위한 Azure 포털 작업. |
| 41 |[Azure SQL 데이터 웨어하우스 복원(PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Azure SQL 데이터 웨어하우스 복원을 위한 PowerShell 작업. |
| 42 |[Azure SQL 데이터 웨어하우스 복원(REST API)](sql-data-warehouse-restore-database-rest-api.md) |Azure SQL 데이터 웨어하우스 복원을 위한 REST API 작업. |

## <a name="tables-and-indexes"></a>테이블 및 인덱스
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 43 |[SQL 데이터 웨어하우스 테이블의 데이터 형식](sql-data-warehouse-tables-data-types.md) |Azure SQL 데이터 웨어하우스 테이블에 대한 데이터 형식으로 시작 |
| 44 |[SQL 데이터 웨어하우스의 테이블 배포](sql-data-warehouse-tables-distribute.md) |Azure SQL 데이터 웨어하우스에서 테이블 배포 시작 |
| 45 |[SQL 데이터 웨어하우스의 테이블 인덱싱](sql-data-warehouse-tables-index.md) |Azure SQL 데이터 웨어하우스에서 테이블 인덱싱 시작 |
| 46 |[SQL 데이터 웨어하우스의 테이블 개요](sql-data-warehouse-tables-overview.md) |Azure SQL 데이터 웨어하우스 테이블로 시작 |
| 47 |[SQL 데이터 웨어하우스의 테이블 분할](sql-data-warehouse-tables-partition.md) |Azure SQL 데이터 웨어하우스에서 테이블 분할 시작 |
| 48 |[SQL 데이터 웨어하우스의 테이블에 대한 통계 관리](sql-data-warehouse-tables-statistics.md) |Azure SQL 데이터 웨어하우스에서 테이블에 대한 통계 시작 |
| 49 |[SQL 데이터 웨어하우스의 임시 테이블](sql-data-warehouse-tables-temporary.md) |Azure SQL 데이터 웨어하우스에서 임시 테이블로 시작 |

## <a name="integrate"></a>통합
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 50 |[SQL 데이터 웨어하우스와 함께 Azure 데이터 팩터리 사용](sql-data-warehouse-integrate-azure-data-factory.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스의 Azure 데이터 팩터리(ADF) 사용을 위한 팁 |
| 51 |[SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용](sql-data-warehouse-integrate-azure-machine-learning.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 기계 학습 사용을 위한 팁 |
| 52 |[SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용](sql-data-warehouse-integrate-azure-stream-analytics.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Azure 스트림 분석 사용을 위한 팁 |
| 53 |[SQL 데이터 웨어하우스와 함께 Power BI 사용](sql-data-warehouse-integrate-power-bi.md) |솔루션 개발을 위한 Azure SQL 데이터 웨어하우스와 함께 Power BI 사용을 위한 팁 |
| 54 |[SQL 데이터 웨어하우스와 함께 기타 서비스 활용](sql-data-warehouse-overview-integrate.md) |SQL 데이터 웨어하우스와 통합된 솔루션과 파트너 및 도구 |

## <a name="load"></a>로드
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 55 |[Azure Blob 저장소에서 Azure SQL 데이터 웨어하우스로 데이터 로드(Azure Data Factory)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Azure 데이터 팩터리를 사용 하 여 tooload 데이터에 알아봅니다 |
| 56 |[Azure blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 로드합니다(PolyBase).](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |어떻게 toouse PolyBase tooload 데이터에서 Azure blob 저장소에 SQL 데이터 웨어하우스에 대해 알아봅니다. 공용 데이터에서 몇 가지 테이블을 hello Contoso 소매 데이터 웨어하우스 스키마를 로드 합니다. |
| 57 |[SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Azure SQL 데이터 웨어하우스에 SQL Server tooflat 파일, AZCopy tooimport 데이터 tooAzure blob 저장소 및 PolyBase tooingest hello 데이터에서 bcp tooexport 데이터를 사용합니다. |
| 58 |[SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(플랫 파일)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |작은 데이터 크기에 대 한 Azure SQL 데이터 웨어하우스에 직접 hello 데이터 가져오기 및 SQL Server tooflat 파일에서 bcp tooexport 데이터를 사용 합니다. |
| 59 |[SQL Server에서 Azure SQL 데이터 웨어하우스로 데이터 로드(SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |다양 한 데이터를에서 SQL Server Integration Services (SSIS) 패키지 toomove 데이터 toocreate tooSQL 데이터 웨어하우스 원본 하는 방법을 보여 줍니다. |
| 60 |[SQL 데이터 웨어하우스에서 PolyBase를 사용하여 데이터 로드](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Azure SQL 데이터 웨어하우스에 SQL Server tooflat 파일, AZCopy tooimport 데이터 tooAzure blob 저장소 및 PolyBase tooingest hello 데이터에서 bcp tooexport 데이터를 사용합니다. |
| 61 |[SQL 데이터 웨어하우스의 PolyBase 사용을 위한 가이드](sql-data-warehouse-load-polybase-guide.md) |SQL 데이터 웨어하우스 시나리오에서 PolyBase를 사용하는 방법에 대한 지침 및 권장 사항입니다. |
| 62 |[SQL 데이터 웨어하우스로 샘플 데이터를 로드](sql-data-warehouse-load-sample-databases.md) |SQL 데이터 웨어하우스로 샘플 데이터를 로드 |
| 63 |[bcp를 사용하여 데이터 로드](sql-data-warehouse-load-with-bcp.md) |Bcp 무엇 인지 알아보고 방법과 toouse 데이터 웨어하우징 시나리오에 대 한 것입니다. |
| 64 |[Azure SQL 데이터 웨어하우스에 데이터 로드](sql-data-warehouse-overview-load.md) |SQL 데이터 웨어하우스를 로드 하는 데이터에 대 한 hello 일반적인 시나리오에 알아봅니다. 여기에는 PolyBase, Azure Blob 저장소, 플랫 파일 및 디스크 배송 사용이 포함됩니다. 타사 도구를 사용할 수도 있습니다. |

## <a name="migrate"></a>마이그레이션
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 65 |[SQL 코드 tooSQL 데이터 웨어하우스 마이그레이션](sql-data-warehouse-migrate-code.md) |솔루션 개발을 위한 SQL 코드 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다. |
| 66 |[데이터 마이그레이션](sql-data-warehouse-migrate-data.md) |솔루션 개발을 위한 사용자 데이터 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다. |
| 67 |[데이터 웨어하우스 마이그레이션 유틸리티(미리 보기)](sql-data-warehouse-migrate-migration-utility.md) |데이터 웨어하우스 tooSQL 마이그레이션하십시오. |
| 68 |[사용자 스키마 tooSQL 데이터 웨어하우스 마이그레이션](sql-data-warehouse-migrate-schema.md) |솔루션 개발을 위한 프로그램 스키마 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다. |
| 69 |[사용자 솔루션 tooSQL 데이터 웨어하우스 마이그레이션](sql-data-warehouse-overview-migrate.md) |마이그레이션 지침 tooAzure SQL 데이터 웨어하우스 솔루션 플랫폼으로 전환 합니다. |

## <a name="partners"></a>파트너
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 70 |[SQL 데이터 웨어하우스 비즈니스 인텔리전스 파트너](sql-data-warehouse-partner-business-intelligence.md) |SQL 데이터 웨어하우스를 지원하는 솔루션을 제공하는 타사 비즈니스 인텔리전스 파트너 목록 |
| 71 |[SQL 데이터 웨어하우스 데이터 통합 파트너](sql-data-warehouse-partner-data-integration.md) |Azure SQL 데이터 웨어하우스를 지원하는 데이터 통합 솔루션을 제공하는 타사 파트너 목록 |
| 72 |[SQL 데이터 웨어하우스 데이터 관리 파트너](sql-data-warehouse-partner-data-management.md) |SQL 데이터 웨어하우스를 지원하는 솔루션을 제공하는 타사 데이터 관리 파트너 목록 |

## <a name="reference"></a>참조
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 73 |[SQL 데이터 웨어하우스에 대한 참조 항목](sql-data-warehouse-overview-reference.md) |SQL 데이터 웨어하우스에 대한 참조 콘텐츠 링크 |
| 74 |[SQL 데이터 웨어하우스용 PowerShell cmdlet 및 REST API](sql-data-warehouse-reference-powershell-cmdlets.md) |Azure SQL 데이터 웨어하우스에 대 한 hello 상위 PowerShell cmdlet을 찾을 방법을 비롯 하 여 toopause 하 고 데이터베이스를 다시 시작 합니다. |
| 75 |[언어 요소](sql-data-warehouse-reference-tsql-language-elements.md) |SQL 데이터 웨어하우스에 대 한 사용 되는 hello TRANSACT-SQL 언어 요소에 대 한 링크 tooreference 콘텐츠의 목록입니다. |
| 76 |[Transact-SQL 항목](sql-data-warehouse-reference-tsql-statements.md) |SQL 데이터 웨어하우스에서 사용 하는 hello TRANSACT-SQL 항목 링크 tooreference 콘텐츠입니다. |
| 77 |[시스템 뷰](sql-data-warehouse-reference-tsql-system-views.md) |SQL 데이터 웨어하우스에 대 한 링크 toosystem 보기 콘텐츠입니다. |

## <a name="security"></a>보안
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 78 |[SQL Data Warehouse - 감사 및 동적 데이터 마스킹에 대한 하위 수준 클라이언트 지원](sql-data-warehouse-auditing-downlevel-clients.md) |데이터 감사에 대한 SQL 데이터 웨어하우스 하위 수준 클라이언트 지원에 대해 알아보기 |
| 79 |[Azure SQL 데이터 웨어하우스 감사](sql-data-warehouse-auditing-overview.md) |Azure SQL 데이터 웨어하우스 감사 시작 |
| 80 |[SQL 데이터 웨어하우스에서 투명한 데이터 암호화(TDE) 시작](sql-data-warehouse-encryption-tde.md) |SQL Data Warehouse의 TDE(투명한 데이터 암호화) |
| 81 |[투명한 데이터 암호화(TDE) 시작](sql-data-warehouse-encryption-tde-tsql.md) |SQL Data Warehouse의 TDE(투명한 데이터 암호화)(T-SQL) |
| 82 |[SQL 데이터 웨어하우스에서 데이터베이스 보호](sql-data-warehouse-overview-manage-security.md) |솔루션 개발을 위해 Azure SQL 데이터 웨어하우스에서 데이터베이스를 보호하는 팁 |

## <a name="miscellaneous"></a>기타
| &nbsp; | 제목 | 설명 |
| ---:|:--- |:--- |
| 83 |[SQL Data Warehouse용 Visual Studio 및 SSDT 설치](sql-data-warehouse-install-visual-studio.md) |Azure SQL 데이터 웨어하우스용 Visual Studio 및 SSDT(SQL Server 개발 도구) 설치 |
| 84 |[마이그레이션 tooPremium 저장소 세부 정보](sql-data-warehouse-migrate-to-premium-storage.md) |기존 SQL 데이터 웨어하우스 toopremium 저장소로 마이그레이션하기 위한 지침 |
| 85 |[위협 감지 시작](sql-data-warehouse-security-threat-detection.md) |위협 검색 tooget 시작 하는 방법 |
| 86 |[SQL 데이터 웨어하우스 용량 제한](sql-data-warehouse-service-capacity-limits.md) |SQL 데이터 웨어하우스의 연결, 데이터베이스, 테이블 및 쿼리에 대한 최대값입니다. |
| 87 |[Azure SQL 데이터 웨어하우스 문제 해결](sql-data-warehouse-troubleshoot.md) |Azure SQL 데이터 웨어하우스 문제 해결 |

