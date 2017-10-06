---
title: "Azure tooan 온-프레미스 사이트에서 aaaReprotect | Microsoft Docs"
description: "Vm tooAzure의 장애 조치 후 장애 복구 toobring 백 tooon-프레미스 Vm 시작할 수 있습니다. 자세한 방법을 장애 복구 하기 전에 tooreprotect 합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Azure tooan 온-프레미스 사이트에서 다시 보호



## <a name="overview"></a>개요
이 문서에서는 설명 방법을 tooreprotect Azure Azure tooan 온-프레미스 사이트에서 가상 컴퓨터. 준비 toofail 중인 경우이 문서의 hello 지침에 따라 후에 다시 VMware 가상 컴퓨터 또는 물리적 Windows/Linux 서버 hello 온-프레미스 사이트 tooAzure에서 조치할 했습니다 (에 설명 된 대로 [복제 VMware 가상 컴퓨터 및 Azure 사이트 복구와 실제 서버 tooAzure](site-recovery-failover.md)).

> [!WARNING]
> 후 다시 실패로 지정할 수 없습니다 [마이그레이션을 완료](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), 가상 컴퓨터 tooanother 리소스 그룹을 이동 하거나 Azure 가상 컴퓨터를 삭제 합니다.


다시 보호를 완료 한 후 hello 보호 된 가상 컴퓨터 복제 하는 가상 컴퓨터 toobring hello에 대 한 장애 복구를 시작할 수 있습니다 이러한 toohello 온-프레미스 사이트입니다.

Hello 또는이 문서의 hello 끝에 메모 또는 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

간략 한 개요에 대 한 hello 다음 방법을 통해 toofail tooan Azure에서 온-프레미스 사이트에 대 한 비디오를 시청 합니다.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>필수 조건
Tooreprotect 가상 컴퓨터를 준비할 때 걸리거나 hello 사전 준비 동작을 따르는 것이 좋습니다.

* 원하는 toofail hello 가상 컴퓨터에 다시, hello 갖도록 vCenter 서버를 관리 하는 경우 [필요한 권한](site-recovery-vmware-to-azure-classic.md) vCenter server에서 가상 컴퓨터의 검색에 대 한 합니다.

  > [!WARNING]
  > 스냅숏은 hello에 존재 하는 경우 온-프레미스 마스터 대상 또는 hello 가상 컴퓨터를 다시 보호 실패 합니다. Tooreprotect 계속 진행 하기 전에 hello 마스터 대상에서 hello 스냅숏을 삭제할 수 있습니다. hello 스냅숏은 hello 가상 컴퓨터에서 다시 보호 하는 동안 자동으로 병합 됩니다.

* 장애 복구하기 전에 다음의 두 가지 추가 구성 요소를 만듭니다.

  * **프로세스 서버**: hello [프로세스 서버](site-recovery-vmware-setup-azure-ps-resource-manager.md) Azure의 hello 보호 된 가상 컴퓨터에서 데이터를 수신 하 고 데이터 toohello 온-프레미스 사이트를 보냅니다. 대기 시간이 짧은 네트워크는 hello 프로세스 서버와 보호 된 hello 가상 컴퓨터 사이 필요 합니다. 따라서 Azure ExpressRoute 연결 또는 Azure 기반 프로세스 서버와 VPN을 사용하는 경우 온-프레미스 프로세스 서버를 포함할 수 있습니다.
  
  * **마스터 대상 서버**: hello 마스터 대상 서버 장애 복구 데이터를 수신 합니다. 만든 hello 온-프레미스 관리 서버에는 기본적으로 설치 하는 마스터 대상 서버를 있습니다. 그러나 장애 트래픽의 hello 볼륨에 따라 toocreate 별도 마스터 대상 서버 장애 복구 할 수 있습니다.
    * [Linux 가상 컴퓨터에는 Linux 마스터 대상 서버가 필요합니다](site-recovery-how-to-install-linux-master-target.md).
    * Windows 가상 컴퓨터에는 Windows 마스터 대상 서버가 필요합니다. Hello 온-프레미스 프로세스 서버와 마스터 대상 컴퓨터를 다시 사용할 수 있습니다.

    hello 마스터 대상에 나열 된 필수 구성 요소에 [다시 보호 하기 전에 마스터 대상에서 일반적인 작업 toocheck](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server)합니다.

