---
title: "Azure 사이트 복구와 Hyper-v VM 복제 tooa 보조 사이트에 대 한 네트워크 aaaMap | Microsoft Docs"
description: "Azure 사이트 복구와 Hyper-v Vm tooa 보조 VMM 사이트를 복제할 때 toomap 네트워크 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a>7 단계: Hyper-v VM 복제 tooa 보조 사이트에 대 한 네트워크를 매핑


설정한 후 [원본 및 대상 설정을](vmm-to-vmm-walkthrough-source-target.md) Hyper-v 가상 컴퓨터 (Vm) tooa 보조 System Center Virtual Machine Manager (VMM) 사이트를 복제에 대 한 가상 Hyper-v에 대 한이 문서 tooconfigure 네트워크 매핑을 사용 컴퓨터 (VM) 복제 tooa 보조 사이트를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="before-you-start"></a>시작하기 전에

- 시작하기 전에 [네트워크 매핑](vmm-to-vmm-walkthrough-network.md#network-mapping-overview)에 대해 알아봅니다.
- VMM 서버에 가상 컴퓨터가 연결 된 tooa VM 네트워크에 있는지 확인 합니다.

## <a name="configure-network-mapping"></a>네트워크 매핑 구성

1. **네트워크 매핑** > **네트워크 매핑**에서 **+네트워크 매핑**을 클릭합니다.
2. **네트워크 매핑을 추가** 탭 hello 소스를 선택 하 고 대상 VMM 서버입니다. hello VMM 서버와 연결 된 hello VM 네트워크가 검색 됩니다.
3. **원본 네트워크**선택, toouse hello 기본 VMM 서버와 연결 된 VM 네트워크의 hello 목록에서 원하는 hello 네트워크입니다.
4. **대상 네트워크**선택, toouse hello 보조 VMM 서버에서 원하는 hello 네트워크입니다. 그런 후 **OK**를 클릭합니다.

    ![네트워크 매핑](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

네트워크 매핑이 시작되면 다음과 같은 동작이 발생합니다.

* Toohello 원본 VM 네트워크에 해당 하는 모든 기존 복제본 가상 컴퓨터에 연결 된 toohello 대상 VM 네트워크 수 있습니다.
* 연결 된 toohello 원본 VM 네트워크는 새 가상 컴퓨터 복제 후 연결 된 toohello 대상 매핑된 네트워크 됩니다.
* 새 네트워크로 기존 매핑을 수정 하는 경우 hello 새 설정을 사용 하 여 복제본 가상 컴퓨터가 연결 됩니다.
* Hello 대상 네트워크에 서브넷이 여러 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제 가상 컴퓨터 장애 조치 후에 대상 서브넷 연결된 toothat 됩니다. 이름이 일치 하는 대상 서브넷 이면 hello 가상 컴퓨터 연결된 toohello hello 네트워크의 첫 번째 서브넷 됩니다.



## <a name="next-steps"></a>다음 단계

너무 이동[8 단계: 복제 정책 구성](vmm-to-vmm-walkthrough-replication.md)합니다.
