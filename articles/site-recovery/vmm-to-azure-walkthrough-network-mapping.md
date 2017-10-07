---
title: "VMM에서 Hyper-v Vm을 복제 하기 위한 네트워크 매핑 aaaConfigure 클라우드의 Azure Site Recovery와 tooAzure | Microsoft Docs"
description: "Tooconfigure 네트워크 매핑을 VMM에서 Hyper-v Vm을 복제 하는 경우 클라우드를 Azure Site Recovery와 tooAzure 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a>9 단계: Hyper-v (VMM)와 복제 tooAzure에 대 한 네트워크 매핑 구성

Hello를 설정한 후 [원본 및 대상 복제 설정을](vmm-to-azure-walkthrough-source-target.md), 온-프레미스 VMM VM 네트워크와 Azure 네트워크 간에이 문서 tooconfigure 네트워크 매핑 toomap를 사용 합니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="before-you-start"></a>시작하기 전에

- [네트워크 매핑](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)에 대해 알아봅니다.
- [네트워크 매핑용 VMM을 준비합니다](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping). 
- 있는지 hello VMM 서버의 가상 컴퓨터에 연결 된 tooa VM 네트워크와 Azure 가상 네트워크를 하나 이상 만든를 확인 합니다. 여러 VM 네트워크에 매핑된 tooa 단일 Azure 네트워크 수 있습니다.

## <a name="configure-mapping"></a>매핑 구성

다음과 같이 매핑을 구성합니다.

1. **사이트 복구 인프라** > **네트워크 매핑을** > **네트워크 매핑을**, hello 클릭 **+ 네트워크 매핑**  아이콘입니다.

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. **네트워크 매핑을 추가**선택, hello 원본 VMM 서버 및 **Azure** hello 대상으로 합니다.
3. 장애 조치 후 구독 hello 및 hello 배포 모델을 확인 합니다.
4. **원본 네트워크**선택, toomap hello VMM 서버와 관련 된 hello 목록에서 원하는 hello 원본 온-프레미스 VM 네트워크입니다.
5. **대상 네트워크**, 어떤 복제본에서 Azure Vm 배치 될 만들 때 Azure 네트워크를 hello 선택 합니다. 그런 후 **OK**를 클릭합니다.

    ![네트워크 매핑](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

네트워크 매핑이 시작되면 다음과 같은 동작이 발생합니다.

* Hello 원본 VM 네트워크에서 기존 Vm은 연결 된 toohello 대상 네트워크 매핑을 시작 될 때입니다. 새 Vm 연결 된 toohello 원본 VM 네트워크에 연결 되어 복제가 실행 되 면 toohello 매핑된 Azure 네트워크입니다.
* 기존 네트워크 매핑을 수정 하는 경우 복제본 가상 컴퓨터는 hello 새 설정을 사용 하 여 연결 합니다.
* Hello 대상 네트워크에 여러 서브넷이 hello에 이러한 서브넷 중 하나는 hello 원본 가상 컴퓨터는 서브넷 이름이 같은 있는 경우 hello 복제본 가상 컴퓨터가 장애 조치 후 toothat 대상 서브넷 연결 합니다.
* 이름이 일치 하는 대상 서브넷 이면 hello 네트워크의 첫 번째 서브넷 toohello hello 가상 컴퓨터에 연결 합니다.



## <a name="next-steps"></a>다음 단계

너무 이동[10 단계: 복제 정책 만들기](vmm-to-azure-walkthrough-replication.md)
