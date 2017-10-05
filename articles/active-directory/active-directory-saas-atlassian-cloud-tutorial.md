---
title: "자습서: Atlassian Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Atlassian Cloud 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>자습서: Atlassian Cloud와 Azure Active Directory 통합

이 자습서에서는 Atlassian Cloud와 Azure AD(Azure Active Directory)를 통합하는 방법에 대해 알아봅니다.

Atlassian Cloud를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Azure AD에서는 Atlassian Cloud에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.
- 사용자가 Azure AD 계정으로 Atlassian Cloud에 자동으로 로그인(Single Sign-on)할 수 있도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Atlassian Cloud와 Azure AD를 통합하도록 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Atlassian Cloud Single Sign-On 사용이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Atlassian Cloud 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-atlassian-cloud-from-the-gallery"></a>갤러리에서 Atlassian Cloud 추가
Azure AD에 Atlassian Cloud와 Azure AD를 통합하도록 구성하려면 갤러리의 Atlassian Cloud를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Atlassian Cloud를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Active Directory][1]

2. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![응용 프로그램][2]
    
3. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![응용 프로그램][3]

4. 검색 상자에서 **Atlassian Cloud**를 입력합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. 결과 패널에서 **Atlassian Cloud**를 선택하고 **추가** 단추를 클릭하여 해당 응용 프로그램을 추가합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 Atlassian Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 대응하는 Atlassian Cloud 사용자가 누구인지 알고 있어야 합니다. 즉 Azure AD 사용자와 Atlassian Cloud의 관련 사용자 간에 연결 관계가 설정되어야 합니다.

이 연결 관계는 Azure AD의 **사용자 이름** 값을 Atlassian Cloud의 **Username** 값으로 할당하여 설정합니다.

Atlassian Cloud에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
3. **[Atlassian Cloud 테스트 사용자 만들기](#creating-an-atlassian-cloud-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Atlassian Cloud에 만듭니다.
4. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Atlassian Cloud 응용 프로그램에서 Single Sign-On을 구성합니다.

**Atlassian Cloud에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Atlassian Cloud** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Single Sign-on 구성][4]

2. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. **Atlassian Cloud 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    a. **식별자** 텍스트 상자에서 `https://<instancename>.atlassian.net/admin/saml/edit` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 URL을 `https://id.atlassian.com/login/saml/acs`로 입력합니다.

4. **SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    **로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instancename>.atlassian.net`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자 및 로그온 URL로 해당 값을 업데이트합니다. Atlassian Cloud SAML 구성 화면에서 정확한 값을 가져올 수 있습니다.
 
5. **SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. **Atlassian Cloud 구성** 섹션에서 **Atlassian Cloud 구성**을 클릭하여 **로그온 구성** 창을 엽니다. **빠른 참조 섹션**에서 **SAML 엔터티 ID 및 SAML Single Sign-On 서비스 URL**을 복사합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. 응용 프로그램에 SSO를 구성하려면 관리자 권한으로 Atlassian Portal에 로그인합니다.

8. 왼쪽 탐색 모음의 [인증] 섹션에서 **도메인**을 클릭합니다.

    ![Single Sign-On 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    a. 텍스트 상자에서 도메인 이름을 입력한 다음 **도메인 추가**를 클릭합니다.
        
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b. 도메인을 확인하려면 **확인**을 클릭합니다. 

    ![Single Sign-On 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. 도메인 확인 HTML 파일을 다운로드하여 도메인 웹 사이트의 루트 폴더에 업로드한 다음 **도메인 확인**을 클릭합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. 도메인이 확인되면 **상태** 필드 값이 **확인됨**이 됩니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. 왼쪽 탐색 모음에서 **SAML**을 클릭합니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. SAML 구성을 만들고 ID 공급자 구성을 추가합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    a. Azure Portal에서 복사한 **SAML 엔터티 ID** 값을 **Identity provider Entity ID**(ID 공급자 엔터티 ID) 텍스트 상자에 붙여넣습니다.

    b. Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **ID 공급자 SSO URL** 텍스트 상자에 붙여넣습니다.

    c. Azure Portal에서 다운로드한 인증서를 열고 시작 및 끝 행을 제외한 값을 복사하여 **공용 X509 인증서** 상자에 붙여넣습니다.
    
    d. **구성 저장**을 클릭하여 설정을 저장합니다.
     
11. Azure AD 설정을 업데이트하여 올바른 식별자 URL을 설정했는지 확인합니다.
  
    a. SAML 화면에서 **SP Identity ID**(SP ID)를 복사하여 Azure AD에 **식별자** 값으로 붙여넣습니다.

    b. [로그인 URL]은 Atlassian Cloud의 테넌트 URL입니다.   

     ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. Azure Portal에서 **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> 이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.  **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다. 포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

![Azure AD 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. **사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. **사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    a. **이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.

    b. **사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.

    c. **암호 표시**를 선택하고 **암호** 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-atlassian-cloud-test-user"></a>Atlassian Cloud 테스트 사용자 만들기

Azure AD 사용자가 Atlassian Cloud에 로그인할 수 있도록 하려면 Atlassian Cloud로 프로비전되어야 합니다.  
Atlassian Cloud의 경우 프로비전이 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. [사이트 관리] 섹션에서 **사용자** 단추를 클릭합니다.

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Atlassian Cloud에서 사용자를 만들기 위해 **사용자 만들기** 단추를 클릭합니다.

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. 사용자의 **메일 주소**, **사용자 이름** 및 **전체 이름**을 입력하고 응용 프로그램 액세스 권한을 할당합니다. 

    ![Atlassian Cloud 사용자 만들기](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. **사용자 만들기** 단추를 클릭하면 사용자에게 메일 초대장을 보내고 이 초대를 수락하면 해당 사용자가 시스템에서 활성화됩니다. 

>[!NOTE] 
>[사용자] 섹션에서 **대량 만들기** 단추를 클릭하여 대량으로 사용자를 만들 수도 있습니다.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Atlassian Cloud에 대한 액세스 권한을 부여합니다.

![사용자 할당][200] 

**Britta Simon을 Atlassian Cloud에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

2. 응용 프로그램 목록에서 **Atlassian Cloud**를 선택합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트합니다.

[액세스 패널]에서 [Atlassian Cloud] 타일을 클릭하면 Atlassian Cloud 응용 프로그램에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요. 

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

