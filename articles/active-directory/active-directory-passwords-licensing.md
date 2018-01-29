---
title: "라이선스 셀프 서비스 암호 재설정 - Azure Active Directory"
description: "Azure AD 셀프 서비스 암호 재설정 라이선스 요구 사항"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2018
ms.author: joflore
ms.custom: it-pro;seohack1
ms.openlocfilehash: ca6d7a6d2b7ffa49f3656510010cfb49a81e22d7
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Azure AD 셀프 서비스 암호 재설정의 라이선스 요구 사항

Azure Active Directory(Azure AD) 암호 재설정이 올바르게 작동하기 위해서는 *조직에서 최소 하나의 라이선스가 할당되어 있어야 합니다*. 암호 재설정 환경에는 사용자당 라이선스가 적용되지 않습니다. Microsoft 라이선스 규약을 준수하려면 프리미엄 기능을 사용하는 모든 사용자에게 라이선스를 할당해야 합니다.

* **클라우드 전용 사용자**: Office 365 유료 SKU 또는 Azure AD Basic
* **클라우드** 또는 **온-프레미스 사용자**: Azure AD Premium P1 또는 P2, Enterprise Mobility + Security(EMS) 또는 Microsoft 365

## <a name="licenses-required-for-password-writeback"></a>비밀번호 쓰기 저장에 필요한 라이선스

비밀번호 쓰기 저장을 사용하려면 테넌트에 다음과 같은 라이선스 중 하나가 할당되어 있어야 합니다.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Microsoft 365(요금제 E3)
* Microsoft 365(요금제 E5)

> [!WARNING]
> 독립 실행형 Office 365 라이선스 요금제는 *비밀번호 쓰기 저장을 지원하지 않습니다*. 비밀번호 쓰기 저장을 사용하려면 위의 요금제 중 하나가 필요합니다.
>

아래와 같은 페이지에서 라이선스와 요금에 대한 자세한 정보를 확인할 수 있습니다.

* [Azure Active Directory 가격 책정 사이트](https://azure.microsoft.com/pricing/details/active-directory/)
* [Azure Active Directory 기능 및 특성](https://www.microsoft.com/cloud-platform/azure-active-directory-features)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise)

## <a name="enable-group-or-user-based-licensing"></a>그룹 또는 사용자 기반 라이선스 사용

Azure AD가 이제 그룹 기반 라이선스를 지원합니다. 관리자는 라이선스를 한 번에 하나씩 할당하는 대신 사용자 그룹에 한꺼번에 라이선스를 할당할 수 있습니다. 자세한 내용은 [라이선스 할당, 확인 및 문제 해결](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)을 참조하세요.

일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. 사용자에게 라이선스를 할당하려면 먼저 관리자가 해당 사용자의 **사용 위치** 속성을 지정해야 합니다. 라이선스는 Azure Portal의 **사용자** > **프로필** > **설정**에서 할당할 수 있습니다. *그룹 라이선스 할당을 사용할 때 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.*

## <a name="next-steps"></a>다음 단계

* [성공적인 SSPR 롤아웃을 어떻게 완료합니까?](active-directory-passwords-best-practices.md)
* [암호 재설정 또는 변경](active-directory-passwords-update-your-own-password.md)
* [셀프 서비스 암호 재설정 등록](active-directory-passwords-reset-register.md)
* [SSPR에서 사용하는 데이터는 무엇이며, 사용자에 대해 어떤 데이터를 채워야 합니까?](active-directory-passwords-data.md)
* [사용자가 사용할 수 있는 인증 방법은 무엇입니까?](active-directory-passwords-how-it-works.md#authentication-methods)
* [SSPR에서 사용하는 정책 옵션은 무엇입니까?](active-directory-passwords-policy.md)
* [비밀번호 쓰기 저장은 무엇이며, 왜 관심을 가져야 합니까?](active-directory-passwords-writeback.md)
* [SSPR 작업은 어떻게 보고 합니까?](active-directory-passwords-reporting.md)
* [모든 SSPR 옵션과 그 의미는 무엇입니까?](active-directory-passwords-how-it-works.md)
* [무엇인가 손상된 문제가 있습니다. SSPR 문제는 어떻게 해결합니까?](active-directory-passwords-troubleshoot.md)
* [다른 곳에서 다루지 않았던 질문이 있습니다.](active-directory-passwords-faq.md)
