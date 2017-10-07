---
title: "자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 Azure Active Directory 사이 로그온 하 고 SAP HANA 클라우드 플랫폼 Id 인증 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>자습서: SAP HANA Cloud Platform Identity Authentication과 Azure Active Directory 통합

이 자습서에 알아봅니다 방법을 toointegrate SAP HANA 클라우드 플랫폼 Id Azure Active Directory (Azure AD) 인증 합니다. SAP HANA 클라우드 플랫폼 Id 인증 된 프록시 IdP tooaccess SAP 응용 프로그램 주 IdP hello 대로 Azure AD를 사용 하 여으로 사용 됩니다.

SAP HANA 클라우드 플랫폼 Id 인증 Azure AD와 통합 hello 다음 이점을 제공 합니다.

- Access tooSAP 응용 프로그램을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자가 tooautomatically get 로그온 tooSAP 응용 프로그램 single sign-on (SSO) 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.


## <a name="prerequisites"></a>필수 조건

SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- **SAP HANA Cloud Platform Identity Authentication** SSO가 설정된 구독


>[!NOTE] 
>이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.
>

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 추가
2. Azure AD SSO 구성 및 테스트

Hello 기술 세부 정보를 알아보기 전에 중요 한 toounderstand hello 개념에서 toolook 거 것 합니다. SAP HANA 클라우드 플랫폼 Id 인증 및 Azure Active Directory 페더레이션 hello tooimplement을 SSO 응용 프로그램 또는 SAP 응용 프로그램 및 SAP HANA 클라우드 플랫폼 Id에 의해 보호 되는 서비스 (IdP)으로 AAD로 보호 되는 서비스 간에 수 있습니다. 인증입니다.

현재 SAP HANA 클라우드 플랫폼 Id 인증 된 프록시 Id 공급자 tooSAP-응용 프로그램으로 동작합니다. 이 설치 프로그램에서 Id 공급자를 선행 hello azure Active Directory 역할을 다시 합니다. 

다음 다이어그램 hello이를 보여줍니다.    

