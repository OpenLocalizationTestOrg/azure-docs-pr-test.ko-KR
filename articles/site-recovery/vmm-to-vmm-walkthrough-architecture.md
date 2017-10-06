---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 사이트에 대 한 aaaReview hello 아키텍처 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery와 온-프레미스 Hyper-v Vm tooa 보조 System Center VMM 사이트 복제에 대 한 hello 아키텍처의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>1 단계: Hyper-v 복제 tooa 보조 사이트에 대 한 hello 아키텍처를 검토 합니다.

이 문서에서는 hello 구성 요소를 설명 및 복제 하는 경우 관련 된 프로세스 온-프레미스 tooa 보조 VMM 사이트 hello를 사용 하 여 System Center Virtual Machine Manager (VMM) 클라우드에서 Hyper-v 가상 컴퓨터 (Vm) [Azure Site Recovery](site-recovery-overview.md)hello Azure 포털의에서 서비스입니다.

Hello 또는이 문서의 hello 맨 아래에 모든 메모를 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



## <a name="architectural-components"></a>아키텍처 구성 요소

Hyper-v Vm tooa 보조 VMM 사이트 복제에 필요한 것 같습니다.

**구성 요소** | **위치** | **세부 정보**
--- | --- | ---
**Azure** | Azure의 구독. | Tooorchestrate hello Azure 구독에서에서 복구 서비스 자격 증명 모음을 만들고 VMM 위치 간에 복제를 관리 합니다.
**VMM 서버** | VMM 기본 및 보조 위치가 필요합니다. | Hello 기본 사이트에서 VMM 서버에 한 hello 보조 사이트는 것이 좋습니다. 
**Hyper-V 서버** |  하나 이상의 Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 있습니다. | Hello LAN 또는 VPN, Kerberos 또는 인증서 인증을 사용 하 여 hello 기본 및 보조 Hyper-v 호스트 서버 간에 데이터가 복제 됩니다.  
**Hyper-V VM** | Hyper-V 호스트 서버에 있습니다. | 원본 호스트 서버 hello tooreplicate 원하는 VM을 하나 이상 있어야 합니다.

## <a name="replication-process"></a>복제 프로세스

1. Hello Azure 계정 설정 하 고 복구 서비스 자격 증명 모음 만들기 수행할 지정 tooreplicate 합니다.
2. 설정을 구성 하면 hello 소스 및 대상 복제를 들어 VMM 서버 및 각 Hyper-v 호스트에서 Microsoft Azure 복구 서비스 에이전트 hello에 hello Azure Site Recovery Provider를 설치 합니다.
3. VMM 클라우드 hello 원본에 대 한 복제 정책을 만듭니다. hello 정책이 적용 된 tooall hello 클라우드의 호스트에 있는 Vm입니다.
4. 각 VMM에 대 한 복제를 사용 하도록 설정 하 고 선택한 hello 설정에 따라 VM의 초기 복제가 실행 합니다.
5. 초기 복제 후 델타 변경 내용의 복제가 시작됩니다. .hrl 파일에는 항목에 대한 추적된 변경 내용이 유지됩니다.


![온-프레미스 tooon 온-프레미스](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>장애 조치 및 장애 복구 프로세스

1. 온-프레미스 사이트 간에 계획된 또는 계획되지 않은 [장애 조치](site-recovery-failover.md)를 실행할 수 있습니다. 경우 계획된 된 장애 조치를 실행 한 후 원본 Vm이 tooensure 종료 데이터가 손실 되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md) tooorchestrate 여러 컴퓨터를 장애 조치 합니다.
4. Hello 보조 위치에서 장애 조치 컴퓨터 hello 후 계획 되지 않은 장애 조치 tooa 보조 사이트를 수행 하는 경우에 사용 되지 않도록 보호 또는 복제용으로 설정 합니다. Hello 장애 조치 후 계획된 된 장애 조치를 실행 한 경우 hello 보조 위치에서 컴퓨터 보호 됩니다.
5. 그런 다음 hello 장애 조치 toostart 액세스 hello 작업을 hello 복제본 VM에서에서 커밋합니다.
6. 기본 사이트를 사용할 수 있는 다시 역방향 복제 tooreplicate hello 보조 사이트 toohello 기본에서 시작 합니다. 역방향 복제 보호 된 상태로 가상 컴퓨터 hello 가져오지만 hello 보조 데이터 센터는 여전히 hello 활성 위치 합니다.
7. hello toomake hello 활성 위치에 기본 사이트를 다시 시작할 있습니다 보조 tooprimary, 다른 역방향 복제 뒤에서 계획된 된 장애 조치 합니다.



## <a name="next-steps"></a>다음 단계

너무 이동[2 단계: hello 필수 구성 요소 및 제한 사항 검토](vmm-to-vmm-walkthrough-prerequisites.md)합니다.
