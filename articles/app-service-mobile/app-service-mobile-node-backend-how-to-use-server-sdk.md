---
title: "Mobile Apps용 Node.js 백 엔드 서버 SDK를 사용하는 방법 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱용 Node.js 백 엔드 서버 SDK를 사용하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="b4dcb-103">Azure 모바일 앱 Node.js SDK를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b4dcb-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="b4dcb-104">이 문서에서는 Azure 앱 서비스 모바일 앱에서 Node.js 백 엔드로 작업하는 방법을 보여주는 자세한 정보와 예를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="b4dcb-105"><a name="Introduction"></a>소개</span><span class="sxs-lookup"><span data-stu-id="b4dcb-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="b4dcb-106">Azure 앱 서비스 모바일 앱은 모바일에 최적화된 데이터 액세스 Web API를 웹 응용 프로그램에 추가하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="b4dcb-107">Azure 앱 서비스 모바일 앱 SDK는 ASP.NET 및 Node.js 웹 응용 프로그램에 대해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="b4dcb-108">SDK는 다음 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="b4dcb-109">데이터 액세스를 위한 테이블 작업(읽기, 삽입, 업데이트, 삭제)</span><span class="sxs-lookup"><span data-stu-id="b4dcb-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="b4dcb-110">API 작업 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-110">Custom API operations</span></span>

<span data-ttu-id="b4dcb-111">두 작업은 모두 Facebook, Twitter, Google Microsoft 등과 같은 소셜 ID 공급자 뿐만 아니라 엔터프라이즈 ID에 대한 Azure Active Directory를 포함하는 Azure 앱 서비스에서 허용된 모든 ID 공급자에 걸쳐 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="b4dcb-112">[GitHub의 샘플 디렉터리]에서 각 사용 사례에 대한 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b4dcb-113">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="b4dcb-113">Supported Platforms</span></span>
<span data-ttu-id="b4dcb-114">Azure Mobile Apps 노드 SDK는 노드의 최신 LTS 릴리스 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="b4dcb-115">이 문서를 작성할 당시 최신 LTS 버전은 노드 v4.5.0입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="b4dcb-116">다른 버전의 노드는 작동할 수는 있지만 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="b4dcb-117">Azure Mobile Apps 노드 SDK는 두 가지 데이터베이스 드라이버를 지원합니다. node-mssql 드라이버는 SQL Azure 및 로컬 SQL Server 인스턴스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="b4dcb-118">sqlite3 드라이버는 단일 인스턴스에서만 SQLite 데이터베이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="b4dcb-119"><a name="howto-cmdline-basicapp"></a>방법: 명령줄을 사용하는 기본 Node.js 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="b4dcb-120">모든 Azure 앱 서비스 모바일 앱 Node.js 백 엔드는 ExpressJS 응용 프로그램으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="b4dcb-121">ExpressJS는 Node.js에 사용할 수 있는 가장 인기 있는 웹 서비스 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="b4dcb-122">다음과 같이 기본 [Express] 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="b4dcb-123">명령 창 또는 PowerShell 창에서 프로젝트의 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="b4dcb-124">npm init를 실행하여 패키지 구조를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="b4dcb-125">npm init 명령은 프로젝트를 초기화하기 위해 몇 가지 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="b4dcb-126">예제 출력을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-126">See the example output:</span></span>

    ![Npm init 출력][0]
