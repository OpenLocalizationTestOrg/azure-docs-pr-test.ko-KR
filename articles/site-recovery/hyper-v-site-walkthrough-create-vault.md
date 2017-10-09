---
title: "Azure Site Recovery를 사용 하 여 Hyper-v 복제 (System Center VMM) 없이 tooAzure에 대 한 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 Hyper-v 복제 tooAzure tooset는 자격 증명 모음을 사용 해야 하는 hello 단계가 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>7단계: Hyper-V 복제를 위한 자격 증명 모음 설정

어떻게 tooset는 자격 증명 모음 및 대상 지정이 문서에서는 설명 tooAzure hello를 사용 하 여 온-프레미스 위치의 tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.


Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>보호 목표 선택

대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.

1. **Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.
2. Hello 리소스 메뉴, 클릭 **사이트 복구** > **인프라 준비** > **보호 목표**합니다.
3. **보호 목표**선택, **tooAzure** > **Hyper-v와 함께 예,**합니다. 선택 **아니요** tooconfirm VMM을 사용 하지 않는다고 합니다. 

    ![목표 선택](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>다음 단계

너무 이동[8 단계: 원본 및 대상 설정](hyper-v-site-walkthrough-source-target.md)
