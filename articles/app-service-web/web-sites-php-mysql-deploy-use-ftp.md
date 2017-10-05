---
title: "Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 FTP를 사용하여 배포"
description: "MySQL에 데이터를 저장하는 PHP 웹 앱을 만들고 FTP를 사용하여 Azure에 배포하는 방법을 보여 주는 자습서입니다."
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
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="816c4-103">Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 FTP를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="816c4-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="816c4-104">이 자습서에서는 PHP-MySQL 웹 앱을 만들고 FTP를 사용하여 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="816c4-105">이 자습서의 내용은 컴퓨터에 [PHP][install-php], [MySQL][install-mysql], 웹 서버 및 FTP 클라이언트가 설치되어 있다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="816c4-106">이 자습서의 지침은 Windows, Mac 및 Linux를 포함하여 모든 운영 체제에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="816c4-107">이 가이드를 완료하면 Azure에서 실행하는 PHP/MySQL 웹 앱이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="816c4-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-108">You will learn:</span></span>

* <span data-ttu-id="816c4-109">Azure 포털을 사용하여 웹 앱 및 MySQL 데이터베이스를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="816c4-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="816c4-110">PHP는 웹 앱에서 기본적으로 사용하도록 설정되어 있으므로 PHP 코드를 실행하기 위해 특별한 조치를 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="816c4-111">FTP를 사용하여 응용 프로그램을 Azure에 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="816c4-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="816c4-112">이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="816c4-113">응용 프로그램은 웹 앱에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="816c4-114">아래에는 완성된 응용 프로그램의 스크린샷이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-114">A screenshot of the completed application is below:</span></span>

![Azure PHP 웹 사이트][running-app]

