---
title: "aaaAzure AD 암호 보안 계층 | Microsoft Docs"
description: "Azure AD가 강력한 암호를 적용하고 사이버 범죄자로부터 사용자 암호를 보호하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>다중 계층 접근 방식 tooAzure AD 암호 보안

몇 가지 모범 사례를 따르면 사용자 또는 관리자 tooprotect로 Azure Active Directory (Azure AD) 또는 Microsoft 계정에 설명 합니다.

 > [!NOTE]
 > Azure AD 관리자가 hello 문서의 hello 지침을 사용 하 여 사용자 암호를 재설정할 수 [Azure Active Directory에서 사용자에 대 한 hello 암호 재설정](active-directory-users-reset-password-azure-portal.md)합니다.
 >
 > 사용자가 hello 문서의 hello 지침을 사용 하 여 자신의 암호를 재설정할 수 [Azure AD 암호를 잊어 버린 도움말](active-directory-passwords-update-your-own-password.md)합니다.
 >

## <a name="password-requirements"></a>암호 요구 사항

Azure AD 통합 hello 다음 일반적인 접근 방식을 toosecuring 암호:

* 암호 길이 요구 사항
* 암호 복잡성 요구 사항
* 일반 및 정기적인 암호 만료

Azure Active Directory에서 암호 재설정에 대 한 내용은 hello 항목을 참조 하십시오. [Azure AD 셀프 서비스 암호 재설정에 대 한 IT 전문가 hello](active-directory-passwords.md)합니다.

## <a name="azure-ad-password-protections"></a>Azure AD 암호 보호

Azure AD 및 Microsoft 계정 시스템 입증 된 업계를 사용 하 여 hello 포함 하 여 사용자 및 관리자 암호의 보안 보호 tooensure 접근 방식을:

* 동적으로 금지된 암호
* 스마트 암호 잠금

현재 조사 결과에 따라 암호 관리에 대 한 내용은 hello 백서를 참조 하십시오. [암호 지침](http://aka.ms/passwordguidance)합니다.

### <a name="dynamically-banned-passwords"></a>동적으로 금지된 암호

Azure AD 및 Microsoft 계정은 일반적으로 사용되는 암호를 동적으로 금지함으로써 암호 보호를 보호합니다. hello Azure ID Id 보호 team 목록 금지 된 암호에서 자주 사용 되는 암호를 선택 하면 사용자가 방지를 정기적으로 분석 합니다. 이 서비스가 사용할 수 있는 tooAzure AD와 hello Microsoft 계정 서비스 고객입니다.

암호를 만들 때 관리자 tooencourage 사용자 toochoose 암호가 포함 된 구를 문자, 숫자, 문자 또는 단어의 고유한 조합에 대 한 것입니다. 이 방법을 사용 하지만 사용자가 tooremember 기 더 쉽도록 거의 없는 toobe 손상 toomake 사용자 암호 수 있습니다.

#### <a name="password-breaches"></a>암호 위반

Microsoft에서는 항상 toostay 한 발 사이버 범죄자 앞서 노력 해야 합니다.

hello Azure AD Identity Protection 팀 일반적으로 사용 되는 암호를 지속적으로 분석 합니다. 사이버 범죄자 또한 사용 하 여 유사한 전략 tooinform 작성 등의 공격을 [레인 보우 테이블](https://en.wikipedia.org/wiki/Rainbow_table) 해독 암호 해시에 대 한 합니다.

Microsoft 분석 하 여 지속적으로 [데이터 침해](https://www.privacyrights.org/data-breaches) toomaintain 실제 해지기 전에 취약 한 암호는 사용 금지 보장 하는 금지 된 암호를 동적으로 업데이트 된 목록을 위협 tooAzure AD 고객 합니다. 우리의 현재 보안 노력에 대 한 자세한 내용은 참조 hello [Microsoft 보안 인텔리전스 보고서](https://www.microsoft.com/security/sir/default.aspx)합니다.

### <a name="smart-password-lockout"></a>스마트 암호 잠금

Azure AD에서 잠재적인 사이버 범죄 동안 toohack 사용자 암호를 검색 하는 경우 hello 사용자 계정과를 스마트 암호 잠금 잠급니다 했습니다. Azure AD는 설계 되었습니다. 특정 로그인 세션과 연결 된 toodetermine hello 위험 합니다. Hello 최신 보안 데이터를 사용 하 여 다음 잠금 의미 체계 toostop 사이버 위협 적용 합니다.

Azure AD에서 사용자가 잠겨 경우 비슷한 toohello 순서에 해당 화면에 표시:

  ![Azure AD에서 차단](./media/active-directory-secure-passwords/locked-out-azuread.png)

다른 Microsoft 계정에 대 한 자신의 화면 표시 순서에 비슷한 toohello:

  ![Microsoft 계정에서 차단](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Azure Active Directory에서 암호 재설정에 대 한 내용은 hello 항목을 참조 하십시오. [Azure AD 셀프 서비스 암호 재설정에 대 한 IT 전문가 hello](active-directory-passwords.md)합니다.

  >[!NOTE]
  >Azure AD 관리자 인 경우 toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid 프로그램 사용자가 기존 암호를 모두 만들 합니다.
  >

## <a name="next-steps"></a>다음 단계

* [어떻게 tooupdate 암호](active-directory-passwords-update-your-own-password.md)
* [hello Azure id 관리 기본 사항](fundamentals-identity.md)
* [암호 재설정 활동에 대한 보고서](active-directory-passwords-reporting.md)


