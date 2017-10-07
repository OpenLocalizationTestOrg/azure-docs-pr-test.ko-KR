---
title: "aaaImport 및 Azure 데이터베이스에서 MySQL에 대 한 내보내기 | Microsoft Docs"
description: "이 문서에서는 MySQL 워크 벤치와 같은 도구를 사용 하 여 MySQL에 대 한 Azure 데이터베이스에서 일반적인 방법으로 tooimport 및 내보내기 데이터베이스를 설명 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>가져오기 및 내보내기를 사용하여 MySQL 데이터베이스 마이그레이션
이 문서 MySQL 워크 벤치를 사용 하 여 두 가지 일반적인 접근 방식 tooimporting 및 MySQL 서버에 대 한 내보내기 데이터 tooan Azure 데이터베이스를 설명 합니다. 

## <a name="before-you-begin"></a>시작하기 전에
이 방법 tooguide 통해 toostep를 해야합니다.
- [Azure Portal을 사용하여 Azure Database for MySQL 서버 만들기](quickstart-create-mysql-server-database-using-azure-portal.md)를 따르는 Azure Database for MySQL 서버
- MySQL 워크 벤치 [다운로드](https://dev.mysql.com/downloads/workbench/), 또는 다른 MySQL 도구 tooimport 및 내보내기.

## <a name="use-common-tools"></a>일반 도구 사용
MySQL 워크 벤치, 토 드, 또는 Navicat tooremotely 연결 및 데이터 가져오기 또는 내보내기 Azure 데이터베이스로 MySQL 용와 같은 일반 도구를 사용 합니다. 

MySQL에 대 한 인터넷 연결 tooconnect tooAzure 데이터베이스와 클라이언트 컴퓨터에 이러한 도구를 사용 합니다. [Azure Database for MySQL에서 SSL 연결 구성](concepts-ssl-connection-security.md)에 설명된 대로 최상의 보안을 위해 SSL 암호화 연결을 사용합니다.

Toomove 가져오기가 필요 하지 않으며 MySQL 용 tooAzure 데이터베이스를 마이그레이션할 때 내보내기 파일 tooany 특수 클라우드 위치 수도 있습니다. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>MySQL 서버에 대 한 hello Azure 데이터베이스에서 데이터베이스 만들기
MySQL 서버 toomigrate hello 데이터에 대 한 hello Azure 데이터베이스에서 빈 데이터베이스를 만듭니다. MySQL 워크 벤치, 토 드, 또는 Navicat toocreate hello 데이터베이스와 같은 도구를 사용 합니다. hello 데이터베이스 hello 대로 다른 이름으로 데이터베이스를 만들 수 있습니다 또는 hello 덤프 데이터를 포함 하는 hello 데이터베이스 이름과 같은 이름을 가질 수 있습니다.

연결 tooget hello hello 연결 정보를 찾으려면 **속성** MySQL에 대 한 Azure 데이터베이스의 창.

![Hello Azure 포털에서에서 hello 연결 정보 찾기](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Hello 연결 정보 tooMySQL 워크 벤치를 추가 합니다.

![MySQL Workbench 연결 문자열](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Toouse 가져오고 내보낼 덤프 및 복원 하는 대신 기술을 시기 결정
MySQL 도구 tooimport를 사용 하 고 hello 다음 시나리오에서에서 Azure의 MySQL 데이터베이스에 데이터베이스를 내보냅니다. 다른 시나리오에서 이점을 얻을 수 hello를 사용 하 여 [덤프 및 복원](concepts-migrate-dump-restore.md) 대신에 접근 합니다. 

- Tooselectively 필요할 때 Azure의 MySQL 데이터베이스에 기존 MySQL 데이터베이스에서 몇 가지 테이블 tooimport 선택, 최상의 toouse hello 가져오기 및 내보내기 방법입니다.  이렇게 함으로써 마이그레이션 toosave 시간 hello 및 리소스에서 불필요 한 테이블을 생략할 수 있습니다. 예를 들어 hello를 사용 하 여 `--include-tables` 또는 `--exclude-tables` 바꾸십시오 [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) 및 hello `--tables` 바꾸십시오 [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables)합니다.
- 테이블 이외의 hello 데이터베이스 개체를 이동할 때 명시적으로 해당 설정을 만듭니다. Toomigrate 지정 하는 다른 데이터베이스 개체 및 제약 조건 (기본 키, 외래 키, 인덱스), 뷰, 함수, 프로시저, 트리거, 포함 됩니다.
- MySQL 데이터베이스 이외의 외부 데이터 원본에서 데이터를 마이그레이션하는 경우 플랫 파일을 만들고 [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html)를 사용하여 가져옵니다.

MySQL에 대 한 Azure 데이터베이스에 데이터를 로드 하는 때 hello 데이터베이스의 모든 테이블 hello InnoDB 저장소 엔진을 사용 하 고 있는지 확인 합니다. MySQL에 대 한 azure 데이터베이스는 대체 저장소 엔진을 지원 하지 않습니다 hello InnoDB 저장소 엔진에만 지원 합니다. 대체 저장소 엔진을 요구 하는 사용자의 테이블 수 있는지 tooconvert로 hello 마이그레이션 tooAzure MySQL에 대 한 데이터베이스 전에 toouse hello InnoDB 엔진 형식입니다. 

예를 들어 hello MyISAM 엔진을 사용 하는 WordPress 또는 웹 앱에 있는 경우 먼저 변환 hello 테이블 hello 데이터 마이그레이션 여 InnoDB 테이블로 합니다. MySQL 용 tooAzure 데이터베이스를 복원 합니다. 사용 하 여 hello 절 `ENGINE=INNODB` tooset 테이블을 만드는 엔진 hello 전송한 다음 hello 마이그레이션 시작 하기 전에 hello 호환 되는 테이블에 hello 데이터를 전송 합니다. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>가져오기 및 내보내기를 위한 성능 권장 사항
-   데이터를 로드하기 전에 클러스터형 인덱스 및 기본 키를 만듭니다. 기본 키 순서로 데이터를 로드합니다. 
-   데이터가 로드될 때까지 보조 인덱스의 생성을 지연합니다. 로드한 후 모든 보조 인덱스를 만듭니다. 
-   로드하기 전에 외래 키 제약 조건을 비활성화합니다. 외래 키 검사 비활성화는 상당한 성능 향상을 제공합니다. Hello 제약 조건을 사용 하 고 hello 부하 tooensure 참조 무결성 후 hello 데이터를 확인 합니다.
-   병렬로 데이터를 로드합니다. 리소스 한계 toohit를 일으킬 및 hello Azure 포털에서에서 사용할 수 있는 hello 메트릭을 사용 하 여 리소스를 모니터링 하는 너무 많은 병렬 처리를 하지 마십시오. 
-   적절한 경우 분할된 테이블을 사용합니다.

## <a name="import-and-export-by-using-mysql-workbench"></a>MySQL Workbench를 사용하여 내보내기 및 가져오기
두 가지가 tooexport 및 가져오기 데이터 MySQL 워크 벤치의 합니다. 각각 다른 용도로 사용됩니다. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>테이블 데이터에서에서 내보내기 및 가져오기 마법사 hello 개체 브라우저의 상황에 맞는 메뉴
![Hello 개체 브라우저의 상황에 맞는 메뉴에서 MySQL 워크 벤치 마법사](./media/concepts-migrate-import-export/p1.png)

테이블 데이터에 대 한 hello 마법사 가져오기를 지원 및 CSV 및 JSON 파일을 사용 하 여 내보내기 작업 합니다. 구분 기호, 열 선택 및 인코딩 선택과 같은 여러 가지 구성 옵션을 포함합니다. 로컬 또는 원격으로 연결된 MySQL 서버에 대해 각 마법사를 수행할 수 있습니다. 테이블, 열 및 형식 매핑을 hello 가져오기 작업에 포함 되어 있습니다. 

테이블을 마우스 오른쪽 단추로 클릭 하 여 이러한 마법사 hello 개체 브라우저의 상황에 맞는 메뉴에서 액세스할 수 있습니다. 그런 다음 **테이블 데이터 내보내기 마법사** 또는 **테이블 데이터 가져오기 마법사**를 선택합니다. 

#### <a name="table-data-export-wizard"></a>테이블 데이터 내보내기 마법사
hello 다음 예제에서는 내보냅니다 hello 테이블 tooa CSV 파일. 
1. 내보낸 hello 데이터베이스 toobe의 hello 테이블을 마우스 오른쪽 단추로 클릭 합니다. 
2. **테이블 데이터 내보내기 마법사**를 선택합니다. Hello 열 toobe 내보낼 행 오프셋 (있는 경우)을 선택 하 고 (있는 경우)를 계산 합니다. 
3. Hello에 **내보내기 위한 데이터 선택** 페이지 **다음**합니다. Hello 파일 경로, CSV 또는 JSON 선택 파일 유형입니다. 또한 hello 줄 구분 기호, 문자열 및 필드 구분 기호를 바깥쪽의 메서드를 선택 합니다. 
4. Hello에 **선택 출력 파일 위치** 페이지 **다음**합니다. 
5. Hello에 **데이터 내보내기** 페이지 **다음**합니다.

#### <a name="table-data-import-wizard"></a>테이블 데이터 가져오기 마법사
hello 다음 예제에서는 가져옵니다 hello 테이블을 CSV 파일에서:
1. 가져온 hello 데이터베이스 toobe의 hello 테이블을 마우스 오른쪽 단추로 클릭 합니다. 
2. 찾아보기 tooand 선택 가져올 CSV 파일 toobe hello를 누른 **다음**합니다. 
3. Hello 대상 테이블 (새로운 또는 기존) 및 선택 또는 취소 hello 선택 **가져오기 전에 테이블 잘라내기** 확인란 합니다. **다음**을 누릅니다.
4. 가져온, 인코딩 및 hello 열 toobe를 선택한 다음 클릭 **다음**합니다. 
5. Hello에 **데이터를 가져올** 페이지 **다음**합니다. hello 마법사는 그에 따라 hello 데이터를 가져옵니다.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>SQL 데이터에서에서 내보내기 및 가져오기 마법사 hello 탐색기 창
마법사 tooexport 사용 하거나 SQL MySQL 워크 벤치에서 생성 된 또는 hello mysqldump 명령에서 생성 된 가져옵니다. Hello에서 이러한 마법사에 액세스 **탐색기** 창 또는 선택 하 여 **서버** hello 주 메뉴에서 합니다. 그런 다음 **데이터 내보내기** 또는 **데이터 가져오기**를 선택합니다. 

#### <a name="data-export"></a>데이터 내보내기
![Hello 탐색기 창을 사용 하 여 MySQL 워크 벤치 데이터 내보내기](./media/concepts-migrate-import-export/p2.png)

Hello를 사용할 수 있습니다 **데이터 내보내기** tooexport MySQL 데이터를 탭 합니다. 
1. 각 스키마 tooexport 원하는, 필요에 따라 각 스키마에서 특정 스키마 개체/테이블을 선택 하는 hello 내보내기 생성을 선택 합니다. 구성 옵션 내보내기 tooa 프로젝트 폴더 또는 자체 포함 된 SQL 파일을 포함, 저장된 루틴 및 이벤트를 덤프 또는 테이블 데이터를 건너뜁니다. 
 
   또는 사용 하 여 **결과 집합 내보내기** tooexport 특정 결과 집합을 CSV, JSON, HTML, XML 등 hello SQL 편집기 tooanother 형식입니다. 
3. Hello 데이터베이스 개체 tooexport를 선택 하 고 구성 hello 관련 옵션입니다.
4. 클릭 **새로 고침** tooload hello에 대 한 현재 개체입니다.
5. 필요에 따라 hello를 열고 **고급 옵션** toorefine hello 내보내기 작업을 탭 합니다. 예를 들어 테이블 잠금을 추가하고, insert 문 대신 replace를 사용하고, 억음 부호로 식별자를 묶는 작업을 수행할 수 있습니다.
6. 클릭 **내보내기 시작** toobegin hello 내보내기 프로세스입니다.


#### <a name="data-import"></a>데이터 가져오기
![관리 탐색 창을 사용하여 MySQL Workbench 데이터 가져오기](./media/concepts-migrate-import-export/p3.png)

Hello를 사용할 수 있습니다 **데이터 가져오기** tooimport 탭 또는 hello mysqldump 명령 또는 hello 데이터 내보내기 작업에서 내보낸된 데이터를 복원 합니다. 
1. Hello 프로젝트 폴더 또는 자체 포함 된 SQL 파일을 선택, hello 스키마 tooimport를 선택 하거나 선택 **새로** toodefine 새 스키마입니다. 
2. 클릭 **가져오기 시작** toobegin hello 가져오기 프로세스입니다.

## <a name="next-steps"></a>다음 단계
다른 마이그레이션 방법으로 [Azure Database for MySQL에서 덤프 및 복원을 사용하여 MySQL 데이터베이스 마이그레이션](concepts-migrate-dump-restore.md)을 참조하세요. 
