---
title: "PHP MySQL aaaCreate Azure 앱 서비스의 응용 프로그램을 웹 및 Git를 사용 하 여 배포"
description: "Toocreate PHP 웹 MySQL의 데이터를 저장 하는 앱 및 Git 배포 tooAzure 사용 방법을 보여 주는 자습서입니다."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="1ace2-103">Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 Git를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="1ace2-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="1ace2-104">이 자습서에서는 웹 앱 toocreate PHP MySQL 방법 등에 toodeploy 것 너무[앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) Git를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="1ace2-105">사용 하 여 [PHP][install-php], hello MySQL 명령줄 도구 (의 일부가 [MySQL][install-mysql]), 및 [Git] [ install-git] 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="1ace2-106">이 자습서의 지침에 hello Windows, Mac 및 Linux를 포함 하 여 모든 운영 체제에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="1ace2-107">이 가이드를 완료하면 Azure에서 실행하는 PHP/MySQL 웹 앱이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="1ace2-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-108">You will learn:</span></span>

* <span data-ttu-id="1ace2-109">웹 앱 toocreate 및 MySQL 데이터베이스 방법 hello를 사용 하 여 [Azure 포털][management-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="1ace2-110">PHP에서 사용 중 이므로 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714) 기본적으로 필요한 toorun 특별할는 PHP 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="1ace2-111">어떻게 toopublish Git을 사용 하 여 응용 프로그램 tooAzure를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="1ace2-112">Tooenable hello 작성기 확장 tooautomate 작성기에서 작업 하는 방법 마다 `git push`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="1ace2-113">이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="1ace2-114">hello 응용 프로그램은 웹 응용 프로그램에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="1ace2-115">완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-115">A screenshot of hello completed application is below:</span></span>

