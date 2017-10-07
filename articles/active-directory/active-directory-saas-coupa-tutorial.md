---
title: "자습서: Coupa와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Coupa toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>자습서: Coupa와 Azure Active Directory 통합
hello이이 자습서는 Azure와 Coupa tooshow hello 통합 합니다.  
이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Coupa SSO(Single Sign-On)가 설정된 구독

이 자습서를 완료 한 후 hello Azure AD 사용자 tooCoupa 배정 됩니다 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

* Coupa에 대 한 hello 응용 프로그램 통합 사용
* Single Sign-On 구성
* 사용자 프로비전 구성
* 사용자 할당

![시나리오](./media/active-directory-saas-coupa-tutorial/IC791897.png "시나리오")

## <a name="enable-hello-application-integration-for-coupa"></a>Coupa에 대 한 hello 응용 프로그램 통합 사용
hello이이 섹션의 목적은 toooutline 어떻게 Coupa에 대 한 tooenable hello 응용 프로그램 통합 합니다.

**Coupa에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-coupa-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-coupa-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Coupa**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-coupa-tutorial/IC791898.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Coupa**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooCoupa hello SAML 프로토콜에 따라 하는 방법입니다.  

Single sign on Coupa에 대 한 구성 하려면 인증서에서 지문 값 tooretrieve 합니다. 이 절차에 익숙하지 않은 경우 참조 [어떻게 tooretrieve 인증서의 지문 값](http://youtu.be/YKQF266SAxI)합니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. 관리자 권한으로 Coupa 회사 사이트 tooyour에 로그인 합니다.
2. 너무 이동**설치 \> 보안 제어**합니다.
   
   ![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")
3. toodownload hello Coupa 메타 데이터 파일 tooyour 컴퓨터 클릭 **다운로드 하 여 SP 메타 데이터를 가져와**합니다.
   
   ![Coupa SP 메타데이터](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP 메타데이터")
4. 다른 브라우저 창에서 toohello Azure 클래식 포털에 로그인 합니다.
5. Hello에 **Coupa** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791902.png "Single Sign-On 구성")
6. Hello에 **어떻게 tooCoupa에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791903.png "Single Sign-On 구성")
7. Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-coupa-tutorial/IC791904.png "앱 URL 구성")   
   1. Hello에 **로그온 URL** tooyour Coupa 응용 프로그램에서 사용자가 toosign 프로그램에서 사용 하는 URL 입력 텍스트 (예:: "*http://company.Coupa.com*").
   2. 다운로드 한 Coupa 메타 데이터 파일을 열고 hello 복사 **AssertionConsumerService index/URL**합니다.
   3. Hello에 **Coupa 회신 URL** 텍스트 붙여넣기 hello **AssertionConsumerService index/URL** 값입니다.
   4. **다음**을 누릅니다.
8. Hello에 **Coupa에서 single sign on 구성** 페이지, toodownload 메타 데이터 파일을 클릭 하 여 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 로컬로 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791905.png "Single Sign-On 구성")
9. Hello Coupa 회사 사이트에서 이동 너무**설치 \> 보안 제어**합니다.
   
   ![보안 제어](./media/active-directory-saas-coupa-tutorial/IC791900.png "보안 제어")
10. Hello에 **Coupa 자격 증명을 사용 하 여 로그인** 섹션를 hello 다음 단계를 수행 합니다.  

   ![Coupa 자격 증명을 사용하여 로그인](./media/active-directory-saas-coupa-tutorial/IC791906.png "Coupa 자격 증명을 사용하여 로그인") 
   1. **SAML을 사용하여 로그인**을 선택합니다.
   2. 클릭 **찾아보기** tooupload 다운로드 한 Azure Active 메타 데이터 파일.
   3. **Save**를 클릭합니다.
11. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
    
   ![Single Sign-On 구성](./media/active-directory-saas-coupa-tutorial/IC791907.png "Single Sign-On 구성")
    
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

Tooenable Azure AD 사용자가 toolog Coupa에 주문 하 고에 Coupa에 이들 프로 비전 해야 합니다.  

* Hello Coupa의 경우에서 프로 비전은 수동 작업입니다.

**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**

1. Tooyour 로그인 **Coupa** 회사 사이트에서 관리자 권한으로 로그인 합니다.
2. Hello 메뉴에서 hello 위에 표시를 클릭 **설치**, 클릭 하 고 **사용자**합니다.
   
   ![사용자](./media/active-directory-saas-coupa-tutorial/IC791908.png "사용자")
3. **만들기**를 클릭합니다.
   
   ![사용자 만들기](./media/active-directory-saas-coupa-tutorial/IC791909.png "사용자 만들기")
4. Hello에 **사용자 만들** 섹션를 hello 다음 단계를 수행 합니다.
   
   ![사용자 세부 정보](./media/active-directory-saas-coupa-tutorial/IC791910.png "사용자 세부 정보")
   
   1. 형식 hello **로그인**, **이름**, **성**, **Single Sign-on ID**, **전자 메일** 의 특성을 유효한 Azure Active Directory 계정을 tooprovision hello에 관련 텍스트 상자입니다.
   2. **만들기**를 클릭합니다.   
   >[!NOTE]
   >따라 활성화 hello Azure Active Directory 계정 소유자 링크 tooconfirm hello 계정 사용 하 여 전자 메일을 받게 됩니다. 
   > 

>[!NOTE]
>다른 Coupa 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Coupa에서 제공 된 Api입니다. 
> 

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooCoupa hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 * * Coupa * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-coupa-tutorial/IC791911.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-coupa-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

