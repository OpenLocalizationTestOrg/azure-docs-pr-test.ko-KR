---
title: "aaaWhat은 hello Azure AD v2.0 끝점에 차이가 있는? | Microsoft Docs"
description: "Hello 원래 Azure AD와 hello v2.0 끝점 간의 비교 합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Hello v2.0 끝점에 대 한 다른 무엇입니까?
Azure Active Directory에 익숙한 hello 이전에 Azure AD와 응용 프로그램을 통합 한 경우 예상 하지 않고 hello v2.0 끝점에 차이가 있을 수 있습니다.  이 문서는 이러한 차이의 이해를 돕기 위해 작성되었습니다.

> [!NOTE]
> 모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.  에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Microsoft 계정과 Azure AD 계정
hello v2.0 끝점 toowrite 앱 로그인 단일 인증 끝점을 사용 하 여 Microsoft 계정과 Azure AD 계정에서 허용 하는 개발자를 수 있습니다.  이렇게 하면 기능 toowrite 앱 완전히 계정을 알 수 없는; hello 사용자가 로그인에 hello 계정의 hello 유형의 무시 수 있습니다.  물론, 있습니다 *수* hello 유형의 특정 세션에서 사용 되는 계정 인식 응용 프로그램을 만들 수 있지만 필요가 없습니다.

예를 들어, 앱 hello를 호출 하는 경우 [Microsoft Graph](https://graph.microsoft.io), 몇 가지 추가 기능 및 데이터에는 해당 SharePoint 사이트나 디렉터리 데이터와 같은 사용 가능한 tooenterprise 사용자가 됩니다.  하지만 많은 동작에 대 한와 같은 [사용자의 메일 읽기](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), hello 코드를 정확 하 게 작성할 수 있습니다. Microsoft 계정과 Azure AD 계정에 대 한 hello 동일 합니다.  

이제 간단한 하나의 프로세스를 통해 Microsoft 계정과 Azure AD 계정을 사용하여 앱을 통합할 수 있습니다.  끝점, 단일 라이브러리 및는 단일 응용 프로그램 등록 toogain 액세스 tooboth hello 소비자 및 엔터프라이즈 세계의 단일 집합을 사용할 수 있습니다.  hello v2.0 끝점, 체크 아웃에 대해 더 알아봅니다 toolearn [개요 hello](active-directory-appmodel-v2-overview.md)합니다.

## <a name="new-app-registration-portal"></a>새 앱 등록 포털
tooregister hello v2.0 끝점을 사용 하는 응용 프로그램을 새 응용 프로그램 등록 포털을 사용 해야: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)합니다.  이 hello 포털 응용 프로그램 ID를 가져올 수 있는 응용 프로그램의 로그인 페이지 등의 hello 모양을 사용자 지정 합니다.  하기만 하면 tooaccess hello 포털 전원이 Microsoft 계정-개인 또는 작업/학교 계정입니다.

## <a name="one-app-id-for-all-platforms"></a>모든 플랫폼에 대한 하나의 앱 ID
Azure Active Directory를 사용한 경우 단일 프로젝트에 여러 가지 다른 앱을 등록했었습니다.  예를 들어 웹 사이트와 iOS 앱을 빌드한 경우 했던 tooregister에 두 개의 서로 다른 응용 프로그램 Id를 사용 하 여 별도로, 합니다. hello Azure AD 응용 프로그램 등록 포털 등록 중 toomake 있습니다 이러한 구분 강제:

![이전 응용 프로그램 등록 UI](../../media/active-directory-v2-flows/old_app_registration.PNG)

마찬가지로 웹 사이트와 백 엔드 웹 API가 있는 경우 Azure AD의 개별 앱처럼 각각 따로 등록해야 했습니다.  또는 iOS 앱과 안드로이드 앱이 있는 경우도 마찬가지로 다른 두 개의 앱에 등록해야 했습니다.  응용 프로그램의 각 구성 요소를 등록 하는 중이 어 졌 toosome 개발자와 고객에 대 한 예기치 않은 동작:

