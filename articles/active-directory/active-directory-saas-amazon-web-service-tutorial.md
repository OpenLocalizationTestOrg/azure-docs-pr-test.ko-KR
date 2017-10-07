---
title: "자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 웹 서비스 AWS (Amazon) 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate 서비스 AWS (Amazon Web) Azure Active directory (Azure AD).

다음 이점을 hello로 제공 서비스 AWS (Amazon Web) Azure AD와 통합:

- Azure ad 액세스 tooAmazon AWS (웹 서비스)를 가진 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooAmazon AWS (Web Services) (Single Sign-on)를 사용할 수 있습니다.
- 하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>필수 조건

Azure AD 통합 된 웹 서비스 AWS (Amazon) tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- AWS(Amazon Web Services) Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 웹 서비스 AWS (Amazon)를 추가합니다.
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Hello 갤러리에서 웹 서비스 AWS (Amazon)를 추가합니다.
Azure AD로 tooconfigure hello 통합의 서비스 AWS (Amazon Web), 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 웹 서비스 AWS (Amazon) tooadd가 필요합니다.

**tooadd 서비스 AWS (Amazon Web) hello 갤러리에서 hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **서비스 AWS (Amazon Web)**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. Hello 결과 패널에서 선택 **서비스 AWS (Amazon Web)**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AWS(Amazon Web Services)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow hello 테이블에 해당 사용자의 웹 서비스 AWS (Amazon)가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 hello 관련된 사용자의 웹 서비스 AWS (Amazon) 사이의 링크 관계를 toobe 설정 해야 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 웹 서비스 AWS (Amazon).

tooconfigure 및 Azure AD에서 single sign-on 테스트와 웹 서비스 AWS (Amazon) 빌딩 블록을 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Amazon 웹 서비스 테스트 사용자 만들기](#creating-an-amazon-web-services-test-user)**  -toohave Britta Simon의 웹 서비스 AWS (Amazon) 표현인 연결 된 Azure AD toohello 그녀의 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 서비스 AWS (Amazon Web) 응용 프로그램에서 single sign on 구성 합니다.

**와 서비스 AWS (Amazon Web), Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 포털에서에서 **서비스 AWS (Amazon Web)** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Hello에 **서비스 AWS (Amazon Web) 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. hello 서비스 AWS (Amazon Web) 소프트웨어 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다. 이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오. Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.
    
    | 특성 이름  | 특성 값 | 네임스페이스 |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
    | 역할            | user.assignedroles |  https://aws.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Tooconfigure hello 사용자 AWS 콘솔에서 모든 hello 역할 toofetch Azure AD에에서 프로 비전 해야 합니다. 다음 단계를 프로 비전 하는 hello를 참조 하십시오.

    a. 클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다. 위에 지정 된 hello Namespace 값을 추가 합니다.
    
    d. **Ok**를 클릭합니다.

7. 클릭 **저장** Azure의 hello 설정을 toosave 단추입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. 다른 브라우저 창에서 관리자 권한으로 로그온 tooyour 서비스 AWS (Amazon Web) 회사 사이트입니다.

9. **콘솔 홈**을 클릭합니다.
   
    ![Single Sign-On 구성][11]

10. **Security, Identity & Compliance(보안, ID 및 규정 준수)** 서비스에서 **IAM**을 클릭합니다.
   
    ![Single Sign-on 구성][12]

11. **ID 공급자**를 클릭한 다음 **공급자 만들기**를 클릭합니다.
   
    ![Single Sign-on 구성][13]

12. Hello에 **공급자 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Single Sign-on 구성][14]
 
    a. **공급자 유형**으로 **SAML**을 선택합니다.

    b. Hello에 **공급자 이름** 텍스트 상자에 공급자 이름 (예:: *WAAD*).

    c. tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **파일 선택**합니다.

    d. **다음 단계**를 클릭합니다.

13. Hello에 **공급자 정보 확인** 대화 상자 페이지에서 클릭 **만들기**합니다. 
    
    ![Single Sign-on 구성][15]

14. **역할**을 클릭하고 **새 역할 만들기**를 클릭합니다. 
    
    ![Single Sign-on 구성][16]

15. Hello에 **역할 이름 설정** 대화 상자에서 hello 다음 단계를 수행 합니다. 
    
    ![Single Sign-on 구성][17] 

    a. Hello에 **역할 이름** textbox 역할 이름을 입력 (예:: *TestUser*). 

    b. **다음 단계**를 클릭합니다.

16. Hello에 **역할 유형 선택** 대화 상자에서 hello 다음 단계를 수행 합니다. 
    
    ![Single Sign-on 구성][18] 

    a. **ID 공급자 액세스에 대한 역할**을 선택합니다. 

    b. Hello에 **액세스 tooSAML 공급자가 부여 웹 Single Sign-on (WebSSO)** 섹션에서 클릭 **선택**합니다.

