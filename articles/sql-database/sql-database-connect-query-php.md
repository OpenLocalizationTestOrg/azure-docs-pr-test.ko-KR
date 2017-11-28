---
title: "Azure SQL 데이터베이스 aaaUse PHP tooquery | Microsoft Docs"
description: "이 항목에서는 toouse PHP toocreate tooan Azure SQL 데이터베이스와 쿼리를 TRANSACT-SQL 문을 사용 하 여 연결 하는 프로그램입니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="6fe3b-103">PHP tooquery Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6fe3b-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="6fe3b-104">이 빠른 시작 자습서에서는 설명 방법을 toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate 프로그램 tooconnect tooan Azure SQL 데이터베이스 및 Transact SQL 문 tooquery 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe3b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6fe3b-105">Prerequisites</span></span>

<span data-ttu-id="6fe3b-106">toocomplete이 빠른 시작 자습서 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="6fe3b-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-107">An Azure SQL database.</span></span> <span data-ttu-id="6fe3b-108">이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="6fe3b-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="6fe3b-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="6fe3b-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="6fe3b-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="6fe3b-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="6fe3b-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fe3b-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="6fe3b-112">A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="6fe3b-113">운영 체제에 맞게 설치된 PHP 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="6fe3b-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="6fe3b-114">**MacOS**: Homebrew를 설치 하 고 PHP hello ODBC 드라이버와 SQLCMD, 설치 하 고 다음 SQL Server 용 PHP 드라이버 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="6fe3b-115">[1.2, 1.3 및 2.1단계](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="6fe3b-116">**Ubuntu**: PHP를 설치 및 기타 SQL Server에 패키지 및 설치 hello PHP Driver 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="6fe3b-117">[1.2 및 2.1단계](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="6fe3b-118">**Windows**: hello 최신 버전의 IIS Express, Chocolatey, hello ODBC 드라이버 및 SQLCMD SQL Server 용 Microsoft 드라이버의 IIS Express 용 PHP의 hello 최신 버전 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="6fe3b-119">[1.2 및 1.3단계](https://www.microsoft.com/sql-server/developer-get-started/php/windows/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="6fe3b-120">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="6fe3b-120">SQL server connection information</span></span>

<span data-ttu-id="6fe3b-121">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="6fe3b-122">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="6fe3b-123">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6fe3b-124">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="6fe3b-125">Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="6fe3b-126">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="6fe3b-128">서버 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="6fe3b-129">코드 tooquery SQL 데이터베이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="6fe3b-130">원하는 텍스트 편집기에서 **sqltest.php** 파일을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="6fe3b-131">Hello 내용을 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a><span data-ttu-id="6fe3b-132">Hello 코드 실행</span><span class="sxs-lookup"><span data-stu-id="6fe3b-132">Run hello code</span></span>

1. <span data-ttu-id="6fe3b-133">Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="6fe3b-134">확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe3b-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fe3b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6fe3b-135">Next steps</span></span>
- [<span data-ttu-id="6fe3b-136">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="6fe3b-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="6fe3b-137">SQL Server용 Microsoft PHP 드라이버</span><span class="sxs-lookup"><span data-stu-id="6fe3b-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="6fe3b-138">문제 보고 또는 질문(영문)</span><span class="sxs-lookup"><span data-stu-id="6fe3b-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
