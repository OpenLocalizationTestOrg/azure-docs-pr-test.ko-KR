---
title: "aaaAzure Active Directory B2B 공동 작업 API 및 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 비즈니스 파트너 tooselectively 액세스 회사 응용 프로그램을 사용 하 여 회사 간 관계 지원"
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Azure Active Directory B2B 공동 작업 API 및 사용자 지정

많은 고객 조직에 가장 적합 하는 방식으로 toocustomize hello 초대 프로세스 않겠다고 알려 주십시오 했습니다. API를 사용하면 이 작업을 수행할 수 있습니다. [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Hello 초대 API의 기능
hello API hello 다음 기능을 제공 합니다.

1. *어떤* 전자 메일 주소가 있는 내부 사용자도 초대할 수 있습니다.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. 사용자 지정 위치 사용자 tooland 자신의 초대를 수락 합니다.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Us를 통해 toosend hello 표준 초대 메일 선택

    ```
    "sendInvitationMessage": true
    ```

  사용자 지정할 수 있는 메시지 toohello 받는 사람으로

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. Toocc 선택: tookeep hello에 원하는 사람 사용자 초대이 공동 작업자에 대 한 반복 합니다.

5. 또는 Azure AD 통해 하지 toosend 알림을 선택 하 여 초대 및 온 보 딩 워크플로 작업을 완벽 하 게 갖추고 있습니다.

    ```
    "sendInvitationMessage": false
    ```

  이 경우 얻게 다시 상환 URL hello 전자 메일 템플릿을, 인스턴트 메시지 또는 선택한 다른 배포 방법을에 포함할 수 있는 API에서.

6. 마지막으로, 관리자 인 경우 멤버로 tooinvite hello 사용자를 선택할 수 있습니다.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>인증 모델
hello API hello 권한 부여 모드를 다음에 실행할 수 있습니다.

### <a name="app--user-mode"></a>앱 + 사용자 모드
이 모드에서는 API hello 요구를 사용 중인 누구 든 지 toohave hello 권한을 toobe B2B 초대를 만듭니다.

### <a name="app-only-mode"></a>앱 전용 모드
앱만 컨텍스트에서 hello 앱 초대 toosucceed hello에 대 한 hello User.ReadWrite.All 또는 Directory.ReadWrite.All 범위를 프로비저닝해야합니다.

자세한 내용은 https://graph.microsoft.io/docs/authorization/permission_scopes를 참조하세요.


## <a name="powershell"></a>PowerShell
것은 이제 가능한 toouse PowerShell tooadd 및 초대 외부 사용자에 게 tooan 조직 쉽게입니다. Hello cmdlet을 사용 하 여 초대를 만듭니다.

```
New-AzureADMSInvitation
```

Hello 다음 옵션을 사용할 수 있습니다.

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Hello 초대 API 참조에도 확인할 수 있습니다 [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>다음 단계

Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:

* [Azure AD B2B 공동 작업이란?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-admin-add-users.md)
* [정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법](active-directory-b2b-iw-add-users.md)
* [hello B2B 공동 작업 초대 메일의 hello 요소](active-directory-b2b-invitation-email.md)
* [B2B 공동 작업 초대 상환](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 공동 작업 라이선스](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B 공동 작업 문제 해결](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)](active-directory-b2b-faq.md)
* [B2B 공동 작업 사용자에 대한 다단계 인증](active-directory-b2b-mfa-instructions.md)
* [초대 없이 B2B 공동 작업 사용자 추가](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
