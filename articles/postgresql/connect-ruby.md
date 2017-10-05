---
title: "Ruby를 사용하여 PostgreSQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 PostgreSQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 Ruby 코드 샘플을 제공합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 9153a5a843dd5c18f27a3af232fea3b152240fe1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="e9c49-103">PostgreSQL용 Azure Database: Ruby를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="e9c49-103">Azure Database for PostgreSQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="e9c49-104">이 빠른 시작에서는 [Ruby](https://www.ruby-lang.org) 응용 프로그램을 사용하여 PostgreSQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="e9c49-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="e9c49-106">이 문서에서는 개발자가 Ruby를 사용하여 개발하는 것에 익숙하고 PostgreSQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9c49-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e9c49-107">Prerequisites</span></span>
<span data-ttu-id="e9c49-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e9c49-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="e9c49-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="e9c49-110">DB 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e9c49-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="e9c49-111">Ruby 설치</span><span class="sxs-lookup"><span data-stu-id="e9c49-111">Install Ruby</span></span>
<span data-ttu-id="e9c49-112">사용자의 컴퓨터에 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="e9c49-113">Windows</span><span class="sxs-lookup"><span data-stu-id="e9c49-113">Windows</span></span>
- <span data-ttu-id="e9c49-114">최신 버전의 [Ruby](http://rubyinstaller.org/downloads/)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-114">Download and Install the latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="e9c49-115">MSI 설치 관리자 마침 화면에서 "MSYS2 및 개발 도구 체인을 설치하려면 'ridk install' 실행"이라는 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-115">On the finish screen of the MSI installer, check the box that says "Run 'ridk install' to install MSYS2 and development toolchain."</span></span> <span data-ttu-id="e9c49-116">그런 다음 **마침**을 클릭하여 다음 설치 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-116">Then click **Finish** to launch the next installer.</span></span>
- <span data-ttu-id="e9c49-117">Windows용 RubyInstaller2 설치 관리자가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-117">The RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="e9c49-118">MSYS2 리포지토리 업데이트를 설치하려면 2를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-118">Type 2 to install the MSYS2 repository update.</span></span> <span data-ttu-id="e9c49-119">완료되고 설치 프롬프트로 돌아오면 명령 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-119">After it finishes and returns to the installation prompt, close the command window.</span></span>
- <span data-ttu-id="e9c49-120">시작 메뉴에서 새 명령 프롬프트(cmd)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-120">Launch a new command prompt (cmd) from the Start menu.</span></span>
- <span data-ttu-id="e9c49-121">Ruby 설치를 테스트하여 설치된 버전을 확인합니다(`ruby -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-121">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-122">Gem 설치를 테스트하여 설치된 버전을 확인합니다(`gem -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-122">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-123">`gem install pg` 명령을 실행하여 Gem으로 Ruby용 PostgreSQL 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-123">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="e9c49-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="e9c49-124">MacOS</span></span>
- <span data-ttu-id="e9c49-125">`brew install ruby` 명령을 실행하여 Homebrew로 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-125">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="e9c49-126">자세한 설치 옵션을 보려면 Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/#homebrew)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-126">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="e9c49-127">Ruby 설치를 테스트하여 설치된 버전을 확인합니다(`ruby -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-127">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-128">Gem 설치를 테스트하여 설치된 버전을 확인합니다(`gem -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-128">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-129">`gem install pg` 명령을 실행하여 Gem으로 Ruby용 PostgreSQL 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-129">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e9c49-130">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e9c49-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="e9c49-131">`sudo apt-get install ruby-full` 명령을 실행하여 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-131">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="e9c49-132">자세한 설치 옵션을 보려면 Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-132">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="e9c49-133">Ruby 설치를 테스트하여 설치된 버전을 확인합니다(`ruby -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-133">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-134">`sudo gem update --system` 명령을 실행하여 Gem에 대한 최신 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-134">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
- <span data-ttu-id="e9c49-135">Gem 설치를 테스트하여 설치된 버전을 확인합니다(`gem -v`).</span><span class="sxs-lookup"><span data-stu-id="e9c49-135">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="e9c49-136">`sudo apt-get install build-essential` 명령을 실행하여 gcc, make 및 기타 빌드 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-136">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="e9c49-137">`sudo apt-get install libpq-dev` 명령을 실행하여 PostgreSQL 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-137">Install the PostgreSQL libraries by running the command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="e9c49-138">`sudo gem install pg` 명령을 실행하여 Gem으로 Ruby pg 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-138">Build the Ruby pg module using Gem by running the command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="e9c49-139">Ruby 코드 실행</span><span class="sxs-lookup"><span data-stu-id="e9c49-139">Run Ruby code</span></span> 
- <span data-ttu-id="e9c49-140">코드를 텍스트 파일에 저장하고 `C:\rubypostgres\read.rb` 또는 `/home/username/rubypostgres/read.rb`와 같은 .rb 파일 확장자를 사용하여 프로젝트 폴더에 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-140">Save the code into a text file, and save the file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="e9c49-141">코드를 실행하려면 명령 프롬프트 또는 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-141">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="e9c49-142">프로젝트 폴더 `cd rubypostgres`로 디렉터리를 변경한 후 `ruby read.rb` 명령을 입력하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-142">Change directory into your project folder `cd rubypostgres`, then type the command `ruby read.rb` to run the application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e9c49-143">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e9c49-143">Get connection information</span></span>
<span data-ttu-id="e9c49-144">PostgreSQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-144">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e9c49-145">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-145">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e9c49-146">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-146">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e9c49-147">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 서버를 검색합니다(예: **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="e9c49-147">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="e9c49-148">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-148">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="e9c49-149">서버의 **개요** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-149">Select the server's **Overview** page.</span></span> <span data-ttu-id="e9c49-150">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-150">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e9c49-151">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="e9c49-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="e9c49-152">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-152">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name.</span></span> <span data-ttu-id="e9c49-153">필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-153">If necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="e9c49-154">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="e9c49-154">Connect and create a table</span></span>
<span data-ttu-id="e9c49-155">**CREATE TABLE** SQL 문 다음에 테이블에 행을 추가하는 **INSERT INTO** SQL 문을 사용하여 테이블을 연결 및 생성하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-155">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="e9c49-156">이 코드는 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 개체와 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) 생성자를 사용하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-156">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e9c49-157">그런 다음 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 메서드를 호출하여 DROP, CREATE TABLE 및 INSERT INTO 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="e9c49-158">이 코드는 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스를 사용하여 오류를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-158">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="e9c49-159">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="e9c49-160">`host`, `database`, `user` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-160">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="e9c49-161">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="e9c49-161">Read data</span></span>
<span data-ttu-id="e9c49-162">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-162">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="e9c49-163">이 코드는 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 개체와 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) 생성자를 사용하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-163">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e9c49-164">그런 다음 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 메서드를 호출하여 SELECT 명령을 실행하고 결과를 결과 집합에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the SELECT command, keeping the results in a result set.</span></span> <span data-ttu-id="e9c49-165">결과 집합 컬렉션이 `resultSet.each do` 루프를 사용하여 반복되고, 현재 행 값이 `row` 변수에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-165">The result set collection is iterated over using the `resultSet.each do` loop, keeping the current row values in the `row` variable.</span></span> <span data-ttu-id="e9c49-166">이 코드는 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스를 사용하여 오류를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-166">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="e9c49-167">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="e9c49-168">`host`, `database`, `user` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-168">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="e9c49-169">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="e9c49-169">Update data</span></span>
<span data-ttu-id="e9c49-170">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-170">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="e9c49-171">이 코드는 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 개체와 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) 생성자를 사용하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-171">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e9c49-172">그런 다음 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 메서드를 호출하여 UPDATE 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="e9c49-173">이 코드는 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스를 사용하여 오류를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-173">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="e9c49-174">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="e9c49-175">`host`, `database`, `user` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-175">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="e9c49-176">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="e9c49-176">Delete data</span></span>
<span data-ttu-id="e9c49-177">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-177">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e9c49-178">이 코드는 [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) 개체와 [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) 생성자를 사용하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-178">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e9c49-179">그런 다음 [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) 메서드를 호출하여 UPDATE 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="e9c49-180">이 코드는 [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) 클래스를 사용하여 오류를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-180">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="e9c49-181">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9c49-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="e9c49-182">`host`, `database`, `user` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="e9c49-182">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="e9c49-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9c49-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e9c49-184">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e9c49-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