![Azure PHP 웹 사이트][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="1ace2-117">Hello 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="1ace2-117">Set up hello development environment</span></span>
<span data-ttu-id="1ace2-118">이 자습서에 있다고 가정 [PHP][install-php], hello MySQL 명령줄 도구 (의 일부가 [MySQL][install-mysql]), 및 [Git] [ install-git] 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="1ace2-119">Azure 웹 앱 만들기 및 Git 게시 설정</span><span class="sxs-lookup"><span data-stu-id="1ace2-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="1ace2-120">웹 앱 및 MySQL 데이터베이스에는 이러한 단계 toocreate를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="1ace2-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="1ace2-121">로그인 toohello [Azure 포털][management-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="1ace2-122">Hello 클릭 **새로** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="1ace2-123">클릭 **모든 참조** 다음 너무**마켓플레이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="1ace2-124">**웹 + 모바일**, **웹앱 + MySQL**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="1ace2-125">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="1ace2-126">리소스 그룹의 올바른 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-126">Enter a valid name for your resource group.</span></span>
   
    ![리소스 그룹 이름 설정][resource-group]
6. <span data-ttu-id="1ace2-128">새 웹 앱의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-128">Enter values for your new web app.</span></span>
   
    ![웹앱 만들기][new-web-app]
7. <span data-ttu-id="1ace2-130">합의 포함 하 여 새 데이터베이스에 대 한 값을 입력 toohello 약관 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![새 MySQL 데이터베이스 만들기][new-mysql-db]
8. <span data-ttu-id="1ace2-132">Hello 웹 응용 프로그램을 만들면 새 웹 앱 블레이드 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="1ace2-133">**설정**에서 **연속 배포**를 클릭하고 *필요한 설정 구성*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Git 게시 설정][setup-publishing]
10. <span data-ttu-id="1ace2-135">선택 **로컬 Git 리포지토리** hello 원본에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Git 리포지토리 설정][setup-repository]
11. <span data-ttu-id="1ace2-137">사용자 이름과 암호를 제공 해야 Git 게시를 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="1ace2-138">Hello 사용자 이름 및 암호를 만들면 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="1ace2-139">이전에 Git 리포지토리를 설정한 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![게시 자격 증명 만들기][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="1ace2-141">원격 MySQL 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="1ace2-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="1ace2-142">tooconnect toohello MySQL 데이터베이스에 사용자가 웹 응용 프로그램에서 실행 되는 연결 정보를 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="1ace2-143">tooget MySQL 연결 정보는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="1ace2-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="1ace2-144">리소스 그룹에서 hello 데이터베이스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-144">From your resource group, click hello database:</span></span>
   
    ![데이터베이스 선택][select-database]
2. <span data-ttu-id="1ace2-146">Hello 데이터베이스에서 **설정**선택, **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![속성 선택][select-properties]
3. <span data-ttu-id="1ace2-148">에 대 한 hello 값을 기록해 `Database`, `Host`, `User Id`, 및 `Password`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![참고 속성][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="1ace2-150">로컬에서 앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1ace2-150">Build and test your app locally</span></span>
<span data-ttu-id="1ace2-151">웹 앱을 만들었으므로 로컬에서 응용 프로그램을 개발하여 테스트 후 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="1ace2-152">hello 등록 응용 프로그램은 사용자 이름 및 전자 메일 주소를 제공 하 여 이벤트에 대 한 tooregister를 허용 하는 간단한 PHP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="1ace2-153">이전 등록자에 대한 정보가 테이블에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="1ace2-154">등록 정보는 MySQL 데이터베이스에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="1ace2-155">hello 응용 프로그램 (복사/붙여넣기 코드 아래) 파일 한 개로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="1ace2-156">**index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="1ace2-157">toobuild 및 실행된 hello 응용 프로그램을 로컬로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="1ace2-158">이러한 단계 가정 hello PHP 및 MySQL 명령줄 도구 (MySQL의 일부) 로컬 컴퓨터에 설치 해야 하 고 활성화 한 hello 것임을 기억 [MySQL에 대 한 확장 PDO][pdo-mysql]합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="1ace2-159">Toohello 원격 MySQL을 사용 하 여 서버에 대 한 hello 값 연결 `Data Source`, `User Id`, `Password`, 및 `Database` 앞서 검색:</span><span class="sxs-lookup"><span data-stu-id="1ace2-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="1ace2-160">hello MySQL 명령 프롬프트 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="1ace2-161">다음 예제 hello 붙여넣기 `CREATE TABLE` 명령 toocreate hello `registration_tbl` 데이터베이스의 테이블에에서:</span><span class="sxs-lookup"><span data-stu-id="1ace2-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="1ace2-162">로컬 응용 프로그램 폴더의 hello 루트에서 만들 **index.php** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="1ace2-163">열기 hello **index.php** 텍스트 편집기 또는 IDE에서 파일 및 코드를 다음 hello 및 필요한 변경을 완료 hello로 표시 추가 `//TODO:` 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="1ace2-164">에 터미널 이동 tooyour 응용 프로그램 유형과 폴더 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="1ace2-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="1ace2-165">검색할 수 있습니다 너무**: //localhost: 8000 /** tootest hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="1ace2-166">앱 게시</span><span class="sxs-lookup"><span data-stu-id="1ace2-166">Publish your app</span></span>
<span data-ttu-id="1ace2-167">로컬로 앱을 테스트 한 후 tooWeb 앱 Git를 사용 하 여 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="1ace2-168">로컬 Git 리포지토리를 초기화 및 hello 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="1ace2-169">이 hello 동일 hello 집합과, Azure 포털의 웹 앱 만들기 hello hello 끝에 위의 Git 게시 섹션에 설명 된 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="1ace2-170">(선택 사항)  Git 원격 repostitory URL 위치가 잘못 하거나 잊어버린 경우에 hello Azure 포털에서 toohello 웹 응용 프로그램 속성을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="1ace2-171">GitBash 엽니다 (또는 Git 중인 경우에 터미널 프로그램 `PATH`), 응용 프로그램의 디렉터리 toohello 루트 디렉터리를 변경 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="1ace2-172">앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Git 통한 초기 푸시 tooAzure][git-initial-push]
3. <span data-ttu-id="1ace2-174">너무 찾아보기**http://[site name].azurewebsites.net/index.php** toobegin hello 응용 프로그램 (사용자 계정 관리 대시보드에이 정보가 저장 됩니다)를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1ace2-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP 웹 사이트][running-app]

<span data-ttu-id="1ace2-176">앱에 게시 한 후 변경 내용을 tooit 만들기를 시작 하 고 Git toopublish를 사용할 수 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="1ace2-177">변경 내용을 tooyour 앱 게시</span><span class="sxs-lookup"><span data-stu-id="1ace2-177">Publish changes tooyour app</span></span>
<span data-ttu-id="1ace2-178">toopublish 변경 tooyour 응용 프로그램에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="1ace2-179">변경 내용을 tooyour 로컬로 앱을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="1ace2-180">GitBash 엽니다 (또는 터미널, Git에는 it 프로그램 `PATH`), 응용 프로그램의 디렉터리 toohello 루트 디렉터리를 변경 하 고 hello 다음 명령을 실행:</span><span class="sxs-lookup"><span data-stu-id="1ace2-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="1ace2-181">앞에서 만든 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Git 통한 사이트 변경 tooAzure 푸시][git-change-push]
3. <span data-ttu-id="1ace2-183">너무 찾아보기**http://[site name].azurewebsites.net/index.php** toosee 앱과 모든 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Azure PHP 웹 사이트][running-app]

> [!NOTE]
> <span data-ttu-id="1ace2-185">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1ace2-186">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="1ace2-187">Hello 작성기 확장을 사용 하 여 작성기 자동화를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1ace2-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="1ace2-188">기본적으로 앱 서비스에서 git 배포 프로세스 hello 작업도 하지 않습니다, composer.json와 PHP 프로젝트에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="1ace2-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="1ace2-189">Composer.json 중 처리를 사용 하도록 설정할 수 `git push` hello 작성기 확장을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="1ace2-190">웹 응용 프로그램의 블레이드 hello에 프로그램 PHP에 [Azure 포털][management-portal], 클릭 **도구** > **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![작성기 확장 설정][composer-extension-settings]
2. <span data-ttu-id="1ace2-192">**추가**를 클릭한 다음 **작성기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-192">Click **Add**, then click **Composer**.</span></span>
   
    ![작성기 확장 추가][composer-extension-add]
3. <span data-ttu-id="1ace2-194">클릭 **확인** tooaccept 약관 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="1ace2-195">클릭 **확인** 다시 tooadd hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="1ace2-196">hello **설치 된 확장** 블레이드 hello 작성기 확장 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="1ace2-197">![작성기 확장 보기][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="1ace2-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="1ace2-198">이제 수행 `git add`, `git commit`, 및 `git push` hello 이전 섹션에서와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="1ace2-199">이제 작성기가 composer.json에 정의된 종속성을 설치하고 있다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![작성기 확장 성공][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="1ace2-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ace2-201">Next steps</span></span>
<span data-ttu-id="1ace2-202">자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ace2-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
