---
title: "Ruby를 사용 하 여 MySQL 용 tooAzure 데이터베이스 연결 | Microsoft Docs"
description: "Tooconnect를 사용 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 여러 Ruby 코드 예제를 제공 하는이 빠른 시작 합니다."
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
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="c5b15-103">MySQL에 대 한 azure 데이터베이스: 사용 하 여 Ruby tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="c5b15-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="c5b15-104">이 빠른 시작에서는 tooconnect tooan Azure를 사용 하 여 MySQL에 대 한 데이터베이스 방법을 [Ruby](https://www.ruby-lang.org) 응용 프로그램 및 hello [mysql2](https://rubygems.org/gems/mysql2) 보석 창, Ubuntu Linux 및 Mac 플랫폼에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="c5b15-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="c5b15-106">이 문서에서는 익숙한 Ruby를 사용 하 여 개발 하지만 새 tooworking MySQL에 대 한 Azure 데이터베이스는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b15-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5b15-107">Prerequisites</span></span>
<span data-ttu-id="c5b15-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c5b15-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="c5b15-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="c5b15-110">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="c5b15-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="c5b15-111">Ruby 설치</span><span class="sxs-lookup"><span data-stu-id="c5b15-111">Install Ruby</span></span>
<span data-ttu-id="c5b15-112">사용자의 컴퓨터에 Ruby, 보석, 및 hello MySQL2 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="c5b15-113">Windows</span><span class="sxs-lookup"><span data-stu-id="c5b15-113">Windows</span></span>
1. <span data-ttu-id="c5b15-114">다운로드 및 설치 hello 2.3 버전의 [Ruby](http://rubyinstaller.org/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="c5b15-115">Hello 시작 메뉴에서 새 명령 프롬프트 (cmd)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="c5b15-116">Hello 버전 2.3에 대 한 Ruby 디렉터리에 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="c5b15-117">테스트 hello hello 명령을 실행 하 여 Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="c5b15-118">Hello 명령을 실행 하 여 hello 보석 설치를 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="c5b15-119">Hello Mysql2 모듈 보석을 사용 하 여 hello 명령을 실행 하 여 Ruby 용 빌드 `gem install mysql2`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="c5b15-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="c5b15-120">MacOS</span></span>
1. <span data-ttu-id="c5b15-121">Homebrew를 사용 하 여 hello 명령을 실행 하 여 Ruby 설치 `brew install ruby`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="c5b15-122">자세한 설치 옵션에 대 한 참조 hello Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/#homebrew)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="c5b15-123">테스트 hello hello 명령을 실행 하 여 Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="c5b15-124">Hello 명령을 실행 하 여 hello 보석 설치를 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="c5b15-125">Hello Mysql2 모듈 보석을 사용 하 여 hello 명령을 실행 하 여 Ruby 용 빌드 `gem install mysql2`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="c5b15-126">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="c5b15-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="c5b15-127">Ruby hello 명령을 실행 하 여 설치 `sudo apt-get install ruby-full`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="c5b15-128">자세한 설치 옵션에 대 한 참조 hello Ruby [설치 설명서](https://www.ruby-lang.org/en/documentation/installation/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="c5b15-129">테스트 hello hello 명령을 실행 하 여 Ruby 설치 `ruby -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="c5b15-130">Hello 명령을 실행 하 여 보석에 대 한 hello 최신 업데이트를 설치 `sudo gem update --system`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="c5b15-131">Hello 명령을 실행 하 여 hello 보석 설치를 테스트 `gem -v` toosee hello 버전이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="c5b15-132">Hello 명령을 실행 하 여 hello gcc, 작성, 및 기타 빌드 도구가 설치 `sudo apt-get install build-essential`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="c5b15-133">Hello 명령을 실행 하 여 hello MySQL 클라이언트 개발자 라이브러리 설치 `sudo apt-get install libmysqlclient-dev`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="c5b15-134">Hello mysql2 모듈 보석을 사용 하 여 hello 명령을 실행 하 여 Ruby 용 빌드 `sudo gem install mysql2`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c5b15-135">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c5b15-135">Get connection information</span></span>
<span data-ttu-id="c5b15-136">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="c5b15-137">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c5b15-138">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c5b15-139">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 같은 creased 한 hello 서버에 대 한 검색 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="c5b15-140">Hello 서버 이름을 클릭 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="c5b15-141">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c5b15-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="c5b15-142">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c5b15-143">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="c5b15-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="c5b15-144">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="c5b15-145">Ruby 코드 실행</span><span class="sxs-lookup"><span data-stu-id="c5b15-145">Run Ruby code</span></span> 
1. <span data-ttu-id="c5b15-146">Hello hello 섹션 아래에서 Ruby 코드 텍스트 파일에 붙여넣고와 같은 파일 확장명.rb와 프로젝트 폴더에 hello 파일을 저장할 `C:\rubymysql\createtable.rb` 또는 `/home/username/rubymysql/createtable.rb`합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="c5b15-147">toorun hello 코드 hello 명령 프롬프트를 시작 또는 bash 셸은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="c5b15-148">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd rubymysql`).</span><span class="sxs-lookup"><span data-stu-id="c5b15-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="c5b15-149">뒤에 같은 hello 파일 이름에 따라 ruby hello 명령을 입력 `ruby createtable.rb` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="c5b15-150">Windows 운영 체제 hello hello ruby 응용 프로그램에 path 환경 변수에 없는 경우 할 수도 있습니다 toouse hello 전체 경로 toolaunch hello 노드 응용 프로그램을와 같은`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="c5b15-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="c5b15-151">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="c5b15-151">Connect and create a table</span></span>
<span data-ttu-id="c5b15-152">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문 다음에 **INSERT INTO** hello 테이블에 SQL 문 tooadd 행입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="c5b15-153">사용 하 여 hello 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) MySQL 용.new() 메서드 tooconnect tooAzure 데이터베이스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c5b15-154">메서드를 호출 하는 다음 [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) 여러 번 toorun hello 놓기, CREATE TABLE 및 INSERT INTO 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="c5b15-155">메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c5b15-156">Hello 대체 `host`, `database`, `username`, 및 `password` 고유한 값이 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection toodatabase.'

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

