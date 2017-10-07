---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Salesforce 샌드박스 toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>자습서: Salesforce Sandbox와 Azure Active Directory 통합

hello이이 자습서는 Azure 및 Salesforce Sandbox의 tooshow hello 통합 합니다.  

>[!TIP]
>피드백에 대 한 참조 hello [Azure 지원 페이지](http://go.microsoft.com/fwlink/?LinkId=521878)합니다. 
> 

샌드박스 제공 하면 hello 기능 toocreate 다양 한 개발, 것과 같은 용도 대 한 별도 환경에서 조직의 여러 복사본 hello 데이터와 Salesforce 프로덕션에서 응용 프로그램을 그대로 유지 하지 않고 학습 및 테스트 하 고, 조직입니다.  

자세한 내용은 [샌드박스 개요](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Salesforce.com에서 샌드박스

하면 유효한 샌드박스가 Salesforce.com에 아직 없는 경우 Salesforce toocontact을 해야 합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. Salesforce Sandbox에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 도메인 사용
4. 사용자 프로비전 구성
5. 사용자 할당

![시나리오](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "시나리오")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Salesforce Sandbox에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정
hello이이 섹션의 목적은 toooutline 어떻게 Salesforce sandbox에 tooenable hello 응용 프로그램 통합 합니다.

**Salesforce sandbox에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "응용 프로그램")
4. tooopen hello **응용 프로그램 갤러리**, 클릭 **앱 추가**, 클릭 하 고 **내 조직 toouse 응용 프로그램 추가**합니다.
   
   ![어떻게 하 시겠습니까 toodo 원하는? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "하 신 toodo 원하는?")
5. Hello에 **검색 상자**, 형식 **Salesforce Sandbox**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "응용 프로그램 갤러리")
6. Hello 결과 창에서 선택 **Salesforce Sandbox**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce 샌드박스")
   
## <a name="configur-single-sign-on-sso"></a>SSO(Single Sign-On) 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSalesforce hello SAML 프로토콜에 따라 하는 방법입니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Salesforce Sandbox** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooSalesforce Sandbox에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce 샌드박스")
3. Hello에 **앱 URL 구성** 페이지 hello **로그온 URL** textbox hello 패턴으로 URL을 입력 `http://company.my.salesforce.com`, 클릭 하 고 **다음**합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "앱 URL 구성")
4. 이미 구성한 single sign on 다른 Salesforce Sandbox 인스턴스 디렉터리의 경우 hello 구성도 해야 **식별자** toohave hello hello와 같은 값 **로그온 URL**합니다. 
 * hello **식별자** hello를 확인 하 여 필드를 찾을 수 **고급 설정 표시** hello에 확인란 **앱 URL 구성** hello 대화 상자의 페이지입니다.
5. Hello에 **Salesforce 샌드박스에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Single Sign-On 구성")
6. 다른 웹 브라우저 창에서 Salesforce 샌드박스에 관리자로 로그인합니다.
7. Hello 메뉴에서 hello 위에 표시를 클릭 **설치**합니다.
   
   ![설치](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "설치")
