---
title: "aaaSAP HANA Azure 백업 스냅숏을 기반으로 저장소 | Microsoft Docs"
description: "Azure 가상 컴퓨터에는 SAP HANA에 대한 두 가지 주요 백업 방법이 있습니다. 이 문서에서는 저장소 스냅숏에 기반한 SAP HANA 백업에 대해 설명합니다"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>저장소 스냅숏에 기반한 SAP HANA 백업

## <a name="introduction"></a>소개

이 문서는 3부로 구성된 SAP HANA 백업 관련 문서 시리즈의 일부입니다. [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md) 시작, 대 한 개요 및 정보를 제공 하 고 [SAP HANA Azure에 백업 파일 수준](sap-hana-backup-file-level.md) 표지 hello 파일 기반 백업 옵션입니다.

단일 인스턴스 내부에서 올인원 데모 시스템에 대 한 VM 백업 기능을 사용할 경우 HANA 백업 hello 운영 체제 수준에서 관리 하는 대신 VM 백업을 수행 하나를 고려해 야 합니다. 연결 된 tooa 가상 컴퓨터에 있으며 hello HANA 데이터 파일을 보관할 수 있는 개별 가상 디스크의 tootake Azure blob 스냅숏을 toocreate 복사본 것이 좋습니다. 하지만 중요 한 점은 hello 시스템이 가동 하는 동안 VM 백업 또는 디스크 스냅숏 생성 및 실행 하는 경우 응용 프로그램 일관성을 유지 합니다. 참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다. SAP HANA에는 이러한 종류의 저장소 스냅숏을 지원하는 기능이 있습니다.

## <a name="sap-hana-snapshots"></a>SAP HANA 스냅숏

저장소 스냅숏 만들기를 지원하는 SAP HANA 기능이 있습니다. 그러나 2016 년 12 월을 기준으로 제한이 됩니다 toosingle 컨테이너 시스템. 다중 테넌트 컨테이너 구성에서는 이러한 종류의 데이터베이스 스냅숏을 지원하지 않습니다([저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문) 참조).

다음과 같이 작동합니다.

- Hello SAP HANA 스냅숏 시작 하 여 저장소 스냅숏에 대 한 준비
- Hello 저장소 스냅숏 (스냅숏, 예를 들어 Azure blob)를 실행 합니다.
- SAP HANA 스냅숏 hello를 확인 합니다.

![SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 주는 스크린샷](media/sap-hana-backup-storage-snapshots/image011.png)

이 스크린샷에서는 SQL 문을 통해 SAP HANA 데이터 스냅숏을 만들 수 있음을 보여 줍니다.

![다음에 스냅숏 hello SAP HANA Studio에서 백업 카탈로그 hello에에서도 나타납니다.](media/sap-hana-backup-storage-snapshots/image012.png)

그런 다음 스냅숏을 hello SAP HANA Studio에서 백업 카탈로그 hello에에서도 나타납니다.

![디스크에 스냅숏 hello에에서 표시 hello SAP HANA 데이터 디렉터리](media/sap-hana-backup-storage-snapshots/image013.png)

디스크에 hello 스냅숏 표시 hello SAP HANA 데이터 디렉터리에 됩니다.

SAP HANA hello 스냅숏 준비 모드에 있는 동안 hello 저장소 스냅숏을 실행 하기 전에 hello 파일 시스템 일관성 보장이 tooensure에 하나 있습니다. 참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다.

