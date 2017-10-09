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
## <a name="create-an-application-express"></a>응용 프로그램(Express) 만들기
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  응용 프로그램 이름과 메일을 입력합니다.
3.  설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인
4.  Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)
이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:
1. Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램
2. 응용 프로그램 이름과 메일을 입력합니다. 
3. 설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인
4. `Add Platform`를 클릭한 다음 `Native Application`을 선택하고 [저장]을 누릅니다.
5.  (`app` > `java` > *`{host}.{namespace}`*에서) `MainActivity`를 엽니다.
6.  Hello 대체 *[hello 응용 프로그램 Id 여기 입력]* 로 시작 하는 hello 줄에 `final static String CLIENT_ID` hello 응용 프로그램 id를 방금 등록:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
열기 `AndroidManifest.xml` (아래 `app`  >  `manifests`) 활동을 너무 다음 추가 hello`manifest\application` 노드. 이렇게 하면 등록 된 `BrowserTabActivity` tooallow hello OS tooresume hello 인증을 완료 한 후 응용 프로그램:
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
Hello에 `BrowserTabActivity`, 대체 `[Enter hello application Id here]` hello 응용 프로그램 id
</li>
</ol>
