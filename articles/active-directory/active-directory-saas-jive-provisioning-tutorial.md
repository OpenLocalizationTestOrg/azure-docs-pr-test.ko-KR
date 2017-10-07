---
title: "자습서: Jive와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Jive 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>자습서: 사용자 프로비전에 대한 Jive 구성

이 자습서의 hello 목표 tooshow tooperform Jive와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooJive에에서 필요한 단계를 hello를입니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트.
*   Jive Single Sign-On이 설정된 구독
*   팀 관리자 권한이 있는 Jive의 사용자 계정

## <a name="assigning-users-toojive"></a>사용자가 tooJive 할당

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.

하기 전에 구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 해야 toodecide 어떤 사용자 및/또는 Azure AD의 그룹을 tooyour Jive 응용 프로그램에 액세스 해야 하는 hello 사용자를 나타냅니다. 결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Jive 응용 프로그램을 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>사용자가 tooJive 할당 하는 데 중요 한 팁

*   것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooJive tootest hello를 할당할 수 있습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*   사용자 tooJive에 할당할 때 유효한 사용자 역할을 선택 해야 합니다. hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.

## <a name="enable-user-provisioning"></a>사용자 프로비저닝 사용

이 섹션 API를 프로 비전 하는 Azure AD tooJive의 사용자 계정을 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, Azure AD에서 사용자 및 그룹 할당을 기준으로 Jive에서 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.

> [!TIP]
> SAML 기반 Single Sign-on hello 지침에 제공 된 Jive에 대 한 tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure 사용자 계정 프로 비전 합니다.

이 섹션의 hello 목적은 toooutline 어떻게 tooJive 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.
이 절차의 일부로 toorequest Jive.com에서 필요한 사용자 보안 토큰이 필요한 tooprovide 됩니다.

1. Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

2. Jive hello 검색 필드를 사용 하 여 인스턴스에 대 한 single sign on Jive를 이미 구성한 경우를 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Jive** hello 응용 프로그램 갤러리에 있습니다. Jive hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

3. Jive, 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

4. 집합 hello **프로 비전 모드** 너무**자동**합니다. 

    ![프로비전](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. Hello에서 **관리자 자격 증명** 섹션에서 다음 구성 설정을 hello를 제공 합니다.
   
    a. Hello에 **Jive 관리자 사용자 이름** 텍스트 상자에 Jive 계정 hello에 이름을 **시스템 관리자에 게** 할당 Jive.com에서 프로필입니다.
   
    b. Hello에 **Jive 관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.
   
    c. Hello에 **Jive 테 넌 트 URL** textbox hello Jive 테 넌 트 URL 입력 합니다.
      
      > [!NOTE]
      > hello Jive 테 넌 트 URL은 사용자 조직 toolog tooJive에 의해 사용 되는 URL입니다.  
      > 일반적으로 hello URL은 형식에 따라 hello: **www.\< 조직\>. jive.com**합니다.          

6. Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Jive 응용 프로그램을 연결할 수 있습니다.

7. 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.

8. **저장**을 클릭합니다.

9. Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooJive 합니다.**

10. Hello에 **특성 매핑을** 섹션에서 Azure AD tooJive에서 동기화 되는 hello 사용자 특성을 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Jive에서 되는 사용 되는 toomatch hello 사용자 계정입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

11. tooenable hello Jive, 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서

12. **저장**을 클릭합니다.

모든 사용자 및/또는 tooJive에 hello 사용자 및 그룹 섹션에 할당 된 그룹의 hello 초기 동기화를 시작 합니다. hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Jive 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

이제 테스트 계정을 만들 수 있습니다. Hello 계정이 되었습니다 tooverify 동기화 tooJive too20 분을 기다리십시오.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [Single Sign-On 구성](active-directory-saas-jive-tutorial.md)