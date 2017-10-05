---
title: "WordPress 앱을 Azure Portal에 5분 안에 배포 | Microsoft Docs"
description: "WordPress 앱을 배포하여 App Service에서 웹앱을 간편하게 실행하는 방법을 알아봅니다. 결과를 즉시 확인합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="0d5a1-104">WordPress 앱을 Azure Portal에 5분 안에 배포</span><span class="sxs-lookup"><span data-stu-id="0d5a1-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="0d5a1-105">이 자습서에서는 첫 번째 [WordPress](https://wordpress.org/) 웹앱을 몇 분 내에 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress 사이트](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="0d5a1-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0d5a1-107">Prerequisites</span></span>
<span data-ttu-id="0d5a1-108">Microsoft Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="0d5a1-109">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="0d5a1-110">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="0d5a1-111">시작 앱을 만들고 최대 한 시간 동안 해당 앱을 사용하여 재생합니다. -- 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="0d5a1-112">WordPress 앱 배포</span><span class="sxs-lookup"><span data-stu-id="0d5a1-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="0d5a1-113">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0d5a1-114">[https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="0d5a1-115">이 링크는 새 WordPress 앱을 Azure Portal에서 즉시 구성할 수 있는 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="0d5a1-116">**앱 이름**에 웹앱 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="0d5a1-117">이름이 `azurewebsites.net` 도메인에서 고유하면 녹색 확인 표시가 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="0d5a1-118">**리소스 그룹**에서 **새로 만들기**를 클릭하여 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만든 다음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="0d5a1-119">**데이터베이스 공급자**에서 **CleaDB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="0d5a1-120">**App Service 계획/위치** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="0d5a1-121">[App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="0d5a1-122">**App Service 계획**에 원하는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="0d5a1-123">**위치**에서 계획을 호스트할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="0d5a1-124">**가격 책정 계층**을 클릭한 다음 **F1 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="0d5a1-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-125">Click **OK**.</span></span>

8. <span data-ttu-id="0d5a1-126">**데이터베이스** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="0d5a1-127">SQL Database를 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="0d5a1-128">**데이터베이스 이름**에 데이터베이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="0d5a1-129">**위치**에서 App Service 계획과 같은 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="0d5a1-130">**가격 책정 계층**을 클릭한 다음 **수성** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="0d5a1-131">**약관**을 선택하고 **구입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="0d5a1-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-132">Click **OK**.</span></span>

9. <span data-ttu-id="0d5a1-133">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-133">Click **Create**.</span></span>

    <span data-ttu-id="0d5a1-134">WordPress 앱이 Azure에서 구성에 따라 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="0d5a1-135">**배포를 시작했습니다.** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-135">You should see a **Deployment started...** notification.</span></span>

    ![배포가 시작됨 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="0d5a1-137">WordPress 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="0d5a1-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="0d5a1-138">Azure에서 앱 배포가 완료되면 다른 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-138">When Azure completes app deployment you see another notification.</span></span>

![배포가 완료됨 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="0d5a1-140">알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-140">Click the notification.</span></span> <span data-ttu-id="0d5a1-141">알림을 놓친 경우 알림 벨(![알림 벨 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png))을 클릭하면 알림에 언제든 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="0d5a1-142">이제 웹앱의 관리 [블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)(*블레이드*: 가로로 열리는 포털 페이지)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="0d5a1-143">개요 페이지의 맨 위에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![찾아보기 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="0d5a1-145">이제 WordPress **시작** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="0d5a1-146">WordPress 설치를 구성하고 사용을 시작하세요!</span><span class="sxs-lookup"><span data-stu-id="0d5a1-146">Configure the WordPress installation and start playing with it!</span></span>

    ![WordPress 구성 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="0d5a1-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d5a1-148">Next steps</span></span>
* <span data-ttu-id="0d5a1-149">[Azure에 Laravel 웹앱을 만들고 구성하여 배포](app-service-web-php-get-started.md) - Azure에서 PHP 웹앱을 실행하는 데 필요한 다음과 같은 기본 기술을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="0d5a1-150">PowerShell/Bash로부터 Azure의 앱을 만들어 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="0d5a1-151">PHP 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-151">Set PHP version.</span></span>
    * <span data-ttu-id="0d5a1-152">루트 응용 프로그램 디렉터리에 있지 않은 시작 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="0d5a1-153">Composer 자동화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="0d5a1-154">특정 환경 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="0d5a1-155">일반적인 오류 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="0d5a1-156">[Azure App Service에 코드 배포](web-sites-deploy.md)- FTP 또는 소스 제어 리포지토리에서 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="0d5a1-157">[첫 번째 웹앱에 기능 추가](app-service-web-get-started-2.md) - Azure 앱을 한 단계 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="0d5a1-158">사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-158">Authenticate your users.</span></span> <span data-ttu-id="0d5a1-159">요구에 따라 규모를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-159">Scale it based on demand.</span></span> <span data-ttu-id="0d5a1-160">몇 가지 성능 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-160">Set up some performance alerts.</span></span> <span data-ttu-id="0d5a1-161">이 모든 작업이 클릭 몇 번으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0d5a1-161">All with a few clicks.</span></span>
