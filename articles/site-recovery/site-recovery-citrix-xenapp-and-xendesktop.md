---
title: "Azure Site Recovery를 사용 하 여 다중 계층 Citrix XenDesktop 및 XenApp 배포 aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 Azure Site Recovery를 사용 하 여 tooprotect 및 복구 Citrix XenDesktop 및 XenApp 배포 합니다."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 다중 계층 Citrix XenApp 및 XenDesktop 배포 복제

## <a name="overview"></a>개요

Citrix XenDesktop ondemand 서비스 tooany 사용자로 아무 곳 이나 데스크톱 및 응용 프로그램을 제공 하는 데스크톱 가상화 솔루션입니다. FlexCast 배달 기술로 XenDesktop 빠르고 안전 하 게 전달할 수 응용 프로그램 및 데스크톱 toousers.
현재 Citrix XenApp은 재해 복구 기능을 제공하지 않습니다.

좋은 재해 복구 솔루션을 복잡 한 응용 프로그램 아키텍처 위에 hello 주위 복구 계획의 모델링을 허용 하 고 hello 기능 사용자 지정 tooadd 단계 toohandle 응용 프로그램 간의 매핑을 제공 되므로 다양 한 계층을 갖게 해야는 단일 클릭 했는지 tooa 선행 재해의 hello 이벤트에서 솔루션을 샷 RTO를 낮추면 합니다.

이 문서에서는 Hyper-V 및 VMware vSphere 플랫폼에서 온-프레미스 Citrix XenApp 배포용 재해 복구 솔루션을 구축하기 위한 단계별 지침을 제공합니다. 이 문서에 대해서도 설명 방법을 tooperform 테스트 장애 조치 (재해 복구 훈련과) 및 복구 계획, 지원 되는 hello 구성 및 필수 구성 요소를 사용 하 여 계획 되지 않은 장애 조치 tooAzure 합니다.


## <a name="prerequisites"></a>필수 조건

시작 하기 전에 hello 다음 알고 있어야 합니다.

1. [가상 컴퓨터 tooAzure 복제](site-recovery-vmware-to-azure.md)
1. 어떻게 너무[복구 네트워크 디자인](site-recovery-network-design.md)
1. [테스트 장애 조치 tooAzure 수행](site-recovery-test-failover-to-azure.md)
1. [장애 조치 tooAzure 수행](site-recovery-failover.md)
1. 어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)
1. 어떻게 너무[SQL Server 복제](site-recovery-sql.md)

## <a name="deployment-patterns"></a>배포 패턴

Citrix XenApp 및 XenDesktop 팜에는 일반적으로 배포 패턴 hello에 있습니다.

**배포 패턴**

AD DNS 서버, SQL Database 서버, Citrix Delivery Controller, StoreFront 서버, XenApp Master(VDA), Citrix XenApp License Server 등을 사용하여 Citrix XenApp 및 XenDesktop 배포

