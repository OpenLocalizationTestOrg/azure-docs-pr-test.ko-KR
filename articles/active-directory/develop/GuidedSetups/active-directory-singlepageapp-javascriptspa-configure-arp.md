---
title: "AD aaaAzure v2 JS SPA 단계별 설치-구성 ARP () | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점(ARP)에 의한 액세스 토큰을 필요로 하는 API를 호출하는 방식"
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="e9318-103">Hello 응용 프로그램의 등록 정보 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="e9318-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="e9318-104">이 단계에서는 응용 프로그램 등록 정보 tooconfigure hello 리디렉션 URL이 필요 고 hello 응용 프로그램 Id tooyour JavaScript SPA 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="e9318-105">리디렉션 URL 구성</span><span class="sxs-lookup"><span data-stu-id="e9318-105">Configure redirect URL</span></span>

<span data-ttu-id="e9318-106">Hello 구성 `Redirect URL` 클릭 한 다음 웹 서버에 따라 index.html 페이지에 대 한 hello url 필드 위에 *업데이트*합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="e9318-107">리디렉션 URL을 얻기 위한 Visual Studio 지침</span><span class="sxs-lookup"><span data-stu-id="e9318-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="e9318-108">tooobtain에 리디렉션 URL을 다음 지침에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="e9318-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="e9318-109">*솔루션 탐색기*hello 프로젝트를 선택 하 고 hello를 살펴보고 `Properties` 창 (키를 눌러 속성 창을 보이지 않으면 `F4`)</span><span class="sxs-lookup"><span data-stu-id="e9318-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="e9318-110">Hello 값에서 복사 `URL` toohello 클립보드:</span><span class="sxs-lookup"><span data-stu-id="e9318-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="e9318-111">![](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="e9318-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="e9318-112">Hello 값으로 붙여는 `Redirect URL` hello이이 페이지의 위쪽에 클릭`Update`</span><span class="sxs-lookup"><span data-stu-id="e9318-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="e9318-113">Python에 대한 리디렉션 URL 설정</span><span class="sxs-lookup"><span data-stu-id="e9318-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="e9318-114">Python에 대 한 명령줄을 통해 hello 웹 서버 포트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="e9318-115">참조에 대 한 hello 포트 8080을 사용 하는이 단계별된 설치 하지만 사용 가능한 다른 포트 무료 toouse 느껴집니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="e9318-116">어떤 경우 든, 아래 지침을 hello tooset hello 응용 프로그램 등록 정보에 리디렉션 URL 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="e9318-117">설정 `http://localhost:8080/` 로 `Redirect URL` 에이 페이지의 맨 위에 hello 또는 사용 하 여 `http://localhost:[port]/` 사용자 지정 TCP 포트를 사용 하는 경우 (여기서 *[port]* 는 TCP 포트 번호를 사용자 지정 하는 hello)를 다음 '업데이트'를 클릭 하 고</span><span class="sxs-lookup"><span data-stu-id="e9318-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="e9318-118">JavaScript SPA 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="e9318-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="e9318-119">라는 파일을 만들어 `msalconfig.js` hello 응용 프로그램 등록 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="e9318-120">Visual Studio, 선택 hello 프로젝트 (프로젝트 루트 폴더)를 사용 하는 인덱스를 마우스 오른쪽 단추로 클릭 하 고 선택: `Add`  >  `New Item`  >  `JavaScript File`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="e9318-121">이름을 `msalconfig.js`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e9318-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="e9318-122">다음 코드 tooyour hello 추가 `msalconfig.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="e9318-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