## <a name="read-data"></a><span data-ttu-id="c5b15-157">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="c5b15-157">Read data</span></span>
<span data-ttu-id="c5b15-158">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="c5b15-159">사용 하 여 hello 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) MySQL 용.new() 메서드 tooconnect tooAzure 데이터베이스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c5b15-160">메서드를 호출 하는 다음 [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="c5b15-161">메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c5b15-162">Hello 대체 `host`, `database`, `username`, 및 `password` 고유한 값이 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="update-data"></a><span data-ttu-id="c5b15-163">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="c5b15-163">Update data</span></span>
<span data-ttu-id="c5b15-164">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="c5b15-165">사용 하 여 hello 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) MySQL 용.new() 메서드 tooconnect tooAzure 데이터베이스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c5b15-166">메서드를 호출 하는 다음 [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello 업데이트 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="c5b15-167">메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c5b15-168">Hello 대체 `host`, `database`, `username`, 및 `password` 고유한 값이 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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


## <a name="delete-data"></a><span data-ttu-id="c5b15-169">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="c5b15-169">Delete data</span></span>
<span data-ttu-id="c5b15-170">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="c5b15-171">사용 하 여 hello 코드는 [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) MySQL 용.new() 메서드 tooconnect tooAzure 데이터베이스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="c5b15-172">메서드를 호출 하는 다음 [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="c5b15-173">메서드를 호출 하는 다음 [close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) 종료 하기 전에 tooclose hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="c5b15-174">Hello 대체 `host`, `database`, `username`, 및 `password` 고유한 값이 포함 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5b15-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="next-steps"></a><span data-ttu-id="c5b15-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5b15-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c5b15-176">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="c5b15-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
