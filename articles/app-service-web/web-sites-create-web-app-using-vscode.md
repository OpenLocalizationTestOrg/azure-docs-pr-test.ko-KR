---
title: "Visual Studio Code에서 ASP.NET Core 웹 앱 aaaCreate"
description: "이 자습서에서는 toocreate ASP.NET Core 웹 앱 Visual Studio 코드를 사용 하 여 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="54e31-103">Visual Studio Code에서 ASP.NET Core 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="54e31-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="54e31-104">개요</span><span class="sxs-lookup"><span data-stu-id="54e31-104">Overview</span></span>
<span data-ttu-id="54e31-105">이 자습서에서는 어떻게 toocreate ASP.NET Core 웹 앱에서 사용 하 여 [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) 너무 배포[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="54e31-106">이 문서에서는 tooweb 앱, 있지만 tooAPI 앱 및 모바일 앱도 적용.</span><span class="sxs-lookup"><span data-stu-id="54e31-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="54e31-107">ASP.NET Core에서는 ASP.NET을 완전히 다시 디자인했습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="54e31-108">ASP.NET Core는 .NET을 사용하여 최신 클라우드 기반 웹앱을 빌드하기 위한 새로운 오픈 소스 크로스 플랫폼 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="54e31-109">자세한 내용은 참조 [소개 tooASP.NET 코어](http://docs.asp.net/latest/conceptual-overview/aspnet.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="54e31-110">Azure 앱 서비스 웹앱에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54e31-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="54e31-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54e31-111">Prerequisites</span></span>
* <span data-ttu-id="54e31-112">[VS Code](http://code.visualstudio.com/Docs/setup)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="54e31-113">Git 설치 - [Chocolatey](https://chocolatey.org/packages/git) 또는 [git-scm.com](http://git-scm.com/downloads)에서 설치할 수 있습니다. 새 tooGit 인 경우 선택 [git scm.com](http://git-scm.com/downloads) 너무 hello 옵션을 선택 하 고**hello Windows 명령 프롬프트에서에서 Git 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="54e31-114">Git를 설치한 다음도 해야 tooset hello Git 사용자 이름 및 전자 메일 (VS Code에서 커밋이 수행 중) 하는 경우 hello 자습서의 뒷부분에서 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="54e31-115">ASP.NET Core 설치</span><span class="sxs-lookup"><span data-stu-id="54e31-115">Install ASP.NET Core</span></span>
<span data-ttu-id="54e31-116">ASP.NET Core는 OS X, Linux 및 Windows에서 실행되는 최신 클라우드 및 웹앱을 빌드하기 위한 린(lean) .NET 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="54e31-117">것에서 작성 된 hello tooprovide를 접지 하거나 배포 된 toohello 클라우드 또는 온-프레미스를 실행 하는 앱에 대 한 최적화 된 개발 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="54e31-118">오버헤드를 최소화하는 모듈식 구성 요소로 구성되므로 솔루션을 구성하는 동안 유연성이 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="54e31-119">이 자습서는 디자인 된 tooget hello 최신 개발 버전의 ASP.NET Core 응용 프로그램 작성을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="54e31-120">hello 지침에 따라 특정 tooWindows 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="54e31-121">OS X, Linux 및 Windows에 대한 설치 지침은 [ASP.NET Core 시작](https://docs.microsoft.com/aspnet/core/getting-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54e31-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="54e31-122">OS X, Linux 및 Windows에 대한 자세한 설치 지침은 [ASP.NET Core 설치](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54e31-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="54e31-123">Hello 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="54e31-123">Create hello web app</span></span>
<span data-ttu-id="54e31-124">이 섹션에서는 tooscaffold는 새 응용 프로그램의 ASP.NET 웹 앱 hello.NET CLI 도구를 사용 하 여 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="54e31-125">Hello 명령 프롬프트 toocreate hello 프로젝트 폴더와 스 캐 폴드 hello 앱에서 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![dotnet CLI - ASP.NET Core 생성기](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="54e31-127">toorestore hello 필요한 NuGet 패키지를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="54e31-128">Hello 웹 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="54e31-128">Run hello web app locally</span></span>
<span data-ttu-id="54e31-129">Hello 웹 앱을 생성 하 고 hello 앱에 대 한 모든 hello NuGet 패키지를 검색 했으므로 hello 웹 응용 프로그램을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="54e31-130">Hello 응용 프로그램을 실행 (hello `dotnet run` 만료 될 때 명령이 hello 앱 빌드할):</span><span class="sxs-lookup"><span data-stu-id="54e31-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="54e31-131">브라우저를 열고 url toohello 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="54e31-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="54e31-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="54e31-133">hello 웹 응용 프로그램의 기본 페이지가 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![브라우저의 로컬 웹앱](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="54e31-135">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-135">Close your browser.</span></span> <span data-ttu-id="54e31-136">Hello에 **명령 창**, 키를 눌러 **Ctrl + C** hello 응용 프로그램 및 닫기 hello tooshut **명령 창**합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="54e31-137">Hello Azure 포털에서에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="54e31-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="54e31-138">hello 다음 단계는 안내 있습니다 hello Azure 포털에서에서 웹 앱을 만드는.</span><span class="sxs-lookup"><span data-stu-id="54e31-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="54e31-139">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54e31-140">클릭 **새로** hello에 hello 포털의 왼쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="54e31-141">**웹앱 > 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-141">Click **Web Apps > Web App**.</span></span>
   
    ![Azure 새 웹앱](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="54e31-143">**이름**에 대한 값을 입력합니다(예: **SampleWebAppDemo**).</span><span class="sxs-lookup"><span data-stu-id="54e31-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="54e31-144">Note이 이름은 고유 toobe 필요 하 고 hello 포털 tooenter hello 이름 할 때를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="54e31-145">따라서 입력 하 여 다른 값을 선택 해야 toosubstitute 해당 값을 각 **SampleWebAppDemo** 이 자습서에서 볼 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="54e31-146">기존 **앱 서비스 계획** 을 선택하거나 새 앱 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="54e31-147">새 계획을 만들면 hello 가격 책정 계층, 위치 및 기타 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="54e31-148">앱 서비스 계획에 대 한 자세한 내용은 hello 문서 참조 [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Azure 새 웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="54e31-150">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-150">Click **Create**.</span></span>
   
    ![웹앱 블레이드](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="54e31-152">Hello 새 웹 앱에 대 한 Git 게시를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="54e31-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="54e31-153">Git는 사용할 수 있는 toodeploy Azure 앱 서비스 웹 앱 분산된 버전 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="54e31-154">Hello 코드 로컬 Git 리포지토리에서 웹 앱에 대 한 쓰기 저장할 및 tooa 원격 리포지토리에 푸시하여 코드 tooAzure를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="54e31-155">Hello에 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54e31-156">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-156">Click **Browse**.</span></span>
3. <span data-ttu-id="54e31-157">클릭 **웹 앱** tooview Azure 구독에 연결 된 hello 웹 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="54e31-158">이 자습서에서 만든 hello 웹 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="54e31-159">Hello 웹 앱 블레이드 클릭 **설정** > **연속 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Azure 웹앱 호스트](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="54e31-161">**원본 선택 > 로컬 Git 리포지토리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="54e31-162">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-162">Click **OK**.</span></span>
   
    ![Azure 로컬 Git 리포지토리](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="54e31-164">이전에 웹앱 또는 다른 앱 서비스 앱을 게시하기 위해 배포 자격 증명을 설정하지 않은 경우 지금 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="54e31-165">**설정** > **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="54e31-166">hello **배포 자격 증명 설정** 블레이드를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="54e31-167">사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-167">Create a user name and password.</span></span>  <span data-ttu-id="54e31-168">나중에 Git를 설정할 때 이 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="54e31-169">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-169">Click **Save**.</span></span>
9. <span data-ttu-id="54e31-170">웹앱의 블레이드에서 **설정 > 속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="54e31-171">아래에 표시 된 toois를 배포 하는 hello 원격 Git 리포지토리의 hello URL **GIT URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="54e31-172">복사 hello **GIT URL** hello 자습서에서 나중에 사용할 값입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Azure Git URL](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="54e31-174">웹 앱 tooAzure 앱 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="54e31-175">이 섹션에서는 로컬 Git 리포지토리를 만들 쿼리하고 해당 리포지토리 tooAzure toodeploy에서 웹 앱 tooAzure 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="54e31-176">VS Code 선택 hello **Git** hello 왼쪽된 탐색 모음에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![VS Code의 Git 아이콘](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="54e31-178">선택 **Initialize git 리포지토리** toomake 있는지 작업 영역은 git 소스 제어입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Git 초기화](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="54e31-180">Hello 명령 창을 열고 웹 응용 프로그램의 디렉터리 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="54e31-181">그런 다음 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="54e31-182">이 명령은 CRLF 끝과 LF 끝이 사용된 텍스트에 대한 문제를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="54e31-183">VS Code에서 커밋 메시지를 추가 하 고 hello 클릭 **커밋 모든** 아이콘을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Git 모두 커밋](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="54e31-185">Hello Git 창 아래에 나열 된 파일이 없는 참조 Git 처리가 완료 되 면 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git 변경 내용 없음](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="54e31-187">뒤로 toohello 웹 앱 위치한 명령 창 위치 hello 명령 프롬프트 가리키는 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="54e31-188">Hello 앞에서 복사한 Git URL (끝에 ".git")를 사용 하 여 업데이트 tooyour 웹 응용 프로그램을 푸시하여에 대 한 원격 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="54e31-189">VS Code에서 생성 된 자동으로 추가 된 tooyour push 명령이 수 있도록 로컬 Git toosave 자격 증명를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="54e31-190">Hello 다음 명령을 입력 하 여 변경 내용을 tooAzure 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="54e31-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="54e31-191">이 초기 푸시 tooAzure 후 VS Code에서 모든 hello 푸시 명령 수 toodo 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="54e31-192">Azure에서 만든 hello 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="54e31-193">**참고: 암호는 표시되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="54e31-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="54e31-194">hello 출력 명령 위에 hello에서 성공적으로 배포 되었는지 메시지와 함께 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="54e31-195">Git 기능을 기본적으로 hello를 사용 하 여 hello를 선택 하 여 VS 코드에 직접 다시 게시할 수 변경 tooyour 응용 프로그램을 만들면 **모든 커밋** hello 옵션 뒤 **푸시** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="54e31-196">Hello 있습니다 **푸시** hello 드롭 다운 메뉴 다음 toohello에서 사용할 수 있는 옵션 **모든 커밋** 및 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="54e31-197">Toocollaborate 프로젝트에서 필요한 경우 tooAzure 푸시하여 사이 tooGitHub 푸시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="54e31-198">Azure의 hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="54e31-198">Run hello app in Azure</span></span>
<span data-ttu-id="54e31-199">웹 앱을 배포한 했으므로 hello 앱 Azure에서 호스트 하는 동안를 실행 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="54e31-200">이 작업은 두 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-200">This can be done in two ways:</span></span>

* <span data-ttu-id="54e31-201">브라우저를 열고 다음과 같이 웹 응용 프로그램의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="54e31-202">에 Azure 포털 hello 웹 앱에 대 한 웹 앱 블레이드 hello을 찾아서 클릭 **찾아보기** tooview 앱</span><span class="sxs-lookup"><span data-stu-id="54e31-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="54e31-203">앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-203">in your default browser.</span></span>

![Azure 웹앱](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="54e31-205">요약</span><span class="sxs-lookup"><span data-stu-id="54e31-205">Summary</span></span>
<span data-ttu-id="54e31-206">이 자습서에서는 방법에 대해 배웠습니다 toocreate VS Code의 웹 앱 및 tooAzure 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="54e31-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="54e31-207">VS Code에 대 한 자세한 내용은 hello 문서 참조 [Visual Studio Code 이유?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="54e31-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="54e31-208">App Service Web Apps에 대한 자세한 내용은 [웹앱 개요](app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54e31-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

