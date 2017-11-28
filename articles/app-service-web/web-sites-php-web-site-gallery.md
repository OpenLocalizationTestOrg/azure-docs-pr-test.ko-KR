---
title: "Azure 앱 서비스에서 WordPress 웹 응용 프로그램 aaaCreate | Microsoft Docs"
description: "Toocreate 새로운 Azure hello Azure 포털을 사용 하 여 WordPress 블로그에 대 한 응용 프로그램 웹 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="ba69a-103">Azure 앱 서비스에서 WordPress 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ba69a-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="ba69a-104">이 자습서에서는 hello Azure Marketplace에서에서 toodeploy WordPress 블로그 사이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="ba69a-105">Hello 자습서와 함께 완료 되 면 WordPress 블로그 사이트 자체를 및 hello 클라우드에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![WordPress 사이트](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="ba69a-107">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-107">You'll learn:</span></span>

* <span data-ttu-id="ba69a-108">어떻게 toofind hello Azure Marketplace에서에서 응용 프로그램 템플릿에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="ba69a-109">어떻게 toocreate Azure 응용 프로그램에서 웹 응용 프로그램 서비스는 hello 서식 파일을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="ba69a-110">어떻게 tooconfigure Azure 앱 서비스 설정을 새 hello에 대 한 웹 앱 및 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="ba69a-111">Azure 마켓플레이스 hello Microsoft, 제 3 자 회사 및 오픈 소스 소프트웨어 프로젝트에서 개발 하는 인기 있는 웹 응용 프로그램의 다양 한 범위의 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="ba69a-112">hello 웹 응용 프로그램을와 같은 다양 한 인기 있는 프레임 워크에서 빌드된 [PHP](/develop/nodejs/) 이 WordPress 예에서 [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), 및 [Python](/develop/python/), 몇 가지 tooname 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="ba69a-113">웹 응용 프로그램에서 필요한 소프트웨어를 hello에 대 한 사용 하는 hello 브라우저 파일인 Azure 마켓플레이스 hello hello toocreate [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="ba69a-114">이 자습서에서 배포 하는 hello WordPress 사이트 hello 데이터베이스에 대 한 MySQL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="ba69a-115">Hello 데이터베이스에 대 한 SQL 데이터베이스 tooinstead 사용 하려는 경우 참조 [프로젝트 Nami](http://projectnami.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="ba69a-116">**Nami 프로젝트** hello 마켓플레이스를 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="ba69a-117">toocomplete이이 자습서에서는 Microsoft Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="ba69a-118">[계정이 없는 경우 Visual Studio 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)을 활성화하거나 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="ba69a-119">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="ba69a-120">여기서 신용 카드와 약정 없이 앱 서비스에서 수명이 짧은 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="ba69a-121">WordPress 선택 및 Azure 앱 서비스에 대한 구성</span><span class="sxs-lookup"><span data-stu-id="ba69a-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="ba69a-122">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ba69a-123">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-123">Click **New**.</span></span>
   
    ![새로 만들기][5]
3. <span data-ttu-id="ba69a-125">**WordPress**를 검색한 다음 **WordPress**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="ba69a-126">Toouse MySQL 대신 SQL 데이터베이스를 원하는 경우 검색할 **프로젝트 Nami**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![목록에서 WordPress][7]
4. <span data-ttu-id="ba69a-128">Hello WordPress 응용 프로그램에 대 한 hello 설명을 읽은 후 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![생성](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="ba69a-130">Hello에 hello 웹 앱에 대 한 이름을 입력 **웹 응용 프로그램** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="ba69a-131">Hello 웹 앱의 URL을 hello {name} 때문에이 이름은 hello azurewebsites.net 도메인에서 고유 해야 합니다. azurewebsites.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="ba69a-132">입력 한 hello 이름이 고유 하지 않으면 빨간색 느낌표가 hello 텍스트 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="ba69a-133">Hello를 선택 하는 둘 이상의 구독이 있는 경우 하나의 원하는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="ba69a-134">**리소스 그룹** 을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="ba69a-135">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba69a-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="ba69a-136">**앱 서비스 계획/위치** 을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="ba69a-137">앱 서비스 계획에 대한 자세한 내용은 [Azure 앱 서비스 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ba69a-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="ba69a-138">클릭 **데이터베이스**, 한 다음 hello **새 MySQL 데이터베이스** 블레이드 MySQL 데이터베이스를 구성 하는 데 필요한 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="ba69a-139">a.</span><span class="sxs-lookup"><span data-stu-id="ba69a-139">a.</span></span> <span data-ttu-id="ba69a-140">새 이름을 입력 하거나 hello 기본 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="ba69a-141">b.</span><span class="sxs-lookup"><span data-stu-id="ba69a-141">b.</span></span> <span data-ttu-id="ba69a-142">Hello 둡니다 **데이터베이스 유형** 도**Shared**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="ba69a-143">c.</span><span class="sxs-lookup"><span data-stu-id="ba69a-143">c.</span></span> <span data-ttu-id="ba69a-144">Hello hello 웹 앱에 대 한 선택한 한 hello으로 같은 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="ba69a-145">d.</span><span class="sxs-lookup"><span data-stu-id="ba69a-145">d.</span></span> <span data-ttu-id="ba69a-146">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-146">Choose a pricing tier.</span></span> <span data-ttu-id="ba69a-147">이 자습서에 Mercury를 사용해도 됩니다.(최소 허용된 연결 및 디스크 공간 무료)</span><span class="sxs-lookup"><span data-stu-id="ba69a-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="ba69a-148">Hello에 **새 MySQL 데이터베이스** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="ba69a-149">Hello에 **WordPress** 블레이드에서 hello 약관을 동의 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![웹앱 구성](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="ba69a-151">Azure 앱 서비스는 hello 웹 응용 프로그램에서 1 분 미만에서 일반적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="ba69a-152">Hello hello 포털 페이지 위쪽에 hello 종 모양 아이콘을 클릭 하 여 hello 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![진행률 표시기](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="ba69a-154">WordPress 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="ba69a-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="ba69a-155">Hello 웹 응용 프로그램 생성이 완료 되 면 hello 응용 프로그램을 만든 하 고 hello web app 및 hello 데이터베이스를 볼 수 있는 hello Azure 포털 toohello 리소스 그룹에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="ba69a-156">hello hello 전구 아이콘을 사용 하 여 추가 리소스는 [Application Insights](/services/application-insights/), 웹 앱에 대 한 모니터링 서비스를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="ba69a-157">Hello에 **리소스 그룹** 블레이드에서 hello 웹 응용 프로그램 선을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![웹앱 구성](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="ba69a-159">Hello 웹 앱 블레이드 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![사이트 URL][browse]
4. <span data-ttu-id="ba69a-161">WordPress hello에 **시작** 페이지, WordPress에 필요한 hello 구성 정보를 입력 한 다음 클릭 **WordPress 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress 구성](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="ba69a-163">Hello에 만든 hello 자격 증명을 사용 하 여 로그인 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ba69a-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="ba69a-164">사이트 대시보드 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress 사이트](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="ba69a-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba69a-166">Next steps</span></span>
<span data-ttu-id="ba69a-167">지금까지 살펴본 어떻게 toocreate hello 갤러리에서 PHP 웹 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="ba69a-168">Azure에서 PHP를 사용 하는 방법에 대 한 자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="ba69a-169">방법에 대 한 자세한 내용은 앱 서비스 웹 앱과 toowork hello hello 페이지 (와이드 브라우저 창)의 왼쪽에 hello 링크를 참조 하십시오. 또는 hello (좁은 브라우저 창)에 대 한 hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="ba69a-170">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="ba69a-170">What's changed</span></span>
* <span data-ttu-id="ba69a-171">가이드 toohello 변경 tooApp 웹 사이트 서비스에서에서 참조 [Azure 앱 서비스와 기존 Azure 서비스에 미치는 영향은](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba69a-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
