---
title: "Azure SQL 데이터 웨어하우스 aaaTroubleshooting | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 문제 해결"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스 문제 해결
이 항목 들이 회사는 고객의 일반적인 문제 해결 질문 hello 중 일부를 나열 합니다.

## <a name="connecting"></a>연결
| 문제 | 해결 방법 |
|:--- |:--- |
| 'NT AUTHORITY\ANONYMOUS LOGON' 사용자에 대해 로그인 실패 (Microsoft SQL Server, 오류: 18456) |AAD 사용자 tooconnect toohello master 데이터베이스를 가져오려고 시도 하지만 master에 사용자를 갖지 않습니다이 오류가 발생 합니다.  이 문제를 지정 하거나 toocorrect hello SQL 데이터 웨어하우스 tooconnect tooat 연결 시간을 선택 하거나 hello 사용자 toohello master 데이터베이스를 추가 합니다.  자세한 내용은 [보안 개요][Security overview]를 참조하세요. |
| hello 서버 보안 주체 ": MyUserName" 않습니다 수 tooaccess hello 현재 보안 컨텍스트 내에서 데이터베이스 "마스터" hello 합니다. 사용자 기본 데이터베이스를 열 수 없습니다. 로그인이 실패했습니다. 사용자 'MyUserName'에 대한 로그인이 실패했습니다. (Microsoft SQL Server, 오류: 916) |AAD 사용자 tooconnect toohello master 데이터베이스를 가져오려고 시도 하지만 master에 사용자를 갖지 않습니다이 오류가 발생 합니다.  이 문제를 지정 하거나 toocorrect hello SQL 데이터 웨어하우스 tooconnect tooat 연결 시간을 선택 하거나 hello 사용자 toohello master 데이터베이스를 추가 합니다.  자세한 내용은 [보안 개요][Security overview]를 참조하세요. |
| CTAIP 오류 |이 오류는 hello SQL server 마스터 데이터베이스를 있지만 hello SQL 데이터 웨어하우스 데이터베이스에 없는 로그인을 만들 때 발생할 수 있습니다.  이 오류를 발생을 살펴보세요 hello [보안 개요] [ Security overview] 문서.  이 문서에서는 toocreate 마스터의 로그인 및 사용자를 만드는 방법 및 방법에 사용자 toocreate hello SQL 데이터 웨어하우스 데이터베이스에 설명 합니다. |
| 방화벽에 의해 차단 |Azure SQL 데이터베이스 서버 및 데이터베이스 수준 방화벽 tooensure만 액세스 tooa 데이터베이스가 있는 IP 주소를 알고로 보호 됩니다. 연결 하기 전에 hello 방화벽은 명시적으로 설정 해야 하는 기본 및 IP 주소 또는 주소 범위의으로 안전 합니다.  tooconfigure 액세스를 위해 방화벽에서 다음과 같이 hello [클라이언트 IP에 대 한 액세스를 허용 하는 서버를 구성] [ Configure server firewall access for your client IP] hello에 [지침 프로 비전] [Provisioning instructions]. |
| 도구 또는 드라이버에 연결할 수 없음 |SQL 데이터 웨어하우스를 사용 하는 것이 좋습니다. [SSMS][SSMS], [Visual Studio 용 SSDT][SSDT for Visual Studio], 또는 [sqlcmd] [ sqlcmd] tooquery 데이터입니다. 드라이버 및 연결 tooSQL 데이터 웨어하우스에 대 한 자세한 내용은 참조 하십시오. [Azure SQL 데이터 웨어하우스에 대 한 드라이버] [ Drivers for Azure SQL Data Warehouse] 및 [tooAzure SQL 데이터 웨어하우스 연결] [ Connect tooAzure SQL Data Warehouse] 문서입니다. |

## <a name="tools"></a>도구
| 문제 | 해결 방법 |
|:--- |:--- |
| Visual Studio 개체 탐색기에 AAD 사용자가 없음 |이는 알려진 문제입니다.  이 문제를 해결에 hello 사용자 보기 [sys.database_principals][sys.database_principals]합니다.  참조 [인증 tooAzure SQL 데이터 웨어하우스] [ Authentication tooAzure SQL Data Warehouse] toolearn Azure Active Directory를 사용 하 여 SQL 데이터 웨어하우스에 대 한 자세한 합니다. |
|수동 스크립팅, hello 스크립팅 마법사를 사용 하 여 또는 SSMS를 통해 연결 하는 느리거나 응답 하지 않는 경우, 생성 오류| 사용자가 만든 hello master 데이터베이스에 있는지 확인 하십시오. 스크립팅 옵션의도 hello 엔진 버전은 "Microsoft Azure SQL 데이터 웨어하우스 버전"으로 설정 하 고 엔진 유형에 "Microsoft Azure SQL 데이터베이스" 있는지 확인 합니다.|

