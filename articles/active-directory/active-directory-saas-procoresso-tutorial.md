---
title: "자습서: Procore SSO와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Procore SSO 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>자습서: Procore SSO와 Azure Active Directory 통합

이 자습서에 설명 어떻게 toointegrate Procore SSO 및 Azure Active Directory (Azure AD).

다음 이점을 hello로 제공 Procore SSO Azure AD와 통합:

- Azure ad 액세스 tooProcore SSO가 제어할 수 있습니다.
- 프로그램 사용자 tooautomatically get 로그온 tooProcore SSO (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.
- 하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>필수 조건

다음 항목 hello가 필요 tooconfigure Procore SSO와 Azure AD 통합 합니다.

- Azure AD 구독
- Procore SSO Single Sign-On을 사용하도록 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Procore SSO hello 갤러리 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-procore-sso-from-hello-gallery"></a>Procore SSO hello 갤러리 추가
tooconfigure hello와의 통합 Procore SSO Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Procore SSO tooadd가 필요합니다.

**hello 갤러리에서 Procore SSO tooadd hello 다음 단계를 수행 합니다.**

1. Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다. 

    ![Active Directory][1]

2. 너무 이동**엔터프라이즈 응용 프로그램**합니다. 이동 하 여 너무**모든 응용 프로그램**합니다.

    ![응용 프로그램][2]
    
3. 클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.

    ![응용 프로그램][3]

4. Hello 검색 상자에 입력 **Procore SSO**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. Hello 결과 패널에서 선택 **Procore SSO**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Procore SSO에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD는 tooknow Procore SSO에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다. 즉, Azure AD 사용자 및 hello Procore SSO에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Procore SSO에서 합니다.

tooconfigure 및 Procore SSO를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[Procore SSO 테스트 사용자 만들기](#creating-a-procore-sso-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello 그녀는 Procore SSO에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Procore SSO 응용 프로그램에서 single sign on 구성 합니다.

**Azure AD tooconfigure single sign on Procore SSO와 hello 다음 단계를 수행 합니다.**

1. Hello에 hello Azure 관리 포털에서 **Procore SSO** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.

    ![Single Sign-on 구성][4]

2. Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign-on입니다.
 
    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Hello에 **Procore SSO 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. **저장** 단추를 클릭합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Hello에 **Procore SSO 구성** 섹션에서 클릭 **Procore SSO 구성** tooopen **sign on 구성** 창. 복사 hello **SAML Single Sign-on 서비스 URL 및 엔터티 ID가 SAML** hello에서 **빠른 참조 섹션.**

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure single sign on에서 **Procore SSO** 쪽, tooyour procore 회사 사이트에 관리자로 로그인 합니다.

8. Hello 도구 상자 드롭다운에서 아래쪽을 클릭 **Admin** tooopen hello SSO 설정 페이지.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Hello 상자에 붙여넣기 hello 값 설명 아래-

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. Hello에 **Single Sign-on 발급자 URL** 상자을 hello hello Azure 포털에서에서 복사 된 SAML 엔터티 ID를 붙여넣습니다.

    b. Hello에 **SAML 로그온 대상 URL** 상자을 hello hello Azure 포털에서에서 복사 된 SAML Single Sign-on 서비스 URL을 붙여넣습니다.

    c. 이제 hello 열 **메타 데이터 XML** 이름이 hello 태그에서 복사 hello 인증서 및 hello Azure 포털에서 다운로드 한 위에 **X509Certificate**합니다. 붙여넣기 hello hello에 값 복사 **Single Sign On x509 인증서** 상자입니다.

10. **변경 내용 저장**을 클릭합니다.

11. 이러한 설정은 후 toosend hello 필요 **도메인 이름** (예: **contoso.com**) Procore toohello에 로그인 하는 통해 [Procore 지원 팀](https://support.procore.com/) 되도록 하 고 해당 도메인에 대 한 페더레이션된 SSO를 활성화 합니다.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][100]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. 너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.

    b. Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.

    c. 선택 **암호 표시** hello hello 값 기록 **암호**합니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-procore-sso-test-user"></a>Procore SSO 테스트 사용자 만들기

지 단계 toocreate Procore 테스트 사용자 아래 hello를 수행 하십시오.

1. Tooyour procore 회사 사이트에 관리자로 로그인 합니다.  

2. Hello 도구 상자 드롭다운에서 아래쪽을 클릭 **디렉터리** tooopen hello 회사 디렉터리 페이지.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. 클릭 **사람을 추가** tooopen hello 폼 옵션 선택한 입력 옵션-다음을 수행할

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. Hello에 **이름** 텍스트 상자와 같은 형식 사용자의 이름을 **Britta**합니다.

    b. Hello에 **성** 텍스트 상자와 같은 형식 사용자의 성 **Simon**합니다.

    c. Hello에 **전자 메일 주소** textbox 유형 사용자의 전자 메일 주소와 같은  **BrittaSimon@contoso.com** 합니다.

    d. **Permission Template**(권한 템플릿)에 **Apply Permission Template Later**(권한 템플릿 나중에 적용)를 선택합니다.

    e. **만들기**를 클릭합니다.

4. 확인 하 고 새로 추가 된 연락처 hello에 대 한 hello 세부 정보를 업데이트 합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. 클릭 **저장 및 보내기 Invitiation** (초대 메일을 통해 필요한 경우) 또는 **저장** (직접 저장) toocomplete hello 사용자 등록 합니다.
    
    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당합니다.

이 섹션에서는 그녀의 액세스 tooProcore SSO를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.

![사용자 할당][200] 

**tooassign Britta Simon tooProcore SSO, hello 다음 단계를 수행 합니다.**

1. Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **Procore SSO**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.

    ![사용자 할당][202] 

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

5. **사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.

Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요. Hello 액세스 패널에서에서 hello Procore SSO 타일을 클릭할 때 자동으로 로그온 tooyour Procore SSO 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

