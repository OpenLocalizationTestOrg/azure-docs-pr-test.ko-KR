---
title: "자습서: SilkRoad Life Suite와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 SilkRoad 수명 도구 모음 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>자습서: SilkRoad Life Suite와 Azure Active Directory 통합
이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 SilkRoad 수명 도구 모음. 

다음 이점을 hello로 제공 SilkRoad 수명 Suite Azure AD와 통합: 

* 액세스 tooSilkRoad 수명 도구 모음을 지닌 Azure AD에서 제어할 수 있습니다. 
* Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSilkRoad 수명 Suite single sign on (SSO)를 사용할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.

## <a name="prerequisites"></a>필수 조건
다음 항목 hello가 필요 tooconfigure SilkRoad 수명 도구 모음과 Azure AD 통합 합니다.

* Azure AD 구독
* SilkRoad Life Suite SSO가 설정된 구독

>[!NOTE]
>이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다. 
> 

이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.

* 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.
* Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다. 

## <a name="scenario-description"></a>시나리오 설명
이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD SSO 테스트 환경에서 합니다.

이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.

1. Hello 갤러리에서 SilkRoad 수명 도구 모음 추가 
2. Azure AD SSO 구성 및 테스트

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Hello 갤러리에서 SilkRoad 수명 도구 모음을 추가 합니다.
tooconfigure hello와의 통합 SilkRoad 수명 Suite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SilkRoad 수명 Suite tooadd가 필요합니다.

**hello 갤러리에서 SilkRoad 수명 Suite tooadd hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다. 
   
    ![Active Directory][1]

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램][2]

4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램][3]

5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![응용 프로그램][4]

6. Hello 검색 상자에 입력 **SilkRoad 수명 Suite**합니다.
   
    ![응용 프로그램][5]