> [!NOTE]
> <span data-ttu-id="816c4-116">계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 평가](https://azure.microsoft.com/try/app-service/)로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="816c4-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="816c4-118">Azure 웹 앱 만들기 및 FTP 게시 설정</span><span class="sxs-lookup"><span data-stu-id="816c4-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="816c4-119">웹 앱 및 MySQL 데이터베이스를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="816c4-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="816c4-120">[Azure Portal][management-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="816c4-121">Azure 포털의 왼쪽 맨 위에서 **+ 새로 만들기** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![새 Azure 웹 사이트 만들기][new-website]
3. <span data-ttu-id="816c4-123">검색에 **웹앱 + MySQL**을 입력하고 **웹앱 + MySQL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![새 웹 사이트 사용자 지정 만들기][custom-create]
4. <span data-ttu-id="816c4-125">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-125">Click **Create**.</span></span> <span data-ttu-id="816c4-126">고유한 앱 서비스 이름, 올바른 리소스 그룹 이름 및 새 서비스 계획을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![리소스 그룹 이름 설정][resource-group]
5. <span data-ttu-id="816c4-128">약관에 대한 동의를 포함하여 새 데이터베이스의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![새 MySQL 데이터베이스 만들기][new-mysql-db]
6. <span data-ttu-id="816c4-130">웹 앱이 만들어지면 새 앱 서비스 블레이드가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="816c4-131">**설정** > **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![배포 자격 증명 설정][set-deployment-credentials]
8. <span data-ttu-id="816c4-133">FTP 게시를 사용하도록 설정하려면 사용자 이름 및 암호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="816c4-134">자격 증명을 저장하고 만든 사용자 이름 및 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![게시 자격 증명 만들기][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="816c4-136">로컬에서 앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="816c4-136">Build and test your app locally</span></span>
<span data-ttu-id="816c4-137">등록 응용 프로그램은 이름과 전자 메일 주소를 지정하여 이벤트에 등록하는 데 사용할 수 있는 간단한 PHP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="816c4-138">이전 등록자에 대한 정보가 테이블에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="816c4-139">등록 정보는 MySQL 데이터베이스에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="816c4-140">앱은 다음 두 파일로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-140">The app consists of two files:</span></span>

* <span data-ttu-id="816c4-141">**index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="816c4-142">**createtable.php**: 응용 프로그램에 대한 MySQL 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="816c4-143">이 파일은 한 번만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-143">This file will only be used once.</span></span>

<span data-ttu-id="816c4-144">앱을 빌드하여 로컬에서 실행하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="816c4-145">이러한 단계는 로컬 컴퓨터에 PHP, MySQL 및 웹 서버가 설정되어 있으며 [PDO extension for MySQL][pdo-mysql]이 사용하도록 설정되어 있다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="816c4-146">`registration`이라는 MySQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="816c4-147">이는 MySQL 명령 프롬프트에서 다음 명령으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="816c4-148">웹 서버의 루트 디렉터리에서 `registration`이라는 폴더를 만들고 이 폴더 내에 `createtable.php` 및 `index.php`라는 두 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="816c4-149">텍스트 편집기 또는 IDE에서 `createtable.php` 파일을 열고 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="816c4-150">이 코드는 `registration` 데이터베이스에 `registration_tbl` 테이블을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   > <span data-ttu-id="816c4-151">에 대 한 값을 업데이트 해야 합니다 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="816c4-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="816c4-152">웹 브라우저를 열고 [http://localhost/registration/createtable.php][localhost-createtable]로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="816c4-153">그러면 데이터베이스에 `registration_tbl` 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="816c4-154">텍스트 편집기 또는 IDE에서 **index.php** 파일을 열고 페이지의 기본 HTML 및 CSS 코드를 추가합니다(PHP 코드는 이후 단계에서 추가 예정).</span><span class="sxs-lookup"><span data-stu-id="816c4-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
6. <span data-ttu-id="816c4-155">PHP 태그 내에서 데이터베이스 연결에 필요한 PHP 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="816c4-156">다시,에 대 한 값을 업데이트 해야 합니다 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="816c4-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="816c4-157">데이터베이스 연결 코드 다음에 등록 정보를 데이터베이스에 삽입하는 데 필요한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="816c4-158">마지막으로 위 코드 다음에 데이터베이스에서 데이터 검색에 필요한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="816c4-159">이제 [http://localhost/registration/index.php][localhost-index]로 이동하여 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="816c4-160">MySQL 및 FTP 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="816c4-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="816c4-161">웹 앱에서 실행되는 MySQL 데이터베이스에 연결하려면 연결 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="816c4-162">MySQL 연결 정보를 가져오려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="816c4-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="816c4-163">앱 서비스 웹앱 블레이드에서 리소스 그룹 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![리소스 그룹 선택][select-resourcegroup]
2. <span data-ttu-id="816c4-165">리소스 그룹에서 다음 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-165">From your resource group, click the database:</span></span>
   
    ![데이터베이스 선택][select-database]
3. <span data-ttu-id="816c4-167">데이터베이스 요약에서 **설정** > **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![속성 선택][select-properties]
4. <span data-ttu-id="816c4-169">`Database`, `Host`, `User Id` 및 `Password` 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![참고 속성][note-properties]
5. <span data-ttu-id="816c4-171">웹앱에서 페이지의 오른쪽 아래에 있는 **게시 프로필 다운로드** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![게시 프로필 다운로드][download-publish-profile]
6. <span data-ttu-id="816c4-173">XML 편집기에서 `.publishsettings` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="816c4-174">다음과 유사한 `publishMethod="FTP"`가 있는 `<publishProfile >` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="816c4-175">`publishUrl`, `userName` 및 `userPWD` 특성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="816c4-176">앱 게시</span><span class="sxs-lookup"><span data-stu-id="816c4-176">Publish your app</span></span>
<span data-ttu-id="816c4-177">앱을 로컬에서 테스트한 후 FTP를 사용하여 웹 앱에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="816c4-178">하지만 먼저 응용 프로그램의 데이터베이스 연결 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="816c4-179">이전에 **MySQL 및 FTP 연결 정보 가져오기** 섹션에서 가져온 데이터베이스 연결 정보를 사용하여 `createdatabase.php` 및 `index.php` 파일 **모두**에서 다음 정보를 적합한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="816c4-180">이제 FTP를 사용하여 앱을 게시할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="816c4-181">원하는 FTP 클라이언트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="816c4-182">앞서 기록한 `publishUrl` 특성의 *호스트 이름 부분*을 FTP 클라이언트에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="816c4-183">FTP 클라이언트를 변경하지 않고 앞서 기록한 `userName` 및 `userPWD` 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="816c4-184">연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-184">Establish a connection.</span></span>

<span data-ttu-id="816c4-185">연결된 후 필요에 따라 파일을 업로드 및 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="816c4-186">루트 디렉터리 `/site/wwwroot`에 파일을 업로드하고 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="816c4-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="816c4-187">`index.php` 및 `createtable.php`를 모두 업로드한 후 **http://[사이트 이름].azurewebsites.net/createtable.php**로 이동하여 응용 프로그램용 MySQL 테이블을 만든 다음 **http://[사이트 이름].azurewebsites.net/index.php**로 이동하여 응용 프로그램을 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="816c4-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="816c4-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="816c4-188">Next steps</span></span>
<span data-ttu-id="816c4-189">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="816c4-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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

