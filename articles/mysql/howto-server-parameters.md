---
title: "MySQL에 대 한 Azure 데이터베이스에서 서버 매개 변수 aaaHow tooConfigure | Microsoft Docs"
description: "이 문서에서는 tooconfigure 사용 가능한 서버 매개 변수 Azure 데이터베이스에서 사용 하 여 MySQL에 대 한 Azure 포털을 hello 하는 방법을 설명 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>어떻게 tooconfigure 서버 매개 변수 Azure 데이터베이스에서 사용 하 여 MySQL에 대 한 hello Azure 포털

MySQL용 Azure Database는 일부 서버 매개 변수 구성을 지원합니다. 이 문서에서 설명 하는 방법을 tooconfigure hello Azure 포털 및 목록 hello를 사용 하 여 이러한 매개 변수 지원 매개 변수, 기본값 hello 및 hello 유효한 값 범위입니다. 일부 서버 매개 변수를 조정할 수 있습니다. Hello 여기에 나열 된 것만 지원 됩니다.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Azure 포털에서 tooServer 매개 변수 블레이드를 탐색 합니다.

로그 toohello Azure 포털에에서 MySQL 서버 이름에 대 한 Azure 데이터베이스를 클릭 합니다. Hello에서 **설정** 섹션에서 클릭 **서버 매개 변수** tooopen hello MySQL에 대 한 Azure 데이터베이스에 대 한 hello 서버 매개 변수 블레이드입니다.

![Azure Portal 서버 매개 변수 블레이드](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>구성 가능한 서버 매개 변수 목록

다음 표에서 hello 현재 지원 되는 hello 서버 매개 변수를 나열 합니다. hello 매개 변수는 tooyour 응용 프로그램 요구 사항에 따라 구성할 수 있습니다.

> [!div class="mx-tableFixed"]
|매개 변수 이름|기본값|범위|설명|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|컨트롤 수 마이크로초 hello hello 이진 로그 파일 toodisk 동기화 하기 전에 이진 로그 커밋 대기 합니다.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|hello에 대 한 hello binlog-그룹-커밋-동기화-지연에 지정 된 대로 현재 지연 시간을 중단 하기 전에 트랜잭션 toowait의 최대 수입니다.|
|character_set_server|LATIN1|BIG5, UTF8MB4 등.|Charset_name hello 기본 서버 문자 집합으로 사용 합니다.|
|div_precision_increment|4|0-30|나누기 연산의 hello 결과의 소수 자릿수가 tooincrease hello 여 자릿수입니다.|
|group_concat_max_len|1024|4-16777216|허용 된 최대 결과 GROUP_CONCAT() hello에 대 한 바이트 길이입니다.|
|innodb_adaptive_hash_index|켜기|켜기, 끄기|innodb 적응 해시 인덱스의 사용 가능 여부를 나타냅니다.|
|innodb_lock_wait_timeout|50|1-3600|hello 기간 (초)에서 InnoDB 트랜잭션 기다렸다가 행 잠금을 포기 합니다.|
|interactive_timeout|1800|10-1800|닫기 전에 대화형 연결에서 활동에 대 한 대기 시간 (초) hello 서버 수입니다.|
|log_bin_trust_function_creators|끄기|켜기, 끄기|이 변수는 이진 로깅이 사용되면 적용됩니다. 작성자 수 있습니다. 저장 된 함수는 안전 하지 않은 이벤트 toobe toohello 이진 로그 기록 저장 toocreate 함수 하지 신뢰할 수 있는 여부를 제어 합니다.|
|log_queries_not_using_indexes|끄기|켜기, 끄기|로그 쿼리는 모든 행 tooslow 쿼리 로그 tooretrieve가 필요 합니다.|
|log_slow_admin_statements|끄기|켜기, 끄기|느린 관리 문이 toohello 느린 쿼리 로그에서 작성 된 hello 문은에 포함 되어 있습니다.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|제한 hello 이러한 쿼리 toohello 느린 쿼리 로그를 쓸 수 있는 분당 횟수입니다.|
|long_query_time|10|1-1E+100|쿼리 시간이이 많은 시간 (초)을 넘으면 hello 서버 hello Slow_queries 상태 변수를 증가 합니다.|
|max_allowed_packet|536870912|1024-1073741824|hello 개 패킷 또는 모든 생성/중간 문자열 또는 hello mysql_stmt_send_long_data() C API 함수에서 보낸 모든 매개 변수의 최대 크기입니다.|
|min_examined_row_limit|0|0-18446744073709551615|사용 하는 쿼리가 구성 된 hello hello 느린 쿼리 로그에 행 개수를 기록 합니다. |
|server_id|3293747068|1000-4294967295|hello 서버 ID, toogive 복제에에서 사용 되는 마스터 각 및 고유 id를 슬레이브 합니다.|
|slave_net_timeout|60|30-3600|읽기, hello를 중단 하 고 tooreconnect 시도 하는 시간 (초) toowait hello 슬레이브 hello 연결 중단 됨, 것으로 간주할 hello 마스터에서 더 많은 데이터에 대 한 hello 수입니다.|
|slow_query_log|끄기|켜기, 끄기|Hello 느린 쿼리 로그를 사용 하지 않도록 설정 하거나 사용 합니다.|
|sql_mode|0개 선택됨|ALLOW_INVALID_DATES, IGNORE_SPACE, 등.|hello 현재 서버 SQL 모드입니다.|
|time_zone|SYSTEM|예: -8:00, +05:30|hello 서버 표준 시간대입니다.|
|wait_timeout|120|60-240|닫기 전에 비 대화형 연결에서 활동에 대 한 대기 하는 hello 수 초 hello 서버입니다.|

## <a name="next-steps"></a>다음 단계
- [MySQL용 Azure 데이터베이스에 대한 연결 라이브러리](concepts-connection-libraries.md)
