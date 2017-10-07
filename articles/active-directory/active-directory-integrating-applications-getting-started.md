---
title: "aaaGet 앱과 Azure AD를 통합 하기 시작 | Microsoft Docs"
description: "이 문서는 온-프레미스 응용 프로그램 및 클라우드 응용 프로그램과 Azure Active Directory(AD)를 통합하는 시작 가이드입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>응용 프로그램과 Azure Active Directory 통합 시작 가이드
## <a name="overview"></a>개요
이 항목은 의도 한 toogive 응용 프로그램으로 Azure AD (Active Directory) 통합에 대 한 로드맵 있습니다. 이 시작된 가이드의 어떤 부분이 관련 tooyou 식별할 수 있도록 더 자세한 항목에 대 한 간단한 요약을 포함 하는 각 hello 섹션 아래  각 주제에 자세히 알아보려면 hello 링크를 따르십시오.

## <a name="before-you-begin-take-inventory"></a>시작 하기 전에 인벤토리를 수행합니다.
Toointegrating 응용 프로그램과 Azure AD에서에서 이동 전에 고 toogo 원하는 중요 한 tooknow 됩니다.  hello 다음 질문은 Azure AD 응용 프로그램 통합 프로젝트에 대해 의견이 의도 한 toohelp입니다.

### <a name="application-inventory"></a>응용 프로그램 인벤토리
* 응용 프로그램은 모두 어디에 있습니까? 누가 소유합니까?
* 응용 프로그램에 어떤 종류의 인증이 필요합니까?
* 응용 프로그램에 액세스할 toowhich 인원?
* 새 응용 프로그램 toodeploy 하 시겠습니까?
  * 사내에 구축하고 Azure 계산 인스턴스에 배포하시겠습니까?
  * Hello Azure 응용 프로그램 갤러리에서에서 사용할 수 있는 하나 사용할 것인가?

### <a name="user-and-group-inventory"></a>사용자 및 그룹 인벤토리
* 사용자 계정은 어디에 있습니까?
  * 온-프레미스 Active Directory
  * Azure AD
  * 사용자가 소유한 별도 응용 프로그램 데이터베이스 내에서
  * 허용되지 않은 응용 프로그램에서
  * 위의 hello의 모든
* 개별 사용자는 현재 어떤 사용 권한 및 역할 할당을 가지고 있습니까? 필요 한가요 tooreview 액세스 또는 사용자 액세스 및 역할 할당 적절 하 게 이제 시겠습니까?
* 그룹은 온-프레미스 Active Directory 내에 만들어 집니까?
  * 그룹을 어떻게 구성합니까?
  * Hello 그룹 멤버는 누구 인가요?
  * 어떤 사용 권한/역할 할당 hello 그룹 현재 해야 합니까?
* 사용자/그룹 데이터베이스를 tooclean을 통합 하기 전에 필요 한가요?  (매우 중요한 질문입니다. 쓰레기를 넣고 쓰레기를 얻는 현상.)

### <a name="access-management-inventory"></a>액세스 관리 인벤토리
* 어떻게 하면 현재 관리 사용자 액세스 tooapplications? toochange에 필요 합니까?  고려 했습니까 다른 방법으로 toomanage 액세스와 같은 [RBAC](role-based-access-control-configure.md) 예를 들어?
* 액세스 toowhat 인원?

어쩌면 없는 이러한 질문의 답변 tooall hello 들겠지만 하지만 괜찮습니다.  이 가이드는 이러한 일부 질문에 대답하고 합리적인 결정을 내릴 수 있습니다.

## <a name="prerequisites"></a>필수 조건
* Azure 구독 및 Azure Active Directory입니다.  Azure 구독이 아직 없는 경우 Azure를 30일 동안 무료로 사용해 볼 수 있습니다. [사용해 보세요!](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Azure AD와 응용 프로그램 통합
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기
위에서 설명한 대로 지금까지 조직에서 관리하지 않은 응용 프로그램이 있을 수 있습니다.  Hello 인벤토리 프로세스의 일환으로, 가능한 toofind 승인 하지 않은 클라우드 응용 프로그램은 것입니다. [클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)를 참조하세요.

### <a name="authentication-types"></a>인증 형식
응용 프로그램에는 각자 다른 인증 요구 사항이 있을 수 있습니다. Azure AD과 함께 인증서 서명은 SAML 2.0, WS-페더레이션 또는 OpenID 연결 프로토콜 뿐만 아니라 암호 Single Sign-on을 사용하는 응용 프로그램을 사용하는 응용 프로그램과 사용될 수 있습니다. Azure AD와 함께 사용할 응용 프로그램 인증 형식에 대한 자세한 내용은 [Azure Active Directory에서 페더레이션된 Single Sign-on에 대한 인증서 관리](active-directory-sso-certs.md) 및 [암호 기반 Single Sign On](active-directory-appssoaccess-whatis.md)을 참조하세요.

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Azure AD 앱 프록시를 사용하는 SSO 사용
Microsoft Azure AD 응용 프로그램 프록시 액세스 tooapplications 어디에서 든 및 모든 장치에서 안전 하 게 개인 네트워크 내부에 제공할 수 있습니다. 환경 내에서 응용 프로그램 프록시 커넥터를 설치한 후에 Azure AD를 이용하여 쉽게 구성될 수 있습니다

### <a name="integrating-applications-with-azure-ad"></a>Azure AD와 응용 프로그램 통합
hello 다음 문서에서 설명 hello 가지가 응용 프로그램을 Azure AD와 통합 하 고 몇 가지 지침을 제공 합니다.

* [Active Directory toouse 결정](active-directory-administer.md)
* [응용 프로그램을 사용 하 여 hello Azure 응용 프로그램 갤러리에서](active-directory-appssoaccess-whatis.md)
* [SaaS 응용 프로그램 통합 자습서 목록](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>액세스 tooapplications 관리
hello 다음 문서 설명 방법으로 Azure AD 커넥터를 사용 하 여 Azure AD 및 Azure AD와 통합 되나요 되 면 액세스 tooapplications를 관리할 수 있습니다.

* [Azure AD를 사용 하 여 액세스 tooapps 관리](active-directory-managing-access-to-apps.md)
* [Azure AD 커넥터를 사용하여 자동화](active-directory-saas-app-provisioning.md)
* [Tooan 응용 프로그램 사용자를 할당합니다.](active-directory-applications-guiding-developers-assigning-users.md)
* [Tooan 응용 프로그램 그룹 지정](active-directory-applications-guiding-developers-assigning-groups.md)
* [계정 공유](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>사용자 지정 응용 프로그램 통합
새 응용 프로그램을 작성 하는 tooassist 개발자가 hello 전원 Azure AD를 활용 하는 경우 참조 [Guiding 개발자](active-directory-applications-guiding-developers-for-lob-applications.md)합니다.

Azure 응용 프로그램 갤러리에 사용자 지정 응용 프로그램 toohello tooadd을 원하는 경우 참조 ["준수 위해 자신의 앱" Azure AD 셀프 서비스 SAML 구성](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)합니다.

## <a name="see-also"></a>참고 항목
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)

