---
title: "Azure AD v2 JS SPA 단계별 설치 - 설치 | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: fc9f88cc8d23abcfa8ea30e346192732b422ffa2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="3c354-103">웹 서버 또는 프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="3c354-103">Setting up your web server or project</span></span>

> <span data-ttu-id="3c354-104">이 샘플의 프로젝트를 다운로드하고 싶으세요?</span><span class="sxs-lookup"><span data-stu-id="3c354-104">Prefer to download this sample's project instead?</span></span> 
> - [<span data-ttu-id="3c354-105">Visual Studio 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="3c354-105">Download the Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="3c354-106">또는</span><span class="sxs-lookup"><span data-stu-id="3c354-106">or</span></span>
> - <span data-ttu-id="3c354-107">로컬 웹 서버(예: python)용 [프로젝트 파일 다운로드](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip)</span><span class="sxs-lookup"><span data-stu-id="3c354-107">[Download the project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="3c354-108">그런 후 [구성 단계](#create-an-application-express)로 건너뛰어 실행 전에 코드 샘플을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-108">And then  skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c354-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3c354-109">Prerequisites</span></span>
<span data-ttu-id="3c354-110">이 단계별 설치를 실행하려면 [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core) 또는 IIS Express와 같은 로컬 웹 서버가 [Visual Studio 2017](https://www.visualstudio.com/downloads/)과 통합되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required to run this guided setup.</span></span> 

<span data-ttu-id="3c354-111">이 가이드의 지침은 Python 및 Visual Studio 2017 둘 다를 기준으로 하지만 다른 개발 환경 또는 웹 서버를 사용해도 무방합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free to use any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="3c354-112">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3c354-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="3c354-113">옵션 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c354-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="3c354-114">Visual Studio를 사용하며 새 프로젝트를 만드는 경우 아래 단계에 따라 새 Visual Studio 솔루션을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="3c354-114">If you are using Visual Studio and are creating a new project, follow the steps below to create a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="3c354-115">Visual Studio:  `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="3c354-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="3c354-116">`Visual C#\Web`에서 `ASP.NET Web Application (.NET Framework)`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="3c354-117">응용 프로그램의 이름을 지정하고 *확인*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="3c354-118">`New ASP.NET Web Application`에서 `Empty`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="3c354-119">옵션 2: Python/기타 웹 서버</span><span class="sxs-lookup"><span data-stu-id="3c354-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="3c354-120">[Python](https://www.python.org/downloads/)을 설치했는지 확인한 후 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow the step below:</span></span>
> - <span data-ttu-id="3c354-121">응용 프로그램을 호스트할 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-121">Create a folder to host your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="3c354-122">단일 페이지 응용 프로그램의 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="3c354-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="3c354-123">JavaScript SPA에 대한 *index.html* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="3c354-124">Visual Studio를 사용하는 경우 프로젝트(프로젝트 루트 폴더)를 마우스 오른쪽 단추로 클릭하고 `Add` > `New Item` > `HTML page`을 선택하고 이름을 index.html로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-124">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="3c354-125">페이지에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c354-125">Add the following code to your page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling the page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn to reference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- The 'bluebird' and 'fetch' references below are required if you need to run this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
