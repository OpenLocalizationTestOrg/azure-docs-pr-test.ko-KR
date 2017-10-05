---
title: "Azure AD v2 JS SPA 단계별 설치 - 구성(ARP) | Microsoft Docs"
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="8b5c2-103">앱에 응용 프로그램의 등록 정보 추가</span><span class="sxs-lookup"><span data-stu-id="8b5c2-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="8b5c2-104">이 단계에서는 응용 프로그램 등록 정보의 리디렉션 URL을 구성하고 JavaScript SPA 응용 프로그램에 응용 프로그램 ID를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="8b5c2-105">리디렉션 URL 구성</span><span class="sxs-lookup"><span data-stu-id="8b5c2-105">Configure redirect URL</span></span>

<span data-ttu-id="8b5c2-106">웹 서버에 따라 index.html 페이지에 대한 URL로 위의 `Redirect URL` 필드를 구성하고 *업데이트*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="8b5c2-107">리디렉션 URL을 얻기 위한 Visual Studio 지침</span><span class="sxs-lookup"><span data-stu-id="8b5c2-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="8b5c2-108">리디렉션 URL을 가져오려면 아래 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="8b5c2-109">*솔루션 탐색기*에서 프로젝트를 선택하고 `Properties` 창을 확인합니다([속성] 창이 보이지 않으면 `F4` 누르기).</span><span class="sxs-lookup"><span data-stu-id="8b5c2-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="8b5c2-110">`URL`의 값을 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="8b5c2-111">![](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c2-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="8b5c2-112">값을 이 페이지 맨 위에 `Redirect URL`로 붙여 넣고 `Update`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="8b5c2-113">Python에 대한 리디렉션 URL 설정</span><span class="sxs-lookup"><span data-stu-id="8b5c2-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="8b5c2-114">Python의 경우 명령줄을 통해 웹 서버 포트를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="8b5c2-115">이 단계별 설치는 참조를 위해 포트 8080을 사용하지만 다른 포트도 자유롭게 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="8b5c2-116">어떤 경우든, 아래 지침에 따라 응용 프로그램 등록 정보에 리디렉션 URL을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="8b5c2-117">이 페이지 맨 위에서 `http://localhost:8080/`을 `Redirect URL`로 설정하거나 사용자 지정 TCP 포트를 사용하는 경우 `http://localhost:[port]/`를 사용하고(여기서 *[port]*는 사용자 지정 TCP 포트 번호임) [업데이트]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="8b5c2-118">JavaScript SPA 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="8b5c2-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="8b5c2-119">응용 프로그램 등록 정보를 포함하는 `msalconfig.js`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="8b5c2-120">Visual Studio를 사용하는 경우 프로젝트(프로젝트 루트 폴더)를 마우스 오른쪽 단추로 클릭하고 `Add` > `New Item` > `JavaScript File`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="8b5c2-121">이름을 `msalconfig.js`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="8b5c2-122">`msalconfig.js` 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b5c2-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
