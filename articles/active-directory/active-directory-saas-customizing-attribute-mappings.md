---
title: "Azure AD 특성 매핑 aaaCustomizing | Microsoft Docs"
description: "Azure Active Directory에서 SaaS 응용 프로그램에 대 한 어떤 특성 매핑을 수정 하는 방법으로 tooaddress 비즈니스 되는지 알아보세요 필요 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정
Microsoft Azure AD는 Salesforce, Google Apps 등 toothird 타사 SaaS 응용 프로그램을 프로 비전 하는 사용자에 대 한 지원을 제공 합니다. Hello Azure 관리 포털에서 "특성 매핑" 이라고 하는 구성의 형태로 해당 특성 값을 제어 타사 SaaS 응용 프로그램 사용에 대 한 프로 비전 하는 사용자를 설정한 경우

Azure AD 사용자 개체와 각 SaaS 앱의 사용자 개체 사이에는 미리 구성된 특성 세트가 있습니다. 일부 앱은 그룹이나 연락처 같은 다른 유형의 개체를 관리합니다. <br> 
 Tooyour 비즈니스 요구에 따라 hello 기본 특성 매핑을 사용자 지정할 수 있습니다. 즉, 기존의 특성 매핑을 변경 또는 삭제하거나 새 특성 매핑을 만들 수 있습니다.

Hello Azure AD 포털에서을 클릭 하 여이 기능에 액세스할 수 있습니다는 **매핑** 에 속하는 구성 **프로 비전** hello에 **관리** 섹션은  **엔터프라이즈 응용 프로그램**합니다.


![Salesforce][5] 

클릭 하는 **매핑** 구성 관련 hello 열립니다 **특성 매핑** 블레이드입니다.  
올바르게 SaaS 응용 프로그램 toofunction에 필요한 특성 매핑이 있습니다. 필수 특성에 대 한 hello **삭제** 기능은 사용할 수 없습니다.


![Salesforce][6]  

위의 hello 예제에서 해당 hello를 볼 수 있습니다 **Username** Salesforce에서 관리 되는 개체의 특성은 hello로 채워집니다 **userPrincipalName** hello의 값이 Azure Active Directory 개체 연결.

매핑을 클릭하여 기존 **특성 매핑**을 사용자 지정할 수 있습니다. Hello 열립니다 **특성 편집** 블레이드입니다.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>특성 매핑 유형 이해
특성 매핑으로 타사 SaaS 응용 프로그램에서 특성이 채워지는 법을 제어합니다. 4 가지의 다른 매핑 형식이 지원됩니다.

* **직접** – hello 대상 특성은 Azure AD에서 hello hello 연결된 개체의 특성 값으로 채워집니다.
* **상수** – hello 대상 특성이 지정한 특정 문자열로 채워집니다.
* **식** -hello 대상 특성이 스크립트와 유사한 식의 hello 결과에 따라 채워집니다. 
  자세한 내용은 [Azure Active Directory의 특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)을 참조하세요.
* **None** -hello 대상 특성을 두면 수정 되지 않은 합니다. 그러나 hello 대상 특성이 비어 있으면 지정 하는 hello 기본 값으로 채워집니다.

사용자 지정 특성 매핑을 추가 toothese 4 기본 특성 매핑 형식에 선택적 hello 개념을 지원 **기본** 값 할당 합니다. hello 기본 값 할당을 사용 하면 Azure AD 디렉터리 또는 hello 대상 개체에 두 값이 있는 경우 대상 특성 값으로 채워집니다. hello 가장 일반적인 구성은 빈 tooleave 합니다.


## <a name="understanding-attribute-mapping-properties"></a>특성 매핑 속성 이해

Hello 이전 섹션에서 도입 된 toohello 특성 매핑 유형 속성 이미 있습니다.
또한 toothis 속성에 특성 매핑을 특성 뒤 hello를 지원도 않습니다.

- **원본 특성** -hello 원본 시스템의 hello 사용자 특성 (예:: Azure Active Directory).
- **대상 특성** – hello 대상 시스템에 hello 사용자 특성 (예:: ServiceNow).
- **이 특성을 사용 하 여 개체를 일치** 이 매핑을 사용할지 여부-toouniquely hello 소스 및 대상 시스템 간에 사용자를 식별 합니다. 이 속성은 일반적으로 hello userPrincipalName에 설정 됩니다 또는 일반적으로 Azure AD의 메일 특성 tooa 사용자 이름 필드는 대상 응용 프로그램에 매핑됩니다.
- **일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다. 여러 개 있는,이 필드에 정의 된 hello 순서로 평가 됩니다. 일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.
- **이 매핑 적용**
    - **항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.
    - **만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.


## <a name="what-you-should-know"></a>알아야 할 사항

Microsoft Azure AD는 동기화 프로세스의 효과적인 구현을 제공합니다. 초기화된 환경에서 동기화 주기 중에는 업데이트가 필요한 개체만 처리됩니다. 동기화 주기의 hello 성능에 영향이 특성 매핑을 업데이트 합니다. 업데이트 toohello 특성 매핑 구성을 다시 평가 하는 모든 관리 되는 개체 toobe가 필요 합니다. 것은 권장 모범 사례 tookeep hello 최소한 연속 된 변경 tooyour 특성 매핑입니다.

## <a name="next-steps"></a>다음 단계

* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [사용자 프로 비전/프로 비전 해제 tooSaaS 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [사용자 프로 비전에 대 한 필터 범위 지정](active-directory-saas-scoping-filters.md)
* [SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여](active-directory-scim-provisioning.md)
* [계정 프로비전 알림](active-directory-saas-account-provisioning-notifications.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

