---
title: "Azure Site Recovery와 aaaEnable Hyper-v 복제 tooa 보조 사이트 | Microsoft Docs"
description: "어떻게 tooa 복제 Hyper-v Vm에 대 한 복제 tooenable 보조 System Center VMM 인 사이트를 Azure Site Recovery에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>9 단계: Hyper-v Vm에 대 한 복제 tooa 보조 사이트를 사용 하도록 설정


복제 정책을 설정한 후이 사이트를 사용할 문서 tooenable 복제 tooa 보조 System Center Virtual Machine Manager (VMM) 온-프레미스 Hyper-v 가상 컴퓨터 (VM)를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



## <a name="select-vms-tooreplicate"></a>Vm tooreplicate 선택

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다. 

    ![복제 활성화](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. **소스**hello VMM 서버를 선택 하 고 hello 클라우드는 hello tooreplicate 추가할 Hyper-v 호스트 위치 됩니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. **대상**, hello 보조 VMM 서버와 클라우드를 확인 합니다.
4. **가상 컴퓨터**, tooprotect hello 목록에서 원하는 hello Vm을 선택 합니다.

    ![가상 컴퓨터 보호 사용](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Hello의 진행률을 추적할 수 있습니다 **보호 사용** 동작에서 **작업** > **사이트 복구 작업이**합니다. Hello 후 **보호 완료** 작업을 완료 하 고 hello 초기 복제가 완료 되 면 hello 가상 컴퓨터가 장애 조치에 대해 준비 되었는지 합니다.

다음 사항에 유의하세요.

- Hello VMM 콘솔에서 가상 컴퓨터에 대 한 보호를 사용할 수 있습니다. 클릭 **보호 사용** hello 가상 컴퓨터 속성에서 hello 도구 모음 > **Azure Site Recovery** 탭 합니다.
- 복제를 사용 하도록 설정한 후에 VM hello에 대 한 속성을 볼 수 있습니다에 **복제 항목**합니다. Hello에 **Essentials** 대시보드를 hello VM 및 서버 인스턴스의 상태에 대 한 hello 복제 정책에 대 한 정보를 볼 수 있습니다. 자세한 내용을 보려면 **속성** 을 클릭합니다.

## <a name="onboard-existing-vms"></a>기존 VM 온보딩

Hyper-V 복제본을 사용하여 복제 중인 기존 가상 컴퓨터가 VMM에 있는 경우 Azure Site Recovery 복제를 위해 다음과 같이 등록할 수 있습니다.

1. Hello 기존 VM을 호스트 하는 hello Hyper-v 서버 hello 기본 클라우드에 위치한 hello 복제본 가상 컴퓨터를 호스팅하는 hello Hyper-v 서버 hello 보조 클라우드에 있는지 확인 하십시오.
2. 기본 VMM 클라우드 hello에 대 한 복제 정책이 구성 되어 있는지 확인 합니다.
3. Hello 주 가상 컴퓨터에 대 한 복제를 사용 하도록 설정 합니다. Azure 사이트 복구 및 VMM hello 동일한 복제본 호스트 및 가상 컴퓨터가 감지 되는지, 및 Azure 사이트 복구를 다시 사용 hello를 사용 하 여 다시 시작 복제 설정을 지정을 확인 합니다.


## <a name="next-steps"></a>다음 단계

너무 이동[10 단계: 테스트 장애 조치 실행](vmm-to-vmm-walkthrough-test-failover.md)합니다.
