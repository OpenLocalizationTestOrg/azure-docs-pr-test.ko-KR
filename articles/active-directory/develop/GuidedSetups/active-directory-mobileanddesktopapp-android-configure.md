---
title: "AD aaaAzure v2 Android 시작-구성 | Microsoft Docs"
description: "Android 앱이 액세스 토큰을 얻고 Azure Active Directory v2 끝점에서 액세스 토큰이 필요한 Microsoft Graph API를 한 개 이상 호출할 수 있는 방법"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="5eafd-103">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="5eafd-103">Create an application (Express)</span></span>
<span data-ttu-id="5eafd-104">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="5eafd-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="5eafd-105">Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="5eafd-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="5eafd-106">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5eafd-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="5eafd-107">설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인</span><span class="sxs-lookup"><span data-stu-id="5eafd-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="5eafd-108">Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여</span><span class="sxs-lookup"><span data-stu-id="5eafd-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="5eafd-109">추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)</span><span class="sxs-lookup"><span data-stu-id="5eafd-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="5eafd-110">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="5eafd-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="5eafd-111">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5eafd-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="5eafd-112">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5eafd-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="5eafd-113">설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인</span><span class="sxs-lookup"><span data-stu-id="5eafd-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="5eafd-114">`Add Platform`를 클릭한 다음 `Native Application`을 선택하고 [저장]을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5eafd-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="5eafd-115">(`app` > `java` > *`{host}.{namespace}`*에서) `MainActivity`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5eafd-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="5eafd-116">Hello 대체 *[hello 응용 프로그램 Id 여기 입력]* 로 시작 하는 hello 줄에 `final static String CLIENT_ID` hello 응용 프로그램 id를 방금 등록:</span><span class="sxs-lookup"><span data-stu-id="5eafd-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="5eafd-117">열기 `AndroidManifest.xml` (아래 `app`  >  `manifests`) 활동을 너무 다음 추가 hello`manifest\application` 노드.</span><span class="sxs-lookup"><span data-stu-id="5eafd-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="5eafd-118">이렇게 하면 등록 된 `BrowserTabActivity` tooallow hello OS tooresume hello 인증을 완료 한 후 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="5eafd-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="5eafd-119">Hello에 `BrowserTabActivity`, 대체 `[Enter hello application Id here]` hello 응용 프로그램 id</span><span class="sxs-lookup"><span data-stu-id="5eafd-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
