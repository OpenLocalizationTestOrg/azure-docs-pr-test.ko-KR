---
title: "Hyper-v 복제 tooAzure에 대 한 System Center VMM aaaPrepare | Microsoft Docs"
description: "설명 방법에 대 한 Azure Site Recovery를 사용 하 여 Hyper-v 복제 tooAzure, tooprepare System Center VMM 서버"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Hyper-v 복제 tooAzure에 대 한 VMM 서버 및 Hyper-v 호스트를 준비 하는 6 단계:

설정한 후 [Azure 구성 요소](vmm-to-azure-walkthrough-prepare-azure.md) hello 배포에 대 한 Azure Site Recovery와이 문서 tooprepare 온-프레미스 VMM 서버 및 Hyper-v 호스트 toointeract hello 지침을 사용 합니다.

이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="prepare-vmm-servers"></a>VMM 서버 준비

- 사이트 복구 복제 (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)에 대 한 hello 지원 요구 사항이 충족 하는 VMM 서버를 하나 이상 해야 합니다.
- 있는지 확인에 대 한 hello VMM 서버를 준비 했으므로 [네트워크 매핑을](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)합니다.
- 해당 hello VMM 서버는 이러한 Url을 액세스할 수 있는지 확인

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.
- Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.
- West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.

사이트 복구를 배포 하는 동안 hello Site Recovery Provider를 다운로드 및 각 VMM 서버에 설치 합니다. VMM 서버 hello hello 복구 서비스 자격 증명 모음에 등록 됩니다.




## <a name="next-steps"></a>다음 단계

너무 이동[7 단계: 자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md)

