---
title: "AD aaaAzure v2 JS SPA 단계별 설치-설치 프로그램 | Microsoft Docs"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>웹 서버 또는 프로젝트 설정

> Toodownload이이 샘플의이 프로젝트를 대신 선호? 
> - [Hello Visual Studio 프로젝트를 다운로드 합니다.](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> 또는
> - [Hello 프로젝트 파일을 다운로드](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) python 로컬 웹 서버에 대 한
>
> 고 toohello 넘어갑니다 [구성 단계](#create-an-application-express) 실행 되기 전에 tooconfigure hello 코드 샘플입니다.

## <a name="prerequisites"></a>필수 조건
로컬 웹 서버와 같은 [Python http.server](https://www.python.org/downloads/), [http-서버](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), 또는 IIS Express와 통합 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 설치가 필요한 toorun이 안내 합니다. 

이 가이드의 지침 Python 및 Visual Studio 2017 모두를 기반으로 하지만 다른 개발 환경 또는 웹 서버 무료 toouse 생각 합니다.

## <a name="create-your-project"></a>프로젝트 만들기 

> ### <a name="option-1-visual-studio"></a>옵션 1: Visual Studio 
> Visual Studio를 사용 하는 새 프로젝트를 만드는 toocreate 새 Visual Studio 솔루션 아래 hello 단계를 수행 하세요.
> 1.    Visual Studio:  `File` > `New` > `Project`
> 2.    `Visual C#\Web`에서 `ASP.NET Web Application (.NET Framework)`을 선택합니다.
> 3.    응용 프로그램의 이름을 지정하고 *확인*을 클릭합니다.
> 4.    `New ASP.NET Web Application`에서 `Empty`를 선택합니다.

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>옵션 2: Python/기타 웹 서버
> 설치 했는지 확인 [Python](https://www.python.org/downloads/), 후 아래 hello 단계를 따릅니다.
> - 폴더 toohost 응용 프로그램을 만듭니다.


## <a name="create-your-single-page-applications-ui"></a>단일 페이지 응용 프로그램의 UI 만들기
1.  JavaScript SPA에 대한 *index.html* 파일을 만듭니다. Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `HTML page` index.html 이라는 이름을 지정
2.  다음 코드 tooyour 페이지 hello를 추가 합니다.
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
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

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
