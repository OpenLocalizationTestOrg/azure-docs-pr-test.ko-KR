---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 aaaReview hello 필수 구성 요소 | Microsoft Docs"
description: "Hyper-v Vm tooa 보조 VMM 사이트 간 Azure Site Recovery를 복제 하기 위한 hello 필수 구성 요소에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>2 단계: hello 필수 구성 요소 및 Hyper-v VM 복제 tooa 보조 VMM 사이트에 대 한 제한 사항 검토


Hello를 검토 한 후 [시나리오 아키텍처](vmm-to-vmm-walkthrough-architecture.md), System Center 가상에서 관리 되는 온-프레미스 Hyper-v 가상 컴퓨터 (Vm)를 복제할 때 hello 배포 필수 구성 요소를 이해 해야이 문서 toomake 읽기 Machine Manager (VMM) tooa 보조 클라우드를 사용 하 여 사이트 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="prerequisites-and-limitations"></a>필수 구성 요소 및 제한 사항

**요구 사항** | **세부 정보**
--- | ---
**Azure** | [Microsoft Azure](http://azure.microsoft.com/) 구독<br/><br/> [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.<br/><br/> Site Recovery 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/).<br/><br/> 사이트 복구를 아래에서 지역 가용성을 위한 지원 hello 영역 확인 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
**VMM 서버** | 두 명의 VMM 서버, hello 기본 사이트와 보조 hello에 각각 하나씩 있는 것이 좋습니다.<br/><br/> 단일 VMM 서버의 클라우드 간 복제가 지원됩니다.<br/><br/> VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.<br/><br/> VMM 서버는 인터넷에 연결되어야 합니다.
**VMM 클라우드** | 각 VMM 서버에서 하나 이상의 클라우드가 있어야 하 고 모든 클라우드 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다. <br/><br/>클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.<br/><br/> 하나의 VMM 서버를만 있는 경우 둘 이상의 클라우드가, tooact를 주 및 보조 필요 합니다.
**Hyper-V** | Hyper-v 서버가 이상 실행 해야 hello Hyper-v 역할을 통해 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.<br/><br/> Hyper-V 서버에 VM이 하나 이상 있어야 합니다.<br/><br/>  Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 들어 있어야 합니다.<br/><br/> Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치합니다.<br/><br/> Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Hello 클러스터 브로커를 수동으로 구성 합니다. [자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Hyper-V 서버는 인터넷에 연결되어야 합니다.




## <a name="next-steps"></a>다음 단계

너무 이동[3 단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)합니다.
