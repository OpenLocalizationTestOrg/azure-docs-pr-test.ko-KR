---
title: "aaaHow tooDump PostgreSQL에 대 한 Azure 데이터베이스에서 복원 하 고 | Microsoft Docs"
description: "덤프 파일에 tooextract는 PostgreSQL 데이터베이스 하는 방법 및 PostgreSQL에 대 한 pg_dump Azure 데이터베이스에 의해 생성 된 보관 파일에서 복원 hello PostgreSQL 데이터베이스에 설명 합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 9ad28e9dec3927b0f80b5e6bab6423cc944f5156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>덤프 및 복원을 사용하여 PostgreSQL 데이터베이스 마이그레이션
사용할 수 있습니다 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract 덤프 파일에 PostgreSQL 데이터베이스 및 [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) pg_dump에 의해 생성 된 보관 파일에서 toorestore hello PostgreSQL 데이터베이스.

## <a name="prerequisites"></a>필수 조건
이 방법 tooguide 통해 toostep를 해야합니다.
- [PostgreSQL 서버에 대 한 Azure 데이터베이스](quickstart-create-server-database-portal.md) 방화벽 규칙 tooallow 액세스와 그 아래에서 데이터베이스.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 및 [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) 명령줄 유틸리티 설치

이러한 단계 toodump를 수행 하 고 PostgreSQL 데이터베이스를 복원 합니다.

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a>Hello 데이터 toobe 로드를 포함 하는 pg_dump를 사용 하 여 덤프 파일 만들기
기존 PostgreSQL tooback 온-프레미스 데이터베이스 또는 VM을 hello 다음 명령을 실행:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a>PostrgeSQL pg_restore를 사용 하 여에 대 한 hello 데이터 hello 대상 Azure 데이터베이스에 복원
Hello 대상 데이터베이스를 만든 후에 hello pg_restore 명령 및 hello-d,-dbname 매개 변수 toorestore hello hello 덤프 파일에서 hello 대상 데이터베이스에 데이터를 사용할 수 있습니다.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
이 예제에서는 hello 데이터 hello 덤프 파일에서 복원 **testdb.dump** hello 데이터베이스로 **mypgsqldb** 대상 서버의 **mypgserver-20170401.postgres.database.azure.com**.
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>다음 단계
- toomigrate 내보내기 및 가져오기를 사용 하 여 PostgreSQL 데이터베이스 참조 [가져오기 및 내보내기를 사용 하 여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-export-and-import.md)
