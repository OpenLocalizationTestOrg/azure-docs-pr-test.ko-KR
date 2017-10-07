---
title: "자습서: Cisco Webex와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 toouse Cisco Webex와 Azure Active Directory tooenable single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>자습서: Cisco Webex와 Azure Active Directory 통합
hello이이 자습서는 Azure와 Cisco Webex tooshow hello 통합 합니다.  
이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Cisco Webex 테넌트

이 자습서를 완료 한 후 할당 한 Webex 됩니다 tooCisco 수 toosingle 기호 hello 응용 프로그램으로 Cisco Webex 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 Azure AD 사용자 hello 또는 hello를 사용 하 여 [toohello 소개 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

* Cisco Webex에 대 한 hello 응용 프로그램 통합 사용
* SSO(Single Sign-On) 구성
* 사용자 프로비전 구성
* 사용자 할당

![시나리오](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "시나리오")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Cisco Webex에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정
hello이이 섹션의 목적은 toooutline 어떻게 Cisco Webex에 대 한 tooenable hello 응용 프로그램 통합 합니다.

**Cisco Webex에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Cisco Webex**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Cisco Webex**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCisco Webex hello SAML 프로토콜에 따라 하는 방법입니다.  

이 절차의 일부로 필수 toocreate e-64로 인코딩된 인증서 됩니다. 이 절차에 익숙하지 않은 경우 참조 [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooCisco Webex에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Single Sign-On 구성")
3. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "앱 URL 구성")   
   1. Hello에 **로그온 URL** 텍스트 상자에 Cisco Webex 테 넌 트 URL (예:: *http://contoso.webex.com*).
   2. Hello에 **Cisco Webex 회신 URL** 텍스트 상자에을 입력 하면 **Cisco Webex AssertionConsumerService URL** (예:: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Hello에 **Cisco Webex에서 single sign on 구성** 페이지, toodownload 인증서를 클릭 하 여 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Single Sign-On 구성")
5. 다른 웹 브라우저 창에서 Cisco Webex 회사 사이트에 관리자로 로그인합니다.
6. Hello 메뉴에서 hello 위에 표시를 클릭 **사이트 관리**합니다.
   
   ![사이트 관리](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "사이트 관리")
7. Hello에 **사이트 관리** 섹션에서 클릭 **SSO 구성**합니다.
   
   ![SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO 구성")
8. Hello 페더레이션 웹 SSO 구성 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.
   
   ![페더레이션 SSO 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "페더레이션 SSO 구성")  
   1. Hello에서 **페더레이션 프로토콜** 목록에서 **SAML 2.0**합니다.
   2. 다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.  
    >[!TIP]
    >자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. 메모장을 선택한 다음의 콘텐츠 복사 hello에서 e-64로 인코딩된 인증서를 엽니다.
   4. **SAML 메타데이터 가져오기**를 클릭하고 Base-64로 인코딩된 인증서를 붙여 넣습니다.
   5. Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **(IdP ID)SAML발급자** 텍스트 상자에 붙여넣습니다.
   6. Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **고객 SSO 서비스 로그인 URL** 텍스트 상자에 붙여넣습니다.
   7. Hello에서 **NameID 형식** 목록에서 **전자 메일 주소**합니다.
   8. Hello에 **AuthnContextClassRef** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:ac:classes:Password**합니다.
   9. Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그 아웃 URL** 값을 복사한 다음 hello에 붙여 넣을 **고객 SSO 서비스 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.
   10. **업데이트**를 클릭합니다.
9. Hello hello에 Azure 클래식 포털에서에서 **Cisco Webex에서 single sign on 구성** 대화 상자 페이지에서 hello single sign on 구성 확인을 선택한 다음 클릭 **완료**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Single Sign-On 구성")
   
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

Tooenable Azure AD 사용자가 toolog Cisco Webex에 주문 하 고에 Cisco Webex에 이들 프로 비전 해야 합니다.  

* Hello Cisco Webex의 경우에서 프로 비전은 수동 작업입니다.

**사용자 계정 수행 tooprovision hello 다음 단계:**

1. Tooyour 로그인 **Cisco Webex** 테 넌 트입니다.
2. 너무 이동**사용자 관리 \> 사용자 추가**합니다.
   
   ![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "사용자 추가")
3. 사용자 추가 섹션 hello hello 다음 단계를 수행 합니다.
   
   ![사용자 추가](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "사용자 추가")   
   1. **계정 유형**으로 **호스트**를 선택합니다.
   2. Hello 다음 텍스트 상자에 기존 Azure AD 사용자의 hello 정보를 입력: **이름, 성**, **사용자 이름**, **전자 메일**, **암호**, **암호 확인**합니다.
   3. **추가**를 클릭합니다.

>[!NOTE]
>다른 Cisco Webex 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Cisco Webex에서 제공 된 Api입니다. 
> 

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooCisco Webex hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 **Cisco Webex** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

