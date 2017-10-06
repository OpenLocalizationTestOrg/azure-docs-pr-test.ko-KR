---
title: "Azure Site Recovery를 사용 하 여 (System Center VMM)을 사용한 Hyper-v tooAzure 복제에 대 한 aaaReview hello 필수 구성 요소 | Microsoft Docs"
description: "복제, 장애 조치 및 Azure Site Recovery와 VMM 클라우드에 tooAzure의 온-프레미스 Hyper-v Vm의 복구를 설정 하기 위한 사전 요구 사항을 hello 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>2 단계: Hyper-v (VMM)과 tooAzure 복제에 대 한 hello 필수 구성 요소를 검토 합니다.

검토 하 고 나 서 hello [시나리오 아키텍처](vmm-to-azure-walkthrough-architecture.md)를 읽고이 문서 toomake hello 배포 필수 구성 요소를 이해 해야 합니다. 

## <a name="prerequisites-and-limitations"></a>필수 구성 요소 및 제한 사항

**요구 사항** | **세부 정보**
--- | ---
**Azure 계정** | [Microsoft Azure 계정](http://azure.microsoft.com/)이 있어야 합니다.
**Azure 저장소** | Azure 저장소 계정 복제 toostore 데이터가 있어야합니다.<br/><br/> hello 저장소 계정은 hello에 있어야 hello와 같은 지역의 Azure 복구 서비스 자격 증명 모음입니다.<br/><br/>[지역 중복 저장소](../storage/common/storage-redundancy.md#geo-redundant-storage) 또는 로컬 중복 저장소를 사용할 수 있습니다. 지역 중복 저장소를 사용하는 것이 좋습니다. 지리적 중복 저장소와 데이터는 복원 력 있는 지역 가동 중단 발생 하는 경우 또는 기본 지역의 hello를 복구할 수 없는 경우입니다.<br/><br/> 표준 Azure Storage 계정을 사용하거나 Azure [Premium Storage](../storage/common/storage-premium-storage.md)를 사용할 수 있습니다. Premium Storage는 I/O를 많이 사용하는 워크로드를 호스트할 수 있으며 일관된 I/O 고성능과 짧은 대기 시간이 요구되는 VM에 일반적으로 사용됩니다. 복제된 데이터에 대해 프리미엄 저장소를 사용하는 경우 표준 저장소 계정도 필요합니다. 표준 저장소 계정이 가져갈 변화 들이 tooon 온-프레미스 데이터를 캡처하는 복제 로그를 저장 합니다.
**Azure 네트워크** | 필요한는 [Azure 네트워크](../virtual-network/virtual-network-get-started-vnet-subnet.md), 장애 조치 후 toowhich Azure Vm에 연결 합니다. hello Azure 네트워크에에서 있어야 hello hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
**온-프레미스 VMM 서버** | System Center 2012 R2 이상에서 실행되는 하나 이상의 VMM 서버가 필요합니다.<br/><br/> 각 VMM 서버에 하나 이상의 사설 클라우드가 포함되어 있어야 합니다. 각 클라우드에 하나 이상의 호스트 그룹이 필요합니다.<br/><br/> hello VMM 서버는 인터넷 액세스가 필요합니다.
**온-프레미스 Hyper-V** | Hyper-v 호스트 서버가 이상 실행 해야 hello Hyper-v 역할이 활성화 되어, 또는 Microsoft Hyper-v Server 2012 r 2와 Windows Server 2012 r 2입니다. hello 최신 업데이트를 설치 해야 합니다.<br/><br/> hello Hyper-v 호스트 (VMM 클라우드에 있는) VMM 호스트 그룹에 있어야 합니다.<br/><br/> 호스트는 tooreplicated 지정 하는 Vm을 하나 이상 있어야 합니다.<br/><br/> Hyper-v 호스트에 연결 된 toohello 여야 합니다. 복제 tooAzure, 직접 또는 프록시와 인터넷 합니다. Hyper-v 서버에는 문서에서 설명 하는 hello 수정 있어야 합니다. [2961977](https://support.microsoft.com/kb/2961977)합니다.
**온-프레미스 Hyper-V VM** | Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다. 복제를 설정한 후에 hello VM 이름을 수정할 수 있습니다. 




## <a name="next-steps"></a>다음 단계

너무 이동[3 단계: 용량 계획](vmm-to-azure-walkthrough-capacity.md)
