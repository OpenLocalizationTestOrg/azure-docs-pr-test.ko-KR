---
title: "자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Cerner Central 구성 | Microsoft Docs"
description: "Azure Active Directory tooautomatically tooconfigure tooa 명단 Cerner 중에 사용자를 프로 비전 방법에 대해 알아봅니다."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Cerner Central 구성

이 자습서의 hello 목표 tooshow tooperform Cerner 중부와 Azure AD tooautomatically 프로 비전 및 프로 비전 해제에서 사용자 계정 Azure AD tooa 사용자 명단 Cerner 중앙에에 필요한 단계를 hello를입니다. 


## <a name="prerequisites"></a>필수 조건

이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.

*   Azure Active Directory 테넌트
*   Cerner Central 테넌트 

> [!NOTE]
> Hello를 사용 하 여 Cerner 중부와 azure Active Directory 통합 [SCIM](http://www.simplecloud.info/) 프로토콜입니다.

## <a name="assigning-users-toocerner-central"></a>사용자가 tooCerner 중앙 할당

Azure Active Directory는 사용자가 액세스 tooselected 앱 받아야 하는 "할당" toodetermine 이라는 개념을 사용 합니다. 자동 사용자 계정 프로 비전의 hello 컨텍스트에서 hello 사용자 및 그룹만 "할당 된" tooan 응용 프로그램이 Azure AD에서 동기화 됩니다. 

구성 하 고 서비스를 프로 비전 하는 hello를 사용 하도록 설정 하기 전에 어떤 사용자 및/또는 Azure AD의 그룹 나타내는 tooCerner 중앙 액세스 해야 하는 hello 사용자를 결정 해야 합니다. 결정, 이러한 사용자 tooCerner 중앙 여기 hello 지침에 따라 할당할 수 있습니다.

[사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>사용자가 tooCerner 중앙 할당 하는 데 중요 한 팁

*   것이 좋습니다는 단일 Azure AD 사용자 프로 비전 구성 tooCerner 중앙 tootest hello를 할당할 수 있습니다. 추가 사용자 및/또는 그룹은 나중에 할당할 수도 있습니다.

* 초기 테스트 한 명의 사용자에 대 한 완료 되 면 Cerner 중부 할당 hello 전체 목록은 사용자가 의도 한 tooaccess 모든 Cerner 솔루션 (뿐 아니라 Cerner 중부) 프로 비전 toobe tooCerner의 사용자 명단을 권장 합니다.  다른 Cerner 솔루션이이 목록은 hello 사용자 명단에 사용자가 활용합니다.

*   Hello를 선택 해야 사용자 tooCerner 중앙에 할당할 때 **사용자** hello 할당 대화 상자에서 역할입니다. Hello "기본 액세스" 역할의 사용자 프로 비전에서 제외 됩니다.


## <a name="configuring-user-provisioning-toocerner-central"></a>사용자 프로비저닝 tooCerner 중앙 구성

이 섹션 API를 프로 비전 Cerner의 SCIM 사용자 계정을 사용 하 여 Azure AD tooCerner 중앙 사용자 명단 연결 하는 방법을 안내 하 고 서비스 toocreate 프로 비전 하는 hello 구성, 업데이트 하 고, Cerner 중앙에서 계정을 기반으로 할당 된 사용자를 사용 하지 않도록 설정 Azure AD에서 사용자 및 그룹 할당 합니다.

> [!TIP]
> [Azure 포털 (https://portal.azure.com)에서 제공 하는 hello 지침 Cerner Central에 대 한 SAML 기반 Single Sign-on tooenabled를 선택할 수도 있습니다. Single Sign-On은 자동 프로비전과 별개로 구성할 수 있습니다. 하지만 이 두 가지 기능은 서로 보완적입니다. 자세한 내용은 참조 hello [대 로그온 단일 자습서 Cerner 중부](active-directory-saas-cernercentral-tutorial.md)합니다.


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>tooCerner 중 Azure AD에서 프로 비전 tooconfigure 자동 사용자 계정:


순서 tooprovision 사용자 계정 tooCerner 중부 toorequest Cerner 중부 시스템 계정, Cerner에서 필요 하 고 Azure AD tooconnect tooCerner SCIM 끝점을 사용할 수 있는 OAuth 전달자 토큰을 생성 합니다. 또한 tooproduction를 배포 하기 전에 hello 통합 Cerner 샌드박스 환경에서 수행 될 것이 좋습니다.

1.  hello 첫 번째 단계는 hello Cerner 관리 tooensure hello 사람 있고 Azure AD 통합 필요한 tooaccess hello 문서 필요한 toocomplete hello 지침 CernerCare 계정. 필요한 경우 각 해당 환경에 toocreate CernerCare 계정 아래 hello Url을 사용 합니다.

   * 샌드박스: https://sandboxcernercare.com/accounts/create

   * 프로덕션: https://cernercare.com/accounts/create  

2.  다음으로 Azure AD에 대해 시스템 계정을 만들어야 합니다. 샌드박스 및 프로덕션 환경에 대 한 시스템 계정 toorequest 아래 hello 지침을 사용 합니다.

   * 지침: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * 샌드박스: https://sandboxcernercentral.com/system-accounts/

   * 프로덕션: https://cernercentral.com/system-accounts/

3.  다음으로 각 시스템 계정에 대해 OAuth 전달자 토큰을 생성합니다. toodo,이 따라 hello 지침은 다음과 같습니다.

   * 지침: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * 샌드박스: https://sandboxcernercentral.com/system-accounts/

   * 프로덕션: https://cernercentral.com/system-accounts/

4. 마지막으로 tooacquire 사용자 명단 영역 Id Cerner toocomplete hello 구성에서 두 hello 샌드박스 및 프로덕션 환경에 대 한 필요 합니다. 방법에 대 한 내용은 tooacquire이,이 참조: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM 합니다. 

5. 이제 Azure AD tooprovision 사용자 계정 tooCerner를 구성할 수 있습니다. Toohello 로그인 [Azure 포털](https://portal.azure.com), toohello 찾아보기 및 **Azure Active Directory > 엔터프라이즈 앱 > 모든 응용 프로그램** 섹션.

6. Single sign on Cerner 중부를 이미 구성한 경우 hello 검색 필드를 사용 하 여 Cerner 중앙 사이트의 인스턴스에 대 한 검색 합니다. 그렇지 않은 경우 선택 **추가** 검색 한 **Cerner 중앙** hello 응용 프로그램 갤러리에 있습니다. Cerner 중앙 hello 검색 결과에서 선택한 응용 프로그램의 tooyour 목록을 추가 합니다.

7.  Cerner 중앙 사이트의 인스턴스를 선택 하 고 hello 선택 **프로 비전** 탭 합니다.

8.  집합 hello **프로 비전 모드** 너무**자동**합니다.

   ![Cerner Central 프로비저닝](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  아래에 필드를 다음 hello 입력 **관리자 자격 증명**:

   * Hello에 **테 넌 트 URL** 필드 #4 단계에서 복사한 hello 영역 ID "사용자-명단-영역-ID" 바꿉니다 아래 hello 형식의 URL을 입력 합니다.

> 샌드박스: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> 프로덕션: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * Hello에 **암호 토큰** 필드 3 단계에서 생성 된 hello OAuth 전달자 토큰을 입력 하 고 클릭 **연결 테스트**합니다.

   * 성공 알림을 포털의 hello upperright 쪽에 표시 됩니다.

10. 개인 이나 hello에 프로 비전 오류 알림의 받을 그룹의 hello 전자 메일 주소를 입력 **알림 전자 메일** 필드 및 hello 확인란 아래를 확인 합니다.

11. **Save**를 클릭합니다. 

12. Hello에 **특성 매핑을** 섹션에서 hello 사용자 및 그룹 특성 toobe Azure AD tooCerner 중부에서에서 동기화를 검토 합니다. 특성으로 선택 된 hello **일치** 속성은 사용 되는 toomatch hello 사용자 계정 및 업데이트 작업에 대 한 Cerner 중앙의 그룹입니다. 변경 내용을 저장 단추 toocommit hello를 선택 합니다.

13. tooenable hello Cerner Central 변경 hello에 대 한 Azure AD 프로 비전 서비스 **프로 비전 상태** 너무**에** hello에 **설정을** 섹션

14. **Save**를 클릭합니다. 

모든 사용자의 hello 초기 동기화가 시작 및/또는 그룹이 할당 tooCerner hello 사용자 및 그룹 섹션에서 중부 hello 초기 동기화는 hello Azure AD에 프로 비전 서비스에서 실행 되 고으로 약 20 분 마다 발생 하는 후속 동기화 보다 더 긴 tooperform 합니다. Hello를 사용할 수 있습니다 **동기화 세부 정보와** toomonitor 진행률 섹션 및 Cerner 중앙 응용 프로그램에서 서비스를 프로 비전 하는 hello에서 수행 하는 모든 작업을 설명 하는 링크 tooprovisioning 작업 보고서를 따릅니다.

Hello Azure AD에 프로 비전 tooread 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자동 사용자 계정 프로 비전에 대 한 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.

## <a name="additional-resources"></a>추가 리소스

* [Cerner Central: Azure AD를 사용하여 ID 데이터 게시](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [자습서: Azure Active Directory를 사용한 Single Sign-On에 대한 Cerner Central 구성](active-directory-saas-cernercentral-tutorial.md)
* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](active-directory-enterprise-apps-manage-provisioning.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>다음 단계
* [Tooreview 기록 하는 방법을 자세히 알아보고 get를 프로 비전 활동 보고](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)합니다.
