---
title: "PHP-SQL 웹 앱 만들기 및 Git를 사용하여 Azure 앱 서비스에 배포하기"
description: "Azure SQL 데이터베이스에 데이터를 저장하는 PHP 웹 앱을 만들고 Git를 사용하여 Azure 앱 서비스에 배포하는 방법을 보여 주는 자습서입니다."
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
ms.openlocfilehash: 0baa3eced3824fec0907ca937c594f127a2bdf8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="d34db-103">PHP-SQL 웹 앱 만들기 및 Git를 사용하여 Azure 앱 서비스에 배포하기</span><span class="sxs-lookup"><span data-stu-id="d34db-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="d34db-104">이 자습서에서는 Azure SQL 데이터베이스에 연결하는 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 에서 PHP 웹앱을 만들고 Git를 사용하여 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="d34db-105">이 자습서는 컴퓨터에 [PHP][install-php], [SQL Server Express][install-SQLExpress], [PHP용 SQL Server를 위한 Microsoft 드라이버](http://www.microsoft.com/download/en/details.aspx?id=20098) 및 [Git][install-git]가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="d34db-106">이 가이드를 완료하면 Azure에서 실행하는 PHP-SQL 웹 앱이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d34db-107">PHP, SQL Server Express 및 PHP용 SQL Server를 위한 Microsoft 드라이버는 [Microsoft 웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)를 사용하여 설치하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="d34db-108">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-108">You will learn:</span></span>

* <span data-ttu-id="d34db-109">[Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)을 사용하여 Azure 웹앱 및 SQL 데이터베이스를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="d34db-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d34db-110">PHP는 앱 서비스 웹 앱에서 기본적으로 사용하도록 설정되어 있으므로 PHP 코드를 실행하기 위해 특별한 조치를 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="d34db-111">Git를 사용하여 응용 프로그램을 Azure에 게시 및 다시 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="d34db-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="d34db-112">이 자습서의 지침에 따라 PHP에서 간단한 등록 웹 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="d34db-113">응용 프로그램은 Azure 웹 사이트에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="d34db-114">아래에는 완성된 응용 프로그램의 스크린샷이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-114">A screenshot of the completed application is below:</span></span>

