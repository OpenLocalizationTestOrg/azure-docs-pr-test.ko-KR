---
title: "aaaCreate 하 고 Azure에서 MySQL 데이터베이스 사용 tooa 연결"
description: "Toouse Azure 포털 toocreate MySQL 데이터베이스 hello 하 한 다음 Azure에서 PHP 웹 응용 프로그램에서 tooit를 연결 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="464ab-103">만들고 Azure에서 MySQL 데이터베이스 사용 tooa 연결</span><span class="sxs-lookup"><span data-stu-id="464ab-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="464ab-104">이 자습서에서는 toocreate MySQL 데이터베이스 hello에 어떻게 [Azure 포털](https://portal.azure.com) (공급자가 [ClearDB](http://www.cleardb.com/)) 어떻게 tooconnect tooit에서 PHP 웹 응용 프로그램에서 실행 되 고 [Azure 앱 서비스](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="464ab-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="464ab-105">[마켓플레이스 앱 템플릿](app-service-web/app-service-web-create-web-app-from-marketplace.md)의 일부로 MySQL 데이터베이스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="464ab-106">Azure 포털에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="464ab-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="464ab-107">toocreate hello Azure 포털에서에서 MySQL 데이터베이스는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="464ab-108">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="464ab-109">Hello 왼쪽된 메뉴에서 클릭 **새로** > **데이터 + 저장소** > **MySQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 시작](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="464ab-111">새 MySQL 데이터베이스 hello에 [블레이드](azure-portal-overview.md), 새 MySQL 데이터베이스를 다음과 같이 구성 (*블레이드*: 가로로 열리면 포털 페이지):</span><span class="sxs-lookup"><span data-stu-id="464ab-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="464ab-112">**데이터베이스 이름**: 고유하게 식별 가능한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="464ab-113">**구독**: hello 구독 toouse 선택</span><span class="sxs-lookup"><span data-stu-id="464ab-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="464ab-114">**데이터베이스 유형**: 선택 **Shared** 저렴 한 비용 또는 무료 계층에 대 한 또는 **전용** tooget 전용 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="464ab-115">**리소스 그룹**: hello MySQL 데이터베이스 tooan 기존 항목 추가 [리소스 그룹](azure-resource-manager/resource-group-overview.md) 또는 새에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="464ab-116">같은 그룹 쉽게 관리할 수 있습니다 함께 hello의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="464ab-117">**위치**: 위치 닫기 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="464ab-118">Tooan 기존 리소스 그룹을 추가할 때 잠긴된 toohello 리소스 그룹 위치 것입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="464ab-119">**가격 책정 계층**: **가격 책정 계층**을 클릭한 후 가격 책정 옵션(**Mercury** 계층은 무료)을 선택한 후 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="464ab-120">**약관**: 클릭 **약관**hello 구매 세부 정보를 검토 하 고 클릭 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="464ab-121">**Pin toodashboard**: tooaccess 하려는 경우 선택 hello 대시보드에서 직접 것입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="464ab-122">포털 탐색에 아직 익숙하지 않은 경우 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="464ab-123">다음 스크린 샷 hello는 MySQL 데이터베이스를 구성 하는 방법의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Azure에서 MySQL 데이터베이스 만들기 - 구성](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="464ab-125">구성을 완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-125">When you're done configuring, click **Create**.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 만들기](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="464ab-127">배포가 시작되었음을 알려주는 팝업 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="464ab-129">배포에 성공하면 다른 팝업을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="464ab-130">hello 포털도 MySQL 데이터베이스 블레이드에서 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="464ab-131">Tooyour MySQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="464ab-132">toosee hello 연결 정보에 대 한 새 MySQL 데이터베이스를 클릭 하기만 **속성** 웹 앱의 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Azure에서 MySQL 데이터베이스 만들기- MySQL 데이터베이스 블레이드](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="464ab-134">이제 모든 웹앱에서 연결 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="464ab-135">간단한 PHP 응용 프로그램에서 toouse hello 연결 정보를 제공 하는 방법을 보여 주는 샘플 [여기](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="464ab-136">Hello PHP get 시작된 자습서) (에서 Laravel 웹 앱에 연결</span><span class="sxs-lookup"><span data-stu-id="464ab-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="464ab-137">완료 된 hello 자습서 한다고 가정해 보세요 [만들기, 구성 및 PHP 웹 응용 프로그램 tooAzure 배포](app-service-web/app-service-web-php-get-started.md) 있고는 [Laravel](https://www.laravel.com/) Azure에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="464ab-138">데이터베이스 기능 tooyour Laravel 응용 프로그램을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="464ab-139">아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="464ab-140">hello 다음 단계에서는 가정 hello 자습서를 완료 했으면 [만들기, 구성 및 PHP 웹 응용 프로그램 tooAzure 배포](app-service-web/app-service-web-php-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="464ab-141">로컬 개발 환경 toopoint toohello MySQL 데이터베이스에서 hello Laravel 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="464ab-142">toodo이,이 오픈 `.env` Laravel 앱에서 루트 디렉터리 및 hello MySQL 데이터베이스 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="464ab-143">Hello에 **속성** 블레이드에서 MySQL 데이터베이스의 이름을 hello 되거나 하나 hello 보이지 않을 hello에 **데이터베이스 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="464ab-144">더 나은 toocheck hello 데이터베이스 매개 변수에서 hello **연결 문자열** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="464ab-146">hello 액세스할 수 있는지 MySQL 이제 가장 빠른 방법은 tooverify은 toouse [Laravel의 기본 인증 스 캐 폴딩](https://laravel.com/docs/5.2/authentication#authentication-quickstart)합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="464ab-147">Hello 명령줄 터미널 hello 명령을 Laravel 응용 프로그램의 루트 디렉터리에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="464ab-148">첫 번째 명령은 hello hello에 미리 정의 된 마이그레이션에 따라 Azure의 hello 테이블을 만듭니다 `database/migrations` 디렉터리 및 hello 두 번째 명령은 스 캐 폴드 hello 기본 뷰 및 사용자 등록 및 인증에 대 한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="464ab-149">이제 hello 개발 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="464ab-150">Hello 브라우저에서 toohttp://localhost:8000 이동한 표시 된 대로 새 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Azure에서 tooMySQL 데이터베이스 연결-사용자 등록](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="464ab-152">Hello UI 프롬프트 완료 hello 등록을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="464ab-153">등록이 완료되면 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-153">Once registration completes, you will be logged in.</span></span>

    ![Azure에서 tooMySQL 데이터베이스 연결-사용자 등록](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="464ab-155">이제 Azure의 hello MySQL 데이터베이스에 대 한 응용 프로그램 개발 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="464ab-156">이제, 하기만 하면 tooreplicate 프로그램 `.env` 설정 tooyour Azure 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="464ab-157">Hello 다음 Azure CLI 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="464ab-158">다음으로 커밋하고 푸시합니다 tooAzure hello 로컬 변경 내용을 실행 하는 동안 이전에 만든 `php artisan make:auth`합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="464ab-159">Toohello Azure 웹 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="464ab-160">앞에서 만든 hello 사용자 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-160">Log in using hello user credentials you created earlier.</span></span>

    ![Azure에서 tooMySQL 데이터베이스 연결-tooAzure 웹 응용 프로그램 찾아보기](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="464ab-162">에 로그인 한 후 hello 친숙 한 사후 로그인 화면을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Azure-로그인에서 tooMySQL 데이터베이스 연결](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="464ab-164">축하합니다. 이제 Azure의 PHP 웹앱으로 MySQL 데이터베이스에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="464ab-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="464ab-165">Next steps</span></span>
<span data-ttu-id="464ab-166">자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="464ab-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
