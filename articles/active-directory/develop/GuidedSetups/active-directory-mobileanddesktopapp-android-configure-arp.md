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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="e6b8b-103">Hello 응용 프로그램의 등록 정보 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="e6b8b-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="e6b8b-104">이 단계에서는 tooadd hello 클라이언트 ID tooyour 프로젝트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6b8b-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="e6b8b-105">(`app` > `java` > *`{host}.{namespace}`*에서) `MainActivity`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6b8b-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="e6b8b-106">로 시작 하는 hello 줄 `final static String CLIENT_ID` 사용:</span><span class="sxs-lookup"><span data-stu-id="e6b8b-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="e6b8b-107">다음을 엽니다. `app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="e6b8b-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="e6b8b-108">추가 활동을 너무 다음 hello`manifest\application` 노드.</span><span class="sxs-lookup"><span data-stu-id="e6b8b-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="e6b8b-109">이 레지스터는 `BrowserTabActivity` tooallow hello OS tooresume hello 인증을 완료 한 후 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="e6b8b-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

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

### <a name="what-is-next"></a><span data-ttu-id="e6b8b-110">다음 내용</span><span class="sxs-lookup"><span data-stu-id="e6b8b-110">What is Next</span></span>

[<span data-ttu-id="e6b8b-111">테스트 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e6b8b-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
