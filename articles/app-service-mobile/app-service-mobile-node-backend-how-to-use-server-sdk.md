---
title: "hello Node.js 백 엔드 서버 모바일 앱에 대 한 SDK와 aaaHow toowork | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱에 대 한와 toowork Node.js 백 엔드 서버 SDK hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="4de84-103">어떻게 toouse hello Azure 모바일 앱 Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="4de84-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="4de84-104">이 문서에서는 상세 정보와 예제를 보여 주는 방법을 Azure 앱 서비스 모바일 앱에서 Node.js 백 엔드와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="4de84-105"><a name="Introduction"></a>소개</span><span class="sxs-lookup"><span data-stu-id="4de84-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="4de84-106">Azure 앱 서비스 모바일 앱 hello 기능 tooadd 모바일에 최적화 된 데이터 액세스 Web API tooa 웹 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="4de84-107">hello Azure 앱 서비스 모바일 앱 SDK는 ASP.NET 및 Node.js 웹 응용 프로그램에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="4de84-108">hello를 SDK hello를 다음 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="4de84-109">데이터 액세스를 위한 테이블 작업(읽기, 삽입, 업데이트, 삭제)</span><span class="sxs-lookup"><span data-stu-id="4de84-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="4de84-110">API 작업 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4de84-110">Custom API operations</span></span>

<span data-ttu-id="4de84-111">두 작업은 모두 Facebook, Twitter, Google Microsoft 등과 같은 소셜 ID 공급자 뿐만 아니라 엔터프라이즈 ID에 대한 Azure Active Directory를 포함하는 Azure 앱 서비스에서 허용된 모든 ID 공급자에 걸쳐 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="4de84-112">각각에 대 한 샘플 사례를 사용 하 여 hello에서 찾을 수 있습니다 [GitHub에서 예제 디렉터리]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4de84-113">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="4de84-113">Supported Platforms</span></span>
<span data-ttu-id="4de84-114">Azure 모바일 앱 노드 SDK hello hello 현재 LTS 노드의 이상 릴리스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="4de84-115">문서를 작성할 당시 hello 최신 LTS 버전이 노드 첫 v4.5.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="4de84-116">다른 버전의 노드는 작동할 수는 있지만 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="4de84-117">Azure 모바일 앱 노드 SDK hello 두 데이터베이스 드라이버 지원-hello 노드 mssql 드라이버가 지 원하는 SQL Azure 및 로컬 SQL Server 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="4de84-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="4de84-118">hello sqlite3 드라이버 단일 인스턴스에서 SQLite 데이터베이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="4de84-119"><a name="howto-cmdline-basicapp"></a>방법: 명령줄 hello를 사용 하 여 기본 Node.js 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="4de84-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="4de84-120">모든 Azure 앱 서비스 모바일 앱 Node.js 백 엔드는 ExpressJS 응용 프로그램으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="4de84-121">ExpressJS는 hello 가장 인기 있는 웹 서비스 프레임 워크 Node.js에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="4de84-122">다음과 같이 기본 [Express] 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="4de84-123">명령 창 또는 PowerShell 창에서 프로젝트의 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="4de84-124">Npm init tooinitialize hello 패키지 구조를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="4de84-125">hello npm init 명령은 질문 tooinitialize hello 프로젝트 집합이 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="4de84-126">Hello 예제 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-126">See hello example output:</span></span>

    ![hello npm init 출력][0]
