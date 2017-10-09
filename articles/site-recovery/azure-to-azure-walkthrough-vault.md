---
title: "Azure Site Recovery와 지역 간 repliction Azure VM에 대 한 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 Azure 지역 간 복제의 Azure 자격 증명 모음을 tooset 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>4 단계: Azure tooAzure 복제에 대 한 자격 증명 모음 설정

후 [네트워크 계획](azure-to-azure-walkthrough-network.md), 복제 tooanother Azure 지역 hello를 사용 하 여 Azure 가상 컴퓨터 (Vm)는 자격 증명 모음을이 문서 tooset를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

- Hello 문서를 완료 하면 복구 서비스 자격 증명 모음 설정 있어야 합니다.
- 이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



>[!NOTE]
>
> Azure VM 복제는 현재 미리 보기로 제공됩니다.




## <a name="create-a-vault"></a>자격 증명 모음 만들기

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Vm tooreplicate 저장할 hello 위치에서 hello 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다. 예를 들어 대상 위치는 hello 중앙 미국, 만들에서 자격 증명 모음의 hello **중미**합니다.


## <a name="next-steps"></a>다음 단계

너무 이동[5 단계: 복제 사용](azure-to-azure-walkthrough-enable-replication.md)
