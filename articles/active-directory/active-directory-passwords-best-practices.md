---
title: "셀프 서비스 암호 재설정 배포 가이드 - Azure Active Directory"
description: "Azure AD 셀프 서비스 암호 재설정을 성공적으로 롤아웃하기 위한 팁"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/11/2018
ms.author: joflore
ms.custom: it-pro;seohack1
ms.openlocfilehash: 0ab45043e2f75ff07a2a1a48e69507be185b56ab
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-successfully-roll-out-self-service-password-reset"></a>셀프 서비스 암호 재설정을 성공적으로 롤아웃하는 방법

Azure AD(Azure Active Directory) SSPR(셀프 서비스 암호 재설정) 기능을 자연스럽게 롤아웃하기 위해 대부분의 고객이 다음 단계를 완료해야 합니다.

1. [디렉터리에서 암호 재설정을 사용하도록 설정합니다](active-directory-passwords-getting-started.md).
2. [비밀번호 쓰기 저장에 대한 온-프레미스 Active Directory 권한을 구성합니다](active-directory-passwords-writeback.md#active-directory-permissions).
3. [비밀번호 쓰기 저장을 구성](active-directory-passwords-writeback.md#configure-password-writeback)하여 Azure AD에서 온-프레미스 디렉터리로 비밀번호 다시 쓰기
4. [필수 라이선스를 할당하고 확인합니다](active-directory-passwords-licensing.md).
5. 단계적 롤아웃을 수행할지를 결정합니다. SSPR을 점진적으로 롤아웃하려면 사용자 그룹에 대한 액세스를 제한하여 특정 그룹에서 프로그램의 파일럿을 수행할 수 있습니다. 특정 그룹을 롤아웃하려면 **셀프 서비스 암호 재설정 사용** 스위치를 **선택됨**으로 설정하고 암호 재설정을 사용하는 보안 그룹을 선택합니다. 
6. 사무실 전화, 휴대폰 및 보조 이메일 주소와 같이 사용자가 등록하는 데 필요한 [인증 데이터](active-directory-passwords-data.md)를 입력합니다.
7. [회사 브랜딩이 포함되도록 Azure AD 로그인 환경을 사용자 지정합니다](active-directory-passwords-customize.md).
8. 사용자에게 SSPR을 사용하는 방법을 설명합니다. 사용자에게 암호를 등록하는 방법 및 다시 설정하는 방법을 보여주는 지침을 보냅니다.
9. 등록을 적용하려는 경우를 결정합니다. 언제든지 등록을 적용할 수 있습니다. 또한 일정 기간이 지나면 인증 정보를 다시 확인하도록 사용자에게 요구할 수 있습니다.
10. 보고 기능을 사용합니다. 시간이 지남에 따라 [Azure AD에서 제공하는 보고 기능](active-directory-passwords-reporting.md)을 사용하여 사용자 등록 및 사용량을 검토할 수 있습니다.
11. 암호 재설정을 사용합니다. 준비가 되면 **셀프 서비스 암호 재설정 사용**을 **전체**로 설정하여 모든 사용자가 암호 재설정을 사용하도록 설정합니다. 

   > [!NOTE]
   > 선택한 그룹에서 모든 사용자로 이 옵션을 변경하면 사용자가 테스트 그룹의 일부로 등록된 기존 인증 데이터를 무효화하지 않습니다. 구성되고 유효한 인증 데이터를 등록한 사용자는 계속 작동합니다.

12. [Windows 10 사용자가 로그인 화면에서 해당 암호를 재설정할 수 있습니다](active-directory-passwords-login.md).

   > [!IMPORTANT]
   > Microsoft가 Azure 관리자 계정에 강력한 인증 요구 사항을 적용하므로 관리자가 아닌 사용자로 SSPR을 테스트합니다. 관리자 암호 정책에 대한 자세한 내용은 [암호 정책](active-directory-passwords-policy.md#administrator-password-policy-differences) 문서를 참조하세요.

## <a name="email-based-rollout"></a>전자 메일 기반 롤아웃

많은 고객은 사용자에게 SSPR을 사용하도록 하는 가장 쉬운 방법으로 사용하기 간단한 지침이 포함된 전자 메일 캠페인을 사용하는 것이라고 생각합니다. [Microsoft는 롤아웃에 도움이 되도록 템플릿으로 사용할 수 있는 세 가지 간단한 전자 메일을 만들었습니다.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **출시 예정**: 롤아웃 몇 주 또는 며칠 전에 사용자에게 어떤 작업을 수행해야 한다는 사실을 알리기 위해 사용하는 전자 메일 템플릿입니다.
* **현재 사용 가능**: 프로그램 출시 당일에 사용자가 인증 데이터를 등록하고 확인하도록 하기 위해 사용하는 전자 메일 템플릿입니다. 사용자가 지금 등록하는 경우 필요할 때 SSPR을 사용할 수 있습니다.
* **등록 미리 알림**: 배포 며칠 후 또는 몇 주 후에 사용자에게 인증 데이터를 등록하고 확인하라고 알려주는 전자 메일 템플릿입니다.

![Email][Email]

## <a name="create-your-own-password-portal"></a>고유 암호 포털 만들기

대부분의 고객은 웹 페이지를 호스팅하고 https://passwords.contoso.com과 같은 루트 DNS 항목을 만드는 방법을 선택합니다. 이 페이지를 다음 정보에 대한 링크로 채웁니다.

* [Azure AD 암호 재설정 포털 - https://aka.ms/sspr](https://aka.ms/sspr)
* [Azure AD 암호 재설정 등록 포털 - http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)
* [Azure AD 암호 변경 포털 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)
* 다른 조직 관련 정보

보낸 전자 메일 통신 또는 전단지에서 사용자가 서비스를 사용해야 할 때 이동할 수 있는 유명하고 기억하기 쉬운 URL을 포함할 수 있습니다. 사용자에게 도움이 되도록 조직의 필요에 맞게 사용하고 사용자 지정할 수 있는 [샘플 암호 재설정 페이지](https://github.com/ajamess/password-reset-page)를 만들었습니다.

## <a name="use-enforced-registration"></a>강제 등록 사용

사용자를 암호 재설정에 등록하려면 사용자가 Azure AD를 통해 로그인할 때 등록하도록 할 수 있습니다. **등록** 탭의 **로그인할 때 사용자가 등록해야 함** 옵션을 사용하여 디렉터리의 **암호 재설정** 창에서 이 옵션을 사용할 수 있습니다.

관리자는 특정 기간 이후에 사용자가 다시 등록하도록 요구할 수 있습니다. **사용자가 인증 정보를 다시 확인하도록 요청받을 때까지의 기간(일) 설정** 옵션을 0에서 730 사이로 설정할 수 있습니다.

이 옵션을 설정한 후에 사용자가 로그인할 경우 해당 관리자의 요청에 따라 인증 정보를 확인해야 한다는 내용의 메시지가 표시됩니다.

## <a name="populate-authentication-data"></a>인증 데이터 채우기

[사용자에 대한 인증 데이터를 채워야](active-directory-passwords-data.md) 합니다. 이러한 방식으로 사용자는 SSPR을 사용하기 전에 암호 재설정에 등록할 필요가 없습니다. 사용자가 정의된 암호 재설정 정책을 충족하는 인증 데이터를 제공하면 해당 암호를 재설정할 수 있습니다.

## <a name="disable-self-service-password-reset"></a>셀프 서비스 암호 재설정 사용 안 함

셀프 서비스 암호 재설정을 사용하지 않게 설정하는 방법은 간단합니다. Azure AD 테넌트를 열고 **암호 재설정** > **속성**으로 이동한 다음 **셀프 서비스 암호 재설정이 사용하도록 설정됨** 아래에서 **없음**을 선택합니다.

## <a name="next-steps"></a>다음 단계

* [암호 재설정 또는 변경](active-directory-passwords-update-your-own-password.md)
* [셀프 서비스 암호 재설정 등록](active-directory-passwords-reset-register.md)
* [라이선스 관련 질문이 있습니까?](active-directory-passwords-licensing.md)
* [SSPR에서 사용하는 데이터는 무엇이며, 사용자에 대해 어떤 데이터를 채워야 합니까?](active-directory-passwords-data.md)
* [SSPR에서 사용하는 정책 옵션은 무엇입니까?](active-directory-passwords-policy.md)
* [비밀번호 쓰기 저장은 무엇이며, 왜 관심을 가져야 합니까?](active-directory-passwords-writeback.md)
* [SSPR 작업은 어떻게 보고 합니까?](active-directory-passwords-reporting.md)
* [모든 SSPR 옵션과 그 의미는 무엇입니까?](active-directory-passwords-how-it-works.md)
* [무엇인가 손상된 문제가 있습니다. SSPR 문제는 어떻게 해결합니까?](active-directory-passwords-troubleshoot.md)
* [다른 곳에서 다루지 않았던 질문이 있습니다.](active-directory-passwords-faq.md)

[Email]: ./media/active-directory-passwords-best-practices/sspr-emailtemplates.png "조직의 요구 사항에 맞게 이러한 전자 메일 템플릿을 사용자 지정"
