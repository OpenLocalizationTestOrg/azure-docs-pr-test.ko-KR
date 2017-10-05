---
title: "Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 Git를 사용하여 배포"
description: "MySQL에 데이터를 저장하는 PHP 웹앱을 만들고 Git를 사용하여 Azure에 배포하는 방법을 보여 주는 자습서입니다."
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
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="f7253-103">Azure 웹 앱 서비스에서 PHP-MySQL 웹 앱 만들기 및 Git를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="f7253-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="f7253-104">이 자습서에서는 PHP-MySQL 웹앱을 만들고 Git를 사용하여 [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="f7253-105">컴퓨터에 설치된 [PHP][install-php], MySQL 명령줄 도구([MySQL][install-mysql]의 일부) 및 [Git][install-git]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="f7253-106">이 자습서의 지침은 Windows, Mac 및 Linux를 포함하여 모든 운영 체제에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="f7253-107">이 가이드를 완료하면 Azure에서 실행하는 PHP/MySQL 웹 앱이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="f7253-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-108">You will learn:</span></span>

* <span data-ttu-id="f7253-109">[Azure Portal][management-portal]을 사용하여 웹 앱 및 MySQL 데이터베이스를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="f7253-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="f7253-110">PHP는 [앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714) 에서 기본적으로 사용하도록 설정되므로 PHP 코드를 실행하기 위해 특별한 조치를 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="f7253-111">Git를 사용하여 응용 프로그램을 Azure에 게시 및 다시 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="f7253-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="f7253-112">작성기 확장을 사용하여 `git push`마다 작성기 태스크를 자동화하는 방법</span><span class="sxs-lookup"><span data-stu-id="f7253-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="f7253-113">이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="f7253-114">응용 프로그램은 Azure 웹 앱에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="f7253-115">아래에는 완성된 응용 프로그램의 스크린샷이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-115">A screenshot of the completed application is below:</span></span>

