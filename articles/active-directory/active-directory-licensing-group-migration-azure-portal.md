---
title: "Azure Active Directory에서 그룹 사용이 허가 된 사용자가 개별 tooa aaaHow toomigrate | Microsoft Docs"
description: "개별 사용자 로부터 tooswitch toogroup 기반 Azure Active Directory를 사용 하 여 라이선스 라이센스 있음을"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Azure Active Directory에서 라이선스에 대 한 tooadd 사용자 tooa 그룹 사용이 허가 된 방법

"직접 할당"; 통해 hello 조직에서 기존 배포 라이선스 toousers를 할 수 있습니다. 즉, PowerShell 스크립트 또는 기타 도구 tooassign 개별 사용자 라이선스를 사용합니다. 마이그레이션 할 toostart 조직에서 그룹 기반의 라이선스 toomanage 라이선스를 사용 하 여 원하는 경우 계획 tooseamlessly 라이선스 그룹을 기반으로 기존 솔루션을 대체 합니다.

hello 가장 중요 한 사항은 tookeep에 주의 하 여 현재 할당 된 라이선스를 일시적으로 손실 되는 사용자가 마이그레이션 toogroup 기반 라이선스 발생 합니다는 상황을 피해 야 한다는입니다. 라이선스 제거 될 수 있는 모든 프로세스를 수행할 수 및 액세스 tooservices과 데이터를 손실 하는 사용자의 tooremove hello 위험을 줄일 수 있습니다.

## <a name="recommended-migration-process"></a>권장 마이그레이션 프로세스

1. 사용자에 대한 라이선스 할당 및 제거를 관리하는 기존 자동화(예: PowerShell) 기능이 있을 것입니다. 이러한 기능은 실행 상태로 둡니다.

2. 새 라이선스 그룹 만들기 (또는 toouse 그룹화 기존 결정) 하 고 필요한 모든 사용자가 구성원으로 추가 해야 합니다.

3. Toothose 그룹; hello 필요한 라이선스를 할당 합니다. 여기서의 목표 tooreflect hello 있어야 합니다. 라이선스 상태 같은 기존 자동화 (예를 들어 PowerShell) 적용 하는 toothose 사용자입니다.

4. 라이선스 그룹에 적용 된 tooall 사용자 되었는지 확인 합니다. 각 그룹에 대해 hello 처리 상태를 확인 하 여 및 감사 로그를 확인 하 여 수행할 수 있습니다.

  - 라이선스 세부 정보를 확인하여 개별 사용자를 부분적으로 확인할 수 있습니다. 그룹에서 동일한 라이선스가 할당 "직접" 및 "상속" hello가 표시 됩니다.

  - 너무 PowerShell 스크립트를 실행할 수[라이선스 toousers 할당 하는 방법을 확인](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)합니다.

  - Hello 동일한 제품 라이선스 할당 하면 toohello 사용자 직접적으로 그리고 그룹을 통해, 하나의 라이선스 hello 사용자가 사용 됩니다. 따라서 추가 라이선스가 없습니다. 필요한 tooperform 마이그레이션 됩니다.

5. 오류 상태의 사용자가 있는지 각 그룹을 확인하여 실패한 라이선스 할당이 없는지 확인합니다. 자세한 내용은 [그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)을 참조하세요.

6. Hello 원래 직접 할당; 제거 하는 것이 좋습니다. toodo 경우가 사용자의 하위 집합에서의 결과 먼저 hello toomonitor "물결"에서 점차적으로 합니다.

  사용자에서는 원래 직접 할당 hello를 발생할 수 있습니다 하지만 hello 사용자가 해당 사용 허가 받은 그룹을 여전히 유지를 떠날 때 되 hello 원래 라이선스 원하지 원하는 합니다.

## <a name="an-example"></a>예제

우리 조직에는 1000명의 사용자가 있습니다. 모든 사용자에게는 EMS(Enterprise Mobility + Security) 라이선스가 필요합니다. 200 명 hello 재무 부서에에서 있으며 Office 365 Enterprise E3 라이선스가 필요 합니다. 온-프레미스에서 PowerShell 스크립트가 실행되고 있으며 사용자가 들어오고 나갈 때 라이선스를 추가 및 제거합니다. Azure AD에서 라이선스가 자동으로 관리 하므로 그룹 기반 라이선스와 tooreplace hello 스크립트를 주시기 바랍니다.

Hello 마이그레이션 프로세스 수 모양을 다음과 같습니다.

1. Azure 포털 할당 hello EMS 라이선스 toohello hello를 사용 하 여 **모든 사용자에 게** Azure AD의 그룹입니다. Hello E3 라이선스 toohello 할당 **재무 부서** 모든 hello 필요한 사용자가 포함 된 그룹입니다.

2. 각 그룹의 모든 사용자에 대한 라이선스 할당이 완료되었는지 확인합니다. 각 그룹에 대 한 이동 toohello 블레이드 **라이선스**, hello hello 맨 hello 처리 상태를 확인 하 고 **라이선스** 블레이드입니다.

  - 찾을 tooconfirm "최신 라이선스 변경 내용이 적용 된 tooall 사용자 되었습니다 없음"에 대 한 처리가 완료 되었습니다.

  - 해당 사용자의 라이선스가 성공적으로 할당되지 않았을 수 있다는 알림은 위쪽에 표시됩니다. 일부 사용자의 라이선스가 부족한가요? 일부 사용자에게 충돌하는 라이선스 SKU가 할당되어 상속 그룹이 라이선스를 할당하지 못하나요?

3. 지점 직접 hello 및 적용 된 그룹 라이선스 모두 포함 하는 일부 사용자가 tooverify를 확인 합니다. 사용자가 선택 이동 toohello 블레이드 **라이선스**, 라이선스 hello 상태를 검사할 합니다.

  - 마이그레이션 중 예상 hello 사용자 상태입니다.

      ![예상되는 사용자 상태](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  이 hello이 사용자는 직접 및 상속 된 라이선스를 확인 합니다. **EMS** 및 **E3**가 둘 다 할당되어 있는 것을 볼 수 있습니다.

  - 사용 하도록 설정 하는 hello 서비스에 대 한 각 라이선스 tooshow 세부 정보를 선택 합니다. 직접 hello 및 라이선스 사용 그룹 hello 사용자에 대 한 동일한 서비스 계획을 정확 하 게 hello 사용된 toocheck 될 수 있습니다.

      ![서비스 계획 확인](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. 직접 및 그룹 라이선스가 동일한 것인지 확인한 후에 사용자에게서 직접 라이선스를 제거할 수 있습니다. Hello 포털에서 개별 사용자에 대 한 제거 하 여이 테스트 하 고 대량에서 제거 하는 자동화 스크립트 toohave를 실행할 수 있습니다. hello hello 직접 라이선스를 갖고 있는 동일한 사용자 hello 포털을 통해 제거 됩니다. 예를 들면 다음과 같습니다. 필름 hello 라이선스 상태 그대로 되지만 직접 할당을 더 이상 참조 했습니다.

  ![직접 라이선스 제거](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>다음 단계

그룹을 통해 라이선스 관리에 대 한 다른 시나리오에 대해 자세히 toolearn 읽기

* [Azure Active Directory에서 tooa 그룹 라이선스 할당](active-directory-licensing-group-assignment-azure-portal.md)
* [Azure Active Directory의 그룹 기반 라이선스란?](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory 그룹 기반 라이선스 추가 시나리오](active-directory-licensing-group-advanced.md)
