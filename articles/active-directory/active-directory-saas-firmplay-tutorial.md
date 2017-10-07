---
title: "자습서: FirmPlay - Employee Advocacy for Recruiting과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FirmPlay-채용에 대 한 직원 대표성 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>자습서: FirmPlay - Employee Advocacy for Recruiting과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate FirmPlay-Azure Active Directory (Azure AD)와 채용에 대 한 직원 지원 합니다.

다음 이점을 hello로 제공 FirmPlay-Azure AD와 채용에 대 한 직원 대표성을 통합:

- 액세스 tooFirmPlay-채용에 대 한 직원 대표성을 지닌 Azure AD에서 제어할 수 있습니다.
- Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooFirmPlay-채용 (Single Sign-on)에 대 한 직원 대표성을 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure FirmPlay-채용에 대 한 직원 대표성와 Azure AD 통합 합니다.

- Azure AD 구독
- FirmPlay - Employee Advocacy for Recruiting Single Sign-On이 설정된 구독


> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.


이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.


## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 채용에 대 한 직원 대표성 FirmPlay-추가
2. Azure AD Single Sign-on 구성 및 테스트


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>Hello 갤러리에서 채용에 대 한 직원 대표성 FirmPlay-추가
FirmPlay-Azure AD로 채용에 대 한 직원 대표성 tooconfigure hello 통합 tooadd FirmPlay-관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 채용에 대 한 직원 지원 해야합니다.

**tooadd FirmPlay-hello 갤러리, 채용에 대 한 직원 대표성 hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **FirmPlay-채용에 대 한 직원 대표성**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. Hello 결과 패널에서 선택 **FirmPlay-채용에 대 한 직원 대표성**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FirmPlay - Employee Advocacy for Recruiting에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow FirmPlay-채용에 대 한 직원 대표성에에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 FirmPlay-채용에 대 한 직원 대표성에에서 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** FirmPlay-채용에 대 한 직원 대표성에에서 합니다.

tooconfigure 및 FirmPlay-채용에 대 한 직원 대표성을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[FirmPlay-채용 테스트 사용자에 대 한 직원 대표성을 만드는](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave Britta Simon FirmPlay에 해당 하는 도구: 즉 채용에 대 한 직원 대표성 그녀의 Azure AD toohello 표현을 연결 합니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 FirmPlay-채용 응용 프로그램에 대 한 직원 대표성에서에서 single sign on 구성 합니다.

**FirmPlay-채용에 대 한 직원 대표성와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **FirmPlay-채용에 대 한 직원 대표성** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. Hello에 **FirmPlay-채용 도메인 및 Url에 대 한 직원 대표성** 섹션 hello **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<your-subdomain>.firmplay.com/`

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Hello 진정한 가치 아닌지 note 하십시오. 이 값을 실제 hello로 로그온 URL tooupdate를 해야 합니다. 연락처 [FirmPlay-채용 지원 팀에 대 한 직원 대표성](mailto:engineering@firmplay.com) tooget이이 값입니다. 

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **새 인증서 만들기**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. Hello에 **새 인증서 만들기** 대화 상자에서 hello 달력 아이콘을 클릭 하 고 선택 된 **만료 날짜**합니다. 그런 후 **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. Hello에 **SAML 서명 인증서** 섹션에서 **새 인증서를 활성화할** 클릭 **저장** 단추입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. Hello 팝업에서 **롤오버 인증서** 창 클릭 **확인**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (base64)** hello 인증서 파일을 컴퓨터에 저장 합니다. 

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. Hello에 **FirmPlay-채용 구성에 대 한 직원 대표성** 섹션에서 클릭 **구성 FirmPlay-채용에 대 한 직원 대표성** tooopen **sign-on구성**대화 상자.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. 응용 프로그램에 tooget SSO 구성에 문의 하시기 바랍니다 [FirmPlay-채용 지원 팀에 대 한 직원 대표성](mailto:engineering@firmplay.com) hello 다음을 제공 합니다. 

    다운로드 한 • hello **인증서 파일**

    • hello **SAML Single Sign-on 서비스 URL**

    • hello **SAML 엔터티 ID**

    • hello **Sign-Out URL**
  

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>FirmPlay - Employee Advocacy for Recruiting 테스트 사용자 만들기

이 섹션에서는 FirmPlay - Employee Advocacy for Recruiting에서 Britta Simon이라는 사용자를 만듭니다. 와 협력 하세요 [FirmPlay-채용 지원 팀에 대 한 직원 대표성](mailto:engineering@firmplay.com) hello FirmPlay-채용 플랫폼에 대 한 직원 대표성에에서 tooadd hello 사용자입니다.


### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooFirmPlay-채용에 대 한 직원 대표성을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooFirmPlay-채용에 대 한 직원 대표성 hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **FirmPlay-채용에 대 한 직원 대표성**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    


### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello FirmPlay-hello 액세스 패널에에서 채용 타일에 대 한 직원 대표성을 클릭할 때 자동으로 로그온 tooyour FirmPlay-채용 응용 프로그램에 대 한 직원 대표성을 구해야 합니다.


## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png