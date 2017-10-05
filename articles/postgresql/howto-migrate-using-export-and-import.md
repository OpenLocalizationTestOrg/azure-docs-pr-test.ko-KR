---
title: "PostgreSQL용 Azure Database에서 가져오기 및 내보내기를 사용한 데이터베이스 마이그레이션 | Microsoft Docs"
description: "PostgreSQL 데이터베이스를 스크립트 파일로 추출하고 데이터를 해당 파일에서 대상 데이터베이스로 가져오는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.openlocfilehash: 5e306d516d04789e4526bfd09bf99139b83573ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a><span data-ttu-id="fbe5c-103">내보내기 및 가져오기를 사용하여 PostgreSQL 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="fbe5c-103">Migrate your PostgreSQL database using export and import</span></span>
<span data-ttu-id="fbe5c-104">[pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html)를 사용하여 PostgreSQL 데이터베이스를 스크립트 파일로 추출하고, [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)을 사용하여 데이터를 해당 파일에서 대상 데이터베이스로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) to extract a PostgreSQL database into a script file and [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to import the data into the target database from that file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbe5c-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fbe5c-105">Prerequisites</span></span>
<span data-ttu-id="fbe5c-106">이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="fbe5c-107">액세스를 허용하기 위한 방화벽 규칙을 사용하는 [PostgreSQL용 Azure Database 서버](quickstart-create-server-database-portal.md) 및 이에 속한 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="fbe5c-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules to allow access and database under it.</span></span>
- <span data-ttu-id="fbe5c-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="fbe5c-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) command-line utility installed</span></span>
- <span data-ttu-id="fbe5c-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="fbe5c-109">[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) command-line utility installed</span></span>

<span data-ttu-id="fbe5c-110">이러한 단계를 수행하여 PostgreSQL 데이터베이스를 내보내고 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-110">Follow these steps to export and import your PostgreSQL database.</span></span>

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a><span data-ttu-id="fbe5c-111">로드할 데이터를 포함하는 pg_dump를 사용하여 스크립트 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="fbe5c-111">Create a script file using pg_dump that contains the data to be loaded</span></span>
<span data-ttu-id="fbe5c-112">온-프레미스 또는 VM의 기존 PostgreSQL 데이터베이스를 sql 스크립트 파일로 내보내려면 기존 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-112">To export your existing PostgreSQL database on-premises or in a VM to a sql script file, run the following command in your existing environment:</span></span>
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
<span data-ttu-id="fbe5c-113">예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="fbe5c-113">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a><span data-ttu-id="fbe5c-114">PostrgeSQL용 대상 Azure Database에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="fbe5c-114">Import the data on target Azure Database for PostrgeSQL</span></span>
<span data-ttu-id="fbe5c-115">psql 명령줄 및 -d, --dbname 매개 변수를 사용하여 sqp 파일에서 데이터를 만들고 로드한 PostrgeSQL용 Azure Database에 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-115">You can use the psql command line and the -d, --dbname parameter to import the data into Azure Database for PostrgeSQL we created and load data from the sql file.</span></span>
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
<span data-ttu-id="fbe5c-116">이 예제에서는 psql 유틸리티 및 이전 단계의 **testdb.sql**이라는 스크립트 파일을 사용하여 데이터를 대상 서버 **mypgserver-20170401.postgres.database.azure.com**의 데이터베이스 **mypgsqldb**로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-116">This example uses psql utility and a script file named **testdb.sql** from previous step to import data into the database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a><span data-ttu-id="fbe5c-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbe5c-117">Next steps</span></span>
- <span data-ttu-id="fbe5c-118">덤프 및 복원을 사용하여 PostgreSQL 데이터베이스를 마이그레이션하려면 [덤프 및 복원을 사용하여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-dump-and-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe5c-118">To migrate a PostgreSQL database using dump and restore, see [Migrate your PostgreSQL database using dump and restore](howto-migrate-using-dump-and-restore.md)</span></span>