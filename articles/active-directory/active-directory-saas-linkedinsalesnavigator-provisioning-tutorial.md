---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Sales Navigator 구성 | Microsoft Docs"
description: "Tooconfigure Azure Active Directory tooautomatically 프로 비전 및 프로 비전 해제 사용자 tooLinkedIn Sales 탐색기를 계정 하는 방법에 대해 알아봅니다."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 LinkedIn Sales Navigator 구성


이 자습서의 hello 목표 tooshow tooperform LinkedIn Sales 탐색기와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooLinkedIn Sales 탐색기에에서 필요한 단계를 hello를입니다. 

## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트
*   LinkedIn Sales Navigator 테넌트 
*   액세스 toohello LinkedIn r e 계정 센터와 LinkedIn Sales 탐색 창에서 관리자 계정

> [!NOTE]
> Hello를 사용 하 여 LinkedIn Sales 탐색기와 azure Active Directory 통합 [SCIM](http://www.simplecloud.info/) 프로토콜입니다.

## <a name="assigning-users-toolinkedin-sales-navigator"></a>사용자가 tooLinkedIn Sales 탐색기 할당

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다. 

구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹을 tooLinkedIn Sales 탐색기에 액세스 해야 하는 hello 사용자를 나타내는 toodecide 필요 합니다. 결정, 여기 hello 지침에 따라 이러한 사용자 tooLinkedIn Sales 탐색기를 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a>사용자가 tooLinkedIn Sales 탐색기를 할당 하기 위한 중요 한 팁

*   것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooLinkedIn Sales 탐색기 tootest hello를 할당할 수 있습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

*   Hello를 선택 해야 사용자 tooLinkedIn Sales 탐색기에 할당할 때 **사용자** hello 할당 대화 상자에서 역할입니다. hello "기본 액세스" 역할 프로 비전 하기 위한 작동 하지 않습니다.


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a>사용자 프로비저닝 tooLinkedIn Sales 탐색기 구성

이 섹션 API를 프로 비전 하는 Azure AD tooLinkedIn Sales 탐색기 SCIM 사용자 계정 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성 업데이트 및 사용자에 따라 LinkedIn Sales 탐색 창에서 할당 된 사용자 계정 사용 안 함 및 Azure AD에서 그룹 할당을 추가 합니다.

> [!TIP]
> Hello 지침에 제공 된 LinkedIn Sales 탐색 창에 대 한 SAML 기반 Single Sign-on tooenabled 선택할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a>Sales 탐색기 tooLinkedIn Azure AD에서 프로 비전 tooconfigure 자동 사용자 계정:


hello 첫 번째 단계는 tooretrieve LinkedIn 액세스 토큰입니다. 엔터프라이즈 관리자인 경우 액세스 토큰을 자체 프로비전할 수 있습니다. 사용자 계정 센터에서 이동 너무**설정 &gt; 전역 설정** 및 열기 hello **SCIM 설치** 패널입니다.

> [!NOTE]
> 하지 않고 직접 링크를 통해 hello r e 계정 센터에 액세스 하는, 단계를 수행 하는 hello를 사용 하 여 도달할 수 있습니다.

1)  TooAccount 센터에 로그인 합니다.

2)  **관리 &gt; 관리 설정**을 선택합니다.

3)  클릭 **통합 고급** hello 왼쪽된 세로 막대에 있습니다. 방향이 지정 된 toohello r e 계정 센터 됩니다.

4)  클릭 **+ 새 SCIM 구성 추가** 각 필드에 입력 하 여 hello 절차에 따라 수행 합니다.

> 자동 할당 라이선스가 활성화되지 않으면 사용자 데이터만 동기화된 것입니다.

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> Autolicense 지정을 사용 하는 경우 toonote 응용 프로그램 인스턴스 및 라이선스 유형 필요 합니다. 첫 번째 돌아와에 라이선스가 할당 된, 모든 hello 라이선스는 수행 될 때까지 먼저 기반을 제공 합니다.

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  **토큰 생성**을 클릭합니다. Hello에서 액세스 토큰 디스플레이 표시 되어야 **액세스 토큰** 필드입니다.

6)  Hello 페이지에서 이동 하기 전에 토큰 tooyour 클립보드 액세스 또는 컴퓨터를 저장 합니다.

7) 다음으로 toohello 로그인 [Azure 포털](https://portal.azure.com), toohello 찾아보기 및 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

8) Single sign on LinkedIn Sales 탐색기를 이미 구성한 경우 hello 검색 필드를 사용 하 여 LinkedIn Sales 검색기의 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **LinkedIn Sales 탐색기** hello 응용 프로그램 갤러리에서 합니다. LinkedIn Sales 탐색기 hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

9)  LinkedIn Sales 탐색기 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

10) 집합 hello **프로 비전 모드** 너무**자동**합니다.

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  아래에 필드를 다음 hello 입력 **관리자 자격 증명** :

* Hello에 **테 넌 트 URL** 필드 https://api.linkedin.com를 입력 합니다.

* Hello에 **암호 토큰** 필드 1 단계에서 생성 한 hello 액세스 토큰을 입력 하 고 클릭 **연결 테스트** 합니다.

* 성공 알림을 포털의 hello upperright 쪽에 표시 됩니다.

12) 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.

13) **Save**를 클릭합니다. 

14) Hello에 **특성 매핑을** 섹션에서 Azure AD tooLinkedIn Sales 탐색기에서에서 동기화 되도록 하는 hello 사용자 및 그룹 특성을 검토 합니다. 특성으로 선택 된 hello 참고 **일치** 사용된 toomatch hello 사용자 계정 및 업데이트 작업에 대 한 LinkedIn Sales 탐색 창에서 그룹 속성이 됩니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

![LinkedIn Sales Navigator 프로비저닝](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello LinkedIn Sales 탐색기에서 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션

16) **Save**를 클릭합니다. 

모든 사용자 및/또는 tooLinkedIn Sales 탐색기 hello 사용자 및 그룹 섹션에서 할당 된 그룹의 hello 초기 동기화가 시작 됩니다. 초기 동기화 hello hello 서비스가 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform을 수행 하는 참고 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 LinkedIn Sales 탐색기 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.


## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-enterprise-apps-manage-provisioning.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