* 장애 복구를 수행할 때 구성 서버가 온-프레미스에 있어야 합니다. 장애 복구 하는 동안 hello 가상 컴퓨터는 hello 구성 서버 데이터베이스에 존재 해야 합니다. 그렇지 않으면 장애 복구가 실패합니다. 

> [!IMPORTANT]
> 정기적으로 예정된 구성 서버 백업을 수행해야 합니다. 재해가 경우 동일한 IP 주소를 장애 복구 작동 하는 hello로 hello 서버를 복원 합니다.

* 집합 hello `disk.EnableUUID=true` VMware에 hello 마스터 대상 가상 컴퓨터의 hello 구성 매개 변수를 설정 합니다. 이 행이 존재하지 않는 경우 추가합니다. 이 설정은 올바르게를 탑재 하는 것에 있도록 필요 tooprovide 일관 된 UUID toohello 가상 컴퓨터 디스크 (VMDK)입니다.

* *Hello 마스터 대상 서버에 저장소 vMotion을 사용할 수 없습니다*합니다. 이 인해 hello 장애 복구 toofail 수 있습니다. hello 디스크 tooit 사용할 수 없는 hello 가상 컴퓨터를 시작할 수 없습니다. tooprevent이이 문제를 vMotion 목록에서 제외 hello 마스터 대상 서버입니다.

* 새 드라이브 toohello 마스터 대상 서버에 추가: 보존 드라이브입니다. 새 디스크 및 서식 hello 드라이브를 추가 합니다.


### <a name="frequently-asked-questions"></a>질문과 대답

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>S2S VPN 또는 express 경로 연결 tooreplicate 데이터 백 toohello 온-프레미스 사이트 필요한 이유
Hello 인터넷을 통해 온-프레미스 tooAzure에서 복제를 발생할 수 있습니다 또는 ExpressRoute을 공용 피어 링을 지닌 연결이, 다시 보호 및 장애 복구 된 사이트 및 사이트 간 (S2S)가 필요 하지만 VPN tooreplicate 데이터입니다. Azure의 hello 장애 조치 된 가상 컴퓨터 (ping) hello 온-프레미스 구성 서버에 연결할 수 있도록 hello 네트워크를 제공 합니다. Hello hello 장애 조치 된 가상 컴퓨터의 Azure 네트워크에에서 프로세스 서버를 배포할 수도 있습니다. 이 프로세스 서버 hello 온-프레미스 구성 서버와 수 toocommunicate도 있어야 합니다.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Azure에 프로세스 서버를 언제 설치해야 합니까?


tooreprotect 원하는 Azure의 hello 가상 컴퓨터 복제 데이터 tooa 프로세스 서버를 보냅니다. Azure에서 가상 컴퓨터 hello hello 프로세스 서버에 연결할 수 있도록 네트워크를 설정 합니다.

Azure에서 프로세스 서버를 배포 하거나 장애 조치에 사용 하는 hello 기존 프로세스 서버를 사용할 수 있습니다. hello 중요 지점 tooconsider는 hello 대기 시간 toosend hello 데이터 hello 서버의 가상 컴퓨터에 Azure toohello 프로세스입니다.

