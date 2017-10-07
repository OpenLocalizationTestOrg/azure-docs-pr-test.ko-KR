---
title: "자습서: LinkedIn Elevate와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 LinkedIn 상승 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>자습서: LinkedIn Elevate와 Azure Active Directory 통합

배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate LinkedIn 상승 하는 방법입니다.

LinkedIn 상승 Azure AD와 통합 이점을 다음 hello로 제공 합니다.

- 액세스 권한 상승 tooLinkedIn을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooLinkedIn 권한 상승 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

LinkedIn 상승와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- LinkedIn Elevate Single Sign-On을 사용하도록 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. LinkedIn 상승 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>LinkedIn 상승 hello 갤러리 추가
tooconfigure hello와의 통합 LinkedIn 상승 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd LinkedIn 승격 해야합니다.

**LinkedIn hello 갤러리에서 권한 상승 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **LinkedIn 상승**합니다. 결과 패널에서 클릭 **LinkedIn 상승** tooadd hello 응용 프로그램입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Elevate에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow LinkedIn 권한 상승에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 권한 상승 LinkedIn에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** LinkedIn 권한 상승에 합니다.

tooconfigure 및 LinkedIn 권한 상승으로 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[LinkedIn 상승 테스트 사용자 만들기](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 사용 하도록 설정 및 LinkedIn 상승 응용 프로그램에서 single sign on 구성 합니다.

**tooconfigure Azure AD single sign on LinkedIn 권한 상승으로 hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **LinkedIn 상승** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. 다른 웹 브라우저 창에서 로그온 tooyour LinkedIn 상승 테 넌 트 관리자 권한으로 합니다.

4. **계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다. 또한 선택 **권한 상승-AAD 테스트 상승** hello 드롭다운 목록에서 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. 클릭 **또는 여기를 클릭 tooload 및 복사의에서 개별 필드 hello 양식** 복사 **엔터티 Id** 및 **Url 액세스 ACS (Assertion Consumer)**

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. Azure 포털에서 **LinkedIn 상승 도메인 및 Url**, hello tooconfigure SSO 하려는 경우 다음 단계를 수행에 **IdP 시작** 모드

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. Hello에 **식별자** textbox hello 입력 **엔터티 ID** LinkedIn 포털에서 복사 

    b. Hello에 **회신 URL** textbox hello 입력 **액세스 ACS (Assertion Consumer) Url** LinkedIn 포털에서 복사

7. SSO tooconfigure 하려는 경우에 **SP 시작**다음 hello 구성 섹션에서 설정 옵션을 표시 하는 고급 URL을 클릭 패턴 hello로 hello 로그온 URL 구성:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. LinkedIn 상승 응용 프로그램 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다. 다음 스크린 샷 hello이에 대 한 예가 나와 있습니다. 기본값을 hello **사용자 식별자** 은 **user.userprincipalname** hello 사용자의 전자 메일 주소에 매핑이 toobe 예상 LinkedIn 상승 하지만 합니다. 사용할 수 있는 **user.mail** hello 목록에서 특성 또는 사용자 조직 구성에 따라 hello 적절 한 특성 값을 사용 합니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. **사용자 특성** 섹션에서 클릭 **보기 및 다른 모든 사용자 특성 편집** hello 특성을 설정 합니다. 명명 된 다른 클레임 tooadd 필요한 **부서** hello 값이 너무 매핑된 toobe**user.department**합니다.

    | 특성 이름 | 특성 값 |
    | --- | --- |    
    | department| user.department |

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. 추가 특성 tooopen hello 특성 세부 정보 페이지를 클릭 아래-표시 된 것 처럼 hello 부서 특성 추가

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. 클릭 **확인** toosave hello 특성입니다.

      c. Hello 특성의 hello 이름 변경 **emailaddress** 너무**전자 메일**합니다.


10. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. **Save**를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. 너무 이동**LinkedIn 관리 설정** 섹션. 방금 다운로드 한 hello Azure 포털에서에서 hello 업로드 XML 파일 옵션을 클릭 하 여 hello XML 파일을 업로드 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. 클릭 **에** tooenable SSO 합니다. SSO 상태에서 변경 됩니다. **연결 되어 있지 않은** 너무**연결 됨**

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다. 

### <a name="creating-a-linkedin-elevate-test-user"></a>LinkedIn Elevate 테스트 사용자 만들기

연결 된 권한 상승 응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다. Hello LinkedIn 상승 포털 플립 hello 스위치 hello 관리자 설정 페이지에서 **자동으로 할당 라이선스** tooactive tooenable Just 적시 프로 비전 하 고이 라이선스 toohello 사용자 할당할 수도 있습니다.

   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooLinkedIn 권한 상승 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooLinkedIn 권한 상승, hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **LinkedIn 상승**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello LinkedIn 상승 타일을 클릭할 때 hello Azure 로그온 페이지를 받아야 하며 및에 성공적으로 로그온 한 후 가져와야 LinkedIn 상승 응용 프로그램에 있습니다.

## <a name="additional-resources"></a>추가 리소스

* [자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Elevate 구성](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
