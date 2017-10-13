---
title: "Recovery Services 자격 증명 모음 개요 | Microsoft Docs"
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
ms.openlocfilehash: 19e2aafe3de106be32f3d90c63c0ea03c626f272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="recovery-services-vaults-overview"></a>Recovery Services 자격 증명 모음 개요

이 문서에서는 Recovery Services 자격 증명 모음의 기능을 설명합니다. Recovery Services 자격 증명 모음은 Azure에서 데이터를 저장하는 저장소 엔터티입니다. 데이터는 일반적으로 데이터의 복사본 또는 가상 컴퓨터(VM), 워크로드, 서버 또는 워크스테이션에 대한 구성 정보입니다. Recovery Services 자격 증명 모음은 Resource Manager 버전의 백업 자격 증명 모음입니다. Microsoft에서는 Recovery Services 자격 증명 모음을 사용하여 모든 백업 자격 증명 모음을 Recovery Services 자격 증명 모음으로 변환하도록 권장합니다.

## <a name="what-is-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음이란?

Recovery Services 자격 증명 모음은 백업 복사본, 복구 지점 및 백업 정책과 같은 데이터를 보관하는 데 사용되는 Azure의 온라인 저장소 엔터티입니다. Recovery Services 자격 증명 모음을 사용하여 IaaS VM(Linux 또는 Windows) 및 Azure SQL Database와 같은 다양한 Azure 서비스에 대한 백업 데이터를 저장할 수 있습니다. Recovery Services 자격 증명 모음은 System Center DPM, Windows Server, Azure Backup Server 등을 지원합니다. Recovery Services 자격 증명 모음을 사용하면 관리 오버헤드를 최소화하면서 백업 데이터를 쉽게 구성할 수 있습니다.

Azure 구독 내에서 Recovery Services 자격 증명 모음을 원하는 만큼 만들 수 있습니다.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Recovery Services 자격 증명 모음 및 백업 자격 증명 모음 비교

Recovery Services 자격 증명은 Azure의 Azure Resource Manager 모델에 기반한 반면 백업 자격 증명 모음은 Azure 서비스 관리자 모델에 기반합니다. 백업 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드할 때 업그레이드 프로세스 전후의 백업 데이터는 그대로 유지됩니다. Recovery Services 자격 증명 모음은 다음과 같은 백업 자격 증명 모음에 사용할 수 없는 기능을 제공합니다.

- **백업 데이터 보호 기능 향상**: Recovery Services 자격 증명 모음에서 Azure Backup은 클라우드 백업을 보호하는 보안 기능을 제공합니다. 이러한 보안 기능을 통해 백업을 보호하고 프로덕션 및 백업 서버가 손상된 경우에도 클라우드 백업에서 데이터를 안전하게 복구할 수 있습니다. [자세히 알아보기](backup-azure-security-feature.md)

