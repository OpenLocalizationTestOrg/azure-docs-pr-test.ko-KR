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
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a><span data-ttu-id="83722-103">덤프 및 복원을 사용하여 PostgreSQL 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="83722-103">Migrate your PostgreSQL database using dump and restore</span></span>
<span data-ttu-id="83722-104">사용할 수 있습니다 [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract 덤프 파일에 PostgreSQL 데이터베이스 및 [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) pg_dump에 의해 생성 된 보관 파일에서 toorestore hello PostgreSQL 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="83722-104">You can use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) tooextract a PostgreSQL database into a dump file and [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) toorestore hello PostgreSQL database from an archive file created by pg_dump.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83722-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83722-105">Prerequisites</span></span>
<span data-ttu-id="83722-106">이 방법 tooguide 통해 toostep를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="83722-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="83722-107">[PostgreSQL 서버에 대 한 Azure 데이터베이스](quickstart-create-server-database-portal.md) 방화벽 규칙 tooallow 액세스와 그 아래에서 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="83722-107">An [Azure Database for PostgreSQL server](quickstart-create-server-database-portal.md) with firewall rules tooallow access and database under it.</span></span>
- <span data-ttu-id="83722-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 및 [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) 명령줄 유틸리티 설치</span><span class="sxs-lookup"><span data-stu-id="83722-108">[pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) and [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) command-line utilities installed</span></span>

<span data-ttu-id="83722-109">이러한 단계 toodump를 수행 하 고 PostgreSQL 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="83722-109">Follow these steps toodump and restore your PostgreSQL database:</span></span>

## <a name="create-a-dump-file-using-pgdump-that-contains-hello-data-toobe-loaded"></a><span data-ttu-id="83722-110">Hello 데이터 toobe 로드를 포함 하는 pg_dump를 사용 하 여 덤프 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="83722-110">Create a dump file using pg_dump that contains hello data toobe loaded</span></span>
<span data-ttu-id="83722-111">기존 PostgreSQL tooback 온-프레미스 데이터베이스 또는 VM을 hello 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="83722-111">tooback up an existing PostgreSQL database on-premises or in a VM, run hello following command:</span></span>
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
<span data-ttu-id="83722-112">예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="83722-112">For example, if you have a local server and a database called **testdb** in it</span></span>
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-hello-data-into-hello-target-azure-database-for-postrgesql-using-pgrestore"></a><span data-ttu-id="83722-113">PostrgeSQL pg_restore를 사용 하 여에 대 한 hello 데이터 hello 대상 Azure 데이터베이스에 복원</span><span class="sxs-lookup"><span data-stu-id="83722-113">Restore hello data into hello target Azure Database for PostrgeSQL using pg_restore</span></span>
<span data-ttu-id="83722-114">Hello 대상 데이터베이스를 만든 후에 hello pg_restore 명령 및 hello-d,-dbname 매개 변수 toorestore hello hello 덤프 파일에서 hello 대상 데이터베이스에 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83722-114">Once you have created hello target database, you can use hello pg_restore command and hello -d, --dbname parameter toorestore hello data into hello target database from hello dump file.</span></span>
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
<span data-ttu-id="83722-115">이 예제에서는 hello 데이터 hello 덤프 파일에서 복원 **testdb.dump** hello 데이터베이스로 **mypgsqldb** 대상 서버의 **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="83722-115">In this example, restore hello data from hello dump file **testdb.dump** into hello database **mypgsqldb** on target server **mypgserver-20170401.postgres.database.azure.com**.</span></span>
```bash
pg_restore -v --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a><span data-ttu-id="83722-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83722-116">Next steps</span></span>
- <span data-ttu-id="83722-117">toomigrate 내보내기 및 가져오기를 사용 하 여 PostgreSQL 데이터베이스 참조 [가져오기 및 내보내기를 사용 하 여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-export-and-import.md)</span><span class="sxs-lookup"><span data-stu-id="83722-117">toomigrate a PostgreSQL database using export and import, see [Migrate your PostgreSQL database using export and import](howto-migrate-using-export-and-import.md)</span></span>
