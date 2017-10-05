---
title: "Azure Mobile Apps용 Apache Cordova 플러그인 사용 방법"
description: "Azure Mobile Apps용 Apache Cordova 플러그인 사용 방법"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="f93de-103">Azure Mobile Apps용 Apache Cordova 클라이언트 라이브러리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f93de-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="f93de-104">이 가이드에서는 최신 [Azure Mobile Apps용 Apache Cordova 플러그 인]을 사용하여 일반적인 시나리오를 수행하는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="f93de-105">Azure Mobile Apps를 처음 접하는 경우 먼저 [Mobile Apps 빠른 시작]을 완료하여 백 엔드를 만들고, 테이블을 만든 다음 미리 빌드된 Apache Cordova 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="f93de-106">이 가이드에서는 클라이언트 쪽 Apache Cordova 플러그 인에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="f93de-107">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="f93de-107">Supported platforms</span></span>
<span data-ttu-id="f93de-108">이 SDK는 iOS, Android 및 Windows 장치에서 Apache Cordova v6.0.0 이상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="f93de-109">지원되는 플랫폼은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-109">The platform support is as follows:</span></span>

* <span data-ttu-id="f93de-110">Android API 19-24(Nougat를 통한 KitKat)</span><span class="sxs-lookup"><span data-stu-id="f93de-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="f93de-111">iOS 버전 8.0 이상.</span><span class="sxs-lookup"><span data-stu-id="f93de-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="f93de-112">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="f93de-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="f93de-113">범용 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="f93de-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="f93de-114"><a name="Setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="f93de-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="f93de-115">이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="f93de-116">이 가이드에서는 해당 테이블에 이러한 자습서의 테이블과 동일한 스키마가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="f93de-117">또한 이 가이드는 사용자 코드에 Apache Cordova 플러그 인을 추가했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="f93de-118">아직 추가하지 않은 경우 명령줄에서 프로젝트에 Apache Cordova 플러그 인을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="f93de-119">[첫 번째 Apache Cordova 앱]을 만드는 방법에 대한 자세한 내용은 해당 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f93de-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="f93de-120"><a name="ionic"></a>Ionic v2 앱 설정</span><span class="sxs-lookup"><span data-stu-id="f93de-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="f93de-121">Ionic v2 프로젝트를 올바르게 구성하려면 먼저 기본 앱을 만들고 Cordova 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="f93de-122">`app.component.ts`에 다음 줄을 추가하여 클라이언트 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="f93de-123">이제 프로젝트를 빌드한 후 브라우저에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="f93de-124">Azure Mobile Apps Cordova 플러그 인은 Ionic v1 및 v2 앱을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="f93de-125">Ionic v2 앱에만 `WindowsAzure` 개체에 대한 추가 선언이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="f93de-126"><a name="auth"></a>방법: 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="f93de-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="f93de-127">Azure App Service는 Facebook, Google, Microsoft 계정 및 Twitter와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="f93de-128">테이블에 대해 사용 권한을 설정하여 특정 작업을 위한 액세스를 인증된 사용자로만 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="f93de-129">인증된 사용자의 ID를 사용하여 서버 스크립트에 인증 규칙을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="f93de-130">자세한 내용은 [인증 시작] 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f93de-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="f93de-131">Apache Cordova 앱에 인증을 사용할 때는 다음 Cordova 플러그 인을 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="f93de-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="f93de-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="f93de-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="f93de-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="f93de-134">두 가지의 인증 흐름, 즉 서버 흐름과 클라이언트 흐름이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="f93de-135">서버 흐름의 경우 공급자의 웹 인증 인터페이스를 사용하므로 인증 경험이 가장 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="f93de-136">클라이언트 흐름의 경우 공급자 특정 장치별 SDK를 사용하므로 Single Sign-On과 같은 장치 특정 기능을 통해 심도 깊은 통합이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="f93de-137"><a name="configure-external-redirect-urls"></a>방법: 외부 리디렉션 URL에 대해 모바일 App Service 구성</span><span class="sxs-lookup"><span data-stu-id="f93de-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="f93de-138">여러 가지 유형의 Apache Cordova 응용 프로그램은 루프백 기능을 사용하여 OAuth UI 흐름을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="f93de-139">기본적으로 인증 서비스만 사용자 서비스의 활용 방법을 알기 때문에 localhost의 OAuth UI 흐름에 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="f93de-140">다음은 문제가 있는 OAuth UI 흐름의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="f93de-141">Ripple 에뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="f93de-141">The Ripple emulator.</span></span>
* <span data-ttu-id="f93de-142">Ionic을 사용하여 라이브 다시 로드.</span><span class="sxs-lookup"><span data-stu-id="f93de-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="f93de-143">로컬에서 모바일 백엔드 실행</span><span class="sxs-lookup"><span data-stu-id="f93de-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="f93de-144">인증을 제공하지 않는 다른 Azure App Service에서 모바일 백 엔드 실행.</span><span class="sxs-lookup"><span data-stu-id="f93de-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="f93de-145">구성에 로컬 설정을 추가하려면 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="f93de-146">[Azure Portal]에 로그인</span><span class="sxs-lookup"><span data-stu-id="f93de-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="f93de-147">**모든 리소스** 또는 **App Services**를 선택한 후 모바일 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="f93de-148">**도구** 클릭</span><span class="sxs-lookup"><span data-stu-id="f93de-148">Click **Tools**</span></span>
4. <span data-ttu-id="f93de-149">관찰 메뉴에서 **리소스 Explorer**를 클릭한 다음 **이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="f93de-150">새 창 또는 탭이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="f93de-151">왼쪽 탐색 창에서 사이트에 대한 **config**, **authsettings** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="f93de-152">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-152">Click **Edit**</span></span>
7. <span data-ttu-id="f93de-153">"allowedExternalRedirectUrls" 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="f93de-154">null 또는 일련의 값으로 설정되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="f93de-155">이 값을 다음 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="f93de-156">URL을 서비스의 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="f93de-157">예를 들면 " http://localhost:3000 "(Node.js 샘플 서비스) 또는 " http://localhost:4400 "(Ripple 서비스)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="f93de-158">그러나 이러한 URL은 예제일 뿐입니다. 예에서 언급된 서비스를 포함하여 사용자의 상황이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="f93de-159">화면 오른쪽 위에 있는 **읽기/쓰기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="f93de-160">녹색 **배치** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="f93de-161">이 시점에서 설정이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-161">The settings are saved at this point.</span></span>  <span data-ttu-id="f93de-162">설정 저장이 완료될 때까지 브라우저 창을 닫지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="f93de-163">또한 App Service에 대한 CORS 설정에 이러한 루프백 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="f93de-164">[Azure Portal]에 로그인</span><span class="sxs-lookup"><span data-stu-id="f93de-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="f93de-165">**모든 리소스** 또는 **App Services**를 선택한 후 모바일 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="f93de-166">설정 블레이드가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="f93de-167">자동으로 열리지 않으면 **모든 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="f93de-168">API 메뉴에서 **CORS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="f93de-169">제공된 입력란에 추가할 URL을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="f93de-170">필요에 따라 추가 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="f93de-171">**저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="f93de-172">새 설정이 적용되는 데는 약 10~15초가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="f93de-173"><a name="register-for-push"></a>방법: 푸시 알림 등록</span><span class="sxs-lookup"><span data-stu-id="f93de-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="f93de-174">푸시 알림을 처리하기 위해 [phonegap-plugin-push]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="f93de-175">이 플러그인은 명령줄에서 `cordova plugin add` 명령을 사용하거나 Visual Studio 내에서 Git 플러그 인 설치 관리자를 통해 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="f93de-176">Apache Cordova 앱에서 다음 코드는 푸시 알림을 위해 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="f93de-177">알림 허브 SDK를 사용하여 서버에서 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="f93de-178">클라이언트에서 직접 푸시 알림을 보내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f93de-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="f93de-179">이렇게 하면 Notification Hubs 또는 PNS에 대한 서비스 거부 공격을 트리거하는 데 이용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="f93de-180">이러한 공격의 결과로 PNS가 트래픽을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="f93de-181">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f93de-181">More information</span></span>

<span data-ttu-id="f93de-182">우리의 [API 설명서](http://azure.github.io/azure-mobile-apps-js-client/)에서 자세한 API 세부 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f93de-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="f93de-183">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f93de-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="f93de-184">[Mobile Apps 빠른 시작]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f93de-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="f93de-185">[인증 시작]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="f93de-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="f93de-186">[Azure Mobile Apps용 Apache Cordova 플러그 인]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="f93de-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="f93de-187">[첫 번째 Apache Cordova 앱]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="f93de-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="f93de-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="f93de-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="f93de-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="f93de-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="f93de-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="f93de-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
