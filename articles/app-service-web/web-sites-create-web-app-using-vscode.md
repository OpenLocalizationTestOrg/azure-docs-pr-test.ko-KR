---
title: "Visual Studio Code에서 ASP.NET Core 웹앱 만들기"
description: "이 자습서에서는 Visual Studio Code를 사용하여 ASP.NET Core 웹앱을 만드는 방법을 보여 줍니다."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="2a0c8-103">Visual Studio Code에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2a0c8-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="2a0c8-104">개요</span><span class="sxs-lookup"><span data-stu-id="2a0c8-104">Overview</span></span>
<span data-ttu-id="2a0c8-105">이 자습서에서는 [VS Code(Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode)를 사용하여 ASP.NET Core 웹앱을 만들어 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에 배포하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="2a0c8-106">이 문서는 웹앱을 참조하지만 API 앱 및 모바일 앱에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="2a0c8-107">ASP.NET Core에서는 ASP.NET을 완전히 다시 디자인했습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="2a0c8-108">ASP.NET Core는 .NET을 사용하여 최신 클라우드 기반 웹앱을 빌드하기 위한 새로운 오픈 소스 크로스 플랫폼 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="2a0c8-109">자세한 내용은 [ASP.NET Core 소개](http://docs.asp.net/latest/conceptual-overview/aspnet.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="2a0c8-110">Azure 앱 서비스 웹앱에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="2a0c8-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2a0c8-111">Prerequisites</span></span>
* <span data-ttu-id="2a0c8-112">[VS Code](http://code.visualstudio.com/Docs/setup)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="2a0c8-113">Git 설치 - [Chocolatey](https://chocolatey.org/packages/git) 또는 [git-scm.com](http://git-scm.com/downloads)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="2a0c8-114">Git를 처음 사용하는 경우 [git-scm.com](http://git-scm.com/downloads) 을 선택하고 **Windows 명령 프롬프트에서 Git 사용**옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="2a0c8-115">Git를 설치한 후 자습서의 뒤에 나오는 VS Code에서 커밋을 수행할 때 필요하므로 Git 사용자 이름과 전자 메일을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="2a0c8-116">ASP.NET Core 설치</span><span class="sxs-lookup"><span data-stu-id="2a0c8-116">Install ASP.NET Core</span></span>
<span data-ttu-id="2a0c8-117">ASP.NET Core는 OS X, Linux 및 Windows에서 실행되는 최신 클라우드 및 웹앱을 빌드하기 위한 린(lean) .NET 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="2a0c8-118">ASP.NET 5/DNX는 클라우드에 배포되거나 온-프레미스로 실행될 앱에 최적화된 개발 프레임워크를 제공하기 위해 처음부터 다시 제작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="2a0c8-119">오버헤드를 최소화하는 모듈식 구성 요소로 구성되므로 솔루션을 구성하는 동안 유연성이 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="2a0c8-120">이 자습서는 ASP.NET Core의 최신 개발 버전으로 응용 프로그램 빌드를 시작하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="2a0c8-121">다음은 Windows에 특정한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="2a0c8-122">OS X, Linux 및 Windows에 대한 설치 지침은 [ASP.NET Core 시작](https://docs.microsoft.com/aspnet/core/getting-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="2a0c8-123">OS X, Linux 및 Windows에 대한 자세한 설치 지침은 [ASP.NET Core 설치](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="2a0c8-124">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2a0c8-124">Create the web app</span></span>
<span data-ttu-id="2a0c8-125">이 섹션에서는 .NET CLI 도구를 사용하여 새 앱 ASP.NET 웹앱을 스캐폴드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="2a0c8-126">프로젝트 폴더를 만들고 앱을 스캐폴딩하려면 명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 생성기](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="2a0c8-128">필요한 NuGet 패키지를 복원하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="2a0c8-129">로컬로 웹앱 실행</span><span class="sxs-lookup"><span data-stu-id="2a0c8-129">Run the web app locally</span></span>
<span data-ttu-id="2a0c8-130">웹앱을 만들고 앱에 대한 모든 NuGet 패키지를 검색했으므로 이제 웹앱을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="2a0c8-131">앱 실행(`dotnet run` 명령은 만료되면 앱을 빌드합니다.):</span><span class="sxs-lookup"><span data-stu-id="2a0c8-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="2a0c8-132">브라우저를 열고 다음 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="2a0c8-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="2a0c8-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="2a0c8-134">웹앱의 기본 페이지가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-134">The default page of the web app will appear as follows.</span></span>
   
    ![브라우저의 로컬 웹앱](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="2a0c8-136">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-136">Close your browser.</span></span> <span data-ttu-id="2a0c8-137">**명령 창**에서 **Ctrl+C**를 눌러 응용 프로그램을 종료하고 **명령 창**을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="2a0c8-138">Azure 포털에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2a0c8-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="2a0c8-139">다음 단계에서는 Azure 포털에서 웹앱을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="2a0c8-140">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2a0c8-141">포털의 왼쪽 위에서 **새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="2a0c8-142">**웹앱 > 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-142">Click **Web Apps > Web App**.</span></span>
   
    ![Azure 새 웹앱](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="2a0c8-144">**이름**에 대한 값을 입력합니다(예: **SampleWebAppDemo**).</span><span class="sxs-lookup"><span data-stu-id="2a0c8-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="2a0c8-145">이 이름은 고유해야 하며 사용자가 이름을 입력할 때 포털에서 해당 이름을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="2a0c8-146">따라서 다른 값을 입력할 경우 이 자습서에 표시되는 각 **SampleWebAppDemo** 항목을 해당 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="2a0c8-147">기존 **앱 서비스 계획** 을 선택하거나 새 앱 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="2a0c8-148">새 계획을 만드는 경우 가격 책정 계층, 위치 및 기타 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="2a0c8-149">앱 서비스 계획에 대한 자세한 내용은 [Azure 앱 서비스 계획의 포괄 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure 새 웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="2a0c8-151">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-151">Click **Create**.</span></span>
   
    ![웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="2a0c8-153">새 웹앱에 Git 게시 사용</span><span class="sxs-lookup"><span data-stu-id="2a0c8-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="2a0c8-154">Git는 Azure 앱 서비스 웹앱을 배포하는 데 사용할 수 있는 분산된 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="2a0c8-155">웹앱에 대해 작성한 코드를 로컬 Git 리포지토리에 저장하고, 원격 리포지토리로 푸시하여 Azure에 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="2a0c8-156">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2a0c8-157">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-157">Click **Browse**.</span></span>
3. <span data-ttu-id="2a0c8-158">**웹앱** 을 클릭하여 Azure 구독과 연결된 웹앱의 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="2a0c8-159">이 자습서에서 만든 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="2a0c8-160">웹앱 블레이드에서 **설정** > **지속적인 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure 웹앱 호스트](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="2a0c8-162">**원본 선택 > 로컬 Git 리포지토리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="2a0c8-163">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-163">Click **OK**.</span></span>
   
    ![Azure 로컬 Git 리포지토리](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="2a0c8-165">이전에 웹앱 또는 다른 앱 서비스 앱을 게시하기 위해 배포 자격 증명을 설정하지 않은 경우 지금 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="2a0c8-166">**설정** > **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="2a0c8-167">**배포 자격 증명 설정** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="2a0c8-168">사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-168">Create a user name and password.</span></span>  <span data-ttu-id="2a0c8-169">나중에 Git를 설정할 때 이 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="2a0c8-170">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-170">Click **Save**.</span></span>
9. <span data-ttu-id="2a0c8-171">웹앱의 블레이드에서 **설정 > 속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="2a0c8-172">배포할 원격 Git 리포지토리의 URL이 **GIT URL**아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="2a0c8-173">이 자습서에서 나중에 사용할 **GIT URL** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="2a0c8-175">Azure 앱 서비스에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="2a0c8-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="2a0c8-176">이 섹션에서는 로컬 Git 리포지토리를 만들고 해당 리포지토리에서 Azure로 푸시하여 웹앱을 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="2a0c8-177">VS Code의 왼쪽 탐색 모음에서 **Git** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![VS Code의 Git 아이콘](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="2a0c8-179">**git 리포지토리 초기화** 를 선택하여 작업 공간이 git 소스 제어 아래에 오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Git 초기화](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="2a0c8-181">명령 창을 열고 디렉터리를 웹앱의 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="2a0c8-182">그런 후 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="2a0c8-183">이 명령은 CRLF 끝과 LF 끝이 사용된 텍스트에 대한 문제를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="2a0c8-184">VS Code에서 커밋 메시지를 추가하고 **모두 커밋** 확인 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Git 모두 커밋](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="2a0c8-186">Git 처리가 완료되면 **변경 내용**아래 Git 창에 나열된 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git 변경 내용 없음](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="2a0c8-188">명령 프롬프트가 웹앱이 위치한 디렉터리를 가리키는 명령 창으로 다시 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="2a0c8-189">앞에서 복사한 Git URL(“.git”로 종료됨)을 사용하여 웹앱에 업데이트를 푸시하기 위한 원격 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="2a0c8-190">자격 증명이 로컬로 저장되도록 Git을 구성하여 자격 증명이 VS 코드에서 생성된 푸시 명령에 자동으로 추가될 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="2a0c8-191">다음 명령을 입력하여 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="2a0c8-192">처음으로 Azure에 푸시한 후에는 VS 코드로부터 모든 푸시 명령을 수행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="2a0c8-193">Azure에서 이전에 만든 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="2a0c8-194">**참고: 암호는 표시되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="2a0c8-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="2a0c8-195">위 명령의 출력은 배포에 성공했다는 메시지로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="2a0c8-196">앱을 변경하면 **모두 커밋** 옵션을 선택한 다음 **푸시** 옵션을 선택하여 기본 Git 기능을 통해 VS 코드에서 직접 다시 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="2a0c8-197">**모두 커밋** 및 **새로 고침** 단추 옆에 있는 드롭다운 메뉴에서 **푸시** 옵션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="2a0c8-198">공동 작업해야 하는 프로젝트의 경우에는 Azure로의 푸시 사이에 GitHub으로의 푸시도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="2a0c8-199">Azure에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="2a0c8-199">Run the app in Azure</span></span>
<span data-ttu-id="2a0c8-200">웹앱을 배포했으므로 이제 Azure에서 호스트된 상태에서 앱을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="2a0c8-201">이 작업은 두 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-201">This can be done in two ways:</span></span>

* <span data-ttu-id="2a0c8-202">브라우저를 열고 웹앱의 이름을 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="2a0c8-203">Azure 포털에서 웹앱에 대한 웹앱 블레이드를 찾은 다음 기본 브라우저에서 **찾아보기** 를 클릭하여</span><span class="sxs-lookup"><span data-stu-id="2a0c8-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="2a0c8-204">앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-204">in your default browser.</span></span>

![Azure 웹앱](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="2a0c8-206">요약</span><span class="sxs-lookup"><span data-stu-id="2a0c8-206">Summary</span></span>
<span data-ttu-id="2a0c8-207">이 자습서에서는 VS Code에서 웹앱을 만들고 Azure에 배포하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="2a0c8-208">VS Code에 대한 자세한 내용은 [Visual Studio Code를 선택해야 하는 이유?](https://code.visualstudio.com/Docs/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="2a0c8-209">App Service Web Apps에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a0c8-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

