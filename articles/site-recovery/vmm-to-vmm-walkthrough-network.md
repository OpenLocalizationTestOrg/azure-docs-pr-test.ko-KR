---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 네트워킹 aaaPlan | Microsoft Docs"
description: "이 문서에서는 Azure 사이트 복구와 Hyper-v Vm tooa 보조 System Center VMM 사이트를 복제할 때 네트워크 계획을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>3 단계: Hyper-v VM 복제 tooa 보조 VMM 사이트에 대 한 네트워킹 계획

System Center Virtual Machine Manager (VMM) 클라우드에서 관리 되는 Hyper-v 가상 컴퓨터 (Vm)를 복제 하는 경우 네트워킹이 문서 tooplan 읽을 배포 필수 조건 검토 한 후 tooa 보조 사이트를 사용 하 여 [Azure사이트복구](site-recovery-overview.md) hello Azure 포털의에서. 

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="network-mapping-overview"></a>네트워크 매핑 개요

네트워크 매핑은 (VMM에서 관리 됨) Hyper-v Vm tooa 보조 데이터 센터를 복제할 때 사용 됩니다. 네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 VMM 서버의 VM 네트워크 사이를 매핑합니다. 매핑 다음 hello지 않습니다.

- **네트워크 연결**-장애 조치 후 Vm 연결 tooappropriate 네트워크입니다. hello 복제본 VM에 연결 된 toohello 대상 네트워크 매핑된 toohello 원본 네트워크를 됩니다.
- **최적의 배치**-최적으로 위치 hello Hyper-v 호스트 서버에 복제본 Vm입니다. 복제본 Vm 수 액세스 hello 매핑되는지 VM 네트워크 호스트에 배치 됩니다.
- **네트워크 매핑이 없는**-네트워크 매핑을 구성 하지 않는 경우 복제본 Vm 장애 조치 후 tooany 연결 된 VM 네트워크에 되지 않습니다.


### <a name="example"></a>예제

다음 예에서는 tooillustrate은이 메커니즘입니다. 뉴욕과 시카고 두 위치에 있는 조직을 보겠습니다.

**위치** | **VMM 서버** | **VM 네트워크** | **다음으로 매핑**
---|---|---|---
뉴욕 | VMM-뉴욕| VMNetwork1-뉴욕 | TooVMNetwork1-시카고와 매핑된
 |  | VMNetwork2-뉴욕 | 매핑되지 않음
시카코 | VMM-시카고| VMNetwork1-시카고 | 매핑된 tooVMNetwork1-뉴욕
 | | VMNetwork1-시카고 | 매핑되지 않음

이 예제에서:

- 연결 된 tooVMNetwork1-뉴욕에 있는 모든 가상 컴퓨터에 대 한 복제 가상 컴퓨터를 만들면 tooVMNetwork1-시카고와 연결된 됩니다.
- VMNetwork2-뉴욕 또는 VMNetwork2-시카고에 대 한 복제 가상 컴퓨터를 만들면 연결된 tooany 네트워크 되지 않습니다.

예제 조직에 hello 논리 네트워크 hello 클라우드와 연결 된 VMM 클라우드가 설정 되어 방법을 다음과 같습니다.

#### <a name="cloud-protection-settings"></a>클라우드 보호 설정

**보호된 클라우드** | **클라우드 보호** | **논리 네트워크(뉴욕)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>해당 없음</p><p></p> | <p>LogicalNetwork1-뉴욕</p><p>LogicalNetwork1-시카고</p>
SilverCloud2 | <p>해당 없음</p><p></p> | <p>LogicalNetwork1-뉴욕</p><p>LogicalNetwork1-시카고</p>

#### <a name="logical-and-vm-network-settings"></a>논리 및 VM 네트워크 설정

**위치** | **논리 네트워크** | **연결된 VM 네트워크**
---|---|---
뉴욕 | LogicalNetwork1-뉴욕 | VMNetwork1-뉴욕
시카코 | LogicalNetwork1-시카고 | VMNetwork1-시카고
 | LogicalNetwork2Chicago | VMNetwork2-시카고

#### <a name="target-network-settings"></a>대상 네트워크 설정

