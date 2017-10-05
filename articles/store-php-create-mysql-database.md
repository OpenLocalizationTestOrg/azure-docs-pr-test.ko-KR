---
title: "Azure에서 MySQL 데이터베이스 만들기 및 연결"
description: "Azure 포털을 사용하여 MySQL 데이터베이스를 만든 후 Azure의 PHP 웹앱에서 연결하는 방법을 알아봅니다."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="7851d-103">Azure에서 MySQL 데이터베이스 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="7851d-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="7851d-104">이 자습서에서는 [Azure Portal](https://portal.azure.com)(공급자가 [ClearDB](http://www.cleardb.com/))에서 MySQL 데이터베이스를 만들고 [Azure App Service](app-service/app-service-value-prop-what-is.md)에서 실행 중인 PHP 웹앱에서 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7851d-105">[마켓플레이스 앱 템플릿](app-service-web/app-service-web-create-web-app-from-marketplace.md)의 일부로 MySQL 데이터베이스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="7851d-106">Azure 포털에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="7851d-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="7851d-107">Azure 포털에서 MySQL 데이터베이스를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="7851d-108">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7851d-109">왼쪽 메뉴에서 **새로 만들기** > **데이터 + 저장소** > **MySQL 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 시작](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="7851d-111">새 MySQL 데이터베이스 [블레이드](azure-portal-overview.md)에서 다음과 같이 새 MySQL 데이터베이스를 구성합니다(*블레이드*: 가로로 열리는 포털 페이지).</span><span class="sxs-lookup"><span data-stu-id="7851d-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="7851d-112">**데이터베이스 이름**: 고유하게 식별 가능한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="7851d-113">**구독**: 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="7851d-114">**데이터베이스 유형**: 저비용 또는 무료 계층의 경우 **공유**를, 전용 리소스를 가져오려면 **전용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="7851d-115">**리소스 그룹**: 기존 [리소스 그룹](azure-resource-manager/resource-group-overview.md) 에 MySQL 데이터베이스를 추가하거나 새 그룹에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="7851d-116">동일한 그룹의 리소스는 쉽게 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="7851d-117">**위치**: 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="7851d-118">기존 리소스 그룹에 추가할 때 리소스 그룹의 위치로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="7851d-119">**가격 책정 계층**: **가격 책정 계층**을 클릭한 후 가격 책정 옵션(**Mercury** 계층은 무료)을 선택한 후 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="7851d-120">**약관**: **약관**을 클릭하고 구매 정보를 검토한 후 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="7851d-121">**대시보드에 고정**: 대시보드에서 직접 액세스하려는 경우 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="7851d-122">포털 탐색에 아직 익숙하지 않은 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="7851d-123">다음 스크린 샷은 MySQL 데이터베이스를 구성하는 방법을 예로 든 것 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Azure에서 MySQL 데이터베이스 만들기 - 구성](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="7851d-125">구성을 완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-125">When you're done configuring, click **Create**.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 만들기](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="7851d-127">배포가 시작되었음을 알려주는 팝업 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="7851d-129">배포에 성공하면 다른 팝업을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="7851d-130">포털에서 MySQL 데이터베이스 블레이드가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="7851d-131">MySQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="7851d-131">Connect to your MySQL database</span></span>
<span data-ttu-id="7851d-132">새 MySQL 데이터베이스에 대한 연결 정보를 보려면 웹앱의 블레이드에서 **속성** 을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Azure에서 MySQL 데이터베이스 만들기- MySQL 데이터베이스 블레이드](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="7851d-134">이제 모든 웹앱에서 연결 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="7851d-135">간단한 PHP 앱에서 연결 정보를 사용하는 방법을 보여 주는 샘플은 [여기](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="7851d-136">Laravel 웹앱 연결(PHP 시작 자습서에서)</span><span class="sxs-lookup"><span data-stu-id="7851d-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="7851d-137">방금 [Azure에 PHP 웹앱 만들기, 구성 및 배포](app-service-web/app-service-web-php-get-started.md) 자습서를 완료했고 [Laravel](https://www.laravel.com/) 웹앱이 Azure에서 실행 중이라고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="7851d-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="7851d-138">Laravel 앱에 데이터베이스 기능을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="7851d-139">다음 단계를 따르기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="7851d-140">다음 단계에서는 [Azure에 PHP 웹앱 만들기, 구성 및 배포](app-service-web/app-service-web-php-get-started.md)자습서를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="7851d-141">로컬 개발 환경에서 MySQL 데이터베이스를 가리키도록 Laravel 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="7851d-142">이 작업을 수행하려면 Laravel 앱의 루트 디렉터리에서 `.env` 를 열고 MySQL 데이터베이스 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="7851d-143">**속성** 블레이드에서 MySQL 데이터베이스의 이름은 **데이터베이스 이름** 필드에 표시된 것이거나 다른 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="7851d-144">**연결 문자열** 필드에서 데이터베이스 매개 변수를 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="7851d-146">MySQL 액세스 권한이 있는지 확인하는 가장 빠른 방법은 [Laravel의 기본 인증 스캐폴딩](https://laravel.com/docs/5.2/authentication#authentication-quickstart)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="7851d-147">명령줄 터미널에서, Laravel 앱의 루트 디렉터리에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="7851d-148">첫 번째 명령은 `database/migrations` 디렉터리에 미리 정의된 마이그레이션에 따라 Azure에 테이블을 만들고 두 번째 명령은 사용자 등록 및 인증을 위해 기본 보기 및 경로를 스캐폴딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="7851d-149">이제 개발 서버를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="7851d-150">브라우저에서 http://localhost:8000 으로 이동하고 표시된 것처럼 새 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Azure에서 MySQL 데이터베이스에 연결 - 사용자 등록](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="7851d-152">UI 프롬프트에 따라 등록을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="7851d-153">등록이 완료되면 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-153">Once registration completes, you will be logged in.</span></span>

    ![Azure에서 MySQL 데이터베이스에 연결 - 사용자 등록](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="7851d-155">이제 Azure에서 MySQL 데이터베이스에 대한 앱을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="7851d-156">`.env` 설정을 Azure 웹앱에 복제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="7851d-157">다음 Azure CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="7851d-158">다음으로, `php artisan make:auth`를 실행하는 동안 이전에 발생한 로컬 변경 내용을 Azure에 커밋 및 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="7851d-159">Azure 웹앱으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="7851d-160">이전에 만든 사용자 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-160">Log in using the user credentials you created earlier.</span></span>

    ![Azure에서 MySQL 데이터베이스에 연결 - Azure 웹앱으로 이동](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="7851d-162">로그인하면 익숙한 로그인 후 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Azure에서 MySQL 데이터베이스에 연결 - 로그인](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="7851d-164">축하합니다. 이제 Azure의 PHP 웹앱으로 MySQL 데이터베이스에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7851d-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7851d-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7851d-165">Next steps</span></span>
<span data-ttu-id="7851d-166">자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7851d-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