![배포 패턴 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Site Recovery 지원

이 문서의 hello 목적으로 vSphere 6.0에서 관리 하는 VMware 가상 컴퓨터에 배포 하는 Citrix/System Center VMM 2012 r 2에 사용 되는 toosetup DR 되었습니다.

### <a name="source-and-target"></a>원본 및 대상

**시나리오** | **tooa 보조 사이트** | **tooAzure**
--- | --- | ---
**Hyper-V** | 이 문서에서 다루지 않는 내용 | 예
**VMware** | 이 문서에서 다루지 않는 내용 | 예
**물리적 서버** | 이 문서에서 다루지 않는 내용 | 예

### <a name="versions"></a>버전
고객은 Hyper-V 또는 VMware에서 실행되는 가상 컴퓨터 또는 물리적 서버로 XenApp 구성 요소를 배포할 수 있습니다. Azure Site Recovery에는 모두 실제 및 가상 배포 tooAzure 보호할 수 있습니다.
XenApp 7.7 또는 그 이후 버전에서는 Azure에서 지원 마이그레이션 또는 재해 복구에 대 한 tooAzure 위에 구성 된 이러한 버전 배포에 실패할 수 있습니다.

### <a name="things-tookeep-in-mind"></a>유의 사항 tookeep

1. 보호 및 복구 온-프레미스의 서버 운영 체제 컴퓨터 toodeliver를 사용 하 여 XenApp 게시 된 앱 및 XenApp 데스크톱 게시 배포가 지원 됩니다.

2. 데스크톱 운영 체제 컴퓨터 toodeliver VDI 데스크톱을 사용 하 여 클라이언트 가상 데스크톱, Windows 10 등의 온-프레미스 배포의 보호 및 복구는 지원 되지 않습니다. 즉, ASR와 OS'es 데스크톱 컴퓨터의 hello 복구를 지원 하지 않습니다.  또한 일부 클라이언트 가상 데스크톱 종류(예: Windows 7)는 Azure에서 아직 라이선스가 지원되지 않습니다. Azure의 클라이언트/서버 데스크톱용 라이선스에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/licensing-faq/).

3.  Azure Site Recovery는 기존 온-프레미스 MCS 또는 PVS 클론을 복제 및 보호할 수 없습니다.
Azure RM 배달 컨트롤러에서 프로 비전을 사용 하 여 이러한 복제본 toorecreate가 필요 합니다.

4. NetScaler는 FreeBSD를 기반으로 하며 Azure Site Recovery는 FreeBSD OS 보호를 지원하지 않으므로 Azure Site Recovery를 사용하여 보호할 수 없습니다. Toodeploy 해야 하는 장애 조치 tooAzure 후 Azure Market place에서 새로운 NetScaler 어플라이언스를 구성 합니다.


## <a name="replicating-virtual-machines"></a>가상 컴퓨터 복제

다음과 같은 hello Citrix XenApp 배포의 구성 요소가 hello 보호 toobe tooenable 복제 및 복구에 필요 합니다.

* AD DNS 서버 보호
* SQL Database 서버 보호
* Citrix Delivery Controller 보호
* StoreFront 서버 보호
* XenApp Master(VDA) 보호
* Citrix XenApp License Server 보호


**AD DNS 서버 복제**

너무를 참조 하십시오[Active Directory를 보호 및 Azure 사이트 복구와 DNS](site-recovery-active-directory.md) 에 복제 하 고 Azure에서 도메인 컨트롤러를 구성 하기 위한 지침입니다.

**SQL Database 서버 복제**

너무를 참조 하십시오[SQL Server를 SQL Server 재해 복구 및 Azure Site Recovery로 보호](site-recovery-sql.md) hello에 대 한 자세한 기술 지침에 대 한 SQL server 보호 옵션을 권장 합니다.

에 따라 [이 지침은](site-recovery-vmware-to-azure.md) 다른 구성 요소 가상 컴퓨터 tooAzure hello toostart 복제 합니다.

![XenApp 구성 요소 보호](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**계산 및 네트워크 설정**

Hello 컴퓨터가 보호 한 후 (복제 된 항목에서 "보호 됨"으로 상태 표시) hello 계산 및 네트워크 설정을 구성 하는 toobe 필요 합니다.
에 계산 및 네트워크 > 계산 속성을 hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다.
Azure 요구 사항에 hello 이름 toocomply 해야 할 경우 수정 합니다. 보고 하 고 hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 정보를 추가할 수도 있습니다.

참고 hello 다음.

* Hello 대상 IP 주소를 설정할 수 있습니다. 주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다. 장애 조치에 사용할 수 없는 주소를 설정 하는 경우에 hello 장애 조치 작동 하지 않습니다. hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.

* Hello AD/DNS 서버에 대 한 hello 그대로 유지 하 고 온-프레미스 hello Azure 가상 네트워크에 대 한 hello DNS 서버로 hello 동일한 주소를 지정할 수는 주소 있습니다.

네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.

*   Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
*   Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.
* 예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.
*   Hello 가상 컴퓨터에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.
*   Hello 가상 컴퓨터 네트워크 어댑터가 여러 개 있으면 hello hello 목록에 표시 된 첫 번째가 됩니다 hello Azure 가상 컴퓨터의에서 hello 기본 네트워크 어댑터.


## <a name="creating-a-recovery-plan"></a>복구 계획 만들기

복제 구성 요소 Vm XenApp hello에 대 한 사용 하는 hello 다음 단계는 toocreate 복구 계획입니다.
복구 계획은 장애 조치 및 복구에 대한 요구 사항이 유사한 가상 컴퓨터를 그룹화합니다.  

**단계 toocreate 복구 계획**

1. 복구 계획 hello에 hello XenApp 구성 요소 가상 컴퓨터를 추가 합니다.
2. 복구 계획 -> + 복구 계획을 클릭합니다. Hello 복구 계획에 대 한 알기 쉬운 이름을 제공 합니다.
3. VMware 가상 컴퓨터의 경우 원본 및 대상을 각각 VMware 프로세스 서버와 Microsoft Azure로 선택하고 배포 모델을 Resource Manager로 선택한 후 항목 선택을 클릭합니다.
4. Hyper-v 가상 컴퓨터용: VMM 서버와 원본 선택, Microsoft Azure 및 배포 모델 리소스 관리자를 대상으로 하 고 선택 항목에 클릭 한 다음 hello XenApp 배포 Vm를 선택 합니다.

### <a name="adding-virtual-machines-toofailover-groups"></a>가상 컴퓨터 toofailover 그룹 추가

복구 계획에는 특정 시작 순서, 스크립트 또는 수동 작업에 대 한 사용자 지정 된 tooadd 장애 조치 그룹 될 수 있습니다. 다음 그룹 hello toobe 추가 toohello 복구 계획이 필요 합니다.

1. 장애 조치 그룹 1: AD DNS
2. 장애 조치 그룹 2: SQL Server VM
2. 장애 조치 그룹 3: VDA 마스터 이미지 VM
3. 장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM


### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello 복구 계획 스크립트 추가

복구 계획의 특정 그룹 이전 또는 이후에 스크립트를 실행할 수 있습니다. 또한 수동 작업을 포함하고 장애 조치 중에 수행할 수 있습니다.

사용자 지정 된 복구 계획 hello hello 아래와 같습니다.

1. 장애 조치 그룹 1: AD DNS
2. 장애 조치 그룹 2: SQL Server VM
3. 장애 조치 그룹 3: VDA 마스터 이미지 VM

   >[!NOTE]     
   >4, 6 및 7 수동 또는 스크립트 동작을 포함 하는 단계는 적용 가능한 tooonly 온-프레미스 XenApp > MCS/PVS 카탈로그와 함께 환경입니다.

4. 그룹 3 수동 또는 스크립트 동작: 종료 마스터 VDA VM hello 마스터 VDA VM 장애 조치 tooAzure 실행 중인 상태가 됩니다. toocreate MCS 카탈로그 새 Azure ARM 호스팅 사용 하 여, hello 마스터 VDA VM이 중지 됨 (할당 된 de)에 필요한 toobe 상태입니다. Azure 포털에서 VM hello를 종료 합니다.

5. 장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM
6. 그룹 3 수동 또는 스크립트 작업 1:

    ***Azure RM 호스트 연결 추가***

    Azure에서 새 MCS 카탈로그 배달 컨트롤러 컴퓨터 tooprovision에 Azure ARM 호스트 연결을 만듭니다. 이 항목에 설명 된 대로 hello 단계에 따라 [문서](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)합니다.

7. 그룹 3 수동 또는 스크립트 작업 2:

    ***Azure에서 MCS 카탈로그 다시 만들기***

    MCS 또는 PVS 클론 hello 기본 사이트에서 기존 hello tooAzure 복제 되지 않습니다. Toorecreate hello를 사용 하 여 이러한 복제본 마스터 VDA 및 프로 비전 하는 Azure ARM을 배달 컨트롤러에서 복제 해야 합니다. 이 항목에 설명 된 대로 hello 단계에 따라 [문서](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) Azure에서 MCS toocreate 카탈로그입니다.

![XenApp 구성 요소에 대한 복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >스크립트에서 사용할 수 있습니다 [위치](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) hello의 Ip를 새 장애 조치 hello로 tooupdate hello DNS > 가상 컴퓨터 또는 tooattach hello에 부하 분산 장치 가상 컴퓨터는 경우 장애 조치 필요 합니다.


## <a name="doing-a-test-failover"></a>테스트 장애 조치 수행

에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.

![복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>장애 조치 수행

장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.

## <a name="next-steps"></a>다음 단계

이 백서에서 XenApp 및 XenDesktop 배포를 복제하는 방법에 대해 [자세히](https://aka.ms/citrix-xenapp-xendesktop-with-asr) 알아볼 수 있습니다. 너무 hello 지침을 살펴보고[다른 응용 프로그램 복제](site-recovery-workload.md) Site Recovery를 사용 하 여 합니다.
