---
title: "aaaDesigning 재해 복구를 위해 네트워크 인프라 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에 대한 실제 네트워크 디자인 고려 사항을 알아봅니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>재해 복구를 위한 네트워크 디자인

이 문서는 방향이 지정 된 tooIT 전문가 tooleverage Microsoft Azure 사이트 복구 (ASR) toosupport 하려는 하 고는 설계, 구현 및 비즈니스 연속성 및 재해 복구 (BCDR) 인프라를 지 원하는 작업을 담당 하 고 BCDR 서비스를 개선 합니다. 이 문서에서는 Azure 또는 다른 온-프레미스 사이트에 해당하는 재해 복구 사이트에서 네트워크를 구성할 때 실제로 고려할 사항에 대해 설명합니다. 

## <a name="overview"></a>개요
[Azure 사이트 복구 (ASR)](https://azure.microsoft.com/services/site-recovery/) 는 비즈니스 연속성 재해 복구용 (BCDR)으로 가상화 된 응용 프로그램의 hello 보호 및 복구를 오케스트레이션 하는 Microsoft Azure 서비스입니다. 이 문서는 IP 범위 및 서브넷 hello 재해 복구 사이트에서 사이트 복구를 사용 하 여 가상 컴퓨터 (Vm)를 복제 하는 경우 설계에 중점을 두기 hello 네트워크 설계 하는 hello 과정을 통해 의도 된 tooguide hello 판독기입니다.

또한이 문서는 사이트 복구에서 설계 하 고 테스트 또는 재해 시 가상 멀티 사이트 데이터 센터 toosupport BCDR 서비스 구현을 사용 하는 방법을 보여 줍니다.

24/7 연결을에서는 모든 사용자 환경에서 현재까지 tookeep 보다 더 중요 한은 인프라 및 응용 프로그램 시작 및 실행 합니다. hello의 비즈니스 연속성 및 재해 복구 (BCDR) 목적은 toorestore 하지 못했습니다 구성 요소 hello 조직 정상 작업을 신속 하 게 다시 시작할 수 있도록 합니다. 개발 재해 복구 전략으 나 가능성이, 충격적인 사건이 이벤트 toodeal 매우 하기는 쉽지 않습니다. Hello 미래 예측의 toohello 내재 된 어려움 때문에 이것이, 특히 관계로 tooimprobable 이벤트 및 높은 hello tooprovide 방지할 수 있는 큰 재난의 적절 한 조치를 비용입니다.

BCDR 계획에 중요한 것은 복구 시간 목표(RTO) 및 복구 지점 목표(RPO)가 재해 복구 계획의 일환으로 정의 되어야 한다는 점입니다. 재해가 발생 하는 hello 고객의 데이터 센터를 신속 하 게 고객 수 있는 Azure Site Recovery를 사용 하 여 (낮은 RTO) 하는 경우 데이터 손실을 (RPO) hello 보조 데이터 센터 또는 Microsoft Azure에 있는 복제 된 가상 컴퓨터의 온라인입니다.

장애 조치는 처음 hello 주 데이터 센터 toohello 보조 데이터 센터 또는 tooAzure (hello 시나리오의 경우)에 따라에서 지정 된 가상 컴퓨터를 복사 하 고 다음 hello 복제본을 주기적으로 새로 고치는 ASR 있기 때문입니다. 인프라를 계획하는 동안 네트워크 디자인은 회사 RTO 및 RPO 목적을 충족하지 못하도록 방해할 수 있는 잠재적 병목 현상으로 간주되어야 합니다.  

관리자는 toodeploy 재해 복구 솔루션을 계획할 때의 머리 hello 주요 질문 중 하나는 어떻게 hello 가상 컴퓨터가 연결할 수 hello 장애 조치를 완료 한 후 합니다. ASR은 hello 관리자 toochoose hello 네트워크 toowhich 가상 컴퓨터를 연결 된 tooafter 장애 조치 될 수 있습니다. Hello 기본 사이트가 있으면 Azure 네트워크 매핑을 사용 하 여 이렇게 한 다음 VMM 서버에서 관리 하는 온-프레미스 사이트 됩니다. 에 대 한 자세한 내용은 [Azure tooAzure DR에서에서 네트워크 매핑을](site-recovery-network-mapping-azure-to-azure.md) 및 [VMM에서 네트워크 매핑](site-recovery-network-mapping.md)


Hello 복구 사이트에 대 한 hello 네트워크를 디자인, 관리자에 게는 두 가지 선택 사항:

* 복구 사이트에서 네트워크 hello에 대 한 다른 IP 주소 범위를 사용 합니다. 이 시나리오에서는 hello 가상 컴퓨터 장애 조치 후 새 IP 주소를 받습니다 및 관리자에 게 갖기 toodo DNS 업데이트 합니다. 
* Hello 복구 사이트에서 네트워크 hello에 대 한 동일한 IP 주소 범위를 사용 합니다. 특정 시나리오에서 관리자 hello 장애 조치 후에 hello 기본 사이트에 있는 tooretain hello IP 주소를 선호 합니다. 일반적인 시나리오에서 관리자 tooupdate hello 경로 tooindicate hello 새 위치를 hello IP 주소의 가집니다. 아니지만 hello hello 가상 컴퓨터 IP 주소가 그대로 유지 하 고 hello 시나리오 늘어난된 서브넷 기본 hello와 hello 복구 사이트 간에 배포 되는 위치를 선택할 수 없었습니다 됩니다. 두 Azure 네트워크 간에 또는 온-프레미스 네트워크 tooan Azure 네트워크에서에서 서브넷을 스트레치할 수는 없습니다.  

관리자는 toodeploy 재해 복구 솔루션을 계획할 때 자신의 염두 hello 주요 질문 중 하나가 속도가 어떻게 hello 응용 프로그램 됩니다 연결할 수 hello 장애 조치를 완료 한 후. 최신 응용 프로그램은 거의 아무 문제가 실제로 네트워킹 문제를 나타내는 서비스에서 하나의 사이트 tooanother 이동 toosome 정도 네트워킹에 의존 합니다. 재해 복구 솔루션에서 이 문제를 처리하는 두 가지 방법이 있습니다. hello 첫 번째 방법은 toomaintain 고정 IP 주소입니다. 이동 하는 hello 서비스와 호스팅 서버를 물리적으로 다른 위치에 있는 것 hello 불구 하 고 응용 프로그램 사람과 hello IP 주소 구성을 toohello 새 위치를 취해야 합니다. hello 두 번째 방법은 아니지만 완전히 hello 복구 된 사이트에 hello 전환 하는 동안 hello IP 주소를 변경 합니다. 각 방법에는 아래에 요약된 것처럼 여러 가지 구현 변형이 있습니다.

Hello 복구 사이트에 대 한 hello 네트워크를 디자인, 관리자에 게는 두 가지 선택 사항:

## <a name="option-1-retain-ip-addresses"></a>옵션 1: IP 주소 유지
재해 복구 프로세스 측면에서 고정 IP 주소를 사용 하 여 toobe hello 쉬운 메서드 tooimplement 나타나지만의 잠재적인 여러 줄 실제로 있는 과제 hello 가장 인기 없는 접근 방식입니다. Azure Site Recovery hello 기능 모든 시나리오에서 tooretain hello IP 주소를 제공합니다. Tooretain IP를 결정 하기 전에 적절 한 생각 hello 장애 조치 기능에 적용 toohello 제약 조건은 지정 되어야 합니다. 에 대해 알아보겠습니다 하 게 하는 의사 결정 tooretain, IP 주소 또는 not toomake hello 요소입니다. 이는 확대된 서브넷을 사용하거나 전체 서브넷 장애 조치를 수행하여 두 가지 방법으로 달성할 수 있습니다.

### <a name="stretched-subnet"></a>늘어난 서브넷
여기 hello 서브넷 주 데이터베이스와 DR 위치 모두에서 동시에 사용할 수 있습니다. 간단히 말해에서 즉, 서버를 이동할 수 있으며 해당 (계층 3) IP 구성 toohello 두 번째 사이트 및 hello 네트워크에서는 hello 트래픽 toohello 새 위치로 자동으로 라우팅합니다. 이것은 서버 측면에서에서와 trivial toodeal 되었지만 시도 횟수:

* 계층 2(데이터 링크 계층)의 관점에서는 확대 VLAN을 관리할 수 있는 네트워킹 장비가 필요하지만 이제 이것을 광범위하게 사용할 수 있으므로 문제가 적어졌습니다. hello 더 어렵고 두 번째 문제는 hello 늘려서 VLAN hello 잠재적인 오류 도메인을 확장 tooboth 사이트의 경우 기본적으로 단일 실패 지점이 되 고 합니다. 드물지만 브로드캐스트 storm이 시작했지만 경리되게 됩니다. 마지막 문제에 대한 복잡한 의견을 발견했으며 "여기에 이 기술을 절대 구현하지 않겠다"는 의견은 물론 여러 성공적인 구현도 살펴보았습니다.
* 스트레치 된 서브넷으로 DR 사이트 hello에 Microsoft Azure를 사용 하는 경우에 수는 없습니다.

### <a name="subnet-failover"></a>서브넷 장애 조치(failover)
가능한 tooimplement 서브넷 장애 조치 tooobtain hello 장점 없이 여러 사이트에 걸쳐 hello 서브넷 늘이기 위에서 설명한 확대 되므로 hello 서브넷 솔루션의 경우 여기서 지정된 서브넷은 사이트 1 또는 사이트 2에 있으며 두 사이트에 동시에 존재하지 않습니다. 순서 toomaintain hello IP 주소 공간에 hello 이벤트에는 장애 조치 가능한은 tooprogrammatically에서 하나의 사이트 tooanother hello 라우터 인프라 toomove hello 서브넷에 대 한 정렬 합니다. 서브넷은 장애 조치 시나리오 hello hello로 이동 보호 되는 Vm을 연결 합니다. hello 주요 단점은 toothis 방법은 오류가의 hello 이벤트에서 toomove hello 전체 서브넷을 확인 수 있지만 hello 장애 조치 세분성 고려 사항에 영향을 줄 수 있습니다.

Contoso 라는 가상의 기업 수 tooreplicate를가 하는 방법에 대해 살펴보겠습니다 hello 전체 서브넷 장애 조치할 하는 동안 Vm tooa 복구 위치입니다. 먼저 살펴보겠습니다 어떻게 Contoso는 수 toomanage 서브넷 동안 두 Vm 복제 온-프레미스 위치와 다음 다음과 같은 작용이 서브넷 장애 조치 경우의 작동 방식 [Azure는 hello 재해 복구 사이트로 사용 되는](#failover-to-azure)합니다.

#### <a name="failover-from-on-premises-tooazure"></a>온-프레미스 tooAzure에서 장애 조치 
Azure 사이트 복구 (ASR) 가상 컴퓨터에 대 한 재해 복구 사이트로 사용 되는 Azure toobe 수 있습니다.  

Woodgrove Bank라는 가상의 회사가 해당 사업 분야 응용 프로그램을 호스트하는 온-프레미스 인프라를 가지고 Azure에서 해당 모바일 응용 프로그램을 호스트하는 시나리오를 살펴보겠습니다. Azure 및 온-프레미스 서버에서 Woodgrove Bank VM 간의 연결은 사이트 간(S2S) VPN(가상 사설망) 또는 ExpressRoute에서 제공됩니다. S2S VPN Woodgrove Bank의 가상 네트워크를 Azure toobe Woodgrove Bank의 확장 온-프레미스 네트워크로 간주할 수 있습니다. 이 통신은 Woodgrove Bank 에지와 Azure 가상 네트워크 간의 S2S VPN을 통해 활성화됩니다. 이제 Woodgrove 기본 Azure 지역 tooanother Azure 지역 실행 되는 해당 작업 toouse ASR tooreplicate를 원합니다. 이 옵션 경제적이 고 DR 옵션이 되었고 공용 클라우드 환경에서 수 toostore 데이터 woodgrove hello 요구를 충족 합니다. Woodgrove toodeal 응용 프로그램과 하드 코드 된 IP 주소에 따라 달라 지는 구성, 따라서 있느냐 응용 프로그램에 대 한 요구 사항 tooretain IP 주소 실패 한 후 Azure에서 tooanother 영역 됩니다.

Woodgrove는 Azure에서 실행 하는 IP 주소 범위 (172.16.1.0/24, 172.16.2.0/24) tooits 리소스에서 tooassign IP 주소를 결정 했습니다.

Hello IP 주소를 유지 하면서 해당 가상 컴퓨터 tooAzure Woodgrove toobe 수 tooreplicate에 대 한 Azure 가상 네트워크 필요 toobe 생성 합니다. 응용 프로그램이 원활 하 게 hello 온-프레미스 사이트 tooAzure에서 장애 조치를 수행할 수 있도록 하는 hello 온-프레미스 네트워크 확장 여야 합니다. Azure에서는 tooadd 지점 및 사이트와 사이트 간 VPN 연결 toohello 만든 가상 네트워크에서 Azure 있습니다. 사이트 간 연결을 설정할 때 Azure 네트워크를 있습니다 tooroute 트래픽 toohello 온-프레미스 위치를 (Azure 호출 로컬 네트워크) Azure 하지 때문에 hello IP 주소 범위는 hello 온-프레미스 IP 주소 범위와에서 다른 경우에 늘이기 서브넷을 지원 합니다.  즉, 있는 경우 서브넷 192.168.1.0/24 온-프레미스 수 없는 로컬 네트워크 192.168.1.0/24 hello Azure 네트워크에에서 추가 합니다. Azure Vm이 없습니다 활성 hello 서브넷에서 및 해당 hello 서브넷 DR 용도에 만들어집니다 인식 하지 않으므로 1 세대입니다. toobe 수 toocorrectly 네트워크 트래픽을 라우팅할 hello 네트워크 및 hello 로컬 네트워크에는 Azure 네트워크 hello 서브넷에서 충돌 하지 않아야 합니다.

![서브넷 장애 조치 전](./media/site-recovery-network-design/network-design7.png)

장애 조치(failover) 전

toohelp Woodgrove 해당 비즈니스 요구를 충족, tooimplement hello 워크플로 수행 해야 합니다.

* 주세요 복구 네트워크를 hello 장애 조치 된 가상 컴퓨터를 만들 수는 있는 호출, 추가 네트워크를 만듭니다.
* tooensure hello IP는 VM에 대 한 장애 조치 후 유지 됩니다 VM 속성에서 toohello 구성 탭, 지정 hello VM hello 동일한 IP 온-프레미스에 있으며 저장을 클릭 합니다. Hello VM 장애 조치 되는 경우 Azure Site Recovery hello 제공 된 IP toohello 가상 컴퓨터를 할당 합니다.

![네트워크 속성](./media/site-recovery-network-design/network-design8.png)

Toothis 네트워크 연결을 사용 하 여 설정할 수 hello 장애 조치가 트리거됩니다 hello 가상 컴퓨터가 원하는 hello IP 사용 하 여 복구 네트워크 hello에 생성 되 면는 [Vnet tooVnet 연결](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다. 필요한 경우 이 작업은 스크립팅될 수 있습니다.  설명한 대로 hello 이전 섹션에서 장애 조치 tooAzure의 hello 경우에도 서브넷 장애 조치에 대 한 경로 toobe 적절 하 게 수정한 tooreflect 해당 192.168.1.0/24 이제 tooAzure 옮겼습니다.

![서브넷 장애 조치 후](./media/site-recovery-network-design/network-design9.png)

장애 조치(failover) 후

경우 위의 hello 그림에 나와 있는 것 처럼 ' Azure 네트워크 ' 필요는 없습니다. Hello 장애 조치 후 ' 주 사이트 ' 및 ' 복구 네트워크 ' 간의 사이트 toosite vpn 연결을 만들 수 있습니다.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>장애 조치 tooa 보조 온-프레미스 사이트
에 대해 알아보겠습니다 시나리오를 원하는 위치로 hello Vm 각각의 hello IP를 유지 하 고 장애 조치 hello 서브넷을 함께 완료 됩니다. hello 기본 사이트의 서브넷 192.168.1.0/24에서 실행 중인 응용 프로그램입니다. Hello 장애 조치 하는 경우이 서브넷의 일부인 모든 hello 가상 컴퓨터는 toohello 복구 사이트를 통해 실패 하며 해당 IP 주소를 유지 합니다. 경로 갖습니다 toobe toosubnet 192.168.1.0/24 속한 모든 hello 가상 컴퓨터 복구 사이트 toohello 이동 이제 했습니다 tooreflect hello 팩트를 적절 하 게 수정 합니다.

Hello에서 다음 그림 hello 주 사이트 및 사이트 복구, 세 번째 사이트 및 기본 사이트 사이의 경로 조정 하 고 세 번째 사이트와 복구 사이트 toobe 적절히 수정 해야 합니다.

다음 그림에서는 hello 서브넷 hello 장애 조치 하기 전에 번호입니다. 서브넷 192.168.0.1/24 hello 장애 조치 하기 전에 hello 기본 사이트에서 활성화 되 고 hello 장애 조치 후 hello 복구 사이트의 활성화 됩니다.

![장애 조치(failover) 전](./media/site-recovery-network-design/network-design2.png)

장애 조치(failover) 전

아래 hello 그림 장애 조치 후 네트워크 및 서브넷을 보여 줍니다.

![장애 조치(failover) 후](./media/site-recovery-network-design/network-design3.png)

장애 조치(failover) 후

보조 사이트는 온-프레미스 VMM 서버 toomanage를 사용 하 고 다음 때 ASR 특정 가상 컴퓨터에 대 한 보호 사용 toohello 워크플로 다음에 따라 네트워킹 리소스를 할당 합니다.

* ASR은 hello 고정 IP 주소 풀에서 각 System Center VMM 인스턴스에 대 한 hello 관련 네트워크에 정의 된 hello 가상 컴퓨터에서 각 네트워크 인터페이스에 대 한 IP 주소를 할당 합니다.
* 동일한 IP 주소와 hello 복구 사이트에 hello 네트워크에 대 한 풀 hello의 hello IP 주소 풀의 네트워크 hello IP 주소 toohello 복제본 가상 컴퓨터 ASR을 할당 하는 동안 hello 기본 사이트에 할당 하는 hello hello 같은 관리자에 게 정의 하는 경우 Hello 주 가상 컴퓨터의 IP 주소입니다.  hello IP VMM에서 예약 되어 있지만 hello hyper-v 호스트에 장애 조치 IP로 설정 하지 합니다. Hyper-v 호스트에서 장애 조치 IP hello 장애 조치 하기 바로 전에 설정 됩니다.


Hello 동일한 IP를 사용할 수 없는 경우 ASR은 정의 된 hello IP 주소 풀에서 몇 가지 다른 사용 가능한 IP 주소를 할당 합니다.

VM에서 보호를 사용할 hello 후 다음 toohello 가상 컴퓨터 할당 된 샘플 스크립트 tooverify hello IP를 사용할 수 있습니다. hello 동일한 IP 장애 조치 IP로 설정 되 고 장애 조치 시 hello toohello VM을 할당 합니다.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> 가상 컴퓨터는 DHCP를 사용 하는 hello 시나리오에서 IP 주소의 hello 관리 ASR의 hello 제어 범위를 벗어난 완전히입니다. 관리자가 tooensure hello에서 hello DHCP 서버 서비스 hello IP 주소 hello 복구 사이트에서 사용할 수 있는 hello 기본 사이트의 동일한 범위입니다.
>
>



## <a name="option-2-changing-ip-addresses"></a>옵션 2: IP 주소 변경
이 방법은 toobe hello 가장 널리 퍼진 관찰 한 내용에 따라 것 같습니다. 걸리는 hello 형태의 장애 조치 hello와 관련 된 모든 VM의 hello IP 주소를 변경 합니다. 이 방법의 단점은 hello 들어오는 네트워크 too'learn 필요 ' IPy IPx에 된 hello 응용 프로그램 상태가 됩니다. IPx 및 IPy은 논리적 이름, 경우에 DNS 항목을 일반적으로 변경 되거나 hello 네트워크 전체에 걸쳐 플러시 toobe 및 네트워크 테이블의 캐시 된 항목 업데이트 되거나 플러시 toobe로 따라서 가동 중지 시간이 나타날 수 있습니다 어떻게 hello DNS 인프라에 따라 합니다. 인트라넷 응용 프로그램의 경우 hello 낮은 TTL 값을 사용 하 고 사용 하 여 이러한 문제를 완화 될 [ASR와 함께 Azure 트래픽 관리자](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) 인터넷 기반 응용 프로그램

### <a name="changing-hello-ip-addresses---illustration"></a>그림 hello IP 주소-를 변경합니다.
에 대해 알아보겠습니다 hello 시나리오 toouse 계획인 기본 hello 및 hello 복구 사이트에서 다른 Ip입니다. 다음 예제는 hello에 주 가상 컴퓨터 또는 복구 사이트에서 호스팅되는 hello 응용 프로그램에 액세스할 수 있는에서 세 번째 사이트를 해야 합니다.

![다른 IP - 장애 조치 전](./media/site-recovery-network-design/network-design10.png)


위의 hello 그림에는 서브넷 192.168.1.0/24 서브넷 hello 기본 사이트에서 호스트 되는 일부 응용 프로그램 및 있다가 구성된 toocome를 hello 복구 사이트에서 서브넷 172.16.1.0/24 장애 조치 후 합니다. 세 사이트 모두 서로 액세스할 수 있도록 VPN 연결/네트워크 라우팅이 적절하게 구성되었습니다.

하나 이상의 응용 프로그램을 장애 조치할 후 쇼, 아래 hello 그림으로 hello 복구 서브넷에 있는 복원은 됩니다. 이 경우 없는 제한 된 toofailover hello 전체 서브넷 hello에서 같은 시간입니다. 필요한 tooreconfigure VPN 또는 네트워크 경로 변경 되지 않았습니다. 장애 조치(failover) 및 일부 DNS 업데이트는 응용 프로그램이 액세스할 수 있도록 유지합니다. Hello DNS가 구성 된 tooallow 동적 업데이트 하는 경우 다음 hello 가상 컴퓨터는 등록 장애 조치 후 시작 되 면 hello 새 IP를 사용 하 여 자신입니다.

![다른 IP - 장애 조치 후](./media/site-recovery-network-design/network-design11.png)


장애 조치 hello 복제 가상 컴퓨터 수에 IP 주소가 없는 후 hello 주 가상 컴퓨터의 hello IP 주소로 hello 동일 합니다. 가상 컴퓨터를 사용 하는 hello DNS 서버를 업데이트 합니다 후 시작 합니다. DNS 항목을 일반적으로 변경 되거나 hello 네트워크 전체에 걸쳐 플러시 toobe 있고 네트워크 테이블의 캐시 된 항목 업데이트 되거나 플러시되 면 toobe 이러한 상태 변경을 수행 하는 동안 가동 중지 시간을 처리 하는 경우를 흔히 볼 toobe 되기 때문입니다. 이 문제는 다음으로 완화할 수 있습니다.

* 인트라넷 응용 프로그램의 경우 낮은 TTL 값 사용
* 인터넷 기반 응용 프로그램에 대한 ASR과 함께 Azure 트래픽 관리자 사용
* Hello 다음을 사용 하 여 복구에 내에서 스크립트 계획 tooupdate hello DNS 서버 tooensure 시기 적절 한 업데이트 (hello 스크립트가 필요 하지 않습니다 hello 동적 DNS 등록 구성 된 경우)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>변경 hello IP 주소-DR tooAzure
hello [재해 복구 사이트도 Microsoft Azure 네트워킹 인프라 설치](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) 블로그 게시물 toosetup hello 필요한 IP 주소를 유지 하는 경우 Azure 네트워킹 인프라 요구 사항이 없는 하는 방법에 대해 설명 합니다. Hello 응용 프로그램 및 어떻게 toosetup 네트워킹 온-프레미스 및 다음 보기를 설명 하는 Azure 및 다음 마지막 방법으로이 메서드는 먼저 toodo 테스트 장애 조치 및 계획된 된 장애 조치 합니다.

## <a name="next-steps"></a>다음 단계
[자세한 내용은](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) VMM 서버를 사용 하는 toomanage hello 주 사이트 중인 경우 사이트 복구 원본 및 대상 네트워크를 매핑하는 방법입니다.
