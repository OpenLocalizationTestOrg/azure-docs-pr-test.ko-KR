---
title: "Active Directory의 조건부 액세스 기술 참조 aaaAzure | Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory hello 사용자를 인증할 때 및 toohello 응용 프로그램 액세스를 허용 하기 전에 선택 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory 조건부 액세스 기술 참조

## <a name="services-enabled-with-conditional-access"></a>조건부 액세스로 설정된 서비스

조건부 액세스 규칙은 다양한 Azure AD 응용 프로그램 종류에서 지원됩니다. 이 목록에는 다음이 포함됩니다.


* 응용 프로그램에 등록 된 hello Azure 응용 프로그램 프록시
* Azure 원격 앱
* Azure AD에 등록된 개발 LOB(기간 업무) 및 다중 테넌트 응용 프로그램
* Dynamics CRM
* Hello Azure AD 응용 프로그램 갤러리에서 페더레이션된 응용 프로그램
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online(비즈니스용 OneDrive 포함)
* Microsoft Power BI 
* Hello Azure AD 응용 프로그램 갤러리에서 암호 SSO 응용 프로그램
* Visual Studio Team Services
* Microsoft 팀









## <a name="enable-access-rules"></a>액세스 규칙 사용
각 규칙을 응용 프로그램 단위로 사용하거나 사용하지 않도록 설정할 수 있습니다. 규칙은 때 **ON** 사용할 수 있고 hello 응용 프로그램에 액세스 하는 사용자가 적용 됩니다. 공백 문자가 있는 경우 **OFF** 영향 hello 사용자가 아닌가 환경에 로그인 하 고 사용 되지 것입니다.

## <a name="applying-rules-toospecific-users"></a>규칙 toospecific 사용자가 적용합니다.
규칙 적용된 toospecific 유형의 설정 하 여 보안 그룹에 따라 사용자가 될 수 있습니다 **적용 대상**합니다. **적용 대상** 너무 설정할 수 있습니다**모든 사용자에 게** 또는 **그룹**합니다. 설정 된 경우 너무**모든 사용자에 게** hello 규칙이 tooany 사용자 액세스 toohello 응용 프로그램에 적용 됩니다. hello **그룹** 특정 보안 및 배포 그룹 toobe 선택 옵션을 사용 하면 규칙이 이러한 그룹에만 적용 됩니다.

일반적 이기는 규칙을 배포할 때는 toofirst 파일럿 그룹의 구성원 인 사용자가 제한적으로 적용 합니다. 너무 완료 hello 규칙을 적용할 수 면**모든 사용자에 게**합니다. 이렇게 하면 hello 규칙 toobe hello 조직의 모든 사용자에 대해 적용 됩니다.

그룹을 선택할 수 있습니다도 hello를 사용 하 여 정책에서 제외 해야 **제외한** 옵션입니다. 제외 옵션으로 선택한 그룹의 모든 멤버는 포함되는 그룹에 표시되더라도 제외됩니다.

## <a name="at-work-networks"></a>"회사" 네트워크
Azure AD에서 구성 된 신뢰할 수 있는 IP 주소 범위에 의존 하는 "회사"에서 네트워크를 사용 하는 조건부 액세스 규칙 또는 AD FS에서 클레임 "내부 corpnet" hello 사용 합니다. 이러한 규칙에는 다음이 포함됩니다.

* 회사에 있지 않을 때 다단계 인증 필요
* 회사에 있지 않을 때 액세스 차단

“회사” 네트워크 지정 옵션

1. Hello에 신뢰할 수 있는 IP 주소 범위 구성 [multi-factor authentication 구성 페이지](../multi-factor-authentication/multi-factor-authentication-whats-next.md)합니다. 조건부 액세스 정책 각 인증 요청과 토큰 발급 tooevaluate 규칙에 구성 된 hello 범위를 사용 합니다. 
2. 회사 네트워크 클레임 내 hello 사용 구성, AD FS를 사용 하는 페더레이션된 디렉터리와이 옵션을 사용할 수 있습니다. 회사 네트워크 클레임 내 hello에 대 한 자세한 toolearn 참조 [Tusted Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)합니다.


## <a name="rules-based-on-application-sensitivity"></a>응용 프로그램 민감도에 기반한 규칙
규칙은 hello 귀중 서비스 toobe 액세스 tooother 서비스 영향을 주지 않고 보안을 허용 하는 응용 프로그램 단위로 구성 됩니다. Hello에 조건부 액세스 규칙을 구성할 수 있습니다 **구성** hello 응용 프로그램을 탭 합니다. 

현재 제공되는 규칙은 다음과 같습니다.

* **다단계 인증 필요**
  
  * 이 정책이 적용 된 toowill 인지 하는 모든 사용자가 적어도 한 번에 다단계 인증을 통해 필요한 tooauthenticate 수 있습니다.
* **회사에 있지 않을 때 다단계 인증 필요**
  
  * 이 정책이 적용 된 경우 비 작업 원격 위치에서 hello 서비스에 액세스할 경우 모든 사용자가 한 번 이상 수행 필요한 toohave 다단계 인증을 됩니다. 작업 tooremote 위치에서 이동 하는 경우 hello 서비스에 액세스할 때 필요한 tooperform 다단계 인증 됩니다.
* **회사에 있지 않을 때 액세스 차단** 
  
  * 사용자가 작업 tooa 원격 위치에서 이동, 이면 hello 정책 ""이 아닐 때 작업 액세스 차단 적용 된 toothem 차단 됩니다.  회사에 있을 때에는 액세스가 다시 허용됩니다.

## <a name="related-topics"></a>관련된 항목
* [연결 된 Active Directory tooAzure tooOffice 365 및 기타 응용 프로그램 액세스 보안](active-directory-conditional-access.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

