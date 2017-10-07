---
title: "자습서: Qualtrics와 Azure Active Directory 통합 | Microsoft Docs"
description: "어떻게 tooenable Azure Active Directory와 Qualtrics toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>자습서: Qualtrics와 Azure Active Directory 통합
hello이이 자습서는 Azure와 Qualtrics tooshow hello 통합 합니다.  

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

* 유효한 Azure 구독
* Qualtrics SSO(Single Sign-On)가 설정된 구독

이 자습서를 완료 한 후 hello Azure AD 사용자 tooQualtrics 배정 됩니다 Qualtrics 회사 사이트 (서비스 공급자에서 시작 된 로그온)에서 또는 hello를 사용 하 여 hello 응용 프로그램에 수 toosingle 로그인 [toohello 소개 액세스 패널](active-directory-saas-access-panel-introduction.md)합니다.

이 자습서에 설명 된 hello 시나리오 hello 빌딩 블록을 다음으로 구성 됩니다.

1. Qualtrics에 대 한 hello 응용 프로그램 통합 사용
2. SSO(Single Sign-On) 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "시나리오")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Qualtrics에 대 한 hello 응용 프로그램 통합 사용
hello이이 섹션의 목적은 toooutline 어떻게 Qualtrics에 tooenable hello 응용 프로그램 통합 합니다.

**tooenable hello 응용 프로그램 통합을 Qualtrics에 대 한 hello 다음 단계를 수행 합니다.**

1. Hello hello 왼쪽된 탐색 창에서 Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.
3. tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.
   
   ![응용 프로그램](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "응용 프로그램")
4. 클릭 **추가** hello hello 페이지 맨 아래에 있습니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "응용 프로그램 추가")
5. Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. Hello에 **검색 상자**, 형식 **Qualtrics**합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "응용 프로그램 갤러리")
7. Hello 결과 창에서 선택 **Qualtrics**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Single Sign-On 구성

hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooQualtrics hello SAML 프로토콜에 따라 하는 방법입니다.

**tooconfigure 단일 로그온 hello 다음 단계를 수행 하십시오.**

1. Hello hello에 Azure 클래식 포털에서에서 **Qualtrics** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Single Sign-On 구성")
2. Hello에 **어떻게 tooQualtrics에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Single Sign-On 구성")
3. Hello에 **앱 URL 구성** 페이지 hello에서 **Qualtrics 로그온 URL** 텍스트 상자에 URL (예:: "*https://ssotest2ut1.qualtrics.com*"), 클릭하고**다음**합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "앱 URL 구성")
4. Hello에 **Qualtrics에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Single Sign-On 구성")
5. Hello 메타 데이터 파일 toohello Qualtrics 지원 팀에 보냅니다.
   
   >[!NOTE]
   >hello SSO 구성에 toobe hello Qualtrics 지원 팀에서 수행 합니다. Hello 구성이 완료 되는 즉시 알림을 받아볼 수 있습니다.
   > 
   > 
6. Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.
   
   ![Single Sign-On 구성](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Single Sign-On 구성")
   
## <a name="configure-user-provisioning"></a>사용자 프로비전 구성

사용자에 대 한 있습니다 tooconfigure tooQualtrics 프로 비전 작업 항목이 없습니다. Toolog hello 액세스 패널을 사용 하 여 Qualtrics에 시도 하는 할당된 된 사용자, Qualtrics hello 사용자의 존재 여부를 확인 합니다.  

사용할 수 있는 사용자 계정이 없으면 자동으로 Qualtrics에 의해 생성됩니다.

## <a name="assign-users"></a>사용자 할당
tootest 구성에 tooallow 할당 하 여 응용 프로그램 액세스 tooit를 사용 하 여 원하는 toogrant hello Azure AD 사용자가 필요 합니다.

**tooassign 사용자 tooQualtrics hello 다음 단계를 수행 합니다.**

1. Azure 클래식 포털 hello 테스트 계정을 만듭니다.
2. Hello에 **Qualtrics** 응용 프로그램 통합 페이지에서 클릭 **사용자 할당**합니다.
   
   ![사용자 할당](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "사용자 할당")
3. 테스트 사용자 선택, 클릭 **할당**, 클릭 하 고 **예** tooconfirm 할당 합니다.
   
   ![예](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "예")

SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다. 액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.

