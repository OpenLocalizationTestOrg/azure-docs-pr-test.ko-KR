---
title: "범위 지정 필터를 사용한 aaaProvisioning 앱 | Microsoft Docs"
description: "Toouse 범위를 지정 하는 자동화 된 사용자가 실제로 프로 비전 되는 개체는 비즈니스 요구 사항을 충족 하지 않는 경우 프로 비전을 지 원하는 응용 프로그램의 tooprevent 개체를 필터링 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>범위 지정 필터를 사용한 특성 기반 응용 프로그램 프로비전
이 섹션의 hello 목표 toohello 응용 프로그램 사용자를 프로 비전 tooexplain toouse 범위 지정 있는 사용자를 결정 하는 toodefine 특성 기반 규칙을 필터링 하는 방법입니다.

## <a name="clauses-and-scope-groups"></a>절 및 범위 그룹
![범위 지정 필터][1] 

범위 지정 필터는 하나 이상의 **그룹 범위**에 의해 정의되며, 각 그룹 범위는 하나 이상의 **절**을 유지하고 있습니다. 특정 범위 그룹에 대 한 toosee hello 절 hello 그룹 이름의 hello 화살표 toohello 왼쪽을 클릭 하 여 확장 합니다.

A **절** hello 각 사용자의 특성을 평가 하 여 범위 지정 필터를 통해 toopass 수 있는 사용자를 결정 합니다. 예를 들어 할 수 있습니다 요구 하는 하나 이상의 절 사용자의 'state' 특성 같은 뉴욕 하므로 뉴욕 사용자만 hello 응용 프로그램에 프로 비전 됩니다.

![범위 지정 그룹 이름][2] 

각 **범위 그룹** 시작 하 고 하나의 필수 **절**또한 위의 스크린 샷에서 hello에 나타난 것 처럼 합니다. 이 절은 단순히 해당 hello 사용자 할당 해야 toohello 응용 프로그램 범위 지정 필터를 여 평가 되기 전에 상태입니다. 이 절은 삭제하거나 수정할 수 없습니다.

Hello 적절 한 단추를 눌러 새 절 이나 새 범위 그룹을 추가할 수 있습니다. **범위 그룹 이름** 속성을 편집하여 각 범위 그룹에 이름을 지정할 수 있습니다.

## <a name="how-scoping-filters-are-evaluated"></a>범위 지정 필터 평가 방법
프로 비전 하는 동안 해당 사용자 기울이게 toohello 응용 프로그램 액세스 하는 경우 범위 지정 필터 toodetermine 프로그램에 대해 할당 된 모든 사용자 테스트. 각 절 필터링 되지 hello 사용자 tooavoid는 순서로 전달 되어야 하는 테스트로 생각할 수 있습니다. 

여러 범위 그룹이 정의 되어 있는 경우 각 사용자 통과 해야 tooaccess 그 중 하나 이상 hello 응용 프로그램입니다. 그러나 각 범위 그룹 내에서 hello 사용자 전달 해야 모든 절 toopass가 특정 범위 그룹입니다. 

즉, 범위 그룹 것으로 생각할 수 있습니다 또는 연산 하 고 있는 것으로 그 안에서 hello 절 생각할 수 있습니다 AND 결합 됩니다. 예를 들어 아래 필터 범위를 지정 하는 hello:

![범위 지정 그룹 이름][3]  

Toothis 범위 지정 필터에 따라, 사용자가 충족 해야 합니다 hello 다음 기준, 사용자를 프로 비전 toobe:

1. Toohello 응용 프로그램을 할당 되어야 합니다.
2. Hello 엔지니어링 부서에서 근무 해야 합니다.
3. 샌프란시스코 또는 캐나다에서 근무해야 합니다.

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [사용자 프로 비전 및 프로 비전 해제 tooSaaS 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [사용자 프로비저닝에 대한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)
* [특성 매핑에 대한 식 작성](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [계정 프로비전 알림](active-directory-saas-account-provisioning-notifications.md)
* [SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여](active-directory-scim-provisioning.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
