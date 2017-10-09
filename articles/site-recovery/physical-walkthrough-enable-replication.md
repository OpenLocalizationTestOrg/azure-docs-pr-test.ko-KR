---
title: "Azure Site Recovery와 tooAzure를 복제 하는 물리적 서버에 대 한 복제 aaaEnable | Microsoft Docs"
description: "Tooenable 복제 tooAzure에 필요한 실제 서버 hello Azure Site Recovery 서비스를 사용 하 여 hello 단계가 요약 되어 있습니다."
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>10 단계: 실제 서버 tooAzure에 대 한 복제를 사용 하도록 설정


이 문서에서는 방법에 대 한 복제 tooenable 온-프레미스 Windows/Linux를 설명 hello를 사용 하 여, 물리적 서버 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 서비스 합니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="before-you-start"></a>시작하기 전에

- 서버 hello 있어야 [모바일 서비스 구성 요소가 설치](physical-walkthrough-install-mobility.md)합니다.
- 강제 설치에 대 한 VM 준비 된 경우 복제를 사용 하도록 설정 하면 프로세스 서버 hello가 자동으로 hello 모바일 서비스를 설치 합니다.
- Azure 사용자 계정에 필요한 특정 복제에 대 한 컴퓨터를 사용 하도록 설정 하면 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure 수 toouse Azure 저장소와는 Azure Vm을 만듭니다.
- 를 추가 하거나 서버에 대 한 IP 주소를 수정할 때이 지나야 too15 분 또는 더 이상 하 고 변경 tootake 효과 대 한 hello 포털에서 tooappear 합니다.


## <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. 디스크를 복제에서 제외할 수 있습니다. 예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다. [자세히 알아보기](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>서버 복제

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다.
2. **소스**선택, hello 구성 서버입니다.
3. **컴퓨터 형식**에서 **물리적 컴퓨터**를 선택합니다.
4. Hello 프로세스 서버를 선택 합니다. 모든 추가 프로세스 서버를 만들지 않은 경우 구성 서버 hello 됩니다. 그런 후 **OK**를 클릭합니다.
5. **대상**리소스 그룹을 장애 조치 Vm toocreate hello 원하는 hello을 hello 구독을 선택 합니다. 장애 조치 Vm hello에 대 한 (기본 또는 리소스 관리), Azure에서 toouse 원하는 hello 배포 모델을 선택 합니다.
6. 데이터 복제를 위한 toouse 원하는 hello Azure 저장소 계정을 선택 합니다. Toouse를 이미 설정한 계정을 사용 하지 않으려는 경우 새를 만들 수 있습니다.
7. 선택 hello **Azure 네트워크** 및 **서브넷** 장애 조치 후 toowhich Azure Vm에 연결 합니다. 선택 **선택한 컴퓨터에 지금 구성** tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다. 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다. Toouse 기존 네트워크를 사용 하지 않으려는 경우 하나를 만들 수 있습니다.

    ![복제 활성화](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. **물리적 컴퓨터**, 클릭 **+ 물리적 컴퓨터** hello 입력 **이름** 및 **IP 주소**합니다. Hello 운영 체제를 선택 하려는 tooreplicate hello 컴퓨터의 합니다. 컴퓨터 검색 되 고 hello 목록에 표시 될 때까지 몇 분 걸립니다.
9. **속성** > **속성 구성**을 선택 하는 hello 프로세스 서버 tooautomatically 사용한 hello 계정 hello 머신에서 hello 모바일 서비스를 설치 합니다.
10. 기본적으로 모든 디스크가 복제됩니다. 클릭 **모든 디스크** tooreplicate 원하는 디스크의 선택을 취소 합니다. 그런 후 **OK**를 클릭합니다. 나중에 추가 VM 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. **복제 설정을** > **복제 설정을 구성**, 복제 정책을 선택 되어 올바른 해당 hello를 확인 합니다. 정책을 수정 하면 변경 사항이 적용 된 tooreplicating 시스템과 toonew 컴퓨터 됩니다.
12. 사용 하도록 설정 **다중 VM 일관성** toogather 컴퓨터를 복제 그룹으로 사용할 hello 그룹의 이름을 지정 하는 경우. 그런 후 **OK**를 클릭합니다. 다음 사항에 유의하세요.

    * 복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.
    * 워크로드를 미러링하도록 물리적 서버를 함께 수집하는 것이 좋습니다. 작업 성능에 영향을 줄 수 다중 VM 일관성이 사용 하도록 설정 하 고 컴퓨터가 hello를 실행 하는 경우에 사용 해야 동일한 작업 및 일관성에 필요 합니다.

13. **복제 사용**을 클릭합니다. Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **설정** > **작업** > **사이트 복구 작업이**. Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.

## <a name="next-steps"></a>다음 단계

너무 이동[11 단계: 테스트 장애 조치 실행](physical-walkthrough-test-failover.md)
