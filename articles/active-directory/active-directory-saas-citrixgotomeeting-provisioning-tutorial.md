---
title: "자습서: Citrix GoToMeeting과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Citrix GoToMeeting 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Citrix GoToMeeting 구성

hello이이 자습서의 단계에서 Citrix GoToMeeting와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooCitrix GoToMeeting tooperform 필요한 hello tooshow가 합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트.
*   Citrix GoToMeeting Single Sign-On이 설정된 구독.
*   팀 관리자 권한이 있는 Citrix GoToMeeting의 사용자 계정.

## <a name="assigning-users-toocitrix-gotomeeting"></a>사용자가 tooCitrix GoToMeeting 할당

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다.

하기 전에 구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 해야 toodecide 어떤 사용자 및/또는 Azure AD의 그룹을 tooyour Citrix GoToMeeting 응용 프로그램에 액세스 해야 하는 hello 사용자를 나타냅니다. 결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Citrix GoToMeeting 응용 프로그램을 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>사용자가 tooCitrix GoToMeeting 할당 하는 데 중요 한 팁

*   것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooCitrix GoToMeeting tootest hello를 할당 합니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*   사용자 tooCitrix GoToMeeting에 할당할 때 유효한 사용자 역할을 선택 해야 합니다. hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.

## <a name="enable-automated-user-provisioning"></a>자동 사용자 프로비전 사용

이 섹션 API를 프로 비전 하는 Azure AD tooCitrix GoToMeeting 사용자 계정을 연결 하는 방법을 안내 하 고 hello 서비스 toocreate 프로 비전을 구성, 업데이트 하 고, 사용자 및 그룹에 따라 계정 Citrix GoToMeeting에 할당 된 사용자를 사용 하지 않도록 설정 Azure AD에 할당 합니다.

> [!TIP]
> Hello 지침에 제공 되는 Citrix GoToMeeting에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure 자동 사용자 계정 프로 비전 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

2. Single sign on Citrix GoToMeeting를 이미 구성한 경우 Citrix GoToMeeting hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Citrix GoToMeeting** hello 응용 프로그램 갤러리에 있습니다. Citrix GoToMeeting hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

3. Citrix GoToMeeting의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

4. 집합 hello **프로 비전** 모드 너무**자동**합니다. 

    ![프로비전](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. Hello 관리자 자격 증명 섹션에서 단계를 수행 하는 hello를 수행 합니다.
   
    a. Hello에 **Citrix GoToMeeting 관리자 사용자 이름** textbox hello 관리자의 사용자 이름 입력 합니다.

    b. Hello에 **Citrix GoToMeeting 관리자 암호** hello 관리자의 암호 텍스트입니다.

6. Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Citrix GoToMeeting 응용 프로그램을 연결할 수 있습니다. Hello 연결이 실패 하는 경우 Citrix GoToMeeting 계정이 팀 관리자 권한을 확인 하 고 hello 시도 **"관리자 자격 증명"** 다시 합니다.

7. 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란을 선택 합니다.

8. **저장**을 클릭합니다.

9. Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooCitrix GoToMeeting 합니다.**

10. Hello에 **특성 매핑을** 섹션에서 Azure AD tooCitrix GoToMeeting에서에서 동기화 되는 hello 사용자 특성을 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 Citrix GoToMeeting에서 되는 사용 되는 toomatch hello 사용자 계정입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

11. tooenable hello 변경 hello, Citrix GoToMeeting에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello 설정 섹션에서

12. **저장**을 클릭합니다.

모든 사용자의 hello 초기 동기화를 시작 및/또는 그룹이 tooCitrix GoToMeeting hello 사용자 및 그룹 섹션에서 할당 hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Citrix GoToMeeting 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-saas-tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [Single Sign-On 구성](active-directory-saas-citrix-gotomeeting-tutorial.md)


