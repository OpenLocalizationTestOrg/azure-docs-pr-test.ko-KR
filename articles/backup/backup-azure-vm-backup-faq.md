---
title: "aaaAzure VM 백업 FAQ | Microsoft Docs"
description: "에 대 한 toocommon 질문에 답변: Azure VM의 백업 작동, 제한 사항 및 어떤 상황이 발생 하는 방법 변경 toopolicy 발생 하는 경우"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "Azure VM 백업, Azure VM 복원, 백업 정책"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Hello Azure VM 백업 서비스에 대 한 질문
이 기술 자료이 문서에 대 한 답변 toocommon 질문 toohelp hello Azure VM 백업 구성 요소를 신속 하 게 이해 합니다. 일부 hello 대답의 링크 toohello 문서 포괄적인 정보가 포함 되어 있습니다. Hello에 hello Azure 백업 서비스에 대 한 질문을 게시할 수도 있습니다 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)합니다.

## <a name="configure-backup"></a>백업 구성
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Recovery Services 자격 증명 모음은 클래식 VM 또는 Resource Manager 기반 VM을 지원하나요? <br/>
Recovery Services 자격 증명 모음은 두 모델을 모두 지원합니다.  클래식 (hello 클래식 포털에서 만든)를 VM 또는 복구 서비스 자격 증명 모음 (hello Azure 포털에서에서 만든) 리소스 관리자 VM tooa를 백업할 수 있습니다.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Azure VM 백업에서 지원되지 않는 구성은 무엇인가요?
[지원되는 운영 체제](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) 및 [VM 백업 제한](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)을 참조하세요.

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>백업 구성 마법사에서 내 VM을 볼 수 없는 이유는 무엇인가요?
백업 구성 마법사에서 Azure Backup은 다음과 같은 VM만 나열합니다.
* 아직 보호-tooVM 블레이드를 이동 하 hello 블레이드의 설정 메뉴에서 백업 상태를 검사 하 여 VM의 hello 백업 상태를 확인할 수 있습니다. 너무 자세한 방법에 대 한 자세한 내용은[VM의 백업 상태를 확인 합니다.](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* VM으로 toosame 영역 속한

## <a name="backup"></a>백업
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>주문형 백업 작업은 예약된 백업과 동일한 보존 일정을 따르나요?
아니요. Toospecify hello 보존 범위는 요청 시 백업 작업에 필요합니다. 기본적으로 포털에서 트리거된 이후 30일 동안 유지됩니다. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>최근에 일부 VM에서 Azure Disk Encryption을 사용할 수 있습니다. 백업이 계속 toowork?
Azure 백업 서비스 tooaccess 주요 자격 증명 모음에 대 한 toogive 권한이 필요 합니다. [PowerShell 설명서](backup-azure-vms-automation.md)의 *백업 사용* 섹션에서 설명하는 단계를 사용하여 PowerShell에서 이러한 권한을 제공할 수 있습니다.

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>I VM toomanaged 디스크의 디스크 마이그레이션됩니다. 백업이 계속 toowork?
예, 백업을 원활 하 게 작동 하 고 필요 toore 없습니다-백업을 구성 합니다. 

## <a name="restore"></a>복원
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>디스크 복원과 전체 VM 복원 중에서 어떻게 결정해야 하나요?
복원된 VM에 대해 빠른 만들기 옵션을 사용하는 방법으로 Azure 전체 VM 복원을 생각해 볼 수 있습니다. VM 복원 컨테이너에서 사용 하는 디스크, 공용 IP 주소, 네트워크 인터페이스를 가져오는 VM 만들기의 일부로 생성 된 리소스의 고유성에 대 한 이름, 옵션에는 디스크의 hello 이름이 변경 됩니다. 또한 hello VM tooavailability 집합 하지 추가 됩니다. 

복원 디스크를 사용하여 다음을 수행합니다.
* Hello 백업 구성에서 hello 크기를 변경 하는 등의 시간 구성 요소에서 생성 되는 VM을 사용자 지정
* 백업 hello 시 존재 하지 않는 구성을 추가합니다 
* 가져오는 생성 된 리소스에 대 한 제어 hello 명명 규칙
* VM tooavailability 집합 추가
* PowerShell/선언적 템플릿 정의를 통해서만 설정할 수 있는 구성이 있습니다.

## <a name="manage-vm-backups"></a>VM 백업 관리
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>VM에서 백업 정책을 변경하면 어떻게 되나요?
새 정책을 VM(s)에 적용 되 면 일정 및 보존 hello 새 정책의 뒤 됩니다. 보존을 연장 기존 복구 지점이 표시될지 tookeep 새 정책에 따라 해당 합니다. 보존을 줄이면 정리 hello 다음 정리 작업에서 표시 되 고 삭제 됩니다. 
