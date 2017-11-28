---
title: "hello 5 분 후에 Azure 포털에서에서 Umbraco 웹 앱 aaaDeploy | Microsoft Docs"
description: "얼마나 쉬운지 앱 서비스에서 toorun 웹 앱 샘플 ASP.NET 응용 프로그램을 배포 하 여에 대해 알아봅니다. 결과를 즉시 확인합니다."
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
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="f1b14-104">5 분 내에 hello Azure 포털에서에서 Umbraco 웹 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="f1b14-105">이 자습서를 통해 배포 n [Umbraco](https://our.umbraco.org/) 웹 앱에 너무[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) (분)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco 앱](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="f1b14-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f1b14-107">Prerequisites</span></span>
<span data-ttu-id="f1b14-108">Microsoft Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="f1b14-109">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="f1b14-110">Azure 계정 없이 [App Service를 체험](https://azure.microsoft.com/try/app-service/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="f1b14-111">시작 응용 프로그램 만들기 및 신용 카드가 필요 없는, 없음의 노력과 헌신 함께 tooan 시간-를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="f1b14-112">Hello ASP.NET 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f1b14-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="f1b14-113">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f1b14-114">[https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="f1b14-115">이 링크는 바로 가기 tooimmediately hello Azure 포털에서에서 새 Umbraco 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="f1b14-116">**앱 이름**에 웹앱 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="f1b14-117">Hello 이름이 hello에 고유한 경우 hello 상자에서 녹색 확인 표시가 나타납니다 `azurewebsites.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="f1b14-118">**리소스 그룹**, 클릭 **새로 만들기** 새 toocreate [리소스 그룹](../azure-resource-manager/resource-group-overview.md), 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="f1b14-119">**App Service 계획/위치** > **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="f1b14-120">Hello 구성 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="f1b14-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="f1b14-121">**앱 서비스 계획**, 형식 hello 원하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="f1b14-122">**위치**, 위치 toohost 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="f1b14-123">**가격 책정 계층**을 클릭한 다음 **F1 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f1b14-124">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-124">Click **OK**.</span></span>

    <span data-ttu-id="f1b14-125">Umbraco CMS 구성 같아야 스크린 샷 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="f1b14-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![구성 진행 중 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="f1b14-127">**SQL Database** > **새 데이터베이스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="f1b14-128">표시 된 것 처럼 hello SQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="f1b14-129">**이름**에 이름(예: **myDB**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="f1b14-130">**가격 책정 계층**을 클릭한 다음 **F 무료** 또는 다른 적합한 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f1b14-131">**대상 서버** > **새 서버 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="f1b14-132">표시 된 것 처럼 hello 데이터베이스 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="f1b14-133">**서버 이름**에 서버 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="f1b14-134">Hello 이름이 hello에 고유한 경우 hello 상자에서 녹색 확인 표시가 나타납니다 `.database.windows.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="f1b14-135">**서버 관리자 로그인**, 형식 hello 원하는 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="f1b14-136">**암호** 및 **암호 확인**, hello 원하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="f1b14-137">위치 선택 hello 웹 앱에 사용할 동일한 위치를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="f1b14-138">확인 **허용 azure 서비스 tooaccess 서버** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="f1b14-139">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="f1b14-140">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-140">Click **Select**.</span></span>

13. <span data-ttu-id="f1b14-141">클릭 **웹 앱 설정**hello 데이터베이스 사용자 이름 및 암호를 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="f1b14-142">Umbraco CMS 구성 같아야 스크린 샷 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="f1b14-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![구성 완료 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="f1b14-144">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-144">Click **Create**.</span></span>
    
    <span data-ttu-id="f1b14-145">Umbraco 앱이 Azure에서 구성에 따라 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="f1b14-146">**배포를 시작했습니다.** 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-146">You should see a **Deployment started...** notification.</span></span>

    ![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="f1b14-148">Umrbaco 웹앱 시작 및 관리</span><span class="sxs-lookup"><span data-stu-id="f1b14-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="f1b14-149">Azure에서 앱 배포가 완료되면 다른 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-149">When Azure completes app deployment you see another notification.</span></span>

![배포 성공 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="f1b14-151">Hello 알림을 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f1b14-151">Click hello notification.</span></span> <span data-ttu-id="f1b14-152">이 누락 하는 경우 항상 액세스할 수 hello 알림 벨을 클릭 하 여 (![알림 아래-Azure 앱 서비스의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="f1b14-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="f1b14-153">이제 웹앱의 관리 [블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)(*블레이드*: 가로로 열리는 포털 페이지)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="f1b14-154">Hello hello 개요 페이지의 위쪽에 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![찾아보기 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="f1b14-156">이제 hello Umbraco 표시 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="f1b14-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="f1b14-157">Hello Umbraco 설치를 구성 하 고 함께 재생 시작!</span><span class="sxs-lookup"><span data-stu-id="f1b14-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Umbraco 구성 - Azure App Service의 첫 번째 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="f1b14-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1b14-159">Next steps</span></span>
* <span data-ttu-id="f1b14-160">[ASP.NET 웹 응용 프로그램 tooAzure Visual Studio를 사용 하 여 응용 프로그램 서비스를 배포](app-service-web-get-started-dotnet.md) -toocreate hello 중 하나를 사용 하 여 Visual Studio에서 새 Azure 웹 앱에서 응용 프로그램 템플릿을 포함 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="f1b14-161">[프로그램 코드 tooAzure 앱 서비스 배포](web-sites-deploy.md)-FTP 또는 원본을 toodeploy 저장소를 제어 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="f1b14-162">[추가 기능 tooyour 첫 번째 웹 응용 프로그램](app-service-web-get-started-2.md) -걸릴 Azure 앱 toohello 다음 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="f1b14-163">사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-163">Authenticate your users.</span></span> <span data-ttu-id="f1b14-164">요구에 따라 규모를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-164">Scale it based on demand.</span></span> <span data-ttu-id="f1b14-165">몇 가지 성능 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-165">Set up some performance alerts.</span></span> <span data-ttu-id="f1b14-166">이 모든 작업이 클릭 몇 번으로 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b14-166">All with a few clicks.</span></span>
