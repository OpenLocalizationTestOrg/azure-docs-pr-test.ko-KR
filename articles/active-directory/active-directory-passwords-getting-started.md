---
title: "빠른 시작: Azure AD SSPR | Microsoft Docs"
description: "신속하게 Azure AD 셀프 서비스 암호 재설정 배포"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>빠른 시작: Azure AD 셀프 서비스 암호 재설정

> [!IMPORTANT]
> **로그인하는 데 문제가 있나요?** 그렇다면 [암호를 변경하고 재설정하는 방법은 다음과 같습니다](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>신속하게 셀프 서비스 암호 재설정 배포

셀프 서비스 암호 재설정 (SSPR)는 단순 일정 또는 IT 관리자가 tooempower 사용자 tooreset에 대 한 의미의 암호나 계정을 잠금 해제 합니다. hello 시스템에 자세한 보고 tootrack 사용자가 알림 tooalert 함께 hello 시스템을 사용 하면 toomisuse 또는 사용상 합니다.

이 가이드에서는 이미 여러분이 작업 평가판 또는 사용이 허가된 Azure AD 테넌트를 갖고 있다고 가정합니다. Azure AD 설정 시 도움이 필요한 경우 hello 문서 참조 [Azure AD 시작](https://azure.microsoft.com/trial/get-started-active-directory/)합니다.

1. 기존 Azure AD 테넌트에서 **"암호 재설정"**을 선택합니다.

2. Hello에서 **"속성"** hello 다음 중 하나를 선택 "셀프 서비스 암호 재설정 사용" hello 옵션 아래에서 화면
    * 아무도-아무도 수 toouse SSPR 기능
    * 그룹-만 특정 Azure AD의 그룹 구성원 선택 하는 수 toouse SSPR 기능
    * 모든 사용자에 게-Azure AD 테 넌 트에 계정이 있는 모든 사용자는 수 toouse SSPR 기능

3. Hello에서 **"인증 방법"** 선택 화면
    * 다양 한 방법 필수 tooreset-적어도 하나 또는 두 개의 최대 지원
    * 메서드 사용 가능한 toousers-하나 이상의 하지만 알아보는 것이 toohave 사용할 수 있는 추가 선택
        * **전자 메일** 코드 toohello 사용자와 전자 메일의 인증 전자 메일 주소를 구성 하는 전송
        * **휴대폰** 제공 hello 사용자 hello 선택 tooreceive 호출 또는 텍스트를 코드 tootheir 모바일 전화 번호 구성
        * **사무실 전화** 코드 tootheir 있는 호출 hello 사용자 구성 사무실 전화 번호
        * **보안 질문** toochoose 해야
            * Tooregister는 데 필요한 질문 수-의미 사용자 등록을 성공적으로 대 한 hello 최소 tooanswer의 풀에서 toopull 질문 자세한 toocreate 선택할 수 있습니다. 이 옵션 3-5에서 설정할 수 있습니다 및 보다 클 수 하거나 질문 필요한 tooreset toohello 수가 동일 해야 합니다.
                * 보안 질문을 선택 하는 경우에 hello "Custom" 단추를 클릭 하 여 사용자 지정 질문을 추가할 수 있습니다.
            * 필요한 질문 수 tooreset-3-5 질문 toobe 사용자 암호 toobe 다시 설정 하거나 잠금 해제를 허용 하기 전에 올바르게 대답에서 설정할 수 있습니다.

4. 권장: **"사용자 지정"** 있습니다 toochange hello "관리자에 게 문의" 링크 toopoint tooa 페이지 또는 전자 메일 주소 정의

5. 선택 사항: hello **"Registration"** 화면 관리자에 대 한 hello 옵션을 제공 합니다.
    * 에 로그인 할 때 사용자가 tooregister 필요
    * 수 일 전에 사용자가 요청 tooreconfirm 해당 인증 정보

6. 선택 사항: hello **"알림"** 화면 hello 옵션을 관리자가 제공 합니다.
    * 사용자에게 암호 재설정에 대해 알림
    * 다른 관리자가 암호를 재설정하면 모든 관리자에게 알림

**현재는 Azure AD 테넌트에 SSPR을 구성했습니다**. 여기서 작업을 중지 하거나 tooconfigure 계속 수 암호 tooan의 동기화 온-프레미스 AD 도메인입니다.

> [!NOTE]
> 관리자가 아닌 사용자로 SSPR을 테스트합니다. Microsoft가 Azure 관리자 유형 계정에 강력한 인증 요구 사항을 적용하기 때문입니다. Hello 관리자 암호 정책에 대 한 자세한 내용은 참조는 [암호 정책 문서](active-directory-passwords-policy.md#administrator-password-policy-differences)합니다.

## <a name="configure-synchronization-tooexisting-identity-source"></a>동기화 tooexisting id 소스를 구성 합니다.

tooenable 온-프레미스 AD identity 동기화 tooAzure, tooinstall 필요 하 고 구성할 [Azure AD Connect](./connect/active-directory-aadconnect.md) 조직에서 서버에 있습니다. 이 응용 프로그램 동기화에서 사용자 및 그룹 기존 identity 소스 tooyour Azure AD 테 넌 트를 처리합니다.

* [AD Connect 디렉터리 동기화 또는 Azure AD Sync tooAzure에서 업그레이드](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [기본 설정을 사용하여 Azure AD Connect 시작](./connect/active-directory-aadconnect-get-started-express.md)
* [암호 쓰기 저장 구성](active-directory-passwords-writeback.md#configuring-password-writeback) Azure AD에서 toowrite 암호 tooyour 온-프레미스 디렉터리를 백업 합니다.

## <a name="disabling-self-service-password-reset"></a>셀프 서비스 암호 재설정 해제

셀프 서비스 암호 재설정을 사용 하지 않도록 설정 하는 것은 Azure AD 테 넌 트를 열고 너무 것 처럼 간단할**암호 재설정 > 속성** > 선택 **None** 아래 **셀프 서비스 암호 재설정 사용 하도록 설정**

### <a name="learn-more"></a>자세한 정보
링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

## <a name="next-steps"></a>다음 단계

이 빠른 시작 사용자를 위해 tooconfigure 셀프 서비스 암호 재설정 하는 방법을 배웠습니다. 다음이 단계를 수행 하는 Azure 포털 toocomplete toocontinue toohello hello toohello 포털 아래에 링크 합니다.

> [!div class="nextstepaction"]
> [셀프 서비스 암호 재설정 사용](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

