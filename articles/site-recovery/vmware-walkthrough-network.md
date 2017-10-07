---
title: "VMware tooAzure 복제에 대 한 네트워킹 aaaPlan | Microsoft Docs"
description: "이 문서에서는 네트워크 VMware Vm tooAzure 복제할 때 필요한 계획"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a>4 단계: VMware tooAzure 복제에 대 한 네트워킹 계획

이 문서 네트워크 때 복제 온-프레미스 VMware Vm tooAzure hello를 사용 하 여 계획 고려 사항에 요약 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="connect-tooreplica-vms"></a>Tooreplica Vm 연결

복제 및 장애 조치 전략을 계획할 때는 hello 주요 질문 중 하나는 어떻게 tooconnect toohello Azure VM 장애 조치 후 합니다. 복제본 Azure VM에 대한 네트워크 전략을 설계할 때 몇 가지 선택 항목이 있습니다.

- **다른 IP 주소를 사용 하 여**:에 대해 선택할 수 toouse 다른 IP 주소 범위 hello Azure VM 네트워크를 복제 합니다. 이 시나리오 hello에 VM 장애 조치 후 새 IP 주소를 갖게 되며 DNS 업데이트가 필요 합니다.
- **동일한 IP 주소가 유지**: 할 수 있습니다 toouse hello hello 장애 조치 후 Azure 네트워크에 대 한 기본 온-프레미스 사이트에 있는 동일한 IP 주소 범위입니다. 동일한 IP 주소를 간소화 하면서 hello 장애 조치 후 네트워크 관련된 문제를 줄여 hello 복구 합니다. 그러나 tooAzure를 복제 하는 경우 tooupdate 경로 hello IP 주소의 hello 새 위치에 장애 조치 후 해야 합니다. 


## <a name="retain-ip-addresses"></a>IP 주소 유지

서브넷 장애 조치 있는 tooAzure 장애 조치할 때 hello 기능 tooretain 고정 IP 주소를 제공 하는 사이트 복구 합니다.

서브넷 장애 조치를 사용하는 경우 특정 서브넷은 사이트 1 또는 사이트 2에 있으며 두 사이트에 동시에 존재하지는 않습니다. 프로그래밍 방식으로 순서 toomaintain hello IP 주소 공간에서 hello 이벤트에는 장애 조치를 하나의 사이트 tooanother에서 hello 라우터 인프라 toomove hello 서브넷에 대 한 정렬합니다. 장애 조치 중 hello 서브넷 이동 hello로 보호 되는 Vm에 연결 합니다. hello 주요 단점은 실패 하는 hello 이벤트에서 toomove hello 전체 서브넷 있는입니다.


### <a name="failover-example"></a>장애 조치 예제

장애 조치 tooAzure에 대 한 예제를 살펴 보겠습니다.

- Woodgrove Bank라는 가상의 회사에는 비즈니스 앱을 호스팅하는 온-프레미스 인프라가 있습니다. 모바일 응용 프로그램은 Azure에서 호스팅됩니다.
- Azure 및 온-프레미스 서버에서 Woodgrove Bank Vm 간의 연결 hello 온-프레미스 지 네트워크와 hello Azure 가상 네트워크 간의 사이트 간 (VPN) 연결에서 제공 됩니다.
- 회사의 가상 네트워크를 Azure의 hello VPN 즉 온-프레미스 네트워크의 확장으로 나타납니다.
- Woodgrove는 toouse 사이트 복구 tooreplicate 온-프레미스 작업 부하 tooAzure 하려고합니다.
 - Woodgrove 응용 프로그램과 하드 코드 된 IP 주소에 따라 다르며 따라서 tooAzure 장애 조치 후 응용 프로그램에 대 한 tooretain IP 주소를 필요한 구성을 toodeal에 있습니다.
 - Woodgrove에 할당 된 IP 주소 범위 172.16.1.0/24에서 172.16.2.0/24 tooits 리소스 Azure에서 실행 합니다.


해당 VM tooAzure IP hello 유지 하는 동안 주소 toobe 수 tooreplicate을 Woodgrove, 여기는 hello 제조업체 필요한 toodo 다음과 같습니다.

1. Azure 가상 네트워크를 만듭니다. 응용 프로그램이 원활 하 게 조치할 수 있도록 hello의 확장 온-프레미스 네트워크에 여야 합니다.
2. Azure 있습니다 tooadd 사이트 간 VPN 연결을 또한 Azure에서 만든 사이트 간 toopoint 연결 toohello 가상 네트워크를 허용 됩니다.
3. Hello 사이트 간 연결을 설정할 때 hello Azure 네트워크, IP 주소 범위 hello hello 온-프레미스 IP 주소 범위와에서 다른 경우에 toohello 온-프레미스 위치 (로컬 네트워크) 트래픽을 라우팅할 수 있습니다.
    - 이는 Azure는 확대 서브넷을 지원하지 않기 때문입니다. 따라서 서브넷 192.168.1.0/24 온-프레미스를 사용 하도록 설정한 경우 로컬 네트워크 192.168.1.0/24 hello Azure 네트워크에에서 추가할 수 없습니다.
    - Azure hello 서브넷에 있는 현재 Vm이 없는 및 재해 복구에 해당 hello 서브넷 만들어집니다 인식 하지 않으므로 1 세대입니다.
    - toobe 수 toocorrectly 네트워크 트래픽을 라우팅할 hello 네트워크 및 hello 로컬 네트워크에는 Azure 네트워크 hello 서브넷 부족 충돌 있어서는 안 됩니다.

![서브넷 장애 조치(failover) 전](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a>장애 조치(failover) 전

1. 추가 네트워크(예: 복구 네트워크)를 만듭니다. 이 hello 네트워크는 Vm 조치할에서 생성 됩니다.
2. hello VM 속성에서 장애 조치 후에 유지 되는 IP 주소는 VM에 대 한 hello tooensure > **구성**, 동일한 IP 주소는 VM 온-프레미스에 있으며 클릭 해당 hello hello 지정 **저장**합니다.
3. Hello VM 장애 조치 되는 경우 Azure Site Recovery 제공 IP 주소 tooit hello를 할당 합니다.

    ![네트워크 속성](./media/site-recovery-network-design/network-design8.png)

4. 장애 조치에는 트리거, 트리거되고 hello 필요한 IP 주소를 가진 hello Vm을 Azure에 생성 되 면 toohello 네트워크를 사용 하 여 연결할 수 있습니다는 [Vnet tooVnet 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다. 이 작업은 스크립팅될 수 있습니다.
5. 경로 필요 toobe 적절히 수정 tooreflect 해당 192.168.1.0/24 이제 tooAzure 옮겼습니다.

    ![서브넷 장애 조치(failover) 후](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a>장애 조치(failover) 후

위에서 설명한 대로 Azure 네트워크가 없는 경우 장애 조치(failover) 후 기본 사이트와 Azure 간의 사이트 간 VPN 연결을 만들 수 있습니다.

## <a name="change-ip-addresses"></a>IP 주소 변경

이 [블로그 게시물](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) 장애 조치 후 tooset hello tooretain IP 필요 하지 않을 때 Azure 네트워킹 인프라를 해결 하는 방법을 설명 합니다. 응용 프로그램 설명으로 시작, 어떻게 네트워킹 tooset 온-프레미스 및 Azure에서 찾아서 장애 조치를 실행 하는 방법에 대 한 정보로 결론을 내립니다.  

## <a name="next-steps"></a>다음 단계

너무 이동[5 단계: Azure 준비](vmware-walkthrough-prepare-azure.md)
