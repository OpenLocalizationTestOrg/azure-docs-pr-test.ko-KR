---
title: "Azure App Service에서 WordPress 웹앱 만들기 | Microsoft Docs"
description: "Azure 포털을 사용하여 WordPress 블로그에 새 Azure 웹앱을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="515cb-103">Azure 앱 서비스에서 WordPress 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="515cb-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="515cb-104">이 자습서는 Azure 마켓플레이스에서 WordPress 블로그 사이트를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="515cb-105">자습서가 완료되면 클라우드에서 고유의 WordPress 블로그 사이트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![WordPress 사이트](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="515cb-107">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-107">You'll learn:</span></span>

* <span data-ttu-id="515cb-108">Azure 마켓플레이스에서 응용 프로그램 템플릿을 찾는 방법.</span><span class="sxs-lookup"><span data-stu-id="515cb-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="515cb-109">템플릿을 기반으로 하는 Azure 앱 서비스에서 웹앱을 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="515cb-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="515cb-110">새 웹앱 및 데이터베이스에 Azure 앱 서비스 설정을 구성하는 방법.</span><span class="sxs-lookup"><span data-stu-id="515cb-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="515cb-111">Azure 마켓플레이스에서 Microsoft, 타사 및 오픈 소스 소프트웨어에서 개발된 다양한 인기 웹 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="515cb-112">웹앱은 이 WordPress 예제에서 [PHP](/develop/nodejs/), [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) 및 [Python](/develop/python/) 등과 같은 광범위하고 인기있는 프레임워크에서 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="515cb-113">Azure 마켓플레이스에서 웹앱을 만들려면 유일하게 필요한 소프트웨어는 [Azure 포털](https://portal.azure.com/)에 대해 사용하는 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="515cb-114">이 자습서에서 배포하는 WordPress 사이트는 데이터베이스에 MySQL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="515cb-115">대신 데이터베이스에 SQL 데이터베이스를 사용하려는 경우 [프로젝트 Nami](http://projectnami.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="515cb-116">**프로젝트 Nami** 는 마켓플레이스를 통해서도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="515cb-117">이 자습서를 완료하려면 Microsoft Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="515cb-118">계정이 없는 경우 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)하거나 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="515cb-119">Azure 계정을 등록하기 전에 Azure 앱 서비스를 시작하려는 경우 [앱 서비스 평가](https://azure.microsoft.com/try/app-service/)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="515cb-120">여기서 신용 카드와 약정 없이 앱 서비스에서 수명이 짧은 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="515cb-121">WordPress 선택 및 Azure 앱 서비스에 대한 구성</span><span class="sxs-lookup"><span data-stu-id="515cb-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="515cb-122">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="515cb-123">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-123">Click **New**.</span></span>
   
    ![새로 만들기][5]
3. <span data-ttu-id="515cb-125">**WordPress**를 검색한 다음 **WordPress**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="515cb-126">MySQL 대신 SQL 데이터베이스를 사용하려는 경우 **프로젝트 Nami**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![목록에서 WordPress][7]
4. <span data-ttu-id="515cb-128">WordPress 앱에 대한 설명을 읽은 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![만들기](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="515cb-130">**웹앱** 상자에서 웹앱에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="515cb-131">웹앱의 URL이 {name}.azurewebsites.net이기 때문에 이 이름은 azurewebsites.net 도메인에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="515cb-132">입력한 이름이 고유하지 않으면 빨간색 느낌표가 텍스트 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="515cb-133">구독이 둘 이상 있는 경우 사용하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="515cb-134">**리소스 그룹** 을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="515cb-135">리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="515cb-136">**앱 서비스 계획/위치** 을 선택하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="515cb-137">앱 서비스 계획에 대한 자세한 내용은 [Azure 앱 서비스 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="515cb-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="515cb-138">**데이터베이스**를 클릭하고 **새 MySQL 데이터베이스** 블레이드에서 MySQL 데이터베이스를 구성하는 데 필요한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="515cb-139">a.</span><span class="sxs-lookup"><span data-stu-id="515cb-139">a.</span></span> <span data-ttu-id="515cb-140">새 이름을 입력하거나 기본 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="515cb-141">b.</span><span class="sxs-lookup"><span data-stu-id="515cb-141">b.</span></span> <span data-ttu-id="515cb-142">**데이터베이스 형식**을 **공유**로 설정해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="515cb-143">c.</span><span class="sxs-lookup"><span data-stu-id="515cb-143">c.</span></span> <span data-ttu-id="515cb-144">웹앱에 사용자가 선택한 동일한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="515cb-145">d.</span><span class="sxs-lookup"><span data-stu-id="515cb-145">d.</span></span> <span data-ttu-id="515cb-146">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-146">Choose a pricing tier.</span></span> <span data-ttu-id="515cb-147">이 자습서에 Mercury를 사용해도 됩니다.(최소 허용된 연결 및 디스크 공간 무료)</span><span class="sxs-lookup"><span data-stu-id="515cb-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="515cb-148">**새 MySQL 데이터베이스** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="515cb-149">**WordPress** 블레이드에서 법적 조건에 동의한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![웹앱 구성](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="515cb-151">Azure 앱 서비스는 일반적으로 일 분 내에 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="515cb-152">포털 페이지의 위쪽에 종 아이콘을 클릭하여 진행률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![진행률 표시기](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="515cb-154">WordPress 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="515cb-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="515cb-155">웹앱 만들기가 완료되면 Azure 포털에서 응용 프로그램을 만든 리소스 그룹으로 이동하고 웹앱 및 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="515cb-156">전구 아이콘이 있는 추가 리소스는 [Application Insights](/services/application-insights/)이며 웹앱에 대한 모니터링 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="515cb-157">**리소스 그룹** 블레이드에서 웹앱 줄을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![웹앱 구성](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="515cb-159">웹앱 블레이드에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-159">In the Web app blade, click **Browse**.</span></span>
   
    ![사이트 URL][browse]
4. <span data-ttu-id="515cb-161">WordPress **시작** 페이지에서 WordPress에 필요한 구성 정보를 입력한 다음 **WordPress 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress 구성](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="515cb-163">**시작** 페이지에서 만든 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="515cb-164">사이트 대시보드 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress 사이트](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="515cb-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="515cb-166">Next steps</span></span>
<span data-ttu-id="515cb-167">갤러리에서 PHP 웹앱을 만들어 배포하는 방법을 살펴봤습니다.</span><span class="sxs-lookup"><span data-stu-id="515cb-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="515cb-168">Azure에서 PHP를 사용하는 방법에 대한 자세한 내용은 [PHP 개발자 센터](/develop/php/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="515cb-169">앱 서비스 웹앱으로 작업하는 방법에 대한 자세한 정보는 페이지의 왼쪽(넓은 브라우저 창의 경우) 또는 페이지의 위쪽(좁은 브라우저 창의 경우)에서 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="515cb-170">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="515cb-170">What's changed</span></span>
* <span data-ttu-id="515cb-171">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="515cb-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