## <a name="performance"></a>성능
| 문제 | 해결 방법 |
|:--- |:--- |
| 쿼리 성능 문제 해결 |특정 쿼리 tootroubleshoot을 시도 하는 경우 시작 [학습 방법을 toomonitor 쿼리][Learning how toomonitor your queries]합니다. |
| 쿼리 성능 및 계획이 부적합하여 종종 통계가 누락됨 |성능 저하의 가장 일반적인 원인은 hello 테이블에 대 한 통계의 부족입니다.  참조 [테이블 통계를 유지 관리] [ Statistics] 방법에 대 한 자세한 내용은 toocreate 통계 및 중요 한 tooyour 성능은 이유입니다. |
| 낮은 동시성/큐에 쿼리 대기 |이해 [작업 관리] [ Workload management] 하는 데 중요 순서 toounderstand 어떻게 동시성 관련 toobalance 메모리를 할당 합니다. |
| 어떻게 tooimplement에 대 한 유용한 정보 |hello 최상의 위치 toostart toolearn 방법 tooimprove 쿼리 성능이 매우 [SQL 데이터 웨어하우스 모범 사례] [ SQL Data Warehouse best practices] 문서. |
| 방법으로 확장 tooimprove 성능 |Hello 솔루션 tooimproving 성능이 toosimply를가 하는 경우에 따라 전원 tooyour 쿼리에 계산 추가 [SQL 데이터 웨어하우스 확장][Scaling your SQL Data Warehouse]합니다. |
| 인덱스 품질 저하로 인한 쿼리 성능 저하 |경우에 따라 [columnstore 인덱스 품질 저하][Poor columnstore index quality]로 인해 쿼리가 느려질 수 있습니다.  자세한 내용은이 문서를 참조 및 어떻게 너무[tooimprove 세그먼트 품질 인덱스를 다시 작성][Rebuild indexes tooimprove segment quality]합니다. |

## <a name="system-management"></a>시스템 관리
| 문제 | 해결 방법 |
|:--- |:--- |
| 서버 hello 허용 45000의 데이터베이스 트랜잭션 단위 할당량을 초과 하므로 메시지 40847: hello 작업을 수행할 수 없습니다. |Hello를 줄이거나 [DWU] [ DWU] hello 데이터베이스의 고치려는 toocreate 또는 [할당량 증가 요청][request a quota increase]합니다. |
| 공간 사용률 조사 |참조 [크기 테이블] [ Table sizes] 시스템의 toounderstand hello 공간 사용률입니다. |
| 테이블 관리 도움말 |Hello 참조 [테이블 개요] [ Overview] 관리 테이블에 대 한 도움말 문서.  이 문서에는 [테이블 데이터 유형][Data types], [테이블 배포][Distribute], [테이블 인덱싱][Index],  [테이블 분할][Partition], [테이블 통계 유지 관리][Statistics] 및 [임시 테이블][Temporary]과 같이 좀 더 자세한 항목으로 연결되는 링크가 포함되어 있습니다. |
|투명 한 데이터 암호화 (TDE) 진행률 표시줄이 hello Azure 포털에서에서 업데이트 되지 않는|통해 tde hello 상태를 볼 수 [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption)합니다.|

## <a name="polybase"></a>Polybase
| 문제 | 해결 방법 |
|:--- |:--- |
| 대용량 행으로 인해 로드 실패 |현재 대용량 행 지원은 Polybase에서 사용할 수 없습니다.  이 테이블에는 varchar (max), nvarchar (max) 또는 varbinary (max)에, 외부 테이블 수 없다는 것을 의미 tooload 사용 되는 데이터를 수 있습니다.  큰 행에 대 한 로드는 현재 (BCP)와 Azure 데이터 팩터리, Azure 스트림 분석, SSIS, BCP 또는 hello.NET SQLBulkCopy 클래스를 통해 에서만 지원 됩니다. 대용량 행에 대한 PolyBase 지원은 후속 릴리스에 추가될 예정입니다. |
| MAX 데이터 형식을 갖는 테이블의 bcp 로드 실패 |일부 시나리오에서는 hello 테이블의 hello 끝에 varchar (max), nvarchar (max) 또는 varbinary (max)을 배치 하는 것을 요구 하는 알려진된 문제가 있습니다.  Hello 테이블의 최대 열 toohello 최종 이동 하십시오. |

## <a name="differences-from-sql-database"></a>SQL 데이터베이스와의 차이점
| 문제 | 해결 방법 |
|:--- |:--- |
| 지원되지 않는 SQL 데이터베이스 기능 |[지원되지 않는 테이블 기능][Unsupported table features]을 참조하세요. |
| 지원되지 않는 SQL 데이터베이스 데이터 형식 |[지원되지 않는 데이터 형식][Unsupported data types]을 참조하세요. |
| DELETE 및 UPDATE 제한 사항 |참조 [업데이트 대안][UPDATE workarounds], [DELETE 대안] [ DELETE workarounds] 및 [지원 되지 않는 업데이트 주위를 사용 하 여 CTAS toowork 및 DELETE 구문][Using CTAS toowork around unsupported UPDATE and DELETE syntax]합니다. |
| MERGE 문이 지원되지 않음 |[MERGE 해결 방법][MERGE workarounds]을 참조하세요. |
| 저장 프로시저 제한 사항 |참조 [저장 프로시저의 제한 사항] [ Stored procedure limitations] toounderstand 저장된 프로시저의 hello 제한 사항 중 일부입니다. |
| UDF가 SELECT 문을 지원하지 않음 |이 문제가 UDF의 현재 제한 사항입니다.  참조 [CREATE FUNCTION] [ CREATE FUNCTION] hello 구문을 지원 합니다. |

## <a name="next-steps"></a>다음 단계
있다면 문제인 없습니다 toofind 솔루션 tooyour 위, 다음은 다른 리소스 시도할 수 있습니다.

* [블로그]
* [기능 요청]
* [비디오]
* [CAT 팀 블로그]
* [지원 티켓 만들기]
* [MSDN 포럼]
* [Stack Overflow 포럼]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[지원 티켓 만들기]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[블로그]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[CAT 팀 블로그]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[기능 요청]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN 포럼]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Stack Overflow 포럼]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[비디오]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
