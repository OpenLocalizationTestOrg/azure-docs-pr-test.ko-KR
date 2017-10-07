---
title: "hello Azure 클래식 포털에서에서 aaaConditional 액세스 | Microsoft Docs"
description: "Tooapplications 액세스를 인증할 때 특정 조건에 대 한 Azure 클래식 포털 toocheck hello에 조건부 액세스 제어를 사용 합니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 조건부 액세스

이 항목은 hello Azure 클래식 포털에서에서 조건부 액세스에 대 한 합니다. Hello hello Azure Active Directory의에서 조건부 액세스에 대 한 최신 정보를 참조 하십시오. [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)합니다.


Azure Active Directory (Azure AD) 조건부 액세스의 제어 기능 hello 간단한 방법으로 toohelp hello 클라우드 및 온-프레미스 리소스의 보안 유지를 제공합니다. Multi-factor authentication을 해결할 수 hello 위험을와 같은 조건부 액세스 정책을 도난 및 phished 자격 증명입니다. 다른 조건부 액세스 정책을 사용하면 조직의 데이터를 안전하게 보관할 수 있습니다. 예를 들어 또한 toorequiring 자격 증명을 해야할 정책을 Microsoft Intune 조직의 중요 한 서비스에 액세스할 수와 같은 모바일 장치 관리 시스템에 등록 된 장치 에서만 해당 됩니다.

