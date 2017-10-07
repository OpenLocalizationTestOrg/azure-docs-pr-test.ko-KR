---
title: "Azure Active Directory에서 aaaAssign 라이선스 tooa 그룹 | Microsoft Docs"
description: "Azure Active Directory 그룹 라이선스를 사용 하 여 tooassign toousers 허가 하는 방법"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Azure Active Directory 그룹 멤버 자격을 통해 toousers 라이선스를 할당 합니다.

이 문서는 Azure Active Directory (Azure AD)에 있는 사용자의 제품 라이선스 tooa 그룹을 할당 하 고 올바르게 허가 하는 다음 확인을 통해 보여 줍니다.

이 예제에서는 hello 테 넌 트에 라는 보안 그룹이 **HR 부서**합니다. 이 그룹 hello 인사 관리 부서의 (약 1000 명의 사용자)의 모든 멤버를 포함합니다. Office 365 Enterprise E3 tooassign 라이선스 toohello 전체 부서를 사용 하는 것이 좋습니다. hello hello 제품에 포함 된 Yammer 엔터프라이즈 서비스 hello 부서 준비 toostart 사용 될 때까지 일시적으로 비활성화 해야 합니다. 시겠습니까 toodeploy Enterprise Mobility + 보안 라이선스 toohello 동일한 사용자 그룹을 합니다.

> [!NOTE]
> 일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다. Tooa 사용자 라이선스를 할당할 수 있습니다, 전에 관리자에 게에 hello 사용자에 toospecify hello 사용 위치 속성이 있습니다.

> 그룹 라이선스 할당에 대 한 사용 위치를 지정 하지 않고 모든 사용자는 hello 디렉터리의 hello 위치를 상속 합니다. 사용자가 여러 위치에 있으면 항상 설정 하 사용 위치 사용자 만들기 흐름의 일환으로 사용자가 받지 않음 및 라이선스 할당의 hello 결과 올바른 항상 방법을 사용 하면 (예를 들어 통해 AAD Connect 구성)-Azure ad에서는 것이 좋습니다. 허용 되지 않는 위치에 있는 서비스입니다.

## <a name="step-1-assign-hello-required-licenses"></a>1 단계: hello 필요한 라이선스를 할당 합니다.

