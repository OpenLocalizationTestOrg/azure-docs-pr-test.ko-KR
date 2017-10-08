---
title: "Azure 보안 센터에서 aaaPermissions | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 역할 기반 액세스 제어 tooassign 권한 toousers를 사용 하는 방법에 대해 설명 하 고 hello 허용 되는 각 역할에 대 한 작업을 식별 합니다."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Azure Security Center의 권한

Azure 보안 센터를 사용 하 여 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md)를 제공 하는 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) toousers, 그룹 및 Azure 서비스에에서 할당할 수 있습니다.

보안 센터의 리소스 tooidentify 보안 문제 및 취약점 hello 구성을 평가합니다. 보안 센터에만 정보를 확인할 때 hello 구독 또는 리소스 그룹에 속한 리소스에 대 한 소유자, 참가자 또는 판독기의 hello 역할이 할당 된 경우 tooa 리소스와 관련 된 합니다.

또한 toothese 역할에는 두 개의 특정 보안 센터 역할이 있습니다.

* **보안 판독기**: toothis 역할에 속하는 사용자에 게 권한 tooSecurity 센터 보기. hello 사용자 권장 사항, 경고, 보안 정책 및 보안 상태를 볼 수 있지만 변경할 수 없습니다.
* **보안 관리자**: toothis 역할에 속하는 사용자 hello 보안 판독기로 권한 같은 hello에 hello 보안 정책을 업데이트 하 고 수 경고 및 권장 사항을 해제 합니다.

> [!NOTE]
> hello 보안 역할, 보안 판독기 및 보안 관리자를 보안 센터에만 액세스할 수 있으며 hello 보안 역할에 Azure 저장소, 웹 및 모바일, 사물 인터넷 등의 액세스 tooother 서비스 분야를 사용할 필요가 없습니다.
>
>

## <a name="roles-and-allowed-actions"></a>역할 및 허용되는 작업

hello 다음 표에서 역할을 표시 하 고 허용 되는 보안 센터에서 작업 합니다. X가 해당 역할에 대 한 hello 작업 허용 됨을 나타냅니다.

| 역할 | 보안 정책 편집 | 리소스에 보안 권장 사항 적용 | 경고 및 권장 사항 해제 | 경고 및 권장 사항 보기 |
|:--- |:---:|:---:|:---:|:---:|
| 구독 소유자 | X | X | X | X |
| 구독 참가자 | X | X | X | X |
| 리소스 그룹 소유자 | -- | X | -- | X |
| 리소스 그룹 참가자 | -- | X | -- | X |
| 판독기 | -- | -- | -- | X |
| 보안 관리자 | X | -- | X | X |
| 보안 판독기 | -- | -- | -- | X |

> [!NOTE]
> Hello를 할당 하는 것이 좋습니다 사이의 역할 작업 사용자 toocomplete에 필요 합니다. 예를 들어 권장 사항을 적용 하거나 정책 편집 등의 작업을 사용 하지는 않지만 hello 보안 상태에 대 한 리소스의 tooview 정보 하기만 hello 판독기 역할 toousers를 할당 합니다.
>
>

## <a name="next-steps"></a>다음 단계
이 문서는 보안 센터 tooassign 권한 toousers RBAC를 사용 하는 방법을 설명 하 고 hello 허용 되는 각 역할에 대 한 작업을 식별 합니다. 익숙한 hello 역할 할당이 필요 toomonitor hello 구독의 보안 상태, 했으므로 보안 정책을 편집 하며 권장 구성 적용, 자세한 내용은 방법:

- [Security Center에서 보안 정책 설정](security-center-policies.md)
- [Security Center의 보안 권장 사항 관리](security-center-recommendations.md)
- [Azure 리소스의 hello 보안 상태를 모니터링 합니다.](security-center-monitoring.md)
- [관리 및 보안 센터에서 toosecurity 경고에 응답](security-center-managing-and-responding-alerts.md)
- [파트너 보안 솔루션 모니터링](security-center-partner-solutions.md)
