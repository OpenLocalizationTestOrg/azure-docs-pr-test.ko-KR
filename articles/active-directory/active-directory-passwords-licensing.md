---
title: "라이선스: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 라이선스 요구 사항"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Azure AD 셀프 서비스 암호 재설정의 라이선스 요구 사항

Azure AD 암호 재설정 toofunction 되려면에서 있습니다 **조직에서 할당 된 하나 이상의 라이선스가 있어야**합니다. 에서는 사용자 단위 hello 암호 재설정 환경에서 라이선스를 적용 하지 않습니다. Microsoft 라이선스 계약 toomaintain 규정 준수, 프리미엄 기능을 사용 하는 tooassign 라이선스 tooany 사용자가 필요 합니다.

* **클라우드 사용자만 해당** - Office 365(O365) 유료 SKU 또는 Azure AD Basic
* **클라우드** 및/또는 **온-프레미스 사용자** - Azure AD Premium P1 또는 P2, EMS(Enterprise Mobility + Security) 또는 SPE(Secure Productive Enterprise)

## <a name="licenses-required-for-password-writeback"></a>비밀번호 쓰기 저장에 필요한 라이선스

toouse 암호 쓰기 저장을 있어야 hello 테 넌 트에 할당 된 라이선스를 다음 중 하나입니다.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> 독립 실행형 Office 365 라이선스 계획 **암호 쓰기 저장을 지원 하지 않는** hello 앞에이 기능 toowork에 대 한 계획 중 하나 필요로 하 고 있습니다.

다음 페이지 hello에서 비용을 포함 하는 추가 라이선스 정보를 확인할 수 있습니다.

* [Azure Active Directory 가격 책정 사이트](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>그룹 또는 사용자 기반 라이선스 사용

Azure AD는 이제 그룹 기반의 라이선스 수 있도록 관리자 tooassign 라이선스 대량 tooa 사용자 그룹에 보다는 한 번에 하나씩 할당을 지원 합니다. [라이선스 할당, 확인 및 문제 해결](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. Tooa 사용자 라이선스를 할당할 수 있습니다, 전에 관리자에 게 hello 사용자에 hello "사용 위치" 속성을 지정 해야 합니다. 사용자 라이선스 할당을 수행할 수 있습니다 > 프로필 > hello Azure 포털의에서 설정 섹션입니다. **그룹 라이선스 할당을 사용할 경우 사용 위치를 지정 하지 않고 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다.**

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