![Azure PHP 웹 사이트](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d34db-116">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d34db-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="d34db-118">Azure 웹 앱 만들기 및 Git 게시 설정</span><span class="sxs-lookup"><span data-stu-id="d34db-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="d34db-119">Azure 웹 앱 및 SQL 데이터베이스를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d34db-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="d34db-120">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d34db-121">대시보드 왼쪽 위에 있는 **새로 만들기** 아이콘을 클릭하여 Azure Marketplace를 열고 마켓플레이스 옆의 **모두 선택**을 클릭한 다음 **웹 + 모바일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="d34db-122">마켓플레이스에서 **웹 + 모바일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="d34db-123">**웹앱 + SQL** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="d34db-124">웹앱 + SQL 앱에 대한 설명을 읽은 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="d34db-125">각 부분(**리소스 그룹**, **웹앱**, **데이터베이스** 및 **구독**)을 클릭하고 필수 필드에 대한 값을 입력하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="d34db-126">선택한 URL 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="d34db-127">데이터베이스 서버 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="d34db-127">Configure database server credentials</span></span>
   * <span data-ttu-id="d34db-128">가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-128">Select the region closest to you</span></span>
     
     ![앱 구성](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="d34db-130">웹앱 정의를 완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="d34db-131">웹앱이 만들어지면 **알림** 단추가 녹색의 **성공**으로 깜박이며 그룹에서 웹 앱 및 SQL 데이터베이스를 모두 보여주는 리소스 그룹 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="d34db-132">리소스 그룹 블레이드에서 웹 앱 아이콘을 클릭하여 웹 앱 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![웹앱의 리소스 그룹](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="d34db-134">**설정**에서 **연속 배포** > **필요한 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="d34db-135">**로컬 Git 리포지토리**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![소스 코드 위치](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="d34db-137">이전에 Git 리포지토리를 설정하지 않았으면 사용자 이름과 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="d34db-138">이를 위해서는 웹앱 블레이드에서 **설정** > **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="d34db-139">나중에 PHP 앱을 배포하는 데 사용할 Git 원격 URL을 보려면 **설정**에서 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="d34db-140">SQL 데이터베이스 연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="d34db-140">Get SQL Database connection information</span></span>
<span data-ttu-id="d34db-141">웹 앱에 연결되는 SQL 데이터베이스 인스턴스에 연결하려면 데이터베이스를 만들었을 때 지정한 연결 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="d34db-142">SQL 데이터베이스 연결 정보를 가져오려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d34db-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="d34db-143">리소스 그룹 블레이드에서 다시 SQL 데이터베이스 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="d34db-144">SQL 데이터베이스 블레이드에서 **설정** > **속성**을 클릭하고 **데이터베이스 연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![데이터베이스 속성 보기](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="d34db-146">결과 대화 상자의 **PHP** 섹션에서 `Server`, `SQL Database` 및 `User Name` 값을 기록해 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="d34db-147">PHP 웹 앱을 Azure 앱 서비스에 게시할 때 나중에 이러한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="d34db-148">로컬에서 응용 프로그램 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d34db-148">Build and test your application locally</span></span>
<span data-ttu-id="d34db-149">등록 응용 프로그램은 이름과 전자 메일 주소를 지정하여 이벤트에 등록하는 데 사용할 수 있는 간단한 PHP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="d34db-150">이전 등록자에 대한 정보가 테이블에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="d34db-151">등록 정보는 SQL 데이터베이스 인스턴스에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="d34db-152">응용 프로그램은 다음과 같은 두 파일로 구성되어 있습니다(아래에서 사용할 수 있는 코드 복사/붙여넣기).</span><span class="sxs-lookup"><span data-stu-id="d34db-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="d34db-153">**index.php**: 등록 양식 및 등록자 정보가 포함된 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="d34db-154">**createtable.php**: 응용 프로그램용 SQL 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="d34db-155">이 파일은 한 번만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-155">This file will only be used once.</span></span>

<span data-ttu-id="d34db-156">응용 프로그램을 로컬에서 실행하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="d34db-157">이러한 단계는 로컬 컴퓨터에 PHP 및 SQL Server Express가 설정되어 있으며 [SQL Server용 PDO 확장][pdo-sqlsrv]이 사용하도록 설정되어 있다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="d34db-158">`registration`이라는 SQL Server 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="d34db-159">이는 `sqlcmd` 명령 프롬프트에서 다음 명령으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="d34db-160">응용 프로그램의 루트 디렉터리에 `createtable.php`, `index.php`(이)라는 두 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="d34db-161">텍스트 편집기 또는 IDE에서 `createtable.php` 파일을 열고 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="d34db-162">이 코드는 `registration` 데이터베이스에 `registration_tbl` 테이블을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   
    <span data-ttu-id="d34db-163">값을 업데이트 해야 합니다 <code>$user</code> 및 <code>$pwd</code> 로컬 SQL Server 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="d34db-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="d34db-164">터미널의 응용 프로그램의 루트 디렉터리에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="d34db-165">웹 브라우저를 열고 **http://localhost:8000/createtable.php**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="d34db-166">그러면 데이터베이스에 `registration_tbl` 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="d34db-167">텍스트 편집기 또는 IDE에서 **index.php** 파일을 열고 페이지의 기본 HTML 및 CSS 코드를 추가합니다(PHP 코드는 이후 단계에서 추가 예정).</span><span class="sxs-lookup"><span data-stu-id="d34db-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
7. <span data-ttu-id="d34db-168">PHP 태그 내에서 데이터베이스 연결에 필요한 PHP 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="d34db-169">다시,에 대 한 값을 업데이트 해야 합니다 <code>$user</code> 및 <code>$pwd</code> 로컬 MySQL 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="d34db-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="d34db-170">데이터베이스 연결 코드 다음에 등록 정보를 데이터베이스에 삽입하는 데 필요한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
9. <span data-ttu-id="d34db-171">마지막으로 위 코드 다음에 데이터베이스에서 데이터 검색에 필요한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="d34db-172">이제 **http://localhost:8000/index.php**로 이동하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="d34db-173">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d34db-173">Publish your application</span></span>
<span data-ttu-id="d34db-174">응용 프로그램을 로컬에서 테스트한 후 Git를 사용하여 앱 서비스 웹 앱에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="d34db-175">하지만 먼저 응용 프로그램의 데이터베이스 연결 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="d34db-176">이전에 **SQL Database 연결 정보 가져오기** 섹션에서 가져온 데이터베이스 연결 정보를 사용하여 `createdatabase.php` 및 `index.php` 파일 **둘 다**에서 다음 정보를 적합한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="d34db-177">에 <code>$host</code>, 서버 값으로 추가 해야 합니다 <code>tcp:</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="d34db-178">이제 Git 게시를 설정하고 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="d34db-179">이러한 단계는 위의 **Azure 웹앱 만들기 및 Git 게시 설정** 섹션 끝에서 설명한 단계와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="d34db-180">GitBash(또는 Git가 `PATH`에 있는 경우 터미널)을 열고 응용 프로그램의 루트 디렉터리( **등록** 디렉터리)로 디렉터리를 변경한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="d34db-181">이전에 만든 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="d34db-182">**http://[웹앱 이름].azurewebsites.net/createtable.php**로 이동하여 응용 프로그램에 대한 SQL 데이터베이스 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="d34db-183">**http://[웹앱 이름].azurewebsites.net/index.php**로 이동하여 응용 프로그램 사용을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="d34db-184">응용 프로그램을 게시한 후 변경을 시작하고 Git를 사용하여 변경 내용을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="d34db-185">응용 프로그램에 변경 내용 게시</span><span class="sxs-lookup"><span data-stu-id="d34db-185">Publish changes to your application</span></span>
<span data-ttu-id="d34db-186">응용 프로그램의 변경 내용을 게시하려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="d34db-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="d34db-187">응용 프로그램을 로컬에서 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="d34db-188">GitBash를 열거나 Git가 `PATH`에 있는 경우 터미널을 열고 응용 프로그램의 루트 디렉터리로 이동한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="d34db-189">이전에 만든 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="d34db-190">**http://[웹앱 이름].azurewebsites.net/index.php**로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d34db-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d34db-191">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="d34db-191">What's changed</span></span>
* <span data-ttu-id="d34db-192">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure App Service와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d34db-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

