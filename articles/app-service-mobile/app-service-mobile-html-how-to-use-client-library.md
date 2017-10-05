---
title: "Azure Mobile Apps용 JavaScript SDK를 사용하는 방법"
description: "Azure Mobile Apps에 v를 사용하는 방법"
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
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="c035f-103">Azure Mobile Apps용 JavaScript 클라이언트 라이브러리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="c035f-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="c035f-104">이 가이드에서는 최신 [Azure Mobile Apps용 JavaScript SDK]를 사용하여 일반적인 시나리오를 수행하는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="c035f-105">Azure Mobile Apps를 처음 접하는 경우 먼저 [Azure Mobile Apps 빠른 시작]을 완료하여 백 엔드를 만들고 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="c035f-106">이 가이드에서는 HTML/JavaScript 웹 응용 프로그램에서 모바일 백 엔드를 사용하는 데 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="c035f-107">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="c035f-107">Supported platforms</span></span>
<span data-ttu-id="c035f-108">브라우저 지원은 주요 브라우저인 Google Chrome, Microsoft Edge, Microsoft Internet Explorer 및 Mozilla Firefox의 최신 버전으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="c035f-109">SDK가 비교적 최신 브라우저와는 호환될 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="c035f-110">패키지는 범용 JavaScript 모듈로 배포되므로 전역, AMD 및 CommonJS 서식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="c035f-111"><a name="Setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="c035f-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="c035f-112">이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="c035f-113">이 가이드에서는 해당 테이블에 이러한 자습서의 테이블과 동일한 스키마가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="c035f-114">`npm` 명령을 통해 Azure Mobile Apps JavaScript SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="c035f-115">또한 라이브러리는 Browserify 및 Webpack과 같은 CommonJS 환경 내에서 ES2015 모듈로 사용할 수 있으며 AMD 라이브러리로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="c035f-116">예:</span><span class="sxs-lookup"><span data-stu-id="c035f-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="c035f-117">또한 우리의 CDN에서 직접 다운로드 하 여 미리 작성 된 버전의 SDK 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="c035f-118"><a name="auth"></a>방법: 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="c035f-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="c035f-119">Azure App Service는 Facebook, Google, Microsoft 계정 및 Twitter와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="c035f-120">테이블에 대해 사용 권한을 설정하여 특정 작업을 위한 액세스를 인증된 사용자로만 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="c035f-121">인증된 사용자의 ID를 사용하여 서버 스크립트에 인증 규칙을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="c035f-122">자세한 내용은 [인증 시작] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c035f-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="c035f-123">두 가지의 인증 흐름, 즉 서버 흐름과 클라이언트 흐름이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="c035f-124">서버 흐름의 경우 공급자의 웹 인증 인터페이스를 사용하므로 인증 경험이 가장 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="c035f-125">클라이언트 흐름의 경우 공급자별 SDK를 사용하므로 Single Sign-On과 같은 장치 특정 기능을 통해 심도 깊은 통합이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="c035f-126"><a name="configure-external-redirect-urls"></a>방법: 외부 리디렉션 URL에 대해 모바일 App Service 구성</span><span class="sxs-lookup"><span data-stu-id="c035f-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="c035f-127">여러 가지 유형의 JavaScript 응용 프로그램은 루프백 기능을 사용하여 OAuth UI 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="c035f-128">이러한 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-128">These capabilities include:</span></span>

* <span data-ttu-id="c035f-129">로컬로 서비스 실행</span><span class="sxs-lookup"><span data-stu-id="c035f-129">Running your service locally</span></span>
* <span data-ttu-id="c035f-130">Ionic Framework와 라이브 다시 로드 사용</span><span class="sxs-lookup"><span data-stu-id="c035f-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="c035f-131">인증을 위해 App Service로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="c035f-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="c035f-132">로컬로 실행하면 기본적으로 App Service 인증이 모바일 앱 백 엔드에서 액세스만 허용하도록 구성되므로 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="c035f-133">다음 단계에 따라 App Service 설정을 변경하여 서버를 로컬로 실행할 때 인증을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="c035f-134">[Azure Portal]에 로그인</span><span class="sxs-lookup"><span data-stu-id="c035f-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="c035f-135">모바일 앱 백 엔드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="c035f-136">**개발 도구** 메뉴에서 **리소스 Explorer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="c035f-137">**이동** 을 클릭하여 새 탭 또는 창에서 모바일 앱 백 엔드에 대한 리소스 Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="c035f-138">앱에 대한 **config** > **authsettings** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="c035f-139">**편집** 단추를 클릭하여 리소스의 편집을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="c035f-140">null이어야 하는 **allowedExternalRedirectUrls** 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="c035f-141">배열에 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="c035f-142">배열의 URL을 서비스 URL로 바꿉니다. 이 예에서 로컬 Node.js 샘플 서비스의 경우 `http://localhost:3000`입니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="c035f-143">또한 앱이 구성된 방식에 따라 Ripple 서비스 또는 기타 URL에 대해 `http://localhost:4400`을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="c035f-144">페이지 맨 위에서 **읽기/쓰기**를 클릭한 후 **PUT**을 클릭하여 업데이트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="c035f-145">또한 CORS 허용 목록 설정에 동일한 루프백 URL을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="c035f-146">[Azure Portal]로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="c035f-147">모바일 앱 백 엔드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="c035f-148">**API** 메뉴에서 **CORS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="c035f-149">빈 **허용된 원본** 텍스트 상자에 각 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="c035f-150">새 텍스트 상자가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-150">A new text box is created.</span></span>
5. <span data-ttu-id="c035f-151">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-151">Click **SAVE**</span></span>

<span data-ttu-id="c035f-152">백 엔드가 업데이트되면 앱에서 새 루프백 URL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c035f-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="c035f-153">[Azure Mobile Apps 빠른 시작]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c035f-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="c035f-154">[인증 시작]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="c035f-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="c035f-155">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="c035f-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="c035f-156">[Azure Mobile Apps용 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="c035f-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
