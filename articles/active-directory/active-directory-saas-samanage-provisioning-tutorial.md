---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Samanage 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooSamanage를 계정 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Samanage 구성


이 자습서의 hello 목표 tooshow tooperform Samanage와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooSamanage에에서 필요한 단계를 hello를입니다. 

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트
*   Hello로 Samanage 테 넌 트 [전문 계획](https://www.samanage.com/pricing/) 또는 더 잘 사용 하도록 설정 
*   관리자 권한이 있는 Samanage의 사용자 계정 

> [!NOTE]
> hello 통합 프로 비전 하는 Azure AD에 의존 hello [Samanage REST API](https://www.samanage.com/api/), Professional hello에 사용할 수 있는 tooSamanage 팀은 계획 이상의 합니다.

## <a name="assigning-users-toosamanage"></a>사용자가 tooSamanage 할당

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다. 

구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 tooyour Samanage 응용 프로그램에 액세스 해야 하는 Azure AD 나타내는 hello 사용자의 그룹 toodecide 필요 합니다. 결정, 여기 hello 지침에 따라 이러한 사용자 tooyour Samanage 응용 프로그램을 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a>사용자가 tooSamanage 할당 하는 데 중요 한 팁

*   것이 좋습니다는 단일 Azure AD 사용자가 프로 비전 구성 tooSamanage tootest hello를 할당 합니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*   Hello 중 하나를 선택 해야 사용자 tooSamanage에 할당할 때 **사용자** 역할 또는 다른 유효한 응용 프로그램 관련 역할 (있는 경우) hello 할당 대화 상자에서. hello **기본 액세스** 역할 프로 비전을 사용할 수 없습니다 및 이러한 사용자는 건너뜁니다.

> [!NOTE]
> 추가 된 기능으로 서비스를 프로 비전 하는 hello Samanage에 정의 된 사용자 정의 역할 읽고 hello 역할 선택 대화 상자에서 선택할 수 있습니다 위치 하는 Azure AD로 가져옵니다. 이러한 역할 서비스를 프로 비전 하는 hello 사용 하도록 설정 하 고 하나의 동기화 주기가 완료 후 hello Azure 포털에에서 표시 됩니다.

## <a name="configuring-user-provisioning-toosamanage"></a>사용자 tooSamanage 프로 비전 구성 

이 섹션 API를 프로 비전 하는 Azure AD tooSamanage의 사용자 계정을 연결 하는 방법을 안내 하 고 업데이트 hello 서비스 toocreate 프로 비전, 구성 및 Azure AD에서 사용자 및 그룹 할당을 기준으로 Samanage에 할당 된 사용자 계정을 사용 하지 않도록 설정 합니다.

> [!TIP]
> 제공 하는 hello 지침 Samanage에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a>자동 사용자 계정 tooSamanage Azure AD에서 프로 비전 구성 합니다.


1. Hello에 [Azure 포털](https://portal.azure.com), toohello 찾아보기 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

2. Single sign on Samanage를 이미 구성한 경우 Samanage hello 검색 필드를 사용 하 여 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Samanage** hello 응용 프로그램 갤러리에 있습니다. Samanage hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

3. Samanage의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

4. 집합 hello **프로 비전 모드** 너무**자동**합니다.

    ![Samanage 프로비전](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. Hello에서 **관리자 자격 증명** 섹션, 입력된 hello **관리자 사용자 이름 및 관리자 암호** Samanage의 계정입니다. 

6. Hello Azure 포털에서에서 클릭 **연결 테스트** tooensure Azure AD tooyour Samanage 응용 프로그램을 연결할 수 있습니다. Hello 연결에 실패 하면 Samanage 계정에 관리자 권한이 있는지 확인 하 고 5 단계를 다시 시도 하십시오.

7. 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 검사 hello 확인란 "보내기" 전자 메일 알림을 오류가 발생 합니다.

8. **Save**를 클릭합니다. 

9. Hello 매핑 섹션에서 선택 **동기화 Azure Active Directory 사용자 tooSamanage**합니다.

10. Hello에 **특성 매핑을** 섹션에서 Azure AD tooSamanage에서 동기화 되는 hello 사용자 특성을 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 업데이트 작업에 대 한 사용 되는 toomatch hello 사용자 계정을 Samanage에 있습니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

11. tooenable hello 변경 hello Samanage에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션

12. **Save**를 클릭합니다. 

이 작업의 모든 사용자 및/또는 tooSamanage에 hello 사용자 및 그룹 섹션에 할당 된 그룹 hello 초기 동기화를 시작 합니다. hello 초기 동기화는 hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.


## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-enterprise-apps-manage-provisioning.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>다음 단계

* [Tooreview 기록 하는 방법을 알아보고 프로 비전 활동에 대 한 보고서](active-directory-saas-provisioning-reporting.md)
