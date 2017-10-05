---
title: "Azure AD v2 Android 시작 - 구성 | Microsoft Docs"
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
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a>앱에 응용 프로그램의 등록 정보 추가

이 단계에서는 프로젝트에 클라이언트 ID를 추가해야 합니다.

1.  (`app` > `java` > *`{host}.{namespace}`*에서) `MainActivity`를 엽니다.
2.  `final static String CLIENT_ID`로 시작하는 줄을 다음으로 바꿉니다.
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. 다음을 엽니다. `app` > `manifests` > `AndroidManifest.xml`
4. 다음 작업을 `manifest\application` 노드에 추가합니다. 이렇게 하면 OS에서 인증 완료 후 응용 프로그램을 다시 시작할 수 있도록 `BrowserTabActivity`가 등록됩니다.

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a>다음 내용

[테스트 및 유효성 검사](active-directory-mobileanddesktopapp-android-test.md)
