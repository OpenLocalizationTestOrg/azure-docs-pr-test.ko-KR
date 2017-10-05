---
title: "Azure에서 ASP.NET 웹앱 만들기 | Microsoft Docs"
description: "기본 ASP.NET 웹앱을 배포하여 Azure App Service에서 웹앱을 실행하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="db2b7-103">Azure에서 ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="db2b7-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="db2b7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="db2b7-105">이 빠른 시작은 첫 번째 ASP.NET 웹앱을 Azure Web Apps에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="db2b7-106">완료되면 배포된 웹 응용 프로그램으로 App Service 계획 및 Azure 웹앱으로 구성된 리소스 그룹을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="db2b7-107">비디오를 시청하여 이 빠른 시작이 실제로 작동하는 모습을 살펴본 후 단계에 따라 직접 첫 번째 .NET 앱을 Azure에 게시해 보세요.</span><span class="sxs-lookup"><span data-stu-id="db2b7-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="db2b7-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db2b7-108">Prerequisites</span></span>

<span data-ttu-id="db2b7-109">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-109">To complete this tutorial:</span></span>

* <span data-ttu-id="db2b7-110">다음 워크로드와 함께 [Visual Studio 2017](https://www.visualstudio.com/downloads/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="db2b7-111">**ASP.NET 및 웹 배포**</span><span class="sxs-lookup"><span data-stu-id="db2b7-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="db2b7-112">**Azure 개발**</span><span class="sxs-lookup"><span data-stu-id="db2b7-112">**Azure development**</span></span>

    ![ASP.NET 및 웹 개발 및 Azure 개발(웹 & 클라우드에서)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="db2b7-114">ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="db2b7-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="db2b7-115">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 선택하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="db2b7-116">**새 프로젝트** 대화 상자에서 **Visual C# > 웹 > ASP.NET 웹 응용 프로그램(.NET Framework)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="db2b7-117">응용 프로그램 이름을 _myFirstAzureWebApp_으로 지정한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![새 프로젝트 대화 상자](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="db2b7-119">모든 종류의 ASP.NET 웹앱을 Azure에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="db2b7-120">이 빠른 시작의 경우 **MVC** 템플릿을 선택하고 인증이 **인증 없음**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="db2b7-121">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-121">Select **OK**.</span></span>

![새 ASP.NET 프로젝트 대화 상자](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="db2b7-123">메뉴에서 **디버그 > 디버깅하지 않고 시작**을 선택하여 웹앱을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![로컬에서 앱 실행](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="db2b7-125">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="db2b7-125">Publish to Azure</span></span>

<span data-ttu-id="db2b7-126">**솔루션 탐색기**에서 **myFirstAzureWebApp** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![솔루션 탐색기에서 게시](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="db2b7-128">**Microsoft Azure App Service**를 선택했는지 확인하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![프로젝트 개요 페이지에서 게시](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="db2b7-130">그러면 **App Service 만들기** 대화 상자가 열리고 Azure에서 ASP.NET 웹앱을 실행하는 데 필요한 모든 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="db2b7-131">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="db2b7-131">Sign in to Azure</span></span>

<span data-ttu-id="db2b7-132">**App Service 만들기** 대화 상자에서 **계정 추가**를 선택하고 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="db2b7-133">이미 로그인한 경우 드롭다운에서 원하는 구독이 포함된 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="db2b7-134">이미 로그인한 경우 **만들기**를 선택하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="db2b7-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Azure에 로그인](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="db2b7-136">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="db2b7-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="db2b7-137">**리소스 그룹** 옆에 있는 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="db2b7-138">리소스 그룹의 이름을 **myResourceGroup**으로 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="db2b7-139">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="db2b7-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="db2b7-140">**App Service 계획** 옆에 있는 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="db2b7-141">**App Service 계획 구성** 대화 상자에서 스크린샷 다음에 나오는 테이블의 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![App Service 계획 만들기](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="db2b7-143">설정</span><span class="sxs-lookup"><span data-stu-id="db2b7-143">Setting</span></span> | <span data-ttu-id="db2b7-144">제안 값</span><span class="sxs-lookup"><span data-stu-id="db2b7-144">Suggested Value</span></span> | <span data-ttu-id="db2b7-145">설명</span><span class="sxs-lookup"><span data-stu-id="db2b7-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="db2b7-146">App Service 계획</span><span class="sxs-lookup"><span data-stu-id="db2b7-146">App Service Plan</span></span>| <span data-ttu-id="db2b7-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="db2b7-147">myAppServicePlan</span></span> | <span data-ttu-id="db2b7-148">App Service 계획의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="db2b7-149">위치</span><span class="sxs-lookup"><span data-stu-id="db2b7-149">Location</span></span> | <span data-ttu-id="db2b7-150">서유럽</span><span class="sxs-lookup"><span data-stu-id="db2b7-150">West Europe</span></span> | <span data-ttu-id="db2b7-151">웹앱이 호스팅된 데이터 센터입니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="db2b7-152">크기</span><span class="sxs-lookup"><span data-stu-id="db2b7-152">Size</span></span> | <span data-ttu-id="db2b7-153">무료</span><span class="sxs-lookup"><span data-stu-id="db2b7-153">Free</span></span> | <span data-ttu-id="db2b7-154">[가격 책정 계층](https://azure.microsoft.com/pricing/details/app-service/)은 호스팅 기능을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="db2b7-155">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="db2b7-156">웹앱 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="db2b7-156">Create and publish the web app</span></span>

<span data-ttu-id="db2b7-157">**웹앱 이름**에서 고유한 앱 이름(유효한 문자는 `a-z`, `0-9` 및 `-`)을 입력하거나 자동으로 생성된 고유한 이름을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="db2b7-158">웹앱의 URL은 `http://<app_name>.azurewebsites.net`이며, 여기서 `<app_name>`은 웹앱 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="db2b7-159">**만들기**를 선택하여 Azure 리소스 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-159">Select **Create** to start creating the Azure resources.</span></span>

![웹앱 이름 구성](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="db2b7-161">마법사가 완료되면 Azure에 ASP.NET 웹앱을 게시한 다음 기본 브라우저에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Azure에서 게시된 ASP.NET 웹앱](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="db2b7-163">[작성 및 게시 단계](#create-and-publish-the-web-app)에서 지정한 웹앱 이름이 `http://<app_name>.azurewebsites.net` 형식의 URL 접두사로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="db2b7-164">축하합니다. ASP.NET 웹앱이 Azure App Service에서 실시간으로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="db2b7-165">앱 업데이트 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="db2b7-165">Update the app and redeploy</span></span>

<span data-ttu-id="db2b7-166">**솔루션 탐색기**에서 _Views\Home\Index.cshtml_을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="db2b7-167">위쪽 가까이에 `<div class="jumbotron">` HTML 태그를 찾아서 전체 요소를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="db2b7-168">Azure에 다시 배포하려면 **솔루션 탐색기**에서 **myFirstAzureWebApp** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="db2b7-169">게시 페이지에서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="db2b7-170">게시가 완료되면 Visual Studio가 웹앱의 URL로 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Azure에서 업데이트된 ASP.NET 웹앱](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="db2b7-172">Azure 웹앱 관리</span><span class="sxs-lookup"><span data-stu-id="db2b7-172">Manage the Azure web app</span></span>

<span data-ttu-id="db2b7-173">웹앱을 관리하려면 <a href="https://portal.azure.com" target="_blank">Azure Portal</a>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="db2b7-174">왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="db2b7-176">웹앱의 개요 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-176">You see your web app's Overview page.</span></span> <span data-ttu-id="db2b7-177">여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure Portal의 App Service 블레이드](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="db2b7-179">왼쪽 메뉴는 앱 구성을 위한 서로 다른 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db2b7-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="db2b7-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db2b7-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db2b7-181">SQL Database를 사용하는 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db2b7-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
