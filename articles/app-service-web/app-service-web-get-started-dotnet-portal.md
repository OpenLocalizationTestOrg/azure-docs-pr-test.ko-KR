---
title: "Umbraco 웹앱을 Azure Portal에 5분 안에 배포 | Microsoft Docs"
description: "샘플 ASP.NET 앱을 배포하여 App Service에서 웹앱을 실행하는 작업이 얼마나 쉬운지 알아봅니다. 결과를 즉시 확인합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="5395a-104">Umbraco 웹앱을 Azure Portal에 5분 안에 배포</span><span class="sxs-lookup"><span data-stu-id="5395a-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="5395a-105">이 자습서는 [Umbraco](https://our.umbraco.org/) 웹앱을 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에 몇 분 이내에 배포하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco 앱](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="5395a-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5395a-107">Prerequisites</span></span>
<span data-ttu-id="5395a-108">Microsoft Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="5395a-109">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="5395a-110">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="5395a-111">시작 앱을 만들고 최대 한 시간 동안 해당 앱을 사용하여 재생합니다. -- 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="5395a-112">ASP.NET 앱 배포</span><span class="sxs-lookup"><span data-stu-id="5395a-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="5395a-113">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5395a-114">[https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="5395a-115">이 링크는 새 Umbraco 앱을 Azure Portal에서 즉시 구성할 수 있는 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="5395a-116">**앱 이름**에 웹앱 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="5395a-117">이름이 `azurewebsites.net` 도메인에서 고유하면 녹색 확인 표시가 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="5395a-118">**리소스 그룹**에서 **새로 만들기**를 클릭하여 새 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 만든 다음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="5395a-119">**App Service 계획/위치** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="5395a-120">[App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="5395a-121">**App Service 계획**에 원하는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="5395a-122">**위치**에서 계획을 호스트할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="5395a-123">**가격 책정 계층**을 클릭한 다음 **F1 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="5395a-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-124">Click **OK**.</span></span>

    <span data-ttu-id="5395a-125">Umbraco CMS 구성이 다음 스크린샷과 같은 모양으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![구성 진행 중 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="5395a-127">**SQL Database** > **새 데이터베이스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="5395a-128">SQL Database를 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="5395a-129">**이름**에 이름(예: **myDB**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="5395a-130">**가격 책정 계층**을 클릭한 다음 **F 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="5395a-131">**대상 서버** > **새 서버 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="5395a-132">데이터베이스 서버를 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="5395a-133">**서버 이름**에 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="5395a-134">이름이 `.database.windows.net` 도메인에서 고유하면 녹색 확인 표시가 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="5395a-135">**서버 관리자 로그인**에 원하는 관리자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="5395a-136">**암호** 및 **암호 확인**에 원하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="5395a-137">위치에서 웹앱에 사용한 것과 같은 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="5395a-138">**Azure 서비스의 서버 액세스 허용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="5395a-139">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="5395a-140">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-140">Click **Select**.</span></span>

13. <span data-ttu-id="5395a-141">**웹앱 설정**을 클릭하고 데이터베이스 사용자 이름 및 암호를 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="5395a-142">Umbraco CMS 구성이 다음 스크린샷과 같은 모양으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![구성 완료 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="5395a-144">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-144">Click **Create**.</span></span>
    
    <span data-ttu-id="5395a-145">Umbraco 앱이 Azure에서 구성에 따라 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="5395a-146">**배포를 시작했습니다.** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-146">You should see a **Deployment started...** notification.</span></span>

    ![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="5395a-148">Umrbaco 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="5395a-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="5395a-149">Azure에서 앱 배포가 완료되면 다른 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-149">When Azure completes app deployment you see another notification.</span></span>

![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="5395a-151">알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-151">Click the notification.</span></span> <span data-ttu-id="5395a-152">알림을 놓친 경우 알림 벨(![알림 벨 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png))을 클릭하면 알림에 언제든 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="5395a-153">이제 웹앱의 관리 [블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)(*블레이드*: 가로로 열리는 포털 페이지)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="5395a-154">개요 페이지의 맨 위에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![찾아보기 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="5395a-156">이제 Umbraco **시작** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="5395a-157">Umbraco 설치를 구성하고 사용을 시작하세요!</span><span class="sxs-lookup"><span data-stu-id="5395a-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Umbraco 구성 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="5395a-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5395a-159">Next steps</span></span>
* <span data-ttu-id="5395a-160">[Visual Studio를 사용하여 ASP.NET 웹앱을 Azure App Service에 배포](app-service-web-get-started-dotnet.md) - 포함된 응용 프로그램 템플릿 중 하나를 사용하여 Visual Studio에서 Azure 웹앱을 새로 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="5395a-161">[Azure App Service에 코드 배포](web-sites-deploy.md)- FTP 또는 소스 제어 리포지토리에서 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="5395a-162">[첫 번째 웹앱에 기능 추가](app-service-web-get-started-2.md) - Azure 앱을 한 단계 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="5395a-163">사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-163">Authenticate your users.</span></span> <span data-ttu-id="5395a-164">요구에 따라 규모를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-164">Scale it based on demand.</span></span> <span data-ttu-id="5395a-165">몇 가지 성능 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-165">Set up some performance alerts.</span></span> <span data-ttu-id="5395a-166">이 모든 작업이 클릭 몇 번으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5395a-166">All with a few clicks.</span></span>
