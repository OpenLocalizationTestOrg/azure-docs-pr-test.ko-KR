---
title: "aaaSQL 오류 코드-데이터베이스 연결 오류 | Microsoft Docs"
description: "일반적인 데이터베이스 연결 오류, 데이터베이스 복사 문제 및 일반적인 오류와 같은 SQL 데이터베이스 클라이언트 응용 프로그램에 대한 SQL 오류 코드에 대해 알아봅니다. "
keywords: "SQL 오류 코드, 액세스 SQL, 데이터베이스 연결 오류, SQL 오류 코드"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>SQL 데이터베이스 클라이언트 응용 프로그램의 SQL 오류 코드: 데이터베이스 연결 오류 및 기타 문제
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


이 문서에서는 데이터베이스 연결 오류, 일시적인 오류(일시적인 폴트라고도 함), 리소스 거버넌스 오류, 데이터베이스 복사 문제, 탄력적 풀 및 기타 오류를 포함하여 SQL 데이터베이스 클라이언트 응용 프로그램의 SQL 오류 코드를 나열합니다. 대부분의 범주는 특정 tooAzure SQL 데이터베이스 되며 tooMicrosoft SQL Server는 적용 되지 않습니다.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>데이터베이스 연결 오류, 일시적인 오류 및 기타 임시 오류
hello 다음 표에 hello 연결 끊김 오류 및 기타 일시적인 오류 응용 프로그램이 tooaccess SQL 데이터베이스를 시도할 때 발생할 수 있습니다. SQL 오류 코드입니다. 시작 하기 자습서는 방법에 대 한 tooconnect tooAzure SQL 데이터베이스 참조 [tooAzure SQL 데이터베이스 연결](sql-database-libraries.md)합니다.

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>가장 일반적인 데이터베이스 연결 오류 및 일시적인 오류
hello Azure 인프라에 과도 한 작업 부하 hello SQL 데이터베이스 서비스에서에서 발생 하는 경우에 서버를 다시 구성 하는 hello 기능 toodynamically 있습니다.  이 동적 동작 클라이언트 프로그램 toolose 발생할 수 있습니다는 연결 tooSQL 데이터베이스입니다. 이러한 종류의 오류 상황을 *일시적 장애*라고 합니다.

자체 hello 일시적인 오류 시간 toocorrect 권한을 부여한 후 연결을 다시 설정할 수 있도록 클라이언트 프로그램에 다시 시도 논리가 것이 좋습니다.  첫 번째 재시도 전에 5초간 지연하는 것이 좋습니다. 5 초 보다 짧은 지연 후 다시 시도 hello 클라우드 서비스를 진행 하기가 매우 될 위험이 있습니다. 각 후속 재시도 대 한 hello 지연 증가 하도록 기하급수적으로 tooa를 최대 60 초입니다.

일시적인 오류는 일반적으로 hello 클라이언트 프로그램에서 다음과 같은 오류 메시지 중 하나로 매니페스트:

* &lt;Azure_instance&gt; 서버에서 &lt;db_name&gt; 데이터베이스를 현재 사용할 수 없는 경우. 나중에 hello 연결을 다시 시도 하십시오. Hello 문제가 계속 되 면 고객 지원에 문의 하 고 hello 세션 추적 ID를 제공 &lt;session_id&gt;
* &lt;Azure_instance&gt; 서버에서 &lt;db_name&gt; 데이터베이스를 현재 사용할 수 없는 경우. 나중에 hello 연결을 다시 시도 하십시오. Hello 문제가 계속 되 면 고객 지원에 문의 하 고 hello 세션 추적 ID를 제공 &lt;session_id&gt;합니다. (Microsoft SQL Server, 오류: 40613)
* 기존 연결 hello 원격 호스트에 의해 강제로 끊겼습니다.
* System.Data.Entity.Core.EntityCommandExecutionException: hello 명령 정의 실행 하는 동안 오류가 발생 했습니다. Hello 자세한 내용은 내부 예외를 참조 하십시오. System.Data.SqlClient.SqlException--->: hello 서버에서 결과 받을 때 전송 수준 오류가 발생 했습니다. (공급자: 세션 공급자, 오류: 19 - 실제 연결을 사용할 수 없습니다.)
* 연결 시도가 tooa 보조 데이터베이스에는 hello 데이터베이스가 reconfguration hello 과정에는 hello 주 데이터베이스에서 활성 거래의 hello 가운데에 중에 새 페이지 적용 중 때문에 실패 했습니다. 

다시 시도 논리의 코드 예제는 다음을 참조하십시오.

* [SQL 데이터베이스 및 SQL Server에 대한 연결 라이브러리](sql-database-libraries.md) 
* [작업 toofix 연결 오류 및 SQL 데이터베이스의 일시적 오류](sql-database-connectivity-issues.md)

