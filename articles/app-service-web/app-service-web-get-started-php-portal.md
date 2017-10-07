---
title: "hello 5 분 후에 Azure 포털에서에서 WordPress 앱 aaaDeploy | Microsoft Docs"
description: "얼마나 쉬운지 앱 서비스에서 toorun 웹 응용 프로그램을 WordPress 응용 프로그램을 배포 하 여에 대해 알아봅니다. 결과를 즉시 확인합니다."
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
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="7e9be-104">5 분 내에 hello Azure 포털에서에서 WordPress 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7e9be-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="7e9be-105">이 자습서에서는 어떻게 toodeploy 첫 번째 [WordPress](https://wordpress.org/) 웹 앱에 너무[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) (분)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress 사이트](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="7e9be-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7e9be-107">Prerequisites</span></span>
<span data-ttu-id="7e9be-108">Microsoft Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="7e9be-109">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="7e9be-110">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="7e9be-111">시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="7e9be-112">Hello WordPress 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7e9be-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="7e9be-113">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7e9be-114">[https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="7e9be-115">이 링크는 바로 가기 tooimmediately hello Azure 포털에서에서 새 WordPress 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="7e9be-116">**앱 이름**에 웹앱 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="7e9be-117">Hello 이름이 hello에 고유한 경우 hello 상자에서 녹색 확인 표시가 나타납니다 `azurewebsites.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="7e9be-118">**리소스 그룹**, 클릭 **새로 만들기** 새 toocreate [리소스 그룹](../azure-resource-manager/resource-group-overview.md), 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="7e9be-119">**데이터베이스 공급자**에서 **CleaDB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="7e9be-120">**App Service 계획/위치** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="7e9be-121">Hello 구성 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="7e9be-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="7e9be-122">**앱 서비스 계획**, 형식 hello 원하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="7e9be-123">**위치**, 위치 toohost 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="7e9be-124">**가격 책정 계층**을 클릭한 다음 **F1 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="7e9be-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-125">Click **OK**.</span></span>

8. <span data-ttu-id="7e9be-126">**데이터베이스** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="7e9be-127">표시 된 것 처럼 hello SQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="7e9be-128">**데이터베이스 이름**에 데이터베이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="7e9be-129">**위치**, 선택 hello 앱 서비스 계획 hello와 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="7e9be-130">**가격 책정 계층**을 클릭한 다음 **수성** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="7e9be-131">**약관**을 선택하고 **구입**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="7e9be-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-132">Click **OK**.</span></span>

9. <span data-ttu-id="7e9be-133">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-133">Click **Create**.</span></span>

    <span data-ttu-id="7e9be-134">WordPress 앱이 Azure에서 구성에 따라 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="7e9be-135">**배포를 시작했습니다.** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-135">You should see a **Deployment started...** notification.</span></span>

    ![배포가 시작됨 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="7e9be-137">WordPress 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="7e9be-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="7e9be-138">Azure에서 앱 배포가 완료되면 다른 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-138">When Azure completes app deployment you see another notification.</span></span>

![배포가 완료됨 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="7e9be-140">Hello 알림을 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7e9be-140">Click hello notification.</span></span> <span data-ttu-id="7e9be-141">이 누락 하는 경우 항상 액세스할 수 hello 알림 벨을 클릭 하 여 (![알림 아래-Azure 앱 서비스의 첫 번째 WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="7e9be-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="7e9be-142">이제 웹앱의 관리 [블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)(*블레이드*: 가로로 열리는 포털 페이지)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="7e9be-143">Hello hello 개요 페이지의 위쪽에 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![찾아보기 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="7e9be-145">이제 hello WordPress 표시 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7e9be-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="7e9be-146">Hello WordPress 설치를 구성 하 고 함께 재생 시작!</span><span class="sxs-lookup"><span data-stu-id="7e9be-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![WordPress 구성 - Azure App Service의 첫 번째 WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="7e9be-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e9be-148">Next steps</span></span>
* <span data-ttu-id="7e9be-149">[만들기, 구성 및 배포 Laravel 웹 응용 프로그램 tooAzure](app-service-web-php-get-started.md) -toorun Azure에서 PHP 웹 응용 프로그램 같은 필요 hello 기본 기술을 익힙니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="7e9be-150">PowerShell/Bash로부터 Azure의 앱을 만들어 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="7e9be-151">PHP 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-151">Set PHP version.</span></span>
    * <span data-ttu-id="7e9be-152">Hello 루트 응용 프로그램 디렉터리에 있지 않은 시작 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="7e9be-153">Composer 자동화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="7e9be-154">특정 환경 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="7e9be-155">일반적인 오류 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="7e9be-156">[프로그램 코드 tooAzure 앱 서비스 배포](web-sites-deploy.md)-FTP 또는 원본을 toodeploy 저장소를 제어 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="7e9be-157">[추가 기능 tooyour 첫 번째 웹 응용 프로그램](app-service-web-get-started-2.md) -걸릴 Azure 앱 toohello 다음 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="7e9be-158">사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-158">Authenticate your users.</span></span> <span data-ttu-id="7e9be-159">요구에 따라 규모를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-159">Scale it based on demand.</span></span> <span data-ttu-id="7e9be-160">몇 가지 성능 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-160">Set up some performance alerts.</span></span> <span data-ttu-id="7e9be-161">이 모든 작업이 클릭 몇 번으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7e9be-161">All with a few clicks.</span></span>
