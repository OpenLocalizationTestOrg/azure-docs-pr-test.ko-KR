---
title: "복구 서비스 자격 증명 모음 aaaOverview | Microsoft Docs"
description: "Recovery Services 자격 증명 모음 및 Azure 백업 자격 증명 모음 간의 개요 및 비교입니다."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Recovery Services 자격 증명 모음 개요

이 문서는 복구 서비스 자격 증명 모음 hello 기능을 설명합니다. Recovery Services 자격 증명 모음은 Azure에서 데이터를 저장하는 저장소 엔터티입니다. hello 데이터는 일반적으로 데이터 또는 가상 컴퓨터 (Vm), 작업, 서버 또는 워크스테이션에 대 한 구성 정보는 복사본입니다. 복구 서비스 자격 증명 모음에는 백업 자격 증명 모음의 hello 리소스 관리자 버전입니다. Microsoft는 것이 권장 toouse 복구 서비스 자격 증명 모음 및 tooconvert 모든 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.

## <a name="what-is-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음이란?

복구 서비스 자격 증명 모음은 Azure의 온라인 저장소 엔터티를 사용 하는 백업 정책, 백업 복사본 및 복구 지점 등 toohold 데이터입니다. IaaS Vm (Windows 또는 Linux) 및 Azure SQL 데이터베이스와 같은 다양 한 Azure 서비스에 대 한 복구 서비스 자격 증명 모음 toohold 백업 데이터를 사용할 수 있습니다. Recovery Services 자격 증명 모음은 System Center DPM, Windows Server, Azure Backup Server 등을 지원합니다. 복구 서비스 자격 증명 모음 쉽게 tooorganize 쉬운 관리 오버 헤드를 최소화 하는 동안 백업 데이터를 합니다.

Azure 구독 내에서 Recovery Services 자격 증명 모음을 원하는 만큼 만들 수 있습니다.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Recovery Services 자격 증명 모음 및 백업 자격 증명 모음 비교

복구 서비스 자격 증명 모음 모델을 기반으로 hello Azure 리소스 관리자의 Azure 백업 자격 증명 모음은 모델을 기반으로 hello Azure 서비스 관리자 반면 합니다. 백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음으로 업그레이드 하면 hello 백업 데이터 처리 도중과 hello 업그레이드 프로세스 후 그대로 유지 됩니다. Recovery Services 자격 증명 모음은 다음과 같은 백업 자격 증명 모음에 사용할 수 없는 기능을 제공합니다.

- **확장 된 기능 toohelp 보안 백업 데이터**:와 복구 서비스 자격 증명 모음, Azure 백업에서는 제공 보안 기능 tooprotect 클라우드 백업 합니다. 이러한 보안 기능을 통해 백업을 보호하고 프로덕션 및 백업 서버가 손상된 경우에도 클라우드 백업에서 데이터를 안전하게 복구할 수 있습니다. [자세히 알아보기](backup-azure-security-feature.md)