## <a name="prerequisites"></a>필수 조건
Azure AD 조건부 액세스는 [Azure Active Directory Premium](http://www.microsoft.com/identity)의 한 기능입니다. 조건부 액세스 정책이 적용된 응용 프로그램에 액세스하는 각 사용자에게는 Azure AD Premium 라이선스가 있어야 합니다. [허가되지 않은 사용자 보고서](https://aka.ms/utc5ix)에서 라이선스 요구 사항에 대해 자세히 알아볼 수 있습니다.

## <a name="how-is-conditional-access-control-enforced"></a>조건부 액세스 제어는 어떻게 적용되나요?
조건부 액세스 제어를에서와 Azure AD 응용 프로그램 사용자 tooaccess에 대 한 설정 hello 특정 조건에 대 한 검사 합니다. 액세스 요구 사항이 충족 후 hello 사용자가 인증 되 고 hello 응용 프로그램에 액세스할 수 있습니다.  

![조건부 액세스 개요](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>조건
조건부 액세스 정책에 포함할 수 있는 조건은 다음과 같습니다.

* **그룹 멤버 자격** - 그룹 멤버 자격에 따라 사용자의 액세스를 제어합니다.
* **위치** - Hello 사용자 tootrigger multi-factor authentication의 hello 위치를 사용 하 고 사용자는 신뢰할 수 있는 네트워크에 없는 경우 블록 컨트롤을 사용 합니다.
* **장치 플랫폼** - IOS, Android, Windows Mobile 또는 Windows에서 같은 hello 장치 플랫폼에 정책을 적용 하기 위한 조건으로 사용 합니다.
* **장치 사용** - 정책 평가 시 장치의 사용 여부에 관계없이 장치 상태의 유효성을 검사합니다. Hello 디렉터리에서 분실 또는 도난 장치를 비활성화 하면 정책 요구 사항을 충족 시킬 더 이상 수 없습니다.
* **로그인 및 사용자 위험** - 조건부 액세스 위험 정책에는 [Azure AD ID 보호](active-directory-identityprotection.md)를 사용할 수 있습니다. 조건부 액세스 위험 정책을 사용하면 조직에서 위험 이벤트 및 비정상적인 로그인 활동에 기반한 사전 예방 조치를 취할 수 있습니다.

## <a name="controls"></a>컨트롤
조건부 액세스 정책 tooenforce를 사용할 수 있는 컨트롤은 다음과 같습니다.

* **다단계 인증** - 다단계 인증을 통해 강력한 인증을 요구할 수 있습니다. Azure Multi-factor Authentication을 통하거나 AD FS(Active Directory Federation Services)와 결합된 온-프레미스 다단계 인증 공급자를 통해 다단계 인증을 사용할 수 있습니다. Multi-factor authentication을 사용 하 여 수 있는 액세스 권한을 받을 유효한 사용자의 자격 증명 toohello 권한이 없는 사용자가 액세스 중인 리소스를 보호할 수 있습니다.
* **차단** - 사용자 위치 tooblock 사용자 액세스와 같은 조건을 적용할 수 있습니다. 예를 들어 사용자가 신뢰할 수 있는 네트워크에 있지 않을 경우 액세스를 차단할 수 있습니다.
* **준수 장치** - Hello 장치 수준에서 조건부 액세스 정책을 설정할 수 있습니다. 도메인 가입 컴퓨터 또는 모바일 장치 관리 응용 프로그램에 등록된 모바일 장치만 조직의 리소스에 액세스할 수 있도록 정책을 설정할 수 있습니다. 예를 들어 Intune toocheck 장치 규정 준수를 사용할 수 있으며 다음 보고 tooAzure 적용에 대 한 AD hello 사용자가 응용 프로그램 tooaccess 시도할 때. Toouse Intune tooprotect 앱 및 데이터를 참조 하는 방법에 대 한 자세한 지침은 [Microsoft Intune로 앱 및 데이터 보호](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune)합니다. 분실 하거나 도난당 한 장치에 대 한 Intune tooenforce 데이터 보호를 사용할 수도 있습니다. 자세한 정보는 [Microsoft Intune을 사용하여 전체 또는 선택적 초기화로 데이터 보호](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)를 참조하세요.

## <a name="applications"></a>응용 프로그램
Hello 응용 프로그램 수준에서 조건부 액세스 정책을 적용할 수 있습니다. Hello 클라우드 또는 온-프레미스 응용 프로그램 및 서비스에 대 한 액세스 수준을 설정 합니다. hello 정책은 적용 된 직접 toohello 웹 사이트 또는 서비스입니다. 액세스 toohello 브라우저 및 tooapplications hello 서비스에 액세스 하는 hello 정책이 적용 됩니다.

## <a name="device-based-conditional-access"></a>장치 기반 조건부 액세스
Azure AD에 등록 하 고 특정 조건을 충족 하는 장치에서 액세스 tooapplications를 제한할 수 있습니다. 장치 기반 조건부 액세스에서 tooaccess hello 리소스 하려는 사용자의 조직 리소스를 보호 합니다.

* 알 수 없거나 관리되지 않는 장치
* Hello 보안 정책에 맞지 않는 장치를 조직 설정 합니다.

다음 요구 사항을 기반으로 하여 정책을 설정할 수 있습니다.

* **도메인 가입 장치** - 정책 toorestrict 액세스 toodevices 조인된 tooan 온-프레미스 Active Directory 도메인에 있으며 Azure AD에 등록도 설정 합니다. 이 정책은 tooWindows 데스크톱, 랩톱 및 태블릿 엔터프라이즈 적용 됩니다.
  방법에 대 한 자세한 내용은 도메인에 가입 된 장치를 Azure AD와의 자동 등록을 tooset 참조 [Windows 도메인에 가입 된 장치를 Azure Active Directory 자동 등록을 설정](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.
* **준수 장치** - 표시 된 정책 toorestrict 액세스 toodevices 설정 **규격** hello 관리 시스템 디렉터리에 있습니다. 이 정책을 설정하면 장치에서 파일 암호화를 적용하는 등 보안 정책을 준수하는 장치만 액세스가 허용됩니다. 이 정책 toorestrict 액세스 hello 다음 장치에서에서 사용할 수 있습니다.
  
  * **Windows 도메인 가입 장치** - System Center Configuration Manager (현재 분기 hello)에서 하이브리드 구성 배포를 관리 합니다.
  * **Windows 10 모바일 회사 또는 개인 장치** - Intune 또는 지원되는 타사 모바일 장치 관리 시스템에서 관리합니다.
  * **iOS 및 Android 장치** - Intune에서 관리합니다.

장치 기반으로 보호 되는 응용 프로그램을 액세스 하는 사용자, 인증 기관 정책이이 정책 요구이 사항을 충족 하는 장치에서 hello 응용 프로그램에 액세스 해야 합니다. 정책 요구 사항을 충족하지 않는 장치에서 액세스하려고 하면 액세스가 거부됩니다.

장치 기반 tooconfigure Azure AD에서 인증 기관 정책을 확인 하는 방법에 대 한 내용은 [Azure Active Directory에 연결 된 응용 프로그램에 대 한 장치 기반 조건부 액세스 정책을 설정할](active-directory-conditional-access-policy-connected-applications.md)합니다.

## <a name="resources"></a>리소스
다음 조직에 대 한 조건부 액세스를 설정 하는 방법에 대 한 자세한 리소스 범주 및 문서 toolearn hello를 참조 하십시오.

### <a name="multi-factor-authentication-and-location-policies"></a>다단계 인증 및 위치 정책
* [조건부 액세스 tooAzure AD에 연결 된 앱 그룹, 위치 및 다단계 인증 정책에 따라 시작](active-directory-conditional-access-azuread-connected-apps.md)
* [지원되는 응용 프로그램 및 브라우저](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>장치 기반 조건부 액세스
* [장치 기반 조건부 액세스 정책에 대 한 액세스 제어 tooAzure Active Directory에 연결 된 응용 프로그램 설정](active-directory-conditional-access-policy-connected-applications.md)
* [Windows 도메인 가입 장치에 대한 Azure Active Directory 자동 등록 설정](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Azure Active Directory 액세스 문제 해결](active-directory-conditional-access-device-remediation.md)
* [Microsoft Intune을 사용하여 분실되거나 도난당한 장치의 데이터 보호](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>로그인 위험에 기반한 리소스 보호
* [Azure AD ID 보호](active-directory-identityprotection.md)

### <a name="next-steps"></a>다음 단계
* [조건부 액세스 FAQ](active-directory-conditional-faqs.md)
* [기술 참조](active-directory-conditional-access-technical-reference.md)

