---
title: "사용 하 여 데이터베이스 가져오고 PostgreSQL에 대 한 Azure 데이터베이스에서 내보낼 aaaMigrate | Microsoft Docs"
description: "설명 어떻게 PostgreSQL 데이터베이스 스크립트 파일에 추출 하 고 해당 파일의 hello 대상 데이터베이스에 hello 데이터를 가져옵니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5ca4650782b02e1067c5a8a3710f2dfbc8c76063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>내보내기 및 가져오기를 사용하여 PostgreSQL 데이터베이스 마이그레이션
사용할 수 있습니다 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract 스크립트 파일에 PostgreSQL 데이터베이스 및 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello 데이터 hello 대상 데이터베이스에서 해당 파일에 있습니다.

## <a name="prerequisites"></a>필수 조건
이 방법 tooguide 통해 toostep를 해야합니다.
- [PostgreSQL 서버에 대 한 Azure 데이터베이스](quickstart-create-server-database-portal.md) 방화벽 규칙 tooallow 액세스와 그 아래에서 데이터베이스.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 명령줄 유틸리티 설치
- [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 명령줄 유틸리티 설치

이러한 단계 tooexport 따르고 PostgreSQL 데이터베이스를 가져옵니다.

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Hello 데이터 toobe 로드를 포함 하는 pg_dump를 사용 하 여 스크립트 파일 만들기
tooexport 프로그램 기존 PostgreSQL 온-프레미스 데이터베이스 또는 VM tooa sql 스크립트 파일에 hello 다음 기존 환경에서 명령을 실행 합니다.
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a>대상 PostrgeSQL에 대 한 Azure 데이터베이스에서 hello 데이터 가져오기
Hello psql 명령줄 및 hello-d,-dbname 매개 변수 tooimport hello PostrgeSQL 생성 하 고 hello sql 파일에서 데이터 로드에 대 한 Azure 데이터베이스에 데이터를 사용할 수 있습니다.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
이 예제에서는 psql 유틸리티 및 라는 스크립트 파일 **testdb.sql** hello 데이터베이스에 이전 단계 tooimport 데이터 로부터 **mypgsqldb** 대상 서버에서  **mypgserver 20170401.postgres.database.azure.com**합니다.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>다음 단계
- toomigrate 덤프 및 복원을 사용 하 여 PostgreSQL 데이터베이스 참조 [덤프 및 복원을 사용 하 여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-dump-and-restore.md)
