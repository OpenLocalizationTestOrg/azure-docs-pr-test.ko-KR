---
title: "PHP를 사용하여 PostgreSQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 PostgreSQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 PHP 코드 샘플을 제공합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="9b138-103">PostgreSQL용 Azure Database: PHP를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="9b138-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="9b138-104">이 빠른 시작에서는 [PHP](http://php.net/manual/intro-whatis.php) 응용 프로그램을 사용하여 PostgreSQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="9b138-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="9b138-106">이 문서에서는 개발자가 PHP를 사용하여 개발하는 것에 익숙하고 PostgreSQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b138-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9b138-107">Prerequisites</span></span>
<span data-ttu-id="9b138-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9b138-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="9b138-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="9b138-110">DB 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b138-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="9b138-111">PHP 설치</span><span class="sxs-lookup"><span data-stu-id="9b138-111">Install PHP</span></span>
<span data-ttu-id="9b138-112">사용자의 서버에 PHP를 설치하거나 PHP를 포함하는 Azure [웹앱](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="9b138-113">Windows</span><span class="sxs-lookup"><span data-stu-id="9b138-113">Windows</span></span>
- <span data-ttu-id="9b138-114">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://windows.php.net/download#php-7.1) 다운로드</span><span class="sxs-lookup"><span data-stu-id="9b138-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="9b138-115">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.windows.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="9b138-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="9b138-116">이 코드는 PHP 설치에 포함된 **pgsql** 클래스(ext/php_pgsql.dll)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="9b138-117">일반적으로 `C:\Program Files\PHP\v7.1\php.ini`에 있는 php.ini 구성 파일을 편집하여 **pgsql** 확장을 활성화했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="9b138-118">구성 파일에는 `extension=php_pgsql.so` 텍스트가 있는 줄이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="9b138-119">표시되지 않는 경우 텍스트를 추가하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="9b138-120">텍스트가 있지만 세미콜론 접두사로 주석 처리된 경우 세미콜론을 제거하여 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9b138-121">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="9b138-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="9b138-122">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="9b138-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="9b138-123">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.unix.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="9b138-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="9b138-124">이 코드는 **pgsql** 클래스(php_pgsql.so)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="9b138-125">`sudo apt-get install php-pgsql`을 실행하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="9b138-126">`/etc/php/7.0/mods-available/pgsql.ini` 구성 파일을 편집하여 **pgsql** 확장을 활성화했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="9b138-127">구성 파일에는 `extension=php_pgsql.so` 텍스트가 있는 줄이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="9b138-128">표시되지 않는 경우 텍스트를 추가하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="9b138-129">텍스트가 있지만 세미콜론 접두사로 주석 처리된 경우 세미콜론을 제거하여 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="9b138-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="9b138-130">MacOS</span></span>
- <span data-ttu-id="9b138-131">[PHP 7.1.4 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="9b138-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="9b138-132">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.macosx.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="9b138-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9b138-133">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b138-133">Get connection information</span></span>
<span data-ttu-id="9b138-134">PostgreSQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b138-135">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9b138-136">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9b138-137">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 서버를 검색합니다(예: **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="9b138-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="9b138-138">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="9b138-139">서버의 **개요** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="9b138-140">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9b138-141">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="9b138-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="9b138-142">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="9b138-143">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="9b138-143">Connect and create a table</span></span>
<span data-ttu-id="9b138-144">**CREATE TABLE** SQL 문 다음에 테이블에 행을 추가하는 **INSERT INTO** SQL 문을 사용하여 테이블을 연결 및 생성하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="9b138-145">이 코드는 [pg_connect()](http://php.net/manual/en/function.pg-connect.php) 메서드를 호출하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b138-146">그런 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) 메서드를 여러 번 호출하여 여러 명령을 실행하고 오류가 발생할 때마다 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) 메서드를 호출하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="9b138-147">그런 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="9b138-148">`$host`, `$database`, `$user` 및 `$password` 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="9b138-149">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="9b138-149">Read data</span></span>
<span data-ttu-id="9b138-150">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="9b138-151">이 코드는 [pg_connect()](http://php.net/manual/en/function.pg-connect.php) 메서드를 호출하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b138-152">그런 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) 메서드를 호출하여 SELECT 명령을 실행하고, 결과 집합에 결과를 보관하고, 오류가 발생할 때마다 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) 메서드를 호출하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="9b138-153">결과 집합을 읽으려면 루프에 행별로 [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) 메서드를 호출하고, 행 데이터가 각 배열 위치에 열당 데이터 값이 하나 있는 배열 `$row`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="9b138-154">결과 집합을 해제하려면 [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="9b138-155">그런 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="9b138-156">`$host`, `$database`, `$user` 및 `$password` 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="9b138-157">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="9b138-157">Update data</span></span>
<span data-ttu-id="9b138-158">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="9b138-159">이 코드는 [pg_connect()](http://php.net/manual/en/function.pg-connect.php) 메서드를 호출하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b138-160">그런 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) 메서드를 호출하여 명령을 실행하고 오류가 발생할 때마다 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) 메서드를 호출하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="9b138-161">그런 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="9b138-162">`$host`, `$database`, `$user` 및 `$password` 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="9b138-163">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="9b138-163">Delete data</span></span>
<span data-ttu-id="9b138-164">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="9b138-165">이 코드는 [pg_connect()](http://php.net/manual/en/function.pg-connect.php) 메서드를 호출하여 PostgreSQL용 Azure Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="9b138-166">그런 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) 메서드를 호출하여 명령을 실행하고 오류가 발생할 때마다 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) 메서드를 호출하여 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="9b138-167">그런 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9b138-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="9b138-168">`$host`, `$database`, `$user` 및 `$password` 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="9b138-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="9b138-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b138-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9b138-170">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9b138-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
