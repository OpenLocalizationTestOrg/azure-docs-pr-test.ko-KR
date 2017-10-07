---
title: "자습서: TOPdesk - Secure와 Azure Active Directory 통합 | Microsoft Docs"
description: "자세한 내용은 방법 toouse TOPdesk-Azure Active Directory tooenable single sign on, 자동화 된 프로 비전 등을 사용 하 여 보안!입니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>자습서: TOPdesk - Secure와 Azure Active Directory 통합
hello이이 자습서는 Azure와 TOPdesk tooshow hello 통합-보안을 설정 합니다.  
이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* TOPdesk - Secure Single Sign-On이 설정된 구독

Hello Azure AD 사용자를이 자습서를 완료 한 후 지정한 tooTOPdesk-보안가 topdesk-Secure 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 hello 응용 프로그램에 수 toosingle 로그인 이거나 hello를 사용 하 여 [소개 액세스 패널 toohello](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. TOPdesk-Secure에 대 한 hello 응용 프로그램 통합 사용
2. Single Sign-On 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "시나리오")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>TOPdesk-Secure에 대 한 hello 응용 프로그램 통합 사용
hello이이 섹션의 목적은 toooutline 어떻게 TOPdesk-Secure에 대 한 tooenable hello 응용 프로그램 통합 합니다.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>TOPdesk-Secure에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.
1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.

3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "응용 프로그램")

4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "응용 프로그램 추가")

5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")

6. Hello에 **검색 상자**, 형식 **TOPdesk-Secure**합니다.
   
    ![응용 프로그램 갤러리](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "응용 프로그램 갤러리")

