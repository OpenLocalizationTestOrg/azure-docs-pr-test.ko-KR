---
title: "Azure SQL 데이터베이스 Ruby tooquery aaaUse | Microsoft Docs"
description: "이 항목에서는 toouse Ruby toocreate tooan Azure SQL 데이터베이스와 쿼리를 TRANSACT-SQL 문을 사용 하 여 연결 하는 프로그램입니다."
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
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="3faba-103">Ruby tooquery Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3faba-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="3faba-104">이 빠른 시작 자습서에서는 설명 방법을 toouse [Ruby](https://www.ruby-lang.org) toocreate 프로그램 tooconnect tooan Azure SQL 데이터베이스 및 Transact SQL 문 tooquery 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3faba-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3faba-105">Prerequisites</span></span>

<span data-ttu-id="3faba-106">toocomplete이 빠른 시작 자습서, hello 필수 구성 요소를 수행 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="3faba-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-107">An Azure SQL database.</span></span> <span data-ttu-id="3faba-108">이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="3faba-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="3faba-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="3faba-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="3faba-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="3faba-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="3faba-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3faba-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="3faba-112">A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="3faba-113">운영 체제에 맞게 설치된 Ruby 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3faba-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="3faba-114">**MacOS**: Homebrew를 설치하고, rbenv와 ruby-build를 설치하고, Ruby를 설치한 다음, FreeTDS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="3faba-115">[1.2, 1.3, 1.4 및 1.5 단계](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) 참조</span><span class="sxs-lookup"><span data-stu-id="3faba-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="3faba-116">**Ubuntu**: Ruby용 필수 구성 요소를 설치하고, rbenv와 ruby-build를 설치하고, Ruby를 설치한 다음, FreeTDS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="3faba-117">[1.2, 1.3, 1.4 및 1.5 단계](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/) 참조</span><span class="sxs-lookup"><span data-stu-id="3faba-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="3faba-118">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="3faba-118">SQL server connection information</span></span>

<span data-ttu-id="3faba-119">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="3faba-120">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="3faba-121">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3faba-122">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="3faba-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3faba-123">Hello에 **개요** 데이터베이스 페이지에서 hello 정규화 된 서버 이름을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="3faba-124">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** hello 다음 이미지에에서 나와 있는 것 처럼 옵션:</span><span class="sxs-lookup"><span data-stu-id="3faba-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="3faba-126">Azure SQL 데이터베이스 서버에 대 한 hello 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3faba-127">방화벽 규칙에는이 자습서를 수행 하는 hello 컴퓨터의 공용 IP 주소를 hello에 대 한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="3faba-128">다른 공용 IP 주소가 있어야 하거나 다른 컴퓨터에는 경우 만들기는 [Azure 포털 hello 사용 하 여 서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="3faba-129">코드 tooquery SQL 데이터베이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="3faba-130">원하는 텍스트 편집기에서 **sqltest.rb** 파일을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="3faba-131">Hello 내용을 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="3faba-132">Hello 코드 실행</span><span class="sxs-lookup"><span data-stu-id="3faba-132">Run hello code</span></span>

1. <span data-ttu-id="3faba-133">Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="3faba-134">확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3faba-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3faba-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3faba-135">Next Steps</span></span>
- [<span data-ttu-id="3faba-136">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="3faba-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="3faba-137">TinyTDS에 대한 GitHub 리포지토리</span><span class="sxs-lookup"><span data-stu-id="3faba-137">GitHub repository for TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds)
- [<span data-ttu-id="3faba-138">TinyTDS에 관한 문제 보고 또는 질문</span><span class="sxs-lookup"><span data-stu-id="3faba-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- [<span data-ttu-id="3faba-139">SQL Server용 Ruby 드라이버</span><span class="sxs-lookup"><span data-stu-id="3faba-139">Ruby Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
