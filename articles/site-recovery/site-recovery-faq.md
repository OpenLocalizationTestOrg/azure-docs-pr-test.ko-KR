---
title: "Azure Site Recovery: 질문과 대답(FAQ) | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에 대한 일반적인 질문에 대답합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: FAQ(질문과 대답)
이 문서는 Azure Site Recovery에 대한 질문과 대답을 제공합니다. 이 문서를 읽은 후 질문이 있으면 hello에 게시할 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="general"></a>일반
### <a name="what-does-site-recovery-do"></a>Site Recovery의 기능은 무엇입니까?
Site Recovery 오케스트레이션 하 고 영역, 온-프레미스 가상 컴퓨터 및 물리적 서버 tooAzure 간에 Azure Vm의 복제를 자동화 함으로써 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 강화 하 고 온-프레미스 컴퓨터 tooa 보조 데이터 센터입니다. [자세히 알아봅니다](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Site Recovery로 무엇을 보호할 수 있습니까?
* **Azure VM**: Site Recovery는 지원되는 Azure VM에서 실행 중인 모든 워크로드를 복제할 수 있습니다.
* **VMware 가상 컴퓨터**: Site Recovery는 Hyper-V VM에서 실행 중인 모든 워크로드를 보호할 수 있습니다.
* **물리적 서버**: Site Recovery는 Windows 또는 Linux를 실행하는 물리적 서버를 보호할 수 있습니다.
* **VMware 가상 컴퓨터**: Site Recovery는 VMware VM에서 실행 중인 모든 워크로드를 보호할 수 있습니다.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>사이트 복구 hello Azure 리소스 관리자 모델을 지원 합니까?
사이트 복구는 hello에 대 한 리소스 관리자를 지 원하는 Azure 포털에서 사용할 수 있습니다. 사이트 복구 hello Azure 클래식 포털에서에서 기존 배포를 지원합니다. Hello 클래식 포털에서 새 자격 증명 모음을 만들 수 없습니다 및 새로운 기능에서 지원 되지 않습니다.

### <a name="can-i-replicate-azure-vms"></a>Azure VM을 복제할 수 있나요?
예, Azure 지역 간에 지원되는 Azure VM을 복제할 수 있습니다. [자세히 알아봅니다](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>사이트 복구와 Hyper-v tooorchestrate 복제에 어떻게 해야 합니까?
Hyper-v 호스트 서버 hello 필요한 hello 배포 시나리오에 따라 다릅니다. 체크 아웃 하 hello에 Hyper-v 필수 구성 요소:

* [Hyper-v Vm (VMM 없음) tooAzure 복제](site-recovery-hyper-v-site-to-azure.md)
* [(VMM)과 Hyper-v Vm tooAzure 복제](site-recovery-vmm-to-azure.md)
* [Hyper-v Vm tooa 보조 데이터 센터에 복제](site-recovery-vmm-to-vmm.md)
* 데이터 센터에 대해 알아보세요 tooa 보조 복제 하는 경우 [Hyper-v Vm에 대 한 지원 되는 게스트 운영 체제](https://technet.microsoft.com/library/mt126277.aspx)합니다.
* 사이트 복구 된 모든 hello 게스트 운영 체제 지원 tooAzure를 복제 하는 경우 [Azure에서 지 원하는](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx)합니다.

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Hyper-V가 클라이언트 운영 체제에서 실행 중인 경우 VM을 보호할 수 있습니까?
아니요, VM은 지원되는 Windows 서버 컴퓨터를 실행하는 Hyper-V 호스트 서버에 위치해야 합니다. Tooprotect 필요한 경우 클라이언트 컴퓨터를 복제 하기 물리적 컴퓨터로 너무[Azure](site-recovery-vmware-to-azure.md) 또는 [보조 데이터 센터](site-recovery-vmware-to-vmware.md)합니다.

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Site Recovery로 어떤 워크로드를 보호할 수 있습니까?
지원 되는 VM 또는 실제 서버에서 실행 되는 대부분 작업 사이트 복구 tooprotect를 사용할 수 있습니다. 사이트 복구 앱 될 수 있도록 응용 프로그램 인식 복제에 대 한 지원을 제공 tooan 지능형 상태를 복구 합니다. SharePoint, Exchange, Dynamics, SQL Server, Active Directory와 같은 Microsoft 응용 프로그램과 통합되고, Oracle, SAP, IBM, Red Hat 등의 선두 공급 업체 제품과 긴밀하게 작동합니다. [자세히 알아봅니다](site-recovery-workload.md) .

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Hyper-v 호스트를 VMM 클라우드에 toobe 필요 합니까?
Hyper-v Vm에 있어야 합니다. 그런 다음 원하는 tooreplicate tooa 보조 데이터 센터, Hyper-v가 VMM 클라우드에 있는 서버를 호스팅합니다. Tooreplicate tooAzure 원하는 Vm 상관 없이 VMM 클라우드의 Hyper-v 호스트 서버에 복제할 수 있습니다. [자세히 알아보기](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>VMM 서버가 하나밖에 없는 경우 VMM을 사용하여 Site Recovery를 배포할 수 있습니까?

예. Hello VMM 클라우드 tooAzure Hyper-v 서버에서 Vm을 복제 하거나 하거나 복제할 수 있습니다 hello에 대 한 VMM 클라우드 간의 동일 서버. 온-프레미스 tooon 온-프레미스 복제에 대 한 두 hello 기본 및 보조 사이트 모두에 VMM 서버가 있어야 하는 것이 좋습니다.  

### <a name="what-physical-servers-can-i-protect"></a>어떤 물리적 서버를 보호할 수 있습니까?
Windows 및 Linux tooAzure 또는 tooa 보조 사이트를 실행 하는 물리적 서버를 복제할 수 있습니다. [알아봅니다](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) .  물리적 서버 tooAzure 또는 tooa 보조 사이트에 복제 하는 관계 없이 동일한 요구 사항을 적용 하는 번호입니다.


온-프레미스 서버가 중지되면 물리적 서버가 Azure에서 VM으로 실행됩니다. 장애 복구 tooan 온-프레미스 물리적 서버에서 현재 지원 되지 않습니다. 물리적으로 보호 하는 컴퓨터를 장애 복구 tooa VMware 가상 컴퓨터만 할 수 있습니다.

### <a name="what-vmware-vms-can-i-protect"></a>어떤 VMware VM을 보호할 수 있습니까?

VMware Vm tooprotect vSphere 하이퍼바이저 및 VMware 도구를 실행 중인 가상 컴퓨터가 필요 합니다. 또한 VMware vCenter server toomanage hello 하이퍼바이저 있는지는 것이 좋습니다. [자세한 내용은](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) VMware 서버 및 Vm tooAzure 또는 tooa 보조 사이트를 복제 하기 위한 정확한 요구 사항에 대 한 합니다.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Site Recovery로 지사의 재해 복구를 관리할 수 있습니까?
예. 사이트 복구 tooorchestrate 복제 및 장애 조치를 사용 하 여 지사에는 중앙 위치에 통합 된 오케스트레이션 및 모든 분기 office 작업 부하의 보기 얻게 됩니다. 쉽게 장애 조치를 실행 하 고 hello 분기를 방문 하지 않고도 본사에서 모든 분기의 재해 복구를 관리할 수 있습니다.

## <a name="pricing"></a>가격

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Azure Site Recovery를 사용하는 동안 어떤 요금이 발생하나요?
사이트 복구를 사용 하는 경우에 hello Site Recovery 라이선스, Azure 저장소, 저장소 트랜잭션 및 아웃 바운드 데이터 전송 요금이 발생 합니다. [자세히 알아봅니다](https://azure.microsoft.com/pricing/details/site-recovery).

보호 된 VM 또는 실제 서버 인스턴스 여기서는 인스턴스당 hello Site Recovery 라이선스가입니다.

- VM 디스크 복제 tooa 표준 저장소 계정, Azure 저장소 청구 hello hello 저장소 사용량입니다. 예를 들어 hello 원본 디스크 크기가 1TB 및 400GB 사용 되는, 사이트 복구 1TB VHD Azure에서 만들지만 400GB (및 복제 로그에 사용 되는 저장 공간의 hello 크기) hello 저장소 요금이 청구 됩니다.
- VM 디스크 복제 tooa 프리미엄 저장소 계정, Azure 저장소 청구 hello 프리미엄 저장소 디스크 옵션에 가장 가까운 hello에 대 한 완성 hello 프로 비전 된 저장소 크기입니다. 예를 들어 hello 원본 디스크 크기가 50GB 인 경우 사이트 복구 50GB 디스크 Azure에서 만들고 Azure 프리미엄 저장소 디스크 (P10) 가장 가까운이 toohello 매핑합니다.  Hello 50GB 디스크 크기가 아니라 P10에 비용을 계산 합니다.  [자세히 알아봅니다](https://aka.ms/premium-storage-pricing).  프리미엄 저장소를 사용 하는 경우 복제 로깅에 대 한 표준 저장소 계정을 필요 하 고 이러한 로그에 사용 되는 표준 저장소 공간의 hello 크기도 요금이 청구 됩니다.
- 테스트 장애 조치(failover) 또는 장애 조치(failover) 때까지 디스크가 만들어지지 않습니다. Hello 복제 상태의 저장소 요금을 "페이지 blob 및 디스크"의 hello 범주 hello에 따라 [저장소 가격 계산기](https://azure.microsoft.com/en-in/pricing/calculator/) 발생 합니다. 이러한 요금은 hello 저장소의 형식을 기반으로 premium/standard 및 hello 데이터 중복-LRS, GRS, RA-GRS 등을 입력 합니다.
- 장애 조치 선택 된 hello 옵션 toouse에서 디스크를 관리 하는 경우 [관리 하는 디스크에 대 한 청구가](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) 장애 조치/테스트 장애 조치 후에 적용 합니다. 복제 중에는 관리 디스크 비용이 적용되지 않습니다.
- Hello에 따라 저장소 요금이 "페이지 blob 및 디스크"의 hello 범주 hello 옵션 toouse 관리 되는 디스크는 장애 조치를 선택 하지 않으면 [저장소 가격 계산기](https://azure.microsoft.com/en-in/pricing/calculator/) 장애 조치 된 후 발생 합니다. 이러한 요금은 hello 저장소의 형식을 기반으로 premium/standard 및 hello 데이터 중복-LRS, GRS, RA-GRS 등을 입력 합니다.
- 저장소 트랜잭션은 안정적 상태 복제 동안 및 장애 조치(failover)/테스트 장애 조치(failover) 후 기본 VM 작업에 대해 요금이 청구됩니다. 하지만 이러한 청구 요금은 무시할 수 있습니다.

또한 비용은 hello VM, 저장소, 전송 및 저장소 트랜잭션 비용을 적용할 테스트 장애 조치 하는 동안 발생 합니다.



## <a name="security"></a>보안
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>복제 데이터를 Site Recovery 서비스 toohello 전송 되나요?
아니요, Site Recovery는 복제된 데이터를 가로채거나 사용자의 가상 컴퓨터 또는 물리적 서버에서 실행 중인 항목에 대한 정보를 보유하지 않습니다.
복제 데이터는 온-프레미스 Hyper-V 호스트, VMware 하이퍼바이저 또는 물리적 서버와 Azure 저장소 또는 보조 사이트 간에 교환됩니다. 사이트 복구에는 해당 데이터 기능 toointercept 없습니다. Hello 메타 데이터만 필요한 tooorchestrate 복제 및 장애 조치 toohello Site Recovery 서비스에 전송 됩니다.  

사이트 복구 이며 ISO 27001: 2013, 27018, HIPAA, DPA 인증 SOC2 및 FedRAMP JAB 평가 hello 진행 중인 합니다.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>규정 준수 상의 이유로 우리의 온-프레미스 메타 데이터도 내에 머물러 있어야 hello 동일한 지리적 지역입니다. Site Recovery가 도움이 되나요?
예. 영역에 사이트 복구 자격 증명 모음을 만들 때 인지 확인 하는 모든 메타 데이터를 복제를 오케스트레이션 및 tooenable 필요 하 고 해당 지역 내에서 장애 조치가 지리적 경계입니다.

### <a name="does-site-recovery-encrypt-replication"></a>Site Recovery는 복제를 암호화합니까?
온-프레미스 사이트 간에 가상 컴퓨터와 물리적 서버를 복제할 때 전송 중 암호화가 지원됩니다. 가상 컴퓨터 및 물리적 서버 tooAzure를 모두 암호화-전송 중인 복제 및 [(Azure)의 나머지에 암호화](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) 지원 됩니다.

## <a name="replication"></a>복제

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>사이트 간 VPN tooAzure 통해 복제할 수 있습니까?
Azure Site Recovery 공용 끝점을 통해 데이터 tooan Azure 저장소 계정에 복제합니다. 사이트 간 VPN을 통해 복제되지 않습니다. Azure 가상 네트워크를 사용하여 사이트 간 VPN을 만들 수 있습니다. Site Recovery 복제를 방해하지 않습니다.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>ExpressRoute tooreplicate 가상 컴퓨터 tooAzure를 사용할 수 있습니까?
예, ExpressRoute 사용된 tooreplicate 가상 컴퓨터 tooAzure 될 수 있습니다. Azure Site Recovery에는 공용 끝점을 통해 데이터 tooan Azure 저장소 계정 복제합니다. Tooset 필요한 [공용 피어 링](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute 사이트 복구 복제에 대 한 합니다. Hello 가상 컴퓨터는 장애 조치 한 tooan Azure 가상 네트워크에 액세스할 수 있습니다 hello를 사용 하 여 [개인 피어 링](../expressroute/expressroute-circuit-peerings.md#private-peering) hello Azure 가상 네트워크를 사용 하 여 설치 합니다.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>가상 컴퓨터 tooAzure 복제 하기 위한 필수 구성 요소가 있습니까?
Tooreplicate tooAzure 원하는 가상 컴퓨터에서 준수 해야 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.

Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Hyper-v 세대 가상 컴퓨터 2 tooAzure를 복제할 수 있습니까?
예. 사이트 복구 장애 조치 중 2 세대 toogeneration 1에서에서 변환합니다. 장애 복구 hello 컴퓨터는 변환 된 뒤로 toogeneration 2 됩니다. [자세히 알아보기](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Azure Vm에 대 한 납부 어떻게 tooAzure 복제 하는 경우?
일반 복제 하는 동안 데이터는 복제 된 toogeo 중복 Azure 저장소 않아도 되며 toopay 모든 Azure IaaS 가상 컴퓨터 요금, 중요 한 장점을 제공 합니다. 자동으로 장애 조치 tooAzure, 사이트 복구를 실행할 때 Azure IaaS 가상 컴퓨터를 만들고 그 후 비용이 청구 됩니다 Azure에서 사용 하는 hello 계산 리소스에 대 한 합니다.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>SDK와 함께 Site Recovery 시나리오를 자동화할 수 있습니까?
예. Hello Rest API, PowerShell 또는 hello Azure SDK를 사용 하 여 사이트 복구 워크플로 자동화할 수 있습니다. 현재 PowerShell을 사용하여 Site Recovery를 배포하기 위한 지원되는 시나리오:

* [VMMs 클라우드 tooAzure PowerShell 리소스 관리자에서에서 Hyper-v Vm으로 복제](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [VMM tooAzure PowerShell 리소스 관리자 없이 Hyper-v Vm 복제](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>TooAzure 복제할 경우 어떤 저장소 계정이 필요 합니까?
* **Azure 클래식 포털**: hello Azure 클래식 포털에서에서 사이트 복구를 배포할 경우 필요 합니다는 [표준 지역 중복 저장소 계정](../storage/common/storage-redundancy.md#geo-redundant-storage)합니다. 프리미엄 저장소는 현재 지원되지 않습니다. hello 계정은 hello에 있어야 hello 사이트 복구 자격 증명 모음과 동일한 지역입니다.
* **Azure 포털**: hello Azure 포털에서에서 사이트 복구를 배포할 경우 LRS 또는 GRS 저장소 계정이 필요 합니다. 데이터는 지역 가동 중단 발생 하는 경우 또는 기본 지역의 hello를 복구할 수 없는 경우 탄력적 있도록 GRS를 좋습니다. hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다. 프리미엄 저장소 hello Azure 포털에서에서 사이트 복구를 배포 하는 경우 VMware VM, Hyper-v VM 및 물리적 서버 복제에 지원 됩니다.

### <a name="how-often-can-i-replicate-data"></a>데이터를 얼마나 자주 복제할 수 있나요?
* **Hyper-V:** Hyper-V VM은 30초(프리미엄 저장소 제외), 5분 또는 15분마다 복제할 수 있습니다. SAN 복제를 설정하면 복제가 동기화됩니다.
* **VMware 및 물리적 서버:** 복제 빈도는 이와 관련이 없습니다. 복제가 계속 됩니다.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>기존 복구 사이트 tooanother 3 차 사이트에서 복제를 확장할 수 있습니까?
확장 복제 또는 체인으로 연결된 복제는 지원되지 않습니다. [사용자 의견 포럼](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication)을 통해 이 기능에 대한 의견을 보내 주세요.

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>하면 오프 라인 복제 hello tooAzure 복제할 처음으로?
지원되지 않습니다. Hello에이 기능을 요청 [피드백 포럼](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from)합니다.

### <a name="can-i-exclude-specific-disks-from-replication"></a>특정 디스크를 복제에서 제외할 수 있습니까?
있는 경우이 지원 [VMware Vm과 Hyper-v Vm 복제](site-recovery-exclude-disk.md) hello Azure 포털을 사용 하 여 tooAzure 합니다.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>동적 디스크를 사용하여 가상 컴퓨터를 복제할 수 있습니까?
동적 디스크는 Hyper-V 가상 컴퓨터를 복제할 때 지원됩니다. 값 형식은 또한 VMware Vm 및 tooAzure 물리적 컴퓨터를 복제 하는 경우 지원 됩니다. hello 운영 체제 디스크는 기본 디스크 여야 합니다.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>새 컴퓨터 tooan 기존 복제 그룹을 추가할 수 있습니까?
새 컴퓨터 tooexisting 복제 그룹을 추가 지원 됩니다. 따라서 toodo는 hello 복제 그룹 ('복제 된 항목' 블레이드에서) 및 hello 복제 그룹에 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭/선택을 선택 하 고 hello 적절 한 옵션을 선택 합니다.

![Tooreplication 그룹 추가](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Hyper-V 복제 트래픽에 할당된 대역폭을 제한할 수 있습니까?
예. 자세한 내용은 hello 배포 문서에서 대역폭을 제한 하는 방법에 대 한:

* [VMware VM 및 물리적 서버를 복제하기 위한 용량 계획](site-recovery-plan-capacity-vmware.md)
* [VMM 클라우드에서 Hyper-V VM을 복제하기 위한 용량 계획](site-recovery-vmm-to-azure.md#capacity-planning)
* [VMM 없이 Hyper-V VM을 복제하기 위한 용량 계획](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>장애 조치(failover)
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>I tooAzure를 통해 실패 한 경우 어떻게 액세스 합니까 hello Azure 가상 컴퓨터 장애 조치 후?
Hello Azure Vm 보안 인터넷 연결을 통해, 사이트 간 VPN을 통해 또는 Azure ExpressRoute를 통해 액세스할 수 있습니다. Tooprepare 다양 한 작업 순서 tooconnect에 필요 합니다. [자세히 알아보기](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Azure 되었는지 확인 하려면 어떻게 tooAzure 장애 조치할 합니까 내 데이터는 탄력적?
Azure는 복원을 위해 디자인되었습니다. 사이트 복구는 이미 장애 조치 tooa 보조 Azure 데이터 센터를 Azure SLA hello 필요한 경우 발생 하는 hello에 따라 엔지니어링 합니다. 이런, 확인 메타 데이터 및 자격 증명 모음 hello 내에 유지 하는 경우 자격 증명 모음에 대해 선택한 동일한 지리적 지역입니다.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>두 데이터 센터 간에 복제하는 동안 주 데이터 센터에서 예기치 않게 정전이 발생하면 어떻게 됩니까?
Hello 보조 사이트에서 계획 되지 않은 장애 조치를 트리거할 수 있습니다. 사이트 복구 hello 주 사이트 tooperform hello 장애 조치에서의 연결에 필요 하지 않습니다.

### <a name="is-failover-automatic"></a>장애 조치(failover)는 자동입니까?
자동이 아닙니다. Hello 포털에서 번의 클릭으로 장애 조치를 시작 하거나 사용할 수 있습니다 [사이트 복구 PowerShell](/powershell/module/azurerm.siterecovery) tootrigger 장애 조치 합니다. 장애 복구 하는 것은 hello Site Recovery 포털에서 간단한 작업입니다.

tooautomate 사용할 수 있습니다 온-프레미스 가상 컴퓨터 오류 toodetect Orchestrator 또는 Operations Manager와 SDK hello 다음 트리거 hello 장애 조치를 사용 하 여 합니다.

* [자세한](site-recovery-create-recovery-plans.md) 복구 계획을 알아봅니다.
* [자세히 알아보기](site-recovery-failover.md) .
* [자세히 알아보기](site-recovery-failback-azure-to-vmware.md) 

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>내 온-프레미스 호스트가 응답 하지 않거나 손상 아닌 경우 I 장애 조치할 수 백 tooa 다른 호스트?
예, hello 대체 위치 복구 toofailback tooa 다른 호스트 Azure에서 사용할 수 있습니다. Hyper-v 및 VMware 가상 컴퓨터에 대 한 hello 옵션 hello 아래 링크에에서 대 한 자세한 읽기입니다.

* [VMware 가상 컴퓨터](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Hyper-V 가상 컴퓨터](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>서비스 공급자
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>서비스 공급자입니다. Site Recovery는 전용 및 공유 인프라 모델에 대해 작동합니까?
예, Site Recovery는 전용 및 공유 인프라 모델 모두에 대해 작동합니다.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>서비스 공급자에 대 한 hello Site Recovery 서비스와 공유 내 테 넌 트의 hello id가입니다.
아니요. 테넌트 ID는 익명으로 유지됩니다. 테 넌 트 액세스 toohello 사이트 복구 포털이 필요 하지 않습니다. 서비스 공급자 관리자만 hello hello 포털 상호 작용합니다.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>테 넌 트 응용 프로그램 데이터도 이동 tooAzure?
서비스 공급자 소유한 사이트 간의 복제를 하는 경우 응용 프로그램 데이터는 tooAzure 절대로 계산 합니다. 전송 하 고 hello 서비스 공급자 사이트 간에 직접 복제 된 데이터는 암호화 됩니다.

TooAzure를 복제 하는 경우에 응용 프로그램 데이터 tooAzure 저장소 하지만 toohello Site Recovery 서비스 하지 보내집니다. 데이터는 전송 중에 암호화되어 Azure에 암호화된 상태로 남아 있습니다.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>내 테넌트로 Azure 서비스에 대한 청구서가 발급됩니까?
아니요. Azure의 요금 청구 관계 hello 서비스 공급자와 직접입니다. 서비스 공급자는 해당 테넌트에 대한 특정 청구서를 생성하는 일을 담당합니다.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>TooAzure를 복제 계획 이라면 필요한 무엇입니까 Azure의 가상 컴퓨터 toorun 항상?
아니요, 데이터는 복제 된 tooan 구독에서 Azure 저장소 계정입니다. 테스트 장애 조치(failover)(DR 드릴) 또는 실제 장애 조치(failover)를 수행하면 Site Recovery가 구독에서 자동으로 가상 컴퓨터를 만듭니다.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>TooAzure 복제할 때 테 넌 트 수준의 격리를 유지 됩니까?
예.

### <a name="what-platforms-do-you-currently-support"></a>현재 어떤 플랫폼이 지원됩니까?
Azure Pack, 클라우드 플랫폼 시스템 및 시스템 센터 기반(2012 이상)의 배포가 지원됩니다. [자세히 알아봅니다](https://technet.microsoft.com/library/dn850370.aspx) .

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>단일 Azure Pack 및 단일 VMM 서버 배포가 지원되나요?
예, Hyper-v 가상 컴퓨터 tooAzure 복제할 수 있습니다 또는 서비스 공급자 사이트 간 합니다.  서비스 공급자 사이트 간에 복제할 경우 Azure Runbook 통합을 사용할 수 없습니다.

## <a name="next-steps"></a>다음 단계
* 읽기 hello [Site Recovery 개요](site-recovery-overview.md)
* 알아봅니다 [Site Recovery 아키텍처](site-recovery-components.md)  
