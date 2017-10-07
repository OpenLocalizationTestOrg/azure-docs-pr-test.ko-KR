---
title: "aaaHow tooconfigure 보안 경고 | Microsoft Docs"
description: "Azure Privileged Identity Management 확장에 대 한 tooconfigure 보안 경고 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management에서 tooconfigure 보안 경고 하는 방법
## <a name="security-alerts"></a>보안 경고
Azure Privileged Identity Management(PIM)은 사용자의 환경에 의심스럽거나 안전하지 않은 활동이 있을 때 경고를 생성합니다. 경고가 트리거 되었을 경우, hello PIM 대시보드에 표시 됩니다. Hello 경고 toosee 사용자 또는 역할 hello 경고를 발생 시킨 목록 hello는 보고서를 선택 합니다.

![PIM 대시보드 보안 경고 - 스크린 샷][1]

| 경고 | 트리거 | 권장 사항 |
| --- | --- | --- |
| **역할이 PIM 외부에서 할당됨** |관리자가 hello PIM 인터페이스 외부에서 tooa 역할에 영구적으로 할당 됩니다. |Hello 새 역할 할당을 검토 합니다. 다른 서비스에는 영구 관리자만 할당할 수, 이후 tooan 적격 할당 필요 하면 변경 합니다. |
| **역할이 너무 자주 활성화됨** |너무 많은 hello 시간 내에서 동일한 역할 hello 설정에서 허용 하는 hello 다시 활성화 했습니다. |Hello 사용자 toosee를 이유은 활성화 한 hello 역할 여러 번에 게 문의 하십시오. Hello 시간에 제한이 너무 짧습니다. 미정 toocomplete은 이전 또는 해당 작업을 사용 하는 스크립트 tooautomatically 역할 활성화 합니다. |
| **역할이 활성화를 위해 Multi-Factor Authentication을 필요로 하지 않음** |MFA hello 설정에서 사용 하도록 설정 하지 않고 역할이 있습니다. |에서는 가장 높은 권한이 있지만 hello 역할에 대 한 MFA를 요구 하지만 모든 역할의 활성화에 MFA를 사용 하는 것을 적극 권장 합니다. |
| **관리자가 권한 있는 역할을 사용 하지 않음** |최근에 해당 역할을 활성화하지 않은 적합한 관리자가 있습니다. |액세스를 더 이상 필요 없는 액세스 검토 toodetermine hello 사용자를 시작 합니다. |
| **전역 관리자가 너무 많음** |권장하는 것보다 전역 관리자가 많습니다. |많은 수의 전역 관리자가 있을 경우, 사용자가 필요 이상으로 많은 사용 권한을 갖게 될 가능성이 있습니다. 이동 사용자 tooless 역할 권한 있는 하거나 그 중 일부만 대신 hello 역할에 대 한 적격 영구적으로 할당 합니다. |

## <a name="configure-security-alert-settings"></a>보안 경고 설정 구성
일부 환경 및 보안 목표에 맞게 PIM toowork에서 보안 경고가 hello 사용자 지정할 수 있습니다. 이러한 단계 tooreach hello 설정 블레이드를 수행 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 및 선택 hello **Azure AD Privileged Identity Management** hello 대시보드에서 타일입니다.
2. **권한 있는 역할 관리** > **설정** > **경고 설정**을 선택합니다.
   
    ![Toosecurity 경고 설정을 이동합니다][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>"역할이 너무 자주 활성화됨" 경고
트리거를 활성화 하는 경우 동일한 권한 있는 역할을 여러 번 지정된 된 기간 내 hello이 경고 합니다. 두 hello 시간 기간 및 hello 정품 인증 횟수를 구성할 수 있습니다.

* **정품 인증 갱신 기간**: 일, 시간, 분에서 지정 하 고 두 번째 hello 시간 기간 원하는 toouse tootrack 의심 스러운 갱신 합니다.
* **정품 인증 갱신 횟수가 높아지면**: hello 고려해 경고 선택한 hello 시간 내에 적합 하는 2 too100에서 정품 인증 수를 지정 합니다. Hello 텍스트 상자에 숫자를 입력 하거나 이동 hello 슬라이더를 통해이 설정을 변경할 수 있습니다.

### <a name="there-are-too-many-global-administrators-alert"></a>"전역 관리자가 너무 많음" 경고
PIM은 서로 다른 두 조건이 충족되고, 그 두 조건을 모두 구성할 수 있을 때 이 경고를 트리거합니다. 첫째, 전역 관리자의 특정 임계값 tooreach를 해야 합니다. 둘째, 총 역할 할당의 특정 비율이 전역 관리자여야 합니다. 이러한 값 중 하나로 충족 하면 hello 경고가 표시 되지 않습니다.  

* **최소 전역 관리자 수**: hello에서 안전 하지 않은 크기를 고려 하는 2 too100, 전역 관리자 수를 지정 합니다.
* **전역 관리자의 백분율**: 0%에서 전역 관리자가 관리자의 hello 백분율 지정 환경에서 안전 하지 않은 too100%입니다.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>“관리자가 권한 있는 역할을 사용 하지 않음” 경고
사용자가 특정 시간 동안 역할을 활성화하지 않는다면 이 경고가 트리거됩니다.

* **일 수**: hello 사용자 역할을 활성화 하지 않고 실행할 수 있는 0 too100에서 일 수를 지정 합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