Hello에 대 한 내용은 *차단 기간* ADO.NET을 사용 하는 클라이언트에서 사용할 수는 [SQL Server 연결 풀링 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)합니다.

### <a name="transient-fault-error-codes"></a>일시적 오류 코드
hello 다음과 같은 오류는 일시적인 항목 및 응용 프로그램 논리에 다시 시도해 야 합니다. 

| 오류 코드 | 심각도 | 설명 |
| ---:| ---:|:--- |
| 4060 |16 |데이터베이스를 열 수 없습니다 "%. & #x2a; ls" hello 로그인에서 요청한 합니다. hello 로그인 하지 못했습니다. |
| 40197 |17 |hello 서비스 요청을 처리 하는 오류가 발생 했습니다. 나중에 다시 시도하세요. 오류 코드 %d.<br/><br/>Hello 서비스 중지 기한 toosoftware 또는 하드웨어 업그레이드, 하드웨어 오류 또는 다른 장애 조치 문제가 되는 경우이 오류를 받습니다. 오류 40197의 hello 메시지 내에 포함 된 hello 오류 코드 (%d) hello 종류의 오류 또는 발생 한 장애 조치에 대 한 추가 정보를 제공 합니다. 코드 오류 40197의 hello 메시지에 포함 된 hello 오류의 예로 40020, 40143, 40166 및 40540는 있습니다.<br/><br/>다시 연결 중인 tooyour SQL 데이터베이스 서버는 해당 데이터베이스의 tooa 정상 복사본 자동으로 연결 됩니다. 응용 프로그램 해야 오류 40197을 로그 hello 포함 된 오류 코드 (%d) 문제 해결을 위해 hello 메시지 내에서 catch 하 고 hello 리소스를 사용할 수 있고 연결이 다시 설정 될 때까지 tooSQL 데이터베이스를 다시 연결 하십시오. |
| 40501 |20 |hello 서비스가 현재 사용 중입니다. 10 초 후 hello 요청을 다시 시도 합니다. 인시던트 ID: %ls. 코드: %d.<br/><br/>*참고:* 자세한 내용은 다음을 참조하세요.<br/>• [Azure SQL 데이터베이스 리소스 제한](sql-database-resource-limits.md)을 참조하세요. |
| 40613 |17 |서버의 데이터베이스 '%.&#x2a;ls' '%.&#x2a;ls'을(를) 사용할 수 없습니다. 나중에 hello 연결을 다시 시도 하십시오. Hello 문제가 계속 되 면 고객 지원에 문의 하 고 hello 세션 추적 ID를 제공 '%. & #x2a; l s'입니다. |
| 49918 |16 |요청을 처리할 수 없습니다. 리소스 부족 tooprocess 요청입니다.<br/><br/>hello 서비스가 현재 사용 중입니다. Hello 요청을 나중에 다시 시도 하십시오. |
| 49919 |16 |요청을 만들거나 업데이트하는 처리를 할 수 없습니다. 구독 "%ld"에 대해 진행 중인 작업을 너무 많이 만들거나 업데이트합니다.<br/><br/>hello 서비스 사용량이 만들기 또는 업데이트 구독 또는 서버에 대 한 요청 여러 처리 합니다. 요청은 현재 리소스 최적화에 대해 차단됩니다. 보류 중인 작업에 대해 [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx)를 쿼리합니다. 만들기 또는 업데이트를 보류 중인 요청이 완료되거나 보류 중인 요청 중 하나를 삭제할 때까지 대기하고 나중에 요청을 다시 시도합니다. |
| 49920 |16 |요청을 처리할 수 없습니다. 구독 "%ld"에 대해 진행 중인 작업을 너무 많습니다.<br/><br/>hello 서비스가이 구독에 대 한 여러 요청을 처리 중입니다. 요청은 현재 리소스 최적화에 대해 차단됩니다. 작업 상태에 대해 [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx)를 쿼리합니다. 보류 중인 요청이 완료되거나 보류 중인 요청 중 하나를 삭제할 때까지 대기하고 나중에 요청을 다시 시도합니다. |
| 4221 |16 |로그인 tooread-보조 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING' toolong 기다리는 못했습니다. hello 복제본 사용할 수 없는 경우 로그인에 대 한 행 버전 진행 중이 던 hello 복제본이 재활용 될 트랜잭션에 대 한 누락 되었기 때문에 hello hello 주 복제본에 활성 트랜잭션이 커밋 또는 롤백하는 hello 문제를 해결할 수 있습니다. 기본 hello에서 긴 쓰기 트랜잭션을 방지 하 여이 조건의 발생 빈도 최소화할 수 있습니다. |

## <a name="database-copy-errors"></a>데이터베이스 복사 오류
다음 오류 hello Azure SQL 데이터베이스에서 데이터베이스를 복사 하는 동안 발생할 수 있습니다. 자세한 내용은 [Azure SQL 데이터베이스 복사](sql-database-copy.md)를 참조하세요.