![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

이 설정을 통해 SAP HANA Cloud Platform Identity Authentication 테넌트가 Azure Active Directory에서 신뢰할 수 있는 응용 프로그램으로 구성됩니다. 

모든 SAP 응용 프로그램 및 서비스 tooprotect이이 방법을 통해 원하는 hello SAP HANA 클라우드 플랫폼 Id 인증 관리 콘솔에서 구성 됩니다!

(Azure Active Directory에서 것과 반대로 tooconfiguring 권한 부여)으로 이러한 설치에 대 한 요구 tootake 위치에서 SAP HANA 클라우드 플랫폼 Id 인증 서비스 이며 tooSAP 응용 프로그램 액세스 허용을 위한 해당 권한 부여를 의미 합니다.

SAP HANA 클라우드 플랫폼 Id 인증 hello Azure Active Directory Marketplace를 통해 응용 프로그램을 구성 하 여 필요한 개별 클레임 구성 care of tootake 않아도 / SAML 어설션 및 변환 필요한 tooproduce는 SAP 응용 프로그램에 대 한 유효한 인증 토큰입니다.

>[!NOTE] 
>현재 웹 SSO는 두 파티에서만 테스트되었습니다. 앱-API 또는 API-API 통신에 필요한 흐름은 작동하지만 아직 테스트되지 않았습니다. 후속 작업의 일부로 테스트될 예정입니다.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 추가
tooconfigure hello와의 통합 SAP HANA 클라우드 플랫폼 Id 인증 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SAP HANA 클라우드 플랫폼 Id 인증 tooadd가 필요합니다.

**hello 갤러리에서 SAP HANA 클라우드 플랫폼 Id 인증 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 [ **Azure 관리 포털**](https://portal.azure.com), 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **SAP HANA 클라우드 플랫폼 Id 인증**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. Hello 결과 패널에서 선택 **SAP HANA 클라우드 플랫폼 Id 인증**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP HANA Cloud Platform Identity Authentication에서 Azure AD SSO를 구성하고 테스트합니다.

SSO toowork에 대 한 Azure AD는 tooknow SAP HANA 클라우드 플랫폼 Id 인증에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 SAP HANA 클라우드 플랫폼 Id 인증에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 SAP HANA 클라우드 플랫폼 Id 인증 합니다.

tooconfigure 및 SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD SSO 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SAP HANA 클라우드 플랫폼 Id 인증 테스트 사용자 만들기](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave Britta Simon SAP HANA 클라우드 플랫폼 Identity 인증 시 그녀의 연결 된 Azure AD toohello 표현에에서 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-sso"></a>Azure AD SSO 구성

이 섹션에서는 hello Azure 관리 포털에서 Azure AD SSO를 사용 하도록 설정 및 SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램에서 single sign on 구성 합니다.

SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.

![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**SAP HANA 클라우드 플랫폼 Id 인증와 Azure AD SSO tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **SAP HANA 클라우드 플랫폼 Id 인증** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성][5]

3. Hello에 **사용자 특성** hello 섹션 **Single sign on** 경우 대화 상자, SAP 응용 프로그램의 예를 들어 "firstName" 특성이 필요 합니다. Hello SAML 토큰 특성 대화 상자에서 hello "firstName" 특성을 추가 합니다.
 1. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.
 
    ![Single Sign-on 구성][6]

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. Hello에 **특성 이름** 텍스트 형식 hello 특성 이름 "firstName"입니다.
 3. Hello에서 **특성 값** "user.givenname" 선택 hello 특성 값을 나열 합니다.
 4. **Ok**를 클릭합니다.

4. Hello에 **SAP HANA 클라우드 플랫폼 Identity 인증 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. Hello에 **로그온 URL** textbox hello SAP 응용 프로그램에 대 한 URL에 hello 기호를 입력 합니다.
 2. Hello에 **식별자** 텍스트 패턴 형식 hello 값:`<entity-id>.accounts.ondemand.com` 
    * 이 값을 모르는 경우에 따라 하십시오 hello SAP HANA 클라우드 플랫폼 Id 인증 설명서 [테 넌 트 SAML 2.0 구성](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)합니다.

5. Hello에 **SAP HANA 클라우드 플랫폼 Identity 인증 구성** 섹션에서 클릭 **SAP HANA 클라우드 플랫폼 Id 인증 구성** tooopen **signon구성** 대화 상자. 그런 다음 클릭 **SAML XML 메타 데이터** hello 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. SSO 응용 프로그램에 대해 구성 된 tooget tooSAP HANA 클라우드 플랫폼 Identity 인증 관리 콘솔을 이동 합니다. hello URL 패턴 hello에 있습니다.`https://<tenant-id>.accounts.ondemand.com/admin`
 * 그런 다음 hello 설명서 SAP HANA 클라우드 플랫폼 Id 인증에 너무 따라[SAP HANA 클라우드 플랫폼 Id 인증에 회사 Id 공급자로 구성 Microsoft Azure AD](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)합니다. 

7. Hello Azure 관리 포털에서 클릭 **저장** 단추입니다.
8. Hello tooadd을 다른 SAP 응용 프로그램에 SSO를 사용 하는 경우에 다음 단계를 계속 합니다. SAP HANA 클라우드 플랫폼 Id 인증의 다른 인스턴스가 hello 섹션 "추가 SAP HANA 클라우드 플랫폼 Id 인증 hello 갤러리에서" tooadd 아래 단계를 반복 합니다.
9. Hello에 hello Azure 관리 포털에서 **SAP HANA 클라우드 플랫폼 Id 인증** 응용 프로그램 통합 페이지에서 클릭 **연결 된 로그온**합니다.

    ![연결된 로그온 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. 그런 다음 hello 구성을 저장 합니다.

>[!NOTE] 
>hello 새 응용 프로그램 hello 이전 SAP 응용 프로그램에 대 한 hello SSO 구성을 활용 됩니다. 있는지 확인 하십시오 있습니다 사용할 hello hello SAP HANA 클라우드 플랫폼 Identity 인증 관리 콘솔의에서 동일한 회사 Id 공급자입니다.
>

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 Britta Simon 라는 hello 새로운 포털에서 toocreate 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.
  2. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.
  3. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.
  4. **만들기**를 클릭합니다. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>SAP HANA Cloud Platform Identity Authentication 테스트 사용자 만들기

SAP HANA 클라우드 플랫폼 Id 인증 된 사용자 toocreate가 필요는 없습니다. Hello Azure AD 사용자 저장소에 있는 사용자를 hello SSO 기능을 사용할 수 있습니다.

SAP HANA 클라우드 플랫폼 Id 인증 hello Id 페더레이션이 옵션을 지원합니다. 이 옵션 hello 회사 id 공급자에 의해 인증 된 hello 사용자의 hello 사용자 저장소의 SAP HANA 클라우드 플랫폼 Id 인증 존재 하는 경우 응용 프로그램 toocheck hello를 허용 합니다. 

Hello 기본 설정에서 hello Id 페더레이션이 옵션은 사용할 수 없습니다. Id 페더레이션을 사용 하는 경우 SAP HANA 클라우드 플랫폼 Id 인증에서 가져온 hello 사용자만 수 tooaccess hello 응용 프로그램을 있습니다. 

Tooenable 또는 사용 안 함 Id 페더레이션이 SAP HANA 클라우드 플랫폼 Identity 인증을 확인 하려면 어떻게 해야 Id 페더레이션이 SAP HANA 클라우드 플랫폼 Identity 인증에 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [Id 페더레이션 구성 사용자 저장소의 SAP HANA 클라우드 플랫폼 Id 인증 안녕하세요와. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 그녀의 액세스 tooSAP HANA 클라우드 플랫폼 Id 인증 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSAP HANA 클라우드 플랫폼 Id 인증 hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SAP HANA 클라우드 플랫폼 Id 인증**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.

Hello 액세스 패널에서에서 hello SAP HANA 클라우드 플랫폼 Id 인증 타일을 클릭할 때 자동으로 로그온 tooyour SAP HANA 클라우드 플랫폼 Id 인증 응용 프로그램을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png