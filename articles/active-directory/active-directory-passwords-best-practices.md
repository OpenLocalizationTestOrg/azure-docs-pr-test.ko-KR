---
title: "롤아웃: Azure AD SSPR | Microsoft 문서"
description: "Azure AD 셀프 서비스 암호 재설정을 성공적으로 롤아웃하기 위한 팁"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>사용자 암호 재설정 롤아웃

대부분의 고객이 tooensure SSPR 기능 공개를 수행 하는 hello 단계를 따릅니다.

1. [디렉터리에서 암호 재설정 사용](active-directory-passwords-getting-started.md)
2. [비밀번호 쓰기 저장을 위한 온-프레미스 AD 권한 구성](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [암호 쓰기 저장 구성](active-directory-passwords-writeback.md#configuring-password-writeback) Azure AD에서 toowrite 암호 tooyour 온-프레미스 디렉터리 백업
4. [필요한 라이선스 할당 및 확인](active-directory-passwords-licensing.md)
5. Tooroll 있습니다 점차적으로 아웃 하려는 경우 필요에 따라 제한 암호 다시 설정할 수 tooa 그룹 사용자 tooroll hello 기능을 천천히 시간이 지남에 따라. toodo이 값은 설정 hello **셀프 서비스 암호 재설정 활성화** 에서 설정/해제 **모든 사용자에 게** 너무**그룹** 하 고 암호 재설정에 대 한 보안 그룹 tooenable를 선택 합니다. hello이 그룹의 구성원 라이선스가 할당 toothem 있어야 이며 좋은 방법 tooenable [그룹 기반 라이선스](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)합니다.
6. Hello 최소 집합을 채우는 [인증 데이터](active-directory-passwords-data.md)정책에 기반 합니다.
7. 사용자가 어떻게 설명 지침 tooshow 보내 toouse SSPR에 어떻게 tooregister와 방법을 tooreset 합니다.
    > [!NOTE]
    > 관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다. Hello 관리자 암호 정책에 대 한 자세한 내용은 참조는 [심층 분석 문서](active-directory-passwords-how-it-works.md)합니다.

8. 언제 든 지 tooenforce 등록을 선택할 수 있으며 사용자 tooreconfirm 일정 기간 후 해당 인증 정보를 요구 합니다. 사용자가 toohave tooregister 사용 하지 않으려는 경우 다음을 할 수 있습니다 [암호 재설정 최종 사용자 등록 필요 없이 배포](active-directory-passwords-data.md)합니다.
9. 시간이 지남에 따라 등록 하 고 hello를 확인 하 여 사용 하 여 사용자가 검토 [Azure AD에서 제공 보고](active-directory-passwords-reporting.md)합니다.

## <a name="email-based-rollout"></a>전자 메일 기반 롤아웃

많은 고객 간단한 toouse 지침이 포함 된 전자 메일 캠페인 hello 가장 쉬운 방법은 tooget 사용자 toouse SSPR을 찾을 합니다. [롤아웃의 템플릿 toohelp으로 사용할 수 있는 세 개의 간단한 전자 메일을 만들었습니다.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **곧 출시 됩니다** 템플릿 toobe hello 주 또는 어떤 toodo 필요한 롤아웃 toolet 사용자가 알고 전 까지의 일에 사용 되는 전자 메일입니다.
* **지금 사용 가능** 시작 toodrive 사용자 tooregister 요일을 사용 toobe hello 서식 파일을 전자 메일 및 SSPR 필요할 때 사용할 수 있도록가 인증 데이터를 확인 합니다.
* **미리 알림 등록** 몇 일 tooweeks에 대 한 템플릿 배포 tooremind 사용자 tooregister 후 전자 메일 및가 인증 데이터를 확인 합니다.

## <a name="creating-your-own-password-portal"></a>고유의 암호 포털 만들기

대부분의 큰 고객 toohost 웹 페이지를 선택 하 고 루트 https://passwords.contoso.com 같은 DNS 항목을 만듭니다. 링크 toohello Azure AD 암호 재설정에이 페이지를 채우는, 암호 재설정 등록, 암호 변경 포털 및 기타 조직 관련 정보입니다. 모든 전자 메일 통신 또는 전단지에 보낸를 포함할 수 있습니다는 브랜드가 지정 된 기억 하기 쉬운, URL toowhen toouse hello 서비스 필요한 사용자가 처리할 수 있다고 합니다.

* 암호 재설정 포털 - https://passwordreset.microsoftonline.com/
* 암호 재설정 등록 포털 - http://aka.ms/ssprsetup
* 암호 변경 포털 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>강제 등록 사용

암호 재설정을 위해 사용자가 tooregister를 원하는 Azure AD를 사용 하 여 로그인 할 때 해당를 tooregister를 강제할 수 있습니다. 사용자 디렉터리에서이 옵션을 사용할 수 있습니다 **암호 재설정** hello를 사용 하 여 블레이드 **에 로그인 할 때 사용자가 필요한 tooRegister** hello에 대 한 옵션 **등록** 탭 합니다.

관리자 hello 설정 하 여 시간이 지나면 사용자 toore 레지스터에 요구할 수 있습니다 **수가 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보** 0-730 사이의 일 수 있습니다.

서명 하는 사용자가 해당 관리자가 tooverify 요청을 알려 주는 메시지가 표시 됩니다이 옵션을 사용 하도록 설정한 후 해당 인증 정보입니다.

## <a name="populate-authentication-data"></a>인증 데이터 채우기

경우 있습니다 [사용자에 대 한 인증 데이터를 채우려면](active-directory-passwords-data.md), 사용자가 암호 재설정 수 toouse SSPR에 대 한 tooregister 필요 하지 않습니다. 사용자가 수 tooreset hello 인증 정의 맞는 데이터 hello 암호 재설정 정책을 정의한를 보유 하는 사용자, 암호입니다.

## <a name="disabling-self-service-password-reset"></a>셀프 서비스 암호 재설정 해제

셀프 서비스 암호 재설정을 사용 하지 않도록 설정 하는 것은 Azure AD 테 넌 트를 열고 너무 것 처럼 간단할**암호 재설정**, **속성**를 선택 하 고 **아무도** 아래 **셀프 서비스 암호 재설정을 사용 하도록 설정**

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다
