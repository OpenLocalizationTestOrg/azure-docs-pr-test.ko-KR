---
title: "Azure Active Directory B2B 공동 작업 API 및 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업은 비즈니스 파트너가 선택적으로 회사 응용 프로그램에 액세스할 수 있게 함으로써 회사 간 관계를 지원합니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Azure Active Directory B2B 공동 작업 API 및 사용자 지정

조직에 가장 잘 작동하는 방식으로 초대 프로세스를 사용자 지정하기 원하는 많은 고객이 있습니다. API를 사용하면 이 작업을 수행할 수 있습니다. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a>초대 API의 기능
이 API는 다음과 같은 기능을 제공합니다.

1. *어떤* 전자 메일 주소가 있는 내부 사용자도 초대할 수 있습니다.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. 초대를 수락한 후에 사용자가 리디렉션되려는 위치를 사용자 지정합니다.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. 다음과 같이 Microsoft를 통해 표준 초대 메일을 보내려면 선택하고

    ```
    "sendInvitationMessage": true
    ```

  사용자 지정할 수 있는 받는 사람에게 보내려는 메시지를 지정합니다.

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. 또한 이 공동 작업자 초대에 대한 정보를 계속 알리려는 사람을 참조:에 추가하도록 선택합니다.

5. 또는 Azure AD 통해 알림을 보내지 않도록 선택하여 초대 및 온보딩 워크플로를 완전히 사용자 지정합니다.

    ```
    "sendInvitationMessage": false
    ```

  이 경우 전자 메일 템플릿, IM 또는 선택한 기타 배포 방법에 포함할 수 있는 API에서 상환 URL을 다시 얻을 수 있습니다.

6. 마지막으로 관리자는 사용자를 구성원으로 초대하도록 선택할 수 있습니다.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>인증 모델
API는 다음과 같은 인증 모드에서 실행될 수 있습니다.

### <a name="app--user-mode"></a>앱 + 사용자 모드
이 모드에서 API를 사용하는 모든 사용자에게 B2B 초대를 만들기 위한 권한이 있어야 합니다.

### <a name="app-only-mode"></a>앱 전용 모드
앱 전용 컨텍스트에서 앱은 성공적인 초대를 위해 User.ReadWrite.All 또는 Directory.ReadWrite.All 범위를 지정해야 합니다.

자세한 내용은 https://graph.microsoft.io/docs/authorization/permission_scopes를 참조하세요.


## <a name="powershell"></a>PowerShell
이제 PowerShell을 사용하여 외부 사용자를 조직에 쉽게 추가하고 초대할 수 있습니다. cmdlet을 사용하여 초대 만들기

```
New-AzureADMSInvitation
```

다음 옵션을 사용할 수 있습니다.

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

[https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)에서 초대 API 참조를 확인할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [B2B 공동 작업 초대 전자 메일의 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
