---
title: "PHP를 사용 하 여 PostgreSQL 데이터베이스 aaaConnect tooAzure | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수는 PHP 코드 샘플을 제공 합니다."
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Azure 데이터베이스에 대 한 PostgreSQL: 사용 하 여 PHP tooconnect 및 쿼리 데이터
이 빠른 시작에서는 방법을 tooconnect tooan Azure PostgreSQL 사용에 대 한 데이터베이스는 [PHP](http://php.net/manual/intro-whatis.php) 응용 프로그램입니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. 이 문서에서는 익숙한 PHP를 사용 하 여 개발 하지만 새 tooworking PostgreSQL에 대 한 Azure 데이터베이스는 가정 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>PHP 설치
사용자의 서버에 PHP를 설치하거나 PHP를 포함하는 Azure [웹앱](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview)을 만듭니다.

### <a name="windows"></a>Windows
- [PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://windows.php.net/download#php-7.1) 다운로드
- PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.windows.php) 향후 구성
- hello 코드 hello를 사용 하 여 **pgsql** hello PHP 설치에에서 포함 된 클래스 (ext/php_pgsql.dll). 
- 활성화 된 hello **pgsql** 확장에 있는 일반적으로 hello php.ini 구성 파일을 편집 하 여 `C:\Program Files\PHP\v7.1\php.ini`합니다. hello 구성 파일에는 hello 텍스트와 인라인으로 포함 되어야 `extension=php_pgsql.so`합니다. 표시 되지 않으면 hello 텍스트를 추가 하 고 hello 파일을 저장 합니다. Hello 텍스트 하지만 세미콜론 접두사로 주석으로 표시 되 면 hello 세미콜론을 제거 하 여 주석 hello 텍스트 처리를 제거 합니다.

### <a name="linux-ubuntu"></a>Linux(Ubuntu)
- [PHP 7.1.4 스레드로부터 안전하지 않은(x64) 버전](http://php.net/downloads.php) 다운로드 
- PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.unix.php) 향후 구성
- hello 코드 hello를 사용 하 여 **pgsql** 클래스 (php_pgsql.so). `sudo apt-get install php-pgsql`을 실행하여 설치합니다.
- 활성화 된 hello **pgsql** hello를 편집 하 여 확장 `/etc/php/7.0/mods-available/pgsql.ini` 구성 파일입니다. hello 구성 파일에는 hello 텍스트와 인라인으로 포함 되어야 `extension=php_pgsql.so`합니다. 표시 되지 않으면 hello 텍스트를 추가 하 고 hello 파일을 저장 합니다. Hello 텍스트 하지만 세미콜론 접두사로 주석으로 표시 되 면 hello 세미콜론을 제거 하 여 주석 hello 텍스트 처리를 제거 합니다.

### <a name="macos"></a>MacOS
- [PHP 7.1.4 버전](http://php.net/downloads.php) 다운로드
- PHP를 설치 하 고 toohello 참조 [PHP 매뉴얼](http://php.net/manual/install.macosx.php) 향후 구성

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.
3. Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.
4. 선택 hello 서버 **개요** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-php/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="connect-and-create-a-table"></a>테이블 연결 및 생성
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 테이블을 만들 **CREATE TABLE** SQL 문 다음에 **INSERT INTO** hello 테이블에 SQL 문 tooadd 행입니다.

코드 호출 메서드에 hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) 여러 번 toorun 몇 가지 명령 및 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 오류가 될 때마다 발생 하는 경우에 대해 자세히 설명 합니다. 메서드를 호출 하는 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 연결 합니다.

Hello 대체 `$host`, `$database`, `$user`, 및 `$password` 를 원하는 값으로 매개 변수입니다. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. 

 코드 호출 메서드에 hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT 명령의 경우 결과 집합의 hello 결과 유지 하 고 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 오류가 발생 한 경우에 대해 자세히 설명 합니다.  tooread hello 결과 집합을 메서드 [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) 배열에서 데이터를 검색할 행 및 hello 행 마다 한 번씩 루프에서 호출 됩니다 `$row`, 각 배열 위치에서 열당 하나의 데이터 값을 사용 합니다.  toofree hello 결과 집합을 메서드 [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) 호출 됩니다. 메서드를 호출 하는 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 연결 합니다.

Hello 대체 `$host`, `$database`, `$user`, 및 `$password` 를 원하는 값으로 매개 변수입니다. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.

코드 호출 메서드에 hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 명령 및 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 오류가 발생 한 경우에 대해 자세히 설명 합니다. 메서드를 호출 하는 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 연결 합니다.

Hello 대체 `$host`, `$database`, `$user`, 및 `$password` 를 원하는 값으로 매개 변수입니다. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. 

 코드 호출 메서드에 hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect 너무 Azure PostgreSQL 데이터베이스. 메서드를 호출 하는 다음 [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 명령 및 [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 오류가 발생 한 경우에 대해 자세히 설명 합니다. 메서드를 호출 하는 다음 [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 연결 합니다.

Hello 대체 `$host`, `$database`, `$user`, 및 `$password` 를 원하는 값으로 매개 변수입니다. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
