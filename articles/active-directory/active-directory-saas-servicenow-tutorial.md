---
title: "자습서: ServiceNow와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ServiceNow ServiceNow Express 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>자습서: ServiceNow와 Azure Active Directory 통합
이 자습서에 설명 어떻게 toointegrate ServiceNow와 Azure Active Directory (Azure AD)와 ServiceNow Express입니다.

Azure AD와 ServiceNow 및 Express ServiceNow를 통합 hello 다음 이점을 제공 합니다.

* 액세스 tooServiceNow을 지닌 Azure AD와 ServiceNow Express에서 제어할 수 있습니다.
* Azure AD 계정을와 tooServiceNow 로그온 사용자 tooautomatically get 및 ServiceNow Express (Single Sign-on)를 사용할 수 있습니다.
* 하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
ServiceNow 및 Express ServiceNow와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

* Azure AD 구독
* ServiceNow의 경우 ServiceNow의 인스턴스 또는 테넌트, Calgary 버전 이상
* ServiceNow Express의 경우 ServiceNow Express의 인스턴스, Helsinki 버전 이상
* hello ServiceNow 테 넌 트 hello 있어야 [여러 공급자 Single Sign에 플러그 인](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) 사용 하도록 설정 합니다. [서비스 요청을 제출](https://hi.service-now.com)하면 이렇게 설정할 수 있습니다. 

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.
> 
> 

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

* 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
* Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. ServiceNow는 hello 갤러리 추가
2. ServiceNow 또는 ServiceNow Express에 대한 Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-servicenow-from-hello-gallery"></a>ServiceNow는 hello 갤러리 추가
tooconfigure hello와의 통합 ServiceNow 또는 ServiceNow Express Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ServiceNow tooadd가 필요합니다. 

**hello 갤러리에서 ServiceNow tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. 
   
    ![Active Directory][1]
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램][2]
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3]
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![응용 프로그램][4]
6. Hello 검색 상자에 입력 **ServiceNow**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Hello 결과 창에서 선택 **ServiceNow**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ServiceNow 또는 ServiceNow Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow ServiceNow에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 ServiceNow의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.
Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ServiceNow에 합니다. tooconfigure와 ServiceNow 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[ServiceNow에 대 한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[ServiceNow Express에 대 한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable 사용자 toouse이이 기능입니다.
3. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
4. **[ServiceNow 테스트 사용자 만들기](#creating-a-servicenow-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 ServiceNow에 해당 하는 도구입니다.
5. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
6. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

> [!NOTE]
> Tooconfigure ServiceNow를 원하는 경우에 2 단계를 생략 합니다. 마찬가지로, tooconfigure ServiceNow Express 하려면 1 단계를 생략 합니다.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>ServiceNow에 대한 Azure AD Single Sign-On 구성
1. Hello에 Azure AD hello 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자 .
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")

2. Hello에 **어떻게 tooServiceNow에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")

3. Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")
   
    a. hello에 **ServiceNow 로그온 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.
   
    b. Hello에 **식별자** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.
   
    c. **다음**을 누릅니다

4. Azure AD toohave 자동으로 ServiceNow SAML 기반 인증에 대 한 구성, hello에 ServiceNow 인스턴스 이름, 관리자 사용자 이름 및 관리자 암호를 입력 **자동 single sign on 구성** 형태와 클릭  *구성*합니다. 제공 된 해당 hello 관리자 권한을 가진 사용자는 hello 해야 **security_admin** 이 toowork에 대 한 ServiceNow에 할당 된 역할입니다. 그렇지 않으면 toomanually ServiceNow toouse Azure AD SAML id 공급자로 구성, 클릭 **hello 응용 프로그램에 single sign-on에 대 한 수동 구성**, 클릭 **다음** 및 전체 hello 다음 단계입니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")

5. Hello에 **ServiceNow에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")

6. 로그온 tooyour 관리자 권한으로 ServiceNow 응용 프로그램입니다.

7. Hello 활성화 *통합-여러 공급자 Single Sign-on 설치 관리자* 플러그 인에 따라 다음 단계를 hello:
   
    a. Hello 왼쪽에 hello 탐색 창에서 이동 너무**시스템 정의** 섹션 및 클릭 **플러그 인**합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "플러그 인 활성화")
   
    b. *통합 - 여러 공급자 Single Sign-On 설치 관리자*를 검색합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "플러그 인 활성화")
   
    c. Hello 플러그 인을 선택 합니다. 마우스 오른쪽을 클릭하고 **활성화/업그레이드**를 선택합니다.
   
    d. Hello 클릭 **Activate** 단추입니다.

8. Hello 왼쪽에 hello 탐색 창에서 클릭 **속성**합니다.  
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "앱 URL 구성")