1. Toohello 로그인 [ **Azure 포털** ](https://portal.azure.com) 관리자 계정으로 합니다. 라이선스 toomanage hello 계정에는 전역 관리자 역할 또는 사용자 계정 관리자 여야 합니다.

2. 선택 **더 많은 서비스** 에 hello 왼쪽된 탐색 창에서 선택한 후 **Azure Active Directory**합니다. 이 블레이드 tooFavorites를 추가 하거나 toohello 포털 대시보드에 고정할 수 있습니다.

3. Hello에 **Azure Active Directory** 블레이드를 **라이선스**합니다. 참조 하 고 hello 테 넌 트의 모든 라이선스 대상 제품을 관리할 수 있는 블레이드가 열립니다.

4. 아래 **모든 제품**, Office 365 Enterprise E3 Enterprise Mobility + 보안 hello 제품 이름을 선택 하 여 선택 합니다. 선택 toostart hello 할당 **할당** hello hello 블레이드 위쪽에 있습니다.

   ![모든 제품, 라이선스 할당](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. Hello에 **할당 라이선스** 블레이드에서 클릭 **사용자 및 그룹** tooopen hello **사용자 및 그룹** 블레이드입니다. Hello 그룹 이름에 대해 *HR 부서*hello 그룹을 선택한 다음 클릭 하 여 있는지 tooconfirm 수 **선택** hello hello 블레이드 맨 아래에 있습니다.

   ![그룹 선택](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. Hello에 **할당 라이선스** 블레이드에서 클릭 **할당 옵션 (선택 사항)**, 이전에 선택 된 두 제품 hello에 포함할 모든 서비스 계획을 표시 하는 합니다. 찾을 **Yammer 엔터프라이즈** 위쪽과 **오프** hello 제품 라이선스에서 서비스 toodisable 합니다. 클릭 하 여 확인 **확인** hello 맨 아래에 **할당 옵션**합니다.

   ![할당 옵션](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. hello에 toocomplete hello 할당 **할당 라이선스** 블레이드에서 클릭 **할당** hello hello 블레이드 맨 아래에 있습니다.

8. Hello 상태 및 hello 프로세스의 결과 보여 주는 hello 오른쪽 위 모퉁이에 알림이 표시 됩니다. Hello 할당 toohello 그룹 (예를 들어 hello 그룹의 기존 라이선스가) 때문에 완료할 수 없습니다, hello 오류의 hello 알림 tooview 자세히를 클릭 합니다.

이제 hello HR 부서 그룹에 대 한 라이선스 템플릿을 지정 했습니다. Azure AD에서 백그라운드 프로세스 해당 그룹의 모든 기존 멤버 tooprocess 시작된 되었습니다. 이 초기 작업 hello hello 그룹의 현재 크기에 따라 몇 시간이 걸릴 수 있습니다. Hello 다음 단계에서 어떻게 tooverify 해당 hello 프로세스를 마쳤는지 설명 알아보고 추가로 주의가 필요한 tooresolve 문제 인지 확인 하겠습니다.

> [!NOTE]
> 시작할 수 있습니다 사용할 다른 위치에서 동일한 할당 hello: **사용자 및 그룹** Azure AD에서 합니다. 너무 이동**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**합니다. 그런 다음 hello 그룹을 찾을 선택 하 고 toohello 이동 **라이선스** 탭 hello **할당** hello 블레이드 맨 위에 단추 hello 라이선스 할당 블레이드를 엽니다.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>2 단계: 초기 할당 hello 완료 되었는지 확인

1. 너무 이동**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**합니다. Hello 찾을 **HR 부서** 라이선스에 할당 된 그룹입니다.

2. Hello에 **HR 부서** 그룹 블레이드에서 **라이선스**합니다. 이 통해 신속 하 게 할당 한 경우 라이선스 완전히 toousers 및 오류가에 toolook 해야 하는 경우를 확인할 수 있습니다. hello 다음 정보를 사용할 수 있습니다.

   - 사용 중인 제품 라이선스 목록으로 toohello 그룹을 할당 합니다. 한 항목 tooshow hello 특정 서비스를 사용할 수 있게 선택한 toomake 변경 합니다.

   - Hello 최신 라이선스 변경 된 내용이 toohello 그룹 (hello 변경 내용을 처리 되는 경우 또는 사용자의 모든 멤버에 대 한 처리가 완료 되는 경우)의 상태입니다.

   - 라이선스를 할당할 수 없습니다 toothem 때문에 오류 상태에 있는 사용자에 대 한 정보입니다.

   ![할당 옵션](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. 라이선스처리에 대한 자세한 내용은 **Azure Active Directory** > **사용자 및 그룹** > *그룹 이름* > **감사 로그**를 참조하세요. 활동이 참고 hello:

   - 활동: **기반 그룹 라이선스 toousers 적용을 시작할**합니다. 이 hello 시스템 hello 그룹과 tooall 사용자 멤버를 적용 하는 시작에 라이선스 할당 변경 hello 선택 하는 경우 기록 됩니다. Hello 변경 내용을 대 한 정보를 포함 합니다.

   - 활동: **다 기반 그룹 라이선스 toousers 적용**합니다. 이 hello 시스템 hello 그룹의 모든 사용자 처리를 완료할 때 기록 됩니다. 성공적으로 처리된 사용자 수와 그룹 라이선스를 할당하지 못한 사용자 수에 대한 요약 정보가 포함되어 있습니다.

   [이 섹션을 읽고](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn 감사 로그 그룹 기반의 라이선스에 의해 사용 되는 tooanalyze 변경한을 수 있는 방법에 대 한 자세한 합니다.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>3단계: 라이선스 문제 확인 및 해결

1. 너무 이동**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**, hello 및 **HR 부서**라이선스에 할당 된 그룹입니다.
2. Hello에 **HR 부서** 그룹 블레이드에서 **라이선스**합니다. hello 블레이드 맨 위에 hello 알림 10 사용자가을 할당할 수 없습니다. 라이선스를 보여 줍니다. 이 알림을 클릭하면 이 그룹에서 라이선스 오류 상태인 모든 사용자 목록이 열립니다.
3. hello **할당 하지 못했습니다** 열 알려줍니다. 두 제품 라이선스를 toohello 사용자를 할당할 수 없습니다. hello **실패 이유를 상위** hello 실패의 원인을 hello 열에 포함 되어 있습니다. 이 예에서는 **충돌하는 서비스 계획**이 실패의 원인입니다.

   ![할당 실패](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. 사용자 tooopen hello 선택 **라이선스** 블레이드입니다. 이 블레이드 toohello 사용자를 현재 할당 된 모든 라이선스를 보여 줍니다. 이 예제에서는 hello 사용자에 게 hello에서 상속 된 Office 365 Enterprise E1 hello 라이선스 **키오스크 사용자** 그룹입니다. Hello에서 시도 하는 시스템 tooapply hello hello E3 라이선스와 충돌 **HR 부서** 그룹입니다. 결과적으로, 해당 그룹에서 hello 라이선스 없음가 할당 toohello 사용자.

   ![사용자의 라이선스 보기](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve이이 충돌을 hello에서 hello 사용자 제거 **키오스크 사용자** 그룹입니다. Azure AD 프로세스가 hello 변경 후 hello **HR 부서** 라이선스 잘못 지정 합니다.

   ![잘못 할당된 라이선스](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>다음 단계

toolearn 그룹을 통해 라이선스 관리에 대 한 설정 hello 기능에 대 한 자세한 참조 문서 다음 hello:

* [Azure Active Directory의 그룹 기반 라이선스란?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Toomigrate 개별 toogroup 기반 라이선스 Azure Active Directory에서 사용자가 사용이 허가 된 방법](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory 그룹 기반 라이선스 추가 시나리오](active-directory-licensing-group-advanced.md)