Hello 저장소 스냅숏 작업이 완료 되 면은 중요 한 tooconfirm hello SAP HANA 스냅숏입니다. 해당 SQL 문이 toorun: 백업 데이터 닫기 스냅숏을 (참조 [백업 데이터 닫기 스냅숏 문 (백업 및 복구)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Hello HANA 스냅숏을 확인 합니다. 기한 너무&quot;쓰기 시 복사&quot; 모드에서 추가 디스크 공간이 스냅숏-준비 하 고 hello SAP HANA 스냅숏 확인 될 때까지 새 백업을 가능한 toostart는 SAP HANA 필요할 수 있습니다.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Azure Backup 서비스를 통한 HANA VM 백업

2016 년 12 월을 기준으로 hello Azure 백업 서비스의 hello 백업 에이전트를 Linux Vm에 사용할 수 없습니다. Azure 백업 사용할 toomake hello 파일/디렉터리 수준에서 하나는 SAP HANA 백업 파일 tooa Windows VM 복사한 다음 hello 백업 에이전트를 사용 하 여 합니다. 그렇지 않으면 전체 Linux VM 백업만 hello Azure 백업 서비스를 통해 불가능합니다. 참조 [hello의 개요 기능 Azure 백업에서](../../../backup/backup-introduction-to-azure-backup.md) 자세히 toofind 합니다.

Azure 백업 서비스 hello 최대 옵션 tooback 제공 하 고 VM을 복원 합니다. 이 서비스 및 작동 방식에 대 한 자세한 내용은 hello 문서에서 참조할 수 있습니다 [Azure에서 VM 백업 인프라 계획](../../../backup/backup-azure-vms-introduction.md)합니다.

Toothat 문서에 따라 두 가지 중요 한 고려 사항이 있습니다.

_&quot;Linux 가상 컴퓨터에만 파일에 일관적인 백업은 가능 Linux 동등한 플랫폼 tooVSS 없기 때문입니다.&quot;_

_&quot;응용 프로그램 필요 tooimplement 자신의 &quot;픽스업&quot; 메커니즘 hello에 데이터를 복원 합니다.&quot;_

따라서 하나 toomake hello 백업이 시작 될 때 SAP HANA이 디스크에서 일관 된 상태에 있는지에 있습니다. 참조 _SAP HANA 스냅숏을_ hello 문서의 앞부분에 설명 합니다. 그러나 SAP HANA에서 이 스냅숏 준비 모드를 유지할 때 잠재적인 문제가 있습니다. 자세한 내용은 [저장소 스냅숏 만들기(SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)(영문)을 참조하세요.

이 문서에서는 다음과 같이 설명하고 있습니다.

_&quot;것 tooconfirm이 가장 좋습니다 또는 만들어진 후 저장소 스냅숏을 가능한 한 빨리 중단. Hello 저장소 스냅숏 준비를 하 고 또는 hello 생성 하는 동안 스냅숏 관련 데이터 고정 필드입니다. Hello 스냅숏 관련 데이터 중지 된 동안 hello 데이터베이스에 변경 내용이 여전히 가능 합니다. 이러한 변경 내용이 변경 된 스냅숏 관련 데이터 toobe 고정 hello를 발생 하지 않습니다. 대신, hello 변경 내용이 toopositions hello 저장소 스냅숏에서 분리 된 hello 데이터 영역에 기록 합니다. 변경 내용은 toohello 로그도 기록 됩니다. 그러나 hello 긴 hello 스냅숏 관련 데이터의 고정 유지, 데이터 볼륨 증가할 수 있는 더 많은 hello hello.&quot;_

Azure 백업은 Azure VM 확장을 통해 파일 시스템 일관성 hello 담당합니다. 이러한 VM 확장은 독립 실행형으로 제공되지 않으며 Azure Backup 서비스와 함께 사용해야 합니다. 그럼에도 불구 하 고 요구 사항 toomanage는 SAP HANA 스냅숏 tooguarantee 응용 프로그램 일관성은 계속 합니다.

Azure Backup에는 다음 두 가지 주요 단계가 있습니다.

- 스냅숏 만들기
- 전송 데이터 toovault

스냅숏을 만드는의 hello Azure 백업 서비스 단계가 완료 되 면 hello SAP HANA 스냅숏을 확인 될 수 있습니다 하나 있습니다. Hello Azure 포털에서에서 몇 분 toosee를 걸릴 수 있습니다.

![이 그림 hello 백업 작업 목록이 Azure 백업 서비스의 일부를 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image014.png)

이 그림에서는 hello 백업 작업 목록이 사용 되는 tooback hello HANA 테스트 VM 하 던는 Azure 백업 서비스의 일부를 보여 줍니다.

![tooshow hello 작업 세부 정보 클릭 hello hello Azure 포털에서에서 백업 작업](media/sap-hana-backup-storage-snapshots/image015.png)

tooshow hello 작업 세부 정보는 hello hello Azure 포털에서에서 백업 작업을 클릭 합니다. 여기에서는 두 개의 단계로 hello를 볼 수 하나. Hello 스냅숏 단계를 완료 됨으로 표시할 때까지 몇 분 정도 걸릴 수 있습니다. 대부분의 hello hello 데이터 전송 단계에서 소비 됩니다.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Azure Backup 서비스를 통한 HANA VM 백업 자동화

앞에서 설명한 대로 hello Azure 백업 스냅숏 단계 완료 되 면 관리자 hello Azure 포털에서에서 백업 작업 목록 hello를 모니터링할 수 없다는 것이 도움이 tooconsider 자동화 되므로 hello SAP HANA 스냅숏을 수동으로 확인 될 수 있습니다 하나 있습니다.

다음은 Azure PowerShell cmdlet을 통해 이 기능을 수행할 수 있는 방법에 대해 설명합니다.

![Hello 이름 hana-백업-자격 증명 모음는 Azure 백업 서비스를 만들었습니다.](media/sap-hana-backup-storage-snapshots/image016.png)

Hello 이름으로는 Azure 백업 서비스를 만든 &quot;hana-백업-자격 증명 모음&quot; PS 명령 hello **Get AzureRmRecoveryServicesVault-hana-백업-자격 증명 모음 이름을** 검색 hello 해당 하는 개체입니다. 이 개체에 있으면 hello 다음 그림에 표시 된 대로 사용 되는 tooset hello 백업 컨텍스트.

![Hello 현재 진행 중인 백업 작업을 확인할 수 있습니다 하나](media/sap-hana-backup-storage-snapshots/image017.png)

설정 hello 올바른 컨텍스트 후 hello 현재 진행 중인 백업 작업에 대 한 확인 하 고 작업 세부 정보를 찾습니다 수 하나. hello 하위 태스크 목록은 hello 백업 작업을 Azure의 hello 스냅숏 단계가 이미 완료 되었는지 여부를 보여줍니다.

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![TooCompleted 설정 될 때까지 루프에서 폴링 hello 값](media/sap-hana-backup-storage-snapshots/image018.png)

Hello 작업 세부 정보는 변수에으로 저장 되 고 나면 단순히 PS 구문 tooget toohello 첫 번째 배열 항목 되며 hello 상태 값을 검색 합니다. toocomplete hello 자동화 스크립트 될 때까지 루프에서 폴링 hello 값 이면 너무&quot;완료 합니다.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Azure Backup 서비스를 통한 HANA 라이선스 키 및 VM 복원

hello Azure 백업 서비스는 설계 된 새 VM toocreate 복원 중입니다. 계획은 없습니다 지금은 toodo는 &quot;내부&quot; 기존 Azure VM의 복원 합니다.

![이 그림은 hello Azure 포털에서에서 hello Azure 서비스의 hello 복원 옵션을 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image019.png)

이 그림 hello Azure 포털에서에서 hello Azure 서비스의 hello 복원 옵션을 보여 줍니다. 하나 복원 하는 동안 VM을 만들거나 hello 디스크 복원 중에서 선택할 수 있습니다. Hello 디스크를 복원한 후 것이 여전히 필요한 toocreate 그 위에 새 VM 합니다. Azure의 hello 고유한 VM ID 변경 내용에 새 VM 생성 될 때마다 (참조 [액세스 및 Azure VM 고유 ID를 사용 하 여](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![이 그림 이전 및 Azure 백업 서비스를 통해 hello 복원 후 hello Azure VM에 대 한 고유 ID를 보여 줍니다.](media/sap-hana-backup-storage-snapshots/image020.png)

이 그림 전과 후 Azure 백업 서비스를 통해 hello 복원 hello Azure VM에 대 한 고유 ID를 보여 줍니다. hello SAP 하드웨어 키를 사용 되는 SAP 라이선스에 대 한 고유한 VM ID를 사용 하는 이 인해 새 SAP 라이선스에 toobe VM 복원 후에 설치 되어 있습니다.

이 백업 가이드의 hello 생성 중에 새로운 Azure 백업 기능 미리 보기 모드에서 발표 합니다. Hello VM 스냅숏으로 hello VM에 대 한 백업 기반 파일 수준 복원을 수 있습니다. 이 hello 필요 toodeploy 새 VM을 방지할 수 따라서 hello 고유한 VM ID 유지 되며 hello 동일 하 고 새 SAP HANA 라이선스 키가 필요 합니다. 이 기능에 대한 자세한 설명서는 완전히 테스트한 후에 제공될 것입니다.

Azure 백업 결국을 사용 하면 개별 Azure 가상 디스크의 백업 및 파일 및 디렉터리를 내부 hello VM입니다. Azure Backup의 큰 이점이 toodo 하는 것과 hello 고객을 저장 하는 모든 hello 백업 관리는 것입니다. 복원 작업은 필요, Azure 백업는 선택 hello 올바른 백업 toouse 합니다.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>수동 디스크 스냅숏을 통한 SAP HANA VM 백업

Hello Azure 백업 서비스를 사용 하는 대신 PowerShell 통해 수동으로 Azure vhd blob 스냅숏을 만들면 개별 백업 솔루션을 구성할 수 하나 있습니다. 참조 [PowerShell과 함께 사용 하 여 blob 스냅숏을](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) hello 단계의 설명에 대 한 합니다.

유연성을 제공 하지만이 문서의 앞부분에서 설명 하는 hello 문제가 해결 되지 않습니다.

- 여전히 SAP HANA가 일관된 상태인지 확인해야 합니다.
- VM의 할당이 취소 됩니다 내용을 입력 하는 오류가 발생 한 임 대권을 hello 있는 경우에 hello OS 디스크를 덮어쓸 수 없습니다. VM tooa 새 고유 VM ID와 hello 필요 tooinstall 새 SAP 라이선스 이어질 hello 삭제 한 후에 작동 합니다.

![Azure VM의 가능한 toorestore 유일한 hello 데이터 디스크는](media/sap-hana-backup-storage-snapshots/image021.png)

가능한 toorestore 새 고유 VM ID를 가져오는 hello 문제를 방지 하는 Azure VM의 데이터 디스크 에서만 hello 이며, 따라서 hello SAP 라이선스를 무효화:

- Hello 테스트에 대 한 두 개의 Azure 데이터 디스크 연결 된 tooa VM 했으며 소프트웨어 RAID 위쪽에 정의 된 
- SAP HANA 스냅숏 기능을 통해 SAP HANA가 일관된 상태에 있음을 확인했습니다.
- 파일 시스템 고정 (참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md))
- 두 데이터 디스크에서 Blob 스냅숏을 만들었습니다.
- 파일 시스템을 고정 취소했습니다.
- SAP HANA 스냅숏을 확인했습니다.
- 양쪽 디스크가 모두 분리 및 toorestore hello 데이터 디스크 hello VM 종료 되었습니다.
- Hello 이전 blob 스냅숏을 사용한 덮어쓸 된 hello 디스크를 분리 후
- 복원 하는 hello 가상 디스크가 연결 된 다음 다시 toohello VM
- 시작 hello hello 소프트웨어 RAID 제대로 작동 하며 toohello blob 설정 된 모든 VM 스냅숏 시간 후
- HANA 다시 toohello HANA 스냅숏 설정 된

SAP HANA 아래로 가능한 tooshut hello blob 스냅숏 전에 되었으면 hello 프로시저 덜 복잡 한 것입니다. 이 경우 하나 수 hello HANA 스냅숏 건너뛰고, hello 시스템에서 진행 되만 수행 하는 경우 hello 파일 시스템 고정을 건너뛸 수도 있습니다. 복잡 한 추가 온라인 상태 이며 모든 것이 필요한 toodo 스냅숏을 경우 hello 그림으로 제공 됩니다. 참조 _저장소 스냅샷을 사용할 때 SAP HANA 데이터 일관성_ hello 관련된 문서에서 [Azure 가상 컴퓨터에서 SAP HANA에 대 한 백업 가이드](sap-hana-backup-guide.md)합니다.

## <a name="next-steps"></a>다음 단계
* [Azure Virtual Machines의 SAP HANA 백업 가이드](sap-hana-backup-guide.md) - 시작에 대한 개요 및 정보를 제공합니다.
* [SAP HANA 백업 파일 수준에 따라](sap-hana-backup-file-level.md) 표지 hello 파일 기반 백업 옵션입니다.
* tooestablish 고가용성 및 (대형 인스턴스) Azure에서 SAP HANA의 재해 복구 계획의 참조 toolearn [SAP HANA (대형 인스턴스) 고가용성 및 재해 복구 Azure에서](hana-overview-high-availability-disaster-recovery.md)합니다.