![Azure PHP 웹 사이트][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="f7253-117">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f7253-117">Set up the development environment</span></span>
<span data-ttu-id="f7253-118">이 자습서의 내용은 컴퓨터에 [PHP][install-php], MySQL 명령줄 도구([MySQL][install-mysql]의 일부) 및 [Git][install-git]가 설치되어 있다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="f7253-119">Azure 웹 앱 만들기 및 Git 게시 설정</span><span class="sxs-lookup"><span data-stu-id="f7253-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="f7253-120">웹 앱 및 MySQL 데이터베이스를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f7253-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="f7253-121">[Azure Portal][management-portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="f7253-122">**새로 만들기** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="f7253-123">**마켓플레이스** 옆의 **모두 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="f7253-124">**웹 + 모바일**, **웹앱 + MySQL**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="f7253-125">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="f7253-126">리소스 그룹의 올바른 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-126">Enter a valid name for your resource group.</span></span>
   
    ![리소스 그룹 이름 설정][resource-group]
6. <span data-ttu-id="f7253-128">새 웹 앱의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-128">Enter values for your new web app.</span></span>
   
    ![웹앱 만들기][new-web-app]
7. <span data-ttu-id="f7253-130">약관에 대한 동의를 포함하여 새 데이터베이스의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![새 MySQL 데이터베이스 만들기][new-mysql-db]
8. <span data-ttu-id="f7253-132">웹 앱이 만들어지면 새 웹앱 블레이드가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="f7253-133">**설정**에서 **연속 배포**를 클릭하고 *필요한 설정 구성*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Git 게시 설정][setup-publishing]
10. <span data-ttu-id="f7253-135">원본에 대한 **로컬 Git 리포지토리** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Git 리포지토리 설정][setup-repository]
11. <span data-ttu-id="f7253-137">Git 게시를 사용하도록 설정하려면 사용자 이름 및 암호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="f7253-138">만든 사용자 이름 및 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="f7253-139">이전에 Git 리포지토리를 설정한 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![게시 자격 증명 만들기][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="f7253-141">원격 MySQL 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="f7253-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="f7253-142">웹 앱에서 실행되는 MySQL 데이터베이스에 연결하려면 연결 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="f7253-143">MySQL 연결 정보를 가져오려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f7253-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="f7253-144">리소스 그룹에서 다음 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-144">From your resource group, click the database:</span></span>
   
    ![데이터베이스 선택][select-database]
2. <span data-ttu-id="f7253-146">데이터베이스 **설정**에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![속성 선택][select-properties]
3. <span data-ttu-id="f7253-148">`Database`, `Host`, `User Id` 및 `Password` 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![참고 속성][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="f7253-150">로컬에서 앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7253-150">Build and test your app locally</span></span>
<span data-ttu-id="f7253-151">웹 앱을 만들었으므로 로컬에서 응용 프로그램을 개발하여 테스트 후 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="f7253-152">등록 응용 프로그램은 이름과 전자 메일 주소를 지정하여 이벤트에 등록하는 데 사용할 수 있는 간단한 PHP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="f7253-153">이전 등록자에 대한 정보가 테이블에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="f7253-154">등록 정보는 MySQL 데이터베이스에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="f7253-155">응용 프로그램은 다음 한 파일로 구성되어 있습니다(아래에서 사용할 수 있는 코드 복사/붙여넣기).</span><span class="sxs-lookup"><span data-stu-id="f7253-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="f7253-156">**index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="f7253-157">응용 프로그램을 빌드하여 로컬에서 실행하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="f7253-158">이러한 단계는 로컬 컴퓨터에 PHP, MySQL 명령줄 도구(MySQL의 일부)가 설정되어 있으며 [PDO extension for MySQL][pdo-mysql]을 사용하도록 설정했다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="f7253-159">이전에 검색한 `Data Source`, `User Id`, `Password` 및 `Database` 값을 사용하여 원격 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="f7253-160">MySQL 명령 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="f7253-161">다음 `CREATE TABLE` 명령을 붙여 넣어 데이터베이스에 `registration_tbl` 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="f7253-162">로컬 응용 프로그램 폴더의 루트에 **index.php** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="f7253-163">텍스트 편집기 또는 IDE에서 **index.php** 파일을 열고 다음 코드를 추가하여 `//TODO:` 주석으로 표시된 필수 변경을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
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

1. <span data-ttu-id="f7253-164">터미널에서 응용 프로그램 폴더로 이동 하고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="f7253-165">이제 **http://localhost:8000/**으로 이동하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="f7253-166">앱 게시</span><span class="sxs-lookup"><span data-stu-id="f7253-166">Publish your app</span></span>
<span data-ttu-id="f7253-167">앱을 로컬에서 테스트한 후 Git를 사용하여 웹 앱에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="f7253-168">로컬 Git 리포지토리를 초기화하고 응용 프로그램을 게시하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="f7253-169">이들은 앞선 웹앱 만들기 및 Git 게시 설정 섹션의 끝에서 Azure 포털에 표시된 단계와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="f7253-170">(옵션) Git 원격 리포지토리 URL을 잊어버렸거나 제대로 보관하지 못한 경우 Azure Portal의 웹앱 속성으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="f7253-171">GitBash를 열거나 Git가 `PATH`에 있는 경우 터미널을 열고 응용 프로그램의 루트 디렉터리로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="f7253-172">이전에 만든 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Git를 통해 최초로 Azure에 푸시][git-initial-push]
3. <span data-ttu-id="f7253-174">**http://[사이트 이름].azurewebsites.net/index.php**로 이동하여 응용 프로그램의 사용을 시작합니다(이 정보는 계정 대시보드에 저장됨).</span><span class="sxs-lookup"><span data-stu-id="f7253-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP 웹 사이트][running-app]

<span data-ttu-id="f7253-176">앱을 게시한 후 변경을 시작하고 Git를 사용하여 변경 내용을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="f7253-177">앱의 변경 내용 게시</span><span class="sxs-lookup"><span data-stu-id="f7253-177">Publish changes to your app</span></span>
<span data-ttu-id="f7253-178">앱에 변경 내용을 게시하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f7253-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="f7253-179">앱을 로컬에서 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="f7253-180">GitBash를 열거나 Git가 `PATH`에 있는 경우 터미널을 열고 앱의 루트 디렉터리로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="f7253-181">이전에 만든 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Git를 통해 사이트 변경 내용을 Azure에 푸시][git-change-push]
3. <span data-ttu-id="f7253-183">**http://[사이트 이름].azurewebsites.net/index.php**로 이동하여 앱과 변경한 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Azure PHP 웹 사이트][running-app]

> [!NOTE]
> <span data-ttu-id="f7253-185">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f7253-186">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="f7253-187">작성기 확장으로 작성기 자동화 사용</span><span class="sxs-lookup"><span data-stu-id="f7253-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="f7253-188">앱 서비스의 git 배포 프로세스가 PHP 프로젝트에 있는 경우 기본적으로 composer.json로 작업하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="f7253-189">작성기 확장을 사용하여 `git push` 중에 composer.json 처리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="f7253-190">[Azure Portal][management-portal]의 PHP 웹앱의 블레이드에서 **도구** > **확장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![작성기 확장 설정][composer-extension-settings]
2. <span data-ttu-id="f7253-192">**추가**를 클릭한 다음 **작성기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-192">Click **Add**, then click **Composer**.</span></span>
   
    ![작성기 확장 추가][composer-extension-add]
3. <span data-ttu-id="f7253-194">**확인** 을 클릭하여 약관을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="f7253-195">**확인** 을 다시 클릭하여 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="f7253-196">**설치된 확장** 블레이드에 이제 작성기 확장이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="f7253-197">![작성기 확장 보기][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="f7253-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="f7253-198">이제 `git add`, `git commit` 및 `git push`을 이전 섹션처럼 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="f7253-199">이제 작성기가 composer.json에 정의된 종속성을 설치하고 있다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7253-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![작성기 확장 성공][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="f7253-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7253-201">Next steps</span></span>
<span data-ttu-id="f7253-202">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7253-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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