3. <span data-ttu-id="b4dcb-128">npm 리포지토리에서 Express 및 azure-mobile-apps 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="b4dcb-129">app.js 파일을 만들어서 기본 모바일 서버를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="b4dcb-130">이 응용 프로그램은 동적 스키마를 사용하여 기본 SQL 데이터 저장소에 대한 인증되지 않은 액세스를 제공하는 단일 끝점(`/tables/TodoItem`)으로 모바일에 최적화된 WebAPI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="b4dcb-131">다음의 클라이언트 라이브러리 빠른 시작에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="b4dcb-132">[Android 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-133">[Apache Cordova 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-134">[iOS 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-135">[Windows 스토어 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-136">[Xamarin.iOS 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-137">[Xamarin.Android 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="b4dcb-138">[Xamarin.Forms 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="b4dcb-139">[GitHub의 기본 앱 샘플]에서 이 기본 응용 프로그램에 대한 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="b4dcb-140"><a name="howto-vs2015-basicapp"></a>방법: Visual Studio 2015를 사용하여 노드 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="b4dcb-141">Visual Studio 2015는 IDE 내에서 Node.js 응용 프로그램 개발하도록 확장이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="b4dcb-142">시작하려면 [Visual Studio용 Node.js Tools 1.1]을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="b4dcb-143">Visual Studio용 Node.js Tools가 설치되면 Express 4.x 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="b4dcb-144">**새 프로젝트** 대화를 엽니다(**파일** > **새로 만들기** > **프로젝트...**에서).</span><span class="sxs-lookup"><span data-stu-id="b4dcb-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="b4dcb-145">**템플릿** > **JavaScript** > **Node.js**으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="b4dcb-146">**기본 Azure Node.js Express 4 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="b4dcb-147">프로젝트 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-147">Fill in the project name.</span></span>  <span data-ttu-id="b4dcb-148">*확인*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-148">Click *OK*.</span></span>

    ![Visual Studio 2015 새 프로젝트][1]
5. <span data-ttu-id="b4dcb-150">마우스 오른쪽 단추로 **npm** 노드를 클릭하고 **새 npm 패키지 설치...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="b4dcb-151">첫 번째 Node.js 응용 프로그램을 만드는 데 npm 카탈로그를 새로 고쳐야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="b4dcb-152">필요한 경우 **새로 고침** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="b4dcb-153">검색 상자에 *azure-mobile-apps* 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="b4dcb-154">**azure-mobile-apps 2.0.0** 패키지를 클릭한 다음 **패키지 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![새 npm 패키지 설치][2]
8. <span data-ttu-id="b4dcb-156">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-156">Click **Close**.</span></span>
9. <span data-ttu-id="b4dcb-157">*app.js* 파일을 열고 Azure 모바일 앱 SDK에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="b4dcb-158">라이브러리의 맨 아래 6 줄에 필요한 명령문, 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="b4dcb-159">다른 app.use 문 뒤 약 27줄에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="b4dcb-160">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-160">Save the file.</span></span>
10. <span data-ttu-id="b4dcb-161">응용 프로그램을 로컬로 실행하거나(API가 http://localhost:3000 에서 제공됨) Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="b4dcb-162"><a name="create-node-backend-portal"></a>방법: Azure 포털을 사용하여 Node.js 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="b4dcb-163">[Azure Portal]에서 바로 모바일 앱 백 엔드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="b4dcb-164">다음 단계를 수행하거나 [모바일 앱 만들기](app-service-mobile-ios-get-started.md) 자습서에 따라 클라이언트 및 서버를 함께 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="b4dcb-165">자습서는 이러한 지침의 단순화된 버전을 포함하고 있으며 개념 증명 프로젝트에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="b4dcb-166">*시작* 블레이드로 돌아가서 **테이블 API 만들기** 아래에서 **백 엔드 언어**로 **Node.js**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="b4dcb-167">“**이렇게 하면 모든 사이트 콘텐츠를 덮어쓴다는 것을 인정합니다.**”라는 상자를 선택하고 **TodoItem 테이블 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="b4dcb-168"><a name="download-quickstart"></a>방법: Git를 사용하여 Node.js 백 엔드 빠른 시작 코드 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b4dcb-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="b4dcb-169">포털 **빠른 시작** 블레이드를 사용하여 Node.js 모바일 앱 백 엔드를 만들 때 Node.js 프로젝트가 생성되어 사이트에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="b4dcb-170">테이블 및 API를 추가하고 포털에서 Node.js 백 엔드에 대한 코드 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="b4dcb-171">또한 다양한 배포 도구를 사용하여 백 엔드 프로젝트를 다운로드할 수 있으므로 테이블 및 API를 추가하거나 수정한 다음 프로젝트를 다시 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="b4dcb-172">자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="b4dcb-173">다음 절차에서는 Git 리포지토리를 사용하여 빠른 시작 프로젝트 코드를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="b4dcb-174">아직 수행하지 않았다면 Git을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="b4dcb-175">Git를 설치하는 데 필요한 단계는 운영 체제마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="b4dcb-176">운영 체제별 배포 및 설치 지침은 [Git 설치](http://git-scm.com/book/en/Getting-Started-Installing-Git) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="b4dcb-177">배포 사용자 이름 및 암호를 기록하여 백 엔드 사이트에 대한 Git 리포지토리를 사용하는 [앱 서비스 앱 리포지토리 사용](../app-service-web/app-service-deploy-local-git.md#Step3)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="b4dcb-178">모바일 앱 백 엔드에 대한 블레이드에서 **Git 복제 URL** 설정을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="b4dcb-179">다음 예제와 같이 Git 복제 URL을 사용하여 `git clone` 명령을 실행하고, 필요한 경우 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="b4dcb-180">로컬 디렉터리를 찾습니다. 앞의 예제에서는 /todolist였습니다. 그리고 프로젝트 파일이 다운로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="b4dcb-181">`/tables` 디렉터리에서 `todoitem.json` 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="b4dcb-182">이 파일은 테이블의 사용 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="b4dcb-183">그리고 같은 디렉터리에서 `todoitem.js` 파일도 찾습니다. 이 파일은 테이블에 대한 CRUD 작업 스크립트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="b4dcb-184">프로젝트 파일을 변경한 후에 다음 사이트에 변경 내용을 추가, 커밋, 업로드하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="b4dcb-185">프로젝트에 새 파일을 추가할 때 먼저 `git add .` 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="b4dcb-186">사이트는 사이트에 새로운 커밋 집합이 푸시될 때마다 다시 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="b4dcb-187"><a name="howto-publish-to-azure"></a>방법: Azure에 Node.js 백 엔드 게시</span><span class="sxs-lookup"><span data-stu-id="b4dcb-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="b4dcb-188">Microsoft Azure는 Azure 앱 서비스 모바일 앱 Node.js 백 엔드를 Azure 서비스에 게시하기 위한 여러 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="b4dcb-189">여기에는 원본 제어에 따라 Visual Studio, 명령줄 도구 및 연속 배포 옵션에 통합된 배포 도구의 활용을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="b4dcb-190">이 항목에 대한 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="b4dcb-191">Azure 앱 서비스에는 배포하기 전에 검토해야 하는 Node.js 응용 프로그램에 대한 구체적인 조언이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="b4dcb-192">[노드 버전 지정]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="b4dcb-193">[노드 모듈 사용]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-193">How to [use Node modules]</span></span>

### <span data-ttu-id="b4dcb-194"><a name="howto-enable-homepage"></a>방법: 응용 프로그램에 대한 홈페이지 사용</span><span class="sxs-lookup"><span data-stu-id="b4dcb-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="b4dcb-195">대부분의 응용 프로그램은 웹앱 및 모바일 앱의 조합이고 ExpressJS 프레임워크를 사용하면 두 가지 측면을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="b4dcb-196">그러나 때로는 모바일 인터페이스를 구현하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="b4dcb-197">앱 서비스를 실행하도록 하기 위해 방문 페이지를 제공하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="b4dcb-198">고유한 홈 페이지에 제공하거나 임시 홈 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="b4dcb-199">임시 홈 페이지를 사용하려면 다음을 사용하여 Azure Mobile Apps를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="b4dcb-200">로컬로 개발할 때에만 이 옵션을 사용하려면 이 설정을 `azureMobile.js` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="b4dcb-201"><a name="TableOperations"></a>테이블 작업</span><span class="sxs-lookup"><span data-stu-id="b4dcb-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="b4dcb-202">azure-mobile-apps Node.js 서버 SDK는 Azure SQL 데이터베이스에 저장된 데이터 테이블을 WebAPI로 노출하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="b4dcb-203">다섯 가지 작업이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-203">Five operations are provided.</span></span>

| <span data-ttu-id="b4dcb-204">작업</span><span class="sxs-lookup"><span data-stu-id="b4dcb-204">Operation</span></span> | <span data-ttu-id="b4dcb-205">설명</span><span class="sxs-lookup"><span data-stu-id="b4dcb-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4dcb-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="b4dcb-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="b4dcb-207">테이블의 레코드 모두 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-207">Get all records in the table</span></span> |
| <span data-ttu-id="b4dcb-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="b4dcb-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="b4dcb-209">테이블의 특정 레코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="b4dcb-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="b4dcb-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="b4dcb-211">테이블에 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-211">Create a record in the table</span></span> |
| <span data-ttu-id="b4dcb-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="b4dcb-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="b4dcb-213">테이블의 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="b4dcb-213">Update a record in the table</span></span> |
| <span data-ttu-id="b4dcb-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="b4dcb-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="b4dcb-215">테이블의 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="b4dcb-215">Delete a record in the table</span></span> |

<span data-ttu-id="b4dcb-216">이 WebAPI는 [OData]를 지원하고 테이블 스키마를 확장하여 [오프라인 데이터 동기화]를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="b4dcb-217"><a name="howto-dynamicschema"></a>방법: 동적 스키마를 사용하여 테이블 정의</span><span class="sxs-lookup"><span data-stu-id="b4dcb-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="b4dcb-218">테이블을 사용하기 전에 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="b4dcb-219">테이블은 정적 스키마(개발자가 스키마 내에서 열을 정의하는 위치) 또는 동적으로(SDK가 들어오는 요청에 따라 스키마를 제어하는 위치) 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="b4dcb-220">또한 개발자는 정의에 Javascript 코드를 추가하여 WebAPI의 특정 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="b4dcb-221">모범 사례로 테이블 디렉터리의 Javascript 파일에 각 테이블을 정의한 다음 테이블을 가져오는 tables.import() 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="b4dcb-222">basic-app을 확장하면 app.js 파일은 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="b4dcb-223">./tables/TodoItem.js에서 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="b4dcb-224">테이블은 기본적으로 동적 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="b4dcb-225">동적 스키마를 전역적으로 해제하려면 앱 설정 **MS_DynamicSchema**를 Azure 포털 내에서 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="b4dcb-226">[GitHub의 할 일 샘플]에서 전체 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="b4dcb-227"><a name="howto-staticschema"></a>방법: 정적 스키마를 사용하여 테이블 정의</span><span class="sxs-lookup"><span data-stu-id="b4dcb-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="b4dcb-228">열을 명시적으로 정의하여 WebAPI를 통해 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="b4dcb-229">azure-mobile-apps Node.js SDK는 오프라인 데이터 동기화에 필요한 모든 열을 사용자가 제공하는 목록에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="b4dcb-230">예를 들어 빠른 시작 클라이언트 응용 프로그램은 텍스트(문자열) 및 완료(부울)이라는 두 열이 있는 테이블이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="b4dcb-231">이 테이블은 다음과 같이 테이블 정의 JavaScript 파일(테이블 디렉터리에 위치)에서 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="b4dcb-232">또한 정적으로 테이블을 정의하는 경우 tables.initialize() 메서드를 호출하여 시작 시 데이터베이스 스키마를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="b4dcb-233">데이터베이스가 초기화되기 전에 웹 서비스가 요청을 처리하지 않도록 하기 위해 tables.initialize() 메서드는 [Promise] 를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="b4dcb-234"><a name="howto-sqlexpress-setup"></a>방법: 로컬 컴퓨터에서 개발 데이터 저장소로 SQL Express 사용</span><span class="sxs-lookup"><span data-stu-id="b4dcb-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="b4dcb-235">Azure 모바일 앱 AzureMobile 앱 노드 SDK는 상자에서 데이터를 처리 하기 위한 세 가지 옵션을 제공합니다. SDK는 상자에서 데이터를 처리 하기 위한 세 가지 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="b4dcb-236">**메모리** 드라이버를 사용하여 비 영구적 예제 저장소를 제공합니다</span><span class="sxs-lookup"><span data-stu-id="b4dcb-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="b4dcb-237">**mssql** 드라이버를 사용하여 개발을 위한 SQL Express 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="b4dcb-238">**mssql** 드라이버를 사용하여 프로덕션을 위한 Azure SQL 데이터베이스 데이터 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="b4dcb-239">Azure 모바일 앱 Node.js SDK는 [mssql Node.js 패키지] 를 사용하여 SQL Express 및 SQL 데이터베이스에 대한 연결을 설정하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="b4dcb-240">이 패키지는 SQL Express 인스턴스에서 TCP 연결을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="b4dcb-241">메모리 드라이버는 테스트하기 위한 완전한 기능 집합을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="b4dcb-242">백 엔드 로컬로 테스트하려는 경우 SQL Express 데이터 저장소 및 mssql 드라이버를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="b4dcb-243">[Microsoft SQL Server 2014 Express]를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="b4dcb-244">Tools Edition을 사용하여 SQL Server 2014 Express를 설치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="b4dcb-245">64비트를 지원하도록 명시적으로 요구하지 않는 한 32비트 버전이 실행할 때 메모리를 적게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="b4dcb-246">SQL Server 2014 구성 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="b4dcb-247">왼쪽 트리 메뉴에서 **SQL Server 네트워크 구성** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="b4dcb-248">**SQLEXPRESS에 대한 프로토콜**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="b4dcb-249">마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="b4dcb-250">팝업 대화 상자에서 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="b4dcb-251">마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="b4dcb-252">**IP 주소** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="b4dcb-253">**IPAll** 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="b4dcb-254">**TCP 포트** 필드에 **1433**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="b4dcb-255">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-255">Click **OK**.</span></span>  <span data-ttu-id="b4dcb-256">팝업 대화 상자에서 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="b4dcb-257">왼쪽 트리 메뉴에서 **SQL Server 서비스** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="b4dcb-258">마우스 오른쪽 단추로 **SQL Server (SQLEXPRESS)**를 클릭하고 **다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="b4dcb-259">SQL Server 2014 구성 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="b4dcb-260">SQL Server 2014 Management Studio를 실행하고 로컬 SQL Express 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="b4dcb-261">개체 탐색기에서 마우스 오른쪽 단추로 인스턴스를 클릭하고 **속성**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="b4dcb-262">**보안** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="b4dcb-263">**SQL Server 및 Windows 인증 모드** 를 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="b4dcb-264">**확인**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="b4dcb-265">**보안** > **로그인** 을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="b4dcb-266">마우스 오른쪽 단추로 **로그인**을 클릭하고 **새 로그인...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="b4dcb-267">로그인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-267">Enter a Login name.</span></span>  <span data-ttu-id="b4dcb-268">**SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="b4dcb-269">암호를 입력한 다음 동일한 암호를 **암호 확인**에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="b4dcb-270">암호는 Windows 복잡성 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="b4dcb-271">**확인**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="b4dcb-272">새 로그인을 마우스 오른쪽 단추로 클릭하고 **속성**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="b4dcb-273">**서버 역할** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="b4dcb-274">**dbcreator** 서버 역할 옆에 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="b4dcb-275">**확인**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-275">Click **OK**</span></span>
   13. <span data-ttu-id="b4dcb-276">SQL Server 2015 Management Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="b4dcb-277">사용자 이름 및 선택한 암호를 기록하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="b4dcb-278">특정 데이터베이스 요구 사항에 따라 추가 서버 역할 또는 사용 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="b4dcb-279">Node.js 응용 프로그램은 이 데이터베이스의 연결 문자열을 읽기 위해 **SQLCONNSTR_MS_TableConnectionString** 환경 변수를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="b4dcb-280">환경 내에서 이 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="b4dcb-281">예를 들어 이 환경 변수를 설정하려면 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="b4dcb-282">TCP/IP 연결을 통해 데이터베이스에 액세스하고 연결에 필요한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="b4dcb-283"><a name="howto-config-localdev"></a>방법: 로컬 개발에 대한 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="b4dcb-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="b4dcb-284">Azure Mobile Apps는 로컬 파일 시스템에서 *azureMobile.js*라는 JavaScript 파일을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="b4dcb-285">이 파일을 사용하여 프로덕션에서 Azure Mobile Apps SDK를 구성하지 마세요. 대신 [Azure Portal] 내에서 앱 설정을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="b4dcb-286">*azureMobile.js* 파일은 구성 개체를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="b4dcb-287">가장 일반적인 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-287">The most common settings are:</span></span>

* <span data-ttu-id="b4dcb-288">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-288">Database Settings</span></span>
* <span data-ttu-id="b4dcb-289">진단 로깅 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="b4dcb-290">대체 CORS 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-290">Alternate CORS Settings</span></span>

<span data-ttu-id="b4dcb-291">앞에 나온 데이터베이스 설정을 구현하는 *azureMobile.js* 예제 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="b4dcb-292">*.gitignore* 파일에 *azureMobile.js*를 추가하여(또는 기타 소스 코드 제어 무시 파일) 암호가 클라우드에 저장되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="b4dcb-293">[Azure Portal]내의 앱 설정에서 프로덕션 설정을 항상 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="b4dcb-294"><a name="howto-appsettings"></a>방법: 모바일 앱에 대한 앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b4dcb-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="b4dcb-295">*azureMobile.js* 파일에서 대부분의 설정은 [Azure Portal]에서 동일한 앱 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="b4dcb-296">다음 목록을 사용하여 앱 설정에서 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="b4dcb-297">앱 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-297">App Setting</span></span> | <span data-ttu-id="b4dcb-298">*azureMobile.js* 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="b4dcb-299">설명</span><span class="sxs-lookup"><span data-stu-id="b4dcb-299">Description</span></span> | <span data-ttu-id="b4dcb-300">유효한 값</span><span class="sxs-lookup"><span data-stu-id="b4dcb-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b4dcb-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="b4dcb-302">name</span><span class="sxs-lookup"><span data-stu-id="b4dcb-302">name</span></span> |<span data-ttu-id="b4dcb-303">앱의 이름</span><span class="sxs-lookup"><span data-stu-id="b4dcb-303">The name of the app</span></span> |<span data-ttu-id="b4dcb-304">string</span><span class="sxs-lookup"><span data-stu-id="b4dcb-304">string</span></span> |
| <span data-ttu-id="b4dcb-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="b4dcb-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="b4dcb-306">logging.level</span></span> |<span data-ttu-id="b4dcb-307">로깅할 메시지의 최소 로그 수준</span><span class="sxs-lookup"><span data-stu-id="b4dcb-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="b4dcb-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="b4dcb-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="b4dcb-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-309">**MS_DebugMode**</span></span> |<span data-ttu-id="b4dcb-310">debug</span><span class="sxs-lookup"><span data-stu-id="b4dcb-310">debug</span></span> |<span data-ttu-id="b4dcb-311">디버그 모드를 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="b4dcb-312">true, false</span><span class="sxs-lookup"><span data-stu-id="b4dcb-312">true, false</span></span> |
| <span data-ttu-id="b4dcb-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-313">**MS_TableSchema**</span></span> |<span data-ttu-id="b4dcb-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="b4dcb-314">data.schema</span></span> |<span data-ttu-id="b4dcb-315">SQL 테이블에 대한 기본 스키마 이름</span><span class="sxs-lookup"><span data-stu-id="b4dcb-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="b4dcb-316">string(기본값: dbo)</span><span class="sxs-lookup"><span data-stu-id="b4dcb-316">string (default: dbo)</span></span> |
| <span data-ttu-id="b4dcb-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="b4dcb-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="b4dcb-318">data.dynamicSchema</span></span> |<span data-ttu-id="b4dcb-319">디버그 모드를 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="b4dcb-320">true, false</span><span class="sxs-lookup"><span data-stu-id="b4dcb-320">true, false</span></span> |
| <span data-ttu-id="b4dcb-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="b4dcb-322">version(undefined로 설정)</span><span class="sxs-lookup"><span data-stu-id="b4dcb-322">version (set to undefined)</span></span> |<span data-ttu-id="b4dcb-323">X-ZUMO-Server-Version 헤더를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="b4dcb-324">true, false</span><span class="sxs-lookup"><span data-stu-id="b4dcb-324">true, false</span></span> |
| <span data-ttu-id="b4dcb-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="b4dcb-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="b4dcb-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="b4dcb-326">skipversioncheck</span></span> |<span data-ttu-id="b4dcb-327">클라이언트 API 버전 검사를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-327">Disables the client API version check</span></span> |<span data-ttu-id="b4dcb-328">true, false</span><span class="sxs-lookup"><span data-stu-id="b4dcb-328">true, false</span></span> |

<span data-ttu-id="b4dcb-329">앱 설정을 지정하려면:</span><span class="sxs-lookup"><span data-stu-id="b4dcb-329">To set an App Setting:</span></span>

1. <span data-ttu-id="b4dcb-330">[Azure Portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="b4dcb-331">**모든 리소스** 또는 **App Services**를 선택한 후 모바일 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="b4dcb-332">설정 블레이드가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-332">The Settings blade opens by default.</span></span> <span data-ttu-id="b4dcb-333">열리지 않으면 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="b4dcb-334">일반 메뉴에서 **응용 프로그램 설정** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="b4dcb-335">앱 설정 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="b4dcb-336">앱 설정이 이미 있는 경우 앱 설정 값을 클릭하여 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="b4dcb-337">앱 설정이 존재하지 않는 경우 키 상자에 앱 설정을 입력하고 값 상자에 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="b4dcb-338">완료했으면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="b4dcb-339">대부분의 앱은 설정 변경 후 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="b4dcb-340"><a name="howto-use-sqlazure"></a>방법: 프로덕션 데이터 저장소로 SQL 데이터베이스 사용</span><span class="sxs-lookup"><span data-stu-id="b4dcb-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="b4dcb-341">Azure SQL 데이터베이스를 데이터 저장소로 사용하면 모든 Azure 앱 서비스 응용 프로그램 형식에 걸쳐 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="b4dcb-342">아직 수행하지 않은 경우 다음 단계에 따라 모바일 앱 백 엔드를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="b4dcb-343">[Azure Portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="b4dcb-344">위쪽에 클릭을 창의 왼쪽는 **+ 새로 만들기** 단추 > **웹 + 모바일** > **모바일 앱**, 모바일 앱 백 엔드에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="b4dcb-345">**리소스 그룹** 상자에 앱과 동일한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="b4dcb-346">기본 App Service 계획이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="b4dcb-347">App Service 계획을 변경하려는 경우 App Service 계획 > **+ 새로 만들기**를 클릭하여 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="b4dcb-348">새 앱 서비스 계획의 이름을 입력하고 적절한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="b4dcb-349">가격 책정 계층을 클릭하고 서비스에 대한 적절한 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="b4dcb-350">**무료** 및 **공유** 등의 더 많은 가격 책정 옵션을 보려면 **모두 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="b4dcb-351">가격 책정 계층을 선택한 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="b4dcb-352">**앱 서비스 계획** 블레이드로 돌아가서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="b4dcb-353">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-353">Click **Create**.</span></span> <span data-ttu-id="b4dcb-354">모바일 앱 백 엔드를 프로비저닝하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="b4dcb-355">모바일 앱 백 엔드가 프로비전되면 포털에서 모바일 앱 백 엔드에 대한 **설정** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="b4dcb-356">모바일 앱 백 엔드를 만들면 모바일 앱 백 엔드에 기존 SQL 데이터베이스를 연결하거나 새 SQL 데이터베이스를 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="b4dcb-357">이 섹션에서 SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="b4dcb-358">모바일 앱 백 엔드와 동일한 위치에 데이터베이스가 이미 있다면 대신 **기존 데이터베이스 사용** 을 선택한 다음 해당 데이터베이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="b4dcb-359">다른 위치에 있는 데이터베이스는 대기 시간이 높기 때문에 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="b4dcb-360">새 모바일 앱 백 엔드에서 **설정** > **모바일 앱** > **데이터** > **+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="b4dcb-361">**데이터 연결 추가** 블레이드에서 **SQL 데이터베이스 - 필요한 설정 구성** > **새 데이터베이스를 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="b4dcb-362">**이름** 필드에 새 데이터베이스 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="b4dcb-363">**서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-363">Click **Server**.</span></span>  <span data-ttu-id="b4dcb-364">**새 서버** 블레이드에서 **서버 이름** 필드에 고유한 서버 이름을 입력하고 적절한 **서버 관리자 로그인** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="b4dcb-365">**Azure 서비스가 서버에 액세스하도록 허용** 이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="b4dcb-366">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-366">Click **OK**.</span></span>

    ![Azure SQL 데이터베이스 만들기][6]
4. <span data-ttu-id="b4dcb-368">**새 데이터베이스** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="b4dcb-369">**데이터 연결 추가** 블레이드로 돌아가서 **연결 문자열**을 선택하고 데이터베이스를 만들 때 입력한 로그인 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="b4dcb-370">기존 데이터베이스를 사용하는 경우 해당 데이터베이스에 대한 로그인 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="b4dcb-371">입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="b4dcb-372">**데이터 연결 추가** 블레이드로 다시 돌아가서 **확인**을 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="b4dcb-373">데이터베이스를 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="b4dcb-374">**알림** 영역을 사용하여 배포의 진행률을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="b4dcb-375">데이터베이스가 성공적으로 배포될 때까지 진행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="b4dcb-376">성공적으로 배포되면 모바일 백 엔드 앱 설정에서 SQL Database 인스턴스에 대한 연결 문자열이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="b4dcb-377">**설정** > **응용 프로그램 설정** > **연결 문자열**에서 각 사용 사례에 대한 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="b4dcb-378"><a name="howto-tables-auth"></a>방법: 테이블에 대한 액세스 인증 요구</span><span class="sxs-lookup"><span data-stu-id="b4dcb-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="b4dcb-379">테이블 끝점을 사용하여 App Service 인증을 사용하려는 경우 [Azure Portal] 에서 우선 App Service 인증을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="b4dcb-380">Azure 앱 서비스에서 인증을 구성하는 데 대한 자세한 내용은 사용하려는 ID 공급자를 위한 구성 가이드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="b4dcb-381">[Azure Active Directory 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="b4dcb-382">[Facebook 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="b4dcb-383">[Google 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="b4dcb-384">[Microsoft 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="b4dcb-385">[Twitter 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="b4dcb-386">각 테이블에는 테이블에 대한 액세스를 제어하는 데 사용할 수 있는 액세스 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="b4dcb-387">다음 샘플에서는 필요한 인증을 사용하여 정적으로 정의된 테이블을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="b4dcb-388">액세스 속성은 세 가지 값 중 하나를 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b4dcb-388">The access property can take one of three values</span></span>

* <span data-ttu-id="b4dcb-389">*익명* 은 클라이언트 응용 프로그램이 인증 없이 데이터를 읽을 수 있다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="b4dcb-390">*인증됨* 은 클라이언트 응용 프로그램이 요청을 사용하여 유효한 인증 토큰을 송신해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="b4dcb-391">*사용 안 함* 은 이 테이블이 현재 사용되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="b4dcb-392">액세스 속성을 정의하지 않으면 인증되지 않은 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="b4dcb-393"><a name="howto-tables-getidentity"></a>방법: 테이블을 사용하여 인증 클레임 사용</span><span class="sxs-lookup"><span data-stu-id="b4dcb-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="b4dcb-394">인증이 설정될 때 요청되는 다양한 클레임을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="b4dcb-395">이러한 클레임은 `context.user` 개체를 통해 정상적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="b4dcb-396">그러나 `context.user.getIdentity()` 메서드를 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="b4dcb-397">`getIdentity()` 메서드는 개체로 확인되는 Promise를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="b4dcb-398">개체는 인증 방법(facebook, google, twitter, microsoftaccount 또는 aad)을 키로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="b4dcb-399">예를 들어 Microsoft 계정 인증을 설정하고 메일 주소 클레임을 요청하는 경우 다음 테이블 컨트롤러를 사용하여 레코드에 메일 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="b4dcb-400">사용할 수 있는 클레임을 보려면 웹 브라우저를 사용하여 사이트의 `/.auth/me` 끝점을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="b4dcb-401"><a name="howto-tables-disabled"></a>방법: 특정 테이블 작업에 대한 액세스 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="b4dcb-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="b4dcb-402">테이블에 나타나는 것 외에도 액세스 속성은 개별 작업을 제어하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="b4dcb-403">네 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-403">There are four operations:</span></span>

* <span data-ttu-id="b4dcb-404">*읽기* 는 테이블의 RESTful 가져오기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="b4dcb-405">*삽입* 은 테이블의 RESTful POST 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="b4dcb-406">*업데이트* 는 테이블의 RESTful PATCH 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="b4dcb-407">*삭제* 는 테이블의 RESTful DELETE 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="b4dcb-408">예를 들어 읽기 전용 인증되지 않은 테이블을 제공하려 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="b4dcb-409"><a name="howto-tables-query"></a>방법: 테이블 작업에 사용되는 쿼리 조정</span><span class="sxs-lookup"><span data-stu-id="b4dcb-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="b4dcb-410">테이블 작업에 대한 일반적인 요구 사항은 데이터의 제한된 보기를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="b4dcb-411">예를 들어 사용자가 본인의 레코드를 읽거나 업데이트하는 것만 가능하도록 인증된 사용자 ID로 태그가 지정된 테이블을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="b4dcb-412">다음 테이블 정의는 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="b4dcb-413">일반적으로 쿼리를 실행하는 작업에는 where 절을 사용하여 조정할 수 있는 쿼리 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="b4dcb-414">쿼리 속성은 데이터 백 엔드가 처리할 수 있는 무언가에 OData 쿼리를 변환하는 데 사용되는 [QueryJS] 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="b4dcb-415">앞의 예처럼 간단한 같음 쿼리의 경우 맵을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="b4dcb-416">또한 특정 SQL 절을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="b4dcb-417"><a name="howto-tables-softdelete"></a>방법: 테이블에 일시 삭제 구성</span><span class="sxs-lookup"><span data-stu-id="b4dcb-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="b4dcb-418">일시 삭제는 레코드를 실제로 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="b4dcb-419">대신 삭제된 열을 true로 설정하여 데이터베이스 내에서 삭제된 것으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="b4dcb-420">모바일 클라이언트 SDK가 IncludeDeleted()를 사용하지 않는 경우 Azure 모바일 앱 SDK는 일시 삭제된 레코드를 결과에서 자동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="b4dcb-421">일시 삭제에 대한 테이블을 구성하려면 테이블 정의 파일에서 `softDelete` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="b4dcb-422">WebJob, Azure 함수 또는 사용자 지정 API를 통해 클라이언트 응용 프로그램에서 레코드를 제거하는 메커니즘을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="b4dcb-423"><a name="howto-tables-seeding"></a>방법: 데이터를 사용하여 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="b4dcb-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="b4dcb-424">새 응용 프로그램을 만들 때 데이터가 있는 테이블을 시드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="b4dcb-425">다음과 같이 테이블 정의 JavaScript 파일 내에서 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="b4dcb-426">데이터의 시드는 Azure Mobile Apps SDK에서 테이블을 만들 때에만 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="b4dcb-427">테이블이 데이터베이스 내에 이미 있으면 데이터는 테이블에 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="b4dcb-428">동적 스키마를 설정한 경우 스키마는 시드된 데이터에서 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="b4dcb-429">서비스가 실행되기 시작하면 `tables.initialize()` 메서드를 명시적으로 호출하여 테이블을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="b4dcb-430"><a name="Swagger"></a>방법: Swagger 지원 사용</span><span class="sxs-lookup"><span data-stu-id="b4dcb-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="b4dcb-431">Azure 앱 서비스 모바일 앱은 기본 제공 [Swagger] 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="b4dcb-432">Swagger 지원을 사용하려면 먼저Swagger UI를 종속성으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="b4dcb-433">설치되면 Azure 모바일 앱 생성자에서 Swagger 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="b4dcb-434">개발 버전에서 Swagger 지원을 사용하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="b4dcb-435">`NODE_ENV` 앱 설정을 활용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="b4dcb-436">Swagger 끝점은 http://*yoursite*.azurewebsites.net/swagger에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="b4dcb-437">`/swagger/ui` 끝점을 통해 Swagger UI에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="b4dcb-438">전체 응용 프로그램에서 인증을 요구하도록 선택하면 Swagger가 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="b4dcb-439">최상의 결과를 위해 Azure 앱 서비스 인증/권한 부여 설정 및 `table.access` 속성을 사용하는 제어 인증에서 인증되지 않은 요청을 허용하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="b4dcb-440">또한 로컬로 개발할 때 Swagger 지원을 원하는 경우 `azureMobile.js` 파일에 Swagger 옵션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="b4dcb-441"><a name="push">푸시 알림</span><span class="sxs-lookup"><span data-stu-id="b4dcb-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="b4dcb-442">모바일 앱은 수많은 모든 주요 플랫폼의 장치에 대상 푸시 알림을 보낼 수 있도록 Azure 알림 허브와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="b4dcb-443">알림 허브를 사용하여 iOS, Android 및 Windows 장치에 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="b4dcb-444">알림 허브를 통해 수행할 수 있는 모든 것에 대한 자세한 내용은 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="b4dcb-445"></a><a name="send-push"></a>방법: 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="b4dcb-446">다음 코드는 등록된 iOS 장치에 브로드캐스트 푸시 알림을 보내기 위해 push 개체를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="b4dcb-447">클라이언트에서 템플릿 푸시 등록을 만들면 지원되는 모든 플랫폼의 장치에 템플릿 푸시 메시지를 대신 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="b4dcb-448">다음 코드는 템플릿 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="b4dcb-449"><a name="push-user"></a>방법: 태그를 사용하여 인증된 사용자에게 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="b4dcb-450">인증된 사용자가 푸시 알림에 등록하면 사용자 ID 태그가 등록에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="b4dcb-451">이 태그를 사용하여 특정 사용자가 등록된 모든 장치에 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="b4dcb-452">다음 코드는 요청을 만드는 사용자의 SID를 가져오고 해당 사용자에 대한 모든 장치 등록에 템플릿 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="b4dcb-453">인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="b4dcb-454"><a name="CustomAPI"></a> 사용자 지정 API</span><span class="sxs-lookup"><span data-stu-id="b4dcb-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="b4dcb-455"><a name="howto-customapi-basic"></a>방법: 사용자 지정 API 정의</span><span class="sxs-lookup"><span data-stu-id="b4dcb-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="b4dcb-456">/tables 끝점을 통한 데이터 액세스 API 외에도 Azure 모바일 앱은 사용자 지정 API 범위를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="b4dcb-457">사용자 지정 API는 유사한 방식으로 테이블 정의에 정의되고 인증을 비롯한 동일한 시설에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="b4dcb-458">사용자 지정 API를 사용하여 App Service 인증을 사용하려는 경우 [Azure Portal] 에서 우선 App Service 인증을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="b4dcb-459">Azure 앱 서비스에서 인증을 구성하는 데 대한 자세한 내용은 사용하려는 ID 공급자를 위한 구성 가이드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="b4dcb-460">[Azure Active Directory 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="b4dcb-461">[Facebook 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="b4dcb-462">[Google 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="b4dcb-463">[Microsoft 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="b4dcb-464">[Twitter 인증을 구성하는 방법]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="b4dcb-465">사용자 지정 API는 거의 동일한 방식으로 테이블 API로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="b4dcb-466">**api** 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="b4dcb-466">Create an **api** directory</span></span>
2. <span data-ttu-id="b4dcb-467">**api** 디렉터리에서 API 정의 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="b4dcb-468">가져오기 메서드를 사용하여 **API** 디렉터리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="b4dcb-469">다음은 이전에 사용된 기본 앱 샘플에 따른 프로토타입 API 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="b4dcb-470">*Date.now()* 메서드를 사용하여 서버 날짜를 반환하는 API 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="b4dcb-471">다음은 api/date.js 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="b4dcb-472">각 매개 변수는 GET, POST, PATCH 또는 DELETE와 같은 RESTful 표준 동사의 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="b4dcb-473">메서드는 필요한 출력을 전송하는 표준 [ExpressJS 미들웨어] 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="b4dcb-474"><a name="howto-customapi-auth"></a>방법: 사용자 지정 API에 대한 액세스 인증 요구</span><span class="sxs-lookup"><span data-stu-id="b4dcb-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="b4dcb-475">Azure 모바일 앱 SDK는 테이블 끝점 및 사용자 지정 API에 대해 동일한 방식으로 인증을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="b4dcb-476">이전 섹션에서 개발된 API에 인증을 추가하려면 **access** 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="b4dcb-477">또한 특정 작업에 인증을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="b4dcb-478">테이블 끝점에 사용되는 동일한 토큰은 인증을 요구하는 사용자 지정 API에 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="b4dcb-479"><a name="howto-customapi-auth"></a>방법: 대용량 파일 업로드 처리</span><span class="sxs-lookup"><span data-stu-id="b4dcb-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="b4dcb-480">Azure 모바일 앱 SDK는 [body-parser middleware](https://github.com/expressjs/body-parser) 를 사용하여 제출하는 본문 내용을 허용 및 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="b4dcb-481">더 큰 파일 업로드를 허용하도록 body-parser를 미리 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="b4dcb-482">이 파일은 Base-64로 인코딩된 후 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="b4dcb-483">이렇게 하면 실제 업로드의 크기가 증가합니다(따라서 고려해야 할 크기도 증가).</span><span class="sxs-lookup"><span data-stu-id="b4dcb-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="b4dcb-484"><a name="howto-customapi-sql"></a>방법: 사용자 지정 SQL 문 실행</span><span class="sxs-lookup"><span data-stu-id="b4dcb-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="b4dcb-485">Azure 모바일 앱 SDK를 사용하면 정의된 데이터 공급자에 대해 매개 변수화된 SQL 문을 쉽게 실행할 수 있는 요청 개체를 통해 전체 컨텍스트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="b4dcb-486"><a name="Debugging"></a>디버깅, 쉬운 테이블 및 간편한 API</span><span class="sxs-lookup"><span data-stu-id="b4dcb-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="b4dcb-487"><a name="howto-diagnostic-logs"></a>방법: Azure Mobile Apps의 디버깅, 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b4dcb-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="b4dcb-488">Azure 앱 서비스는 Node.js 응용 프로그램에 대한 여러 디버깅 및 문제 해결 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="b4dcb-489">Node.js 모바일 백 엔드 문제 해결에서 시작하는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="b4dcb-490">[Azure 앱 서비스 모니터링]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="b4dcb-491">[Azure 앱 서비스에 진단 로그 사용]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="b4dcb-492">[Visual Studio에서 Azure 앱 서비스 문제 해결]</span><span class="sxs-lookup"><span data-stu-id="b4dcb-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="b4dcb-493">Node.js 응용 프로그램은 넓은 범위의 진단 로그 도구에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="b4dcb-494">내부적으로 Azure 모바일 앱 Node.js SDK는 진단 로깅에 [윈스턴] 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="b4dcb-495">[Azure Portal]에서 디버그 모드를 사용하거나 **MS_DebugMode** 앱 설정을 true로 설정하여 로깅이 자동으로 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="b4dcb-496">생성된 로그는 [Azure Portal]의 진단 로그에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="b4dcb-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>방법: Azure 포털에서 테이블로 간편하게 작업</span><span class="sxs-lookup"><span data-stu-id="b4dcb-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="b4dcb-498">포털에서 쉬운 테이블을 통해 포털에서 테이블을 만들고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="b4dcb-499">앱 서비스 편집기를 사용하여 테이블 작업을 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="b4dcb-500">백 엔드 사이트 설정에서 **쉬운 테이블** 을 클릭하면 테이블을 추가, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="b4dcb-501">테이블의 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-501">You can also see data in the table.</span></span>

![쉬운 테이블 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="b4dcb-503">다음 명령을 테이블에 대한 명령 모음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="b4dcb-504">**사용 권한 변경** - 작업 테이블에서 읽기, 삽입, 업데이트 및 삭제에 대한 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="b4dcb-505">옵션은 익명 액세스를 허용하거나 인증을 요구하거나 작업에 대한 모든 액세스를 사용할 수 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="b4dcb-506">**스크립트 편집** - 테이블에 대한 스크립트 파일은 앱 서비스 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="b4dcb-507">**스키마 관리** - 열을 추가 또는 삭제하거나 테이블 인덱스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="b4dcb-508">**테이블 지우기** - 기존 테이블을 잘라서 모든 데이터 행을 삭제하지만 스키마를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="b4dcb-509">**행 삭제** - 데이터의 개별 행을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="b4dcb-510">**스트리밍 로그 보기** - 사이트에 대한 스트리밍 로그 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="b4dcb-511"><a name="work-easy-apis"></a>방법: Azure 포털에서 API로 간편하게 작업</span><span class="sxs-lookup"><span data-stu-id="b4dcb-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="b4dcb-512">포털에서 쉬운 API를 통해 포털에서 사용자 지정 API를 만들고 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="b4dcb-513">App Service 편집기를 사용하여 API 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="b4dcb-514">백 엔드 사이트 설정에서 **쉬운 API** 를 클릭하면 사용자 지정 API 끝점을 추가, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![쉬운 API 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="b4dcb-516">포털에서 지정된 HTTP 작업에 대한 액세스 권한을 변경하거나, App Service 편집기에서 API 스크립트 파일을 편집하거나, 스트리밍 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="b4dcb-517"><a name="online-editor"></a>방법: 앱 서비스 편집기에서 코드 편집</span><span class="sxs-lookup"><span data-stu-id="b4dcb-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="b4dcb-518">Azure 포털을 사용하면 로컬 컴퓨터에 프로젝트를 다운로드하지 않고도 앱 서비스 편집기에서 Node.js 백 엔드 스크립트 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="b4dcb-519">온라인 편집기에서 스크립트 파일을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="b4dcb-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="b4dcb-520">모바일 앱 백 엔드 블레이드에서 **모든 설정** > **쉬운 테이블** 또는 **쉬운 API** 중 하나를 클릭하고 테이블 또는 API를 클릭한 다음 **스크립트 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="b4dcb-521">스크립트 파일은 앱 서비스 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-521">The script file is opened in the App Service Editor.</span></span>

    ![앱 서비스 편집기](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="b4dcb-523">온라인 편집기에서 코드 파일의 내용을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="b4dcb-524">변경 내용은 입력할 때 자동으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4dcb-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="b4dcb-525">[Android 클라이언트 빠른 시작]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="b4dcb-526">[Apache Cordova 클라이언트 빠른 시작]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b4dcb-527">[iOS 클라이언트 빠른 시작]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="b4dcb-528">[Xamarin.iOS 클라이언트 빠른 시작]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="b4dcb-529">[Xamarin.Android 클라이언트 빠른 시작]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="b4dcb-530">[Xamarin.Forms 클라이언트 빠른 시작]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="b4dcb-531">[Windows 스토어 클라이언트 빠른 시작]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="b4dcb-532">[오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="b4dcb-533">[Azure Active Directory 인증을 구성하는 방법]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="b4dcb-534">[Facebook 인증을 구성하는 방법]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="b4dcb-535">[Google 인증을 구성하는 방법]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="b4dcb-536">[Microsoft 인증을 구성하는 방법]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="b4dcb-537">[Twitter 인증을 구성하는 방법]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="b4dcb-538">[Azure App Service 배포 가이드]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="b4dcb-539">[Azure 앱 서비스 모니터링]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="b4dcb-540">[Azure 앱 서비스에 진단 로그 사용]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="b4dcb-541">[Visual Studio에서 Azure 앱 서비스 문제 해결]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="b4dcb-542">[노드 버전 지정]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="b4dcb-543">[노드 모듈 사용]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="b4dcb-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="b4dcb-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="b4dcb-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="b4dcb-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="b4dcb-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="b4dcb-546">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b4dcb-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="b4dcb-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="b4dcb-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="b4dcb-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="b4dcb-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="b4dcb-549">[GitHub의 기본 앱 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="b4dcb-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="b4dcb-550">[GitHub의 할 일 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="b4dcb-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="b4dcb-551">[GitHub의 샘플 디렉터리]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="b4dcb-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="b4dcb-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="b4dcb-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="b4dcb-553">[Visual Studio용 Node.js Tools 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="b4dcb-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="b4dcb-554">[mssql Node.js 패키지]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="b4dcb-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="b4dcb-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="b4dcb-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="b4dcb-556">[ExpressJS 미들웨어]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="b4dcb-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="b4dcb-557">[윈스턴]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="b4dcb-557">[Winston]: https://github.com/winstonjs/winston</span></span>
