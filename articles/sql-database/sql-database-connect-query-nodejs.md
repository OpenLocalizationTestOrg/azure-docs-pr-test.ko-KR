---
title: "Azure SQL 데이터베이스 aaaUse Node.js tooquery | Microsoft Docs"
description: "이 항목에서는 toouse Node.js toocreate tooan Azure SQL 데이터베이스와 쿼리를 TRANSACT-SQL 문을 사용 하 여 연결 하는 프로그램입니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="e25f5-103">Node.js tooquery Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e25f5-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="e25f5-104">이 빠른 시작 자습서에서는 설명 방법을 toouse [Node.js](https://nodejs.org/en/) toocreate 프로그램 tooconnect tooan Azure SQL 데이터베이스 및 Transact SQL 문 tooquery 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e25f5-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e25f5-105">Prerequisites</span></span>

<span data-ttu-id="e25f5-106">toocomplete이 빠른 시작 자습서 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="e25f5-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-107">An Azure SQL database.</span></span> <span data-ttu-id="e25f5-108">이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="e25f5-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="e25f5-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="e25f5-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="e25f5-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="e25f5-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="e25f5-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25f5-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="e25f5-112">A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="e25f5-113">운영 체제에 맞게 설치된 Node.js 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="e25f5-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="e25f5-114">**MacOS**: Homebrew 및 Node.js를 설치 하 고 다음 SQLCMD 및 hello ODBC 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="e25f5-115">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) 참조</span><span class="sxs-lookup"><span data-stu-id="e25f5-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="e25f5-116">**Ubuntu**: Node.js를 설치 하 고 다음 SQLCMD 및 hello ODBC 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="e25f5-117">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) 참조</span><span class="sxs-lookup"><span data-stu-id="e25f5-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="e25f5-118">**Windows**: Chocolatey 및 Node.js를 설치 하 고 다음 hello ODBC 드라이버 및 SQL 명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="e25f5-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="e25f5-119">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/windows/) 참조</span><span class="sxs-lookup"><span data-stu-id="e25f5-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="e25f5-120">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="e25f5-120">SQL server connection information</span></span>

<span data-ttu-id="e25f5-121">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="e25f5-122">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="e25f5-123">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e25f5-124">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e25f5-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="e25f5-125">Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="e25f5-126">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="e25f5-128">Azure SQL 데이터베이스 서버에 대 한 hello 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e25f5-129">방화벽 규칙에는이 자습서를 수행 하는 hello 컴퓨터의 공용 IP 주소를 hello에 대 한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="e25f5-130">다른 공용 IP 주소가 있어야 하거나 다른 컴퓨터에는 경우 만들기는 [Azure 포털 hello 사용 하 여 서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="e25f5-131">Node.js 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e25f5-131">Create a Node.js project</span></span>

<span data-ttu-id="e25f5-132">명령 프롬프트를 열고 *sqltest*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="e25f5-133">만들고 hello 다음 명령을 실행 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="e25f5-134">코드 tooquery SQL 데이터베이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="e25f5-135">개발 환경 또는 원하는 텍스트 편집기에서 **sqltest.js** 파일 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="e25f5-136">Hello 내용을 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt tooconnect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from hello Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-hello-code"></a><span data-ttu-id="e25f5-137">Hello 코드 실행</span><span class="sxs-lookup"><span data-stu-id="e25f5-137">Run hello code</span></span>

1. <span data-ttu-id="e25f5-138">Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="e25f5-139">확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e25f5-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e25f5-140">Next steps</span></span>

- <span data-ttu-id="e25f5-141">Hello에 대 한 자세한 내용은 [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="e25f5-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="e25f5-142">너무 방법에 대해 알아봅니다[연결 및.NET core를 사용 하 여 Azure SQL 데이터베이스 쿼리](sql-database-connect-query-dotnet-core.md) macOS/Windows/Linux에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="e25f5-143">에 대 한 자세한 내용은 [Windows/Linux/macOS hello 명령줄을 사용 하 여에서.NET Core 시작](/dotnet/core/tutorials/using-with-xplat-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="e25f5-144">너무 방법에 대해 알아봅니다[SSMS를 사용 하 여 첫 번째 Azure SQL 데이터베이스 디자인](sql-database-design-first-database.md) 또는 [.NET을 사용 하 여 첫 번째 Azure SQL 데이터베이스 디자인](sql-database-design-first-database-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="e25f5-145">너무 방법에 대해 알아봅니다[연결 및 SSMS 사용 하 여 쿼리](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="e25f5-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="e25f5-146">너무 방법에 대해 알아봅니다[연결 및 Visual Studio 코드 쿼리](sql-database-connect-query-vscode.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e25f5-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


