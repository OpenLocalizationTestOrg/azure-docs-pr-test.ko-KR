---
title: "자습서: Replicon과 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Replicon toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>자습서: Replicon과 Azure Active Directory 통합
hello이이 자습서는 Azure와 Replicon tooshow hello 통합 합니다. 이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Replicon 테넌트

이 자습서를 완료 한 후 hello Azure AD 사용자 tooReplicon 배정 됩니다 Replicon 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 또는 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [소개 toohello 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. Replicon에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-replicon-tutorial/IC777798.png "시나리오")

## <a name="enable-hello-application-integration-for-replicon"></a>Replicon에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정
hello이이 섹션의 목적은 toooutline 어떻게 Replicon에 tooenable hello 응용 프로그램 통합 합니다.

**Replicon에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램](./media/active-directory-saas-replicon-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-replicon-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Replicon**합니다.
   
    ![응용 프로그램 갤러리](./media/active-directory-saas-replicon-tutorial/IC777799.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Replicon**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooReplicon hello SAML 프로토콜에 따라 하는 방법입니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Replicon** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777801.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooReplicon에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777802.png "Single Sign-On 구성")
3. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-replicon-tutorial/IC777803.png "앱 URL 구성")
  1. Hello에 **Replicon 로그온 URL** 텍스트 상자에 Replicon 테 넌 트 URL (예:: *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. Hello에 **Replicon 회신 URL** 텍스트 상자에 Replicon **AssertionConsumerService** URL (예:: *https://global.replicon.com/! / saml2/회사/sso/post*).  
      
     >[!NOTE]
     >Hello Replicon 메타 데이터에서 hello URL을 가져올 수 있습니다: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**합니다.
     > 
     > 
 
  3. **다음**을 누릅니다.

4. Hello에 **Replicon에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, 한 다음 컴퓨터에 hello 메타 데이터를 저장 합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC777804.png "Single Sign-On 구성")
5. 다른 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.

6. SAML 2.0 tooconfigure hello 다음 단계를 수행 합니다.
   
    ![SAML 인증 사용](./media/active-directory-saas-replicon-tutorial/IC777805.png "SAML 인증 사용")
  
  1. toodisplay hello **EnableSAML Authentication2** 대화 상자에서 회사 키 뒤 tooyour URL을 따라 hello 추가: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * hello 다음 hello 전체 URL의 hello 스키마를 보여 줍니다.  
   **https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Hello 클릭 ** + ** tooexpand hello **v20Configuration** 섹션.
   3. Hello 클릭 ** + ** tooexpand hello **metaDataConfiguration** 섹션.
   4. 클릭 **파일 선택**, tooselect identity 공급자 메타 데이터 XML 파일 및 클릭 **전송**합니다.

7. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-replicon-tutorial/IC778418.png "Single Sign-On 구성")
   
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

Tooenable Azure AD 사용자가 toolog Replicon에 주문 하 고에 Replicon에 이들 프로 비전 해야 합니다.  

Hello Replicon의 경우에서 프로 비전은 수동 작업입니다.

**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**

1. 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.
2. 너무 이동**관리 \> 사용자**합니다.
   
    ![사용자](./media/active-directory-saas-replicon-tutorial/IC777806.png "사용자")
3. **+사용자 추가**를 클릭합니다.
   
    ![사용자 추가](./media/active-directory-saas-replicon-tutorial/IC777807.png "사용자 추가")
4. Hello에 **사용자 프로필** 섹션를 hello 다음 단계를 수행 합니다.
   
    ![사용자 프로필](./media/active-directory-saas-replicon-tutorial/IC777808.png "사용자 프로필")
   
  1. Hello에 **로그인 이름** 텍스트 형식 hello Azure AD 전자 메일 주소 하려는 hello Azure AD 사용자의 tooprovision 합니다.
  2. **인증 유형**으로 **SSO**를 선택합니다.
  3. Hello에 **부서** textbox hello 사용자의 부서를 입력 합니다.
  4. **직원 형식**으로 **관리자**를 선택합니다.
  5. **사용자 프로필 저장**을 클릭합니다.

>[!NOTE]
>다른 Replicon 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Replicon에서 제공 된 Api입니다.
> 
> 

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooReplicon hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.

2. Hello에 **Replicon** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
    ![사용자 할당](./media/active-directory-saas-replicon-tutorial/IC777809.png "사용자 할당")

3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
    ![예](./media/active-directory-saas-replicon-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

