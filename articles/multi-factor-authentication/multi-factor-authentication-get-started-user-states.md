---
title: "aaaMicrosoft Azure Multi-factor Authentication 사용자 상태"
description: "Azure MFA의 사용자 상태에 대해 알아보세요."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>어떻게 사용자 또는 그룹에 대 한 toorequire 2 단계 인증

2단계 인증을 요구하는 두 가지 방법이 있습니다. 첫 번째 옵션 hello tooenable 각 개별 사용자가 Azure Multi-factor Authentication (MFA)에 대 한 합니다. 사용자가 개별적으로 설정 된 몇 가지 예외가 있지만, 장치 기능이 설정 된 신뢰할 수 있는 IP 주소에서 로그인 할 때 또는 hello 기억 하는 경우 처럼 2 단계 인증 항상 수행 합니다. hello 두 번째 옵션은 tooset 특정 조건에서 2 단계 인증을 요구 하는 조건부 액세스 정책 구성 합니다.

>[!TIP] 
>둘 다 이러한 메서드 toorequire 2 단계 인증 중 하나를 선택 합니다. 사용자가 Azure MFA를 사용하도록 설정하면 모든 조건부 액세스 정책이 무시됩니다.

## <a name="which-option-is-right-for-you"></a>어떤 옵션이 적합한가요?

**사용자 상태를 변경 하 여 Azure MFA를 활성화** hello 일반적인 방법에 대 한 2 단계 인증을 요구 합니다. Hello 클라우드에서 모두 Azure MFA 및 Azure MFA 서버 작동합니다. 사용 하도록 설정 하면 모든 hello 사용자가 hello에 로그인 할 때마다 tooperform 2 단계 인증을 사용 하 되 같은 경험 합니다. 사용자가 사용하도록 설정되면 해당 사용자에게 영향을 줄 수 있는 모든 조건부 액세스 정책이 무시됩니다. 

