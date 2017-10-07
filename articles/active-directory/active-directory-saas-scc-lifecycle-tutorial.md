---
title: "자습서: SCC LifeCycle과 Azure Active Directory 통합 | Microsoft Docs"
description: "로그온, 자동화 된 프로 비전 등와 Azure Active Directory tooenable toouse SCC LifeCycle single 하는 방법에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>자습서: SCC LifeCycle과 Azure Active Directory 통합
hello이이 자습서는 Azure와 SCC LifeCycle tooshow hello 통합 합니다.  

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* SCC LifeCycle SSO(Single Sign-On)가 설정된 구독

이 자습서를 완료 하면 Azure AD 할당 한 사용자는 수명 주기 됩니다 tooSCC 수 toosingle 기호 hello 응용 프로그램으로 SCC LifeCycle 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 hello 또는 hello를 사용 하 여 [소개 액세스 패널 toohello](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. SCC LifeCycle에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "시나리오")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>SCC LifeCycle에 대 한 hello 응용 프로그램 통합을 사용 하도록 설정
hello이이 섹션의 목적은 toooutline 어떻게 SCC LifeCycle에 대 한 tooenable hello 응용 프로그램 통합 합니다.

**SCC LifeCycle에 대 한 tooenable hello 응용 프로그램 통합 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
    ![응용 프로그램](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
    ![응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
    ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **SCC LifeCycle**합니다.
   
    ![응용 프로그램 갤러리](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **SCC LifeCycle**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooSCC 수명 주기 hello SAML 프로토콜에 따라 하는 방법입니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **SCC LifeCycle** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello * * Single Sign-on 구성 * * 대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooSCC 수명 주기에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
    ![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Single Sign-On 구성")
3. Hello에 **앱 URL 구성** 페이지 hello **로그온 URL** textbox hello URL 입력에서 사용 하는 사용자가 toosign tooyour SCC LifeCycle 응용 프로그램 패턴 hello를 사용 하 여 "*https:// bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*"를 클릭 하 고 **다음**합니다.
   
    ![앱 URL 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "앱 URL 구성")
4. Hello에 **SCC LifeCycle에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, 메타 데이터 파일을 컴퓨터에 로컬로 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Single Sign-On 구성")
5. 해당 메타 데이터 파일 tooSCC LifeCycle 지원 팀으로 전달 합니다.
   
   >[!NOTE]
   >Single sign on에 toobe hello SCC LifeCycle 지원 팀으로 사용할 수 있습니다.
   > 
   > 

6. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
   
    ![Single Sign-On 구성](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Single Sign-On 구성")
   
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

Tooenable Azure AD 사용자가 toolog SCC LifeCycle에 주문 하 고에서 SCC LifeCycle에 이들 프로 비전 해야 합니다. 사용자에 대 한 있습니다 tooconfigure tooSCC 수명 주기를 프로 비전 작업 항목이 없습니다.

SCC LifeCycle에 할당 된 사용자 시도 toolog 때 필요한 경우 SCC LifeCycle 계정이 자동으로 생성 됩니다.

>[!NOTE]
>다른 SCC LifeCycle 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision SCC LifeCycle에서 제공 된 Api입니다.
> 
> 

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooSCC 수명 주기 단계를 수행 하는 hello를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 * * SCC LifeCycle * * 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
    ![사용자 할당](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
    ![예](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "예")

SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

