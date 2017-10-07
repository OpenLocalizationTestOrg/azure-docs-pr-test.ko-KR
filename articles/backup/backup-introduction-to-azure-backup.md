---
title: "aaaWhat은 Azure 백업 이란? | Microsoft Docs"
description: "Azure 백업 tooback 사용 하 여 및 Windows 서버, Windows 워크스테이션, System Center DPM 서버 및 Azure 가상 컴퓨터에서 데이터 및 작업을 복원 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 및 복원; 복구 서비스; 백업 솔루션"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Azure 백업에 hello 기능 개요
Azure 백업에서 hello Azure 기반 서비스로 수 tooback 사용 하 여 (또는 보호) 및 Microsoft 클라우드 hello에서 데이터를 복원 합니다. 기존의 온-프레미스 또는 오프사이트 백업 솔루션을 신뢰할 수 있고 안전하며 가격 경쟁력이 있는 클라우드 기반 솔루션으로 대체합니다. Azure 백업 제공 다운로드 하 고 hello 적절 한 컴퓨터에 배포 하는 여러 구성 요소 서버 또는 hello 클라우드입니다. 대상에 따라 달라 집니다 hello 구성 요소 또는 배포 하는 에이전트 tooprotect 합니다. 모든 Azure 백업 구성 요소 (온-프레미스 데이터를 보호 하는 여부에 관계 없이 또는 hello 클라우드)에 Azure에서 데이터 tooa 복구 서비스 자격 증명 모음을 사용 하는 tooback 될 수 있습니다. Hello 참조 [Azure 백업 구성 요소 테이블](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (이 문서의 뒷부분에)는 구성 요소 toouse tooprotect 특정 데이터, 응용 프로그램 또는 워크 로드에 대 한 정보에 대 한 합니다.

[Azure Backup의 비디오 개요 시청](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Azure Backup을 사용하는 이유
일반적인 백업 솔루션 tootreat hello 클라우드 끝점 또는 유사한 toodisks 또는 테이프 정적 저장소 대상으로 발전 하 고 있어야 합니다. 이 방법은 간단 제한 되며 tooan 비용이 많이 드는, 비효율적인 솔루션으로 변환 하는 기본 클라우드 플랫폼을 사용 하지 않습니다. 다른 솔루션은 hello 잘못 된 유형의 저장소나 필요 하지 않은 저장소에 대 한 저하가 발생 하기 때문에 비용이 많이 드는입니다. 다른 솔루션 종종 효율적인 hello 유형 또는 스토리지를 양의 있습니다 제공 하지 않거나 관리 작업에 너무 많은 시간이 소요. 반면 Azure Backup은 다음과 같은 주요 이점을 제공합니다.

**자동 저장소 관리** -하이브리드 환경에서는 필요할 수 다른 유형의 저장소-일부 온-프레미스 및 클라우드 hello의 일부입니다. Azure Backup을 사용하면 온-프레미스 저장소 장치를 사용하기 위한 비용이 들지 않습니다. Azure Backup은 백업 저장소를 자동으로 할당하고 관리하며 사용한 만큼 지불(pay-as-you-use) 모델을 사용합니다. 사용량 기준 과금-으로--사용 hello 저장소 사용에 대 한 요금만 지불을 의미 합니다. 자세한 내용은 참조 hello [문서 가격 Azure](https://azure.microsoft.com/pricing/details/backup)합니다.

**무제한 배율** -Azure 백업 전원 기본 hello를 사용 하 고 무제한 확장 hello Azure의 클라우드 toodeliver 고가용성-유지 관리 하지 않고 또는 오버 헤드를 모니터링 합니다. 이벤트에 대 한 경고 tooprovide 정보를 설정할 수 있지만 hello 클라우드에서 데이터에 대 한 고가용성에 대 한 tooworry 필요 하지 않습니다.

**여러 저장소 옵션** - 높은 가용성의 한 양상으로 저장소 복제가 있습니다. Azure Backup에는 두 가지 유형의 복제, 즉 [로컬 중복 저장소](../storage/common/storage-redundancy.md#locally-redundant-storage)와 [지역 중복 저장소](../storage/common/storage-redundancy.md#geo-redundant-storage)가 있습니다. 필요에 따라 hello 백업 저장소 옵션을 선택 합니다.

* 로컬 중복 저장소 (LRS) 데이터를 hello에 쌍 이룬된 데이터 센터에 3 번 (3 개의 데이터 복사본이 만듭니다) 복제 동일한 지역입니다. LRS는 로컬 하드웨어 오류로부터 데이터를 보호하기 위한 저비용 옵션입니다.

* 지역 중복 저장소 (GRS) 데이터 tooa 보조 영역은 (수백 마일 떨어진 hello hello 원본 데이터의 기본 위치)를 복제합니다. GRS는 LRS보다 많은 비용이 소요되지만 GRS는 지역 가동 중단이 발생해도 높은 수준의 데이터 내구성을 제공합니다.

**무제한 데이터 요금 전송** -Azure 백업 인바운드 hello 크기를 제한 하지 않습니다 또는 아웃 바운드 데이터 전송 합니다. Azure 백업도 충전 되지 않습니다. 전송 되는 hello 데이터에 대 한 합니다. 그러나 hello Azure 가져오기/내보내기 서비스 tooimport 많은 양의 데이터를 사용 하는 경우 인바운드 데이터와 관련 된 비용은. 이 비용에 대한 자세한 내용은 [Azure Backup의 오프라인 백업 워크플로](backup-azure-backup-import-export.md)를 참조하세요. 아웃 바운드 데이터에는 복원 작업 중에 복구 서비스 자격 증명 모음에서 전송 toodata를 참조 합니다.

**데이터 암호화** -보안 전송 및 hello 공용 클라우드에서 데이터 저장소에 대 한 데이터 암호화를 허용 합니다. Hello 암호화의 로컬에 암호를 저장 하 고 전송 되거나 Azure에 저장 되지 않습니다. 어떤 것이 필요한 toorestore 경우 hello 데이터의만 암호화의 암호 했거나 키입니다.

**응용 프로그램 일치 백업** -데이터 toorestore hello 백업 복사본을 필요한 해야 할지 여부를 파일 서버, 가상 컴퓨터 또는 SQL 데이터베이스를 백업, 복구 지점에 모든 tooknow 합니다. Azure 백업에는 추가 수정 프로그램은 필요한 toorestore hello 데이터 되지 않습니다 보장 하는 응용 프로그램에 일관 된 백업을 제공 합니다. 응용 프로그램 일치 데이터를 복원 tooquickly 반환 tooa 실행 상태를 허용 되는 hello 복원 시간을 줄어듭니다.

**장기 보존** -디스크 tootape 및 이동 hello 테이프 tooan 오프 사이트 위치에서 백업 복사본을 전환 하는 대신 단기 및 장기 보존에 대 한 Azure를 사용할 수 있습니다. Azure 백업 또는 복구 서비스 자격 증명 모음에 유지 되는 데이터 시간 hello 길이 제한 하지 않습니다. 원하는 만큼 자격 증명 모음에 데이터를 유지할 수 있습니다. Azure Backup에는 보호된 인스턴스당 9999개 복구 지점의 제한이 있습니다. Hello 참조 [백업 및 보존](backup-introduction-to-azure-backup.md#backup-and-retention) 이 한도 필요한 백업 영향을 줄 수는 방법에 대 한 설명은이 문서의 섹션.  

## <a name="which-azure-backup-components-should-i-use"></a>어떤 Azure Backup 구성 요소를 사용해야 합니까?
Azure 백업 구성 요소를 요구에 맞게 작동 하는 확실 하지 않은 경우 hello 다음 각 구성 요소와 보호에 대 한 정보에 대 한 표를 참조 하십시오. Azure 포털 hello hello 포털 tooguide 구성 요소 toodownload hello를 통해 선택 하 고 배포에 기본 제공 되는 마법사를 제공 합니다. 복구 서비스 자격 증명 모음 만들기 hello의 일부인 hello 마법사 hello hello 데이터 또는 응용 프로그램 tooprotect 하 고 백업 목표를 선택 하는 단계를 안내 합니다.

| 구성 요소 | 이점 | 제한 | 보호 대상 | 백업 저장 위치 |
| --- | --- | --- | --- | --- |
| Azure Backup(MARS) 에이전트 |<li>실제 또는 가상 Windows OS에 있는 파일 및 폴더를 백업함(온-프레미스 또는 Azure에 VM 배치 가능)<li>별도의 백업 서버가 필요하지 않음 |<li>매일 3회 백업 <li>응용 프로그램 인식 안 함. 파일, 폴더, 볼륨 수준 복원만 지원 <li>  Linux 지원 안 함 |<li>파일 <li>폴더 |Recovery Services 자격 증명 모음 |
| System Center DPM |<li>VSS(응용 프로그램 인식 스냅숏)<li>시기에 대 한 완전 한 유연성 tootake 백업<li>복구 세분성(모두)<li>Recovery Services 자격 증명 모음을 사용할 수 있음<li>Hyper-V 및 VMware VM에 대한 Linux 지원 <li>DPM 2012 R2를 사용하여 VMware VM 백업 및 복원 |Oracle 워크로드는 백업할 수 없음|<li>파일 <li>폴더<li> 볼륨 <li>VM<li> 응용 프로그램<li> 워크로드 |<li>Recovery Services 자격 증명 모음<li> 로컬 연결된 디스크<li>  테이프(온-프레미스 전용) |
| Azure Backup 서버 |<li>VSS(앱 인식 스냅숏)<li>시기에 대 한 완전 한 유연성 tootake 백업<li>복구 세분성(모두)<li>Recovery Services 자격 증명 모음을 사용할 수 있음<li>Hyper-V 및 VMware VM에 대한 Linux 지원<li>VMware VM 백업 및 복원 <li>System Center 라이선스 필요하지 않음 |<li>Oracle 워크로드는 백업할 수 없음<li>항상 라이브 Azure 구독 필요<li>테이프 백업 지원 안 함 |<li>파일 <li>폴더<li> 볼륨 <li>VM<li> 응용 프로그램<li> 워크로드 |<li>Recovery Services 자격 증명 모음<li> 로컬 연결된 디스크 |
| Azure IaaS VM Backup |<li>Windows/Linux용 기본 백업<li>특정 에이전트 설치할 필요 없음<li>백업 인프라가 필요 없는 패브릭 수준 백업 |<li>하루 한 번 VM 백업 <li>디스크 수준에서만 VM 복원<li>온-프레미스 백업 불가능 |<li>VM <li>모든 디스크(PowerShell 사용) |<p>Recovery Services 자격 증명 모음</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>각 구성 요소에 대 한 hello 배포 시나리오는 무엇입니까?
| 구성 요소 | Azure에 배포할 수 있나요? | 온-프레미스로 배포할 수 있나요? | 지원되는 대상 저장소 |
| --- | --- | --- | --- |
| Azure Backup(MARS) 에이전트 |<p>**예**</p> <p>hello Azure 백업 에이전트는 Azure에서 실행 되는 모든 Windows Server VM에 배포할 수 있습니다.</p> |<p>**예**</p> <p>hello 백업 에이전트는 모든 Windows Server VM 또는 물리적 컴퓨터에 배포할 수 있습니다.</p> |<p>Recovery Services 자격 증명 모음</p> |
| System Center DPM |<p>**예**</p><p>에 대 한 자세한 내용은 [어떻게 System Center DPM을 사용 하 여 Azure에서 tooprotect 작업](backup-azure-dpm-introduction.md)합니다.</p> |<p>**예**</p> <p>에 대 한 자세한 내용은 [어떻게 tooprotect 작업 및 데이터 센터에서 Vm](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager)합니다.</p> |<p>로컬 연결된 디스크</p> <p>Recovery Services 자격 증명 모음</p> <p>테이프(온-프레미스 전용)</p> |
| Azure Backup 서버 |<p>**예**</p><p>에 대 한 자세한 내용은 [어떻게 Azure 백업 서버를 사용 하 여 Azure에서 tooprotect 작업](backup-azure-microsoft-azure-backup.md)합니다.</p> |<p>**예**</p> <p>에 대 한 자세한 내용은 [어떻게 Azure 백업 서버를 사용 하 여 Azure에서 tooprotect 작업](backup-azure-microsoft-azure-backup.md)합니다.</p> |<p>로컬 연결된 디스크</p> <p>Recovery Services 자격 증명 모음</p> |
| Azure IaaS VM Backup |<p>**예**</p><p>Azure 패브릭의 일부</p><p>[Azure IaaS(Infrastructure as a Service) 가상 컴퓨터의 백업](backup-azure-vms-introduction.md)에 맞게 특별히 설정됩니다.</p> |<p>**아니요**</p> <p>System Center DPM tooback 가상 컴퓨터를 사용 하 여 데이터 센터에서.</p> |<p>Recovery Services 자격 증명 모음</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>어떤 응용 프로그램 및 워크로드를 백업할 수 있나요?
다음 표에서 hello hello 데이터 및 Azure 백업을 사용 하 여 보호할 수 있는 작업의 매트릭스를 제공 합니다. hello Azure 백업 솔루션 열에는 해당 솔루션에 대 한 링크 toohello 배포 설명서를 있습니다. 각 Azure Backup 구성 요소는 클래식 (Service Manager 배포 모델) 또는 Resource Manager 배포 모델 환경에 배포할 수 있습니다.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| 데이터 또는 워크로드 | 원본 환경 | Azure Backup 솔루션 |
| --- | --- | --- |
| 파일 및 폴더 |Windows Server |<p>[Azure Backup 에이전트](backup-configure-vault.md)</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| 파일 및 폴더 |Windows 컴퓨터 |<p>[Azure Backup 에이전트](backup-configure-vault.md)</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Hyper-V 가상 컴퓨터(Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Hyper-V 가상 컴퓨터(Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Microsoft SQL Server에 대한 연결 문자열 |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) (+ hello Azure 백업 에이전트)</p> <p>[Azure 백업 서버](backup-azure-microsoft-azure-backup.md) (hello Azure 백업 에이전트 포함)</p> |
| Azure IaaS VM(Windows) |Azure에서 실행 |[Azure Backup(VM 확장)](backup-azure-vms-introduction.md) |
| Azure IaaS VM(Linux) |Azure에서 실행 |[Azure Backup(VM 확장)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Linux 지원
hello 다음 표에서 Linux에 대 한 지지도가지고 있는 hello Azure 백업 구성 요소입니다.  

| 구성 요소 | Linux(Azure 인증) 지원 |
| --- | --- |
| Azure Backup(MARS) 에이전트 |아니요(Windows 기반 에이전트만) |
| System Center DPM |<li> Hyper-V 및 VMWare에서 일관성 있는 Linux 게스트 VM 파일 백업<br/> <li> Hyper-V 및 VMWare Linux 게스트 VM의 VM 복원 </br> </br>  *Azure VM에서 파일 일치 백업을 사용할 수 없음* <br/> |
| Azure Backup 서버 |<li>Hyper-V 및 VMWare에서 일관성 있는 Linux 게스트 VM 파일 백업<br/> <li> Hyper-V 및 VMWare Linux 게스트 VM의 VM 복원 </br></br> *Azure VM에서 파일 일치 백업을 사용할 수 없음*  |
| Azure IaaS VM Backup |[사전 스크립트 및 사후 스크립트 프레임워크](backup-azure-linux-app-consistent.md)를 사용하여 응용 프로그램 일치 백업<br/> [세분화된 파일 복구](backup-azure-restore-files-from-vm.md)<br/> [모든 VM 디스크 복원](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [VM 복원](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Azure Backup에서 Premium Storage VM 사용
Azure Backup은 Premium Storage VM을 보호합니다. Azure 프리미엄 저장소는 SSD (반도체 드라이브)-저장소 설계 toosupport O 집중형 작업 부하를 기반으로 합니다. VM(가상 컴퓨터) 워크로드에 유용합니다. 프리미엄 저장소에 대 한 자세한 내용은 hello 문서 참조 [프리미엄 저장소: Azure 가상 컴퓨터 워크 로드 용 고성능 저장소](../storage/common/storage-premium-storage.md)합니다.

### <a name="back-up-premium-storage-vms"></a>Premium Storage VM 백업
프리미엄 저장소 Vm hello 백업 서비스에 백업 임시 준비 위치를 만드는 동안 이름이 "azure 백업-" hello 프리미엄 저장소 계정에서입니다. 스테이징 위치 hello hello 크기는 hello 복구 지점 스냅숏의 같은 toohello 크기입니다. 프리미엄 저장소 계정의 hello 여유 공간이 충분 tooaccommodate hello 임시 스테이징 위치에 있어야 합니다. 자세한 내용은 hello 문서 참조 [프리미엄 저장소 제한](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)합니다. Hello 백업 작업이 완료 되 면 hello 스테이징 위치 삭제 됩니다. hello hello 스테이징 위치에 사용 되는 저장소의 가격이 모두와 일치 [프리미엄 저장소 가격](../storage/common/storage-premium-storage.md#pricing-and-billing)합니다.

> [!NOTE]
> Hello 스테이징 위치를 편집 하거나 수정 하지 마십시오.
>
>

### <a name="restore-premium-storage-vms"></a>Premium Storage VM 복원
프리미엄 저장소 Vm 복원된 tooeither 프리미엄 저장소 또는 toonormal 저장 될 수 있습니다. 복원의 hello 일반적인 프로세스를를 프리미엄 저장소 VM 복구 지점 백 tooPremium 저장소를 복원 합니다. 그러나 비용 효율적인 toorestore 프리미엄 저장소 VM 복구 지점 toostandard 저장소 수 있습니다. Hello VM에서에서 파일의 하위 집합을 사용 해야 할 경우이 사용할 수 있습니다.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Azure Backup으로 Managed Disks VM 사용
Azure Backup은 Managed Disks VM을 보호합니다. Managed Disks를 사용하면 가상 컴퓨터의 저장소 계정을 관리하지 않아도 되며 VM 프로비전이 매우 간소화됩니다.

### <a name="back-up-managed-disk-vms"></a>Managed Disks VM 백업
VM을 Managed Disks에 백업하는 것은 Resource Manager VM을 백업하는 것과 다르지 않습니다. Hello Azure 포털에서에서 hello 가상 컴퓨터 보기에서 직접 hello 백업 작업을 구성할 수도 있고 hello 복구 서비스에서 보기를 자격 증명 모음 키를 누릅니다. Managed Disks에 VM 백업은 Managed Disks를 기반으로 구축된 RestorePoint 컬렉션을 통해 지원됩니다. Azure Backup도 Azure Disk Encryption(ADE)을 사용하여 암호화된 Managed Disks VM을 백업하도록 지원합니다.

### <a name="restore-managed-disk-vms"></a>Managed Disks VM 복원
Azure 백업을 사용 하면 관리 되는 디스크를 사용 하 여 전체 VM toorestore 또는 관리 되는 디스크 tooa 저장소 계정을 복원 합니다. Azure는 hello 복원 프로세스 중 관리 되는 hello 디스크를 관리합니다. 있습니다 (hello 고객) hello 복원 프로세스의 일부로 만들어진 hello 저장소 계정을 관리 합니다. 관리 되는 암호화 된 Vm을 복원 하는 중 때 hello VM의 키와 암호에에서 있어야 hello 주요 자격 증명 모음 이전 toostarting hello 복원 작업 합니다.

## <a name="what-are-hello-features-of-each-backup-component"></a>각 백업 구성 요소 hello 기능 이란?
다음 섹션 hello hello 가용성 또는 각 Azure 백업 구성 요소에서 다양 한 기능 지원을 요약 하는 테이블을 제공 합니다. 추가 지원 또는 세부 정보에 대 한 각 표의 hello 정보를 참조 하십시오.

### <a name="storage"></a>저장소
| 기능 | Azure Backup 에이전트 | System Center DPM | Azure Backup 서버 | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| Recovery Services 자격 증명 모음 |![예][green] |![예][green] |![예][green] |![예][green] |
| 디스크 저장소 | |![예][green] |![예][green] | |
| 테이프 저장소 | |![예][green] | | |
| 압축 <br/>(Recovery Services 자격 증명 모음에서) |![예][green] |![예][green] |![예][green] | |
| 증분 백업 |![예][green] |![예][green] |![예][green] |![예][green] |
| 디스크 중복 제거 | |![부분적으로][yellow] |![부분적으로][yellow] | | |

![테이블 키](./media/backup-introduction-to-azure-backup/table-key.png)

hello 복구 서비스 자격 증명 모음에는 모든 구성 요소에서 hello 원하는 저장소 대상입니다. System Center DPM 및 Azure 백업 서버도 복사본을 제공 hello 옵션 toohave 로컬 디스크입니다. 그러나 System Center DPM hello 옵션 toowrite 데이터 tooa 테이프 저장 장치를 제공합니다.

#### <a name="compression"></a>압축
백업 압축 tooreduce hello 저장 공간이 필요 합니다. 압축을 사용 하지 않는 hello 유일한 구성 요소는 hello VM 확장입니다. hello VM 확장 복사본에서 모든 백업 데이터를 저장소 계정 toohello 복구 서비스 자격 증명 모음에 동일한 지역을 hello 합니다. 압축 되지 않습니다는 hello 데이터를 전송할 때 사용 됩니다. 사용 하는 hello 저장소를 팽창 약간 압축 되지 않고 hello 데이터를 전송 합니다. 그러나 더 빠른 복원에 대 한 압축 허용 하지 않고 hello 데이터를 저장, 필요한 경우에 해당 복구 지점입니다.


#### <a name="disk-deduplication"></a>디스크 중복 제거
[Azure Backup Server 가상 컴퓨터에서](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx) System Center DPM 또는 Azure Backup Server를 배포할 때 중복 제거를 활용할 수 있습니다. Windows Server 백업 저장소로 연결 된 toohello 가상 컴퓨터는 가상 하드 디스크 (Vhd)에 hello 호스트 수준에서 데이터 중복 제거를 수행 합니다.

> [!NOTE]
> Azure에서 중복 제거를 모든  Backup 구성 요소에 제공하지는 않습니다. System Center DPM 및 백업 서버는 Azure에서 배포 된 경우 hello 저장소 디스크 연결 toohello VM 중복 될 수 없습니다.
>
>

### <a name="incremental-backup-explained"></a>증분 백업 설명
모든 Azure 백업 구성 요소는 hello 대상 저장소 (예: 디스크, 테이프, 복구 서비스 자격 증명 모음)에 상관 없이 증분 백업을 지원합니다. 증분 백업을 하면 백업 저장소와 시간을 효율적으로 hello 마지막 백업 이후 수행 된 변경 내용만 전송 하 여 됩니다.

#### <a name="comparing-full-differential-and-incremental-backup"></a>전체, 차등 및 증분 백업 비교

저장소 사용량, 복구 시간 목표(RTO) 및 네트워크 사용량은 각 유형의 백업 방법마다 다양합니다. tookeep hello 백업 총 소유 비용 (TCO) 아래로, 필요한 toounderstand 어떻게 toochoose hello 최상의 백업 솔루션입니다. 다음 이미지는 hello 전체 백업, 차등 백업 및 증분 백업을 비교 합니다. Hello 이미지 A 10 저장소로 이루어져 데이터 소스는 A1 A10 매월으로 백업 되는 차단 됩니다. 블록 A2, A3, A4, 및 A9 hello에 첫 번째 월을 변경 하 고 달 hello A5 변경을 차단 합니다.

![백업 방법에 대한 비교를 보여주는 이미지](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

와 **전체 백업**, 각 백업 복사본 hello 전체 데이터 원본을 포함 합니다. 전체 백업은 백업 복사본이 전송될 때마다 대량의 네트워크 대역폭과 저장소가 사용됩니다.

**차등 백업** hello 초기 전체 백업 이후 변경, 그 결과 적은 양의 저장소 및 네트워크 소비 하는 hello 차단에 저장 합니다. 차등 백업은 변경되지 않은 데이터의 중복 복사본을 유지하지 않습니다. 그러나 후속 백업 간에 변경 되지 않은 상태로 유지 하는 hello 데이터 블록 전송 되 고 저장, 하므로 차등 백업의 효율적인 받지 않습니다. Hello에 두 번째 달 A2, A3, A4, 및 A9 변경 된 블록에 백업 됩니다. Hello 세 번째 달 이러한 동일한 블록은 백업 다시 변경 된 블록이 A5. 블록을 변경 하는 hello toobe 백업 될 때까지 hello 다음 전체 백업이 수행 되는 작업을 계속 합니다.

**증분 백업을** 만 hello hello 이전 백업 이후에 변경 된 데이터 블록을 저장 하 여 저장소 및 네트워크에 대 한 높은 효율성을 얻을 수 있습니다. 증분 백업을 사용 하 여 필요는 없습니다 tootake 정기적으로 전체 백업 합니다. Hello 예제에서는 첫 번째 월 hello에 대 한 전체 백업 hello을 가져온 직후 변경 된 블록 A2, A3, A4, 및 A9로 표시 된 변경 및 두 번째 달 hello에 대 한 전송 합니다. Hello에 세 번째 달 블록 a 5가 표시 하 고 전송만 변경 합니다. 적은 데이터를 이동하면 저장소 및 네트워크 리소스가 절약되어 TCO가 감소됩니다.   

### <a name="security"></a>보안
| 기능 | Azure Backup 에이전트 | System Center DPM | Azure Backup 서버 | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| 네트워크 보안<br/> (tooAzure) |![예][green] |![예][green] |![예][green] |![부분적으로][yellow] |
| 데이터 보안<br/> (Azure에서) |![예][green] |![예][green] |![예][green] |![부분적으로][yellow] |

![테이블 키](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>네트워크 보안
복구 서비스 자격 증명 모음에 서버 toohello 프로그램의 모든 백업 트래픽이 고급 암호화 표준 256을 사용 하 여 암호화 됩니다. hello 백업 데이터 보안 HTTPS 연결을 통해 전송 됩니다. hello 백업 데이터는 암호화 된 형태로 hello 복구 서비스 자격 증명 모음에도 저장 됩니다. 만 hello Azure 고객 hello 암호 toounlock이이 데이터가 있는 경우 Microsoft는 언제 든 지 hello 백업 데이터를 해독할 수 없습니다.

> [!WARNING]
> Hello 복구 서비스 자격 증명 모음을 설정 하면 액세스 toohello 암호화 키를만 합니다. Microsoft는 하지 암호화 키의 복사본을 유지 관리 및 액세스 toohello 키가 없습니다. Hello 키, 위치가 잘못 된 Microsoft hello 백업 데이터를 복구할 수 없습니다.
>
>

#### <a name="data-security"></a>데이터 보안
Azure Vm을 백업 하려면 암호화를 설정 해야 *내* hello 가상 컴퓨터. Windows 가상 컴퓨터에서는 BitLocker를 사용하고 Linux 가상 컴퓨터에서는 **dm-crypt**를 사용합니다. Azure Backup은 이 경로를 통해 제공되는 백업 데이터를 자동으로 암호화하지 않습니다.

### <a name="network"></a>네트워크
| 기능 | Azure Backup 에이전트 | System Center DPM | Azure Backup 서버 | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| 네트워크 압축 <br/>(너무**백업 서버**) | |![예][green] |![예][green] | |
| 네트워크 압축 <br/>(너무**복구 서비스 자격 증명 모음에**) |![예][green] |![예][green] |![예][green] | |
| 네트워크 프로토콜 <br/>(너무**백업 서버**) | |TCP |TCP | |
| 네트워크 프로토콜 <br/>(너무**복구 서비스 자격 증명 모음에**) |HTTPS |HTTPS |HTTPS |HTTPS |

![테이블 키](./media/backup-introduction-to-azure-backup/table-key-2.png)

hello (hello IaaS VM)에서 VM 확장 데이터를 읽습니다 hello는 hello Azure 저장소 계정에서 직접 hello 저장소 네트워크를 통해 필요한 toocompress 되기 때문이 트래픽을.

System Center DPM 서버 또는 Azure 백업 서버는 보조 백업 서버를 사용 하면 백업 서버를 toohello hello 주 서버에서 이동 하는 hello 데이터를 압축 합니다. 대역폭을 절감할 tooDPM 또는 Azure 백업 서버를 백업 하기 전에 데이터를 압축 합니다.

#### <a name="network-throttling"></a>네트워크 제한
데이터 전송 시 네트워크 대역폭을 어떻게 사용 되는지 toocontrol 수 있는 네트워크 제한 hello Azure 백업 에이전트에서 제공 합니다. 제한 작업 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용할 수 있습니다. 데이터에 대 한 조정을 전송 tooback를 적용 하 고 활동을 복원 합니다.

## <a name="backup-and-retention"></a>백업 및 보존

Azure Backup에는 *보호된 인스턴스*당 최대 9999개 복구 지점(백업 복사본 또는 스냅숏이라고도 함)이 있습니다. 보호 된 인스턴스는 컴퓨터, 서버 (실제 또는 가상) 또는 데이터 tooAzure 구성 하는 작업 tooback입니다. 자세한 내용은 hello 섹션을 참조 하십시오. [보호 된 인스턴스를 이란](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)합니다. 데이터의 백업 복사본이 저장되면 인스턴스가 보호됩니다. 데이터의 백업 복사본 hello hello 보호 됩니다. Hello 원본 데이터 손실 되었거나 손상 되었습니다 hello 백업 복사본 hello 원본 데이터를 복원할 수 없습니다. hello 다음 표에 각 구성 요소에 대 한 최대 백업 빈도 hello 있습니다. 백업 정책 구성 hello 복구 지점을 사용 하는 속도 결정 합니다. 예를 들어 매일 복구 지점을 만들면 복구 지점을 27년 동안 보존한 후 실행합니다. 매월 복구 지점에 수행 하는 경우을 실행 하기 전에 833 년에 대 한 복구 지점을 유지할 수 있습니다. hello 백업 서비스에는 복구 지점에 만료 시간 제한을 설정 하지 않습니다.

|  | Azure Backup 에이전트 | System Center DPM | Azure Backup 서버 | Azure IaaS VM Backup |
| --- | --- | --- | --- | --- |
| 백업 주기<br/> (tooRecovery 서비스 자격 증명 모음) |매일 3회 백업 |하루에 두 번 백업 |하루에 두 번 백업 |매일 1회 백업 |
| 백업 주기<br/> (toodisk) |해당 없음 |<li>SQL Server에 대해 15분마다 <li>다른 워크로드에 대해 1시간마다 |<li>SQL Server에 대해 15분마다 <li>다른 워크로드에 대해 1시간마다</p> |해당 없음 |
| 보존 옵션 |매일, 매주, 매월, 매년 |매일, 매주, 매월, 매년 |매일, 매주, 매월, 매년 |매일, 매주, 매월, 매년 |
| 보호된 인스턴스당 최대 복구 지점 |9999|9999|9999|9999|
| 최대 보존 기간 |백업 빈도에 따라 다름 |백업 빈도에 따라 다름 |백업 빈도에 따라 다름 |백업 빈도에 따라 다름 |
| 로컬 디스크의 복구 지점 |해당 없음 |<li>파일 서버의 경우 64<li>응용 프로그램 서버의 경우 448 |<li>파일 서버의 경우 64<li>응용 프로그램 서버의 경우 448 |해당 없음 |
| 테이프의 복구 지점 |해당 없음 |Unlimited |해당 없음 |해당 없음 |

## <a name="what-is-a-protected-instance"></a>보호된 인스턴스란 무엇인가요?
보호 된 인스턴스는 일반 참조 tooa Windows 컴퓨터, 서버 (실제 또는 가상) 또는 구성 된 tooback tooAzure 구성 된 SQL 데이터베이스입니다. 인스턴스는 hello 컴퓨터, 서버 또는 데이터베이스에 대 한 백업 정책을 구성 하 고 hello 데이터의 백업 복사본을 만들 보호 됩니다. (이라고 하는 복구 지점) 해당 보호 된 인스턴스에 대 한 hello 백업 데이터의 후속 복사본 hello 사용 되는 저장소 양을 늘립니다. 보호 된 인스턴스에 대 한 복구 지점을 too9999 만들 수 있습니다. 저장소에서 복구 지점을 삭제 하면 hello 9999 복구 지점 합계에 대 한 계산 하지 않습니다.
보호 된 인스턴스 중 몇 가지 일반적인 예는 가상 컴퓨터, 응용 프로그램 서버, 데이터베이스 및 hello Windows 운영 체제를 실행 하는 개인용 컴퓨터 됩니다. 예:

* Hello Hyper-v 또는 Azure IaaS 하이퍼바이저 패브릭을 실행 하는 가상 컴퓨터. hello 가상 컴퓨터에 대 한 hello 게스트 운영 체제는 Windows Server 또는 Linux 수 있습니다.
* 응용 프로그램 서버: hello 응용 프로그램 서버는 물리적 컴퓨터 또는 toobe 백업 해야 하는 데이터와 함께 Windows Server 및 워크 로드를 실행 하는 가상 컴퓨터 일 수 있습니다. 일반적인 작업에는 Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server 및 Windows Server에서 hello 파일 서버 역할은 합니다. tooback System Center Data Protection Manager (DPM) 또는 Azure 백업 서버 해야 이러한 워크 로드를 합니다.
* 개인용 컴퓨터, 워크스테이션 또는 노트북 hello Windows 운영 체제를 실행 합니다.


## <a name="what-is-a-recovery-services-vault"></a>Recovery Services 자격 증명 모음이란?
복구 서비스 자격 증명 모음은 Azure의 온라인 저장소 엔터티를 사용 하는 백업 정책, 백업 복사본 및 복구 지점 등 toohold 데이터입니다. Azure 서비스와 온-프레미스 서버와 워크스테이션에 대 한 복구 서비스 자격 증명 모음 toohold 백업 데이터를 사용할 수 있습니다. 복구 서비스 자격 증명 모음 쉽게 tooorganize 쉬운 관리 오버 헤드를 최소화 하는 동안 백업 데이터를 합니다. 구독 내에서 Recovery Services 자격 증명 모음을 원하는 만큼 만들 수 있습니다.

Azure 서비스 관리자에 기반을 백업 자격 증명 모음 자격 증명 모음의 hello hello 첫 번째 버전 이었습니다. 복구 서비스 자격 증명 모음을 hello Azure 리소스 관리자의 모델 기능을 추가 하는 hello hello 자격 증명 모음의 두 번째 버전입니다. Hello 참조 [복구 서비스 자격 증명 모음 개요 문서](backup-azure-recovery-services-vault-overview.md) hello 기능 차이점에 대 한 전체 설명은 대 한 합니다. 만들 수 없습니다 더 이상 사용 하 여 hello 포털 toocreate 백업 자격 증명 모음은, 하지만 백업 자격 증명 모음은 계속 지원 합니다.

> [!IMPORTANT]
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> **2017 년 10 월 15**, 수 toouse PowerShell toocreate 백업 자격 증명 모음은 더 이상 됩니다. <br/> **2017년 11월 1일까지**:
>- 나머지 모든 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Azure Backup은 Azure Site Recovery와 어떻게 다른가요?
Azure Backup 및 Azure Site Recovery는 모두 데이터를 백업하고 해당 데이터를 복원할 수 있다는 점에서 서로 관련되어 있습니다. 그러나 이러한 서비스에는 비즈니스 연속성과 재해 복구를 비즈니스에 제공하는 데 있어 다른 목적이 있습니다. Azure 백업 tooprotect를 사용 하 고 보다 세부적인 수준에서 데이터를 복원 합니다. 예를 들어 랩톱에서 프레젠테이션 손상 된 경우 Azure 백업 toorestore hello 프레젠테이션을 사용 합니다. 다른 데이터 센터 전체의 tooreplicate hello 구성 및 VM에서 데이터를 하려는 경우 Azure Site Recovery를 사용 합니다.

Azure 백업은 온-프레미스 데이터를 보호 하 고 hello 클라우드에서 합니다. Azure Site Recovery는 가상 컴퓨터 및 실제 서버의 복제, 장애 조치 및 복구를 조정합니다. 두 서비스는 재해 복구 솔루션이 필요한 tookeep 데이터 안전 하 고 복구 가능 (백업) 때문에 중요 *및* 중단이 발생할 때 사용할 수 있는 작업 (사이트 복구)를 유지 합니다.

hello 개념을 다음 백업 및 재해 복구 주위 중요 한 결정을 내릴 수 있습니다.

| 개념 | 세부 정보 | 백업 | 재해 복구(DR) |
| --- | --- | --- | --- |
| 복구 지점 목표(RPO) |복구를 수행 하는 toobe 있어야 하는 경우 사용할 수 있는 데이터 손실의 hello 양입니다. |백업 솔루션은 허용되는 RPO에 큰 변동성을 가집니다. 데이터베이스 백업은 최소 15분 정도의 RPO를 갖는 반면 가상 컴퓨터 백업은 대개 1일이라는 RPO를 가집니다. |재해 복구 솔루션은 RPO가 낮습니다. hello DR 복사본 몇 초 또는 몇 분 뒤에 있을 수 있습니다. |
| 복구 시간 목표(RTO) |복구 또는 복원 toocomplete 걸리는 시간의 hello 양입니다. |더 큰 RPO hello 양의 데이터를 백업 솔루션 tooprocess를 해야 하는 hello 때문에 훨씬 더 일반적으로 toolonger Rto 잠재 고객입니다. 예를 들어 걸릴 수 일 tootransport hello 테이프 오프 사이트 위치에서 걸리는 hello 시간에 따라 테이프에서 toorestore 데이터. |재해 복구 솔루션 더 동기화 되어 hello 원본과 때문에 더 작은 Rto를 갖습니다. 변경 사항이 적으므로 toobe 처리 해야 합니다. |
| 보존 |데이터 저장 toobe 해야 하는 기간 |작업 복구(데이터 손상, 실수로 인한 파일 삭제, OS 오류)가 필요한 경우 백업 데이터는 일반적으로 최대 30일 동안 보존됩니다.<br>규정 준수의 관점에서 데이터 toobe 월 또는 연도 대 한 저장 해야 합니다. 이러한 경우에 보관을 위해 백업 데이터가 이상적입니다. |재해 복구에 몇 시간이 나 tooa 시간을 몇 가지 걸리는 작업 복구 데이터만 필요 합니다. Hello 세분화 된 데이터 캡처 DR 솔루션에서 사용으로 인해 DR 데이터를 사용 하 여 장기 보존을 위해 권장 되지 않습니다. |

## <a name="next-steps"></a>다음 단계
Windows Server에서 데이터를 보호 하거나 보호 하는 가상 컴퓨터 (VM)에 대 한 자세한 단계별, 지침에 대 한 자습서를 따라 hello 중 하나를 사용 하 여 Azure에서:

* [파일 및 폴더 백업](backup-try-azure-backup-in-10-mins.md)
* [Azure Virtual Machines 백업](backup-azure-vms-first-look-arm.md)

다른 워크로드를 보호하는 방법에 대한 자세한 내용은 다음 문서 중 하나를 사용하세요.

* [Windows Server 백업](backup-configure-vault.md)
* [응용 프로그램 워크로드 백업](backup-azure-microsoft-azure-backup.md)
* [Azure IaaS VM Backup](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
