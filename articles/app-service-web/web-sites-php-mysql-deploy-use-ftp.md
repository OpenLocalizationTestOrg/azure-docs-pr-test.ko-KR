---
title: "PHP MySQL aaaCreate Azure 앱 서비스의 응용 프로그램을 웹 및 FTP를 사용 하 여 배포"
description: "Toocreate PHP MySQL 및 사용 하 여 FTP 배포 tooAzure에 데이터를 저장 하는 응용 프로그램 웹 하는 방법을 보여 주는 자습서입니다."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 FTP를 사용하여 배포
이 자습서에서는 웹 앱 toocreate PHP MySQL 방법 등에 toodeploy FTP를 사용 하 여 합니다. 이 자습서의 내용은 컴퓨터에 [PHP][install-php], [MySQL][install-mysql], 웹 서버 및 FTP 클라이언트가 설치되어 있다는 것을 전제로 합니다. 이 자습서의 지침에 hello Windows, Mac 및 Linux를 포함 하 여 모든 운영 체제에서 수행할 수 있습니다. 이 가이드를 완료하면 Azure에서 실행하는 PHP/MySQL 웹 앱이 완성됩니다.

다음 내용을 배웁니다.

* 어떻게 toocreate 웹 앱 및 MySQL hello Azure 포털을 사용 하 여 데이터베이스입니다. 필요한 toorun 특별 한 아무 것도 기본적으로 PHP 웹 응용 프로그램에서 활성화 되므로 PHP 코드입니다.
* 어떻게 toopublish FTP를 사용 하 여 응용 프로그램 tooAzure 합니다.

이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 앱을 빌드할 수 있습니다. hello 응용 프로그램은 웹 응용 프로그램에서 호스팅할 수 있습니다. 완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.

![Azure PHP 웹 사이트][running-app]

> [!NOTE]
> Tooget 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Azure 웹 앱 만들기 및 FTP 게시 설정
웹 앱 및 MySQL 데이터베이스에는 이러한 단계 toocreate를 따르십시오.

1. 로그인 toohello [Azure 포털][management-portal]합니다.
2. Hello 클릭 **+ 새로 만들기** hello Azure 포털의 왼쪽 hello 위에 표시 아이콘입니다.
   
    ![새 Azure 웹 사이트 만들기][new-website]
3. Hello 검색 글꼴로 **웹 응용 프로그램 + MySQL** 을 클릭할 **웹 응용 프로그램 + MySQL**합니다.
   
    ![새 웹 사이트 사용자 지정 만들기][custom-create]
4. **만들기**를 클릭합니다. 고유한 응용 프로그램 서비스 이름, hello 리소스 그룹에 대 한 올바른 이름 및 새 서비스 계획을 입력 합니다.
   
    ![리소스 그룹 이름 설정][resource-group]
5. 합의 포함 하 여 새 데이터베이스에 대 한 값을 입력 toohello 약관 합니다.
   
    ![새 MySQL 데이터베이스 만들기][new-mysql-db]
6. Hello 웹 응용 프로그램을 만들면 hello 새 앱 서비스 블레이드가 표시 됩니다.
7. **설정** > **배포 자격 증명**을 클릭합니다. 
   
    ![배포 자격 증명 설정][set-deployment-credentials]