9. Hello에 **여러 공급자 SSO 속성** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "앱 URL 구성")
   
    a. **여러 공급자 SSO 사용**을 **예**로 선택합니다.
   
    b. 으로 **내용이 디버그 로깅을 사용 hello 여러 공급자 SSO 통합**선택, **예**합니다.
   
    c. **hello 사용자에 대 한 hello 필드는 테이블 중...**  텍스트 상자에 **user_name**합니다.
   
    d. **Save**를 클릭합니다.

10. Hello 왼쪽에 hello 탐색 창에서 클릭 **x509 인증서**합니다.
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Single Sign-On 구성")

11. Hello에 **X.509 인증서** 대화 상자를 클릭 하 여 **새로**합니다.
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Single Sign-On 구성")

12. Hello에 **X.509 인증서** 대화 상자에서 hello 다음 단계를 수행 합니다.
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")
    
     a. **새로 만들기**를 클릭합니다.
    
     b. Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **TestSAML2.0**).
    
     c. **활성**을 선택합니다.
    
     d. **형식**으로 **PEM**을 선택합니다.
    
     e. **형식**으로 **저장소 인증서 신뢰**를 선택합니다.
    
     f. 메모장에 복사 hello 내용을 클립보드의 내용에 Base64 인코딩된 인증서를 열고 toohello 붙여 **PEM Certificate** 텍스트 상자에 붙여넣습니다.
    
     g. **업데이트**를 클릭합니다.

13. Hello 왼쪽에 hello 탐색 창에서 클릭 **Id 공급자**합니다.
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Single Sign-On 구성")

14. Hello에 **Id 공급자** 대화 상자를 클릭 하 여 **새로**:
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Single Sign-On 구성")

15. Hello에 **Id 공급자** 대화 상자를 클릭 하 여 **SAML2 업데이트 1?**:
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Single Sign-On 구성")

16. Hello SAML2 업데이트 1 속성 대화 상자에서 hello 다음 단계를 수행 합니다.
    
     ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Single Sign-On 구성")

    a. hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **SAML 2.0**).

    b. Hello에 **사용자 필드** 텍스트 상자에 **전자 메일** 또는 **user_name**, 사용 되는 필드에 따라 toouniquely ServiceNow 배포에서 사용자를 식별 합니다. 

    > [!NOTE] 
    > Azure AD 구성 tooemit 어느 hello Azure AD 사용자 ID (사용자 계정 이름) 수 또는 toohello 이동 하 여 hello SAML 토큰의 고유 식별자를 hello으로 전자 메일 주소를 hello **ServiceNow > 특성 > Single Sign On** 의 섹션 Azure 클래식 포털 및 매핑 원하는 hello 필드 toohello hello **nameidentifier** 특성입니다. hello 선택한 특성에 대 한 Azure AD (예: 사용자 계정 이름)에 저장 하는 hello 값에는 입력 한 hello 필드 (예: user_name)에 대 한 ServiceNow에 저장 된 hello 값과 일치 해야 합니다

    c. Azure AD hello 클래식 포털에서 복사 hello **Id 공급자 ID** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 URL** 텍스트 상자에 붙여넣습니다.

    d. Azure AD hello 클래식 포털에서 복사 hello **인증 요청 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.

    e. Azure AD hello 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 SingleLogoutRequest** 텍스트 상자에 붙여넣습니다.

    f. Hello에 **ServiceNow 홈 페이지** 텍스트 상자에 ServiceNow 인스턴스 홈 페이지의 hello URL 입력 합니다.

    > [!NOTE] 
    > hello ServiceNow 인스턴스 홈 페이지는 연결의 프로그램 **ServieNow 테 넌 트 URL** 및 **/navpage.do** (예::`https://fabrikam.service-now.com/navpage.do`).

    g. Hello에 **엔터티 ID / 발급자** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.

    h. Hello에 **Audience URL** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다. 

    i. Hello에 **hello IDP의 SingleLogoutRequest에 대 한 프로토콜 바인딩** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:bindings:HTTP-리디렉션**합니다.

    j. Hello NameID 정책 텍스트 상자에에서 입력 **urn: oasis: 이름: tc: SAML:1.1:nameid-형식: 지정 되지 않은**합니다.

    k. **AuthnContextClass 만들기**의 선택을 취소합니다.

    l. Hello에 **AuthnContextClassRef 메서드**, 형식 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`합니다. 클라우드 전용 조직인 경우에만 필요합니다. 인증으로 온-프레미스 ADFS 또는 MFA를 사용하는 경우 이 값을 구성하면 안 됩니다. 

    m. **시계 기울이기** 텍스트 상자에 **60**을 입력합니다.

    n. **Single Sign On 스크립트**로 **MultiSSO_SAML2_Update1**를 선택합니다.

    o. 으로 **x509 인증서**선택, hello 이전 단계에서 만든 hello 인증서입니다.

    p. **제출**을 클릭합니다. 

1. Azure AD hello 클래식 포털에서 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다. 
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")

2. Hello에 **Single sign on 확인** 페이지 **완료**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>ServiceNow Express에 대한 Azure AD Single Sign-On 구성
1. Hello에 Azure AD hello 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자 .
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")

2. Hello에 **어떻게 tooServiceNow에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")

3. Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")
   
    a. hello에 **ServiceNow 로그온 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.
   
    b. Hello에 **발급자 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자 `https://<instance-name>.service-now.com`합니다.
   
    c. **다음**을 누릅니다

