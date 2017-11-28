---
title: "PHP에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 여러 PHP 코드 샘플을 제공 합니다."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="a204d-103">MySQL에 대 한 azure 데이터베이스: 사용 하 여 PHP tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="a204d-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="a204d-104">이 빠른 시작에서는 방법을 tooconnect tooan Azure를 사용 하 여 MySQL에 대 한 데이터베이스는 [PHP](http://php.net/manual/intro-whatis.php) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="a204d-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="a204d-106">이 문서에서는 익숙한 PHP를 사용 하 여 개발 하지만 새 tooworking MySQL에 대 한 Azure 데이터베이스는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a204d-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a204d-107">Prerequisites</span></span>
<span data-ttu-id="a204d-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="a204d-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="a204d-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="a204d-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="a204d-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="a204d-111">PHP 설치</span><span class="sxs-lookup"><span data-stu-id="a204d-111">Install PHP</span></span>
<span data-ttu-id="a204d-112">사용자의 서버에 PHP를 설치하거나 PHP를 포함하는 Azure [웹앱](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="a204d-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="a204d-113">MacOS</span></span>
- <span data-ttu-id="a204d-114">[PHP 7.1.4 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="a204d-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="a204d-115">PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.macosx.php) 향후 구성</span><span class="sxs-lookup"><span data-stu-id="a204d-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="a204d-116">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="a204d-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="a204d-117">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://php.net/downloads.php) 다운로드</span><span class="sxs-lookup"><span data-stu-id="a204d-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="a204d-118">PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.unix.php) 향후 구성</span><span class="sxs-lookup"><span data-stu-id="a204d-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="a204d-119">Windows</span><span class="sxs-lookup"><span data-stu-id="a204d-119">Windows</span></span>
- <span data-ttu-id="a204d-120">[PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://windows.php.net/download#php-7.1) 다운로드</span><span class="sxs-lookup"><span data-stu-id="a204d-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="a204d-121">PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.windows.php) 향후 구성</span><span class="sxs-lookup"><span data-stu-id="a204d-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="a204d-122">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a204d-122">Get connection information</span></span>
<span data-ttu-id="a204d-123">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="a204d-124">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="a204d-125">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a204d-126">Hello 왼쪽된 창에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 (예를 들어 **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="a204d-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="a204d-127">Hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-127">Click hello server name.</span></span>
4. <span data-ttu-id="a204d-128">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="a204d-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="a204d-129">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="a204d-130">![MySQL용 Azure Database 서버 이름](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="a204d-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="a204d-131">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="a204d-132">테이블 연결 및 생성</span><span class="sxs-lookup"><span data-stu-id="a204d-132">Connect and create a table</span></span>
<span data-ttu-id="a204d-133">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="a204d-134">hello 코드 hello를 사용 하 여 **MySQL 향상 확장** PHP에 포함 된 (mysqli) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="a204d-135">메서드를 호출 하는 코드를 hello [mysqli_init](http://php.net/manual/mysqli.init.php) 및 [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="a204d-136">메서드를 호출 하는 다음 [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="a204d-137">메서드를 호출 하는 다음 [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="a204d-138">Hello 호스트, 사용자 이름, 암호 및 db_name 매개 변수를 원하는 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
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

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="a204d-139">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="a204d-139">Insert data</span></span>
<span data-ttu-id="a204d-140">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 데이터를 삽입 한 **삽입** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="a204d-141">hello 코드 hello를 사용 하 여 **MySQL 향상 확장** PHP에 포함 된 (mysqli) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="a204d-142">hello 코드 메서드를 사용 하 여 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 준비 toocreate insert 문, 다음 바인딩 메서드를 사용 하 여 각 삽입 된 열 값에 대 한 매개 변수를 hello [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="a204d-143">hello 코드 실행 메서드를 사용 하 여 hello 문을 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 나중에 닫히는 hello 메서드를 사용 하 여 문 및 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="a204d-144">Hello 호스트, 사용자 이름, 암호 및 db_name 매개 변수를 원하는 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
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

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="a204d-145">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="a204d-145">Read data</span></span>
<span data-ttu-id="a204d-146">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="a204d-147">hello 코드 hello를 사용 하 여 **MySQL 향상 확장** PHP에 포함 된 (mysqli) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="a204d-148">hello 코드 메서드를 사용 하 여 [mysqli_query](http://php.net/manual/mysqli.query.php) hello sql 쿼리를 사용 하 여 수행 [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) 메서드 toofetch hello 결과 행.</span><span class="sxs-lookup"><span data-stu-id="a204d-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="a204d-149">Hello 호스트, 사용자 이름, 암호 및 db_name 매개 변수를 원하는 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="a204d-150">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="a204d-150">Update data</span></span>
<span data-ttu-id="a204d-151">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="a204d-152">hello 코드 hello를 사용 하 여 **MySQL 향상 확장** PHP에 포함 된 (mysqli) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="a204d-153">hello 코드 메서드를 사용 하 여 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 준비 된 update 문을 다음 메서드를 사용 하 여 각 업데이트 된 열 값에 대 한 hello 매개 변수를 바인딩합니다 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="a204d-154">hello 코드 실행 메서드를 사용 하 여 hello 문을 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 나중에 닫히는 hello 메서드를 사용 하 여 문 및 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="a204d-155">Hello 호스트, 사용자 이름, 암호 및 db_name 매개 변수를 원하는 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="a204d-156">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="a204d-156">Delete data</span></span>
<span data-ttu-id="a204d-157">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="a204d-158">hello 코드 hello를 사용 하 여 **MySQL 향상 확장** PHP에 포함 된 (mysqli) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="a204d-159">hello 코드 메서드를 사용 하 여 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 준비 된 문을 삭제 한 다음 바인딩 hello hello에 대 한 매개 변수 있는 메서드를 사용 하 여 hello 문에서 절 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="a204d-160">hello 코드 실행 메서드를 사용 하 여 hello 문을 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 나중에 닫히는 hello 메서드를 사용 하 여 문 및 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="a204d-161">Hello 호스트, 사용자 이름, 암호 및 db_name 매개 변수를 원하는 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="a204d-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="a204d-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a204d-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a204d-163">Azure에서 PHP 및 MySQL 웹앱 빌드</span><span class="sxs-lookup"><span data-stu-id="a204d-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
