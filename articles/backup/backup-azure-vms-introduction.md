---
title: "aaaPlanning Azure에서 VM 백업 인프라 | Microsoft Docs"
description: "Azure에서 가상 컴퓨터를 tooback를 계획할 때 중요 한 고려 사항"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "vm 백업, virtual machines 백업"
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Azure에서 VM 백업 인프라 계획
이 문서에서는 성능 및 리소스 제안 toohelp VM 백업 인프라를 계획을 제공 합니다. Hello 백업 서비스의 주요 측면을 정의 합니다. 이러한 측면을이 충분히를 해당 아키텍처를 결정 하는 데 사용할 수 있습니다 용량 계획 및 예약 합니다. 선택한 경우 [환경이 준비](backup-azure-vms-prepare.md), hello 다음 단계를 시작 하기 전에 계획은 [vm tooback](backup-azure-vms.md)합니다. Azure 가상 컴퓨터에 대 한 자세한 정보를 보려면 hello 참고 [가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/)합니다.

## <a name="how-does-azure-back-up-virtual-machines"></a>Azure에서 가상 컴퓨터를 백업하는 방법
Azure 백업 서비스 hello가 hello 예약 된 시간에 백업 작업을 시작 hello 예비 내선 번호 tootake를 지정 시간에 스냅숏으로 트리거합니다. Azure 백업 서비스 hello hello를 사용 하 여 _VMSnapshot_ 창과 hello에서 확장 _VMSnapshotLinux_ Linux에서 확장 합니다. hello 확장 hello 첫 번째 VM 백업 하는 동안 설치 됩니다. tooinstall hello 확장 hello VM 실행 되어야 합니다. Hello VM 실행 되지 않는 경우, hello 백업 서비스는 hello (응용 프로그램 쓰기가 수행 되지 hello VM을 중지 하는 동안) 이후 기본 저장소의 스냅숏을 만듭니다.

Windows Vm의 스냅숏을 만드는, hello 백업 서비스 hello 가상 컴퓨터의 디스크의 일관 된 스냅숏을 hello 볼륨 섀도 복사본 서비스 (VSS) tooget와 동등 합니다. Linux Vm을 백업 하는 경우 VM 스냅숏을 만드는 경우 사용자 고유의 사용자 지정 스크립트 tooensure 일관성을 작성할 수 있습니다. 이러한 스크립트 호출에 대한 자세한 내용은 이 문서의 뒷부분에 제공됩니다.

Hello Azure 백업 서비스는 hello 스냅숏을, 되 면 hello 데이터는 전송 된 toohello 자격 증명 모음입니다. toomaximize 효율성 hello 서비스를 식별 하 고 hello 이전 백업 이후에 변경 된 데이터의 hello 블록만 전송 합니다.