4. 클릭 **hello 응용 프로그램에 single sign-on에 대 한 수동 구성**, 클릭 **다음** 전체 hello 단계를 수행 하 고 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")

5. Hello에 **ServiceNow에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 하 고 클릭 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")

6. 로그온 tooyour 관리자 권한으로 ServiceNow Express 응용 프로그램입니다.

7. Hello 왼쪽에 hello 탐색 창에서 클릭 **Single Sign On**합니다.  
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "앱 URL 구성")

8. Hello에 **Single Sign On** 대화 상자에서 hello 구성 아이콘 hello 위 오른쪽과 설정 hello 다음 속성을 클릭 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "앱 URL 구성")
   
    a. 설정/해제 **여러 공급자 SSO 설정** toohello 오른쪽입니다.
   
    b. 설정/해제 **여러 공급자 SSO 통합 hello에 대 한 로깅을 사용 하도록 설정 디버그** toohello 오른쪽입니다.
   
    c. **hello 사용자에 대 한 hello 필드는 테이블 중...**  텍스트 상자에 **user_name**합니다.
9. Hello에 **Single Sign On** 대화 상자를 클릭 하 여 **새 인증서 추가**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Single Sign-On 구성")
10. Hello에 **X.509 인증서** 대화 상자에서 hello 다음 단계를 수행 합니다.
    
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")
    
    a. Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **TestSAML2.0**).
    
    b. **활성**을 선택합니다.
    
    c. **형식**으로 **PEM**을 선택합니다.
    
    d. **형식**으로 **저장소 인증서 신뢰**를 선택합니다.
    
    e. 다운로드한 인증서에서 Base64로 인코딩된 파일을 만듭니다.
    
    > [!NOTE]
    > 자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.
    > 
    > 
    
    f. 메모장에 복사 hello 내용을 클립보드의 내용에 Base64 인코딩된 인증서를 열고 toohello 붙여 **PEM Certificate** 텍스트 상자에 붙여넣습니다.
    
    g. **업데이트**를 클릭합니다.
11. Hello에 **Single Sign On** 대화 상자를 클릭 하 여 **새 IdP 추가**합니다.
    
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Single Sign-On 구성")
12. Hello에 **새 Id 공급자 추가** 대화 아래 **Id 공급자 구성**, hello 다음 단계를 수행 합니다.
    
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Single Sign-On 구성")

    a. hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **SAML 2.0**).

    b. Azure AD hello 클래식 포털에서 복사 hello **Id 공급자 ID** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 URL** 텍스트 상자에 붙여넣습니다.

    c. Azure AD hello 클래식 포털에서 복사 hello **인증 요청 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.

    d. Azure AD hello 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 SingleLogoutRequest** 텍스트 상자에 붙여넣습니다.

    e. 으로 **Id 공급자 인증서**선택, hello 이전 단계에서 만든 hello 인증서입니다.


1. 클릭 **고급 설정**, 아래에서 **추가 Id 공급자 속성**, hello 다음 단계를 수행 합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Single Sign-On 구성")
   
    a. Hello에 **hello IDP의 SingleLogoutRequest에 대 한 프로토콜 바인딩** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:bindings:HTTP-리디렉션**합니다.
   
    b. Hello에 **NameID 정책** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-형식: 지정 되지 않은**합니다.    
   
    c. Hello에 **AuthnContextClassRef 메서드**, 형식 **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**합니다.
   
    d. **AuthnContextClass 만들기**의 선택을 취소합니다.

