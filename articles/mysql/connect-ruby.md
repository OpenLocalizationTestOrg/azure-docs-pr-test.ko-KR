---
title: "Ruby를 사용하여 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL용 Azure Database에서 데이터를 연결하고 쿼리하는 데 사용할 수 있는 몇 가지 Ruby 코드 샘플을 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: e54f1dccbae060c52f48bfeb277c045b99a91715
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="cf1fa-103">MySQL용 Azure Database: Ruby를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="cf1fa-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="cf1fa-104">이 빠른 시작에서는 Windows, Ubuntu Linux 및 Mac 플랫폼에서 [Ruby](https://www.ruby-lang.org) 응용 프로그램 및 [mysql2](https://rubygems.org/gems/mysql2) gem을 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="cf1fa-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="cf1fa-106">이 문서에서는 Ruby를 사용하여 개발하는 데 익숙하고 MySQL용 Azure Database를 처음 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf1fa-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cf1fa-107">Prerequisites</span></span>
<span data-ttu-id="cf1fa-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cf1fa-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cf1fa-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="cf1fa-110">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cf1fa-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="cf1fa-111">Ruby 설치</span><span class="sxs-lookup"><span data-stu-id="cf1fa-111">Install Ruby</span></span>
<span data-ttu-id="cf1fa-112">Ruby, Gem 및 MySQL2 라이브러리를 자신의 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-112">Install Ruby, Gem, and the MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="cf1fa-113">Windows</span><span class="sxs-lookup"><span data-stu-id="cf1fa-113">Windows</span></span>
1. <span data-ttu-id="cf1fa-114">[Ruby](http://rubyinstaller.org/downloads/) 버전 2.3을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="cf1fa-115">시작 메뉴에서 새 명령 프롬프트(cmd)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="cf1fa-116">디렉터리를 Ruby 버전 2.3에 대한 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="cf1fa-117">`ruby -v` 명령을 실행하여 설치된 버전을 확인함으로써 Ruby 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="cf1fa-118">`gem -v` 명령을 실행하여 설치된 버전을 확인함으로써 Gem 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="cf1fa-119">`gem install mysql2` 명령을 실행하여 Gem을 사용하는 Ruby용 Mysql2 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="cf1fa-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="cf1fa-120">MacOS</span></span>
1. <span data-ttu-id="cf1fa-121">`brew install ruby` 명령을 실행하여 Homebrew로 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="cf1fa-122">자세한 설치 옵션을 보려면 Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/#homebrew)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="cf1fa-123">`ruby -v` 명령을 실행하여 설치된 버전을 확인함으로써 Ruby 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="cf1fa-124">`gem -v` 명령을 실행하여 설치된 버전을 확인함으로써 Gem 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="cf1fa-125">`gem install mysql2` 명령을 실행하여 Gem을 사용하는 Ruby용 Mysql2 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="cf1fa-126">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="cf1fa-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="cf1fa-127">`sudo apt-get install ruby-full` 명령을 실행하여 Ruby를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="cf1fa-128">자세한 설치 옵션을 보려면 Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="cf1fa-129">`ruby -v` 명령을 실행하여 설치된 버전을 확인함으로써 Ruby 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="cf1fa-130">`sudo gem update --system` 명령을 실행하여 Gem에 대한 최신 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="cf1fa-131">`gem -v` 명령을 실행하여 설치된 버전을 확인함으로써 Gem 설치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="cf1fa-132">`sudo apt-get install build-essential` 명령을 실행하여 gcc, make 및 기타 빌드 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="cf1fa-133">`sudo apt-get install libmysqlclient-dev` 명령을 실행하여 MySQL 클라이언트 개발자 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="cf1fa-134">`sudo gem install mysql2` 명령을 실행하여 Gem을 사용하는 Ruby용 mysql2 모듈을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="cf1fa-135">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="cf1fa-135">Get connection information</span></span>
<span data-ttu-id="cf1fa-136">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="cf1fa-137">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cf1fa-138">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf1fa-139">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="cf1fa-139">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="cf1fa-140">**myserver4demo** 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-140">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="cf1fa-141">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-141">Select the server's **Properties** page.</span></span> <span data-ttu-id="cf1fa-142">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-142">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cf1fa-143">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="cf1fa-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="cf1fa-144">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-144">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="cf1fa-145">Ruby 코드 실행</span><span class="sxs-lookup"><span data-stu-id="cf1fa-145">Run Ruby code</span></span> 
1. <span data-ttu-id="cf1fa-146">아래 섹션에서 Ruby 코드를 텍스트 파일에 붙여넣고 .rb 파일 확장명이 포함된 프로젝트 폴더에 저장합니다(예: `C:\rubymysql\createtable.rb` 또는 `/home/username/rubymysql/createtable.rb`).</span><span class="sxs-lookup"><span data-stu-id="cf1fa-146">Paste the Ruby code from the sections below into text files, and save the files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="cf1fa-147">코드를 실행하려면 명령 프롬프트 또는 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-147">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="cf1fa-148">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd rubymysql`).</span><span class="sxs-lookup"><span data-stu-id="cf1fa-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="cf1fa-149">그런 다음 응용 프로그램을 실행하려면 ruby 명령 다음에 파일 이름을 입력합니다(예: `ruby createtable.rb`).</span><span class="sxs-lookup"><span data-stu-id="cf1fa-149">Then type the ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="cf1fa-150">Windows OS에서 ruby 응용 프로그램이 경로 환경 변수에 없는 경우 전체 경로를 사용하여 노드 응용 프로그램을 시작해야 할 수도 있습니다(예: `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`).</span><span class="sxs-lookup"><span data-stu-id="cf1fa-150">On the Windows OS, if the ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="cf1fa-151">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="cf1fa-151">Connect and create a table</span></span>
<span data-ttu-id="cf1fa-152">**CREATE TABLE** SQL 문 다음에 테이블에 행을 추가하는 **INSERT INTO** SQL 문을 사용하여 테이블을 연결 및 생성하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-152">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="cf1fa-153">이 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 클래스 .new() 메서드를 사용하여 MySQL용 Azure 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-153">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="cf1fa-154">그런 다음 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 메서드를 여러 번 호출하여 DROP, CREATE TABLE 및 INSERT INTO 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="cf1fa-155">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="cf1fa-156">`host`, `database`, `username` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-156">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="cf1fa-157">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="cf1fa-157">Read data</span></span>
<span data-ttu-id="cf1fa-158">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-158">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="cf1fa-159">이 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 클래스 .new() 메서드를 사용하여 MySQL용 Azure 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-159">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="cf1fa-160">그런 다음 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 메서드를 호출하여 SELECT 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="cf1fa-161">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="cf1fa-162">`host`, `database`, `username` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-162">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="cf1fa-163">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="cf1fa-163">Update data</span></span>
<span data-ttu-id="cf1fa-164">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-164">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="cf1fa-165">이 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 클래스 .new() 메서드를 사용하여 MySQL용 Azure 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-165">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="cf1fa-166">그런 다음 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 메서드를 호출하여 UPDATE 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="cf1fa-167">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="cf1fa-168">`host`, `database`, `username` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-168">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="cf1fa-169">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="cf1fa-169">Delete data</span></span>
<span data-ttu-id="cf1fa-170">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-170">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="cf1fa-171">이 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) 클래스 .new() 메서드를 사용하여 MySQL용 Azure 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-171">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="cf1fa-172">그런 다음 [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 메서드를 호출하여 DELETE 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="cf1fa-173">그런 다음 종료하기 전에 [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="cf1fa-174">`host`, `database`, `username` 및 `password` 문자열은 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf1fa-174">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="cf1fa-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf1fa-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cf1fa-176">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cf1fa-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
