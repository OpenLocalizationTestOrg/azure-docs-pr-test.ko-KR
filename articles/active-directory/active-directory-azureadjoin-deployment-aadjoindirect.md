---
title: "aaaUsage 시나리오 및 Azure AD Join에 대 한 배포 고려 사항 | Microsoft Docs"
description: "관리자가 최종 사용자(직원, 학생, 다른 사용자)를 위해 Azure AD 조인을 설정하는 방법을 설명합니다. 또한 Azure AD Join을 사용 하기 위한 hello 다른 실제 시나리오를 설명 합니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Azure AD 연결에 대한 사용 시나리오와 배포 고려 사항
## <a name="usage-scenarios-for-azure-ad-join"></a>Azure AD 연결에 대한 사용 시나리오
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Hello 클라우드에서 대부분의 시나리오 1: 비즈니스
Azure Active Directory Join (Azure AD Join) 장점 현재 작동 하 고 hello 클라우드에서 비즈니스에 대 한 id를 관리 하거나 toohello 클라우드 곧 이동 합니다. 사용자가 만든 tooWindows 10의에서 Azure AD toosign에서 계정을 사용할 수 있습니다. 통해 [먼저 경험 (FRX) 프로세스를 실행 하는 hello](active-directory-azureadjoin-user-frx.md), 또는 Azure AD에서 조인 하 여 [hello 설정 메뉴](active-directory-azureadjoin-user-upgrade.md), 사용자가 자신의 컴퓨터 tooAzure AD에 조인할 수 있습니다.  사용자가 single sign on (SSO)도 즐길 수 너무 클라우드 Office 응용 프로그램 또는 브라우저에 Office 365와 같은 리소스를 액세스 합니다.

### <a name="scenario-2-educational-institutions"></a>시나리오 2: 교육 기관
교육 기관에는 일반적으로 두 가지 사용자 유형인 교직원 및 학생이 있습니다. 교사는 hello 조직의 장기적인 멤버로 간주 됩니다. 교직원에 대한 온-프레미스 계정을 만드는 것이 바람직합니다. 하지만 학생 shorter-term 팀원 들의 hello 되며 Azure AD에서 자신의 계정을 관리할 수 있습니다. 즉, 온 프레미스 저장된 되지 않고 toohello 클라우드 디렉터리 눈금을 밀어넣을 수는 있습니다. 또한 학생 수에 Azure AD 계정와 tooWindows 수 toosign 되며 Office 응용 프로그램에서 액세스 tooOffice 365 리소스를 가져올 의미 합니다.

### <a name="scenario-3-retail-businesses"></a>시나리오 3: 소매 기업
소매 기업에는 비정규직 근로자가 있고 장기 직원이 있습니다. 일반적으로 장기적인 정규직 직원에 대해서는 온-프레미스 계정을 만든 후 도메인에 연결된 컴퓨터를 사용합니다. 하지만 계절별 작업자는 hello 조직의 shorter-term 멤버 이므로 바람직한 toomanage 자신의 계정에 사용자 라이선스를 더 쉽게 이동할 수 있습니다. Office 365 라이선스를 갖고 있는 hello 클라우드에서 자신의 사용자 계정을 만들 때 이러한 사용자가 hello 활용 남깁니다 후에 자신의 라이선스를 갖고 있는 더 많은 유연성을 유지 관리 하는 동안 tooWindows와 Azure AD 계정으로 Office 응용 프로그램에 로그인 합니다.

### <a name="scenario-4-additional-scenarios"></a>시나리오 4: 시나리오
사용자가 자신의 장치 tooAzure AD 단순화 조인 환경을, 효율적인 장치 관리, 자동 모바일 장치 관리 등록 및 single sign on tooAzure 때문에 조인 하는 것과 이점이 있습니다. 앞에서 설명한 hello 혜택을 함께 AD 및 온-프레미스 리소스입니다.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Azure AD 연결에 대한 배포 고려 사항
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>에 사용자가 toojoin 회사 소유 장치를 사용 하도록 설정 tooAzure AD 직접
클라우드 전용 계정 toopartner 회사와 조직에 기업에서는 제공할 수 있습니다. 이러한 파트너는 Single Sign-On을 사용하여 회사 앱 및 리소스에 쉽게 액세스할 수 있습니다. 이 시나리오는 주로 hello 클라우드 인증을 위해 Azure AD를 사용 하는 Office 365 또는 SaaS 앱 등의 리소스에 액세스 하는 적용 가능한 toousers입니다.

### <a name="prerequisites"></a>필수 조건
**Hello 엔터프라이즈 수준 (관리자)**

* Azure Active Directory를 사용하는 Azure 구독  

**Hello 사용자 수준**

* Windows 10(Professional 및 Enterprise 버전)

### <a name="administrator-tasks"></a>관리자 작업
* [장치 등록 설정](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>사용자 작업
* [설치하는 동안 Azure AD로 새 Windows 10 장치 설정](active-directory-azureadjoin-user-frx.md)
* [Hello 설정 메뉴에서 Azure AD와 Windows 10 장치를 설정 합니다.](active-directory-azureadjoin-user-upgrade.md)
* [개인 Windows 10 장치 tooyour 조직 참가](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>조직의 BYOD를 Windows 10에서 사용하도록 설정
사용자 및 직원 toouse 자신의 개인 Windows 장치 (BYOD) tooaccess 회사 앱 및 리소스 설정할 수 있습니다. 사용자가 안전 하 고 규격 방식 자신의 Azure AD 계정 (회사 또는 학교 계정) tooa 개인 Windows 장치 tooaccess 리소스를 추가할 수 있습니다.

### <a name="prerequisites"></a>필수 조건
**Hello 엔터프라이즈 수준 (관리자)**

* Azure AD 구독

**Hello 사용자 수준**

* Windows 10(Professional 및 Enterprise 버전)

### <a name="administrator-tasks"></a>관리자 작업
* [장치 등록 설정](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>사용자 작업
* [개인 Windows 10 장치 tooyour 조직 참가](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>추가 정보
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport를 통해 암호 없이 ID 인증](active-directory-azureadjoin-passport.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