- **하이브리드 IT 환경을 위한 중심 모니터링**: Recovery Services 자격 증명 모음에서 [Azure IaaS VM](backup-azure-manage-vms.md)뿐만 아니라 중앙 포털에서 [온-프레미스 자산](backup-azure-manage-windows-server.md#manage-backup-items)도 모니터링할 수 있습니다. [자세히 알아보기](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **RBAC(역할 기반 액세스 제어)**: RBAC는 Azure에서 세밀한 액세스 관리 제어를 제공합니다. [Azure에서 다양 한 기본 제공 역할이 제공](../active-directory/role-based-access-built-in-roles.md), Azure 백업에는 3 개의 및 [기본 제공 역할 toomanage 복구 지점](backup-rbac-rs-vault.md)합니다. 복구 서비스 자격 증명 모음을 백업 제한 RBAC와 호환 되는 및 사용자 역할의 액세스 toohello 정의 집합을 복원 합니다. [자세히 알아보기](backup-rbac-rs-vault.md)

- **Azure Virtual Machines의 모든 구성 보호**: Recovery Services 자격 증명 모음은 프리미엄 디스크, Managed Disks 및 암호화된 VM을 비롯한 Resource Manager 기반 VM을 보호합니다. 백업 자격 증명 모음 tooa 업그레이드 복구 서비스 자격 증명 모음에 기회 tooupgrade에 Service Manager 기반 Vm tooResource 관리자 기반 Vm을 hello 제공 합니다. Hello 자격 증명 모음을 업그레이드 하는 동안 Service Manager 기반 VM 복구 지점을 유지 하 고 hello 업그레이드 (리소스 관리자 사용) Vm에 대 한 보호를 구성할 수 있습니다. [자세히 알아보기](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **IaaS Vm에 대 한 인스턴트 복원을**:를 사용 하 여 복구 서비스 자격 증명 모음, 파일을 복원할 수 있습니다 및 폴더를 복원 하지 않고 IaaS VM에서 더 빠른 복원 시간 수 있는 전체 VM hello 합니다. IaaS VM에 대한 인스턴트 복원은 Windows 및 Linux VM 모두에서 제공됩니다. [자세히 알아보기](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Hello 포털에서 사용자 복구 서비스 자격 증명 모음 관리
Hello Azure 포털에서에서 복구 서비스 자격 증명 모음의 생성 및 관리 되므로 쉽게 hello 백업 서비스는 hello Azure 설정 블레이드에서에 통합 합니다. 만들거나 복구 서비스 자격 증명 모음을 관리할 수 있습니다 이러한 통합 의미 *hello 대상 서비스의 hello 컨텍스트에서*합니다. 예를 들어 VM에 대해 tooview hello 복구 지점을 선택한 클릭 **백업** hello 설정 블레이드에서 합니다. hello 백업 정보에 대 한 특정 toothat VM 나타납니다. 다음 예에서는, hello에 **ContosoVM** hello hello 가상 컴퓨터 이름입니다. **ContosoVM demovault** hello hello 복구 서비스 자격 증명 모음 이름입니다. Tooremember hello hello 복구 서비스 자격 증명 모음의 이름을 hello 복구 지점을 저장 하는 필요 하지 않습니다, 그리고 hello 가상 컴퓨터에서이 정보에 액세스할 수 있습니다.  

![Recovery Services 자격 증명 모음 세부 정보 VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Hello를 사용 하 여 여러 서버를 보호 하는 경우 동일한 복구 서비스 자격 증명 모음, hello 복구 서비스 자격 증명 모음에 더 많은 논리 toolook 수도 있습니다. Hello 구독에서 모든 복구 서비스 자격 증명 모음을 검색 하 고 hello 목록에서 하나를 선택 합니다.

hello 다음 단원에서는 각 유형의 활동에서 toouse 복구 서비스 자격 증명 모음에 방법을 설명 하는 링크 tooarticles 합니다.

### <a name="back-up-data"></a>데이터 백업
- [Azure VM 백업](backup-azure-vms-first-look-arm.md)
- [Windows Server 또는 Windows 워크스테이션 백업](backup-try-azure-backup-in-10-mins.md)
- [DPM 작업 부하 tooAzure 백업](backup-azure-dpm-introduction.md)
- [Azure 백업 서버를 사용 하 여 워크 로드를 tooback 준비](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>복구 지점 관리
- [Azure VM 백업 관리](backup-azure-manage-vms.md)
- [파일 및 폴더 구성](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Hello 자격 증명 모음에서 데이터를 복원 합니다.
- [Azure VM에서 개별 파일 복구](backup-azure-restore-files-from-vm.md)
- [Azure VM 복원](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>보안 hello 자격 증명 모음
- [Recovery Services 자격 증명 모음에서 클라우드 백업 데이터 보안](backup-azure-security-feature.md)



## <a name="next-steps"></a>다음 단계
다음 문서에 대 한 hello를 사용 합니다.</br>
[IaaS VM 백업](backup-azure-arm-vms-prepare.md)</br>
[Azure Backup Server 백업](backup-azure-microsoft-azure-backup.md)</br>
[Windows Server 백업](backup-configure-vault.md)
