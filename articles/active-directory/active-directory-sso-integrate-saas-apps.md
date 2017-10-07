---
title: "SaaS 앱 Azure Active Directory single sign on aaaIntegrate | Microsoft Docs"
description: "Azure Active Directory에서 SaaS 앱의 Single Sign-On 인증과 사용자 프로비전 집중식 액세스 관리를 사용하도록 설정합니다. 방법의 개요 toointegrate Azure Active Directory tooSaaS 앱."
services: active-directory
keywords: "Azure AD와 SaaS 앱 통합"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Azure Active Directory Single Sign-On과 SaaS 앱 통합
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Azure 클래식 포털](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget 조직으로 가져오는 중인 응용 프로그램에 single sign-on을 설정 합니다. 시작, 사용 하려는 기존 디렉터리를 Azure Active Directory (Azure AD)에 있습니다. Microsoft Azure, Office 365 또는 Windows Intune을 통해 얻은 Azure AD 디렉터리를 사용할 수 있습니다. 이 중 두 개 이상의 경우 참조 [에서는 Azure AD 디렉터리 관리](active-directory-administer.md) toodetermine 어느 한 toouse 합니다.

> [!IMPORTANT]
> Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다. Admin 님 안녕하세요 Azure AD에서에서 관리자 역할 tooassign 센터 하는 방법에 대 한 참조 [Azure Active Directory에서 관리자 역할 할당](active-directory-enterprise-apps-manage-sso.md)합니다.

## <a name="authentication"></a>인증
응용 프로그램에 대해 지 원하는 Ws-federation, SAML 2.0 hello 또는 OpenID Connect 프로토콜, tooestablish 트러스트 관계 인증서를 서명 하는 Azure Active Directory 사용 합니다. 이에 대한 자세한 내용은 [페더레이션된 Single Sign-On에 대한 인증서 관리](active-directory-sso-certs.md)를 참조하세요.

Azure Active Directory 사용 하 여 '암호 보관' tooestablish만 HTML 양식 기반 로그인 지원 응용 프로그램에 대 한 트러스트 관계입니다. 이 통해 hello 사용자 조직 toobe에 자동으로 로그인 tooa hello hello SaaS 응용 프로그램 사용자 계정 정보를 사용 하 여 Azure AD에서 SaaS 응용 프로그램. Azure AD는 수집 하 고 안전 하 게 hello 사용자 계정 정보와 관련된 암호가 hello 저장 합니다. 자세한 내용은 [암호 기반 Single Sign-On](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)을 참조하세요.

## <a name="authorization"></a>권한 부여
프로 비전 된 계정에 single sign-on을 통해 인증 된 후 사용자 권한을 부여 toobe toouse를 응용 프로그램을 수 있습니다. 수동으로 또는 일부 경우에 추가 하 고 Azure Active Directory에서 수행한 변경을 기준 hello SaaS 응용 프로그램에서 사용자 정보를 제거할 수 사용자 프로 비전을 수행할 수 있습니다. 자동화된 프로비저닝을 위해 기존 Azure AD 커넥터를 사용하는 방법에 대한 자세한 내용은 [SaaS 응용 프로그램에 대한 자동화된 사용자 프로비저닝 및 프로비저닝 해제](active-directory-saas-app-provisioning.md)를 참조하세요.

그렇지 않은 경우 수동으로 사용자 정보 tooan 응용 프로그램을 추가 하거나 hello 시장에서 사용할 수 있는 다른 프로 비전 솔루션을 사용 하 여 수 있습니다.

## <a name="access"></a>Access
Azure AD는 사용자 지정 가능한 여러 가지 방법으로 toodeploy 응용 프로그램 tooend 조직의 사용자가 제공합니다. 특정 배포 또는 액세스 솔루션으로 제한되지 않으며, 사용할 수 있습니다 [hello 요구 사항에 가장 적합 한 솔루션](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)합니다.

## <a name="additional-considerations-for-applications-already-in-use"></a>이미 사용 중인 응용 프로그램에 대한 추가 고려 사항
새 응용 프로그램에 대 한 새 계정을 만드는 hello 프로세스에서 다른 프로세스를 이미 조직에서 사용 하는 응용 프로그램에 단일 로그인에 설정 합니다. 예비 단계는 두 가지가: hello 응용 프로그램 tooAzure AD id의 사용자 id 매핑 및 방법을 모드 통합 된 후 tooan 응용 프로그램에 로그인을 이해 합니다.

> [!NOTE]
> tooset 기존 응용 프로그램에 대 한 SSO를를 모두 Azure AD에서 toohave 전역 관리자 권한이 필요 하 고이 hello SaaS 응용 프로그램입니다.
>
>

### <a name="mapping-user-accounts"></a>사용자 계정 매핑
사용자의 ID에는 일반적으로 전자 메일 주소 또는 사용자 계정 이름(UPN)일 수 있는 고유 식별자가 있습니다. Toolink (map) 할 각 사용자의 응용 프로그램 id tootheir 해당 Azure AD id입니다. 되는 몇 가지 방법으로 tooaccomplish이 방법에 따라 응용 프로그램 인증의 hello 요구 사항이 있습니다.

Azure AD id 갖는 응용 프로그램 id 매핑 방법에 대 한 자세한 내용은 참조 [hello SAML 토큰에서 발급 된 클레임을 사용자 지정](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) 및 [프로 비전 하기 위한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)합니다.

### <a name="understanding-hello-users-log-in-experience"></a>Hello 사용자의 로그인 환경 이해
이미 사용 되는 응용 프로그램에 SSO를 통합할 때 반드시 사용자 경험 hello toorealize 영향을 받게 됩니다. 모든 응용 프로그램에 대 한 사용자가 자신의 Azure AD 자격 증명 toosign에서 사용 하 여 시작 합니다. 다른 포털 tooaccess hello 응용 프로그램을 사용 해야 수 있습니다.

Hello 응용 프로그램의 로그인 인터페이스에서 일부 응용 프로그램에 대 한 SSO를 수행할 수 있지만 다른 응용 프로그램에서는 hello 사용자는 중앙 포털을 통해 toogo와 같은 ([My Apps](http://myapps.microsoft.com) 또는 [Office365](http://portal.office.com/myapps))에서 toosign 합니다. Hello 다양 한 유형의 SSO 및 해당 사용자의 환경에 대 한 자세한 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

또 다른 중요 한 리소스는 *사용자 동의 억제* hello에 [Guiding 개발자](active-directory-applications-guiding-developers-for-lob-applications.md) 문서.

## <a name="next-steps"></a>다음 단계
Azure AD는 다양 한 hello 응용 프로그램 갤러리에서에서 제공 되는 SaaS 앱에 대 한 제공 [방법에 대 한 자습서 toointegrate SaaS 앱](active-directory-saas-tutorial-list.md)합니다.

응용 프로그램 응용 프로그램 갤러리에 없는 경우 다음을 할 수 있습니다 [사용자 지정 응용 프로그램으로 Azure AD 앱 갤러리 toohello 추가](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)합니다.

부터는 hello Azure.com 라이브러리에 이러한 문제가 모두에 훨씬 더 많은 세부 정보가 [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

또한 hello 잊지 [Azure Active Directory에 응용 프로그램 관리용 문서 인덱스](active-directory-apps-index.md)합니다.
