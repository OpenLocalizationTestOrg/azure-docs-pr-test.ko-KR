---
title: "자습서: FreshDesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FreshDesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a>자습서: FreshDesk와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate FreshDesk와 Azure Active Directory (Azure AD).

Azure AD와 FreshDesk 통합 이점을 다음 hello로 제공 합니다.

- 액세스 tooFreshDesk을 지닌 Azure AD에서 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooFreshDesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

FreshDesk와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- FreshDesk Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. FreshDesk은 hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-freshdesk-from-hello-gallery"></a>FreshDesk은 hello 갤러리 추가
tooconfigure hello와의 통합 FreshDesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 FreshDesk tooadd가 필요합니다.

**FreshDesk hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 ** [Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **FreshDesk**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. Hello 결과 패널에서 선택 **FreshDesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FreshDesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow FreshDesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자와 FreshDesk에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** FreshDesk에 합니다.

tooconfigure와 FreshDesk와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[FreshDesk 테스트 사용자 만들기](#creating-a-freshdesk-test-user) ** -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 FreshDesk에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 FreshDesk 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on와 FreshDesk를 hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **FreshDesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. Hello에 **FreshDesk 도메인 및 Url** 섹션에서 hello를 입력 하십시오 **로그온 URL** 으로: `https://<tenant-name>.freshdesk.com` 이나 Freshdesk에 제안 된 다른 모든 값입니다.

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 이러한 값은 실제 로그온 URL로 업데이트해야 합니다. 이 값을 얻으려면 [FreshDesk Client 지원 팀](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)에 문의하세요.  

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. Hello에 **FreshDesk 구성** 섹션에서 클릭 **구성 FreshDesk** sign on 구성 tooopen 창. Hello에서 hello SAML Single Sign-on 서비스 URL 및 Sign-Out URL 복사 **빠른 참조** 섹션.

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. 다른 웹 브라우저 창에서 Freshdesk 회사 사이트에 관리자로 로그인합니다.

8. Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.
   
   ![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "관리자")

9. Hello에 **일반 설정** 탭을 클릭 **보안**합니다.
   
   ![보안](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "보안")

10. Hello에 **보안** 섹션를 hello 다음 단계를 수행 합니다.
   
    ![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")
   
    a. **SSO(Single Sign On)**의 경우 **On**을 선택합니다.

    b. **SAML SSO**를 선택합니다.

    c. 형식 hello **SAML Single Sign-on 서비스 URL** hello에 Azure 포털에서 복사한 **SAML 로그인 URL** 텍스트 상자에 붙여넣습니다.

    d. 형식 hello **Sign-Out URL** hello에 Azure 포털에서 복사한 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.

    e. 복사 hello **지문** 값 Azure 포털에서 다운로드 한 hello 인증서에서 복사한 hello에 **보안 인증서 지문** 텍스트 상자에 붙여넣습니다.  
 
    >[!TIP]
    >자세한 내용은 참조 하십시오. [어떻게 tooretrieve 인증서의 지문 값](http://youtu.be/YKQF266SAxI)합니다. 
    
    f. **Save**를 클릭합니다.


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-freshdesk-test-user"></a>FreshDesk 테스트 사용자 만들기

Tooenable Azure AD 사용자가 toolog FreshDesk에 주문 하 고에 FreshDesk에 이들 프로 비전 해야 합니다.  
Hello FreshDesk의 경우에서 프로 비전은 수동 작업입니다.

**사용자 계정 수행 tooprovision hello 다음 단계:**

1. Tooyour 로그인 **Freshdesk** 테 넌 트입니다.
2. Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.
   
   ![관리자](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "관리자")

3. Hello에 **일반 설정** 탭을 클릭 **에이전트**합니다.
   
   ![에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "에이전트")

4. **새 에이전트**를 클릭합니다.
   
    ![새 에이전트](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "새 에이전트")

5. Hello 에이전트 정보 대화 상자에서 hello 다음 단계를 수행 합니다.
   
   ![에이전트 정보](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "에이전트 정보")
   
   a. Hello에 **전체 이름을** tooprovision hello Azure AD 계정 형식 hello 이름 텍스트 상자입니다.

   b. Hello에 **전자 메일** 텍스트 형식 hello Azure AD 전자 메일 주소 hello Azure AD 계정 tooprovision 합니다.

   c. Hello에 **제목** textbox tooprovision hello Azure AD 계정 hello 제목을 입력 합니다.

   d. **에이전트 역할**을 선택한 다음 **할당**을 클릭합니다.
       
   e. **Save**를 클릭합니다.     
   
    >[!NOTE]
    >hello Azure AD 계정 보유자 활성화 되기 전에 tooconfirm hello 계정 연결을 포함 하는 전자 메일을 받게 됩니다. 
    > 
    
    >[!NOTE]
    >다른 Freshdesk 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Freshdesk에서 제공 된 Api입니다. tooFreshDesk 합니다.

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 액세스 tooBox 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooFreshDesk hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **FreshDesk**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Hello 액세스 패널에서에서 hello FreshDesk 타일을 클릭할 때 로그인 페이지 tooget 로그온 tooyour FreshDesk 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

