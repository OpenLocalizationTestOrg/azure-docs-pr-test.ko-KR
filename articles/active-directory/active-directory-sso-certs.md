---
title: "Azure AD의 페더레이션 인증서 aaaManage | Microsoft Docs"
description: "어떻게 toorenew 인증서는 페더레이션 인증서에 사용 되는 hello 만료 날짜 toocustomize 곧 만료 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Azure Active Directory에서 페더레이션된 Single Sign-On에 대한 인증서 관리
이 문서에서는 일반적인 질문 및 Azure Active Directory (Azure AD) tooestablish 만들어지는 toohello 인증서 페더레이션된 single sign-on (SSO) tooyour SaaS 응용 프로그램 관련 정보입니다. Hello Azure AD 앱 갤러리에서 또는 비 갤러리 응용 프로그램 템플릿을 사용 하 여 응용 프로그램을 추가 합니다. Hello 페더레이션 SSO 옵션을 사용 하 여 hello 응용 프로그램을 구성 합니다.

이 문서는 있는 통해 SAML 페더레이션 구성된 toouse Azure AD SSO 관련만 tooapps hello 다음 예제와 같이:

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>갤러리 및 비갤러리 응용 프로그램에 대해 자동 생성된 인증서
Hello 갤러리에서 새 응용 프로그램을 추가 하는 SAML 기반 로그온을 구성 하는 경우 Azure AD는 3 년 동안 유효 하는 hello 응용 프로그램에 대 한 인증서를 생성 합니다. Hello에서이 인증서를 다운로드할 수 있습니다 **SAML 서명 인증서** 섹션. 갤러리 응용 프로그램에 대 한이 섹션은 옵션 toodownload hello 인증서 또는 hello 응용 프로그램의 hello 요구 사항에 따라 메타 데이터를 표시할 수 있습니다.

![Azure AD Single Sign-On](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>페더레이션 인증서에 대 한 hello 만료 날짜를 사용자 지정 하 고 tooa 새 인증서 롤오버
인증서는 기본적으로 3 년 후 tooexpire를 설정 됩니다. Hello 다음 단계를 완료 하 여 인증서에 대 한 다른 만료 날짜를 선택할 수 있습니다.
hello 스크린샷에서 Salesforce 등의 hello 위해서 사용 하 여 하지만 다음이 단계는 tooany 페더레이션 SaaS 응용 프로그램을 적용할 수 있습니다.

1. Hello에 [Azure 포털](https://aad.portal.azure.com), 클릭 **엔터프라이즈 응용 프로그램** 왼쪽된 창의 hello와 클릭 **새 응용 프로그램** hello에 **개요** 페이지:

   ![열기 hello SSO 구성 마법사](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Hello 갤러리 응용 프로그램에 대 한 검색 하 고 원하는 tooadd hello 응용 프로그램을 선택 합니다. Hello 필요한 응용 프로그램을 찾을 수 없으면 hello를 사용 하 여 hello 응용 프로그램을 추가 **비 갤러리 응용 프로그램** 옵션입니다. 이 기능은 Azure AD Premium (P1 및 P2) SKU hello 에서만 사용할 수 있습니다.

    ![Azure AD Single Sign-On](./media/active-directory-sso-certs/add_gallery_application.png)

3. Hello 클릭 **Single sign on** 링크의 왼쪽 창에서 데이터 및 변경 하는 hello **Single Sign on 모드** 너무**SAML 기반 로그온**합니다. 이 단계에서는 응용 프로그램에 대해 3년 유효 인증서를 생성합니다.

4. 새 인증서를 toocreate 클릭 hello **새 인증서 만들기** hello에 대 한 링크 **SAML 서명 인증서** 섹션.

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

5. hello **새 인증서를 만들** 링크 hello 달력 컨트롤을 엽니다. 에서 설정할 수 있습니다 날짜 및 시간을 toothree 년 hello 현재 날짜입니다. hello 날짜를 선택 하 고 새로운 만료 날짜로 hello와 새 인증서의 시간 시간입니다. **Save**를 클릭합니다.

    ![다운로드 한 다음 hello 인증서 업로드](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. 이제 hello 새 인증서는 사용할 수 있는 toodownload입니다. Hello 클릭 **인증서** 링크 toodownload 것입니다. 이 시점에서 인증서는 활성 상태가 아닙니다. Toothis 인증서를 통해 tooroll 하려는 경우 선택 hello **새 인증서를 활성화할** 확인란과 클릭 **저장**합니다. 해당 시점에서 Azure AD 서명 hello 응답에 대 한 hello 새 인증서를 사용 하 여 시작 합니다.

7.  toolearn tooupload hello tooyour 특정 SaaS 응용 프로그램 인증서 방법 클릭 hello **보기 응용 프로그램 구성 자습서** 링크 합니다.

## <a name="renew-a-certificate-that-will-soon-expire"></a>곧 만료되는 인증서 갱신
hello 다음 갱신 단계를 유발 사용자에 게 중요 한 중단 되지 않습니다. 예를 들어 있지만 이러한 단계가이 섹션 기능 Salesforce에서에서 hello 스크린 샷 tooany 페더레이션 SaaS 응용 프로그램을 적용할 수 있습니다.

1. Hello에 **Azure Active Directory** 응용 프로그램 **Single sign on** 페이지에서 응용 프로그램에 대 한 hello 새 인증서를 생성 합니다. Hello를 클릭 하 여이 작업을 수행할 수 **새 인증서 만들기** hello에 대 한 링크 **SAML 서명 인증서** 섹션.

    ![새 인증서 생성](./media/active-directory-sso-certs/create_new_certficate.png)

2. 만료 날짜와 새 인증서에 해당 시간 선택 hello 원하는 **저장**합니다.

3. Hello에 hello 인증서 다운로드 **SAML 서명 인증서** 옵션입니다. Hello 새 인증서 toohello SaaS 응용 프로그램의 single sign on 구성 화면을 업로드 합니다. toolearn 어떻게 toodo 특정 SaaS 응용 프로그램에 대 한이 클릭 hello **보기 응용 프로그램 구성 자습서** 링크 합니다.
   
4. Azure ad에서는 선택 hello tooactivate hello 새 인증서 **새 인증서를 활성화할** 확인란을 클릭 hello **저장** hello hello 페이지 위쪽에 단추입니다. 이 hello 새 인증서를 통해 Azure AD 쪽 hello에 롤업합니다. hello 인증서의 hello 상태에서 변경 **새로** 너무**활성**합니다. 해당 시점에서 Azure AD 서명 hello 응답에 대 한 hello 새 인증서를 사용 하 여 시작 합니다. 
   
    ![새 인증서 생성](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>관련 문서
* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)
* [SAML 기반 Single Sign-On 문제 해결](active-directory-saml-debugging.md)
