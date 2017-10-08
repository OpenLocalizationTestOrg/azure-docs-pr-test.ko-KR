---
title: "Azure Site Recovery를 사용 하 여 (System Center VMM) 없이 Hyper-v tooAzure 복제에 대 한 aaaReview hello 필수 구성 요소 | Microsoft Docs"
description: "복제, 장애 조치 및 Azure 사이트 복구와 온-프레미스 Hyper-v Vm tooAzure의 복구를 설정 하기 위한 사전 요구 사항을 hello 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>2 단계: Hyper-v (VMM 없음) tooAzure 복제에 대 한 hello 필수 구성 요소를 검토 합니다.

hello 필수 구성 요소는 hello 표에 요약 되어 있습니다.


**필수 요소** | **세부 정보** 
--- | --- 
**Azure** | [Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.
**온-프레미스 서버** | [자세한 내용은](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) hello 온-프레미스 Hyper-v 호스트에 대 한 요구 사항에 대 한 합니다.
**온-프레미스 Hyper-V VM** | Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
**Azure URL** | Hyper-v 호스트 toothese Url에 액세스할 필요:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.<br/></br> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.<br/></br> West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.



## <a name="next-steps"></a>다음 단계

- 전체 배포를 수행 하는 경우 너무 이동[3 단계: 용량 계획](hyper-v-site-walkthrough-capacity.md)
- 간단한 테스트 배포를 수행 하는 경우 너무 이동[4 단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)합니다.
