---
title: "PHP SQL aaaCreate 웹 앱 및 tooAzure 앱 서비스 배포 Git를 사용 하 여"
description: "Toocreate PHP 웹 앱에 Azure SQL 데이터베이스에 데이터를 저장 하는 방법과 Git 배포 tooAzure 앱 서비스를 사용 하 여 보여 주는 자습서입니다."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>PHP SQL 웹 응용 프로그램을 만들고 tooAzure 앱 서비스 배포 Git를 사용 하 여
이 자습서에서는 어떻게 toocreate PHP 웹 응용 프로그램에서 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) tooAzure SQL 데이터베이스를 연결 하는 방법과 toodeploy Git를 사용 하 여 합니다. 이 자습서에 있다고 가정 [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for PHP 용 SQL Server ](http://www.microsoft.com/download/en/details.aspx?id=20098), 및 [Git] [ install-git] 컴퓨터에 설치 합니다. 이 가이드를 완료하면 Azure에서 실행하는 PHP-SQL 웹 앱이 완성됩니다.

> [!NOTE]
> 설치 하 고 hello를 사용 하 여 PHP 용 SQL Server 용 PHP, SQL Server Express 및 hello Microsoft 드라이버를 구성 [Microsoft 웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.
> 
> 

다음 내용을 배웁니다.

* 어떻게 toocreate Azure 웹 앱 및 hello를 사용 하 여 SQL 데이터베이스 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)합니다. 필요한 toorun 특별 한 아무 것도 PHP 기본적으로 앱 서비스 웹 앱에 활성화 되므로 PHP 코드입니다.
* 어떻게 toopublish Git을 사용 하 여 응용 프로그램 tooAzure를 다시 게시 합니다.

이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 응용 프로그램을 빌드할 수 있습니다. hello 응용 프로그램을 Azure 웹 사이트에서 호스트 됩니다. 완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.

![Azure PHP 웹 사이트](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Azure 웹 앱 만들기 및 Git 게시 설정
이러한 단계 toocreate Azure 웹 앱 및 SQL 데이터베이스를 수행 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello를 클릭 하 여 열기 hello Azure 마켓플레이스 **새로** hello 대시보드의 남아 있는 hello 위에 표시 아이콘을 클릭 **모두 선택** 다음 tooMarketplace 및 선택 **웹 + 모바일**합니다.
3. 마켓플레이스 hello 선택 **웹 + 모바일**합니다.
4. Hello 클릭 **웹 응용 프로그램 + SQL** 아이콘입니다.
5. 웹 응용 프로그램 hello + SQL 응용 프로그램에 대 한 hello 설명을 읽은 후 선택 **만들기**합니다.
6. 각 부분을 클릭 (**리소스 그룹**, **웹 앱**, **데이터베이스**, 및 **구독**)를 입력 하거나 필요한 hello에 대 한 값을 선택 필드:
   
   * 선택한 URL 이름을 입력합니다.    
   * 데이터베이스 서버 자격 증명 구성
   * Hello 지역 가장 가까운 tooyou 선택
     
     ![앱 구성](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Hello 웹 응용 프로그램 정의 완료 되 면 클릭 **만들기**합니다.
   
    Hello 웹 응용 프로그램을 만들면 hello **알림** 단추가 녹색 깜박입니다 **성공** 모두 hello 웹 앱과 hello SQL 데이터베이스 hello 그룹의 리소스 그룹 블레이드 열기 tooshow hello 및 합니다.
8. Hello 리소스 그룹 블레이드 tooopen hello 웹 응용 프로그램의 블레이드에서 hello 웹 앱의 아이콘을 클릭 합니다.
   
    ![웹앱의 리소스 그룹](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. **설정**에서 **연속 배포** > **필요한 설정 구성**을 클릭합니다. **로컬 Git 리포지토리**를 선택하고 **확인**을 클릭합니다.
   
    ![소스 코드 위치](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    이전에 Git 리포지토리를 설정하지 않았으면 사용자 이름과 암호를 제공해야 합니다. toodo이를 클릭 하이 여 **설정** > **배포 자격 증명** hello 웹 앱의 블레이드에서 합니다.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. **설정** 클릭 **속성** toosee hello Git 원격 URL 하면 나중에 필요 toouse toodeploy PHP 응용 프로그램입니다.

## <a name="get-sql-database-connection-information"></a>SQL 데이터베이스 연결 정보 가져오기
tooconnect toohello SQL 데이터베이스 인스턴스를 연결 tooyour 웹 응용 프로그램에 사용자가 hello 데이터베이스를 만들 때 지정한 연결 정보를 hello 필요 합니다. tooget hello SQL 데이터베이스 연결 정보는 다음이 단계를 따르십시오.

1. Hello 리소스 그룹의 블레이드에 다시 hello SQL 데이터베이스의 아이콘을 클릭 합니다.
2. Hello SQL 데이터베이스 블레이드 클릭 **설정** > **속성**, 클릭 **데이터베이스 연결 문자열 표시**합니다. 
   
    ![데이터베이스 속성 보기](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Hello에서 **PHP** 섹션 대화 상자의 결과 hello 메모해 hello 값에 대 한 `Server`, `SQL Database`, 및 `User Name`합니다. PHP 웹 응용 프로그램 tooAzure 앱 서비스를 게시 경우 나중에 이러한 값을 사용 합니다.

## <a name="build-and-test-your-application-locally"></a>로컬에서 응용 프로그램 빌드 및 테스트
hello 등록 응용 프로그램은 사용자 이름 및 전자 메일 주소를 제공 하 여 이벤트에 대 한 tooregister를 허용 하는 간단한 PHP 응용 프로그램입니다. 이전 등록자에 대한 정보가 테이블에 표시되어 있습니다. 등록 정보는 SQL 데이터베이스 인스턴스에 저장되어 있습니다. 두 파일 (복사/붙여넣기 코드 아래)의 hello 응용 프로그램 구성 됩니다.

* **index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.
* **createtable.php**: hello 응용 프로그램에 대 한 hello SQL 데이터베이스 테이블을 만듭니다. 이 파일은 한 번만 사용됩니다.

toorun hello 응용 프로그램을 로컬로 아래 hello 단계를 따릅니다. PHP 있고 SQL Server Express 로컬 컴퓨터에 설정 하 고 활성화 한 hello 가정 하면 다음이 단계는 [SQL Server에 대 한 확장 PDO][pdo-sqlsrv]합니다.

1. `registration`이라는 SQL Server 데이터베이스를 만듭니다. Hello에서 이렇게 하려면 `sqlcmd` 이러한 명령 사용 하 여 명령 프롬프트:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. 응용 프로그램의 루트 디렉터리에 `createtable.php`, `index.php`(이)라는 두 파일을 만듭니다.
3. 열기 hello `createtable.php` 텍스트 편집기 또는 IDE에서 파일을 아래 hello 코드를 추가 합니다. 이 코드를 사용 하는 toocreate hello 됩니다 `registration_tbl` hello 표에 `registration` 데이터베이스입니다.
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    에 대 한 tooupdate hello 값 해야 <code>$user</code> 및 <code>$pwd</code> 로컬 SQL Server 사용자 이름 및 암호.
4. 다음 명령을 hello 응용 프로그램 유형 hello의 hello 루트 디렉터리에서 종료:
   
        php -S localhost:8000
5. 웹 브라우저를 열고 너무 찾아보기**http://localhost:8000/createtable.php**합니다. 이렇게 하면 hello 만들어집니다 `registration_tbl` hello 데이터베이스의 테이블입니다.
6. 열기 hello **index.php** 텍스트 편집기 또는 IDE에서 파일을 hello 기본 HTML 및 CSS 코드 hello 페이지에 대 한 추가 (PHP 코드 hello 이후 단계에서 추가 될 예정임).
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. Hello PHP 태그 내 toohello 데이터베이스를 연결 하기 위한 PHP 코드를 추가 합니다.
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    에 대 한 tooupdate hello 값이 필요 합니다 다시 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.
8. Hello 데이터베이스 연결 코드를 다음 hello 데이터베이스에 등록 정보를 삽입 하기 위한 코드를 추가 합니다.
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. 마지막으로, 위 hello 코드 뒤 hello 데이터베이스에서 데이터를 검색 하기 위한 코드를 추가 합니다.
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

검색할 수 있습니다 너무**http://localhost:8000/index.php** tootest hello 응용 프로그램입니다.

## <a name="publish-your-application"></a>응용 프로그램 게시
응용 프로그램을 로컬로 테스트 한 후 tooApp 서비스 웹 앱 Git를 사용 하 여 게시할 수 있습니다. 그러나 먼저 tooupdate hello 데이터베이스 연결 정보 hello 응용 프로그램에 필요 합니다. 이전에 얻은 hello 데이터베이스 연결 정보를 사용 하 여 (hello에 **가져올 SQL 데이터베이스 연결 정보** 섹션), 다음 정보에는 업데이트 hello **둘 다** hello `createdatabase.php` 및 `index.php` hello 사용 하 여 파일을 적절 한 값:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> Hello에 <code>$host</code>와 서버 hello 값 앞에 추가 될 해야 <code>tcp:</code>합니다.
> 
> 

이제 Git 게시를 준비 tooset 있고 hello 응용 프로그램을 게시 합니다.

> [!NOTE]
> 이 hello의 hello 끝에 동일한 단계를 설명 하는 hello **Azure 웹 앱을 만들고 Git 게시 설정** 위의 섹션.
> 
> 

1. GitBash 엽니다 (또는 터미널, Git에 있으면 프로그램 `PATH`), 응용 프로그램의 디렉터리 toohello 루트 디렉터리를 변경 (hello **등록** 디렉터리), 실행된 hello 명령에 따라:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.
2. 너무 찾아보기**http://[web 앱 name].azurewebsites.net/createtable.php** hello 응용 프로그램에 대 한 toocreate hello SQL 데이터베이스 테이블입니다.
3. 너무 찾아보기**http://[web 앱 name].azurewebsites.net/index.php** toobegin hello 응용 프로그램을 사용 합니다.

응용 프로그램을 게시 한 후 변경 tooit 만들기를 시작 하는 Git toopublish를 사용 하 여 해당 합니다. 

## <a name="publish-changes-tooyour-application"></a>변경 내용을 tooyour 응용 프로그램 게시
toopublish 변경 tooapplication, 다음이 단계를 수행 합니다.

1. 변경 내용을 로컬로 tooyour 응용 프로그램을 확인 합니다.
2. GitBash 엽니다 (또는 터미널, Git에는 it 프로그램 `PATH`), 응용 프로그램의 디렉터리 toohello 루트 디렉터리를 변경 하 고 hello 다음 명령을 실행:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.
3. 너무 찾아보기**http://[web 앱 name].azurewebsites.net/index.php** toosee 변경 내용을 합니다.

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