Hello 대상 VM 네트워크를 선택 하면 이러한 설정에 따라 hello 다음 표에서 사용할 수 있는 hello 선택 항목을 표시 합니다.

**선택** | **보호된 클라우드** | **클라우드 보호** | **사용 가능한 대상 네트워크**
---|---|---|---
VMNetwork1-시카고 | SilverCloud1 | SilverCloud2 | 사용 가능
 | GoldCloud1 | GoldCloud2 | 사용 가능
VMNetwork2-시카고 | SilverCloud1 | SilverCloud2 | 사용할 수 없음
 | GoldCloud1 | GoldCloud2 | 사용 가능


Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.


#### <a name="failback-behavior"></a>장애 복구 동작

장애 복구 (역방향 복제)의 hello 경우 어떤 일이 생기 toosee VMNetwork1-뉴욕 매핑된 tooVMNetwork1-시카고와 설정을 다음 hello로 인지를 가정해 보겠습니다.


**가상 컴퓨터** | **연결 된 tooVM 네트워크**
---|---
VM1 | VMNetwork1-네트워크
VM2(VM1의 복제) | VMNetwork1-시카고

이러한 설정을 사용하여 몇 가지 가능한 시나리오에서 발생하는 결과를 검토해 보겠습니다.

**시나리오** | **결과**
---|---
장애 조치 후 v M-2의 hello 네트워크 속성 변경 되지 않습니다. | V M-1에 연결 된 toohello 원본 네트워크 유지 됩니다.
장애 조치(failover) 후 VM-2의 네트워크 속성이 변경되고 연결이 끊김 | VM-1의 연결이 끊김
V M-2의 네트워크 속성은 장애 조치 후 변경 되 고 tooVMNetwork2-시카고와 연결된 됩니다. | VMNetwork2-시카고가 매핑되지 않는 경우 VM-1의 연결이 끊김
VMNetwork1-시카고의 네트워크 매핑이 변경됨 | V M-1에 연결 된 toohello 매핑된 네트워크와 지금 tooVMNetwork1-시카고 됩니다.



## <a name="prepare-for-network-mapping"></a>네트워크 매핑을 준비

1. Hello 원본 및 대상 VMM 서버에서 hello 원본 클라우드와 대상 클라우드에 연결한 논리 네트워크에 있어야 합니다. 
2. Hello 원본 및 대상 서버의 VM 네트워크 논리 네트워크 연결 된 toohello 있어야 합니다.
3. Hello 원본 위치에 있는 Hyper-v 호스트에서 Vm에 연결 된 toohello 원본 VM 네트워크 수 있어야 합니다. 동일한 hello에 VM 네트워크 간 매핑을 구성할 수만 단일 VMM 서버를 사용 하는 경우 서버.

Site Recovery를 배포하는 동안 네트워크 매핑을 설정하면 다음 작업이 수행됩니다.

- 네트워크 매핑을 설정 하 고 대상 VM 네트워크를 선택 하는 경우 hello 원본 VM 네트워크를 사용 하는 hello VMM 원본 클라우드가 표시 됩니다, hello hello 대상 클라우드가 사용 가능한 대상 VM 네트워크와 함께 합니다.
- - 매핑이 올바르게 구성 된 하 고 복제가 활성화 되어 원본이 VM 연결된 tooits 원본 VM 네트워크 수와 hello 대상 위치의 복제본 연결 될 tooits VM 네트워크를 매핑됩니다.
- Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello VM hello 네트워크에 연결 된 toohello 첫 번째 서브넷 됩니다.

## <a name="connect-toovms-after-failover"></a>장애 조치 후 tooVMs 연결

복제 및 장애 조치 전략을 계획할 때는 hello 주요 질문 중 하나는 어떻게 장애 조치 후 tooconnect toohello 복제 합니다. 다음의 두 가지 방법 중에서 선택할 수 있습니다. 