![Azure 가상 컴퓨터 백업 아키텍처](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다.

> [!NOTE]
> 1. Hello 백업 프로세스 중 Azure 백업 하지 않습니다 hello 연결 된 임시 디스크 toohello 가상 컴퓨터를 포함 합니다. 자세한 내용은 블로그를 참조 하세요 hello에 [임시 저장소](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)합니다.
> 2. Azure 백업에서는 저장소 수준의 스냅숏 및 스냅숏 toovault 전송, 이후 hello 백업 작업이 완료 될 때까지 hello 저장소 계정 키 변경 하지 마십시오.
> 3. 프리미엄 Vm hello 스냅숏 toostorage 계정에 복사 했습니다. 이 toomake 있는지 Azure 백업 서비스 toovault 데이터를 전송 하는 데 충분 한 IOPS를 가져옵니다. 이 저장소의 추가 복사본 hello VM 할당 크기를 기준으로 대금이 청구 됩니다. 
>

### <a name="data-consistency"></a>데이터 일관성
백업 및 복원 중요 한 비즈니스 데이터 hello 응용 프로그램 데이터를 사용 중인 hello를 생성 하는 동안 중요 한 비즈니스 데이터 백업 해야 하는 hello 팩트 복잡 합니다. tooaddress Windows와 Linux Vm에 대 한이 Azure 백업 지원 응용 프로그램 일치 백업을
#### <a name="windows-vm"></a>Windows VM
Windows VM에서 Azure 백업은 VSS 전체 백업을 사용합니다( [VSS 전체 백업](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)에 대해 자세히 알아보기). tooenable VSS는 백업, hello 레지스트리 키 필요 toobe 집합에 나오는 hello VM에 복사 합니다.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Linux VM
Azure Backup은 스크립팅 프레임워크를 제공합니다. Linux Vm을 백업할 때 tooensure 응용 프로그램 일관성에는 사용자 지정 사전 스크립트 및 사후 스크립트로 hello 백업 워크플로 및 환경 제어 하는 만듭니다. Azure 백업 hello VM 스냅샷을 수행 하기 전에 hello 전 스크립트를 호출 하 고 hello VM 스냅숏 작업이 완료 되 면 hello 후 스크립트를 호출 합니다. 자세한 내용은 [사전 스크립트 및 사후 스크립트를 사용하여 응용 프로그램 일치 VM 백업](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)을 참조하세요.
> [!NOTE]
> Azure 백업에만 hello 고객 작성 호출 사전 및 사후 스크립트로 합니다. Hello 사전 스크립트 및 사후 스크립트로 성공적으로 실행 하는 경우 Azure 백업 hello 복구 지점으로 표시 응용 프로그램 일치 합니다. 그러나 사용자 지정 스크립트를 사용 하는 경우 hello 고객 hello 응용 프로그램 일관성에 대 한 최종 책임은 있습니다.
>


이 표에서 hello 유형의 일관성과 hello 조건에서 Azure VM 백업 하는 동안 발생 하 고 복원 절차를 설명 합니다.

| 일관성 | VSS 기반 | 설명 및 세부 정보 |
| --- | --- | --- |
| 응용 프로그램 일관성 |Windows 경우 예|응용 프로그램 일관성은 다음을 보장하므로 워크로드에 이상적입니다.<ol><li> hello VM *가상 컴퓨터를 부팅*합니다. <li>*손상이 없습니다*. <li>*데이터 손실*이 없습니다.<li> hello 데이터는 백업-VSS 또는 사전/사후 스크립트를 사용 하 여 hello 시 hello 응용 프로그램을 포함 하 여 hello 데이터를 사용 하는 일관 된 toohello 응용 프로그램입니다.</ol> <li>*Windows Vm*-가장 Microsoft 작업 관련된 toodata 일관성 작업 관련 동작을 수행 하는 VSS 기록기가 있습니다. 예를 들어 Microsoft SQL Server hello 쓰기 toohello 트랜잭션 로그 파일 및 hello 데이터베이스 올바르게 수행 되도록 하려면 VSS 기록기를 있습니다. Windows Azure VM 백업, toocreate는 응용 프로그램 일치 복구 지점에 대 한 hello 예비 내선 번호 hello VSS 워크플로 호출 하 고 hello VM 스냅샷을 수행 하기 전에 완료 해야 합니다. Hello Azure VM 스냅샷 toobe 정확 하 게에 대 한 모든 Azure VM 응용 프로그램의 hello VSS 기록기도 완료 해야 합니다. (자세한 hello [VSS의 기본 사항](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) hello 세부 정보를 심층적으로 및 [작동 방식을](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Linux Vm*-고객 실행할 수 있는 [전 스크립트와 사후 스크립트 tooensure 사용자 지정 응용 프로그램 일관성](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)합니다. </li> |
| 파일 시스템 일관성 |예 - Windows 기반 컴퓨터 |두 가지 시나리오 hello 복구 지점이 될 수 있는 *파일 시스템 일관성 있는*:<ul><li>사전 스크립트/사후 스크립트 없이 또는 사전 스크립트/사후 스크립트가 실패한 경우 Azure에서 Linux VM의 백업. <li>Azure에서 Windows VM을 백업하는 중에 VSS 오류가 발생합니다.</li></ul> 두이 경우 모두 수행할 수 있는 최상의 hello는 tooensure입니다. <ol><li> hello VM *가상 컴퓨터를 부팅*합니다. <li>*손상이 없습니다*.<li>*데이터 손실*이 없습니다.</ol> 응용 프로그램에는 복원 hello 데이터에 대해 자신의 "픽스업" tooimplement 메커니즘이 필요합니다. |
| 충돌 일관성 |아니요 |이 상황은 (소프트 또는 하드 리셋)를 통해 발생 하는 "크래시" tooa 해당 가상 컴퓨터입니다. 크래시 일관성에는 일반적으로 백업 hello 시 hello Azure 가상 컴퓨터 종료 될 때 발생 합니다. 크래시 일관성이 있는 복구 지점을 hello 운영 체제 또는 hello 응용 프로그램의 hello 관점에서 hello 저장 매체-에 hello hello 데이터 일관성이 보장은 없습니다를 제공합니다. 백업 hello 시 hello 디스크에 이미 할당 된 hello 데이터만 캡처되고를 백업 합니다. <br/> <br/> 일반적으로 보장 되지 않습니다, 동안 hello 뒤에 디스크를 확인 하 여 운영 체제 부팅 프로시저 chkdsk toofix 처럼 한 손상 오류입니다. 모든 메모리 내 데이터 또는 쓰기에 전송 된 toohello 디스크 않은 손실 됩니다. hello 응용 프로그램 데이터 롤백 toobe 수행 해야 하는 경우에 일반적으로 확인 메커니즘을를 따릅니다. <br><br>예를 들어 hello 트랜잭션 로그에 항목이 hello 데이터베이스에 존재 하지 않는 경우 다음 hello 데이터베이스 소프트웨어에서는 롤백이 hello 데이터가 일관 될 때까지 합니다. 여러 가상 디스크 (예: 스팬된 볼륨)에 걸쳐 분산 되는 데이터는 크래시 일관성 복구 지점 hello 데이터의 hello 정확성에 대 한 보장은 없습니다를 제공 합니다. |

## <a name="performance-and-resource-utilization"></a>성능 및 리소스 사용률
온-프레미스에 배포되는 백업 소프트웨어와 마찬가지로 Azure에서 VM을 백업하는 경우 용량 및 리소스 사용률에 대한 계획을 세워야 합니다. hello [Azure 저장소 제한](../azure-subscription-service-limits.md#storage-limits) toostructure VM 배포 tooget 최대 성능을 최소한으로 toorunning 워크 로드에 영향 방법을 정의 합니다.

백업 성능을 계획할 때 다음 Azure 저장소를 제한 하는 주의 기울여야 toohello 비용을 지불 합니다.

* 저장소 계정당 최대 송신
* 저장소 계정당 총 요청 속도

### <a name="storage-account-limits"></a>저장소 계정 제한
백업 데이터는 저장소 계정에서 복사, toohello 입/출력 작업 IOPS (초당) 및 송신 (또는 처리량) 메트릭 hello 저장소 계정의 수를 추가 합니다. At hello 동일 IOPS 및 처리량에도 시간, 가상 컴퓨터가 사용 하 고 있습니다. hello ´ ֲ tooensure 백업 및 가상 컴퓨터 트래픽 저장소 계정 제한 초과 하지 않도록 합니다.

### <a name="number-of-disks"></a>디스크 수
hello 백업 프로세스는 최대한 빨리 toocomplete 백업 작업을 시도합니다. 이렇게 하면 가능한 많은 리소스를 소모합니다. 그러나 모든 I/O 작업은 hello에 의해 제한 *단일 Blob의 목표 처리량*, 하는 초당 60MB 제한 합니다. 속도가 시도 toomaximize에 hello 백업 프로세스에서 각 hello VM 디스크를 tooback *병렬로*합니다. VM에 4 개의 디스크가, hello 서비스 tooback 동시에 모든 4 개의 디스크를 시도 합니다. hello **디스크 번호** hello 저장소 계정에 대 한 백업 트래픽을 결정 하는 데 가장 중요 한 요소에는 백업 중인 합니다.

### <a name="backup-schedule"></a>백업 일정
성능에 영향을 주는 추가 요소는 hello **백업 일정**합니다. 모든 Vm에서 백업 hello 동일 하므로 hello 정책을 구성 하는 경우 트래픽 걸림은 예정 된 시간입니다. 백업 프로세스 hello tooback 동시에 모든 디스크를 시도합니다. 겹치지 않는 hello 일 서로 다른 시간에 여러 Vm 백업 저장소 계정에서 tooreduce hello의 백업 트래픽을 합니다.

## <a name="capacity-planning"></a>용량 계획
Tooplan hello 저장소 계정 사용 해야 하는 필요 hello 이전 요소를 함께 배치 합니다. Hello 다운로드 [VM 백업 용량 계획 Excel 스프레드시트](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) toosee hello 영향 디스크 및 백업 일정 선택 항목의 합니다.

### <a name="backup-throughput"></a>백업 처리량
백업 중인 각 디스크에 대 한 Azure 백업 hello 디스크에 블록 hello 읽고 저장소에만 변경 된 데이터 (증분 백업) hello 합니다. hello 다음 표에 hello 평균 백업 서비스 처리량 값 있습니다. 같은 데이터가 hello를 사용 하 여 hello 기간 필요한 tooback 지정된 된 크기의 디스크를 예측할 수 있습니다.

| 백업 작업 | 최상의 처리량 |
| --- | --- |
| 초기 백업 |160Mbps |
| 증분 백업(DR) |640Mbps  <br><br> 처리량이 감소 크게 hello에 필요한 다른 데이터 (백업 toobe) 변경 된 경우 분산 된 hello 디스크 간에 합니다.|

## <a name="total-vm-backup-time"></a>총 VM 백업 시간
대부분의 hello 백업 시간 소비 읽는 데이터 복사, 동안 toohello 데 필요한 총 시간은 tooback VM 다른 작업에 기여:

* 시간이 너무 필요[hello 백업 확장을 설치 또는](backup-azure-vms.md)합니다.
* 스냅숏 시간을 hello에 걸린 시간 tootrigger 스냅숏으로 됩니다. 스냅숏은 트리거된 닫기 toohello 예약 된 백업 시간입니다.
* 큐 대기 시간입니다. Hello 백업 서비스가 백업을 여러 고객 으로부터 처리 하 고, 이후 스냅숏 toohello 백업 또는 복구 서비스에서 백업 데이터를 복사 자격 증명 모음을 시작할 수 없습니다 즉시 합니다. 최대 부하 시간, hello 대기는 처리 중인 백업의 toohello 수 인해 tooeight 시간을 늘릴 수 있는 합니다. 그러나 VM 백업 시간을 총 hello는 매일 백업 정책에 대 한 24 시간 보다 작습니다.
* 데이터 전송 시간, 백업에 필요한 시간은 toocompute hello 증분 변경 내용은 이전 백업에서 서비스 및 이러한 변경 내용을 toovault 저장소를 전송 합니다.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>백업 시간이 길어진(12시간 초과) 이유는 무엇인가요?
백업은 다음과 같은 두 단계로 구성 됩니다: 스냅숏 만들기 및 전송 hello 스냅숏을 toohello 자격 증명 모음입니다. hello 백업 서비스 저장소에 대 한 최적화합니다. Hello 스냅숏 데이터 tooa 자격 증명 모음으로 내보낼 때 hello 서비스 hello 이전 스냅숏에서 증분 변경만 전송 합니다.  toodetermine hello 증분 변경 hello 서비스는 hello 블록의 hello 체크섬을 계산합니다. 블록 변경 되 면 hello 블록은 toohello 자격 증명 모음을 전송 하는 블록 toobe로 식별 됩니다. 그런 다음 hello 서비스 드릴 각 hello로 식별 된 블록, 기회 toominimize hello 데이터 tootransfer 찾고 있습니다. 변경 된 모든 블록을 평가한 후 hello 서비스 hello 변경 내용을 결합 하 고 자격 증명 모음 toohello 보냅니다. 일부 레거시 응용 프로그램의 경우 소규모의 조각난 쓰기는 저장소에 적합하지 않습니다. Hello 스냅숏 작은, 조각난 쓰기 작업이 잦은 있으면 hello 서비스 대부분 hello 응용 프로그램에 의해 기록 된 hello 데이터를 처리 하는 추가 시간을 보냅니다. hello VM 내에서 실행 되는 응용 프로그램에 azure에서 응용 프로그램 쓰기 블록을 권장 하는 hello 8KB의 최소값입니다. 응용 프로그램에서 8KB 보다 작은 블록을 사용할 경우 백업 성능에 영향을 미칩니다. 응용 프로그램 tooimprove 백업 성능 조정 도움말을 참조 하십시오. [Azure 저장소의 성능 최적화에 대 한 응용 프로그램 튜닝](../storage/common/storage-premium-storage-performance.md)합니다. 경우에 백업 성능에 hello 문서 프리미엄 저장소 예제를 사용 하는 hello 지침 표준 저장소 디스크에 대 한 적용 됩니다.

## <a name="total-restore-time"></a>총 복원 시간
복원 작업을 두 가지 주요 하위 작업으로 구성 됩니다: hello 자격 증명 모음 선택 toohello 고객 저장소 계정에서 다시 데이터를 복사 하 고 hello 가상 컴퓨터를 만드는 중입니다. Hello 자격 증명 모음에서 다시 데이터를 복사 하는 작업은 hello 백업은 Azure에 내부적으로 저장 되어 있는 hello 고객 저장소 계정 저장 된 등에 따라 다릅니다. Toocopy 데이터에 걸린 시간에 따라 달라 집니다.
* 큐 대기 시간-hello에 여러 고객 으로부터 hello 서비스 프로세스 복원 작업 후 같은 시간 복원 요청은 큐에 저장 합니다.
* 데이터 복사 작업에 시간-hello 자격 증명 모음 toohello 고객 저장소 계정에서 복사 됩니다. 복원 시간은 iops 수에 따라 및 hello 선택한 고객 저장소 계정에 Azure 백업 서비스 처리량을 가져옵니다. tooreduce는 hello 복원 프로세스 중에 시간 복사 hello, 및 다른 응용 프로그램 쓰기 및 읽기 로드 되지 않음 저장소 계정을 선택 합니다.

## <a name="best-practices"></a>모범 사례
가상 컴퓨터에 대한 백업을 구성하는 동안 다음 사례를 따르는 것이 좋습니다.

* 동일한 클라우드 서비스 tooback hello에 hello에서 10 개 이상의 클래식 Vm 예약 안 함 동시 합니다. 동일한 클라우드 서비스에서 여러 vm tooback 하려는 경우 한 시간 hello 백업 시작 시간을 분산 합니다.
* 40 개 이상의 Vm tooback를 hello에 예약 하지 않는 같은 시간입니다.
* 사용량이 많지 않은 시간에 VM 백업을 예약하세요. 이 방식으로 hello 백업 서비스는 hello 고객 저장소 계정 toohello 자격 증명 모음에서 데이터를 전송에 대 한 IOPS를 사용 합니다.
* 정책이 서로 다른 저장소 계정에 분산된 VM에 적용되어야 합니다. 20 개 이하의 제안 hello에 의해 단일 저장소 계정에서 총 디스크 보호 동일한 백업 일정. 20 디스크는 저장소 계정에 확산 하는 보다 큰 경우 해당 Vm에서 여러 정책 tooget 필요한 IOPS hello 백업 프로세스의 hello 전송 단계 동안 hello 합니다.
* 프리미엄 저장소 toosame 저장소 계정에서 실행 하 고 복원 하지 마십시오. Hello 감소 hello 복원 작업 프로세스 hello 백업 작업, 일치 하는 경우 백업에 대 한 IOPS를 사용할 수 있습니다.
* 프리미엄 VM 백업의 경우 프리미엄 디스크를 호스트하는 저장소 계정에 성공적인 백업을 위해 스냅샷 준비에 사용할 50% 이상의 사용 가능한 공간이 있는지 확인합니다. 
* 백업에 사용할 수 있는 Linux VM의 python 버전이 2.7인지 확인합니다.

## <a name="data-encryption"></a>데이터 암호화.
Azure 백업 hello 백업 프로세스의 일부로 데이터를 암호화 하지 않습니다. 그러나 hello VM 내에서 데이터를 암호화할 수 있으며 hello를 백업 데이터 보호 데이터를 원활 하 게 (에 대해 자세히 알아보세요 [암호화 된 데이터의 백업](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>보호 된 인스턴스의 hello 비용 계산
Azure 백업을 통해 백업 된 azure 가상 컴퓨터는 너무[Azure 백업 가격](https://azure.microsoft.com/pricing/details/backup/)합니다. hello 인스턴스 보호 계산 hello 기반 *실제* "리소스 디스크" hello 제외 하 고-hello 가상 컴퓨터의 모든 hello 데이터의 합계와 hello hello 가상 컴퓨터의 크기

Vm의 백업은 대 한 가격 책정 *하지* 각 데이터 디스크 연결 된 toohello 가상 컴퓨터에 대 한 hello 최대 지원 크기를 기반 합니다. 가격 책정 hello 데이터 디스크에 저장 된 hello 실제 데이터를 기반으로 합니다. 마찬가지로, hello 백업 저장소 요금 hello 양의 hello 각 복구 지점에 실제 데이터의 hello 합계는 Azure 백업에 저장 된 데이터를 기반으로 합니다.

최대 크기가 각각 1TB인 두 개의 추가 데이터 디스크가 있는 A2 표준 크기 가상 컴퓨터를 예로 들 수 있습니다. hello 다음 표에 나와 각이 디스크에 저장 된 hello 실제 데이터:

| 디스크 유형 | 최대 크기 | 실제 데이터 표시 |
| --- | --- | --- |
| 운영 체제 디스크 |1023GB |17GB |
| 로컬 디스크/리소스 디스크 |135GB |5GB(백업에 포함되지 않음) |
| 데이터 디스크 1 |1023GB |30GB |
| 데이터 디스크 2 |1023GB |0GB |

hello *실제* hello 가상 컴퓨터의 크기는이 경우 17 GB + 30GB + 0 = 47 g B입니다. 이 보호 된 인스턴스 크기 (47 GB) hello 월별 요금은 hello 기준이 됩니다. Hello hello 가상 컴퓨터의 데이터 양을 많아지면, 그에 따라 청구 변경 내용에 대해 사용 되는 hello 보호 된 인스턴스 크기입니다.

청구는 hello 첫 번째 성공적인 백업 완료 될 때까지 시작 되지 않습니다. 이 시점에서 저장소 및 보호 된 인스턴스 모두에 대 한 hello 청구를 시작합니다. 이 때만 요금이 계속 청구 *자격 증명 모음에 저장 된 데이터를 백업 하는 모든* hello 가상 컴퓨터에 대 한 합니다. Hello 가상 컴퓨터 보호를 중지 되지만 자격 증명 모음에 가상 컴퓨터 백업 데이터가 있는 요금이 계속 청구 합니다.

지정 된 가상 컴퓨터 중지 hello 보호가 중지 된 경우에 대금 청구 *및* 모든 백업 데이터가 삭제 됩니다. 보호를 중지 하 고 현재 백업 작업이 없는지, hello 마지막으로 성공한 VM 백업 hello 크기 hello 보호 된 인스턴스 크기 hello 월별 요금 청구에 사용 됩니다.

## <a name="questions"></a>질문이 있으십니까?
기능의 경우 원하는 toosee 포함 또는 질문이 있는 경우 [피드백](http://aka.ms/azurebackup_feedback)합니다.

## <a name="next-steps"></a>다음 단계
* [가상 컴퓨터 설정](backup-azure-vms.md)
* [가상 컴퓨터 백업 관리](backup-azure-manage-vms.md)
* [가상 컴퓨터 복원](backup-azure-restore-vms.md)
* [VM 백업 문제 해결](backup-azure-vms-troubleshoot.md)