8. Hello hello 왼쪽의 탐색 창에서 클릭 **보안 제어**, 클릭 하 고 **Single Sign On 설정**합니다.
   
   ![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On 설정")
9. Single Sign-on 설정 섹션 hello hello 다음 단계를 수행 합니다.
   
   ![Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On 설정")  
 1.  **SAML 사용**을 선택합니다. 
 2.  **새로 만들기**를 클릭합니다.
10. SAML Single Sign-on 설정 섹션 hello hello 다음 단계를 수행 합니다.
    
    ![SAML Single Sign-On 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On 설정")  
 1. Hello 이름 텍스트 상자에 입력 hello 구성의 hello 이름 (예:: *SPSSOWAAD\_테스트*). 
 2. Hello hello에 Azure 클래식 포털에서에서 **Salesforce 샌드박스에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **발급자**텍스트 상자에 붙여넣습니다.
 3. Hello에 **엔터티 Id** 텍스트 상자에 **https://test.salesforce.com** 인스턴스인 경우 hello 첫 번째 Salesforce Sandbox tooyour 디렉터리를 추가 합니다. Hello에 대 한 한 다음 Salesforce Sandbox의 인스턴스를 이미 추가한 경우 **엔터티 ID** hello에서 형식을 **로그온 URL**를이 형식에:`http://company.my.salesforce.com`   
 4. 클릭 **찾아보기** tooupload hello 인증서를 다운로드 합니다.  
 5. 으로 **SAML Id 유형**선택, **어설션 hello 사용자 개체에서 hello 페더레이션 ID가 포함 되어**합니다. 
 6. 으로 **SAML Id 위치**선택, **hello hello Subject 문의 NameIdentifier 요소에 Id가**합니다.
 7. Hello hello에 Azure 클래식 포털에서에서 **Salesforce 샌드박스에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **원격 로그인 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다. 
 8. SFDC는 SAML 로그아웃을 지원하지 않습니다.  문제를 해결 붙여 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello로 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.
 9. **서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다. 
 10. **Save**를 클릭합니다.
11. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
    
    ![Single Sign-On 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Single Sign-On 구성")

## <a name="enable-your-domain"></a>도메인 활성화
이 섹션에서는 이미 도메인을 만들었다고 가정합니다.  자세한 내용은 [도메인 이름 정의](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)를 참조하세요.

**tooenable 해당 도메인을 hello 다음 단계를 수행 합니다.**

1. Hello 왼쪽된 탐색 창에서 클릭 **도메인 관리**, 클릭 하 고 **내 도메인입니다.**
   
   ![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "내 도메인")
   
   >[!NOTE]
   >도메인이 올바르게 구성되었는지 확인합니다. 
   > 
2. Hello에 **로그인 페이지 설정** 섹션에서 클릭 **편집**,으로 다음 **인증 서비스**선택, 이전 hello에서 hello SAML Single Sign-on 설정의 hello 이름 섹션을 마지막으로 클릭 **저장**합니다.
   
   ![내 도메인](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "내 도메인")

구성 된 도메인이 되는 즉시 사용자가 hello 도메인 URL toologin toohello Salesforce sandbox를 사용 해야 합니다.  

hello URL tooget hello 값 hello 이전 섹션에서 만든 hello SSO 프로필을 클릭 합니다.

## <a name="configure-user-provisioning"></a>사용자 프로비전 구성
이 섹션의 hello 목적은 toooutline 어떻게 tooSalesforce 샌드박스 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.

**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**

1. Hello 위쪽 탐색 모음에서 hello Salesforce 포털에서 사용자 메뉴 이름 tooexpand 선택 합니다.
   
   ![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "내 설정")
2. 사용자 메뉴에서 선택 **내 설정** tooopen 프로그램 **내 설정** 페이지.
3. Hello 왼쪽된 창에서 클릭 **개인** tooexpand 개인 섹션 hello 및 클릭 **Reset My Security Token**:
   
   ![내 설정](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "내 설정")
4. Hello에 **Reset My Security Token** 페이지 **보안 토큰 재설정** toorequest Salesforce.com 보안 토큰이 포함 된 전자 메일입니다.
   
   ![새 토큰](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "새 토큰")
5. "**Salesforce.com.com 보안 확인**"을 제목으로 Salesforce.com에서 온 이메일의 받은 편지함을 확인합니다.
6. 이 전자 메일 및 복사 hello 보안 토큰 값을 검토 합니다.
7. Hello hello에 Azure 클래식 포털에서에서 **salesforce Sandbox** 응용 프로그램 통합 페이지에서 클릭 **사용자 프로비저닝을 구성할** tooopen hello **사용자 프로비저닝 구성**대화 상자.
   
   ![사용자 프로비전 구성](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "사용자 프로비전 구성")
8. Hello에 **프로그램 Salesforce Sandbox 자격 증명 tooenable 자동 사용자 프로비저닝 입력** 페이지 hello 다음 구성 설정을 제공 합니다.
   
   ![Salesforce 샌드박스](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce 샌드박스")   
 1. Hello에 **Salesforce Sandbox 관리자 사용자 이름** 텍스트 상자에 Salesforce 계정에 hello 이름 **시스템 관리자** 할당 Salesforce.com에 프로필입니다.
 2. Hello에 **Salesforce Sandbox 관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.
 3. Hello에 **사용자 보안 토큰** 텍스트 붙여넣기 hello 보안 토큰 값입니다.
 4. 클릭 **유효성 검사** tooverify 구성 합니다.
 5. Hello 클릭 **다음** 단추 tooopen hello **확인** 페이지.
9. Hello에 **확인** 페이지 **완료** toosave 구성 합니다.
   
## <a name="assigning-users"></a>사용자 할당

tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooSalesforce 샌드박스 hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 * * Salesforce Sandbox * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "예")

이제 10 분 동안 기다렸다가 hello 계정 동기화 된 tooSalesforce 샌드박스 되었는지 확인 합니다.

SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](https://msdn.microsoft.com/library/dn308586)합니다.

