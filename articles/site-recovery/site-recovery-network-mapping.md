---
title: "사이트 복구와 Hyper-v VM 복제에 대 한 네트워크 매핑 aaaPlan | Microsoft Docs"
description: "온-프레미스 데이터 센터 tooAzure 또는 tooa 보조 사이트에서 Hyper-v 가상 컴퓨터 복제에 대 한 네트워크 매핑을 설정 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Site Recovery를 사용하여 Hyper-V VM 복제를 위한 네트워크 매핑 계획



이 문서에서는 Hyper-v Vm tooAzure 또는 tooa 보조 사이트의 복제 하는 동안 매핑, hello를 사용 하 여 네트워크에 대 한 계획과 toounderstand [Azure Site Recovery 서비스](site-recovery-overview.md)합니다.

읽은 후이 문서 hello 아래쪽이 문서에 대 한 설명을 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="network-mapping-for-replication-tooazure"></a>복제 tooAzure에 대 한 네트워크 매핑

네트워크 매핑은 (VMM에서 관리 됨) Hyper-v Vm tooAzure 복제할 때 사용 됩니다. 네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 Azure 네트워크 사이를 매핑합니다. 매핑 다음 hello지 않습니다.

- **네트워크 연결**-복제 된 Azure Vm으로 연결 된 toohello 매핑된 네트워크 유지 합니다. 장애 조치 hello에 동일 하는 모든 컴퓨터에서 서로 다른 복구 계획 장애 조치 될 경우에 네트워크 tooeach 기타, 연결할 수 있습니다.
- **네트워크 게이트웨이**-hello 대상 Azure 네트워크에 네트워크 게이트웨이가 설치 되 면 하는 경우 Vm tooother 온-프레미스 가상 컴퓨터에 연결할 수 있습니다.

다음 사항에 유의하세요.

- 소스를 VMM VM 네트워크 tooan Azure 가상 네트워크를 매핑합니다.
- Hello에 Azure Vm 장애 조치 후 원본 네트워크에 연결 된 toohello 매핑된 대상 가상 네트워크가 됩니다.
- 새 Vm toohello 원본 VM 네트워크에 연결 된 추가 복제가 실행 되 면 toohello 매핑된 Azure 네트워크입니다.
- Hello 대상 네트워크에 여러 서브넷이 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제본 가상 컴퓨터가 장애 조치 후 toothat 대상 서브넷 연결 합니다.
- 이름이 일치 하는 대상 서브넷 이면 hello 네트워크의 첫 번째 서브넷 toohello hello 가상 컴퓨터에 연결 합니다.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>복제 tooa 보조 데이터 센터에 대 한 네트워크 매핑

네트워크 매핑은 (System Center Virtual Machine Manager (VMM)에서 관리 됨) Hyper-v Vm tooa 보조 데이터 센터를 복제할 때 사용 됩니다. 네트워크 매핑은 원본 VMM 서버의 VM 네트워크와 대상 VMM 서버의 VM 네트워크 사이를 매핑합니다. 매핑 다음 hello지 않습니다.

- **네트워크 연결**-장애 조치 후 Vm 연결 tooappropriate 네트워크입니다. hello 복제본 VM에 연결 된 toohello 대상 네트워크 매핑된 toohello 원본 네트워크를 됩니다.
- **최적의 배치**-최적으로 위치 hello Hyper-v 호스트 서버에 복제본 Vm입니다. 복제본 Vm 수 액세스 hello 매핑되는지 VM 네트워크 호스트에 배치 됩니다.
- **네트워크 매핑이 없는**-네트워크 매핑을 구성 하지 않는 경우 복제본 Vm 장애 조치 후 tooany 연결 된 VM 네트워크에 되지 않습니다.

다음 사항에 유의하세요.

- 네트워크 매핑은 두 명의 VMM 서버의 VM 네트워크 간 구성할 수 있습니다 또는 단일 VMM 서버에서 두 사이트에서 관리 하는 경우 환영 동일 서버.
- 매핑이 올바르게 구성 되 고 복제가 설정 되어 hello 기본 위치의 VM에 연결 된 tooa 네트워크 됩니다와 hello 대상 위치의 복제본 연결 될 네트워크 tooits에 매핑됩니다.
-
- 네트워크가 올바르게 설정 되었는지, VMM에서 네트워크 매핑 중 대상 VM 네트워크를 선택 하면, hello 원본 VM 네트워크를 사용 하는 hello VMM 원본 클라우드가 표시 됩니다, hello에 사용 되는 hello 대상 클라우드가 사용 가능한 대상 VM 네트워크와 함께 보호 합니다.
- Hello 대상 네트워크에 여러 서브넷과 이러한 서브넷 중 하나가 이름이 같은 hello는 hello에서 원본 가상 컴퓨터가 위치한 서브넷,으로 다음 hello hello 복제 가상 컴퓨터에 장애 조치 후 연결 된 toothat 대상 서브넷이 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.



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



## <a name="next-steps"></a>다음 단계

에 대 한 자세한 내용은 [hello 네트워크 인프라 계획](site-recovery-network-design.md)합니다.