2. 아래 **추가 서비스 공급자 속성**, hello 다음 단계를 수행 합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Single Sign-On 구성")
   
    a. Hello에 **ServiceNow 홈 페이지** 텍스트 상자에 ServiceNow 인스턴스 홈 페이지의 hello URL 입력 합니다.
   
    > [!NOTE]
    > hello ServiceNow 인스턴스 홈 페이지는 연결의 프로그램 **ServieNow 테 넌 트 URL** 및 **/navpage.do** (예:: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. Hello에 **엔터티 ID / 발급자** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.
   
    c. Hello에 **Audience URI** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다. 
   
    d. **시계 기울이기** 텍스트 상자에 **60**을 입력합니다.
   
    e. Hello에 **사용자 필드** 텍스트 상자에 **전자 메일** 또는 **user_name**, 사용 되는 필드에 따라 toouniquely ServiceNow 배포에서 사용자를 식별 합니다.
   
    > [!NOTE]
    > Azure AD 구성 tooemit 어느 hello Azure AD 사용자 ID (사용자 계정 이름) 수 또는 toohello 이동 하 여 hello SAML 토큰의 고유 식별자를 hello으로 전자 메일 주소를 hello **ServiceNow > 특성 > Single Sign On** 의 섹션 Azure 클래식 포털 및 매핑 원하는 hello 필드 toohello hello **nameidentifier** 특성입니다. hello 선택한 특성에 대 한 Azure AD (예: 사용자 계정 이름)에 저장 하는 hello 값에는 입력 한 hello 필드 (예: user_name)에 대 한 ServiceNow에 저장 된 hello 값과 일치 해야 합니다
    > 
    > 
   
    f. **Save**를 클릭합니다. 

3. Azure AD hello 클래식 포털에서 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다. 
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")

4. Hello에 **Single sign on 확인** 페이지 **완료**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")

## <a name="configuring-user-provisioning"></a>사용자 프로비전 구성
이 섹션의 hello 목적은 toooutline 어떻게 tooServiceNow 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:
1. Hello에 hello 관리 Azure 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **사용자 프로비저닝을 구성할**합니다. 
   
    ![사용자 프로비전](./media/active-directory-saas-servicenow-tutorial/IC769498.png "사용자 프로비전")

2. Hello에 **프로그램 ServiceNow 자격 증명 tooenable 자동 사용자 프로비저닝 입력** 페이지 hello 다음 구성 설정을 제공 합니다.
   
     a. Hello에 **ServiceNow 인스턴스 이름을** 텍스트 형식 hello ServiceNow 인스턴스 이름입니다.
   
     b. Hello에 **ServiceNow 관리자 사용자 이름** 텍스트 형식 hello 이름 hello ServiceNow 관리자 계정입니다.
   
     c. Hello에 **ServiceNow 관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.
   
     d. 클릭 **유효성을 검사** tooverify 구성 합니다.
   
     e. Hello 클릭 **다음** 단추 tooopen hello **다음 단계** 페이지.
   
     f. 모든 사용자가 toothis 응용 프로그램 tooprovision 하려는 경우 선택 "**자동으로 hello 디렉터리 toothis 응용 프로그램의 모든 사용자 계정을 프로 비전**"입니다. 
   
    ![다음 단계](./media/active-directory-saas-servicenow-tutorial/IC698804.png "다음 단계")
   
     g. Hello에 **다음 단계** 페이지 **완료** toosave 구성 합니다.

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.

![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. 사용자 유형에서 조직의 새 사용자를 선택합니다.
   
    b. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.
   
    c. **다음**을 누릅니다.

6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. Hello에 **이름** 텍스트 상자에 **Britta**합니다.  
   
   b. Hello에 **성** 텍스트 상자에, **Simon**합니다.
   
   c. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.
   
   d. Hello에 **역할** 목록에서 **사용자**합니다.
   
   e. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Hello hello 값 적어 **새 암호**합니다.
   
    b. **완료**를 클릭합니다.   

### <a name="creating-a-servicenow-test-user"></a>ServiceNow 테스트 사용자 만들기
이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다. 이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다. ServiceNow 또는 ServiceNow Express에 있는 사용자 계정을 하는 tooadd 방법을 모르는 경우 ServiceNow 지원 팀에 문의 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.
이 섹션에서는 액세스 tooServiceNow 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooServiceNow hello 다음 단계를 수행 합니다.**

1. Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **ServiceNow**합니다.
   
    ![Single Sign-on 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![사용자 할당][203] 

4. Hello 모든 사용자가 목록에서 선택 **Britta Simon**합니다.

5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.

Hello 액세스 패널에서에서 hello ServiceNow 타일을 클릭할 때 자동으로 로그온 tooyour ServiceNow 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
