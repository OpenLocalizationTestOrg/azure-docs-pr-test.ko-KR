---
title: "aaaHow tooUse hello Azure 모바일 앱 용 JavaScript SDK"
description: "어떻게 Azure 모바일 앱에 대 한 tooUse v"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="520e3-103">TooUse는 Azure 모바일 앱 용 JavaScript 클라이언트 라이브러리를 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="520e3-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="520e3-104">이 가이드 최신 버전의 hello를 사용 하 여 tooperform 일반적인 시나리오에 설명 [Azure 모바일 앱 용 JavaScript SDK]합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="520e3-105">새로운 tooAzure 모바일 앱의 경우 먼저 완료 [Azure 모바일 앱 빠른 시작] toocreate 백 엔드 고 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="520e3-106">이 가이드에서는 hello 모바일 백 엔드를 사용 하 여 HTML/JavaScript 웹 응용 프로그램에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="520e3-107">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="520e3-107">Supported platforms</span></span>
<span data-ttu-id="520e3-108">브라우저 지원 toohello 현재 제한 하 고 마지막 버전의 hello 주요 브라우저: Google Chrome, Microsoft Edge, Microsoft Internet Explorer 및 Mozilla Firefox 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="520e3-109">상대적으로 최신 브라우저와 SDK toofunction hello 라고 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="520e3-110">hello 패키지는 전역, AMD 지원 하 고 CommonJS 형식을 지정 하므로 유니버설 JavaScript 모듈로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="520e3-111"><a name="Setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="520e3-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="520e3-112">이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="520e3-113">이 가이드에서는 해당 hello 테이블에 hello 가정 해당 자습서의 hello 테이블이 동일한 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="520e3-114">Hello Azure 모바일 앱의 JavaScript SDK 설치 hello를 통해 수행할 수 있습니다 `npm` 명령:</span><span class="sxs-lookup"><span data-stu-id="520e3-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="520e3-115">hello 라이브러리를 ES2015 모듈로 Browserify 등 시스템용 및 AMD 라이브러리로 CommonJS 환경 내에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="520e3-116">예:</span><span class="sxs-lookup"><span data-stu-id="520e3-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="520e3-117">또한 우리의 CDN에서 직접 다운로드 하 여 미리 작성 된 버전의 hello SDK 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="520e3-118"><a name="auth"></a>방법: 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="520e3-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="520e3-119">Azure App Service는 Facebook, Google, Microsoft 계정 및 Twitter와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="520e3-120">권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="520e3-121">서버 스크립트에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="520e3-122">자세한 내용은 참조 hello [인증 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="520e3-123">두 가지의 인증 흐름, 즉 서버 흐름과 클라이언트 흐름이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="520e3-124">hello 서버 흐름 hello 공급자의 웹 인증 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="520e3-125">hello 클라이언트 흐름 고려한 장치 전용 기능이 있는 밀접 하 게 통합와 같은 단일 로그온 공급자별 Sdk를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="520e3-126"><a name="configure-external-redirect-urls"></a>방법: 외부 리디렉션 URL에 대해 모바일 App Service 구성</span><span class="sxs-lookup"><span data-stu-id="520e3-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="520e3-127">여러 유형의 JavaScript 응용 프로그램 UI OAuth 흐름 루프백 기능 toohandle를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="520e3-128">이러한 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-128">These capabilities include:</span></span>

* <span data-ttu-id="520e3-129">로컬로 서비스 실행</span><span class="sxs-lookup"><span data-stu-id="520e3-129">Running your service locally</span></span>
* <span data-ttu-id="520e3-130">라이브 다시 로드를 사용 하 여 Ionic 프레임 워크 hello로</span><span class="sxs-lookup"><span data-stu-id="520e3-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="520e3-131">인증에 대 한 서비스 tooApp을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="520e3-132">로컬로 실행 중 앱 서비스 인증은 기본적으로 모바일 앱 백 엔드에서 tooallow 액세스를 구성 하기 때문에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="520e3-133">Hello 단계 toochange hello 응용 프로그램 서비스 설정 tooenable 인증 hello 서버를 로컬로 실행 하는 경우 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="520e3-134">Toohello 로그인 [Azure 포털]</span><span class="sxs-lookup"><span data-stu-id="520e3-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="520e3-135">모바일 앱 백 엔드에서 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="520e3-136">선택 **리소스 탐색기** hello에 **개발 도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="520e3-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="520e3-137">클릭 **이동** 새 탭 또는 창에서 모바일 앱 백 엔드에 대 한 tooopen hello 리소스 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="520e3-138">Hello 확장 **config** > **authsettings** 응용 프로그램에 대 한 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="520e3-139">Hello 클릭 **편집** tooenable hello 리소스의 편집 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="520e3-140">Hello **allowedExternalRedirectUrls** 요소는 null 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="520e3-141">배열에 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="520e3-142">이 예제는 서비스의 url이 hello hello 배열의 hello Url 바꾸기 `http://localhost:3000` hello 로컬 Node.js 샘플 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="520e3-143">사용 해도 `http://localhost:4400` hello Ripple 서비스 또는 응용 프로그램 구성 된 방식에 따라 다른 URL에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="520e3-144">Hello hello 페이지의 위쪽에 클릭 **읽기/쓰기**, 클릭 **배치** toosave 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="520e3-145">또한 tooadd 해야 hello toohello CORS 허용 목록 설정에 대 한 동일한의 루프백 Url:</span><span class="sxs-lookup"><span data-stu-id="520e3-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="520e3-146">뒤로 toohello 이동 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="520e3-147">모바일 앱 백 엔드에서 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="520e3-148">클릭 **CORS** hello에 **API** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="520e3-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="520e3-149">빈 hello에 각 URL을 입력 **허용 된 원본을** 입력란.</span><span class="sxs-lookup"><span data-stu-id="520e3-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="520e3-150">새 텍스트 상자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-150">A new text box is created.</span></span>
5. <span data-ttu-id="520e3-151">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-151">Click **SAVE**</span></span>

<span data-ttu-id="520e3-152">Hello 백 엔드 업데이트 후에 응용 프로그램에서 수 toouse hello 새 루프백 Url 됩니다.</span><span class="sxs-lookup"><span data-stu-id="520e3-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure 모바일 앱 빠른 시작]: app-service-mobile-cordova-get-started.md
[인증 시작]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure 포털]: https://portal.azure.com/
[Azure 모바일 앱 용 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