17. Hello에 **신뢰 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.  
    
    ![Single Sign-on 구성][19] 

    a. SAML 공급자 이전에 만든 hello SAML 공급자 선택 (예:: *WAAD*)
  
    b. **다음 단계**를 클릭합니다.

18. Hello에 **역할 트러스트 확인** 대화 상자를 클릭 하 여 **다음 단계**합니다.
    
    ![Single Sign-on 구성][32]

19. Hello에 **정책 연결** 대화 상자를 클릭 하 여 **다음 단계**합니다.
    
    ![Single Sign-on 구성][33]

20. Hello에 **검토** 대화 상자에서 hello 다음 단계를 수행 합니다.
    
    ![Single Sign-on 구성][34]
 
    a. **역할 만들기**를 클릭합니다.

    b. 필요에 따라 역할 만들고 toohello Id 공급자에 매핑하십시오.

21. 이제 hello 사용자 toofetch 프로 비전을 AWS에서 모든 hello 역할 구성

    a. 루트 계정으로 hello AWS 콘솔 로그인

    b. Hello 상단 오른쪽 모서리에서 프로그램 이름을 클릭 하 고 클릭 hello **내 보안 자격 증명** 옵션입니다. 그러면 화면이 경고 메시지로 열립니다. Hello 단추 클릭 **보안 자격 증명** 단추 toopass hello 화면입니다.
        
       ![Single Sign-on 구성][36]

       ![Single Sign-On 구성][37]

    c. 선택 키 hello 섹션 클릭 hello **새 액세스 키 만들기** 단추입니다. 액세스 키 ID hello와 토큰 값을 생성합니다.
    
       ![Single Sign-on 구성][38]

    d. 이 값을 읽어버리지 않도록 모두 복사하고 다운로드합니다.

    e. Hello 서비스 AWS (Amazon Web) 응용 프로그램 통합 페이지에서 hello Azure 포털에서에서 클릭 **프로 비전**합니다.
        
       ![Single Sign-on 구성][35]

    f. 너무 hello 프로 비전 모드를 설정**자동**
        
       ![Single Sign-on 구성][39]

    g. Hello에 이제 **clientsecret** 및 **암호 토큰** AWS 콘솔에서 복사한는 hello 해당 값을 붙여 넣습니다.
    
    h. Hello를 클릭할 수 있는 **연결 테스트** tootest hello 연결 단추입니다. 성공적으로 수행 되 면 hello 커넥터를 프로 비전을 시작할 수 있습니다.
       
       ![Single Sign-on 구성][40]

    i. 이제 hello 프로 비전 상태를 너무 하도록**에**합니다. 이 hello 역할 hello 응용 프로그램에서 가져오기 시작 합니다.

       ![Single Sign-on 구성][41]

    > [!NOTE]
    > Azure AD 프로 비전 서비스를 실행 후 AWS 일부 시간 toosync hello 역할 마다. 표시 되어야 모든 hello Id 공급자로 Azure AD로 AWS 역할을 연결 하 고 응용 프로그램 toousers hello 또는 그룹을 할당 하는 동안 사용할 수 있습니다.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-an-amazon-web-services-test-user"></a>AWS(Amazon Web Services) 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog tooAmazon AWS (웹 서비스)의 주문 하 고에 이들에 웹 서비스 AWS (Amazon) 프로 비전 해야 합니다. 웹 서비스 AWS (Amazon) hello 경우에서 프로 비전은 수동 작업입니다.

**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**

1. Tooyour 로그인 **서비스 AWS (Amazon Web)** 회사 사이트에서 관리자 권한으로 로그인 합니다.

2. Hello 클릭 **콘솔 홈** 아이콘입니다. 
   
    ![Single Sign-on 구성][11]

3. ID 및 액세스 관리를 클릭합니다. 
   
    ![Single Sign-on 구성][28]

4. Hello 대시보드, 클릭 **사용자**, 클릭 하 고 **새 사용자 만들기**합니다. 
   
    ![Single Sign-on 구성][29]

5. Hello 사용자 만들기 대화 상자에서 hello 다음 단계를 수행 합니다. 
   
    ![Single Sign-on 구성][30]   
    
    a. Hello에 **사용자 이름 입력** 텍스트 상자, Azure AD에서 Brita Simon의 사용자 이름 (userprincipalname)을 입력 합니다.

    b. **만들기**를 클릭합니다.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooAmazon AWS (웹 서비스)을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooAmazon AWS (웹 서비스), hello 다음 단계를 수행 합니다.**

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **서비스 AWS (Amazon Web)**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **역할 선택** 선택 hello hello 사용자에 대 한 적절 한 역할, 탭 합니다. 이러한 모든 역할 hello 역할 이름 및 id 공급자 이름으로 표시 됩니다. 이러한 방식으로 AWS의 역할을 hello를 쉽게 식별할 수 있습니다.

8. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 서비스 AWS (Amazon Web) hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour 서비스 AWS (Amazon Web) 응용 프로그램을 구해야 합니다. 

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