8. 사용자 이름과 암호를 제공 해야 FTP 게시를 tooenable 합니다. Hello 자격 증명을 저장 하 고 hello 사용자 이름 및 암호를 만들면를 기록 합니다.
   
    ![게시 자격 증명 만들기][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>로컬에서 앱 빌드 및 테스트
hello 등록 응용 프로그램은 사용자 이름 및 전자 메일 주소를 제공 하 여 이벤트에 대 한 tooregister를 허용 하는 간단한 PHP 응용 프로그램입니다. 이전 등록자에 대한 정보가 테이블에 표시되어 있습니다. 등록 정보는 MySQL 데이터베이스에 저장되어 있습니다. hello 앱 두 개의 파일로 구성 됩니다.

* **index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.
* **createtable.php**: hello 응용 프로그램에 대 한 hello MySQL 테이블을 만듭니다. 이 파일은 한 번만 사용됩니다.

toobuild 및 실행된 hello 응용 프로그램을 로컬로 아래의 hello 단계를 수행 합니다. 다음이 단계 가정 하 고 PHP, MySQL 및 로컬 컴퓨터에 설정 된 웹 서버 있고 활성화 한 hello [MySQL에 대 한 확장 PDO][pdo-mysql]합니다.

1. `registration`이라는 MySQL 데이터베이스를 만듭니다. 이 명령 사용 하 여 hello MySQL 명령 프롬프트에서이 수행할 수 있습니다.
   
        mysql> create database registration;
2. 웹 서버의 루트 디렉터리에서 `registration`이라는 폴더를 만들고 이 폴더 내에 `createtable.php` 및 `index.php`라는 두 파일을 만듭니다.
3. 열기 hello `createtable.php` 텍스트 편집기 또는 IDE에서 파일을 아래 hello 코드를 추가 합니다. 이 코드를 사용 하는 toocreate hello 됩니다 `registration_tbl` hello 표에 `registration` 데이터베이스입니다.
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > 에 대 한 tooupdate hello 값이 필요 합니다 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.
   > 
   > 
4. 웹 브라우저를 열고 너무 찾아보기[http://localhost/registration/createtable.php][localhost-createtable]합니다. 이렇게 하면 hello 만들어집니다 `registration_tbl` hello 데이터베이스의 테이블입니다.
5. 열기 hello **index.php** 텍스트 편집기 또는 IDE에서 파일을 hello 기본 HTML 및 CSS 코드 hello 페이지에 대 한 추가 (PHP 코드 hello 이후 단계에서 추가 될 예정임).
   
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
6. Hello PHP 태그 내 toohello 데이터베이스를 연결 하기 위한 PHP 코드를 추가 합니다.
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > 에 대 한 tooupdate hello 값이 필요 합니다 다시 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.
   > 
   > 
7. Hello 데이터베이스 연결 코드를 다음 hello 데이터베이스에 등록 정보를 삽입 하기 위한 코드를 추가 합니다.
   
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
8. 마지막으로, 위 hello 코드 뒤 hello 데이터베이스에서 데이터를 검색 하기 위한 코드를 추가 합니다.
   
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

검색할 수 있습니다 너무[http://localhost/registration/index.php] [ localhost-index] tootest hello 앱.

## <a name="get-mysql-and-ftp-connection-information"></a>MySQL 및 FTP 연결 정보 가져오기
tooconnect toohello MySQL 데이터베이스에 사용자가 웹 응용 프로그램에서 실행 되는 연결 정보를 hello 필요 합니다. tooget MySQL 연결 정보는 다음이 단계를 따르십시오.

1. Hello 앱 서비스에서 웹 앱 블레이드 hello 리소스 그룹 링크를 클릭 합니다.
   
    ![리소스 그룹 선택][select-resourcegroup]
2. 리소스 그룹에서 hello 데이터베이스를 클릭 합니다.
   
    ![데이터베이스 선택][select-database]
3. Hello 데이터베이스 요약에서 선택 **설정** > **속성**합니다.
   
    ![속성 선택][select-properties]
4. 에 대 한 hello 값을 기록해 `Database`, `Host`, `User Id`, 및 `Password`합니다.
   
    ![참고 속성][note-properties]
5. 웹 앱에서 클릭 hello **게시 프로필 다운로드** hello의 오른쪽 아래 모서리 hello 페이지에 있는 링크:
   
    ![게시 프로필 다운로드][download-publish-profile]
6. 열기 hello `.publishsettings` XML 편집기에서 파일입니다. 
7. Hello `<publishProfile >` 요소 `publishMethod="FTP"` 비슷한 toothis 좋아보이지:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Hello 기록 `publishUrl`, `userName`, 및 `userPWD` 특성입니다.

## <a name="publish-your-app"></a>앱 게시
로컬로 앱을 테스트 한 후 tooyour 웹 응용 프로그램에 FTP를 사용 하 여 게시할 수 있습니다. 그러나 먼저 tooupdate hello 데이터베이스 연결 정보 hello 응용 프로그램에 필요 합니다. 이전에 얻은 hello 데이터베이스 연결 정보를 사용 하 여 (hello에 **MySQL 가져오기 및 FTP 연결 정보가** 섹션), 다음 정보에는 업데이트 hello **둘 다** hello `createdatabase.php` 및 `index.php` hello 사용 하 여 파일을 적절 한 값:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

이제 toopublish FTP를 사용 하 여 앱을 준비 합니다.

1. 원하는 FTP 클라이언트를 엽니다.
2. Hello 입력 *호스트 이름 부분은* hello에서 `publishUrl` FTP 클라이언트에 위에서 언급 한 특성입니다.
3. Hello 입력 `userName` 및 `userPWD` 위에서 언급 한 특성 FTP 클라이언트에는 변경 되지 않습니다.
4. 연결을 설정합니다.

연결한 후 수 tooupload 수 및 필요에 따라 파일을 다운로드 합니다. 파일 toohello 루트 디렉터리를 업로드 하 고 있는지 확인 `/site/wwwroot`합니다.

둘 다에 업로드 한 후 `index.php` 및 `createtable.php`, 너무 찾아보기**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL hello 응용 프로그램에 대 한 테이블 다음 너무**http://[site 이름 ].azurewebsites.net/index.php** toobegin hello 응용 프로그램을 사용 합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

