---
title: "Ruby를 사용하여 Azure SQL Database 쿼리 | Microsoft Docs"
description: "이 항목에서는 Ruby를 사용하여 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 쿼리하는 프로그램을 만드는 방법을 보여 줍니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 25ff9a9cfaa5494dbb006c84e235099fe51e6545
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ruby-to-query-an-azure-sql-database"></a><span data-ttu-id="b1352-103">Ruby를 사용하여 Azure SQL Database 쿼리</span><span class="sxs-lookup"><span data-stu-id="b1352-103">Use Ruby to query an Azure SQL database</span></span>

<span data-ttu-id="b1352-104">이 빠른 시작 자습서에서는 [Ruby](https://www.ruby-lang.org)를 통해 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 데이터를 쿼리하는 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-104">This quick start tutorial demonstrates how to use [Ruby](https://www.ruby-lang.org) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1352-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b1352-105">Prerequisites</span></span>

<span data-ttu-id="b1352-106">이 빠른 시작 자습서를 완료하려면 다음 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="b1352-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-107">An Azure SQL database.</span></span> <span data-ttu-id="b1352-108">이 빠른 시작에서는 다음과 같은 빠른 시작 중 하나에서 만든 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="b1352-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="b1352-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="b1352-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="b1352-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="b1352-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1352-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="b1352-112">이 빠른 시작 자습서에서 사용하는 컴퓨터의 공용 IP 주소에 대한 [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)</span><span class="sxs-lookup"><span data-stu-id="b1352-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="b1352-113">운영 체제에 맞게 설치된 Ruby 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="b1352-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="b1352-114">**MacOS**: Homebrew를 설치하고, rbenv와 ruby-build를 설치하고, Ruby를 설치한 다음, FreeTDS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="b1352-115">[1.2, 1.3, 1.4 및 1.5 단계](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) 참조</span><span class="sxs-lookup"><span data-stu-id="b1352-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="b1352-116">**Ubuntu**: Ruby용 필수 구성 요소를 설치하고, rbenv와 ruby-build를 설치하고, Ruby를 설치한 다음, FreeTDS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="b1352-117">[1.2, 1.3, 1.4 및 1.5 단계](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/) 참조</span><span class="sxs-lookup"><span data-stu-id="b1352-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="b1352-118">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="b1352-118">SQL server connection information</span></span>

<span data-ttu-id="b1352-119">Azure SQL Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-119">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="b1352-120">다음 절차에는 정규화된 서버 이름, 데이터베이스 이름 및 로그인 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-120">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="b1352-121">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-121">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b1352-122">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-122">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="b1352-123">데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-123">On the **Overview** page for your database, review the fully qualified server name.</span></span> <span data-ttu-id="b1352-124">해당 서버 이름을 마우스로 가리키면 다음 이미지와 같이 **복사하려면 클릭** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-124">You can hover over the server name to bring up the **Click to copy** option, as shown in the following image:</span></span>

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="b1352-126">Azure SQL Database 서버의 로그인 정보를 잊어버린 경우 SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-126">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1352-127">이 자습서를 수행하는 컴퓨터의 공용 IP 주소에 대한 방화벽 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="b1352-128">다른 컴퓨터에 있거나 다른 공용 IP 주소가 있으면 [Azure Portal을 사용하여 서버 수준 방화벽 규칙을 만듭니다](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="b1352-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="b1352-129">SQL 데이터베이스 쿼리 코드 삽입</span><span class="sxs-lookup"><span data-stu-id="b1352-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="b1352-130">원하는 텍스트 편집기에서 **sqltest.rb** 파일을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="b1352-131">내용을 다음 코드로 바꾸고, 서버, 데이터베이스, 사용자 및 암호에 대해 적절한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-the-code"></a><span data-ttu-id="b1352-132">코드 실행</span><span class="sxs-lookup"><span data-stu-id="b1352-132">Run the code</span></span>

1. <span data-ttu-id="b1352-133">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-133">At the command prompt, run the following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="b1352-134">상위 20개 행이 반환되는지 확인한 다음 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b1352-134">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b1352-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1352-135">Next Steps</span></span>
- [<span data-ttu-id="b1352-136">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="b1352-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="b1352-137">TinyTDS에 대한 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b1352-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="b1352-138">TinyTDS에 관한 문제 보고 또는 질문</span><span class="sxs-lookup"><span data-stu-id="b1352-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="b1352-139">SQL Server용 Ruby 드라이버</span><span class="sxs-lookup"><span data-stu-id="b1352-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
