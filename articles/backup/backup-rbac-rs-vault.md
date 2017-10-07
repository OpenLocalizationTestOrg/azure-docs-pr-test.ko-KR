---
title: "역할 기반 액세스 제어를 사용하여 백업 관리 | Microsoft Docs"
description: "복구 서비스 자격 증명 모음에 역할 기반 액세스 제어 toomanage 액세스 toobackup 관리 작업을 사용 합니다."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>역할 기반 액세스 제어 toomanage Azure 백업 복구 지점을 사용 하 여
Azure RBAC(역할 기반 액세스 제어)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 팀 내에서 업무를 구분할 수 있으며 필요 하다는 tooperform 업무 hello 양의 데이터만 toousers 액세스 권한을 부여 수도 있습니다.

> [!IMPORTANT]
> Azure 백업에서 제공 하는 역할은 Azure 포털에서 수행할 수 있는 제한 tooactions 또는 복구 서비스 자격 증명 모음에 PowerShell cmdlet. Azure 백업 에이전트 클라이언트 UI, System Center Data Protection Manager UI 또는 Azure Backup Server UI에서 실행되는 작업은 이러한 역할의 제어를 받지 않습니다.

Azure 백업 3 기본 제공 역할 toocontrol 백업 관리 작업을 제공합니다. [Azure RBAC 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)에 대해 알아보기

* [참가자 백업](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -이 역할에 모든 권한을 toocreate 및 백업 복구 서비스 자격 증명 모음 만들기 및 액세스 tooothers 제공 제외 하 고 관리 합니다. 모든 백업 관리 작업을 수행할 수 있는 백업 관리 관리자 역할로 생각하시면 됩니다.
* [연산자 백업](../active-directory/role-based-access-built-in-roles.md#backup-operator) -이 역할에 사용 권한을 tooeverything 백업 하 고 관리할 백업 정책 제거는 참가자는 제외 합니다. 온-프레미스 리소스의 등록을 제거 또는 삭제 데이터와 함께 백업 중지 등의 삭제 작업을 수행할 수 없습니다 것이 역할 해당 toocontributor는 합니다.
* [판독기 백업](../active-directory/role-based-access-built-in-roles.md#backup-reader) -이 역할에 사용 권한을 tooview 모든 백업 관리 작업입니다. 이 역할 toobe 모니터링 사람을 가정해 보세요.

찾고 있는 경우 toodefine 더 많은 컨트롤에 대 한 사용자 역할, 참조 방법을 너무[빌드 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md) Azure RBAC에 있습니다.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>백업 기본 제공 역할 toobackup 관리 작업 매핑
다음 표에서 hello hello 백업 관리 작업을 캡처하고 해당 최소 RBAC 역할 필요한 tooperform 해당 작업 합니다.

| 관리 작업 | 필요한 최소 RBAC 역할 |
| --- | --- |
| Recovery Services 자격 증명 모음 만들기 | 자격 증명 모음 리소스 그룹의 참여자 |
| Azure VM의 백업 활성화 | 자격 증명 모음의 Backup 운영자, VM의 가상 컴퓨터 참여자 |
| VM의 주문형 백업 | Backup 운영자 |
| VM 복원 | 백업 운영자, 리소스 그룹 참가자는 VM 및 Vnet에 배포 하는 진행 중인 tooget 됩니다. |
| 디스크, VM 백업의 개별 파일 복원 | Backup 운영자 |
| Azure VM 백업에 대한 백업 정책 만들기 | Backup 참여자 |
| Azure VM 백업의 백업 정책 수정 | Backup 참여자 |
| Azure VM 백업의 백업 정책 삭제 | Backup 참여자 |
| VM 백업에서 백업 중지(데이터 보존 또는 데이터 삭제를 통해) | Backup 참여자 |
| 온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 등록 | Backup 운영자 |
| 등록된 온-프레미스 Windows 서버/클라이언트/SCDPM 또는 Azure Backup Server 삭제 | Backup 참여자 |

## <a name="next-steps"></a>다음 단계
* [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.
* Toomanage로 액세스 하는 방법에 대해 알아봅니다.
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [역할 기반 액세스 제어 문제 해결](../active-directory/role-based-access-control-troubleshooting.md): 일반적인 문제를 수정하기 위한 제안 사항을 봅니다.