- **다른 IP 주소를 사용 하 여**:에 대해 선택할 수 toouse 다른 IP 주소를 hello VM을 복제 합니다. 이 시나리오 hello에 VM 장애 조치 후 새 IP 주소를 갖게 되며 DNS 업데이트가 필요 합니다.
- **유지 동일한 IP 주소를 hello**: 할 수 있습니다 toouse hello hello 복제본 VM에 대 한 동일한 IP 주소입니다. 동일한 IP 주소를 간소화 하면서 hello 장애 조치 후 네트워크 관련된 문제를 줄여 hello 복구 합니다. 

## <a name="retain-ip-addresses"></a>IP 주소 유지

Hello toohello 보조 사이트 장애 조치 한 후 기본 사이트, 전체 서브넷 장애 조치를 수행 하 고 업데이트할 수 경로 tooindicate hello hello IP 주소의 새 위치 또는 대체 배포 hello 간의 늘어난된 서브넷 tooretain hello IP 주소를 원하는 경우 기본 및 복구 사이트 hello 합니다.

### <a name="stretched-subnet"></a>늘어난 서브넷

스트레치 된 서브넷에 hello 서브넷은 동시에 hello 기본 및 보조 사이트 모두 있습니다. 서버와 해당 (계층 3) IP 구성 toohello 보조 사이트를 이동 하는 경우 hello 네트워크 hello 트래픽 toohello 새 위치로 자동으로 라우팅할 됩니다. 

계층 2(데이터 링크 계층) 측면을 고려하면 확대 VLAN을 관리할 수 있는 네트워킹 장비가 필요합니다. 또한 늘이기 hello VLAN, 여 hello 잠재적인 장애 도메인은 tooboth 사이트의 경우 기본적으로 단일 실패 지점이 되 고 확장 합니다. 이러한 현상이 발생할 가능성은 거의 없기는 하지만, 브로드캐스트 스톰이 시작해서 격리되지 못하게 될 수도 있습니다. 


### <a name="subnet-failover"></a>서브넷 장애 조치(failover)

서브넷 장애 조치 tooobtain hello 확대 되므로 hello 서브넷의 이점 실제로 늘이거나 하지 않고 실행할 수 있습니다. 이 솔루션에서는 서브넷을 사용할 수 hello 원본 또는 대상 사이트에서 하지만 둘 다에 없는 동시에 합니다. toomaintain hello IP 주소 공간 hello 이벤트에는 장애 조치를 정렬할 수 있습니다 프로그래밍 방식으로 한 사이트 tooanother에서 hello 라우터 인프라 toomove hello 서브넷에 대 한 합니다. 서브넷으로 이동 하므로 장애 조치 발생 후 hello Vm에 연결 합니다. hello 주요 단점은 실패 하는 hello 이벤트에서 toomove hello 전체 서브넷 있는입니다.

### <a name="example"></a>예제

전체 서브넷 장애 조치(failover)의 예는 다음과 같습니다. hello 기본 사이트의 서브넷 192.168.1.0/24에서 실행 중인 응용 프로그램입니다. 장애 조치가이 서브넷의 모든 hello Vm toohello 보조 사이트를 통해 실패 하는 IP 주소를 유지 합니다. 경로 필요 toobe 수정 tooreflect hello 팩트 toosubnet 192.168.1.0/24 속한 모든 hello VM 가상 컴퓨터 toohello 보조 사이트를 이동 이제 했습니다.

다음 그래픽 표시 hello 서브넷 장애 조치 전후 hello:

- 장애 조치 하기 전에 서브넷 192.168.0.1/24 활성화 되어 hello 원본 사이트에서 장애 조치 후 hello 보조 사이트에 활성화 됩니다.
- 주 사이트 및 사이트 복구, 세 번째 사이트 및 기본 사이트 간의 hello 라우팅합니다 및 세 번째 사이트와 복구 사이트 toobe 적절히 수정 해야 합니다.

**장애 조치(failover) 전**

