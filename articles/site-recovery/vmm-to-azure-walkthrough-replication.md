---
title: "Azure Site Recovery와 복제 tooAzure Hyper-v VM (VMM)에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "설명 방법 (VMM)과 Hyper-v VM 복제 tooAzure Azure 사이트 복구에 대 한 복제 정책을 tooset"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>10 단계: Hyper-v VM (VMM)와 복제 tooAzure에 대 한 복제 정책 설정


설정한 후 [네트워크 매핑을](vmm-to-azure-walkthrough-network-mapping.md),이 문서 tooconfigure 복제 정책 T\tooreplicate 온-프레미스 클라우드 tooAzure System Center Virtual Machine Manager (VMM)에서 관리 되는 Hyper-v 가상 컴퓨터를 사용 하 여, hello를사용하여[ Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



## <a name="create-a-policy"></a>정책 만들기

1. 새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.

    ![네트워크](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. **만들기 및 연결 정책**에서 정책 이름을 지정합니다.
3. **복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.

    > [!NOTE]
    >  두 번째 30 주파수 toopremium 저장소를 복제할 때 지원 되지 않습니다. hello 제한 프리미엄 저장소에서 지 원하는 (100) blob 당 스냅숏 hello 수로 결정 됩니다. [자세히 알아보기](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. **복구 지점 보존**, 지정 시간에 시간 hello 보존 기간이 각 복구 지점에 대 한 수입니다. 보호 된 컴퓨터 수 있는 창 내에서 tooany 포인트를 복구 합니다.
5. **응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1-12시간)를 지정합니다. Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다. 응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다. 응용 프로그램 일치 스냅숏을 사용할 경우 영향을 주므로 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능을 확인 합니다. 설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.
6. **초기 복제 시작 시간**때 toostart hello 초기 복제를 나타냅니다. hello 복제 하므로 tooschedule 해도 인터넷 대역폭을 통해 발생 사용 중인 시간 외 것입니다.
7. **Azure에 저장 된 데이터를 암호화**를 지정 하는지 여부를 tooencrypt Azure 저장소에 나머지 데이터에 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 정책](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. 새 정책을 만들 때 hello v m M 클라우드로 자동으로 연결 되어 있습니다. **확인**을 클릭합니다. 이 복제 정책에 추가 VMM 클라우드에 (및 그 안의 hello Vm) 연결할 수 있습니다 **복제** > 정책 이름 > **VMM 클라우드에 연결**합니다.

    ![복제 정책](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>다음 단계

너무 이동[11 단계: 복제 사용](vmm-to-azure-walkthrough-enable-replication.md)
