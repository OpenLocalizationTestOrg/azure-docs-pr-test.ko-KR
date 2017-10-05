---
title: "Node.js를 사용하여 Azure SQL Database 쿼리 | Microsoft Docs"
description: "이 항목에서는 Node.js를 사용하여 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 쿼리하는 프로그램을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: 1907a95df9132c059d7985b6d5cd913536bf3403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-nodejs-to-query-an-azure-sql-database"></a><span data-ttu-id="148f3-103">Node.js를 사용하여 Azure SQL Database 쿼리</span><span class="sxs-lookup"><span data-stu-id="148f3-103">Use Node.js to query an Azure SQL database</span></span>

<span data-ttu-id="148f3-104">이 빠른 시작 자습서에서는 [Node.js](https://nodejs.org/en/)를 통해 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 데이터를 쿼리하는 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-104">This quick start tutorial demonstrates how to use [Node.js](https://nodejs.org/en/) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="148f3-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="148f3-105">Prerequisites</span></span>

<span data-ttu-id="148f3-106">이 빠른 시작 자습서를 완료하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="148f3-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-107">An Azure SQL database.</span></span> <span data-ttu-id="148f3-108">이 빠른 시작에서는 다음과 같은 빠른 시작 중 하나에서 만든 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="148f3-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="148f3-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="148f3-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="148f3-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="148f3-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="148f3-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="148f3-112">이 빠른 시작 자습서에서 사용하는 컴퓨터의 공용 IP 주소에 대한 [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)</span><span class="sxs-lookup"><span data-stu-id="148f3-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="148f3-113">운영 체제에 맞게 설치된 Node.js 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="148f3-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="148f3-114">**MacOS**: Homebrew와 Node.js를 설치한 다음 ODBC 드라이버와 SQLCMD를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-114">**MacOS**: Install Homebrew and Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="148f3-115">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) 참조</span><span class="sxs-lookup"><span data-stu-id="148f3-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="148f3-116">**Ubuntu**: Node.js를 설치한 다음 ODBC 드라이버와 SQLCMD를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-116">**Ubuntu**: Install Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="148f3-117">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) 참조</span><span class="sxs-lookup"><span data-stu-id="148f3-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="148f3-118">**Windows**: Chocolatey와 Node.js를 설치한 다음 ODBC 드라이버와 SQLCMD를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-118">**Windows**: Install Chocolatey and Node.js, and then install the ODBC driver and SQL CMD.</span></span> <span data-ttu-id="148f3-119">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/node/windows/) 참조</span><span class="sxs-lookup"><span data-stu-id="148f3-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="148f3-120">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="148f3-120">SQL server connection information</span></span>

<span data-ttu-id="148f3-121">Azure SQL Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="148f3-122">다음 절차에는 정규화된 서버 이름, 데이터베이스 이름 및 로그인 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="148f3-123">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="148f3-124">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="148f3-125">데이터베이스의 **개요** 페이지에서 다음 이미지와 같이 정규화된 서버 이름을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="148f3-126">서버 이름 위로 마우스를 가져가면 **복사하려면 클릭** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="148f3-128">Azure SQL Database 서버의 로그인 정보를 잊어버린 경우 SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="148f3-129">이 자습서를 수행하는 컴퓨터의 공용 IP 주소에 대한 방화벽 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-129">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="148f3-130">다른 컴퓨터에 있거나 다른 공용 IP 주소가 있으면 [Azure Portal을 사용하여 서버 수준 방화벽 규칙을 만듭니다](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="148f3-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="148f3-131">Node.js 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="148f3-131">Create a Node.js project</span></span>

<span data-ttu-id="148f3-132">명령 프롬프트를 열고 *sqltest*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="148f3-133">생성한 폴더로 이동하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-133">Navigate to the folder you created and run the following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="148f3-134">SQL 데이터베이스 쿼리 코드 삽입</span><span class="sxs-lookup"><span data-stu-id="148f3-134">Insert code to query SQL database</span></span>

1. <span data-ttu-id="148f3-135">개발 환경 또는 원하는 텍스트 편집기에서 **sqltest.js** 파일 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="148f3-136">내용을 다음 코드로 바꾸고, 서버, 데이터베이스, 사용자 및 암호에 대해 적절한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-136">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection to database
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

   // Attempt to connect and execute queries if connection goes through
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
      { console.log('Reading rows from the Table...');

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

## <a name="run-the-code"></a><span data-ttu-id="148f3-137">코드 실행</span><span class="sxs-lookup"><span data-stu-id="148f3-137">Run the code</span></span>

1. <span data-ttu-id="148f3-138">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-138">At the command prompt, run the following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="148f3-139">상위 20개 행이 반환되는지 확인한 다음 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-139">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="148f3-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="148f3-140">Next steps</span></span>

- <span data-ttu-id="148f3-141">[SQL Server용 Microsoft Node.js Driver](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-141">Learn about the [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="148f3-142">Windows/Linux/macOS에서 [.NET Core를 사용하여 Azure SQL Database를 연결 및 쿼리하는 방법](sql-database-connect-query-dotnet-core.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-142">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="148f3-143">[명령줄을 사용하여 Windows/Linux/macOS에서 .NET Core를 시작하는 방법](/dotnet/core/tutorials/using-with-xplat-cli)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="148f3-144">[SSMS를 사용하여 첫 번째 Azure SQL Database를 설계하는 방법](sql-database-design-first-database.md) 또는 [.NET을 사용하여 첫 번째 Azure SQL Database를 설계하는 방법](sql-database-design-first-database-csharp.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-144">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="148f3-145">[SSMS를 사용하여 연결 및 쿼리하는 방법](sql-database-connect-query-ssms.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-145">Learn how to [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="148f3-146">[Visual Studio Code를 사용하여 연결 및 쿼리하는 방법](sql-database-connect-query-vscode.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="148f3-146">Learn how to [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


