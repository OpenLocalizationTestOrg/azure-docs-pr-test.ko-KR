---
title: "PHP에서 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 여러 PHP 코드 샘플을 제공합니다."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="105e0-103">MySQL용 Azure Database: PHP를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="105e0-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="105e0-104">이 빠른 시작에서는 [PHP](http://php.net/manual/intro-whatis.php) 응용 프로그램을 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="105e0-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="105e0-106">이 문서에서는 개발자가 PHP를 사용하여 개발하는 것에 익숙하고 MySQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="105e0-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="105e0-107">Prerequisites</span></span>
<span data-ttu-id="105e0-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="105e0-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="105e0-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="105e0-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="105e0-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="105e0-111">PHP 설치</span><span class="sxs-lookup"><span data-stu-id="105e0-111">Install PHP</span></span>
<span data-ttu-id="105e0-112">사용자의 서버에 PHP를 설치하거나 PHP를 포함하는 Azure [웹앱](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="105e0-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="105e0-113">MacOS</span></span>
- <span data-ttu-id="105e0-114">[PHP 7.1.4 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="105e0-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="105e0-115">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.macosx.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="105e0-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="105e0-116">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="105e0-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="105e0-117">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="105e0-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="105e0-118">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.unix.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="105e0-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="105e0-119">Windows</span><span class="sxs-lookup"><span data-stu-id="105e0-119">Windows</span></span>
- <span data-ttu-id="105e0-120">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://windows.php.net/download#php-7.1) 다운로드</span><span class="sxs-lookup"><span data-stu-id="105e0-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="105e0-121">PHP를 설치하고 [PHP 매뉴얼](http://php.net/manual/install.windows.php)에서 자세한 구성 정보 참조</span><span class="sxs-lookup"><span data-stu-id="105e0-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="105e0-122">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="105e0-122">Get connection information</span></span>
<span data-ttu-id="105e0-123">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="105e0-124">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="105e0-125">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="105e0-126">왼쪽 창에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="105e0-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="105e0-127">서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-127">Click the server name.</span></span>
4. <span data-ttu-id="105e0-128">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="105e0-129">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="105e0-130">![MySQL용 Azure Database 서버 이름](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="105e0-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="105e0-131">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="105e0-132">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="105e0-132">Connect and create a table</span></span>
<span data-ttu-id="105e0-133">**CREATE TABLE** SQL 문을 사용하여 테이블을 연결하고 생성하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="105e0-134">이 코드는 PHP에 포함된 **MySQL Improved Extension**(mysqli) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="105e0-135">이 코드는 [mysqli_init](http://php.net/manual/mysqli.init.php) 및 [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) 메서드를 호출하여 MySQL에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="105e0-136">그리고 [mysqli_query](http://php.net/manual/mysqli.query.php) 메서드를 호출하여 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="105e0-137">그런 다음 [mysqli_close](http://php.net/manual/mysqli.close.php) 메서드를 호출하여 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="105e0-138">host, username, password 및 db_name 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="105e0-139">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="105e0-139">Insert data</span></span>
<span data-ttu-id="105e0-140">**INSERT** SQL 문을 사용하여 데이터를 연결하고 삽입하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="105e0-141">이 코드는 PHP에 포함된 **MySQL Improved Extension**(mysqli) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="105e0-142">이 코드는 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 메서드를 사용하여 준비된 INSERT 문을 만든 후 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 메서드를 사용하여 삽입된 각 열 값의 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="105e0-143">[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 메서드를 사용하여 문을 실행한 후 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 메서드를 사용하여 문을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="105e0-144">host, username, password 및 db_name 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="105e0-145">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="105e0-145">Read data</span></span>
<span data-ttu-id="105e0-146">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="105e0-147">이 코드는 PHP에 포함된 **MySQL Improved Extension**(mysqli) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="105e0-148">[mysqli_query](http://php.net/manual/mysqli.query.php) 메서드를 사용하여 sql 쿼리를 수행하고 [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) 메서드를 사용하여 결과 행을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="105e0-149">host, username, password 및 db_name 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="105e0-150">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="105e0-150">Update data</span></span>
<span data-ttu-id="105e0-151">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="105e0-152">이 코드는 PHP에 포함된 **MySQL Improved Extension**(mysqli) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="105e0-153">이 코드는 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 메서드를 사용하여 준비된 UPDATE 문을 만든 후 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 메서드를 사용하여 업데이트된 각 열 값의 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="105e0-154">[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 메서드를 사용하여 문을 실행한 후 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 메서드를 사용하여 문을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="105e0-155">host, username, password 및 db_name 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="105e0-156">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="105e0-156">Delete data</span></span>
<span data-ttu-id="105e0-157">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="105e0-158">이 코드는 PHP에 포함된 **MySQL Improved Extension**(mysqli) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="105e0-159">이 코드는 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 메서드를 사용하여 준비된 DELETE 문을 만든 후 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 메서드를 사용하여 문의 Where 절에 대한 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="105e0-160">[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 메서드를 사용하여 문을 실행한 후 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 메서드를 사용하여 문을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="105e0-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="105e0-161">host, username, password 및 db_name 매개 변수는 원하는 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="105e0-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="105e0-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="105e0-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="105e0-163">Azure에서 PHP 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="105e0-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