* 각 구성 요소는 각 고객의 hello Azure Active Directory 테 넌 트에 별도 응용 프로그램으로 표시 되었습니다.
* Toodo 업로드 테 넌 트 관리자에 대 한 액세스를 관리 하거나 응용 프로그램을 삭제 하려면 tooapply 정책을 시도 하므로 hello 응용 프로그램의 각 구성 요소에 대 한 합니다.
* 고객이 동의한 tooan 응용 프로그램을 하는 경우 각 구성 요소는 고유한 응용 프로그램으로 hello 동의 화면에 나타납니다.

Hello v2.0 끝점과 단일 응용 프로그램 등록으로 프로젝트의 모든 구성 요소를 등록 하 고 전체 프로젝트에 대 한 단일 응용 프로그램 Id를 사용 하 여 이제 있습니다.  여러 "플랫폼" tooa 각 프로젝트를 추가 하 고 추가한 각 플랫폼에 대 한 hello 적절 한 데이터를 제공.  물론, 요구 사항에 따라 있지만 hello 대부분의 경우 하나의 응용 프로그램 Id 해야 할 수 만큼 앱을 만들 수 있습니다.

목표를 두고는이 됩니다 간체 tooa 더 많은 앱 관리 되며 개발 환경에서 작업할 수 있는 단일 프로젝트의 더 통합 된 보기를 만들입니다.

## <a name="scopes-not-resources"></a>리소스가 아닌 범위
Azure Active Directory에서 앱은 **리소스** 또는 토큰 수신자로 작동할 수 있습니다.  리소스의 수를 정의할 수 **범위** 또는 **oAuth2Permissions** 자신이 이해 하 toorequest 토큰 toothat 리소스의 범위는 특정 집합에 대 한 클라이언트 앱을 허용 합니다.  리소스의 예를 들어 hello Azure AD Graph API를 고려 합니다.

* 리소스 식별자, 또는 `AppID URI`: `https://graph.windows.net/` 
* 범위, 또는 `OAuth2Permissions`: `Directory.Read`, `Directory.Write` 등.  

이 모든 hello hello v2.0 끝점에 대 한도 마찬가지입니다.  앱은 여전히 리소스로 작동하고, 범위를 정의하고, URI로 식별될 수 있습니다.  클라이언트 응용 프로그램 액세스 toothose 범위를 요청할 여전히 수 있습니다.  그러나 클라이언트가 해당 권한을 요청 하는 hello 방식으로 변경 되었습니다.  Hello 지난, OAuth 2.0 요청 tooAzure AD 같은 보지 못했을 수 있습니다를 승인:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

여기서 hello **리소스** 매개 변수는 리소스 hello 클라이언트 응용 프로그램에 대 한 권한 부여 요청을 표시 합니다.  Azure AD는 hello Azure 포털에서에서 정적 구성에 따라 하 고 그에 따라 발급 된 토큰 hello 응용 프로그램에 필요한 hello 권한을 계산 합니다.  이제 hello 같은 OAuth 2.0 권한 부여 요청 같습니다.

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