| 오류 코드 | 심각도 | 설명 |
| ---:| ---:|:--- |
| 40635 |16 |IP 주소 '%.&#x2a;ls'을(를) 사용하는 클라이언트가 일시적으로 비활성화되었습니다. |
| 40637 |16 |데이터베이스 복사본 만들기를 현재 사용할 수 없습니다. |
| 40561 |16 |데이터베이스를 복사하지 못했습니다. Hello 소스 또는 대상 데이터베이스 이거나 존재 하지 않습니다. |
| 40562 |16 |데이터베이스를 복사하지 못했습니다. hello 원본 데이터베이스가 삭제 되었습니다. |
| 40563 |16 |데이터베이스를 복사하지 못했습니다. hello 대상 데이터베이스가 삭제 되었습니다. |
| 40564 |16 |Tooan 내부 오류 때문에 데이터베이스 복사 하지 못했습니다. 대상 데이터베이스를 삭제하고 다시 시도하십시오. |
| 40565 |16 |데이터베이스를 복사하지 못했습니다. Hello 동일한 원본을 사용할 수에서 1 개 이하의 동시 데이터베이스 복사본입니다. 대상 데이터베이스를 삭제하고 나중에 다시 시도하십시오. |
| 40566 |16 |Tooan 내부 오류 때문에 데이터베이스 복사 하지 못했습니다. 대상 데이터베이스를 삭제하고 다시 시도하십시오. |
| 40567 |16 |Tooan 내부 오류 때문에 데이터베이스 복사 하지 못했습니다. 대상 데이터베이스를 삭제하고 다시 시도하십시오. |
| 40568 |16 |데이터베이스를 복사하지 못했습니다. 원본 데이터베이스를 사용할 수 없습니다. 대상 데이터베이스를 삭제하고 다시 시도하십시오. |
| 40569 |16 |데이터베이스를 복사하지 못했습니다. 대상 데이터베이스를 사용할 수 없습니다. 대상 데이터베이스를 삭제하고 다시 시도하십시오. |
| 40570 |16 |Tooan 내부 오류 때문에 데이터베이스 복사 하지 못했습니다. 대상 데이터베이스를 삭제하고 나중에 다시 시도하십시오. |
| 40571 |16 |Tooan 내부 오류 때문에 데이터베이스 복사 하지 못했습니다. 대상 데이터베이스를 삭제하고 나중에 다시 시도하십시오. |

## <a name="resource-governance-errors"></a>리소스 관리 오류
다음 오류 hello는 Azure SQL 데이터베이스 작업을 수행 하는 동안 리소스의 과도 한 사용으로 발생 합니다. 예:

* 트랜잭션이 너무 오랫동안 열려 있었습니다.
* 트랜잭션이 너무 많은 잠금을 보유하고 있습니다.
* 응용 프로그램이 너무 많은 메모리를 사용하고 있습니다.
* 응용 프로그램이 너무 많은 `TempDb` 공간을 사용하고 있습니다.

관련 항목:

* 자세한 정보는 여기에서 제공됩니다. [Azure SQL Database 리소스 제한](sql-database-resource-limits.md)