7. Hello 결과 창에서 선택 **TOPdesk-Secure**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Single Sign-On 구성
hello이이 섹션의 목적은 toooutline 어떻게 tooenable 사용자 tooauthenticate tooTOPdesk-hello SAML 프로토콜 기반의 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 보안을 설정 합니다.  
구성 single sign on TOPdesk-Secure에 대 한 하려면 로고 아이콘 파일을 tooupload 합니다. tooget hello 아이콘 파일 연락처 hello TOPdesk 지원 팀입니다.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.
1. Tooyour 로그온 **TOPdesk-Secure** 회사 사이트에 관리자 권한으로 합니다.
2. Hello에 **TOPdesk** 메뉴를 클릭 하 여 **설정을**합니다.
   
    ![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")

3. **로그인 설정**을 클릭합니다.
   
    ![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")

4. Hello 확장 **로그인 설정** 메뉴를 차례로 클릭 **일반**합니다.
   
    ![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")

5. Hello에 **Secure** hello의 섹션 **SAML 로그인** 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.
   
    ![기술 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "기술 설정")
   
    a. 클릭 **다운로드** toodownload hello 공용 메타 데이터 파일을 한 다음 컴퓨터에 로컬로 저장 합니다.
   
    b. Hello 메타 데이터 파일을 열고 찾은 후 hello **AssertionConsumerService** 노드.
    
    ![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")
   
    c. 복사 hello **AssertionConsumerService** 값입니다.  
      
    > [!NOTE]
    > Hello에 대 한 값 hello 필요 합니다 **앱 URL 구성** 이 자습서의 뒷부분에 나오는 섹션.
    > 
    > 

6. 다른 웹 브라우저 창에서 **Azure 클래식 포털** 에 관리자 권한으로 로그인합니다.

7. Hello에 **TOPdesk-Secure** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Single Sign-On 구성")

8. Hello에 **방법을 tooTOPdesk-에 toosign 사용자 같은 보안** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Single Sign-On 구성")

9. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "앱 URL 구성")
   
    a. Hello에 **TOPdesk-Secure 로그온 URL** 사용자 toosign TOPdesk-Secure 응용 프로그램에 사용 하는 형식 hello URL 텍스트 상자 (예:: "*https://qssolutions.topdesk.net*").
   
    b. Hello에 **TOPdesk – Public 회신 URL** 텍스트 붙여넣기 hello **TOPdesk-Secure AssertionConsumerService URL** (예:: "*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. **다음**을 누릅니다.

10. Hello에 **TOPdesk-Secure에서 single sign on 구성** 페이지, toodownload 메타 데이터 파일을 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 로컬로 저장 합니다.
    
    ![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Single Sign-On 구성")

11. toocreate 인증서 파일을 hello 다음 단계를 수행 합니다.
    
    ![인증서](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "인증서")
    
    a. Hello open 다운로드 한 메타 데이터 파일입니다.
    b. Hello 확장 **RoleDescriptor** 노드에 **xsi: type** 의 **fed: ApplicationServiceType**합니다.
    c. Hello의 hello 값을 복사 **X509Certificate** 노드.
    d. 복사 저장 hello **X509Certificate** 파일에서 컴퓨터에 로컬로 값입니다.

12. Topdesk-Secure 회사 사이트에 hello **TOPdesk** 메뉴를 클릭 하 여 **설정을**합니다.
    
    ![설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "설정")

13. **로그인 설정**을 클릭합니다.
    
    ![로그인 설정](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "로그인 설정")

14. Hello 확장 **로그인 설정** 메뉴를 차례로 클릭 **일반**합니다.
    
    ![일반](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "일반")

15. Hello에 **공용** 섹션에서 클릭 **추가**합니다.
    
    ![추가](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "추가")

16. Hello에 **SAML 구성 도우미** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.
    
    ![SAML 구성 도우미](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 구성 도우미")
    
    a. 다운로드 한 메타 데이터 파일 tooupload **페더레이션 메타 데이터**, 클릭 **찾아보기**합니다.

    b. 인증서 파일 tooupload **Certificate (RSA)**, 클릭 **찾아보기**합니다.

    c. 아래에서 hello TOPdesk 지원 팀에서 받은 tooupload hello 로고 파일 **로고 아이콘**, 클릭 **찾아보기**합니다.

    d. Hello에 **사용자 이름 특성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.

    e. Hello에 **표시 이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.

    f. **Save**를 클릭합니다.

17. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
    
    ![Single Sign-On 구성](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Single Sign-On 구성")

## <a name="configuring-user-provisioning"></a>사용자 프로비전 구성
TOPdesk-에 순서 tooenable Azure AD 사용자가 toolog에서 안전은 프로 비전 해야 TOPdesk-Secure에 있습니다.  
TOPdesk-hello 경우에서 안전한 프로 비전은 수동 작업입니다.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:
1. Tooyour 로그온 **TOPdesk-Secure** 회사 사이트에서 관리자 권한으로 로그인 합니다.
2. Hello 메뉴에서 hello 위에 표시를 클릭 **TOPdesk \> 새로 \> 지원 파일 \> 연산자**합니다.
   
    ![연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "연산자")

3. Hello에 **New 연산자** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![새로운 연산자](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "새로운 연산자")
   
    a. Hello 일반 탭을 클릭 합니다.
   
    b. Hello에 **Surname** hello 텍스트 상자 **일반** 섹션 tooprovision 하려는 유효한 Azure Active Directory 계정의 hello 마지막 이름을 입력 합니다.
   
    c. 선택 된 **사이트** hello 계정 hello에 대 한 **위치** 섹션.
   
    d. Hello에 **로그인 이름** hello 텍스트 상자 **TOPdesk Login** 섹션에서 사용자에 대 한 로그인 이름을 입력 합니다.
   
    e. **Save**를 클릭합니다.

> [!NOTE]
> 모든 다른 TOPdesk-Secure 사용자 계정 만들기 도구 또는 TOPdesk-에서 제공 된 Api tooprovision AAD 사용자 계정을 보안을 사용할 수 있습니다.
> 
> 

## <a name="assigning-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign 사용자 tooTOPdesk-Secure에 hello 다음 단계를 수행 합니다.
1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 * * TOPdesk-Secure * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
    ![사용자 할당](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "사용자 할당")

3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
    ![예](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