![장애 조치(failover) 전](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**장애 조치(failover) 후**

![장애 조치(failover) 후](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

장애 조치(failover) 후에는 다음 작업이 수행됩니다.

- 사이트 복구 hello 고정 IP 주소 풀에서 각 VMM 인스턴스에 대 한 hello 관련 네트워크에서 VM hello에서 각 네트워크 인터페이스에 대 한 IP 주소를 할당합니다.
- Hello 보조 사이트에 hello IP 주소 풀은 하는 경우와 같지 않다는 hello 원본 사이트, 사이트 복구에 할당 하는 hello 동일한 IP 주소 (hello 원본 VM)의 toohello 복제본 VM hello 합니다. VMM에서 hello IP 주소가 예약 되었는지 하지만 hello Hyper-v 호스트에 hello 장애 조치 IP 주소로 설정 되어 있지 않습니다. hello hyper-v 호스트의 IP 주소를 장애 조치 hello 장애 조치 하기 바로 전에 설정 됩니다.
- Hello 동일한 IP 주소를 사용할 수 없는 경우 사이트 복구 hello 풀에서 사용 가능한 다른 IP 주소를 할당 합니다.
- Vm에서 DHCP를 사용 하는 경우 사이트 복구 hello IP 주소를 관리 하지 않습니다. DHCP hello toocheck 필요한 hello 보조 사이트 서버 hello hello 원본 사이트와 동일한 범위에서 주소를 할당할 수 있습니다.

### <a name="validate-hello-ip-address"></a>Hello IP 주소의 유효성을 검사합니다

VM에 대 한 보호를 활성화 한 후에 다음 샘플 스크립트 tooverify hello 할당 된 주소 toohello VM 사용할 수 있습니다. hello 동일한 IP 주소 hello 장애 조치 IP 주소로 설정 되며 장애 조치 시 hello toohello VM을 할당 합니다.

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>IP 주소 변경

이 시나리오에서는 장애 조치 하는 Vm의 hello IP 주소가 변경 됩니다. hello이이 솔루션의 단점은 hello 유지 관리가 필요 합니다. 일반적으로는 복제본 VM이 시작된 후에 DNS가 업데이트됩니다. DNS 항목 toobe 변경 하거나 되는 네트워크와 업데이트 된 캐시 된 항목에 fluster 수 있습니다. 이로 인해 가동 중지 시간이 발생할 수 있습니다. 다음 방법을 통해 가동 중지 시간을 줄일 수 있습니다.

- 인트라넷 응용 프로그램의 경우 낮은 TTL 값을 사용합니다.
- Tooupdate hello DNS 서버 tooensure 시기 적절 한 업데이트를 사이트 복구 복구 계획 스크립트 다음에 오는 hello를 사용 합니다. 동적 DNS 등록을 사용 하는 경우에 hello 스크립트를 필요 하지 않습니다.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>예제 

기본 hello 간에 toouse 서로 다른 IP 주소 및 hello 복구 사이트를 계획 중인 시나리오를 살펴보겠습니다. 이 예제에서는 서로 다른 IP 주소 기본 및 보조 사이트에 걸쳐 있고 hello 주 가상 컴퓨터 또는 복구 사이트에서 호스팅되는 응용 프로그램에서 세 번째의 사이트에 액세스할 수 있습니다.

- 장애 조치 하기 전에 앱 hello 기본 사이트에 호스팅된 서브넷 192.168.1.0/24 이므로 서브넷 172.16.1.0/24 hello 보조 사이트에 구성 된 toobe 장애 조치 후 있습니다.
- 세 사이트 모두 서로 액세스할 수 있도록 VPN 연결/네트워크 라우팅이 적절하게 구성되었습니다.
- 장애 조치 후 응용 프로그램 hello 복구 서브넷에 복원 됩니다. 이 시나리오에서는 없습니다 필요 toofail hello 전체 서브넷을 통해 않으며 변경이 필요한 tooreconfigure VPN 또는 네트워크 경로입니다. hello 장애 조치 및 일부 DNS 업데이트를 응용 프로그램에 계속 액세스할 수 있는지 확인 합니다.
- DNS 구성된 tooallow 동적 업데이트를 하는 경우 다음 hello Vm 등록 됩니다 장애 조치 후 시작할 때 hello 새 IP 주소를 사용 하 여 합니다.

**장애 조치(failover) 전**

![다른 IP - 장애 조치 전](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**장애 조치(failover) 후**

![다른 IP - 장애 조치 후](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>다음 단계

너무 이동[4 단계: 준비 VMM 및 Hyper-v](vmm-to-vmm-walkthrough-vmm-hyper-v.md)합니다.