| 오류 코드 | 심각도 | 설명 |
| ---:| ---:|:--- |
| 10928 |20 |리소스 ID: %d입니다. hello %s hello 데이터베이스에 대 한 %d 한계와 도달 했습니다. 자세한 내용은 [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637)을 참조하세요.<br/><br/>hello 리소스 ID가 hello 제한에 도달 하는 hello 리소스를 나타냅니다. 작업자 스레드의 경우 리소스 ID hello = 1입니다. 세션에 대 한 hello 리소스 ID = 2입니다.<br/><br/>*참고:* 이 오류에 대 한 자세한 내용은 방법과 tooresolve를 참조 하세요.<br/>• [Azure SQL 데이터베이스 리소스 제한](sql-database-resource-limits.md)을 참조하세요. |
| 10929 |20 |리소스 ID: %d입니다. hello %s 최소값은 %d, 최대 한도 %d 및 hello hello 데이터베이스에 대 한 현재 사용량은 %d입니다. 그러나 hello 서버가 현재이 데이터베이스에 대 한 %d 보다 큰 사용량이 toosupport 요청입니다. 자세한 내용은 [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637)을 참조하세요. 그렇지 않으면 나중에 다시 시도하세요.<br/><br/>hello 리소스 ID가 hello 제한에 도달 하는 hello 리소스를 나타냅니다. 작업자 스레드의 경우 리소스 ID hello = 1입니다. 세션에 대 한 hello 리소스 ID = 2입니다.<br/><br/>*참고:* 이 오류에 대 한 자세한 내용은 방법과 tooresolve를 참조 하세요.<br/>• [Azure SQL 데이터베이스 리소스 제한](sql-database-resource-limits.md)을 참조하세요. |
| 40544 |20 |hello 데이터베이스가 크기 할당량에 도달 했습니다. 파티션 또는 삭제 데이터는 인덱스를 삭제 또는 가능한 해결 방법에 대 한 hello 설명서를 참조 하십시오. |
| 40549 |16 |실행 시간이 긴 트랜잭션이 있으므로 세션이 종료됩니다. 트랜잭션 실행 시간을 줄이십시오. |
| 40550 |16 |잠금을 너무 많이 획득 hello 세션이 종료 되었습니다. 단일 트랜잭션에서 읽기 또는 수정 행 수를 줄이십시오. |
| 40551 |16 |과도 한 많아 hello 세션이 종료 된 `TEMPDB` 사용 합니다. 쿼리 tooreduce hello 임시 테이블 공간 사용량을 수정 하세요.<br/><br/>*팁:* 임시 개체를 사용 하는 경우 hello의 공간을 절약할 `TEMPDB` hello 세션에서 더 이상 필요 없는 임시 개체를 삭제 하 여 데이터베이스입니다. |
| 40552 |16 |과도 한 트랜잭션 로그 공간 사용으로 인해 hello 세션이 종료 되었습니다. 단일 트랜잭션에서 행 수를 줄이세요.<br/><br/>*팁:* hello를 사용 하 여 대량 삽입을 수행 하는 경우 `bcp.exe` 유틸리티 또는 hello `System.Data.SqlClient.SqlBulkCopy` 클래스, hello를 사용 하 여 시도 `-b batchsize` 또는 `BatchSize` 행 수가 toolimit hello 옵션 각 트랜잭션에서 toohello 서버를 복사 합니다. Hello이 있는 인덱스 다시 작성 하는 경우 `ALTER INDEX` 문, try hello를 사용 하 여 `REBUILD WITH ONLINE = ON` 옵션입니다. |
| 40553 |16 |메모리 사용량이 너무 많아 hello 세션이 종료 되었습니다. 수정 하세요 쿼리 tooprocess 행 수가 더 줄어듭니다.<br/><br/>*팁:* hello 수를 줄입니다 `ORDER BY` 및 `GROUP BY` Transact SQL 코드의 작업에는 쿼리 hello 메모리 요구 사항을 줄일 수 있습니다. |

## <a name="elastic-pool-errors"></a>탄력적 풀 오류
다음 오류 hello은 관련된 toocreating 및 Elastics 풀을 사용 하 여입니다.

