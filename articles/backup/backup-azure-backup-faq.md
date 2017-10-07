---
title: "aaaAzure 백업 FAQ | Microsoft Docs"
description: "에 대 한 toocommon 질문에 답변: 복구 서비스 자격 증명 모음를 백업할 수 내용, 작동 방법, 암호화 및 제한을 비롯 한 Azure 백업 기능입니다. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 및 재해 복구; 백업 서비스"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Hello Azure 백업 서비스에 대 한 질문
이 기술 자료이 문서에 대 한 답변 toocommon 질문 toohelp hello Azure 백업 구성 요소를 신속 하 게 이해 합니다. 일부 hello 대답의 링크 toohello 문서 포괄적인 정보가 포함 되어 있습니다. 클릭 하 여 Azure 백업에 대 한 질문을 요청 **주석** (toohello 오른쪽)입니다. 주석은은 hello이이 문서의 맨 아래에 나타납니다. Livefyre 계정은 필요한 toocomment입니다. Hello에 hello Azure 백업 서비스에 대 한 질문을 게시할 수도 있습니다 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)합니다.

이 문서의 tooquickly 스캔 hello 섹션 사용 hello 링크 toohello 오른쪽 아래에서 **이 문서의**합니다.


## <a name="recovery-services-vault"></a>Recovery Services 자격 증명 모음

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>이 각 Azure 구독에서 만들 수 있는 자격 증명 모음 hello 수에 제한이 있습니까? <br/>
예. 2016년 9월을 기준으로 구독 당 25개 Recovery Services 또는 백업 자격 증명 모음을 만들 수 있습니다. 자격 증명 모음 당 구독 당 Azure Backup의 지원 되는 지역 too25 복구 서비스를 만들 수 있습니다. 추가 자격 증명 모음이 필요한 경우 추가 구독을 만드세요.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>각 자격 증명 모음에 대해 등록할 수 있는 서버/컴퓨터 hello 수에 대 한 제한 사항이 있습니까? <br/>
예, 자격 증명 모음 당 too50 컴퓨터를 등록할 수 있습니다. Azure IaaS 가상 컴퓨터에 대 한 hello 제한은 200 Vm 당 자격 증명 모음입니다. 더 많은 컴퓨터 tooregister 해야 할 경우 다른 자격 증명 모음을 만듭니다.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>내 조직에 하나의 자격 증명 모음이 있는 경우 데이터를 복원할 때 서버 간에 데이터를 어떻게 격리할 수 있나요?<br/>
모든 서버에 동일한 자격 증명 모음을 복구할 수는 등록 된 toohello hello 다른 서버에서 백업 된 데이터 *사용 하는 동일한 암호를 hello*합니다. 원하는 tooisolate 서버가 해당 백업 데이터가 있는 경우 조직의 다른 서버에서 해당 서버에 대해 지정 된 암호를 사용 합니다. 예를 들어 인사부 서버가 첫 번째 암호화 암호를 사용하고, 회계 서버가 두 번째, 저장소 서버가 세 번째 암호화 암호를 사용할 수 있습니다.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>구독 간에 내 백업 데이터 또는 자격 증명 모음을 “마이그레이션”할 수 있나요? <br/>
아니요. hello 자격 증명 모음 구독 수준에서 만들어지고가 만들어지면 재할당할된 tooanother 구독 일 수 없습니다.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Recovery Services 자격 증명 모음은 Resource Manager에 기반합니다. Backup 자격 증명 모음(기본 모드)은 계속 지원되나요? <br/>
모든 기존 백업에서에서 자격 증명 모음 hello [클래식 포털](https://manage.windowsazure.com) 지원 toobe를 계속 합니다. 그러나 hello 클래식 포털 toodeploy 새 백업 자격 증명 모음은 더 이상 사용할 수 없습니다. 이후의 향상 된 내용을 tooRecovery 서비스 자격 증명 모음을만 적용 되므로 모든 배포에 대해 복구 서비스 자격 증명 모음을 사용 하는 것이 좋습니다. 리디렉션된 toohello 됩니다 toocreate hello 클래식 포털에서 백업 자격 증명 모음을 시도 하면 [Azure 포털](https://portal.azure.com)합니다.

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음을 마이그레이션할 수 있습니까? <br/>
아쉽게도 아니요, 복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa의 hello 콘텐츠를 마이그레이션할 수 없습니다. 이 기능을 추가하려고 노력하고 있지만 현재는 사용할 수 없습니다.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Backup 자격 증명 모음에 내 클래식 VM을 백업했습니다. 클래식 모드 tooResource 관리자 모드에서 내 Vm 마이그레이션을 복구 서비스 자격 증명 모음에서 보호할 수 있습니까?
백업 자격 증명 모음에 클래식 VM 복구 지점을 클래식 tooResource 관리자 모드에서에서 hello VM을 이동할 때 tooa 복구 서비스 자격 증명 모음을 자동으로 마이그레이션합니다 하지 않습니다. 이러한 단계 tootransfer VM 백업을 수행 합니다.

1. Hello 백업 자격 증명 모음에서 이동 toohello **보호 된 항목** 탭 하 고 hello VM을 선택 합니다. [보호 중지](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)를 클릭합니다. *연결된 백업 데이터 삭제* 옵션을 **검사하지 않음**으로 둡니다.
2. Hello VM에서에서 hello 백업/스냅숏 확장을 삭제 합니다.
3. 클래식 모드 tooResource 관리자 모드에서 hello 가상 컴퓨터를 마이그레이션하십시오. 해당 toohello 가상 컴퓨터가 이기도 hello 저장소 및 네트워크 정보 tooResource 관리자 모드 마이그레이션 되었는지 확인 합니다.
4. 복구 서비스 자격 증명 모음 만들기 및 구성 hello에 백업 마이그레이션된 가상 컴퓨터를 사용 하 여 **백업** 자격 증명 모음 대시보드를 기반으로 동작 합니다. 자격 증명 모음에 대 한 자세한 내용은 VM tooa 복구 서비스를 백업, hello 문서 참조 [복구 서비스 자격 증명 모음 Azure Vm 보호](backup-azure-vms-first-look-arm.md)합니다.

## <a name="azure-backup-agent"></a>Azure Backup 에이전트
자세한 질문 목록은 [Azure 파일 폴더 백업 FAQ](backup-azure-file-folder-backup-faq.md)에 있습니다.

## <a name="azure-vm-backup"></a>Azure VM 백업
자세한 질문 목록은 [Azure VM 백업 FAQ](backup-azure-vm-backup-faq.md)에 있습니다.

## <a name="back-up-vmware-servers"></a>VMware 서버 백업

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>VMware vCenter 서버 tooAzure을 백업할 수 있습니까?

예. Azure 백업 서버 tooback VMware vCenter와 ESXi tooAzure를 사용할 수 있습니다. 지원 되는 hello VMware 버전에 대 한 내용은 hello 문서를 참조 [Azure 백업 서버 보호 매트릭스](backup-mabs-protection-matrix.md)합니다. 단계별 지침은 참조 하십시오. [VMware 서버를 사용 하 여 Azure 백업 서버 tooback](backup-azure-backup-server-vmware.md)합니다.


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup Server 및 System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>사용할 수 있습니까 Azure 백업 서버 toocreate 완전 복구 (BMR) 백업 하는 물리적 서버에 대 한? <br/>
예.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>내 DPM 서버 toomultiple 자격 증명 모음을 등록할 수 있습니까? <br/>
아니요. DPM 또는 MABS 서버 자격 증명 모음 등록된 tooonly 하나 될 수 있습니다.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>지원되는 System Center Data Protection Manager의 버전은 무엇인가요? <br/>
Hello를 설치 하는 것이 좋습니다 [최신](http://aka.ms/azurebackup_agent) hello 최신 업데이트 롤업 (UR)에 대 한 System Center Data Protection Manager (DPM)에서 Azure 백업 에이전트입니다. 2016 년 8 월 업데이트 롤업 11을 hello 최신 업데이트 했습니다.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Azure 백업 에이전트 tooprotect 내 파일 및 폴더 설치 했습니다. 설치할 수 있는 이제 System Center DPM toowork와 Azure 백업 에이전트 tooprotect 온-프레미스 응용 프로그램/v M 작업 tooAzure? <br/>
toouse Azure 백업으로 System Center Data Protection Manager (DPM), DPM을 먼저 설치 하 고 Azure 백업 에이전트를 설치 합니다. DPM과 함께 작동 하는 hello Azure 백업 에이전트 확인이 순서로 hello Azure 백업 구성 요소를 설치 합니다. DPM을 설치 하기 전에 hello Azure 백업 에이전트 설치 사전에 알고 있던 하거나 지원 하지 않습니다.


## <a name="how-azure-backup-works"></a>Azure Backup 작동 방식
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>시작 된 후 백업 작업은 취소를 hello 전송 되는 백업 데이터 삭제 됩니다. <br/>
아니요. Hello 자격 증명 모음에 hello 백업 작업을 취소 하기 전에 hello 자격 증명 모음으로 전송 되는 모든 데이터가 유지 됩니다. 검사점 메커니즘 toooccasionally 하는 동안 검사점 toohello 백업 데이터를 추가 하는 azure 백업에서는 hello 백업 합니다. Hello 백업 데이터에서 검사점 있기 때문에 hello 다음 백업 프로세스 hello 파일의 hello 무결성 유효성을 검사할 수 있습니다. hello 다음 백업 작업을 증분 toohello 데이터는 이전에 백업 됩니다. 증분 백업을 대역폭의 사용률과 toobetter은 새롭거나 변경 된 데이터를 전송 합니다.

Azure VM에 대한 백업 작업을 취소하면 모든 전송된 데이터는 무시됩니다. 다음 백업 작업 hello hello 마지막으로 성공한 백업 작업에서 증분 데이터를 전송합니다.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>백업 작업을 예약할 수 있는 시간 또는 횟수에 제한이 있나요?<br/>
예. Windows Server 또는 toothree 시간 / 일을 Windows 워크스테이션에서 백업 작업을 실행할 수 있습니다. 하루 tootwice를 System Center DPM에서 백업 작업을 실행할 수 있습니다. IaaS VM의 경우 하루에 한 번 백업 작업을 실행할 수 있습니다. Windows Server 또는 Windows 워크스테이션 toospecify 예약 정책 hello를 사용할 수 있습니다 매일 또는 매주 일정입니다. System Center DPM을 사용하여 일별, 주별, 월별, 연도별로 일정을 지정할 수 있습니다.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>복구 서비스 자격 증명 모음에 백업 하려면 hello 데이터 보다 더 작은 hello 전송 되는 데이터 toohello의 hello 크기 이유는 무엇입니까?<br/>
 Azure 백업 에이전트 또는 SCDPM 또는 Azure 백업 서버에서 백업 된 모든 hello 데이터가 압축 되 고 전송 전에 암호화 됩니다. Hello 압축 및 암호화를 적용 한 후 hello 데이터 hello 백업 자격 증명 모음에는 30-40% 더 작은입니다.

## <a name="what-can-i-back-up"></a>어떤 것을 백업할 수 있나요?
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Azure Backup에서 지원하는 운영 체제는 무엇인가요? <br/>
Azure 백업 지원를 백업 하기 위한 운영 체제 목록은 다음 hello: 파일 및 폴더와 작업 응용 프로그램을 Azure 백업 서버 및 System Center Data Protection Manager (DPM)를 사용 하 여 보호 합니다.

| 운영 체제 | 플랫폼 | SKU |
|:--- | --- |:--- |
| Windows 8 및 최신 SP |64비트 |Enterprise, Pro |
| Windows 7 및 최신 SP |64비트 |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 및 최신 SP |64비트 |Enterprise, Pro |
| Windows 10 |64비트 |Enterprise, Pro, Home |
| Windows Server 2016 |64비트 |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 및 최신 SP |64비트 |Standard, Datacenter, Foundation |
| Windows Server 2012 및 최신 SP |64비트 |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 및 최신 SP |64비트 |Standard, Workgroup | 
| Windows Storage Server 2012 R2 및 최신 SP |64비트 |Standard, Workgroup |
| Windows Storage Server 2012 및 최신 SP |64비트 |Standard, Workgroup |
| Windows Server 2012 R2 및 최신 SP |64비트 |Essential |
| Windows Server 2008 R2 SP1 |64비트 |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64비트 |Standard, Enterprise, Datacenter, Foundation |

**Azure VM 백업의 경우:**

* **Linux**: Azure Backup은 Core OS Linux를 제외한 [Azure 인증 배포 목록](../virtual-machines/linux/endorsed-distros.md)을 지원합니다.  도 하 게 다른 Bring-Your-소유-Linux 배포판 hello VM 에이전트는 hello 가상 컴퓨터에서 사용할 수 있는 정상적으로 작동 못할 수도 있으며 Python에 대 한 지원.
* **Windows Server**: Windows Server 2008 R2 이전 버전은 지원되지 않습니다.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>백업 중인 데이터 원본의 크기 hello에 대 한 제한을 거기? <br/>
Hello tooa 자격 증명 모음에 백업할 수 하는 데이터 크기 제한은 없습니다. Azure 백업 hello hello 데이터 원본에 대 한 최대 크기 제한, 이러한 제한 사항은 큰 합니다. 2015 년 8 월 현재 hello hello 지원 운영 체제에 대 한 데이터 원본에 대 한 최대 크기는:

| S.No | 운영 체제 | 데이터 원본의 최대 크기 |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 이상 |54,400GB |
| 2 |Windows 8 이상 |54,400GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700GB |
| 4 |Windows 7 |1700GB |

다음 표에서 hello 각 데이터 원본 크기를 결정 하는 방법을 설명 합니다.

| 데이터 원본 | 세부 정보 |
|:---:|:--- |
| 볼륨 |서버 또는 클라이언트 컴퓨터의 단일 볼륨에서 백업 되는 데이터 양을 hello |
| Hyper-V 가상 컴퓨터 |백업 중인 hello 가상 컴퓨터의 모든 hello Vhd의 데이터의 합계 |
| Microsoft SQL Server 데이터베이스 |백업되는 단일 SQL Database 크기 |
| Microsoft SharePoint |백업 되는 SharePoint 팜 내부에서 hello 콘텐츠 및 구성 데이터베이스의 합계 |
| Microsoft Exchange |백업되는 Exchange 서버의 모든 Exchange 데이터베이스 합계 |
| BMR/시스템 상태 |각 개별 사본을 hello 컴퓨터의 BMR 또는 시스템 상태 백업 |

Azure VM 백업 각 VM 인 각 데이터 디스크 크기가 1023GB 이하의 too16 데이터 디스크를 포함할 수 있습니다. 

## <a name="retention-policy-and-recovery-points"></a>보존 정책 및 복구 지점
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>DPM에 대 한 hello 보존 정책 및 Windows Server/client 간의 차이가 (즉, Windows Server DPM 없이)?<br/>
아니요, DPM 및 Windows Server/클라이언트 모두 일별, 주별, 월별, 연도별 보존 정책을 포함합니다.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>내 보존 정책을 선택적으로 구성할 수 있나요? 즉, 연도별, 월별 정책은 구성하지 않고 주별, 일별 정책을 구성할 수 있나요?<br/>
예, Azure 백업 보존 구조 hello가 있습니다 toohave 완벽 한 유연성을 hello 보존 정책 요구 사항에 따라 정의 합니다.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>오후 6시에 "백업을 예약"하고 다른 시간에 "보존 정책"을 지정할 수 있나요?<br/>
아니요. 보존 정책은 백업 지점에만 적용할 수 있습니다. 다음 이미지는 hello, 오전 12 시와 오후 6 시 백업에 대 한 hello 보존 정책 지정 되어 있습니다. <br/>

![백업 일정 및 보존](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>오랜 시간 동안 백업을 유지 하는 경우 데 더 많은 시간 toorecover 이전 하는 데이터 요소? <br/>
아니요 – hello 시간 toorecover 가장 오래 된 hello 또는 최신 지점 hello 같은 hello 됩니다. 각 복구 지점은 전체 지점처럼 동작합니다.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>각 복구 지점이 전체 지점 같은 있으면 않습니다으로 영향을 총 청구 가능 백업 저장소 hello?<br/>
일반적인 장기 보존 지점 제품은 백업 데이터를 전체 지점으로 저장합니다. hello 전체 요소가 저장소 *비효율적인* 더 쉽습니다 및 더 빠른 toorestore 합니다. 증분 복사본은 저장소 *효율적인* 있지만 toorestore 복구 시간에 영향을 주는 데이터의 체인을 해야 합니다. Azure 백업 저장소 아키텍처를 사용 최적으로 빠른 복원에 대 한 데이터를 저장 하 고 낮은 저장소 비용이 발생 하 여의 장점 hello 있습니다. 이 데이터 저장소 방법을 사용하면 수신 및 발신 대역폭이 효율적으로 사용됩니다. 모두 데이터 저장소 및 hello 시간의 hello 크기 필요한 toorecover hello 데이터, 최소 tooa 유지 됩니다. [증분 백업](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/)이 얼마나 효율적인지 자세히 알아보세요.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>이 hello 만들 수 있는 복구 지점 수에 제한이 있습니까?<br/>
보호 된 인스턴스 당 too9999 복구 포인트를 만들 수 있습니다. 보호 된 인스턴스는 컴퓨터, 서버 (실제 또는 가상) 또는 데이터 tooAzure 구성 하는 작업 tooback입니다. 자세한 내용은 hello 설명은 참조 하십시오. [백업 및 보존](./backup-introduction-to-azure-backup.md#backup-and-retention), 및 [보호 된 인스턴스를 이란](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>TooAzure 백업 된 hello 데이터에 대해 수행할 수 있는 개수 복구는 있습니까?<br/>
Azure 백업에서 복구 hello 수 제한은 없습니다.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>데이터를 복원할 때 납부 hello 송신 트래픽에 대 한 Azure에서? <br/>
아니요. 프로그램 복구 수 있고 hello 송신 트래픽에 대 한 비용이 청구 되지 않습니다.

## <a name="azure-backup-encryption"></a>Azure Backup 암호화
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>hello 데이터 암호화 tooAzure 전송 되나요? <br/>
예. 데이터는 a e s 256을 사용 하 여 hello 온-프레미스 서버/클라이언트/SCDPM 컴퓨터에서 암호화 및 hello 데이터 보안 HTTPS 링크를 통해 전송 됩니다.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>암호화 된 상태로 Azure에서 백업 데이터 hello 인가요?<br/>
예. hello 데이터 전송 tooAzure (rest)로 암호화 된 상태로 유지 됩니다. Microsoft는 언제 든 지 hello 백업 데이터를 해독 하지 않습니다. Azure VM에 백업 하는 경우 Azure 백업 hello 가상 컴퓨터의 암호화 의존 합니다. 예를 들어 VM은 Azure 디스크 암호화 또는 일부 다른 암호화 기술을 사용 하 여 암호화 되 면 Azure 백업을 사용 하 여 해당 암호화 toosecure 데이터.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Tooencrypt 백업 데이터를 사용할 암호화 키의 최소 길이 hello 이란? <br/>
Azure 백업 에이전트를 사용 하는 경우에 16 자 이상인 ' hello 암호화 키 해야 합니다. Azure Vm에 대 한 Azure KeyVault 사용 되는 키의 없습니다 제한 toolength가 있습니다. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>Hello 암호화 키를 잃어버리기 하려면 어떻게 됩니까? 복구 하는 hello 데이터 (또는) Microsoft hello 데이터를 복구할 수 있습니까? <br/>
hello 사용 되는 키 tooencrypt hello에 대 한 백업 데이터는 hello 고객 사업장에 대해서만 존재 합니다. Microsoft은 Azure의 복사본을 유지 하지 않는 및 모든 액세스 toohello 키가 없습니다. Hello 고객 misplaces hello 키를 Microsoft hello 백업 데이터를 복구할 수 없습니다.