- **하이브리드 IT 환경을 위한 중심 모니터링**: Recovery Services 자격 증명 모음에서 [Azure IaaS VM](backup-azure-manage-vms.md)뿐만 아니라 중앙 포털에서 [온-프레미스 자산](backup-azure-manage-windows-server.md#manage-backup-items)도 모니터링할 수 있습니다. [자세히 알아보기](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **RBAC(역할 기반 액세스 제어)**: RBAC는 Azure에서 세밀한 액세스 관리 제어를 제공합니다. [Azure는 다양한 기본 제공 역할을 제공](../active-directory/role-based-access-built-in-roles.md)하고 Azure Backup에는 3가지 [복구 지점을 관리하는 기본 제공 역할](backup-rbac-rs-vault.md)이 포함됩니다. Recovery Services 자격 증명 모음은 RBAC와 호환되어 백업을 제한하고 정의된 집합의 사용자 역할에 대한 액세스를 복원합니다. [자세히 알아보기](backup-rbac-rs-vault.md)

- **Azure Virtual Machines의 모든 구성 보호**: Recovery Services 자격 증명 모음은 프리미엄 디스크, Managed Disks 및 암호화된 VM을 비롯한 Resource Manager 기반 VM을 보호합니다. 백업 자격 증명 모음을 Recovery Services 자격 증명 모음으로 업그레이드하면 서비스 관리자 기반 VM을 Resource Manager 기반 VM으로 업그레이드할 수 있습니다. 자격 증명 모음을 업그레이드하는 동안 서비스 관리자 기반 VM 복구 지점을 유지하고 업그레이드된(Resource Manager 사용 가능) VM에 대한 보호를 구성할 수 있습니다. [자세히 알아보기](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **IaaS VM에 대한 인스턴트 복원**: Recovery Services 자격 증명 모음을 사용하여 전체 VM을 복원하지 않고 IaaS VM의 파일 및 폴더를 복원할 수 있습니다. 그러면 복원 시간이 빨라집니다. IaaS VM에 대한 인스턴트 복원은 Windows 및 Linux VM 모두에서 제공됩니다. [자세히 알아보기](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-the-portal"></a>포털에서 Recovery Services 자격 증명 모음 관리
백업 서비스가 Azure 설정 블레이드에서 통합되기 때문에 Azure Portal에서 Recovery Services 자격 증명 모음을 쉽게 만들고 관리할 수 있습니다. 이 통합으로 인해 *대상 서비스의 컨텍스트에서* Recovery Services 자격 증명 모음을 만들거나 관리할 수 있습니다. 예를 들어 VM의 복구 지점을 보려면 해당 VM을 선택하고 설정 블레이드에서 **백업**을 클릭합니다. 해당 VM에 지정된 백업 정보가 표시됩니다. 다음 예제에서 **ContosoVM**은 가상 컴퓨터의 이름입니다. **ContosoVM-demovault**는 Recovery Services 자격 증명 모음의 이름입니다. 가상 컴퓨터에서 이 정보에 액세스할 수 있으므로 복구 지점을 저장하는 Recovery Services 자격 증명 모음의 이름을 기억할 필요가 없습니다.  

![Recovery Services 자격 증명 모음 세부 정보 VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

동일한 Recovery Services 자격 증명 모음을 사용하여 여러 서버를 보호하는 경우 Recovery Services 자격 증명 모음을 살펴보는 것이 좋습니다. 구독에서 모든 Recovery Services 자격 증명 모음을 검색하고 목록에서 하나를 선택할 수 있습니다.

다음 섹션에는 각 종류의 활동에서 Recovery Services 자격 증명 모음을 사용하는 방법을 설명하는 문서에 대한 링크가 있습니다.

### <a name="back-up-data"></a>데이터 백업
- [Azure VM 백업](backup-azure-vms-first-look-arm.md)
- [Windows Server 또는 Windows 워크스테이션 백업](backup-try-azure-backup-in-10-mins.md)
- [Azure에 DPM 워크로드 백업](backup-azure-dpm-introduction.md)
- [Azure Backup Server를 사용하여 워크로드 백업 준비](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>복구 지점 관리
- [Azure VM 백업 관리](backup-azure-manage-vms.md)
- [파일 및 폴더 구성](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-the-vault"></a>자격 증명 모음에서 데이터 복원
- [Azure VM에서 개별 파일 복구](backup-azure-restore-files-from-vm.md)
- [Azure VM 복원](backup-azure-arm-restore-vms.md)

### <a name="secure-the-vault"></a>자격 증명 모음 보안
- [Recovery Services 자격 증명 모음에서 클라우드 백업 데이터 보안](backup-azure-security-feature.md)



## <a name="next-steps"></a>다음 단계
다음과 같은 경우에 다음 문서를 사용합니다.</br>
[IaaS VM 백업](backup-azure-arm-vms-prepare.md)</br>
[Azure Backup Server 백업](backup-azure-microsoft-azure-backup.md)</br>
[Windows Server 백업](backup-configure-vault.md)
