---
title: "aaaAzure AD v2 JS SPA 단계별 설치-구성 | Microsoft Docs"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="117f6-103">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="117f6-103">Register your application</span></span>

<span data-ttu-id="117f6-104">여러 방법으로 toocreate 응용 프로그램, 그 중 하나를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="117f6-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="117f6-105">옵션 1: 응용 프로그램 등록(기본 모드)</span><span class="sxs-lookup"><span data-stu-id="117f6-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="117f6-106">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="117f6-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="117f6-107">Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="117f6-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="117f6-108">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="117f6-109">있는지 hello 옵션에 대 한 확인 *단계별 설치* 확인</span><span class="sxs-lookup"><span data-stu-id="117f6-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="117f6-110">Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여</span><span class="sxs-lookup"><span data-stu-id="117f6-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="117f6-111">옵션 2: 응용 프로그램 등록(고급 모드)</span><span class="sxs-lookup"><span data-stu-id="117f6-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="117f6-112">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="117f6-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="117f6-113">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="117f6-114">있는지 hello 옵션에 대 한 확인 *단계별 설치* 선택 하지 않으면</span><span class="sxs-lookup"><span data-stu-id="117f6-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="117f6-115">`Add Platform`를 클릭한 다음 `Web`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="117f6-116">Hello 추가 `Redirect URL` 해당 하는 웹 서버에 따라 toohello 응용 프로그램의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="117f6-117">방법에 대 한 지침은 아래 hello 섹션을 참조 하십시오. tooset / Visual Studio 및 Python에서 hello 리디렉션 URL을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="117f6-118">페이지 맨 아래에 있는 *저장*</span><span class="sxs-lookup"><span data-stu-id="117f6-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="117f6-119">리디렉션 URL을 얻기 위한 Visual Studio 지침</span><span class="sxs-lookup"><span data-stu-id="117f6-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="117f6-120">Hello 지침 tooobtain 리디렉션 URL을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="117f6-121">*솔루션 탐색기*hello 프로젝트를 선택 하 고 hello를 살펴보고 `Properties` 창 (키를 눌러 속성 창을 보이지 않으면 `F4`)</span><span class="sxs-lookup"><span data-stu-id="117f6-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="117f6-122">Hello 값에서 복사 `URL` toohello 클립보드:</span><span class="sxs-lookup"><span data-stu-id="117f6-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="117f6-123">![](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="117f6-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="117f6-124">뒤로 toohello 전환 *응용 프로그램 등록 포털* hello 값으로 붙여는 `Redirect URL` '저장'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="117f6-125">Python에 대한 리디렉션 URL 설정</span><span class="sxs-lookup"><span data-stu-id="117f6-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="117f6-126">Python에 대 한 명령줄을 통해 hello 웹 서버 포트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="117f6-127">참조에 대 한 hello 포트 8080을 사용 하는이 단계별된 설치 하지만 사용 가능한 다른 포트 무료 toouse 느껴집니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="117f6-128">어떤 경우 든, 아래 지침을 hello tooset hello 응용 프로그램 등록 정보에 리디렉션 URL 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="117f6-129">뒤로 toohello 전환 *응용 프로그램 등록 포털* 설정 `http://localhost:8080/` 로 `Redirect URL`, 사용 또는 `http://localhost:[port]/` 사용자 지정 TCP 포트를 사용 하는 경우 (여기서 *[port]* 는 hello 사용자 지정 하는 TCP 포트 번호) '저장'를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="117f6-130">JavaScript SPA 구성</span><span class="sxs-lookup"><span data-stu-id="117f6-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="117f6-131">라는 파일을 만들어 `msalconfig.js` hello 응용 프로그램 등록 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="117f6-132">Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `JavaScript File`합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="117f6-133">이름을 `msalconfig.js`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="117f6-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="117f6-134">다음 코드 tooyour hello 추가 `msalconfig.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="117f6-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="117f6-135">대체 <code>Enter_the_Application_Id_here</code> hello 방금 등록 한 응용 프로그램 Id로</span><span class="sxs-lookup"><span data-stu-id="117f6-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