**조건부 액세스 정책을 사용하여 Azure MFA를 사용하도록 설정**하는 것은 2단계 인증을 요구하는 것보다 더 유연한 방법입니다. 것에 대해서만 작동 hello 클라우드에서 Azure MFA 하지만 및 조건부 액세스는는 [유료 Azure Active Directory의 기능](https://www.microsoft.com/cloud-platform/azure-active-directory-features)합니다. Toogroups 뿐만 아니라 개별 사용자에 게 적용 되는 조건부 액세스 정책을 만들 수 있습니다. 위험 수준이 높은 그룹에는 위험 수준이 낮은 그룹보다 더 많은 제한이 제공되거나 위험 수준이 높은 클라우드 앱에만 2단계 인증이 요구되고 위험 수준이 낮은 그룹에는 건너뛸 수 있습니다. 

Hello 요구 사항 설정 후에 로그인 할 처음으로 Azure Multi-factor Authentication hello에 대 한 사용자가 tooregister 라는 두이 옵션 모두. 두 옵션 모두 구성 가능한 hello로 확대할 [Azure Multi-factor Authentication 설정](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>사용자 상태를 변경하여 Azure MFA를 사용하도록 설정

Azure Multi-factor Authentication에서 사용자 계정에는 다음 세 가지 상태는 hello를 사항이 있습니다.

| 가동 상태 | 설명 | 영향 받는 비브라우저 앱 |
|:---:|:---:|:---:|
| 사용 안 함 |새 사용자에 대 한 기본 상태 hello Azure Multi-factor Authentication (MFA) 등록 되지 않은 합니다. |아니요 |
| 사용 |hello 사용자가 Azure MFA에 등록 되어 있지만 등록 되지 않았습니다. 입력 정보 요청된 tooregister hello 다음 번에 로그인 됩니다. |아니요.  Toowork hello 등록 프로세스가 완료 될 때까지 계속 합니다. |
| 적용 |hello 사용자가 등록 되어 있고 Azure MFA에 대 한 hello 등록 프로세스를 완료 합니다. |예.  앱에 앱 암호가 필요합니다. |

사용자의 상태는 관리자가에 등록 되었는지 여부에 Azure MFA 및 hello 등록 프로세스를 완료 여부를 반영 합니다.

모든 사용자는 *사용 안 함*으로 시작합니다. Azure MFA에 사용자를 등록하면 상태는 *사용*으로 변경됩니다. 사용 되는 사용자에 로그인 하 고 hello 등록 프로세스 완료를 상태로 변경 너무*적용*합니다.  

### <a name="view-hello-status-for-a-user"></a>사용자에 대 한 hello 상태 보기

사용 하 여 hello 다음 단계를 확인 하 고 사용자 상태를 관리할 수 있는 tooaccess hello 페이지 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. 너무 이동**Azure Active Directory** > **사용자 및 그룹** > **모든 사용자에 게**합니다.
3. **Multi-Factor Authentication**을 선택합니다.
   ![Multi-Factor Authentication 선택](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Hello 사용자 상태를 표시 하는 새 페이지를 엽니다.
   ![다단계 인증 사용자 상태 - 스크린샷](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>사용자에 대 한 hello 상태 변경

1. Hello 앞 단계 tooget toohello multi-factor authentication 사용자가 페이지를 사용 합니다.
2. Azure MFA에 대 한 tooenable 되도록 찾기 hello 사용자입니다. Toochange 할 수 있습니다 hello hello 위쪽에는 보기입니다. 
   ![사용자 찾기 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Hello 상자 다음 tootheir 이름을 확인 하십시오.
4. 오른쪽의 빠른 단계에서 사용 되는 hello, 선택 **사용** 또는 **사용 하지 않도록 설정**합니다.
   ![선택한 사용자 사용 - 스크린샷](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*활성화* 사용자를 자동으로 너무 전환할*적용* Azure MFA에 대해 등록할 때. Hello 사용자 상태 tooenforced를 수동으로 변경 하지 않아야 합니다. 

5. Hello 팝업 창이 열리면 선택한 내용을 확인 합니다. 

사용자를 사용으로 설정한 후 전자 메일을 통해 알려야 합니다. 증명이 요구 됩니다 tooregister hello 다음에 로그인 할 때 알려 줍니다. 또한 조직에서 최신 인증을 지원 하지 않는 비 브라우저 앱을 사용 하는 경우 toocreate 앱 암호 해야 합니다. 링크 tooour 포함할 수도 있습니다 [Azure MFA 최종 사용자 가이드](./end-user/multi-factor-authentication-end-user.md) toohelp을 시작 합니다.

### <a name="use-powershell"></a>PowerShell 사용
toochange hello 사용자 상태 사용 하 여 상태 [Azure AD PowerShell](/powershell/azure/overview), 변경 `$st.State`합니다. 여기에는 세 가지 상태가 있습니다.

* 사용
* 적용
* 사용 안 함  

사용자가 이동 하지 직접 toohello *Enforced* 상태입니다. 비 브라우저 기반 앱 hello 사용자가 하지 등록 MFA 완료 하 고 가져올 수 없기 때문에 작동 중지 됩니다는 [앱 암호](multi-factor-authentication-whats-next.md#app-passwords)합니다. 

PowerShell을 사용 하는 것이 좋습니다 toobulk 사용자가 사용 하도록 설정 해야 합니다. 사용자 목록을 통해 반복하여 이 사용자들을 사용하도록 설정하는 PowerShell 스크립트를 만듭니다.

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

다음은 예제입니다.

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>조건부 액세스 정책으로 Azure MFA 사용

조건부 액세스는 여러 가지 구성 옵션이 가능한 Azure Active Directory의 유료 기능입니다. 다음이 단계를 안내는 한 가지 방법은 toocreate 정책. 자세한 내용은 [Azure Active Directory 조건부 액세스](../active-directory/active-directory-conditional-access-azure-portal.md)를 참조하세요.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.
2. 너무 이동**Azure Active Directory** > **조건부 액세스**합니다.
3. **새 정책**을 선택합니다.
4. **할당** 아래에서 **사용자 및 그룹**을 선택합니다. 사용 하 여 hello **Include** 및 **제외** 탭 toospecify 있는 사용자 및 그룹 hello 정책에 의해 관리 됩니다.
5. **할당** 아래에서 **클라우드 앱**을 선택합니다. Tooinclude 선택 **모든 클라우드 앱**합니다.
6. **액세스 제어** 아래에서 **허용**을 선택합니다. **다단계 인증 필요**를 선택합니다.
7. 설정 **정책 사용** 너무**에** 선택한 후 **저장**합니다.

hello hello 조건부 액세스 정책에서 다른 옵션 사용 하면 toospecify 2 단계 인증 해야 하는 경우에 정확 하 게 있습니다. 예를 들어 함을 나타내는 정책을 만들 수 있습니다: 계약자는 tooaccess 도메인에 가입 되지 않은 장치에서 신뢰할 수 없는 네트워크에서 조달 앱을 시도할 때 2 단계 인증을 요구 합니다. 

## <a name="next-steps"></a>다음 단계

- Hello에 대 한 팁 가져오기 [조건부 액세스에 대 한 유용한 정보](../active-directory/active-directory-conditional-access-best-practices.md)

- [사용자 및 장치](multi-factor-authentication-manage-users-and-devices.md)에 대한 Multi-Factor Authentication 설정을 관리합니다.