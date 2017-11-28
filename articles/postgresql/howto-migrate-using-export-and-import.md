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
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="7d247-103">내보내기 및 가져오기를 사용하여 PostgreSQL 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7d247-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="7d247-104">사용할 수 있습니다 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract 스크립트 파일에 PostgreSQL 데이터베이스 및 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello 데이터 hello 대상 데이터베이스에서 해당 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooimport hello data into hello target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d247-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7d247-105">Prerequisites</span></span>
<span data-ttu-id="7d247-106">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="7d247-107">[PostgreSQL 서버에 대 한 Azure 데이터베이스](quickstart-create-server-database-portal.md) 방화벽 규칙 tooallow 액세스와 그 아래에서 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="7d247-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="7d247-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="7d247-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="7d247-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="7d247-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="7d247-110">이러한 단계 tooexport 따르고 PostgreSQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-110">Follow these steps tooexport and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="7d247-111">Hello 데이터 toobe 로드를 포함 하는 pg_dump를 사용 하 여 스크립트 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="7d247-111">Create a script file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="7d247-112">tooexport 프로그램 기존 PostgreSQL 온-프레미스 데이터베이스 또는 VM tooa sql 스크립트 파일에 hello 다음 기존 환경에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-112">tooexport your existing PostgreSQL database on-premises or in a VM tooa sql script file, run hello following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="7d247-113">예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="7d247-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-hello-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="7d247-114">대상 PostrgeSQL에 대 한 Azure 데이터베이스에서 hello 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="7d247-114">Import hello data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="7d247-115">Hello psql 명령줄 및 hello-d,-dbname 매개 변수 tooimport hello PostrgeSQL 생성 하 고 hello sql 파일에서 데이터 로드에 대 한 Azure 데이터베이스에 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-115">You can use hello psql command line and hello -d, --dbname parameter tooimport hello data into Azure Database for PostrgeSQL we created and load data from hello sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="7d247-116">이 예제에서는 psql 유틸리티 및 라는 스크립트 파일 **testdb.sql** hello 데이터베이스에 이전 단계 tooimport 데이터 로부터 **mypgsqldb** 대상 서버에서  **mypgserver 20170401.postgres.database.azure.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d247-116">This example uses psql utility and a script file named **testdb.sql** from previous step tooimport data into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="7d247-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d247-117">Next steps</span></span>
- <span data-ttu-id="7d247-118">toomigrate 덤프 및 복원을 사용 하 여 PostgreSQL 데이터베이스 참조 [덤프 및 복원을 사용 하 여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-dump-and-restore.md)</span><span class="sxs-lookup"><span data-stu-id="7d247-118">toomigrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>