여기서 hello **범위** 매개 변수는 리소스 및 사용 권한 hello 앱에 대 한 권한 부여 요청을 나타냅니다. hello는 리소스는 hello 요청에 있는 매우 여전히-hello hello 범위 매개 변수 값의 각 롤포워드되지 단순히 않았습니다 원하는입니다.  이런이 방식으로 hello scope 매개 변수를 사용 하 여 hello v2.0 끝점 toobe hello OAuth 2.0 사양 보다 규격 허용과 업계의 일반적인 사례 보다 긴밀 하 게 정렬 합니다.  앱 tooperform 해줍니다 [증분 동의](#incremental-and-dynamic-consent), hello 다음 섹션에 설명 합니다.

## <a name="incremental-and-dynamic-consent"></a>증분 및 동적 동의
응용 프로그램 작성 시 hello Azure 포털의 필요한 OAuth 2.0 권한을 toospecify 필요한 이전에 Azure AD에에서 등록 하는 응용 프로그램:

![권한 등록 UI](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

hello 사용 권한이 필요한 응용 프로그램 구성 된 **정적으로**합니다.  Hello Azure 포털에서에서 hello 앱 tooexist의 구성을 허용이 깔끔하고 단순 hello 코드를 유지 하는 동안 개발자를 위한 몇 가지 문제를 제공 합니다.

* 응용 프로그램에 tooknow 모든 hello 권한이 응용 프로그램을 만들 때 필요한 것입니다.  시간의 경과에 따라 권한을 추가하는 것은 어려운 작업이었습니다.
* 응용 프로그램에 tooknow 모든 것도 액세스 하는 것 보다 앞선 시간 hello 리소스입니다.  임의 개수의 리소스를 액세스할 수 있는 어려운 toocreate 앱 있었습니다.
* 응용 프로그램 toorequest 모든 hello 사용 권한을 hello 사용자의 첫 번째 로그인 시 필요한 것을 했습니다.  일부 경우에이 어 졌 최종 사용자는 초기 로그인에 대 한 hello 응용 프로그램의 액세스를 허용 하지 않는 것이 권한의 tooa 매우 긴 목록입니다.

Hello v2.0 끝점과 hello 권한을 지정할 수 있습니다 응용 프로그램 요구 사항 **동적으로**, 응용 프로그램의 일반 사용 하는 동안 런타임에 합니다.  toodo hello hello에 포함 하 여 특정된 시점에서 응용 프로그램 요구 사항 시간에서 범위를 지정할 수는 따라서 `scope` 의 권한 부여 요청 매개 변수:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

위의 hello Azure AD 사용자의 디렉터리 데이터 뿐만 아니라 데이터 tootheir 디렉터리 쓰기 앱 tooread hello에 대 한 권한을 요청합니다.  Hello 사용자가 지난 hello에서 toothose 권한을 동의 하는 경우이 특정 응용 프로그램에 대 한 자격 증명을 입력 하기만 하면 됩니다 하며 hello 앱에 서명 합니다.  Hello 사용자가 이러한 사용 권한은 tooany 동의 하지, hello v2.0 끝점 동의 toothose 사용 권한에 대 한 hello 사용자 라는 표시 됩니다.  더 많은 toolearn까지 읽을 수 있습니다에 [권한과 승인 범위](active-directory-v2-scopes.md)합니다.

응용 프로그램 hello 통해 동적으로 toorequest 권한을 허용 `scope` 매개 변수는 사용자의 경험에 대 한 모든 권한을 제공 합니다.  원하는 경우 사용자가 동의 하 고 한 초기 인증 요청에 모든 권한을 요청할 toofrontload를 선택할 수 있습니다.  또는 앱에 권한 수가 많은 필요한 경우 선택할 수 있습니다 toogather 사용 권한만 hello 사용자 로부터 증분, 시간이 지남에 따라 toouse 응용 프로그램의 특정 기능을 시도할 때.

## <a name="well-known-scopes"></a>잘 알려진 범위
#### <a name="offline-access"></a>오프라인 액세스
앱 hello v2.0 끝점을 사용 하는 hello 사용 해야 새로운 잘 알려진 사용 권한 앱-에 대 한 hello `offline_access` 범위입니다.  Hello 사용자 적극적으로 사용 하지 않을 hello 앱 하는 경우에 사용자의 hello 대신 tooaccess 리소스는 시간을 연장된 된 기간 동안 해야 하는 경우 모든 앱이 사용이 권한을 toorequest 필요 합니다.  hello `offline_access` 범위는 "오프 라인 데이터 액세스"로 toohello 사용자 승인 대화 상자 표시 됩니다는 hello 사용자에 동의 해야 합니다.  요청 hello `offline_access` 권한 웹 응용 프로그램 tooreceive OAuth 2.0 refresh_tokens hello v2.0 끝점에서 사용 하도록 설정 합니다.  Refresh_token은 수명이 길며, 액세스의 기간이 확장된 새로운 OAuth 2.0 access_token으로 바꿀 수 있습니다.  

앱 hello를 요청 하지 않고 `offline_access` 범위 refresh_tokens을 받지 것입니다.  즉,는 hello OAuth 2.0 권한 부여 코드 흐름에서 authorization_code을 교환할 때만 받습니다 다시는 access_token hello에서 `/token` 끝점입니다.  해당 access_token은 짧은 기간(일반적으로 1시간) 동안 유효하지만 결국 만료됩니다.  앱에서 tooredirect hello 사용자 백 toohello 시간, 해당 시점에 필요한 `/authorize` 끝점 tooretrieve 새 authorization_code 합니다.  이 이동 하는 동안 hello 사용자 수 또는 tooenter 자격 증명을 다시 필요 없거나 toopermissions hello hello 유형의 응용 프로그램에 따라 다시 동의 합니다.

OAuth 2.0, refresh_tokens, 및 access_tokens, 체크아웃 hello에 대 한 자세한 toolearn [v 2.0 프로토콜 참조](active-directory-v2-protocols.md)합니다.

#### <a name="openid-profile-and-email"></a>OpenID, 프로필 및 전자 메일
지금까지 hello 가장 기본적인 OpenID Connect 로그인 흐름 Azure Active Directory와은 다양 한 결과 id_token hello에에서 hello 사용자에 대 한 정보를 제공 합니다.  id_token의 hello 클레임 hello 사용자의 이름, 기본 사용자 이름, 전자 메일 주소, 개체 ID 및 더 포함할 수 있습니다.

이제 해당 hello hello 정보를 제한 하는 `openid` 범위에 대 한 앱 액세스를 제공 합니다.  hello 'openid' 범위를 통해 응용 프로그램 toosign hello 사용자가을 hello 사용자에 대 한 응용 프로그램별 식별자를 수신만 됩니다.  Hello 사용자에 대 한 응용 프로그램에서 tooobtain 개인 식별이 가능한 정보 (PII)를 원하는 경우 응용 프로그램에 hello 사용자 로부터 toorequest 추가 권한이 필요 합니다.  도입 새 범위 두 – hello `email` 및 `profile` 수 있게 해 주는 toodo 하므로 범위 – 합니다.

hello `email` 범위는 매우 단순 – hello 통해 응용 프로그램 액세스 toohello 사용자 기본 전자 메일 주소를 허용 `email` hello id_token에 클레임입니다.  hello `profile` ID, 개체 범위는 응용 프로그램 액세스 tooall hello 사용자-해당 이름, 기본 사용자 이름에 대 한 다른 기본 정보를 제공 합니다.

이렇게 하면 toocode – 최소 공개 방식에서 앱만 요청 hello 사용자 hello 집합이 필요한 정보를 응용 프로그램 toodo 작업 합니다.  이러한 범위에 대 한 자세한 내용은 참조 너무[v2.0 범위 참조가 hello](active-directory-v2-scopes.md)합니다.

## <a name="token-claims"></a>토큰 클레임
hello v2.0 끝점에서 발급 한 토큰의 클레임을 hello를 동일한 tootokens hello 일반적으로 사용할 수 있는 Azure AD 끝점에서 발급 됩니다.-앱 toohello 새 서비스를 마이그레이션하는 특정 클레임은 id_tokens 또는 access_tokens 존재 가정 하지 않아야 합니다. toolearn v 2.0 토큰에 포함 된 hello 특정 클레임에 대 한 참조 hello [v2.0 토큰 참조](active-directory-v2-tokens.md)합니다.

## <a name="limitations"></a>제한 사항
Hello v2.0 포인트를 사용 하는 경우 인식 몇 가지 제한 사항이 toobe가 않습니다.  Toohello를 참조 하십시오 [v2.0 제한 doc](active-directory-v2-limitations.md) toosee tooyour 특정 시나리오를 적용 하는 이러한 모든 제한 합니다.
