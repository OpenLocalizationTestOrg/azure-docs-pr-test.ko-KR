---
title: "덤프 및 MySQL 용 Azure 데이터베이스에서 복원 사용 하 여 MySQL 데이터베이스 aaaMigrate | Microsoft Docs"
description: "이 문서 mysqldump, MySQL 워크 벤치 및 PHPMyAdmin와 같은 도구를 사용 하 여 MySQL에 대 한 두 가지를 일반적인 방법으로 tooback 및 Azure 데이터베이스에서 데이터베이스를 복원할을 설명 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>덤프 및 복원을 사용 하는 MySQL에 대 한 MySQL 데이터베이스 tooAzure 데이터베이스 마이그레이션
이 문서를 두 가지 일반적인 방법으로 tooback를 설명 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터베이스 복원
- Dump 및에서 복원을 hello 명령줄 (mysqldump 사용) 
- PHPMyAdmin을 사용하여 덤프 및 복원 

## <a name="before-you-begin"></a>시작하기 전에
이 방법 tooguide 통해 toostep, toohave가 필요합니다.
- [MySQL용 Azure 데이터베이스 서버 만들기 - Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md)
- [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) 명령줄 유틸리티가 컴퓨터에 설치되어 있어야 함
- MySQL 워크 벤치 [MySQL 워크 벤치 다운로드](https://dev.mysql.com/downloads/workbench/), 토 드, Navicat, 또는 다른 제 3 자 MySQL 도구 toodo 덤프 및 명령을 복원 합니다.

## <a name="use-common-tools"></a>일반 도구 사용
연결 하 고 MySQL에 대 한 Azure 데이터베이스에 데이터를 복원 하는 MySQL 워크 벤치, mysqldump, 토 드, 또는 Navicat tooremotely와 같은 공통 유틸리티와 도구를 사용 합니다. MySQL에 대 한 인터넷 연결 tooconnect toohello Azure 데이터베이스와 클라이언트 컴퓨터에 이러한 도구를 사용 합니다. 최상의 보안을 위해 SSL 암호화 연결을 사용합니다. [MySQL용 Azure 데이터베이스에서 SSL 연결 구성](concepts-ssl-connection-security.md)을 참조하세요. MySQL 용 tooAzure 데이터베이스를 마이그레이션할 때 toomove hello 덤프 파일 tooany 특수 클라우드 위치를 않아도 됩니다. 

## <a name="common-uses-for-dump-and-restore"></a>덤프 및 복원을 위한 일반적인 사용
몇 가지 일반적인 시나리오에서 MySQL 유틸리티 mysqldump 및 mysqlpump toodump 및 부하 데이터베이스와 같은 Azure MySQL 데이터베이스를 사용할 수 있습니다. 다른 시나리오에서는 hello를 사용할 수 있습니다 [가져오기 및 내보내기](concepts-migrate-import-export.md) 대신에 접근 합니다.

- Hello 전체 데이터베이스를 마이그레이션할 때 사용 하 여 데이터베이스를 덤프 합니다. 이 권장 사항은 많은 양의 MySQL 데이터를 이동할 때 또는 실시간 사이트 또는 응용 프로그램에 대 한 toominimize 서비스 중단 하려는 경우를 보유 합니다. 
-  MySQL에 대 한 Azure 데이터베이스에 데이터를 로드할 때 hello 데이터베이스의 모든 테이블 hello InnoDB 저장소 엔진을 사용 하 고 있는지 확인 합니다. Azure Database for MySQL은 InnoDB 저장소 엔진만을 지원하므로 대체 저장소 엔진을 지원하지 않습니다. 테이블은 다른 저장소 엔진으로 구성 된, 데이터베이스 마이그레이션 tooAzure 전에 hello InnoDB 엔진 형식으로 MySQL에 대 한 변환 합니다.
   예를 들어, WordPress 또는 hello MyISAM 테이블을 사용 하 여 WebApp 있으면 먼저 변환 해당 테이블으로 MySQL 용 tooAzure 데이터베이스를 복원 하기 전에 InnoDB 형식으로 마이그레이션합니다. 사용 하 여 hello 절 `ENGINE=InnoDB` tooset 새 테이블을 만들 때 사용 되는 엔진 hello 다음 hello 복원 하기 전에 hello 호환 되는 테이블에 hello 데이터를 전송 합니다. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- tooavoid 모든 호환성 문제는 동일한 버전의 MySQL 데이터베이스를 덤프할 때 hello 원본 및 대상 시스템에 사용 되는 hello를 확인 합니다. 예를 들어 기존 MySQL 서버 버전 5.7 이면 구성 된 MySQL toorun 5.7 버전에 대 한 데이터베이스 tooAzure 마이그레이션할 해야 있습니다. hello `mysql_upgrade` 명령 MySQL server에 대 한 Azure 데이터베이스에서 작동 하지 않습니다 되며 지원 되지 않습니다. MySQL 버전 간에 tooupgrade 해야 할 경우 먼저 덤프 하거나 사용자 환경에 MySQL의 더 높은 버전으로 더 낮은 버전 데이터베이스를 내보냅니다. 그런 다음 Azure Database for MySQL로 마이그레이션을 시도하기 전에 `mysql_upgrade`를 실행합니다.

## <a name="performance-considerations"></a>성능 고려 사항
큰 데이터베이스를 덤프할 때 이러한 고려 사항에 대 한 take 공지 toooptimize 성능:
-   사용 하 여 hello `exclude-triggers` mysqldump 데이터베이스를 덤프할 때의 옵션입니다. 덤프 파일 tooavoid hello 트리거 명령은 hello 데이터 복원 과정에서 발생 하에서 트리거를 제외 합니다. 
-   Hello 방지 `single-transaction` mysqldump 매우 큰 데이터베이스를 덤프할 때의 옵션입니다. 추가 저장소 사용 하면 단일 트랜잭션 내에서 여러 테이블을 덤프 하 고 메모리 리소스 toobe 복원 하는 동안 사용 하 고 성능 지연을 또는 리소스 제약 조건이 발생할 수 있습니다.
-   사용 하 여 데이터베이스를 덤프할 때 SQL toominimize 문 실행 오버 헤드를 로드할 때 다중 값 삽입 합니다. mysqldump 유틸리티에 의해 생성된 덤프 파일을 사용할 경우 다중 값 삽입은 기본적으로 활성화됩니다. 
-  사용 하 여 hello `order-by-primary` mysqldump 기본 키 순서로 hello 데이터가 스크립팅 되는지 되도록 데이터베이스를 덤프할 때의 옵션입니다.
-   사용 하 여 hello `disable-keys` mysqldump toodisable 외래 키 제약 조건을 로드 전에 데이터를 덤프할 때의 옵션입니다. 외래 키 검사 비활성화는 성능 향상을 제공합니다. Hello 제약 조건을 사용 하 고 hello 부하 tooensure 참조 무결성 후 hello 데이터를 확인 합니다.
-   적절한 경우 분할된 테이블을 사용합니다.
-   병렬로 데이터를 로드합니다. 리소스 한계 toohit를 일으킬 및 hello Azure 포털에서에서 사용할 수 있는 hello 메트릭을 사용 하는 리소스를 모니터링 하는 너무 많은 병렬 처리를 하지 마십시오. 
-   사용 하 여 hello `defer-table-indexes` mysqlpump 테이블 데이터가 로드 된 후 발생 하는 인덱스를 만들 수 있도록 데이터베이스를 덤프할 때의 옵션입니다.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Hello에서 백업 파일을 명령줄 만들 mysqldump를 사용 하 여
hello 로컬 온-프레미스 서버 또는 hello 다음 명령을 실행 하는 가상 컴퓨터에 기존 MySQL 데이터베이스를 tooback: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

hello 매개 변수 tooprovide가 됩니다.
- [uname] 데이터베이스 사용자 이름 
- 데이터베이스에 대 한 [통과] hello 암호 (-p 암호 hello 사이의 공간이 참고) 
- 데이터베이스의 [dbname] hello 이름 
- 데이터베이스 백업에 대 한 hello filename [backupfile.sql] 
- [-opt] hello mysqldump 옵션 

예를 들어 데이터베이스를 tooback 라는 'testdb' MySQL 서버에 없는 암호 tooa 파일 testdb_backup.sql hello 사용자 이름 'testuser'와 다음 명령을 hello를 사용 합니다. hello 명령은 백업 hello `testdb` 라는 파일에는 데이터베이스 `testdb_backup.sql`, toore 필요한 모든 hello SQL 문에 포함 된-hello 데이터베이스를 만듭니다. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect를 데이터베이스 tooback 프로그램의 특정 테이블, 목록 hello 테이블 이름을 공백으로 구분 합니다. 예를 들어 tooback hello 'testdb'에서 유일한 table1 및 table2 테이블을이 예제를 수행 합니다. 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

사용 하 여 hello-는 한 번에 둘 이상의 데이터베이스를 tooback 데이터베이스 전환 하 고 공백으로 구분 된 목록 hello 데이터베이스 이름입니다. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
한 번에 hello 서버에서 모든 hello 데이터베이스를 tooback, hello-모든 데이터베이스 옵션을 사용 해야 합니다.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>MySQL 서버에 대 한 hello 대상 Azure 데이터베이스에서 데이터베이스 만들기
MySQL 서버 toomigrate hello 데이터에 대 한 hello 대상 Azure 데이터베이스에서 빈 데이터베이스를 만듭니다. MySQL 워크 벤치, 토 드, 또는 Navicat toocreate hello 데이터베이스와 같은 도구를 사용 합니다. hello 데이터베이스 이름이 포함 된 hello 덤프 데이터는 hello 데이터베이스 hello 하거나 다른 이름으로 데이터베이스를 만들 수 있습니다.

Azure 데이터베이스에서 MySQL에 대 한 hello 속성 페이지에서 hello 연결 정보를 찾을 tooget 연결.
![Hello Azure 포털에서에서 hello 연결 정보 찾기](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

MySQL Workbench로 hello 연결 정보를 추가 합니다.
![MySQL Workbench 연결 문자열](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>명령줄 또는 MySQL Workbench를 사용하여 MySQL 데이터베이스 복원
Hello 대상 데이터베이스를 만든 후에 hello mysql 명령 또는 hello 덤프 파일에서 데이터베이스를 새로 만든 특정 hello에 MySQL 워크 벤치 toorestore hello 데이터를 사용할 수 있습니다.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
이 예제에서는 MySQL server에 대 한 hello 대상 Azure 데이터베이스에서 데이터베이스를 새로 만든 hello에 hello 데이터를 복원 합니다.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>PHPMyAdmin을 사용하여 내보내기
tooexport, 이미 설치한 로컬 환경에서 hello 공통 도구 phpMyAdmin를 사용할 수 있습니다. tooexport PHPMyAdmin를 사용 하 여 MySQL 데이터베이스:
- phpMyAdmin을 엽니다.
- 데이터베이스를 선택합니다. Hello hello 왼쪽 목록에서 hello 데이터베이스 이름을 클릭 합니다. 
- Hello 클릭 **내보내기** 링크 합니다. 새 페이지에는 데이터베이스의 tooview hello 덤프 나타납니다.
- Hello 내보내기 영역에서에서 클릭 hello **모두 선택** toochoose hello 데이터베이스 테이블을에서 연결 합니다. 
- SQL 옵션 영역 hello hello 적절 한 옵션을 클릭 합니다. 
- Hello 클릭 **파일로 저장** 옵션 및 해당 하는 hello 압축 옵션 선택한 hello 클릭 **이동** 단추입니다. 대화 상자를 확인 하면 toosave hello 파일을 로컬 나타나야 합니다.

## <a name="import-using-phpmyadmin"></a>PHPMyAdmin을 사용하여 가져오기
데이터베이스를 가져오는 비슷한 tooexporting입니다. 다음 작업 hello 마십시오.
- phpMyAdmin을 엽니다. 
- Hello phpMyAdmin 설치 페이지에서 클릭 **추가** tooadd MySQL server에 대 한 Azure 데이터베이스입니다. Hello 연결 정보 및 로그인 정보를 제공 합니다.
- 적절 하 게 명명 된 데이터베이스를 만들고 hello hello 화면 왼쪽에서 선택 합니다. toorewrite hello 기존 데이터베이스를 클릭 hello 데이터베이스 이름, hello 테이블 이름 옆에 있는 모든 hello 확인란을 선택 하 고 **Drop** toodelete hello 기존 테이블입니다. 
- Hello 클릭 **SQL** 링크 tooshow hello 페이지 SQL 명령에 입력 하거나 SQL 파일을 업로드할 수 있습니다. 
- 사용 하 여 hello **찾아보기** 단추 toofind hello 데이터베이스 파일입니다. 
- Hello 클릭 **이동** tooexport hello 백업 단추 hello SQL 명령을 실행 하 고 데이터베이스를 다시 만듭니다.

## <a name="next-steps"></a>다음 단계
[MySQL에 대 한 응용 프로그램 tooAzure 데이터베이스 연결](./howto-connection-string.md)