| ErrorNumber | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |hello 탄력적인 풀이 저장소 제한에 도달 했습니다. hello 탄력적 풀에 대 한 hello 저장소 사용량 (%d) Mb를 초과할 수 없습니다. |MB 단위의 탄력적 풀 공간 한도. |Hello 탄력적 풀의 hello 저장소 용량 한도 도달한 경우 toowrite 데이터 tooa 데이터베이스를 시도 합니다. |Hello 탄력적 풀의 가능한 경우 순서 tooincrease 증가 hello Dtu 할당량 제한을 고려, hello 탄력적 풀에서 개별 데이터베이스에서 사용 하는 hello 저장소를 줄일 하거나 hello 탄력적 풀에서 데이터베이스를 제거 하십시오. |
| 10929 |EX_USER |hello %s 최소값은 %d, 최대 한도 %d 및 hello hello 데이터베이스에 대 한 현재 사용량은 %d입니다. 그러나 hello 서버가 현재이 데이터베이스에 대 한 %d 보다 큰 사용량이 toosupport 요청입니다. 도움이 필요하면 [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) 을 참조하세요. 그렇지 않으면 나중에 다시 시도하세요. |데이터베이스당 DTU 최소값, 데이터베이스당 DTU 최대값 |hello 탄력적 풀 시도한 tooexceed hello 풀 제한에서 모든 데이터베이스에서 동시 작업자 (요청)의 총 수를 hello 합니다. |Hello hello 탄력적 풀의 가능한 경우 순서 tooincrease Dtu에서 작업자 제한 증가 고려 하거나 hello 탄력적 풀에서 데이터베이스를 제거 하십시오. |
| 40844 |EX_USER |서버 '%ls'에 있는 데이터베이스 '%ls'은(는) 탄력적 풀에 포함된 '%ls' 버전 데이터베이스이며, 연속 복사 관계를 가질 수 없습니다. |데이터베이스 이름, 데이터베이스 버전, 서버 이름 |탄력적 풀에 있는 프리미엄이 아닌 데이터베이스에 대해 StartDatabaseCopy 명령이 발급되었습니다. |서비스 예정 |
| 40857 |EX_USER |서버: '%ls'에서 탄력적 풀을 찾을 수 없음, 탄력적 풀 이름: '%ls'. |서버 이름, 탄력적 풀 이름 |지정 된 탄력적 풀이 hello 지정 된 서버에 존재 하지 않습니다. |유효한 탄력적 풀 이름을 입력하세요. |
| 40858 |EX_USER |탄력적 풀 '%ls'이(가) 서버 '%ls'에 이미 있습니다. |탄력적 풀 이름, 서버 이름 |지정 된 탄력적 풀이 hello 지정 된 논리 서버에 이미 있습니다. |새 탄력적 풀 이름을 입력하세요. |
| 40859 |EX_USER |탄력적 풀이 서비스 계층 '%ls'을(를) 지원하지 않습니다. |탄력적 풀 서비스 계층 |지정한 서비스 계층은 탄력적 풀 프로비저닝에 대해 지원되지 않습니다. |Hello 정확한 버전을 제공 하거나 서비스 계층 빈 toouse hello 기본 서비스 계층을 유지 합니다. |
| 40860 |EX_USER |탄력적 풀 '%ls' 및 서비스 목표'%ls'의 조합은 유효하지 않습니다. |탄력적 풀 이름, 서비스 수준 목표 이름 |서비스 목표가 'ElasticPool'로 지정된 경우에만 탄력적 풀과 서비스 목표를 함께 지정할 수 있습니다. |탄력적 풀과 서비스 목표의 올바른 조합을 지정하세요. |
| 40861 |EX_USER |hello 데이터베이스 버전 ' %. *l s은 인 hello 탄력적인 풀 서비스 계층과 다를 수 없습니다 ' %.* l s. |데이터베이스 버전, 탄력적 풀 서비스 계층 |hello 데이터베이스 버전은 hello 탄력적인 풀 서비스 계층과 다릅니다. |hello 탄력적인 풀 서비스 계층과 달리 데이터베이스 버전을 지정 하지 마십시오.  Note 해당 hello 데이터베이스 버전 지정 toobe 필요 하지 않습니다. |
| 40862 |EX_USER |탄력적 풀 이름은 해야 hello 탄력적인 풀 서비스 목표가 지정 된 경우 지정 합니다. |없음 |탄력적 풀 서비스 목표가 탄력적 풀을 고유하게 식별하지 못합니다. |탄력적인 풀 서비스 목표가 hello를 사용 하는 경우 hello 탄력적인 풀 이름을 지정 하십시오. |
| 40864 |EX_USER |hello 탄력적 풀에 대 한 hello Dtu 이상 이어야 합니다 (%d) Dtu 서비스 계층에 대 한 ' %. * l s. |탄력적 풀의 DTU, 탄력적 풀 서비스 계층 |Hello 최소 제한 값 아래로 hello 탄력적 풀에 대 한 Dtu tooset hello를 시도합니다. |탄력적 풀 tooat hello에 대 한 Dtu hello 설정 다시 시도 하세요. 최소 hello 최소 제한 합니다. |
| 40865 |EX_USER |hello 탄력적 풀에 대 한 Dtu hello (%d) Dtu 서비스 계층에 대 한를 초과할 수 없습니다 ' %. * l s. |탄력적 풀의 DTU, 탄력적 풀 서비스 계층 |Hello 최대 제한 초과 hello 탄력적 풀에 대 한 Dtu tooset hello를 시도합니다. |탄력적 풀 toono hello에 대 한 hello Dtu hello 최대 한도 보다 큰 값으로 설정 다시 시도 하십시오. |
| 40867 |EX_USER |데이터베이스당 DTU 최대값 hello에 있어야 합니다. 최소 (%d)에 대 한 서비스 계층 ' %. * l s. |데이터베이스당 DTU 최대값, 탄력적 풀 서비스 계층 |Tooset hello hello 아래 데이터베이스당 DTU 최대값 시도 한도 지원 됩니다. |지 원하는 hello 설정을 원하는 hello 탄력적인 풀 서비스 계층을 사용 하 여 고려 하십시오. |
| 40868 |EX_USER |서비스 계층에 대 한 hello 데이터베이스당 DTU 최대값 (%d)를 초과할 수 없습니다 ' %. * l s. |데이터베이스당 DTU 최대값, 탄력적 풀 서비스 계층 |Tooset hello hello 초과 데이터베이스당 DTU 최대값 시도 한도 지원 됩니다. |지 원하는 hello 설정을 원하는 hello 탄력적인 풀 서비스 계층을 사용 하 여 고려 하십시오. |
| 40870 |EX_USER |데이터베이스당 DTU 최소값 hello 서비스 계층에 대하여 (%d)를 초과할 수 없습니다 ' %. * l s. |데이터베이스당 DTU 최소값, 탄력적 풀 서비스 계층 |Tooset hello 최소 DTU hello 이상 데이터베이스는 지원 되는 제한 합니다. |지 원하는 hello 설정을 원하는 hello 탄력적인 풀 서비스 계층을 사용 하 여 고려 하십시오. |
| 40873 |EX_USER |hello 데이터베이스 수 (%d) 및 (%d) 데이터베이스당 DTU 최소값 hello 탄력적 풀 (%d)의 hello Dtu를 초과할 수 없습니다. |탄력적 풀에 포함된 데이터베이스 수, 데이터베이스당 DTU 최소값, 탄력적 풀의 DTU |Hello hello 탄력적 풀의 Dtu를 초과 하는 hello 탄력적 풀의 데이터베이스에 대 한 DTU 최소값 toospecify 하려고 합니다. |하십시오 hello hello 탄력적 풀의 Dtu를 늘리는 것이 좋습니다 또는, 데이터베이스당 DTU 최소값 hello 줄이거나 hello hello 탄력적 풀의 데이터베이스 수를 줄입니다. |
| 40877 |EX_USER |탄력적 풀에 데이터베이스가 포함되어 있으면 삭제할 수 없습니다. |없음 |hello 탄력적 풀은 하나 이상의 데이터베이스를 포함 하며 삭제할 수 없습니다. |하십시오 제거의 데이터베이스에 순서 toodelete hello 탄력적 풀에서 해당 합니다. |
| 40881 |EX_USER |탄력적 풀 hello ' %. * l s에 해당 데이터베이스 수 제한에 도달 했습니다.  hello 탄력적 풀에 대 한 hello 데이터베이스 수 제한 (%d) Dtu와 탄력적 풀에 대 한 (%d)를 초과할 수 없습니다. |탄력적 풀 이름, 탄력적 풀의 데이터베이스 개수 한도, 리소스 풀의 DTU. |Toocreate 시도 하거나 hello 탄력적 풀의 hello 데이터베이스 수 제한에 도달한 경우 데이터베이스 tooelastic 풀을 추가 합니다. |Hello hello 탄력적 풀의 가능한 경우 순서 tooincrease Dtu 데이터베이스도 늘리는 것이 좋습니다 하거나 hello 탄력적 풀에서 데이터베이스를 제거 하십시오. |
| 40889 |EX_USER |hello Dtu 또는 hello 탄력적 풀 저장소 용량 한도 ' %. * l s를 얻을 수 없는 충분 한 저장 공간 해당 데이터베이스에 대 한 이후 낮출 수 없습니다. |탄력적 풀의 이름 |해당 저장소 사용 아래 hello 탄력적 풀의 toodecrease hello 저장소 용량 한도 시도합니다. |Hello 탄력적 풀의 개별 데이터베이스의 hello 저장소 사용량을 줄여 보세요 또는 해당 Dtu 또는 저장소 순서 tooreduce hello 풀에서 데이터베이스 제거 제한 합니다. |
| 40891 |EX_USER |(%d) 데이터베이스당 DTU 최소값 hello (%d) 데이터베이스당 DTU 최대값 hello를 초과할 수 없습니다. |데이터베이스당 DTU 최소값, 데이터베이스당 DTU 최대값 |Hello 데이터베이스당 DTU 최대값 보다 높은 데이터베이스당 tooset hello DTU 최소값을 시도합니다. |Hello 데이터베이스 최소 DTU hello 데이터베이스당 DTU 최대값을 초과 하지 않는지 확인 하십시오. |
| TBD |EX_USER |탄력적 풀에서 개별 데이터베이스에 대 한 hello 저장소 크기에서 허용 하는 hello 최대 크기를 초과할 수 없습니다 ' %. * l s 서비스 계층 탄력적 풀입니다. |탄력적 풀 서비스 계층 |hello hello 데이터베이스에 대 한 최대 크기는 hello hello 탄력적인 풀 서비스 계층에서 허용 되는 최대 크기를 초과 합니다. |Hello hello hello hello 탄력적인 풀 서비스 계층에서 허용 되는 최대 크기의 hello 제한 내에 데이터베이스의 최대 크기를 설정 하십시오. |