3. <span data-ttu-id="4de84-128">Hello npm 리포지토리에서 hello express 및 azure 모바일 앱 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="4de84-129">app.js 파일 tooimplement hello 기본 모바일 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="4de84-130">이 응용 프로그램을 단일 끝점과 모바일 액세스에 최적화 된 WebAPI를 만듭니다 (`/tables/TodoItem`) 인증 되지 않은 액세스 tooan 동적 스키마를 사용 하 여 SQL 데이터 저장소를 기본 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="4de84-131">다음의 클라이언트 라이브러리 빠른 시작에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="4de84-132">[Android 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="4de84-133">[Apache Cordova 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="4de84-134">[iOS 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="4de84-135">[Windows 스토어 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="4de84-136">[Xamarin.iOS 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="4de84-137">[Xamarin.Android 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="4de84-138">[Xamarin.Forms 클라이언트 빠른 시작]</span><span class="sxs-lookup"><span data-stu-id="4de84-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="4de84-139">Hello에서이 기본 응용 프로그램에 대 한 hello 코드를 찾을 수 [GitHub에 basicapp 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="4de84-140"><a name="howto-vs2015-basicapp"></a>방법: Visual Studio 2015를 사용하여 노드 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="4de84-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="4de84-141">Visual Studio 2015 hello IDE 내에서 확장 toodevelop Node.js 응용 프로그램을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="4de84-142">toostart, 설치 hello [Visual Studio 용 Node.js 도구 1.1]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="4de84-143">Visual Studio 용 Node.js 도구 hello 설치 되 면 Express 4.x 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="4de84-144">열기 hello **새 프로젝트** 대화 (에서 **파일** > **새로** > **프로젝트...** ).</span><span class="sxs-lookup"><span data-stu-id="4de84-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="4de84-145">**템플릿** > **JavaScript** > **Node.js**으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="4de84-146">선택 hello **기본 Azure Node.js Express 4 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="4de84-147">Hello 프로젝트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-147">Fill in hello project name.</span></span>  <span data-ttu-id="4de84-148">*확인*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-148">Click *OK*.</span></span>

    ![Visual Studio 2015 새 프로젝트][1]
5. <span data-ttu-id="4de84-150">마우스 오른쪽 단추로 클릭 hello **npm** 노드 선택한 **npm 패키지를 새 설치 중...** .</span><span class="sxs-lookup"><span data-stu-id="4de84-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="4de84-151">첫 번째 Node.js 응용 프로그램을 만드는 방법에 toorefresh hello npm 카탈로그를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="4de84-152">필요한 경우 **새로 고침** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="4de84-153">입력 *azure 모바일 앱* hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="4de84-154">Hello 클릭 **azure 모바일 앱 2.0.0** 패키지 하 고, 한 다음 클릭 **패키지 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![새 npm 패키지 설치][2]
8. <span data-ttu-id="4de84-156">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-156">Click **Close**.</span></span>
9. <span data-ttu-id="4de84-157">열기 hello *app.js* 파일 hello Azure 모바일 앱 SDK에 대 한 tooadd 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="4de84-158">Hello 라이브러리의 줄에 6 hello 아래쪽에 문이 필요 hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="4de84-159">선에서 약 27 hello 후 다른 app.use 문 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="4de84-160">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-160">Save hello file.</span></span>
10. <span data-ttu-id="4de84-161">Hello 응용 프로그램을 로컬 (http://localhost:3000에 배달 API 광고가 hello)를 실행 하거나 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="4de84-162"><a name="create-node-backend-portal"></a>방법: hello Azure 포털을 사용 하 여 Node.js 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="4de84-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="4de84-163">Hello에 대 한 모바일 앱 백 엔드 권한을 만들 수 있습니다 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="4de84-164">다음 단계 또는 클라이언트와 서버 hello를 수행 하 여 함께 만들 hello 하거나 따르면 [모바일 앱을 만들](app-service-mobile-ios-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="4de84-165">hello 자습서가이 지침의 단순화 된 버전을 포함 하 고 프로젝트 개념 증명에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="4de84-166">Hello에 다시 *시작* 블레이드 아래 **API 테이블을 만들**, 선택 **Node.js** 으로 프로그램 **백 엔드 언어**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="4de84-167">Hello 확인란에 대 한 "**는 덮어씁니다 모든 사이트 콘텐츠. 것에 동의**"를 클릭 한 다음 **만들 TodoItem 테이블**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="4de84-168"><a name="download-quickstart"></a>방법: Git를 사용 하 여 다운로드 hello Node.js 백 엔드 퀵 스타트 코드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="4de84-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="4de84-169">Hello 포털을 사용 하 여 Node.js 모바일 앱 백 엔드를 만들면 **퀵 스타트** 블레이드에서 Node.js 프로젝트 및 배포 된 tooyour 사이트에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="4de84-170">테이블 및 Api 추가 및 hello 포털에서 hello Node.js 백 엔드에 대 한 코드 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="4de84-171">다양 한 배포 도구 toodownload hello 백 엔드 프로젝트를 추가 하거나 테이블 및 Api를 수정한 다음 hello 프로젝트를 다시 게시할 수 있습니다 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="4de84-172">자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4de84-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="4de84-173">hello 다음 절차에서는 사용 Git 리포지토리 toodownload hello 퀵 스타트 프로젝트 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="4de84-174">아직 수행하지 않았다면 Git을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="4de84-175">hello 단계 필요한 tooinstall Git 운영 체제 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="4de84-176">운영 체제별 배포 및 설치 지침은 [Git 설치](http://git-scm.com/book/en/Getting-Started-Installing-Git) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4de84-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="4de84-177">Hello 단계에 따라 [사용 hello 앱 서비스 앱 저장소](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello 배포 사용자 이름 및 암호의 한 노트 백 엔드 사이트에 Git 리포지토리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="4de84-178">모바일 앱 백 엔드에 대 한 hello 블레이드에서 hello 기록해 **Git 복제 URL** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="4de84-179">Hello 실행 `git clone` 다음 예제와 같이 필요한 경우 암호를 입력 hello Git 복제 URL을 사용 하 여 명령을:</span><span class="sxs-lookup"><span data-stu-id="4de84-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="4de84-180">앞 예제는 hello에서는 /todolist 인 검색 toolocal 디렉터리 및 프로젝트 파일에 다운로드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="4de84-181">Hello 찾을 `todoitem.json` hello에 대 한 파일 `/tables` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="4de84-182">이 파일은 테이블의 사용 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="4de84-183">Hello 오류도 찾을 `todoitem.js` hello 동일 파일 hello 테이블에 대 한 CRUD 작업 스크립트를 정의 하는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="4de84-184">변경을 마쳤으면 tooproject 파일을 한 후 명령을 tooadd, 커밋, 다음 변경 내용을 toohello 사이트 업로드를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="4de84-185">Tooexecute hello 먼저 새 파일 toohello 프로젝트에 추가 하면 `git add .` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="4de84-186">hello 사이트는 새로운 집합이 커밋 toohello 사이트 푸시됩니다 될 때마다 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="4de84-187"><a name="howto-publish-to-azure"></a>방법: Node.js 백 엔드 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="4de84-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="4de84-188">Microsoft Azure hello Azure 서비스를 Azure 앱 서비스 모바일 앱 Node.js 백 엔드를 게시 하기 위한 여러 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="4de84-189">여기에는 원본 제어에 따라 Visual Studio, 명령줄 도구 및 연속 배포 옵션에 통합된 배포 도구의 활용을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="4de84-190">이 항목에 대한 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4de84-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="4de84-191">Azure 앱 서비스에는 배포하기 전에 검토해야 하는 Node.js 응용 프로그램에 대한 구체적인 조언이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="4de84-192">어떻게 너무[hello 노드 버전을 지정 합니다.]</span><span class="sxs-lookup"><span data-stu-id="4de84-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="4de84-193">어떻게 너무[노드 모듈 사용]</span><span class="sxs-lookup"><span data-stu-id="4de84-193">How too[use Node modules]</span></span>

### <span data-ttu-id="4de84-194"><a name="howto-enable-homepage"></a>방법: 응용 프로그램에 대한 홈페이지 사용</span><span class="sxs-lookup"><span data-stu-id="4de84-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="4de84-195">대부분의 응용 프로그램은 웹 및 모바일 앱의 조합 및 hello ExpressJS 프레임 워크 있습니다 toocombine 두 패싯 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="4de84-196">그러나 경우에 따라 수도 있습니다 tooonly 구현 모바일 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="4de84-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="4de84-197">것이 유용한 tooprovide 방문 페이지 tooensure hello 앱 서비스 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="4de84-198">고유한 홈 페이지에 제공하거나 임시 홈 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="4de84-199">tooenable 임시 홈 페이지를 사용 하 여 hello 다음 tooinstantiate Azure 모바일 앱:</span><span class="sxs-lookup"><span data-stu-id="4de84-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="4de84-200">로컬 개발 하는 경우이 옵션을 사용 하려면,이 설정은 tooyour를 추가할 수 있습니다 `azureMobile.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="4de84-201"><a name="TableOperations"></a>테이블 작업</span><span class="sxs-lookup"><span data-stu-id="4de84-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="4de84-202">hello azure 모바일 앱 Node.js 서버 SDK 메커니즘을 제공 tooexpose 데이터 테이블을 WebAPI와 Azure SQL 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="4de84-203">다섯 가지 작업이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-203">Five operations are provided.</span></span>

| <span data-ttu-id="4de84-204">작업</span><span class="sxs-lookup"><span data-stu-id="4de84-204">Operation</span></span> | <span data-ttu-id="4de84-205">설명</span><span class="sxs-lookup"><span data-stu-id="4de84-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4de84-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="4de84-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="4de84-207">Hello 테이블의 모든 레코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="4de84-207">Get all records in hello table</span></span> |
| <span data-ttu-id="4de84-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="4de84-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="4de84-209">Hello 테이블에서 특정 레코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="4de84-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="4de84-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="4de84-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="4de84-211">Hello 테이블의 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-211">Create a record in hello table</span></span> |
| <span data-ttu-id="4de84-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="4de84-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="4de84-213">Hello 테이블의 레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="4de84-213">Update a record in hello table</span></span> |
| <span data-ttu-id="4de84-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="4de84-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="4de84-215">Hello 테이블에서 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="4de84-215">Delete a record in hello table</span></span> |

<span data-ttu-id="4de84-216">이 WebAPI 지원 [OData] hello 테이블 스키마 toosupport 확장 [오프 라인 데이터 동기화]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="4de84-217"><a name="howto-dynamicschema"></a>방법: 동적 스키마를 사용하여 테이블 정의</span><span class="sxs-lookup"><span data-stu-id="4de84-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="4de84-218">테이블을 사용하기 전에 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="4de84-219">테이블 스키마 (hello 개발자 정의 hello 스키마 내의 hello 열) 정적 또는 동적으로 정의할 수 있습니다 (SDK hello 컨트롤 hello 스키마 들어오는 요청에 따라).</span><span class="sxs-lookup"><span data-stu-id="4de84-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="4de84-220">또한 hello 개발자는 Javascript 코드 toohello 정의 추가 하 여 hello WebAPI의 특정 측면을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="4de84-221">모범 사례로, hello 테이블 디렉터리에 Javascript 파일에 각 테이블을 정의한 다음 tables.import() 메서드 tooimport hello 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="4de84-222">Hello basic 앱을 확장 hello app.js 파일 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="4de84-223">Hello 테이블에 정의 됩니다. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="4de84-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="4de84-224">테이블은 기본적으로 동적 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="4de84-225">동적 스키마 오프 tooturn hello 앱 설정을 전역으로 설정 **MS_DynamicSchema** toofalse hello Azure 포털 내에서.</span><span class="sxs-lookup"><span data-stu-id="4de84-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="4de84-226">전체 예제는 hello에서 찾을 수 [GitHub에 todo 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="4de84-227"><a name="howto-staticschema"></a>방법: 정적 스키마를 사용하여 테이블 정의</span><span class="sxs-lookup"><span data-stu-id="4de84-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="4de84-228">Hello 열 tooexpose hello WebAPI 통해 명시적으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="4de84-229">hello azure 모바일 앱 Node.js SDK 제공 하는 오프 라인 데이터 동기화 toohello 목록에 필요한 모든 추가 열을 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="4de84-230">예를 들어 빠른 시작 클라이언트 응용 프로그램은 텍스트(문자열) 및 완료(부울)이라는 두 열이 있는 테이블이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="4de84-231">hello 테이블 hello 테이블 정의 JavaScript 파일에 (hello 테이블 디렉터리에 위치) 다음과 같이 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="4de84-232">테이블을 정적으로 정의 하는 경우 다음도 호출 해야 hello tables.initialize() 메서드 toocreate hello 데이터베이스 스키마 시작할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="4de84-233">hello tables.initialize() 메서드 반환는 [프라미스] hello 웹 서비스는 hello 데이터베이스 초기화 하기 전에 요청을 처리 하지 않는 경우 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="4de84-234"><a name="howto-sqlexpress-setup"></a>방법: 로컬 컴퓨터에서 개발 데이터 저장소로 SQL Express 사용</span><span class="sxs-lookup"><span data-stu-id="4de84-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="4de84-235">hello Azure 모바일 앱 hello AzureMobile 앱 노드 SDK는 트랜잭션 구성을 위해 hello 초기 데이터 서비스를 제공할: SDK는 hello 초기 데이터를 처리 하기 위한 세 가지 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="4de84-236">사용 하 여 hello **메모리** 드라이버 tooprovide 비 영구적인 예제 저장소</span><span class="sxs-lookup"><span data-stu-id="4de84-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="4de84-237">사용 하 여 hello **mssql** 드라이버 tooprovide 개발을 위한 SQL Express 데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="4de84-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="4de84-238">사용 하 여 hello **mssql** 드라이버 tooprovide Azure SQL 데이터베이스 데이터 저장소를 사용 하 여 프로덕션에</span><span class="sxs-lookup"><span data-stu-id="4de84-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="4de84-239">Azure 모바일 앱 Node.js SDK hello hello를 사용 하 여 [mssql Node.js 패키지] tooestablish 연결 tooboth SQL Express 및 SQL 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="4de84-240">이 패키지는 SQL Express 인스턴스에서 TCP 연결을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="4de84-241">hello 메모리 드라이버는 완전 한 테스트 하기 위한 기능 집합을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="4de84-242">로컬로 백 엔드 tootest을 원할 경우에서는 SQL Express 데이터 저장소의 hello 사용 고 권장 mssql 드라이버 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="4de84-243">[Microsoft SQL Server 2014 Express]를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="4de84-244">Hello SQL Server 2014 Express with Tools 버전 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="4de84-245">64 비트 지원 기능을 명시적으로 요구 하지 않는 한 hello 32 비트 버전 실행 하는 경우 메모리를 적게 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="4de84-246">Hello SQL Server 2014 구성 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="4de84-247">Hello 확장 **SQL Server 네트워크 구성** hello 왼쪽 트리 메뉴에서 노드.</span><span class="sxs-lookup"><span data-stu-id="4de84-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="4de84-248">**SQLEXPRESS에 대한 프로토콜**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="4de84-249">마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="4de84-250">클릭 **확인** hello 팝업 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="4de84-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="4de84-251">마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="4de84-252">Hello 클릭 **IP 주소** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="4de84-253">Hello **IPAll** 노드.</span><span class="sxs-lookup"><span data-stu-id="4de84-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="4de84-254">Hello에 **TCP 포트** 필드에, 입력 **1433**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="4de84-255">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-255">Click **OK**.</span></span>  <span data-ttu-id="4de84-256">클릭 **확인** hello 팝업 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="4de84-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="4de84-257">클릭 **SQL Server 서비스** hello 왼쪽 트리 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="4de84-258">마우스 오른쪽 단추로 **SQL Server (SQLEXPRESS)**를 클릭하고 **다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="4de84-259">Hello SQL Server 2014 구성 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="4de84-260">Hello SQL Server 2014 Management Studio를 실행 하 고 tooyour 로컬 SQL Express 인스턴스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="4de84-261">Hello 개체 탐색기에서에서 인스턴스를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**</span><span class="sxs-lookup"><span data-stu-id="4de84-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="4de84-262">선택 hello **보안** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4de84-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="4de84-263">Hello 확인 **SQL Server 및 Windows 인증 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="4de84-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="4de84-264">**확인**</span><span class="sxs-lookup"><span data-stu-id="4de84-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="4de84-265">확장 **보안** > **로그인** hello 개체 탐색기에서</span><span class="sxs-lookup"><span data-stu-id="4de84-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="4de84-266">마우스 오른쪽 단추로 **로그인**을 클릭하고 **새 로그인...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="4de84-267">로그인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-267">Enter a Login name.</span></span>  <span data-ttu-id="4de84-268">**SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="4de84-269">암호를 입력 한 다음 hello 입력에 동일한 암호를 **암호 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="4de84-270">hello 암호 Windows 복잡성 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="4de84-271">**확인**</span><span class="sxs-lookup"><span data-stu-id="4de84-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="4de84-272">새 로그인을 마우스 오른쪽 단추로 클릭하고 **속성**</span><span class="sxs-lookup"><span data-stu-id="4de84-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="4de84-273">선택 hello **서버 역할** 페이지</span><span class="sxs-lookup"><span data-stu-id="4de84-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="4de84-274">Hello 상자 다음 toohello 확인 **dbcreator** 서버 역할</span><span class="sxs-lookup"><span data-stu-id="4de84-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="4de84-275">**확인**</span><span class="sxs-lookup"><span data-stu-id="4de84-275">Click **OK**</span></span>
   13. <span data-ttu-id="4de84-276">Hello SQL Server 2015 Management Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="4de84-277">레코드 hello 사용자 이름 및 암호 선택한 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4de84-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="4de84-278">특정 데이터베이스 요구 사항에 따라 tooassign 추가 서버 역할 또는 권한을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="4de84-279">Node.js 응용 프로그램 hello 읽고 hello **SQLCONNSTR_MS_TableConnectionString** 이 데이터베이스에 대 한 연결 문자열 hello에 대 한 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="4de84-280">환경 내에서 이 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="4de84-281">예를 들어이 환경 변수 PowerShell tooset를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="4de84-282">TCP/IP 연결을 통해 hello 데이터베이스에 액세스 하 고 hello 연결에 대 한 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="4de84-283"><a name="howto-config-localdev"></a>방법: 로컬 개발에 대한 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="4de84-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="4de84-284">Azure 모바일 앱 이라는 JavaScript 파일을 읽고 *azureMobile.js* hello 로컬 파일 시스템에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="4de84-285">프로덕션 환경에서이 파일 tooconfigure hello Azure 모바일 앱 SDK를 사용 하 여-hello 내에서 응용 프로그램 설정을 사용 하지 않는 [Azure 포털] 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="4de84-286">hello *azureMobile.js* 파일 구성 개체를 내보낼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="4de84-287">hello 가장 일반적인 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-287">hello most common settings are:</span></span>

* <span data-ttu-id="4de84-288">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-288">Database Settings</span></span>
* <span data-ttu-id="4de84-289">진단 로깅 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="4de84-290">대체 CORS 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-290">Alternate CORS Settings</span></span>

<span data-ttu-id="4de84-291">예로 *azureMobile.js* 데이터베이스 설정을 다음과 같이 앞 hello를 구현 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="4de84-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

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

<span data-ttu-id="4de84-292">추가 하는 것이 좋습니다 *azureMobile.js* tooyour *.gitignore* 파일 (또는 파일을 무시 다른 소스 코드 제어) hello 클라우드에 저장 되지 tooprevent 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="4de84-293">항상 hello 내에서 프로덕션 설정을 응용 프로그램 설정에서 구성 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="4de84-294"><a name="howto-appsettings"></a>방법: 모바일 앱에 대한 앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="4de84-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="4de84-295">Hello에 대부분의 설정은 *azureMobile.js* 파일이 hello에 해당 하는 응용 프로그램 설정을 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="4de84-296">사용 하 여 hello 다음 tooconfigure 앱 설정에서 응용 프로그램을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="4de84-297">앱 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-297">App Setting</span></span> | <span data-ttu-id="4de84-298">*azureMobile.js* 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="4de84-299">설명</span><span class="sxs-lookup"><span data-stu-id="4de84-299">Description</span></span> | <span data-ttu-id="4de84-300">유효한 값</span><span class="sxs-lookup"><span data-stu-id="4de84-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4de84-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="4de84-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="4de84-302">name</span><span class="sxs-lookup"><span data-stu-id="4de84-302">name</span></span> |<span data-ttu-id="4de84-303">hello hello 앱 이름</span><span class="sxs-lookup"><span data-stu-id="4de84-303">hello name of hello app</span></span> |<span data-ttu-id="4de84-304">string</span><span class="sxs-lookup"><span data-stu-id="4de84-304">string</span></span> |
| <span data-ttu-id="4de84-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="4de84-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="4de84-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="4de84-306">logging.level</span></span> |<span data-ttu-id="4de84-307">메시지 toolog의 최소 로그 수준</span><span class="sxs-lookup"><span data-stu-id="4de84-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="4de84-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="4de84-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="4de84-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="4de84-309">**MS_DebugMode**</span></span> |<span data-ttu-id="4de84-310">debug</span><span class="sxs-lookup"><span data-stu-id="4de84-310">debug</span></span> |<span data-ttu-id="4de84-311">디버그 모드를 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="4de84-312">true, false</span><span class="sxs-lookup"><span data-stu-id="4de84-312">true, false</span></span> |
| <span data-ttu-id="4de84-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="4de84-313">**MS_TableSchema**</span></span> |<span data-ttu-id="4de84-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="4de84-314">data.schema</span></span> |<span data-ttu-id="4de84-315">SQL 테이블에 대한 기본 스키마 이름</span><span class="sxs-lookup"><span data-stu-id="4de84-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="4de84-316">string(기본값: dbo)</span><span class="sxs-lookup"><span data-stu-id="4de84-316">string (default: dbo)</span></span> |
| <span data-ttu-id="4de84-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="4de84-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="4de84-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="4de84-318">data.dynamicSchema</span></span> |<span data-ttu-id="4de84-319">디버그 모드를 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="4de84-320">true, false</span><span class="sxs-lookup"><span data-stu-id="4de84-320">true, false</span></span> |
| <span data-ttu-id="4de84-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="4de84-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="4de84-322">버전 (집합 tooundefined)</span><span class="sxs-lookup"><span data-stu-id="4de84-322">version (set tooundefined)</span></span> |<span data-ttu-id="4de84-323">Hello X ZUMO-서버 버전 헤더를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="4de84-324">true, false</span><span class="sxs-lookup"><span data-stu-id="4de84-324">true, false</span></span> |
| <span data-ttu-id="4de84-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="4de84-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="4de84-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="4de84-326">skipversioncheck</span></span> |<span data-ttu-id="4de84-327">Hello 클라이언트 API 버전 검사를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="4de84-327">Disables hello client API version check</span></span> |<span data-ttu-id="4de84-328">true, false</span><span class="sxs-lookup"><span data-stu-id="4de84-328">true, false</span></span> |

<span data-ttu-id="4de84-329">tooset 앱 설정:</span><span class="sxs-lookup"><span data-stu-id="4de84-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="4de84-330">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="4de84-331">선택 **모든 리소스** 또는 **응용 프로그램 서비스** 모바일 응용 프로그램의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="4de84-332">기본적으로 hello 설정 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="4de84-333">열리지 않으면 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="4de84-334">클릭 **응용 프로그램 설정** hello 일반 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="4de84-335">응용 프로그램 설정 섹션 toohello를 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="4de84-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="4de84-336">앱 설정에 이미 있는 경우 hello 앱 설정 tooedit hello 값의 hello 값을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="4de84-337">응용 프로그램 설정에 없는 경우 hello 키 상자와 hello 값 상자에 hello 값에 hello 응용 프로그램 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="4de84-338">완료했으면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="4de84-339">대부분의 앱은 설정 변경 후 서비스를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="4de84-340"><a name="howto-use-sqlazure"></a>방법: 프로덕션 데이터 저장소로 SQL 데이터베이스 사용</span><span class="sxs-lookup"><span data-stu-id="4de84-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="4de84-341">Azure SQL 데이터베이스를 데이터 저장소로 사용하면 모든 Azure 앱 서비스 응용 프로그램 형식에 걸쳐 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="4de84-342">아직 수행 하지 않은, 이러한 단계 toocreate 모바일 앱 백 엔드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="4de84-343">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="4de84-344">Hello 왼쪽 위 hello 창의 hello 클릭에서 **+ 새로 만들기** 단추 > **웹 + 모바일** > **모바일 앱**, 모바일 앱 백 엔드에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="4de84-345">Hello에 **리소스 그룹** 상자에 응용 프로그램으로 hello 이름과 같은 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="4de84-346">hello 기본 앱 서비스 계획 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="4de84-347">앱 서비스 계획 toochange을 원할 경우 후 그렇게 hello 앱 서비스 계획을 클릭 하 여 > **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="4de84-348">Hello 새 앱 서비스 계획의 이름을 제공 하 고 적절 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="4de84-349">Hello 가격 책정 계층을 클릭 하 고 hello 서비스에 대 한 적절 한 가격대를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="4de84-350">선택 **모든 보기** 더와 같은 옵션, 가격 책정 tooview **무료** 및 **Shared**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="4de84-351">가격 책정 계층을 선택 하면 클릭 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="4de84-352">Hello에 다시 **앱 서비스 계획** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="4de84-353">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-353">Click **Create**.</span></span> <span data-ttu-id="4de84-354">모바일 앱 백 엔드를 프로비저닝하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="4de84-355">Hello 포털이 열립니다 hello hello 모바일 앱 백 엔드는 프로 비전 되 면 **설정을** 블레이드 hello 모바일 앱 백 엔드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="4de84-356">Hello 모바일 앱 백 엔드를 만든 후 tooeither 선택할 수 있습니다는 기존 SQL 데이터베이스 tooyour 모바일 앱 백 엔드 연결 하거나 새 SQL 데이터베이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="4de84-357">이 섹션에서 SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="4de84-358">Hello에 데이터베이스를 이미 만든 경우 hello 모바일 앱 백 엔드에서와 동일한 위치를 선택할 수 있습니다 대신 **기존 데이터베이스를 사용 하 여** 한 다음 해당 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="4de84-359">hello를 사용 하 여 다른 위치에 데이터베이스의 대기 시간이 늘어날 때문에 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="4de84-360">Hello 새로운 모바일 앱 백 엔드에서 클릭 **설정** > **모바일 앱** > **데이터** > **+ 추가**.</span><span class="sxs-lookup"><span data-stu-id="4de84-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="4de84-361">Hello에 **데이터 연결 추가** 블레이드에서 클릭 **SQL 데이터베이스-필요한 설정 구성** > **새 데이터베이스를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="4de84-362">Hello에 hello 새 데이터베이스의 hello 이름을 입력 **이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="4de84-363">**서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-363">Click **Server**.</span></span>  <span data-ttu-id="4de84-364">Hello에 **새 서버** 블레이드에서 hello에 고유한 서버 이름을 입력 **서버 이름** 필드를 한 번 살펴보고 적절 한 **서버 관리자 로그인** 및 **암호**.</span><span class="sxs-lookup"><span data-stu-id="4de84-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="4de84-365">확인 **허용 azure 서비스 tooaccess 서버** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="4de84-366">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-366">Click **OK**.</span></span>

    ![Azure SQL 데이터베이스 만들기][6]
4. <span data-ttu-id="4de84-368">Hello에 **새 데이터베이스** 블레이드에서 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="4de84-369">Hello에 다시 **데이터 연결 추가** 블레이드를 **연결 문자열**, hello 로그인 및 사용자가 제공한 hello 데이터베이스를 만들 때 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="4de84-370">기존 데이터베이스를 사용 하는 경우 해당 데이터베이스에 대 한 hello 로그인 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="4de84-371">입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="4de84-372">Hello에 다시 **데이터 연결 추가** 블레이드를 다시 클릭 **확인** toocreate hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="4de84-373">Hello 데이터베이스 만들기에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="4de84-374">사용 하 여 hello **알림** 영역 toomonitor hello 배포의 진행 상황 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="4de84-375">Hello 데이터베이스를 성공적으로 배포 될 때까지 진행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="4de84-376">성공적으로 배포 되 면 모바일 백 엔드 응용 프로그램 설정의에서 hello SQL 데이터베이스 인스턴스에 대 한 연결 문자열을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="4de84-377">Hello에서이 응용 프로그램 설정을 볼 수 있습니다 **설정** > **응용 프로그램 설정** > **연결 문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="4de84-378"><a name="howto-tables-auth"></a>방법: 액세스 tootables에 인증 필요</span><span class="sxs-lookup"><span data-stu-id="4de84-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="4de84-379">Hello에 응용 프로그램 서비스 인증을 구성 해야 응용 프로그램 서비스 인증 toouse hello 테이블 끝점을 사용 하려는 경우 [Azure 포털] 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="4de84-380">Azure 응용 프로그램 서비스에 인증을 구성 하는 방법에 대 한 자세한 내용은 hello id 공급자에 대 한 hello 구성 가이드를 확인 하려는 toouse:</span><span class="sxs-lookup"><span data-stu-id="4de84-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="4de84-381">[어떻게 tooconfigure Azure Active Directory 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="4de84-382">[어떻게 tooconfigure Facebook 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="4de84-383">[어떻게 tooconfigure Google 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="4de84-384">[어떻게 tooconfigure Microsoft 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="4de84-385">[어떻게 tooconfigure Twitter 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="4de84-386">각 테이블에 사용 되는 toocontrol access toohello 테이블 일 수 있는 액세스 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="4de84-387">다음 예제는 hello 인증 필요로 정적으로 정의 된 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="4de84-388">hello 액세스 속성 세 값 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="4de84-389">*익명* hello 클라이언트 응용 프로그램 인증 없이 tooread 데이터 허용 됨을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="4de84-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="4de84-390">*인증 된* hello 클라이언트 응용 프로그램 hello 요청과 함께 유효한 인증 토큰이 송신 해야 함을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="4de84-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="4de84-391">*사용 안 함* 은 이 테이블이 현재 사용되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="4de84-392">Hello 액세스 속성을 정의 하지 않으면 인증 되지 않은 액세스가 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="4de84-393"><a name="howto-tables-getidentity"></a>방법: 테이블을 사용하여 인증 클레임 사용</span><span class="sxs-lookup"><span data-stu-id="4de84-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="4de84-394">인증이 설정될 때 요청되는 다양한 클레임을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="4de84-395">이러한 클레임이 hello를 통해 일반적으로 제공 되지 않습니다. `context.user` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="4de84-396">그러나 검색할 수 있는 hello를 사용 하 여 `context.user.getIdentity()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4de84-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="4de84-397">hello `getIdentity()` 메서드 tooan 개체를 확인 되는 프라미스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="4de84-398">hello 개체는 인증 방법 (facebook, google, twitter, microsoftaccount, 또는 aad)에서 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="4de84-399">예를 들어 Microsoft 계정 인증 및 요청 hello 전자 메일 주소 클레임을 설정한 경우 다음 테이블 컨트롤러 hello로 hello 전자 메일 주소 toohello 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="4de84-400">toosee 어떤 클레임을 사용할 수, 웹 브라우저 tooview hello를 사용 하 여 `/.auth/me` 사이트의 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="4de84-401"><a name="howto-tables-disabled"></a>방법: 사용 안 함 액세스 toospecific 테이블 작업</span><span class="sxs-lookup"><span data-stu-id="4de84-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="4de84-402">Hello 테이블에 추가 tooappearing, hello 액세스 속성 사용된 toocontrol 개별 작업 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="4de84-403">네 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-403">There are four operations:</span></span>

* <span data-ttu-id="4de84-404">*읽기* 은 hello 테이블에 hello RESTful GET 작업</span><span class="sxs-lookup"><span data-stu-id="4de84-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="4de84-405">*삽입* hello RESTful POST 작업 hello 테이블에는</span><span class="sxs-lookup"><span data-stu-id="4de84-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="4de84-406">*업데이트* hello RESTful PATCH 작업 hello 테이블에는</span><span class="sxs-lookup"><span data-stu-id="4de84-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="4de84-407">*삭제* hello 테이블에서 hello RESTful 삭제 작업은</span><span class="sxs-lookup"><span data-stu-id="4de84-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="4de84-408">예, 읽기 전용 인증 되지 않은 테이블 tooprovide를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="4de84-409"><a name="howto-tables-query"></a>방법: 테이블 작업에 사용 되는 hello 쿼리를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="4de84-410">테이블 작업에 대 한 일반적인 요구 사항은 tooprovide hello 데이터의 제한 된 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="4de84-411">예를 들어 hello로 태그가 지정 된 테이블 에서만 읽을 하거나 사용자 고유의 레코드를 업데이트할 수 있도록 사용자 ID를 인증을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="4de84-412">이 기능을 제공 하는 테이블 정의 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="4de84-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="4de84-413">일반적으로 쿼리를 실행하는 작업에는 where 절을 사용하여 조정할 수 있는 쿼리 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="4de84-414">hello 쿼리 속성은 한 [QueryJS] 되는 개체를 사용 하는 백 엔드 데이터 hello 하는 OData 쿼리 toosomething tooconvert 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="4de84-415">(예: hello 앞서) 간단 비교의 경우에 대 한 지도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="4de84-416">또한 특정 SQL 절을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="4de84-417"><a name="howto-tables-softdelete"></a>방법: 테이블에 일시 삭제 구성</span><span class="sxs-lookup"><span data-stu-id="4de84-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="4de84-418">일시 삭제는 레코드를 실제로 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="4de84-419">대신 표시에 열 tootrue hello 삭제를 설정 하 여 hello 데이터베이스 내에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="4de84-420">hello Azure 모바일 앱 SDK에서에서 자동으로 제거 일시 삭제 된 레코드 결과 hello 모바일 클라이언트 SDK IncludeDeleted() 사용 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="4de84-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="4de84-421">소프트에 대 한 테이블 삭제 tooconfigure hello 설정 `softDelete` hello 테이블 정의 파일에서 속성:</span><span class="sxs-lookup"><span data-stu-id="4de84-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="4de84-422">WebJob, Azure 함수 또는 사용자 지정 API를 통해 클라이언트 응용 프로그램에서 레코드를 제거하는 메커니즘을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="4de84-423"><a name="howto-tables-seeding"></a>방법: 데이터를 사용하여 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="4de84-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="4de84-424">새 응용 프로그램을 만들 때 데이터가 있는 테이블을 tooseed를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="4de84-425">이렇게 hello 테이블 정의 JavaScript 파일 내에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="4de84-426">데이터 시드 hello 테이블은 hello Azure 모바일 앱 SDK가 작성 하는 경우에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="4de84-427">Hello 테이블에 이미 있으면 hello 데이터베이스 내에서 데이터가 없는 hello 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="4de84-428">동적 스키마를 설정 하는 경우 스키마는 hello 시드 데이터에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="4de84-429">안녕하세요 명시적으로 호출 하는 것이 좋습니다 `tables.initialize()` hello 서비스 실행을 시작할 때 메서드 toocreate hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="4de84-430"><a name="Swagger"></a>방법: Swagger 지원 사용</span><span class="sxs-lookup"><span data-stu-id="4de84-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="4de84-431">Azure 앱 서비스 모바일 앱은 기본 제공 [Swagger] 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="4de84-432">먼저 tooenable Swagger 지원 종속성으로 hello swagger ui를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="4de84-433">설치 되 면 hello Azure 모바일 앱 생성자에서 Swagger 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="4de84-434">있습니다 수만 원하는 tooenable 개발 버전의 Swagger 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="4de84-435">`NODE_ENV` 앱 설정을 활용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="4de84-436">hello swagger 끝점은에 http://*yoursite*.azurewebsites.net/swagger 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="4de84-437">Hello Swagger UI hello 통해 액세스할 수 있습니다 `/swagger/ui` 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="4de84-438">Swagger 전체 응용 프로그램에서 toorequire 인증을 선택한 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="4de84-439">최상의 결과 통해 인증 되지 않은 tooallow 요청에서 선택 hello Azure 앱 서비스 인증에에서 권한 부여 설정 후 hello를 사용 하 여 인증을 제어 하는 / `table.access` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="4de84-440">Hello Swagger 옵션 tooyour를 추가할 수도 있습니다 `azureMobile.js` 로컬로 개발할 때만 Swagger 지원을 원하는 경우에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="4de84-441"><a name="push">푸시 알림</span><span class="sxs-lookup"><span data-stu-id="4de84-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="4de84-442">모바일 앱 통합 Azure 알림 허브 tooenable 하면 장치를 대상 toosend 푸시 알림을 toomillions 모든 주요 플랫폼 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="4de84-443">알림 허브를 사용 하 여 푸시를 보낼 수 있습니다 알림 tooiOS, Android 및 Windows 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="4de84-444">사용 하 여 수행할 수 있는 모든 작업에 대 한 자세한 toolearn 알림 허브 참조 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="4de84-445"></a><a name="send-push"></a>방법: 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4de84-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="4de84-446">코드 다음 hello toouse hello 푸시 개체 toosend 브로드캐스트 알림 tooregistered iOS 장치를 강제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="4de84-447">Hello 클라이언트에서 템플릿 푸시 등록을 만들어, 지원 되는 모든 플랫폼에서 템플릿 푸시 메시지 toodevices 대신 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="4de84-448">코드에서 보여 주는 방법을 다음 hello toosend 템플릿 알림:</span><span class="sxs-lookup"><span data-stu-id="4de84-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="4de84-449"><a name="push-user"></a>방법: 태그를 사용 하 여 사용자를 인증 하는 송신 푸시 알림을 tooan</span><span class="sxs-lookup"><span data-stu-id="4de84-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="4de84-450">인증된 된 사용자 푸시 알림에 등록, 사용자 ID 태그 toohello 등록 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="4de84-451">이 태그를 사용 하 여 푸시 알림 tooall 장치는 특정 사용자가 등록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="4de84-452">hello 다음 코드 hello hello 요청을 만드는 사용자의 SID를 가져오고 해당 사용자에 대 한 템플릿 푸시 알림 tooevery 장치 등록을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="4de84-453">인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="4de84-454"><a name="CustomAPI"></a> 사용자 지정 API</span><span class="sxs-lookup"><span data-stu-id="4de84-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="4de84-455"><a name="howto-customapi-basic"></a>방법: 사용자 지정 API 정의</span><span class="sxs-lookup"><span data-stu-id="4de84-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="4de84-456">또한 toohello 데이터 액세스 API hello /tables 끝점을 통해, Azure 모바일 앱에서 사용자 지정 API 검사를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="4de84-457">사용자 지정 Api와 비슷한 방식으로 toohello 테이블 정의에 정의 되어 있고 모든 액세스할 수 있습니다 hello 인증을 비롯 한 동일한 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="4de84-458">Hello에 응용 프로그램 서비스 인증을 구성 해야 toouse 사용자 지정 API를 사용 하는 응용 프로그램 서비스 인증을 원하는 경우 [Azure 포털] 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="4de84-459">Azure 응용 프로그램 서비스에 인증을 구성 하는 방법에 대 한 자세한 내용은 hello id 공급자에 대 한 hello 구성 가이드를 확인 하려는 toouse:</span><span class="sxs-lookup"><span data-stu-id="4de84-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="4de84-460">[어떻게 tooconfigure Azure Active Directory 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="4de84-461">[어떻게 tooconfigure Facebook 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="4de84-462">[어떻게 tooconfigure Google 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="4de84-463">[어떻게 tooconfigure Microsoft 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="4de84-464">[어떻게 tooconfigure Twitter 인증]</span><span class="sxs-lookup"><span data-stu-id="4de84-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="4de84-465">사용자 지정 Api에서 정의 된 hello 같은 방식으로 테이블 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="4de84-466">**api** 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="4de84-466">Create an **api** directory</span></span>
2. <span data-ttu-id="4de84-467">API 정의 JavaScript 파일에는 hello에 만들 **api** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="4de84-468">사용 하 여 hello 가져오기 메서드 tooimport hello **api** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="4de84-469">다음은 이전 사용 되는 hello basic 앱 샘플을 기준으로 hello 프로토타입 api 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="4de84-470">예를 들어 hello를 사용 하 여 hello 서버 날짜를 반환 하는 API 보겠습니다 *Date.now()* 메서드.</span><span class="sxs-lookup"><span data-stu-id="4de84-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="4de84-471">다음은 hello api/date.js 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="4de84-472">각 매개 변수에 hello 표준 RESTful 동사-GET, POST, PATCH 또는 DELETE 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="4de84-473">hello 메서드는 표준 [ExpressJS 미들웨어] 를 보내는 데 필요한 hello 출력 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="4de84-474"><a name="howto-customapi-auth"></a>방법: 액세스 tooa 사용자 지정 API에 인증 필요</span><span class="sxs-lookup"><span data-stu-id="4de84-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="4de84-475">Hello에서 인증을 구현 하는 azure 모바일 앱 SDK hello 테이블 끝점 및 사용자 지정 Api를 모두에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="4de84-476">Hello 이전 섹션에서 개발 된 인증 toohello API를 추가 하려면 추가 **액세스** 속성:</span><span class="sxs-lookup"><span data-stu-id="4de84-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="4de84-477">또한 특정 작업에 인증을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="4de84-478">hello hello 테이블 끝점에 사용 되는 동일한 토큰 따라야 인증을 요구 하는 사용자 지정 Api에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="4de84-479"><a name="howto-customapi-auth"></a>방법: 대용량 파일 업로드 처리</span><span class="sxs-lookup"><span data-stu-id="4de84-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="4de84-480">Azure 모바일 앱 SDK hello를 사용 하 여 [본문 파서 미들웨어](https://github.com/expressjs/body-parser) tooaccept 등록의 본문 콘텐츠를 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="4de84-481">본문-파서 tooaccept 더 큰 파일 업로드를 미리 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="4de84-482">hello 파일은 base-64 전송 하기 전에 인코딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="4de84-483">이 hello 실제 업로드의 hello 크기를 늘리는 (및 따라서 크기를 계산 해야 hello).</span><span class="sxs-lookup"><span data-stu-id="4de84-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="4de84-484"><a name="howto-customapi-sql"></a>방법: 사용자 지정 SQL 문 실행</span><span class="sxs-lookup"><span data-stu-id="4de84-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="4de84-485">Azure 모바일 앱 SDK hello 액세스 toohello 허용 tooexecute 있도록 hello 요청 개체를 통해 전체 컨텍스트 SQL 문을 toohello 정의 된 데이터 공급자를 쉽게 parameterized:</span><span class="sxs-lookup"><span data-stu-id="4de84-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="4de84-486"><a name="Debugging"></a>디버깅, 쉬운 테이블 및 간편한 API</span><span class="sxs-lookup"><span data-stu-id="4de84-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="4de84-487"><a name="howto-diagnostic-logs"></a>방법: Azure Mobile Apps의 디버깅, 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4de84-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="4de84-488">몇 가지 디버깅 및 문제 해결 기술 Node.js 응용 프로그램에 대 한 hello Azure 앱 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="4de84-489">Toohello 문서 tooget Node.js 모바일 백 엔드 문제 해결에서 시작 하는 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4de84-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="4de84-490">[Azure 앱 서비스 모니터링]</span><span class="sxs-lookup"><span data-stu-id="4de84-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="4de84-491">[Azure 앱 서비스에 진단 로그 사용]</span><span class="sxs-lookup"><span data-stu-id="4de84-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="4de84-492">[Visual Studio에서 Azure 앱 서비스 문제 해결]</span><span class="sxs-lookup"><span data-stu-id="4de84-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="4de84-493">Node.js 응용 프로그램에 대 한 액세스 권한이 tooa 다양 한 진단 로그 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="4de84-494">Azure 모바일 앱 Node.js SDK를 사용 하는 hello 내부적으로 [윈스턴] 진단 로깅에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="4de84-495">자동으로 로깅을 hello 설정 하거나 디버그 모드를 사용 하도록 설정 하 여 **MS_DebugMode** hello에 응용 프로그램 설정 tootrue [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="4de84-496">Hello에 hello 진단 로그에에서 생성 된 로그 표시 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="4de84-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>방법: hello Azure 포털에서에서 쉽게 테이블 작업</span><span class="sxs-lookup"><span data-stu-id="4de84-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="4de84-498">Hello 포털에서 쉽게 테이블을 사용 하 여 만들고 hello 포털에서 바로 테이블을 작업할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="4de84-499">도 hello 응용 프로그램 서비스 편집기를 사용 하 여 테이블 작업을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="4de84-500">백 엔드 사이트 설정에서 **쉬운 테이블** 을 클릭하면 테이블을 추가, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="4de84-501">Hello 테이블의에서 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-501">You can also see data in hello table.</span></span>

![쉬운 테이블 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="4de84-503">hello 다음 명령을 사용 하는 테이블에 대 한 hello 명령 모음에서:</span><span class="sxs-lookup"><span data-stu-id="4de84-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="4de84-504">**사용 권한을 변경** -읽기에 대 한 hello 권한을 수정, 삽입, 업데이트 및 hello 테이블에 대 한 작업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="4de84-505">옵션은 tooallow 익명 액세스, toorequire 인증 또는 toodisable 모든 toohello 작업에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="4de84-506">**스크립트를 편집** -hello 테이블에 대 한 hello 스크립트 파일은 hello 응용 프로그램 서비스 편집기에서에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="4de84-507">**스키마 관리** -추가 또는 열 삭제 또는 hello 테이블 인덱스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="4de84-508">**결과 지우기** -기존 테이블을 자릅니다 될 모든 데이터 행을 삭제 하지만 hello 스키마 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="4de84-509">**행 삭제** - 데이터의 개별 행을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="4de84-510">**스트리밍 로그 보기** -toohello 스트리밍 사이트에 대 한 로그 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="4de84-511"><a name="work-easy-apis"></a>방법: hello Azure 포털에서 쉽게 Api를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="4de84-512">Hello 포털에서 쉽게 Api를 사용 하 여 만들고 hello 포털에서 사용자 지정 Api 바로 작업할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="4de84-513">응용 프로그램 서비스 편집기 hello를 사용 하 여 API 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="4de84-514">백 엔드 사이트 설정에서 **쉬운 API** 를 클릭하면 사용자 지정 API 끝점을 추가, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![쉬운 API 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="4de84-516">Hello 포털에서 지정된 된 HTTP 동작에 대 한 액세스 권한을 hello 변경 hello API 스크립트 파일이 응용 프로그램 서비스 편집기에서 편집 하거나 hello 스트리밍 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="4de84-517"><a name="online-editor"></a>방법: hello 응용 프로그램 서비스 편집기에서에서 코드를 편집</span><span class="sxs-lookup"><span data-stu-id="4de84-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="4de84-518">Azure 포털 hello hello 프로젝트 tooyour 로컬 컴퓨터에 다운로드 하지 않고 hello 응용 프로그램 서비스 편집기의에서 Node.js 백 엔드 스크립트 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="4de84-519">tooedit hello 온라인 편집기에서 스크립트 파일:</span><span class="sxs-lookup"><span data-stu-id="4de84-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="4de84-520">모바일 앱 백 엔드 블레이드에서 **모든 설정** > **쉬운 테이블** 또는 **쉬운 API** 중 하나를 클릭하고 테이블 또는 API를 클릭한 다음 **스크립트 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="4de84-521">hello 스크립트 파일 hello 응용 프로그램 서비스 편집기에서에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-521">hello script file is opened in hello App Service Editor.</span></span>

    ![앱 서비스 편집기](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="4de84-523">Hello 온라인 편집기에서 변경 내용을 toohello 코드 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="4de84-524">변경 내용은 입력할 때 자동으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de84-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android 클라이언트 빠른 시작]: app-service-mobile-android-get-started.md
[Apache Cordova 클라이언트 빠른 시작]: app-service-mobile-cordova-get-started.md
[iOS 클라이언트 빠른 시작]: app-service-mobile-ios-get-started.md
[Xamarin.iOS 클라이언트 빠른 시작]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android 클라이언트 빠른 시작]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms 클라이언트 빠른 시작]: app-service-mobile-xamarin-forms-get-started.md
[Windows 스토어 클라이언트 빠른 시작]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[오프 라인 데이터 동기화]: app-service-mobile-offline-data-sync.md
[어떻게 tooconfigure Azure Active Directory 인증]: app-service-mobile-how-to-configure-active-directory-authentication.md
[어떻게 tooconfigure Facebook 인증]: app-service-mobile-how-to-configure-facebook-authentication.md
[어떻게 tooconfigure Google 인증]: app-service-mobile-how-to-configure-google-authentication.md
[어떻게 tooconfigure Microsoft 인증]: app-service-mobile-how-to-configure-microsoft-authentication.md
[어떻게 tooconfigure Twitter 인증]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service 배포 가이드]: ../app-service-web/web-sites-deploy.md
[Azure 앱 서비스 모니터링]: ../app-service-web/web-sites-monitor.md
[Azure 앱 서비스에 진단 로그 사용]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Visual Studio에서 Azure 앱 서비스 문제 해결]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[hello 노드 버전을 지정 합니다.]: ../nodejs-specify-node-version-azure-apps.md
[노드 모듈 사용]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure 포털]: https://portal.azure.com/
[OData]: http://www.odata.org
[프라미스]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[GitHub에 basicapp 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[GitHub에 todo 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[GitHub에서 예제 디렉터리]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Visual Studio 용 Node.js 도구 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js 패키지]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS 미들웨어]: http://expressjs.com/guide/using-middleware.html
[윈스턴]: https://github.com/winstonjs/winston