Express 경로 연결을 설정 하는 경우에 hello 가상 컴퓨터와 프로세스 서버 hello 간의 hello 대기 시간이 낮은 이므로 toosend 데이터는 온-프레미스 처리 서버를 사용할 수 있습니다.

 ![ExpressRoute 아키텍처 다이어그램](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



그러나는 S2S VPN만 있는 경우 Azure의 hello 프로세스 서버 배포는 것이 좋습니다.

 ![VPN 아키텍처 다이어그램](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


해당 복제 hello S2S VPN 또는 express 경로 네트워크의 피어 링 개인 hello에 대해서만 수행 해야 합니다. 네트워크 채널을 통해 충분한 대역폭을 사용할 수 있는지 확인합니다.

Azure 기반 프로세스 서버를 설치하는 방법에 대한 자세한 내용은 [Azure에서 실행되는 프로세스 서버 관리](site-recovery-vmware-setup-azure-ps-resource-manager.md)를 참조하세요.

> [!TIP]
> 장애 복구(failback) 중에는 Azure 기반 프로세스 서버를 사용하는 것이 좋습니다. hello 복제 성능 hello 프로세스 서버를 더 가깝기 때문 toohello 가상 컴퓨터 (Azure의 hello 실패 한 컴퓨터)에 복제 하는 경우 더 높습니다. 그러나 개념 (POC) 또는 데모 증명서를 하는 동안 개인 피어 링 toocomplete hello POC 더 빠른로 ExpressRoute과 함께 hello 온-프레미스 프로세스 서버를 사용할 수 있습니다.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>다시 보호가 작동할 수 있도록 다른 구성 요소에서 열어야 할 포트는 무엇인가요?

![장애 조치 및 장애 복구용 포트](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>다시 보호하는 데 사용해야 하는 마스터 대상 서버는 무엇인가요?
온-프레미스 마스터 대상 서버 hello 프로세스 서버에서 필요한 tooreceive 데이터 이며 toohello 온-프레미스 가상 컴퓨터의 VMDK를 작성 합니다. Windows 가상 컴퓨터를 보호하는 경우 Windows 마스터 대상 서버가 필요합니다. Hello 온-프레미스 프로세스 서버와 마스터 대상 다시 사용할 수 있습니다<!-- !todo component -->합니다. Linux 가상 컴퓨터에 대 한 추가 온-프레미스 Linux 마스터 대상을 tooset을 해야합니다.


마스터 대상 서버를 설치하는 방법은 다음을 참조하세요.

* [어떻게 tooinstall Windows 마스터 대상 서버](site-recovery-vmware-to-azure.md)
* [어떻게 tooinstall Linux 마스터 대상 서버](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>장애 복구 하는 동안 hello 온-프레미스 ESXi 호스트에서 지원 되는 데이터 저장소 유형은 무엇입니까?

현재 Azure Site Recovery에서는 실패 한 tooa 가상 컴퓨터 파일 시스템 (VMFS) 또는 vSAN 데이터 저장소에 백업 합니다. NFS 데이터 저장소는 지원되지 않습니다. 다시 보호 화면 NFS 데이터 저장소의 hello 경우에서 비어 있거나 hello vSAN 데이터 저장소 보여주지만 hello 작업 중에 실패 하면 toothis 제한으로 인해 hello 데이터 저장소 선택 hello에 입력 합니다. 다시 toofail 가져오려는 경우 온-프레미스 VMFS 데이터 저장소를 만들 수 있으며 백 tooit 실패. 이 장애 복구 hello VMDK 전체를 다운로드를 하면 됩니다.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>일반적인 작업 toocheck hello 마스터 대상 서버 설치를 완료 한 후

* Hello 가상 컴퓨터가 있는 경우 온-프레미스에 vCenter 서버 hello, hello 마스터 대상 서버 필요한 액세스 toohello 온-프레미스 가상 컴퓨터의 VMDK 합니다. 액세스가 필요한 toowrite hello 복제 데이터 toohello 가상 컴퓨터의 디스크 합니다. 읽기/쓰기 권한으로 hello 마스터 대상 호스트에 탑재 되어 해당 hello 온-프레미스 가상 컴퓨터의 데이터 저장소를 확인 합니다.

* Hello 가상 컴퓨터가 있는 온-프레미스 hello vCenter 서버의 경우 사이트 복구 서비스 hello toocreate 새 가상 컴퓨터를 다시 보호 하는 동안 필요 합니다. Hello 마스터 대상을 만드는 hello ESX 호스트에이 가상 컴퓨터가 만들어집니다. 원하는 hello 호스트에 hello 장애 복구 가상 컴퓨터를 만들 수 있도록 신중 하 게 hello ESX 호스트를 선택 합니다.

* *마스터 대상 서버 hello에 대 한 저장소 vMotion을 사용할 수 없습니다*합니다. 이 인해 hello 장애 복구 toofail 수 있습니다. hello 디스크 tooit 사용할 수 없는 hello 가상 컴퓨터를 시작할 수 없습니다.

  > [!WARNING]
  > 마스터 대상 다시 보호 한 후 저장소 vMotion 작업에서, hello 보호 된 가상 컴퓨터 디스크를 연결 된 toohello 마스터 대상 hello vMotion 작업의 대상 toohello 마이그레이션합니다. Toofail이 후 다시 시도 하면 hello 디스크의 분리 hello 디스크를 찾을 수 없는 때문에 실패 합니다. 그러면 저장소 계정에서 하드 toofind hello 디스크가 됩니다. Toofind 필요한을 수동으로 toohello 가상 컴퓨터를 연결 합니다. 그 후 hello 온-프레미스 가상 컴퓨터를 부팅 될 수 있습니다.

* 보존 드라이브 tooyour 기존 Windows 마스터 대상 서버를 추가 합니다. 새 디스크 및 서식 hello 드라이브를 추가 합니다. hello 보존 드라이브는 hello 가상 컴퓨터에서 뒤로 toohello 온-프레미스 사이트를 복제 하는 시점에 사용 되는 toostop hello 포인트입니다. 보존 드라이브에 대한 몇 가지 기준을 따릅니다. 이러한 기준 없이 hello 드라이브 hello 마스터 대상 서버에 대 한 표시 되지 않습니다.

   * hello 볼륨의 복제 대상이 같은 다른 목적을 위해 사용 되지 않습니다.

   * hello 볼륨이 잠금 모드 아닙니다.

   * hello 볼륨 캐시 볼륨이 아닙니다. hello 마스터 대상 설치 해당 볼륨에 존재 하지 않아야 합니다. hello 프로세스 서버와 마스터 대상에 대 한 사용자 지정 설치 볼륨 hello 보존 볼륨에 대 한 대상이 되지 않습니다. Hello 프로세스 서버와 마스터 대상 볼륨에 설치 되 면 hello 볼륨은 hello 마스터 대상 캐시 볼륨에 해당 합니다.

   * hello 볼륨의 파일 시스템 형식을 hello FAT 또는 FAT32 아닙니다.

   * hello 볼륨 용량은 0이 아닌 값입니다.

   * Windows 용 hello 기본 보존 볼륨은 R hello 볼륨.

   * Linux 용 hello 기본 보존 볼륨 /mnt/retention입니다.

  > [!IMPORTANT]
  > 기존 프로세스 서버/구성 서버 컴퓨터 또는 소수 자릿수 또는 프로세스 서버/마스터 대상 서버 컴퓨터를 사용 하는 새 드라이브 tooadd가 필요 합니다. hello 새 드라이브 hello 앞에 요구 사항을 충족 해야 합니다. Hello 보존 드라이브 없으면 hello 포털에 hello 선택 드롭다운 목록에 표시 되지 않습니다. 드라이브 toohello 온-프레미스 마스터 대상을 추가 하면 hello 포털에 hello 선택 영역에서 드라이브 tooappear hello에 대 일 분을 차지 합니다. 15 분 후 hello 드라이브가 표시 되지 않으면 hello 구성 서버를 새로 고칠 수도 있습니다.

* 장애 조치된 Linux 가상 컴퓨터에는 Linux 마스터 대상 서버가 필요합니다. 장애 조치된 Windows 가상 컴퓨터에는 Windows 마스터 대상 서버가 필요합니다.

* Hello 마스터 대상 서버에서 VMware tools를 설치 합니다. Hello VMware 도구 없이 hello 마스터 대상의 ESXi 호스트에 hello 데이터 저장소를 검색할 수 없습니다.

* Hello를 사용 하도록 설정 `disk.EnableUUID=true` hello vCenter 속성을 사용 하 여 hello 마스터 대상 가상 컴퓨터에 대 한 매개 변수입니다. <!-- !todo Needs link. -->

* hello 마스터 대상에 연결 된 VMFS 데이터 저장소를 하나 이상 있어야 합니다. 없는 경우, hello **데이터 저장소** hello 다시 보호 페이지에서 입력은 비어 있게 고 계속할 수 없습니다.

* 마스터 대상 서버 hello hello 디스크 스냅숏을 가질 수 없습니다. 스냅숏이 있으면 다시 보호 및 장애 복구가 실패합니다.

* 마스터 대상 hello Paravirtual SCSI 컨트롤러를 사용할 수 없습니다. hello 컨트롤러 LSI 논리 컨트롤러 수만 있습니다. LSI Logic 컨트롤러가 없으면 다시 보호가 실패합니다.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>단계 tooreprotect

> [!NOTE]
> Azure에서 가상 컴퓨터 부팅 후 시간이 걸리는 hello 에이전트에 대 한 tooregister 백 toohello 구성 서버 (위쪽 too15 분)입니다. 이 시간 동안 다시 보호 실패 하 고 오류 메시지가 표시 되는 해당 hello 에이전트가 설치 되지 않았습니다. 몇 분 동안 기다린 다음 다시 보호를 다시 시도합니다.



1. **자격 증명 모음** > **복제 항목**를 장애 조치는 hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **다시 보호**합니다. 시스템 및 선택 hello를 클릭할 수도 있습니다 **다시 보호** hello 명령 단추에서입니다.
2. Hello 블레이드 보호, 해당 hello 방향 알 수 있듯이 **Azure tooOn 프레미스**, 이미 선택 되어 있습니다.
3. **마스터 대상 서버** 및 **프로세스 서버**프로세스 서버 hello을 hello 온-프레미스 마스터 대상 서버를 선택 합니다.
4. 에 대 한 **데이터 저장소**, 선택 hello toorecover hello 디스크 온-프레미스를 원하는 데이터 저장소 toowhich 합니다. 이 옵션은 hello 온-프레미스 가상 컴퓨터는 삭제 되 고 toocreate 새 디스크를 해야 하는 경우 사용 됩니다. Hello 디스크가 이미 존재 하지만 계속 toospecify 값을 사용 해야 하는 경우이 옵션은 무시 됩니다.
5. Hello 보존 드라이브를 선택 합니다.
6. hello 장애 복구 정책은 자동으로 선택 됩니다.
7. 클릭 **확인** toobegin 다시 보호 합니다. 작업을 Azure toohello 온-프레미스 사이트에서 tooreplicate hello 가상 컴퓨터를 시작합니다. Hello에 hello 진행률을 추적할 수 **작업** 탭 합니다.

Toorecover tooan 대체 위치 (hello 온-프레미스 가상 컴퓨터를 삭제 하 고) 하는 경우를 원하는 경우 hello 보존 드라이브 및 hello 마스터 대상 서버에 대해 구성 된 데이터 저장소를 선택 합니다. 뒤로 toohello 온-프레미스 사이트 실패 하는 경우 hello VMware 가상 컴퓨터 장애 복구 보호 계획 사용 hello hello 마스터 hello 마찬가지로 동일한 데이터 저장소를 대상 서버. 새 가상 컴퓨터가 vCenter에 만들어집니다.

기존 Azure tooan toorecover hello 가상 컴퓨터가 온-프레미스 가상 컴퓨터를 원하는 경우 탑재 hello 온-프레미스 ESXi 호스트 hello 마스터 대상 서버에 대 한 읽기/쓰기 권한으로 가상 컴퓨터의 데이터 저장소.
    ![다시 보호 대화 상자](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

복구 계획의 hello 수준에서 다시 보호도 있습니다. 복제 그룹은 복구 계획을 통해서만 다시 보호할 수 있습니다. 복구 계획을 사용 하 여 다시 보호를 모든 보호 된 컴퓨터에 대 한 tooprovide hello 값 필요 합니다.

> [!NOTE]
> 사용 하 여 동일한 마스터 대상 서버 tooreprotect 복제 그룹을 hello 합니다. 다른 마스터 대상 서버 tooreprotect 복제 그룹을 사용 하 여 hello 서버 시간에 일반적인 포인트를 제공할 수 없습니다.

> [!NOTE]
> hello 온-프레미스 가상 컴퓨터 다시 보호 하는 동안 꺼져 있습니다. 이렇게 하면 복제 중 데이터 일관성을 보장할 수 있습니다. 다시 보호 완료 된 후 hello 가상 컴퓨터에 설정 하지 마십시오.

Hello 다시 보호에 성공 하면 hello 가상 컴퓨터 보호 되는 상태로 입력 합니다.

## <a name="next-steps"></a>다음 단계

Hello 가상 컴퓨터 보호 상태를 입력 한 후 다음을 할 수 있습니다 [는 장애 복구를 시작할](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back)합니다. 

hello 장애 복구 Azure의 hello 가상 컴퓨터 및 부팅 hello 온-프레미스 가상 컴퓨터를 종료 합니다. Hello 응용 프로그램에 대 한 가동 중지 시간이 필요 합니다. Hello 응용 프로그램 가동 중시 시간이 허용 하는 경우에 장애 복구에 대 한 시간을 선택 합니다.

## <a name="common-problems"></a>일반적인 문제

* 가상 컴퓨터 템플릿 toocreate를 사용한 경우 각 가상 컴퓨터 디스크 hello에 대 한 자체 UUID 갖는지 확인 합니다. 경우 hello 온-프레미스 가상 컴퓨터의 UUID 충돌 hello 마스터 대상의 둘 다에서 만들어진 hello 동일 하기 때문에 서식 파일을 다시 보호에 실패 합니다. 생성 되지 않은 hello에서 동일한 다른 마스터 대상 배포 템플릿.

* 읽기 전용 사용자 vCenter 검색을 수행하고 가상 컴퓨터를 보호하면 보호에 성공하고 장애 조치가 작동합니다. 를 다시 보호 하는 동안 장애 조치 hello 데이터 저장소를 검색할 수 없으므로 실패 합니다. 증상은 다시 보호 하는 동안 데이터 저장소 목록에 없는 해당 hello입니다. tooresolve이이 문제를 적절 한 권한이 있는 계정으로 hello vCenter 자격 증명을 업데이트할 수 있습니다 hello 작업을 다시 시도 하십시오. 자세한 내용은 참조 [복제 VMware 가상 컴퓨터 및 Azure 사이트 복구와 실제 서버 tooAzure](site-recovery-vmware-to-azure-classic.md)합니다.

* Linux 가상 컴퓨터를 다시 장애 복구 하 고 온-프레미스를 실행 하는 경우 해당 hello 네트워크 관리자 패키지 hello 컴퓨터에서 제거 된 것을 볼 수 있습니다. 이 제거 hello 네트워크 관리자 패키지는 Azure에서 가상 컴퓨터 hello가 복구 될 때 제거 되기 때문에 발생 합니다.

* Linux 가상 컴퓨터에 고정 IP 주소로 구성 되어 있고 tooAzure 장애 조치가 시 hello IP 주소는 DHCP에서 획득 됩니다. 장애 조치 tooon 온-프레미스 하면 hello 가상 컴퓨터는 toouse DHCP tooacquire hello IP 주소를 계속 합니다. 수동으로 toohello 컴퓨터에 로그인 하 고 필요한 경우 hello IP 주소 다시 tooa 고정 주소를 설정 합니다. Windows 가상 컴퓨터에서 고정 IP를 다시 얻을 수 있습니다.

* ESXi 5.5 체험 버전 또는 vSphere 6 하이퍼바이저 체험 버전을 사용하는 경우 장애 조치는 성공하지만 장애 복구가 실패합니다. 평가판 라이선스로 업그레이드 tooeither 프로그램 tooenable 장애을 복구 합니다.

* Hello 프로세스 서버에서 구성 서버 hello을 연결할 수 없는 경우 포트 443에서 텔넷 toocheck 연결 toohello 구성 서버를 사용 합니다. Tooping hello 구성 서버 hello 프로세스 서버에서 사용할 수 있습니다. 프로세스 서버 연결된 toohello 구성 서버의 경우 하트 비트가 있어야 합니다.

* Toofail 백 tooan 대체 vCenter을 시도 하는 경우 새 vCenter와 마스터 대상 서버 hello 검색 되었는지 확인 합니다. 일반적인 증상은 hello 데이터 저장소 액세스할 수 없거나 hello에 표시 되지 않는다는 **다시 보호** 대화 상자.

* 실제 온-프레미스 서버에 보호 되는 Windows Server 2008 R2 SP1 server Azure tooan 온-프레미스 사이트에서 다시 장애 할 수 없습니다.
