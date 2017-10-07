---
title: "자습서: Benefitsolver와 Azure Active Directory 통합 | Microsoft Docs"
description: "방법을 toouse Benefitsolver tooenable Azure Active Directory와 single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>자습서: Benefitsolver와 Azure Active Directory 통합
hello이이 자습서는 Azure와 Benefitsolver tooshow hello 통합 합니다.  

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Benefitsolver SSO(Single Sign-On)가 설정된 구독

이 자습서를 완료 한 후 hello Azure AD 사용자 tooBenefitsolver 배정 됩니다 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. Benefitsolver에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "시나리오")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Benefitsolver에 대 한 hello 응용 프로그램 통합 사용
hello이이 섹션의 목적은 toooutline 어떻게 Benefitsolver에 tooenable hello 응용 프로그램 통합 합니다.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>Benefitsolver에 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.
1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Benefitsolver**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Benefitsolver**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooBenefitsolver hello SAML 프로토콜에 따라 하는 방법입니다.  

Benefitsolver 응용 프로그램에 사용자 지정 특성 매핑을 tooyour tooadd 요구 하는 특정 형식으로 hello SAML 어설션이 **saml 토큰 특성** 구성 합니다. 

다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.

![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Benefitsolver** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooBenefitsolver에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Single Sign-On 구성")
3. Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.
   
   ![앱 설정 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "앱 설정 구성")
   
   1. Hello에 **로그온 URL** 텍스트 상자에 **http://azure.benefitsolver.com**합니다.
   2. Hello에 **회신 URL** 텍스트 상자에 **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**합니다.  
   3. **다음**을 누릅니다.
4. Hello에 **Benefitsolver에서 single sign on 구성** 페이지, toodownload 메타 데이터를 클릭 하 여 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 로컬로 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Single Sign-On 구성")
5. Hello 다운로드 한 메타 데이터 파일 tooyour Benefitsolver 지원 팀에 보냅니다.
   
   >[!NOTE]
   >Benefitsolver 지원 팀에 toodo hello 실제 SSO 구성을 있습니다. 구독에 SSO를 사용하도록 설정하면 알림을 받을 수 있습니다.
   >

6. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Single Sign-On 구성")
7. Hello 메뉴에서 hello 위에 표시를 클릭 **특성** tooopen hello **SAML 토큰 특성** 대화 상자.
   
   ![특성](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "특성")
8. tooadd hello 필요한 특성 매핑을 hello 다음 단계를 수행 합니다.
   
   ![특성](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "특성")
   
   | 특성 이름 | 특성 값 |
   | --- | --- |
   | ClientID |이 값이 필요한 tooget이 Benefitsolver 지원 팀에서. |
   | ClientKey |이 값이 필요한 tooget이 Benefitsolver 지원 팀에서. |
   | LogoutURL |이 값이 필요한 tooget이 Benefitsolver 지원 팀에서. |
   | EmployeeID |이 값이 필요한 tooget이 Benefitsolver 지원 팀에서. |
   
   1. 위의 hello 테이블의 각 데이터 행에 대 한 클릭 **사용자 특성 추가**합니다.
   2. Hello에 **특성 이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.
   3. Hello에 **특성 값** textbox, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.
   4. 페이지 맨 아래에 있는 **완료**을 참조하세요.
9. **변경 내용 적용**을 클릭합니다.

## <a name="configure-user-provisioning"></a>사용자 프로비전 구성
Tooenable Azure AD 사용자가 toolog Benefitsolver로 주문 하 고에 Benefitsolver에 이들 프로 비전 해야 합니다.  

Hello 경우 Benefitsolver의 직원 데이터는 채워집니다 (일반적으로 nightly) HRIS 시스템에서 Census 파일을 통해 응용 프로그램입니다.  

>[!NOTE]
>다른 Benefitsolver 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 Benefitsolver tooprovision에서 제공 된 Api입니다. 
> 

## <a name="assigning-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign 사용자 tooBenefitsolver hello 다음 단계를 수행 합니다.
1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 * * Benefitsolver * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "예")

Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

