---
title: "자습서: vxMaintain과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 vxMaintain 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>자습서: vxMaintain과 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate vxMaintain Azure Active directory (Azure AD).

이 통합은 몇 가지 중요한 이점을 제공합니다. 다음을 수행할 수 있습니다.

- 컨트롤에 있는 Azure AD 액세스 toovxMaintain 합니다.
- Azure AD 계정을 사용 하 여 toovxMaintain single sign-on에서 (SSO)에 대 한 사용자가 tooautomatically 로그인을 사용 합니다.
- 하나의 중앙 위치에 계정 관리: hello Azure 포털입니다.

Azure AD와 SaaS 앱 통합에 대 한 더 toolearn 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure vxMaintain와 Azure AD 통합 합니다.

- Azure AD 구독
- vxMaintain SSO가 설정된 구독

> [!NOTE]
> 이 자습서에서는 hello 단계를 테스트할 때에 프로덕션 환경 사용 하지 않는 것이 좋습니다.

이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 

이 자습서에 간략하게 설명 하는 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

* VxMaintain hello 갤러리 추가
* Azure AD Single Sign-on 구성 및 테스트

## <a name="add-vxmaintain-from-hello-gallery"></a>VxMaintain hello 갤러리 추가
tooconfigure hello와의 통합 vxMaintain Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd vxMaintain 필요합니다.

tooadd vxMaintain hello 갤러리에서 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다. 

    ![hello Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.

    ![hello "엔터프라이즈 응용 프로그램" 창][2]
    
3. 응용 프로그램에 hello tooadd **모든 응용 프로그램** 대화 상자에서 **새 응용 프로그램**합니다.

    !["새 응용 프로그램" hello 단추][3]

4. Hello 검색 상자에 입력 **vxMaintain**합니다.

    ![hello "Single Sign on 모드" 드롭 다운 목록](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Hello 결과 목록에서 선택 **vxMaintain**를 선택한 후 **추가**합니다.

    ![hello vxMaintain 링크](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 vxMaintain을 사용하여 Azure AD SSO를 구성하고 테스트합니다.

SSO toowork에 대 한 Azure AD tooknow hello vxMaintain 대응 toohello Azure AD 사용자는 필요 합니다. 즉, hello Azure AD 사용자 및 hello 해당 vxMaintain 사용자 간의 링크 관계를 설정 해야 합니다.

tooestablish hello 링크 관계를 할당 hello vxMaintain **사용자 이름** hello Azure AD로 값 **Username** 값입니다.

tooconfigure 및 Azure AD SSO vxMaintain, 구성 요소를 다음 전체 hello를 사용 하 여 테스트 합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

이 섹션에서는 hello Azure 포털에서에서 Azure AD SSO를 통해와 hello 다음을 수행 하 여 vxMaintain 응용 프로그램에서 SSO를 구성 합니다.

1. Hello hello에 Azure 포털에서에서 **vxMaintain** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.

    ![명령 "Single sign-on" hello][4]

2. hello에 SSO, tooenable **Single Sign on 모드** 드롭 다운 목록 **SAML 기반 로그온**합니다.
 
    ![hello "SAML 기반 로그온" 명령](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. 아래 **vxMaintain 도메인 및 Url**, 다음 hello지 않습니다.

    ![hello vxMaintain 도메인 및 Url 섹션](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. Hello에 **식별자** 상자 구문 다음 hello에 URL을 입력 합니다.`https://<company name>.verisae.com`

    b. Hello에 **회신 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > hello 이전 값이 실제. 실제 hello 식별자로 업데이트 하 고 회신 URL입니다. tooobtain hello 값, 연락처 hello [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다.
 
4. 아래 **SAML 서명 인증서**선택, **메타 데이터 XML**, hello 메타 데이터 파일 tooyour 컴퓨터를 저장 합니다.

    ![hello "SAML 서명 인증서" 섹션](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. **저장**을 선택합니다.

    ![hello 저장 단추](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO를 다운로드 하는 송신 hello **메타 데이터 XML** toohello 파일 [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다.

> [!TIP]
> Hello 지침 hello에서 앞의 간결한 버전을 읽을 수 hello 앱을 설정할 때 [Azure 포털](https://portal.azure.com)합니다. Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single Sign On** 탭을 클릭 한 다음 액세스 hello hello의 설명서에 포함 된 **구성** 섹션. 
>
>hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [single sign on 엔터프라이즈 앱에 대 한 관리](https://go.microsoft.com/fwlink/?linkid=845985)합니다.
> 

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 hello 다음을 수행 하 여 hello Azure 포털에서에서 Britta Simon 테스트 사용자를 만듭니다.

![Azure AD hello 테스트 사용자][100]

1. Hello에 **Azure 포털**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.

    ![hello "Azure Active Directory" 단추](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay 사용자 목록이 너무 이동**사용자 및 그룹** > **모든 사용자에 게**합니다.
    
    !["모든 사용자" 링크를 hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    hello **모든 사용자에 게** 대화 상자가 열립니다. 

3. tooopen hello **사용자** 대화 상자에서 **추가**합니다.
 
    ![hello 추가 단추](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자에서 다음 hello지 않습니다.
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 상자의 테스트 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    c. 선택 hello **암호 표시** 확인란을 선택한 다음 참고 hello 생성 된 값을 hello에 **암호** 상자입니다.

    d. **만들기**를 선택합니다.
 
### <a name="create-a-vxmaintain-test-user"></a>vxMaintain 테스트 사용자 만들기

이 섹션에서는 vxMaintain에서 테스트 사용자인 Britta Simon을 만듭니다. hello vxMaintain 플랫폼에서 tooadd 사용자가 작업할는 [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다. SSO를 사용 하기 전에 만들고 hello 사용자를 활성화 합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 toovxMaintain 액세스 권한을 부여 하 여 테스트 사용자 Britta Simon toouse Azure SSO를 사용 합니다. 따라서 toodo 다음 hello지 않습니다.

![Hello 표시 이름 목록에서 테스트 사용자][200] 

1. Hello Azure 포털에서에서 **응용 프로그램** 보기, 너무 이동**디렉터리** 보기 > **엔터프라이즈 응용 프로그램** > **모든응용프로그램**.

    !["모든 응용 프로그램" 링크를 hello][201] 

2. Hello에 **응용 프로그램** 목록에서 **vxMaintain**합니다.

    ![hello vxMaintain 링크](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Hello 왼쪽된 창에서 선택 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][202] 

4. 선택 **추가** 선택한 다음 hello **할당 추가** 창 선택 **사용자 및 그룹**합니다.

    ![hello "사용자 및 그룹" 링크][203]

5. Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**, 선택한 후 hello **선택** 단추입니다.

7. Hello에 **할당 추가** 대화 상자에서 **할당**합니다.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.

선택 hello **vxMaintain** hello 액세스 패널에서에서 타일은 자동으로 로그인 하도록 tooyour vxMaintain 응용 프로그램입니다.

액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="next-steps"></a>다음 단계

* [Azure Active Directory와 SaaS 앱 통합에 대한 자습서 목록](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

