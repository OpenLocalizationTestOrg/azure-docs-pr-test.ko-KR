---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Salesforce 샌드박스 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Salesforce Sandbox 구성

이 자습서의 hello 목표 tooshow tooperform Salesforce Sandbox와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooSalesforce 샌드박스에에서 필요한 단계를 hello를입니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트.
*   Salesforce Sandbox for Work 또는 Salesforce Sandbox for Education에 대한 유효한 테넌트가 있어야 합니다. 어느 서비스에나 평가판 계정을 사용할 수 있습니다.
*   팀 관리자 권한이 있는 Salesforce Sandbox의 사용자 계정.

## <a name="assigning-users-toosalesforce-sandbox"></a>사용자가 tooSalesforce 샌드박스를 할당합니다.

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.

하기 전에 구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 해야 toodecide 어떤 사용자 및/또는 Azure AD의 그룹을 tooyour Salesforce 샌드박스에 응용 프로그램에 액세스 해야 하는 hello 사용자를 나타냅니다. 결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Salesforce 샌드박스에 응용 프로그램을 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>사용자가 tooSalesforce 샌드박스를 할당 하기 위한 중요 한 팁

* 것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooSalesforce 샌드박스 tootest hello를 할당 합니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

* 사용자 tooSalesforce 샌드박스에 할당할 때 유효한 사용자 역할을 선택 해야 합니다. hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.

> [!NOTE]
> 이 응용 프로그램 프로 비전 프로세스를 사용자 지정 하는 경우는 hello 고객 tooselect 경우가 hello의 일환으로 Salesforce Sandbox에서 사용자 지정 역할을 가져옵니다.

## <a name="enable-automated-user-provisioning"></a>자동 사용자 프로비전 사용

이 섹션 API를 프로 비전 하는 Azure AD tooSalesforce 샌드박스 사용자 계정을 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello를 구성 하는 경우, 업데이트 하 고, 사용자 및 그룹에 따라 계정 Salesforce Sandbox에 할당 된 사용자를 사용 하지 않도록 설정 Azure AD에 할당 합니다.

>[!Tip]
>Hello 지침에 제공 된 Salesforce 샌드박스에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 자동 사용자 계정 프로 비전 합니다.

이 섹션의 hello 목적은 toooutline 어떻게 tooSalesforce 샌드박스 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

2. Single sign on 이미 Salesforce 샌드박스를 구성 하는 경우 Salesforce Sandbox hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Salesforce Sandbox** hello 응용 프로그램 갤러리에 있습니다. Salesforce Sandbox hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

3. Salesforce Sandbox의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

4. 집합 hello **프로 비전 모드** 너무**자동**합니다. 
    ![프로비전](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Hello에서 **관리자 자격 증명** 섹션에서 다음 구성 설정을 hello를 제공 합니다.
   
    a. Hello에 **관리자 사용자 이름** 텍스트 상자에 Salesforce 계정에 hello 이름 **시스템 관리자** 할당 Salesforce.com에 프로필입니다.
   
    b. Hello에 **관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.

6. tooget Salesforce Sandbox 보안 토큰에 새 탭을 열고 hello에 동일한 로그인 Salesforce Sandbox 관리자 계정. Hello 오른쪽 위 hello 페이지를 사용자 이름을 클릭 한 다음 클릭 **내 설정**합니다.

     ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "자동 사용자 프로비저닝 사용")
7. Hello 왼쪽된 탐색 창에서 클릭 **개인** tooexpand hello 관련된 섹션을 클릭 하 고 **Reset My Security Token**합니다.
  
    ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "자동 사용자 프로비저닝 사용")
8. Hello에 **Reset My Security Token** 페이지에서 hello **보안 토큰 재설정** 단추입니다.

    ![자동 사용자 프로비저닝 사용](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "자동 사용자 프로비저닝 사용")
9. 이 관리자 계정과 연결 된 hello 전자 메일 받은 편지함을 확인 합니다. Salesforce Sandbox.com hello 새 보안 토큰을 포함 하는 전자 메일을 찾습니다.
10. Hello 토큰, 이동 tooyour Azure AD 창을 복사 하 고 hello에 붙여 **소켓 토큰** 필드입니다.

11. Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Salesforce 샌드박스에 응용 프로그램을 연결할 수 있습니다.

12. Hello에 **알림 전자 메일** 필드에, 개인 또는 프로 비전 오류 알림을 수신 하 고 hello 확인란을 선택 해야 하는 그룹의 hello 전자 메일 주소를 입력 합니다.

13. **저장**을 클릭합니다.  
    
14.  Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooSalesforce 샌드박스 합니다.**

15. Hello에 **특성 매핑을** 섹션에서 Azure AD tooSalesforce 샌드박스에서에서 동기화 되는 hello 사용자 특성을 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 사용 되는 toomatch hello 사용자 계정 Salesforce Sandbox에 있습니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

16. tooenable hello Salesforce 샌드박스 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서

17. **저장**을 클릭합니다.


모든 사용자의 hello 초기 동기화를 시작 및/또는 그룹이 tooSalesforce hello 사용자 및 그룹 섹션에는 샌드박스 할당 hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Salesforce 샌드박스에 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

이제 테스트 계정을 만들 수 있습니다. Hello 계정이 되었습니다 tooverify 동기화 toosalesforce too20 분을 기다리십시오.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [Single Sign-On 구성](active-directory-saas-salesforcesandbox-tutorial.md)