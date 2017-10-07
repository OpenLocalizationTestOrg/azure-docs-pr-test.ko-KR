---
title: "자습서: SAP Business Object Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 SAP 비즈니스 개체 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a>자습서: SAP Business Object Cloud와 Azure Active Directory 통합

Toointegrate SAP 방법을 배우게이 자습서에서는 Azure Active Directory (Azure AD)와 함께 비즈니스 개체 클라우드입니다.

Azure AD와 SAP 비즈니스 개체 클라우드 통합 시 이점은 다음과 같습니다. hello를 발생할 수 있습니다.

- Azure AD에서 액세스 tooSAP 비즈니스 개체 클라우드를가지고 있는 사람을 제어할 수 있습니다.
- Single sign on 및 사용자의 Azure AD 계정을 사용 하 여 프로그램 사용자 tooSAP 비즈니스 개체 클라우드에에서 자동으로 서명할 수 있습니다.
- 프로그램을 하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.

참조로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건

Azure AD와 통합 된 SAP 비즈니스 개체 클라우드를 tooset, 다음 항목 hello가 필요 합니다.

- Azure AD 구독
- Single Sign-On이 설정된 SAP Business Object Cloud

> [!NOTE]
> 이 자습서에서는 hello 단계를 테스트 하는 경우는 프로덕션 환경에서 테스트할 하지 있습니다 하는 것이 좋습니다.

이 자습서에서는 hello 단계를 테스트 하기 위한 권장 사항:

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 SAP 비즈니스 개체 클라우드를 추가 합니다.
2. Azure AD Single Sign-On 설정 및 테스트

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a>Hello 갤러리에서 SAP 비즈니스 개체 클라우드를 추가 합니다.
hello와 hello 갤러리에서 SAP 비즈니스 개체 클라우드 Azure AD와의 통합을 tooset SAP 비즈니스 개체 클라우드 tooyour 목록은 관리 되는 SaaS 앱을 추가 합니다.

hello 갤러리에서 SAP 비즈니스 개체 클라우드 tooadd:

1. Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 메뉴에서 선택 **Azure Active Directory**합니다. 

    ![hello Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![hello 엔터프라이즈 응용 프로그램 페이지][2]
    
3. 새 응용 프로그램을 tooadd 선택 **새 응용 프로그램**합니다.

    ![hello 새 응용 프로그램 단추][3]

4. Hello 검색 상자에 입력 **SAP 비즈니스 개체 클라우드**합니다.

    ![hello 검색 상자](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. Hello 결과 패널에서 선택 **SAP 비즈니스 개체 클라우드**를 선택한 후 **추가**합니다.

    ![Hello 결과 목록에서 SAP 비즈니스 개체 클라우드](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 설정 및 테스트

이 섹션에서는 *Britta Simon*이라는 테스트 사용자를 기반으로 SAP Business Object Cloud에서 Azure AD Single Sign-On을 설정하고 테스트합니다.

Single sign on toowork에 대 한 Azure AD에는 SAP 비즈니스 개체 클라우드에서 tooknow hello Azure AD에 관련 사용자가 있어야 합니다. Azure AD 사용자 및 SAP 비즈니스 개체 클라우드에서 hello 관련된 사용자 간 링크 관계를 설정 해야 합니다.

tooestablish hello에 대 한 SAP 비즈니스 개체 클라우드에서 관계 링크 **Username**, hello hello 값을 할당 **사용자 이름** Azure AD에서 합니다.

tooconfigure 및 SAP 비즈니스 개체 클라우드 작업을 수행 하는 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:

1. [Azure AD Single Sign-On 설정](#set-up-azure-ad-single-sign-on). 이 기능은 사용자 toouse를 설정합니다.
2. [Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user). 테스트 Azure AD single sign on hello 사용자 Britta Simon와 합니다.
3. [SAP Business Object Cloud 테스트 사용자 만들기](#create-an-sap-business-object-cloud-test-user) 연결 된 toohello hello 사용자의 Azure AD 표현 되는 SAP 비즈니스 개체 클라우드에서 Britta Simon의 해당 하는 도구를 만듭니다.
4. [Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)합니다. Azure AD에서 single sign-on Britta Simon toouse를 설정합니다.
5. [Single Sign-On 테스트](#test-single-sign-on). 해당 hello 구성이 작동을 확인 합니다.

### <a name="set-up-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 설정

이 섹션에서는 켜면 Azure AD single sign-on hello Azure 포털의. 그런 다음 SAP Business Object Cloud 응용 프로그램에서 Single Sign-On을 설정합니다.

Azure AD single sign-on을 SAP 비즈니스 개체 클라우드와 tooset:

1. Hello hello에 Azure 포털에서에서 **SAP 비즈니스 개체 클라우드** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.

    ![Single Sign-On 선택][4]

2. Hello에 **Single sign on** 페이지에 대 한 **모드**선택, **SAML 기반 로그온**합니다.
 
    ![SAML 기반 로그온 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. 아래 **SAP 비즈니스 개체 클라우드 도메인 및 Url**완료, 다음 단계 hello:

    1. Hello에 **로그온 URL** 상자에 URL hello 패턴을 입력 합니다. 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. Hello에 **식별자** 상자에 URL hello 패턴을 입력 합니다.
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud 도메인 및 URL 페이지 URL](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > 이러한 Url hello 값 데모 목적 으로만 사용 됩니다. 실제 hello 사용 하 여 업데이트 hello 값 로그온 URL과 식별자 URL입니다. tooget hello 로그온 URL, 연락처 hello [SAP 비즈니스 개체 클라우드 클라이언트 지원 팀](https://www.sap.com/product/analytics/cloud-analytics.support.html)합니다. Hello 관리 콘솔에서 hello SAP 비즈니스 개체 클라우드 메타 데이터를 다운로드 하 여 hello 식별자 URL을 가져올 수 있습니다. Hello 자습서의 뒷부분에서 설명 합니다. 

4. **SAML 서명 인증서** 아래에서 **메타데이터 XML**을 선택합니다. 그런 다음 hello 메타 데이터 파일을 컴퓨터에 저장 합니다.

    ![메타데이터 XML 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. **저장**을 선택합니다.

    ![저장 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. 다른 웹 브라우저 창에서 관리자 권한으로 tooyour SAP 비즈니스 개체 클라우드 회사 사이트에 로그인 합니다.

7. **메뉴** > **시스템** > **관리**를 선택합니다.
    
    ![메뉴, 시스템 및 관리 선택](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. Hello에 **보안** 탭, 선택 hello **편집** (펜) 아이콘입니다.
    
    ![Hello 보안 탭에서 선택 hello 편집 아이콘](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. **인증 방법**으로 **SAML SSO(Single Sign-On)**를 선택합니다.

    ![SAML Single Sign-on hello 인증 방법 선택](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. toodownload hello 서비스 공급자 메타 데이터 (1 단계) 선택 **다운로드**합니다. Hello 메타 데이터 파일에서 찾아서 복사할 hello **entityID** 값입니다. Hello Azure에서에서 포털에서 **SAP 비즈니스 개체 클라우드 도메인 및 Url**, hello에 hello 값을 붙여 **식별자** 상자입니다.

    ![복사 및 붙여넣기 hello entityID 값](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. tooupload hello 서비스 공급자 (2 단계) 파일의 메타 데이터 hello에서 다운로드 한 hello Azure 포털에서 **업로드 Id 공급자 메타 데이터**선택, **업로드**합니다.  

    ![ID 공급자 메타데이터 업로드 아래에서 업로드 선택](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. Hello에 **사용자 특성** 구현을 위해 toouse 않겠다고 선택 hello 사용자 특성 (3 단계)를 나열 합니다. 이 사용자 특성 toohello id 공급자를 매핑합니다. tooenter hello 사용자 페이지를 사용 하 여 hello에 사용자 지정 특성 **사용자 지정 SAML 매핑** 옵션입니다. 선택할 수 있습니다 또는 **전자 메일** 또는 **사용자 ID** hello 사용자 특성입니다. 예제에서는 선택한 **전자 메일** hello로 hello 사용자 식별자 클레임을 매핑하면 때문에 **userprincipalname** hello에 대 한 특성 **사용자 특성** hello의 섹션 Azure 포털입니다. 모든 성공적인 SAML 응답에서 SAP 비즈니스 개체 클라우드 응용 프로그램 toohello 전송 되는 고유한 사용자 전자 메일을 제공 합니다.

    ![사용자 특성 선택](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. hello에 hello id 공급자 (4 단계)와 tooverify hello 계정 **로그인 자격 증명 (전자 메일)** 상자 hello 사용자의 전자 메일 주소를 입력 합니다. 그런 다음 **계정 확인**을 선택합니다. hello 로그인 자격 증명 toohello 사용자 계정으로 추가 됩니다.

    ![전자 메일을 입력하고 계정 확인을 선택합니다.](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. 선택 hello **저장** 아이콘입니다.

    ![저장 아이콘](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> Hello에이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)응용 프로그램을 설정 하는 반면,! 선택 하 여 hello 앱을 추가한 후 **Active Directory** > **엔터프라이즈 응용 프로그램**선택, hello **Single Sign On** 탭 합니다. Hello에 포함 된 hello 설명서에 액세스할 수 있습니다 **구성** 섹션 hello hello 페이지 맨 아래에 있습니다. 자세한 내용은 [Azure AD 포함 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)를 참조하세요.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션에서는 hello Azure 포털에서에서 Britta Simon 이라는 테스트 사용자를 만듭니다.

Azure AD에서 테스트 사용자 toocreate:

1. Hello hello 왼쪽된 메뉴에 Azure 포털에서에서 선택 **Azure Active Directory**합니다.

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. 사용자 선택 toodisplay hello 목록 **사용자 및 그룹**, 선택한 후 **모든 사용자에 게**합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. tooopen hello **사용자** 대화 상자에서 **추가**합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. Hello에 **사용자** 대화 상자에서 다음 단계 완료 hello:
 
    1. Hello에 **이름** 상자에 입력 **BrittaSimon**합니다.

    2. Hello에 **사용자 이름** 상자 hello 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.

    3. 선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.

    4. **만들기**를 선택합니다.

        ![hello 사용자 대화 상자](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD 사용자 만들기][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a>SAP Business Object Cloud 테스트 사용자 만들기

TooSAP 비즈니스 개체 클라우드 로그인 하기 전에 azure AD 사용자를 SAP 비즈니스 개체 클라우드에서 프로 비전 해야 합니다. SAP Business Object Cloud에서 프로비전은 수동 작업입니다.

tooprovision 사용자 계정:

1. 관리자 권한으로 SAP 비즈니스 개체 클라우드 회사 사이트 tooyour에 로그인 합니다.

2. **메뉴** > **보안** > **사용자**를 선택합니다.

    ![직원 추가](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. Hello에 **사용자** tooadd 새, 사용자 세부 정보 페이지 선택  **+** 합니다. 

    ![사용자 추가 페이지](./media/active-directory-saas-sapboc-tutorial/user4.png)

    그런 다음 단계를 수행 하는 hello를 완료 합니다.

    1. Hello에 **사용자 ID** 상자 같은 hello 사용자의 hello 사용자 ID를 입력 합니다 **Britta**합니다.

    2. Hello에 **이름** 상자 같은 hello hello 사용자 이름을 입력 합니다 **Britta**합니다.

    3. Hello에 **성** 상자을 같은 hello hello 사용자의 성을 입력 **Simon**합니다.

    4. Hello에 **표시 이름** 상자 같은 hello hello 사용자의 전체 이름을 입력 합니다 **Britta Simon**합니다.

    5. Hello에 **전자 메일** 상자 같은 hello 사용자의 hello 전자 메일 주소를 입력 합니다  **brittasimon@contoso.com** 합니다.

    6. Hello에 **역할 선택** 페이지 hello hello 사용자에 대 한 적절 한 역할을 선택 하 고 다음 선택 **확인**합니다.

      ![역할 선택](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. 선택 hello **저장** 아이콘입니다.  


### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.

이 섹션에서는 hello 사용자 계정 액세스 tooSAP 비즈니스 개체 클라우드를 부여 하 여 toouse Azure AD에서 single sign-on hello 사용자 Britta Simon를 허용 합니다.

비즈니스 개체 클라우드 Britta Simon tooSAP tooassign:

1. Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오. **엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.

    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SAP 비즈니스 개체 클라우드**합니다.

    ![Single Sign-on 구성](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. Hello 왼쪽된 메뉴에서 선택 **사용자 및 그룹**합니다.

    ![사용자 및 그룹 선택][202] 

4. **추가**를 선택합니다. 그런 다음 hello **할당 추가** 페이지에서 **사용자 및 그룹**합니다.

    ![hello 할당 추가 페이지][203]

5. Hello에 **사용자 및 그룹** 페이지의 사용자를 hello 목록 **Britta Simon**합니다.

6. Hello에 **사용자 및 그룹** 페이지에서 **선택**합니다.

7. Hello에 **할당 추가** 페이지에서 **할당**합니다.

![Hello 사용자 역할 할당][200] 
    
### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.

Hello 액세스 패널에서 hello SAP 비즈니스 개체 클라우드 타일을 선택 하면 해야 자동으로 로그인 될 tooyour SAP 비즈니스 개체 클라우드 응용 프로그램입니다.

Hello 액세스 패널에 대 한 자세한 내용은 참조 [toohello 액세스 패널 소개](active-directory-saas-access-panel-introduction.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

