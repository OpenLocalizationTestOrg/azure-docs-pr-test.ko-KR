---
title: "aaaAzure AD 셀프 서비스 암호 재설정 개요 | Microsoft Docs"
description: "Azure AD의 셀프 서비스 암호 재설정이 조직에서 어떤 작업을 수행할 수 있나요?"
services: active-directory
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
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>IT 전문가 hello에 대 한 azure AD 셀프 서비스 암호 재설정

내에서 throw 주위 많은 IT 부서에서 다양 한 의미를 사용 하는 hello world 용어가 "셀프 서비스"입니다. hello 시장 toomanage 온-프레미스 그룹, 암호 또는 hello 클라우드 또는 온-프레미스에서 사용자 프로필 수 있는 제품과 서비스 장애 유발입니다.

Azure Active Directory(Azure AD) SSPR(셀프 서비스 암호 재설정)은 사용 및 배포 편의로부터 분리됩니다. Azure AD 셀프 서비스 암호 재설정은 다음과 같은 일련의 기능을 결합합니다.

* 사용자가 toomanage 자신의 암호 허용
  * 어떤 장치든지
  * 어디에서든지
  * 언제든지
* 관리자 권한으로 정의한 정책을 준수하여 관리할 수 있게 됩니다.

준비를 마쳤다면 [빠른 시작 설명서](active-directory-passwords-getting-started.md)를 사용하여 Azure AD SSPR을 시작하고 사용자가 자신의 고유한 암호를 재설정할 수 있습니다.

## <a name="what-is-possible"></a>가능한 기능

* **셀프 서비스 암호 변경** 최종 사용자나 관리자가 toochange 관리자의 도움 없이 암호 허용
* **셀프 서비스 계정 잠금 해제** 최종 사용자가 toounlock 관리자의 도움 없이 자신의 계정 허용
* **셀프 서비스 암호 재설정** 최종 사용자나 관리자가 tooreset 관리자의 도움 없이 자동으로 해당 암호를 허용 합니다. 셀프 서비스 암호 재설정 기능을 사용하려면 Azure AD Premium 또는 Basic - [Azure Active Directory 버전](active-directory-editions.md)이 필요합니다.
* **관리자 시작한 암호 재설정** 관리자 tooreset hello 내에서 다른 관리자 또는 최종 사용자의 암호를 사용 하면 [Azure 포털](https://docs.microsoft.com/azure/azure-portal-overview)
* **암호 관리 작업 보고서**는 조직에서 발생하는 암호 재설정 및 등록 작업에서의 관리자 이해도를 높여줍니다. [관리 보고서](active-directory-passwords-reporting.md)
* **암호 쓰기 저장** 모든 hello 앞에 있는 by 또는 hello 대신 하 여 시나리오를 수행할 수 있습니다 페더레이션 또는 암호 동기화 사용자가 있으므로 hello 클라우드에서 온-프레미스 암호도 관리할 수 있습니다. 비밀번호 쓰기 저장을 사용하려면 [Azure AD Premium](active-directory-get-started-premium.md)이 필요합니다.

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Azure AD 셀프 서비스 암호 재설정을 선택하는 이유

* **비용 절감** 기술 지원팀의 지원 기반 암호 재설정은 일반적으로 IT 조직 지출의 20%입니다.
* **최종 사용자 환경을 개선 하기 위해** 및 **기술 지원팀 량을 줄이는** 제공 하 여 최종 사용자가 hello 전원 tooresolve 자신의 암호 문제가 한 번에 기술 지원팀에 연락 하거나 지원 요청을 열지 않고도 합니다.
* **이동성 공급** - 사용자가 어디에서든 암호를 재설정할 수 있습니다

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD 셀프 서비스 암호 재설정 가용성

Azure AD 셀프 서비스 암호 재설정은 구독에 따라 세 가지 계층으로 제공됩니다.

* **Azure AD Free** - 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다
* **Azure AD 기본** 또는 **유료 Office 365 구독** - 클라우드 전용 사용자 및 클라우드 전용 관리자는 해당하는 고유한 암호를 재설정할 수 있습니다
* **Azure AD Premium** - 사용자 또는 관리자는 클라우드 전용, 페더레이션된 또는 암호 동기화된 사용자를 포함하여 해당하는 고유한 암호를 재설정할 수 있습니다. 온-프레미스 암호는 암호 쓰기 저장 toobe 사용 하도록 설정 해야 합니다.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD 셀프 서비스 암호 재설정 hello 파트의 합계

셀프 서비스 암호 재설정 Azure AD에서 다음과 같은 구성 요소가 hello 구성 됩니다.

* **암호 관리 구성 포털** hello Azure 포털을 통해 테 넌 트의 암호를 관리 하는 방법에 대 한 옵션을 제어할 수 있습니다
* **암호 재설정 등록 포털** 사용자가 암호 재설정을 자동 등록할 수 있습니다.
* **암호 재설정 포털** 여기서 사용자가 관리자에 게에 정의 된 hello 과제를 사용 하 여 자신의 암호를 재설정할 수 하 고 hello 응답 사용자가 제공한
* **사용자 암호 변경 포털** 사용자는 이전 암호를 입력하고 새 암호를 제공하여 자신의 암호를 변경할 수 있습니다.
* **암호 관리 보고서** hello Azure 포털에서에서 해당 테 넌 트에 대 한 관리자가 보고 하 고 암호 활동 분석할 수 있는 보고서
* **Azure AD Connect를 사용 하 여 암호 쓰기 저장 tooon 프레미스** 관리할 수 있게 하면 tooenable 온-프레미스와 페더레이션 또는 암호 동기화 사용자가 hello 클라우드에서

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD 가격 책정, SLA, 업데이트 및 로드맵

Hello 다음 페이지에서 이러한 항목에 대 한 자세한 정보를 확인할 수 있습니다.

* [**Azure AD 가격 책정 정보**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Office 365 가격 책정**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Azure Service Level Agreements(서비스 수준 약정)**](https://azure.microsoft.com/support/legal/sla/)
* [**Microsoft 온라인 서비스에 대한 Service Level Agreements(서비스 수준 약정)**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Azure 업데이트**](https://azure.microsoft.com/updates/)
* [**Azure 로드맵**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다

