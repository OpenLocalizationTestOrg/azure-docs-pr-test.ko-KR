---
title: "Azure Site Recovery를 사용하여 VMware VM을 Azure에 복제하기 위한 복제 정책 설정 | Microsoft Docs"
description: "VMware VM을 Azure Storage에 복제할 때 복제 정책을 설정하는 데 필요한 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 3c4b7ad16e6a03fb605447def18f7475d502fdd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-to-azure"></a>9단계: VMware VM을 Azure에 복제하기 위한 복제 정책 설정


이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 VMware VM을 Azure에 복제할 때 복제 정책을 설정하는 방법을 설명합니다.


이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.


## <a name="configure-a-policy"></a>정책 구성

시작하기 전에 간단한 동영상 개요를 보세요.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. 새 복제 정책을 만들려면 **Site Recovery 인프라** > **복제 정책** > **+복제 정책**을 클릭합니다.
2. **복제 정책 만들기**에서 정책 이름을 지정합니다.
3. **RPO 임계값**에서 RPO 제한을 지정합니다. 이 값은 데이터 복구 지점 생성 횟수를 지정합니다. 연속 복제가 이 제한을 초과하면 경고가 생성됩니다.
4. **복구 지점 보존**에서 각 복구 지점에 대해 지속될 보존 시간을 시간 단위로 지정합니다. 복제된 VM은 하나의 시간대에서 임의의 시점으로 복구할 수 있습니다. 프리미엄 저장소에 복제된 컴퓨터의 경우 최대 24시간 보존이 지원되고 표준 저장소에 복제된 경우 72시간 보존이 지원됩니다.
5. **응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다. **확인** 을 클릭하여 정책을 만듭니다.

    ![복제 정책](./media/vmware-walkthrough-replication/gs-replication2.png)
8. 새 정책을 만들면 새 정책이 자동으로 구성 서버에 연결됩니다. 기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다. 예를 들어 복제 정책이 **rep-policy**인 경우 장애 복구(failback) 정책은 **rep-policy-failback**이 됩니다. 이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.

## <a name="next-steps"></a>다음 단계

[10단계: 모바일 서비스 설치](vmware-walkthrough-install-mobility.md)로 이동합니다.