관련 항목:

* [탄력적 풀 만들기(C#)](sql-database-elastic-pool-manage-csharp.md) 
* [탄력적 풀을 관리합니다(C#)](sql-database-elastic-pool-manage-csharp.md). 
* [탄력적 풀 만들기(PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [탄력적 풀을 모니터링하고 관리합니다(PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>일반 오류
다음 오류 hello 이전 범주에 포함 되지 않습니다.

| 오류 코드 | 심각도 | 설명 |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin>은 잘못된 문자를 포함하므로 올바른 이름이 아닙니다. |
| 18452 |14 |로그인이 실패했습니다. hello 로그인이 트러스트 되지 않은 도메인에서 하 고 Windows authentication.%. & #x2a; 함께 사용할 수 없습니다 (Windows 로그인이이 버전의 SQL Server에서 지원 되지 않습니다.) ls |
| 18456 |14 |사용자에 대 한 로그인 하지 못했습니다. ' %. #x2a;ls'.%. & #x2a; ls %. & #x2a; ls (사용자에 대 한 hello 로그인 하지 못했습니다. "%. & #x2a; ls". hello 암호 변경 하지 못했습니다. 해당 버전의 SQL Server에서 로그인 시 암호 변경이 지원되지 않습니다.) |
| 18470 |14 |사용자 '%.&#x2a;ls'에 대한 로그인이 실패했습니다. 원인: hello 계정은 disabled.%. & #x2a; ls |
| 40014 |16 |Hello에 여러 데이터베이스를 사용할 수 없습니다 동일한 트랜잭션. |
| 40054 |16 |클러스터형 인덱스가 없는 테이블은 해당 버전의 SQL Server에서 지원되지 않습니다. 클러스터형 인덱스를 만들고 다시 시도하십시오. |
| 40133 |15 |이 작업은 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40506 |16 |지정된 SID가 해당 버전의 SQL Server에 유효하지 않습니다. |
| 40507 |16 |해당 버전의 SQL Server에서 '%.&#x2a;ls'을(를) 매개 변수와 함께 호출할 수 없습니다. |
| 40508 |16 |USE 문은 데이터베이스 간에 지원 되는 tooswitch 않습니다. 새 연결 tooconnect tooa 다른 데이터베이스를 사용 합니다. |
| 40510 |16 |문 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40511 |16 |기본 제공 기능 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40512 |16 |사용되지 않은 기능 '%ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40513 |16 |서버 변수 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40514 |16 |'%ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40515 |16 |참조 toodatabase 및/또는 서버 이름에 '%. & #x2a; l s'이 버전의 SQL Server에서 지원 되지 않습니다. |
| 40516 |16 |전역 임시 개체는 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40517 |16 |키워드 또는 문 옵션 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40518 |16 |DBCC 명령 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40520 |16 |보안 개체 클래스 '%S_MSG'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40521 |16 |보안 개체 클래스 '%S_MSG' hello 서버 범위에서이 버전의 SQL Server에서 지원 되지 않습니다. |
| 40522 |16 |데이터베이스 보안 주체 '%.&#x2a;ls' 형식은 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40523 |16 |암시적 사용자 '%.&#x2a;ls' 만들기는 해당 버전의 SQL Server에서 지원되지 않습니다. 명시적으로 사용 하기 전에 hello 사용자를 만듭니다. |
| 40524 |16 |데이터 형식 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40525 |16 |WITH '%.ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40526 |16 |'%.&#x2a;ls' 행 집합 공급자는 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40527 |16 |연결된 서버는 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40528 |16 |사용자가 매핑된 toocertificates, 비대칭 키 또는 Windows 로그인이이 버전의 SQL Server에 수 없습니다. |
| 40529 |16 |가장 컨텍스트의 기본 제공 기능 '%.&#x2a;ls'은(는) 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40532 |11 |서버를 열 수 없습니다 "%. & #x2a; ls" hello 로그인에서 요청한 합니다. hello 로그인 하지 못했습니다. |
| 40553 |16 |메모리 사용량이 너무 많아 hello 세션이 종료 되었습니다. 수정 하세요 쿼리 tooprocess 행 수가 더 줄어듭니다.<br/><br/>*참고:* hello 수를 줄입니다 `ORDER BY` 및 `GROUP BY` Transact SQL 코드에서 작업 쿼리 메모리 요구 사항을 hello를 줄이는 데 도움이 됩니다. |
| 40604 |16 |Hello 서버 hello 할당량 초과 하므로 CREATE/ALTER DATABASE 하지 수 없습니다. |
| 40606 |16 |데이터베이스 연결은 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40607 |16 |Windows 로그인은 해당 버전의 SQL Server에서 지원되지 않습니다. |
| 40611 |16 |서버에는 최대 128개의 정의된 방화벽 규칙이 있을 수 있습니다. |
| 40614 |16 |방화벽 규칙의 시작 IP 주소는 끝 IP 주소를 초과할 수 없습니다. |
| 40615 |16 |서버 ' {'이 (가) hello 로그인에서 요청한 파일을 열 수 없습니다. IP 주소를 사용 하 여 클라이언트 tooaccess hello 서버에는 '{1 \}' 허용 되지 않습니다.  tooenable 액세스 hello SQL 데이터베이스 포털을 사용 하거나 hello master 데이터베이스 toocreate이 IP 주소 또는 주소 범위에 대 한 방화벽 규칙에 sp_set_firewall_rule을 실행 합니다.  이 변경 tootake 효과 대 일 분이 걸릴 수도 있습니다. |
| 40617 |16 |로 시작 하는 hello 방화벽 규칙 이름은 <rule name> 너무 깁니다. 최대 길이는 128자입니다. |
| 40618 |16 |hello 방화벽 규칙 이름은 비워 둘 수 없습니다. |
| 40620 |16 |사용자에 대 한 hello 로그인 하지 못했습니다. "%. & #x2a; ls". hello 암호 변경 하지 못했습니다. 해당 버전의 SQL Server에서 로그인 시 암호 변경이 지원되지 않습니다. |
| 40627 |20 |서버 '{0}' 및 데이터베이스 '{1}'에 작업이 진행 중입니다. 다시 시도하기 전에 잠시 기다려 주십시오. |
| 40630 |16 |암호 유효성 검사에 실패했습니다. hello 암호 너무 짧아서 정책 요구를 충족 하지 않습니다. |
| 40631 |16 |지정한 hello 암호가 너무 깁니다. hello 암호는 128 자 있어야 합니다. |
| 40632 |16 |암호 유효성 검사에 실패했습니다. hello 암호 정책 요구 사항을 충분히 복잡 하지 않기 때문에 맞지 않습니다. |
| 40636 |16 |이 작업에서 예약된 데이터베이스 이름 '%.&#x2a;ls'을(를) 사용할 수 없습니다. |
| 40638 |16 |잘못된 구독 ID <subscription-id>. 구독이 존재하지 않습니다. |
| 40639 |16 |요청 tooschema에 맞지 않습니다: <schema error>합니다. |
| 40640 |20 |hello 서버에 예기치 않은 예외가 발생 했습니다. |
| 40641 |16 |hello 지정한 위치가 잘못 되었습니다. |
| 40642 |17 |hello 서버가 현재 사용 중입니다. 나중에 다시 시도하세요. |
| 40643 |16 |hello 지정 x-ms-버전 헤더 값이 올바르지 않습니다. |
| 40644 |14 |실패 한 tooauthorize 액세스 toohello 구독을 지정 합니다. |
| 40645 |16 |서버 이름 <servername>은 비어 있거나 null일 수 없습니다. 것만 구성 될 수 있습니다 소문자 'a'-'z', hello 숫자 0-9 및 하이픈 hello 합니다. hello 하이픈 하지 hello 이름에 처음 이나 올 수 있습니다. |
| 40646 |16 |구독 ID는 비워둘 수 없습니다. |
| 40647 |16 |구독 < 구독-id에 서버 servername이 없습니다. |
| 40648 |17 |너무 많은 요청이 수행되었습니다. 나중에 다시 시도하십시오. |
| 40649 |16 |잘못된 콘텐츠 형식이 지정되었습니다. application/xml만 지원됩니다. |
| 40650 |16 |구독 < 구독-i d >가 없거나 hello 작업에 대 한 준비 되지 않았습니다. |
| 40651 |16 |Toocreate 서버를 hello 구독 < 구독-i d >를 사용 하지 않도록 설정 하지 못했습니다. |
| 40652 |16 |서버를 이동하거나 만들 수 없습니다. 구독 <subscription-id>이(가) 서버 할당량을 초과합니다. |
| 40671 |17 |Hello 게이트웨이와 hello 관리 서비스 간의 통신 오류가 발생 했습니다. 나중에 다시 시도하십시오. |
| 40852 |16 |데이터베이스를 열 수 없습니다 ' %. *ls' 서버의 ' %.* hello 로그인에서 요청한 l s입니다. Access toohello 데이터베이스 보안 사용 연결 문자열을 사용 하 여 에서만 허용 됩니다. tooaccess이 데이터베이스를 연결 문자열 toocontain 수정 hello 서버 FQDN-'서버 이름'.database.windows ' 보안'.net 이름 이어야 합니다. 수정 된 too'server'.database 합니다. `secure`. windows.net 합니다. |
| 45168 |16 |hello SQL Azure 시스템 부하를 상태 이며 단일 서버에 대 한 동시 DB CRUD 작업에 대 한 상한을 두고 됩니다 (예: 데이터베이스 만들기). hello 오류 메시지에 지정 된 hello 서버 hello 최대 동시 연결 수를 초과 했습니다. 나중에 다시 시도하십시오. |
| 45169 |16 |hello SQL azure 시스템이 부하가 이며 hello 다양 한 단일 구독의 동시 서버 CRUD 작업에 한 상한을 두고 (예: 서버 만들기). hello 구독에에서 지정 된 hello 오류 메시지가 hello 최대 동시 연결 수를 초과 했습니다 hello 요청이 거부 되었습니다. 나중에 다시 시도하십시오. |

## <a name="related-links"></a>관련 링크
* [Azure SQL Database 기능](sql-database-features.md)
* [Azure SQL 데이터베이스 리소스 제한](sql-database-resource-limits.md)

