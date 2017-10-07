---
title: "Azure Site Recovery aaaUsing 역할 기반 액세스 제어 toomanage | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 tooapply 및 사용 역할 기반 액세스 제어 (RBAC) toomanage Azure 사이트 복구 배포"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>역할 기반 액세스 제어 toomanage Azure 사이트 복구 배포를 사용 하 여

Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 팀 내에서 책임을 구분할 수 있으며 필요한 tooperform 특정 작업으로 사용 권한을 toousers만 특정 액세스 권한을 부여할 수도 있습니다.

Azure Site Recovery 3 기본 제공 역할 toocontrol 사이트 복구 관리 작업을 제공합니다. [Azure RBAC 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)에 대해 알아보기

* [사이트 복구 참가자](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -이 역할은 복구 서비스 자격 증명 모음에 모든 권한이 필요한 toomanage Azure 사이트 복구 작업을 갖습니다. 그러나이 역할을 통해 사용자 만들거나 수 없습니다 또는 복구 서비스 자격 증명 모음 삭제 액세스 tooother 사용자 권한 할당. 이 역할은 hello 사례 수 있으므로 재해 복구 관리자를 사용 하도록 설정 하 고 응용 프로그램이 나 전체 조직에 대 한 재해 복구를 관리할 수 있는 가장 적합 합니다.
* [사이트 복구 연산자](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -이 역할에 사용 권한을 tooexecute 및 관리자 장애 조치 및 장애 복구 작업입니다. 이 역할의 사용자에 수 없습니다 활성화 또는 비활성화 복제, 만들기 또는 자격 증명 모음 삭제, 새로운 인프라를 등록 하거나 액세스 권한 tooother 사용자를 할당 합니다. 이 역할은 실제 또는 시뮬레이션된 재해 상황에서 DR 드릴과 같은 응용 프로그램 소유자 및 IT 관리자가 지시하는 경우 가상 컴퓨터 또는 응용 프로그램을 장애 조치할 수 있는 재해 복구 연산자에 가장 적합합니다. Post hello 재해 해상도 hello DR 연산자 다시 보호할 수 있으며 장애 복구 hello 가상 컴퓨터.
* [사이트 복구 판독기](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -이 역할에 사용 권한을 tooview 모든 사이트 복구 관리 작업입니다. 이 역할은 IT 모니터링 임원 hello 보호의 현재 상태를 모니터링 하 고 필요한 경우 지원 티켓을 발생 시킬 수 있는 가장 적합 합니다.

찾고 있는 경우 toodefine 더 많은 컨트롤에 대 한 사용자 역할, 참조 방법을 너무[빌드 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md) Azure에서.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>새 가상 컴퓨터에 대 한 복제 tooEnable 필요한 권한
Hello 연결 된 사용자의 액세스 수준을 사용자 hello 유효성이 검사 된 tooensure은 새 가상 컴퓨터를 Azure Site Recovery를 사용 하 여 복제 된 tooAzure 이면 hello 요구에 사용 권한을 toouse hello 제공 하는 Azure 리소스 tooSite 복구 합니다.

새 가상 컴퓨터에 대 한 복제 tooenable, 사용자에 게 있어야 합니다.
* 사용 권한 toocreate hello 선택한 리소스 그룹에서 가상 컴퓨터
* 사용 권한 toocreate hello 선택한 가상 네트워크의 가상 컴퓨터
* 사용 권한 toowrite toohello 선택한 저장소 계정

사용자에 게 필요한 hello 새 가상 컴퓨터의 사용 권한 toocomplete 복제를 수행 합니다.

> [!IMPORTANT]
>관련 사용 권한을 hello 배포 모델에 대해 추가 되었는지 확인 (리소스 관리자 / 클래식) 리소스 배포에 사용 합니다.

| **리소스 종류** | **배포 모델** | **사용 권한** |
| --- | --- | --- |
| Compute | 리소스 관리자 | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | 클래식 | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| 네트워크 | 리소스 관리자 | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | 클래식 | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| 저장소 | 리소스 관리자 | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | 클래식 | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| 리소스 그룹 | 리소스 관리자 | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Hello ' 가상 컴퓨터 참가자 ' 및 ' 클래식 가상 컴퓨터 참가자 '를 사용 하는 것이 좋습니다 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md) 리소스 관리자 및 클래식 배포에 대 한 각각을 모델링 합니다.

## <a name="next-steps"></a>다음 단계
* [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.
* Toomanage로 액세스 하는 방법에 대해 알아봅니다.
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [역할 기반 액세스 제어 문제 해결](../active-directory/role-based-access-control-troubleshooting.md): 일반적인 문제를 수정하기 위한 제안 사항을 봅니다.