7. Hello 결과 창에서 선택 **SilkRoad 수명 Suite**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![응용 프로그램][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트
이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Azure AD SSO SilkRoad 수명 도구 모음 및 테스트 합니다.

SSO toowork에 대 한 Azure AD는 tooknow SilkRoad 수명 Suite tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다. 즉, Azure AD 사용자 및 hello SilkRoad 수명 도구 모음에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.

Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SilkRoad 수명 도구 모음에서 합니다.

tooconfigure 및 Azure AD에서 single sign-on SilkRoad 수명 도구 모음과 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.

1. **[Azure AD single sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.
2. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.
3. **[SilkRoad 수명 Suite 테스트 사용자 만들기](#creating-a-silkroad-life-suite-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 SilkRoad 수명 도구 모음에 해당 하는 도구입니다.
4. **[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.
5. **[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성
이 섹션의 hello 목표는 hello Azure 클래식 포털에서에서 Azure AD SSO tooenable 및 SilkRoad 수명 Suite 응용 프로그램에 SSO tooconfigure입니다.

**SilkRoad 수명 도구 모음과 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**

1. 관리자 권한으로 로그온 tooyour SilkRoad 회사 사이트입니다. 

  >[!NOTE] 
  > Microsoft Azure AD와 페더레이션 구성 하기 위한 응용 프로그램 SilkRoad 수명 Suite 인증 tooobtain 액세스 toohello SilkRoad 지원 또는 SilkRoad 서비스 담당자를 문의 하십시오.
  > 

2. 너무 이동**서비스 공급자**, 클릭 하 고 **페더레이션 세부 정보**합니다. 
   
    ![Azure AD Single Sign-On][10] 

3. 클릭 **페더레이션 메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.
   
    ![Azure AD Single Sign-On][11] 

4. Hello hello에 Azure 클래식 포털에서에서 **SilkRoad 수명 Suite** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.
   
    ![Single Sign-on 구성][6] 

5. Hello에 **어떻게 tooSilkRoad 수명 Suite에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Azure AD Single Sign-On][7] 

6. Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD Single Sign-On][8]   
 1. Hello에 **로그온 URL** textbox, 사용자에 대 한 toosign tooyour SilkRoad 수명 Suite 사이트에서 사용 하는 hello URL 입력 (예:: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. 다운로드 한 열기 hello **Silkroad** 메타 데이터 파일. 
 3. Hello 찾을 **AssertionConsumerService** 태그 및 복사 hello **위치** 특성입니다.         
   
    ![Azure AD Single Sign-On][21] 
 4. Hello에 hello 값을 붙여 **회신 URL** 텍스트 상자에 붙여넣습니다.  
 5. **다음**을 누릅니다.

6. Hello에 **SilkRoad 수명 도구 모음에서 single sign on 구성** 페이지 hello 다음 단계를 수행 합니다.
   
    ![Azure AD Single Sign-On][9]  
 1. 다운로드 인증서를 클릭 한 다음 컴퓨터에 hello 파일을 저장 합니다.  
 2. **다음**을 누릅니다.

7. **SilkRoad** 응용 프로그램에서 **인증 원본**을 클릭합니다.
   
    ![Azure AD Single Sign-On][12] 

8. **인증 원본 추가**를 클릭합니다. 
   
    ![Azure AD Single Sign-On][13] 

9. Hello에 **인증 소스 추가** 섹션를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD Single Sign-On][14]  
 1. 아래 **옵션 2-메타 데이터 파일**, 클릭 **찾아보기** tooupload hello 메타 데이터 파일을 다운로드 합니다.  
 2. **파일 데이터를 사용하여 ID 공급자 만들기**를 클릭합니다.

10. Hello에 **인증 원본** 섹션에서 클릭 **편집**합니다. 
    
     ![Azure AD Single Sign-On][15] 

11. Hello에 **인증 원본 편집** 대화 상자에서 hello 다음 단계를 수행 합니다. 
    
     ![Azure AD Single Sign-On][16] 
 1. **사용**을 **예**로 선택합니다.   
 2. Hello에 **IdP 설명** 텍스트 상자에 구성에 대 한 설명 입력 합니다 (예:: *Azure AD SSO*).  
 3. Hello에 **IdP 이름** 텍스트 상자에는 특정 tooyour 구성 이름 (예:: *Azure SP*).  
 4. **Save**를 클릭합니다.

12. 다른 모든 인증 원본을 사용하지 않도록 설정합니다. 
    
     ![Azure AD Single Sign-On][17]

13. Hello hello에 Azure 클래식 포털에서에서 **Single sign on 확인** 페이지 **다음**합니다.  
    
     ![Azure AD Single Sign-On][18]

14. Hello에 **Single sign on 확인** 페이지 **완료**합니다.
    
     ![Azure AD Single Sign-On][19]

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.

![Azure AD 사용자 만들기][20]

**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**

1. Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. 사용자 유형에서 조직의 새 사용자를 선택합니다.  
 2. Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다. 
 3. **다음**을 누릅니다.

6. Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다. 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. Hello에 **이름** 텍스트 상자에 **Britta**합니다.    
 2. Hello에 **성** 텍스트 상자에, **Simon**합니다. 
 3. Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다. 
 4. Hello에 **역할** 목록에서 **사용자**합니다.
 5. **다음**을 누릅니다.

7. Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Hello hello 값 적어 **새 암호**합니다. 
 2. 페이지 맨 아래에 있는 **완료**을 참조하세요.   

### <a name="create-a-silkroad-life-suite-test-user"></a>SilkRoad Life Suite 테스트 사용자 만들기
hello이이 섹션의 목적은 toocreate SilkRoad 수명 도구 모음에서 Britta Simon 라고 하는 사용자입니다. Britta의는 SSO ID가 있어야 합니다 (tooas 라고도 *AuthParam*) Britta의 일치 하는 **emailaddress** Azure AD에서 합니다.

**toocreate Britta Simon SilkRoad 수명 제품군의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**

- 프로그램 SilkRoad 수명 Suite 지원 팀 toocreate로 있는 사용자는 요청 **SSO ID** hello과 같은 값인 특성 hello **emailaddress** Azure AD에서 Britta Simon의 합니다.

### <a name="assign-hello-azure-ad-test-user"></a>Azure AD hello 테스트 사용자를 할당 합니다.
이 섹션의 hello 목표 그녀의 액세스 tooSilkRoad 수명 도구 모음을 부여 하 여 tooenable Britta Simon toouse Azure SSO를입니다.

![사용자 할당][200] 

**tooassign Britta Simon tooSilkRoad 수명 Suite hello 다음 단계를 수행 합니다.**

1. Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.
   
    ![사용자 할당][201] 

2. Hello 응용 프로그램 목록에서 선택 **SilkRoad 수명 Suite**합니다.
   
    ![사용자 할당][202] 

3. Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.
   
    ![사용자 할당][203] 

4. Hello [사용자] 목록에서 선택 **Britta Simon**합니다.

5. Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a>Single Sign-On 테스트
이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.  

Hello 액세스 패널에서에서 hello SilkRoad 수명 Suite 타일을 클릭할 때 자동으로 로그온 tooyour SilkRoad 수명 Suite 응용 프로그램을 구해야 합니다.

## <a name="additional-resources"></a>추가 리소스
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





