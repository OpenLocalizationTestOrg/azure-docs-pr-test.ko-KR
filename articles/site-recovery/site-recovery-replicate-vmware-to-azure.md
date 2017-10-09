---
title: "복제 응용 프로그램 (VMware tooAzure) | Microsoft Docs"
description: "이 문서에서는 가상의 복제를 tooset 실행 컴퓨터 하는 방법을 설명 Azure에 VMware에 있습니다."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>VMware Vm tooAzure에서 실행 중인 응용 프로그램 복제



이 문서에서는 가상의 복제를 tooset 실행 컴퓨터 하는 방법을 설명 Azure에 VMware에 있습니다.
## <a name="prerequisites"></a>필수 조건

hello 문서 이미 있다고 가정 합니다.

1.  [온-프레미스 원본 환경 설정](site-recovery-set-up-vmware-to-azure.md)
2.  [Azure에서 대상 환경 설정](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>복제 활성화
#### <a name="before-you-start"></a>시작하기 전에
VMware 가상 컴퓨터를 복제하는 경우 다음 사항에 유의하세요.

* Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.
* VMware VM은 15분마다 검색됩니다. 15 분 걸릴 수 있습니다 하 이상 tooappear 검색 후 hello 포털에서입니다. 마찬가지로 vCenter Server 또는 vSphere 호스트를 추가할 때 검색이 15분 이상 걸릴 수 있습니다.
* (예: VMware 도구 설치) hello 가상 컴퓨터에서 환경 변화는 15 분 또는 hello 포털에서 업데이트 하는 자세한 toobe 걸릴 수 있습니다.
* Hello 마지막으로 검색 한 시간 VMware Vm에 대 한 hello에서 확인할 수 있습니다 **마지막 연락처에** hello vCenter 서버/vSphere 호스트 hello에 대 한 필드 **구성 서버** 블레이드입니다.
* hello 예약 된 검색에 대 한 대기 하지 않고 복제에 대 한 tooadd 컴퓨터 hello 구성 서버를 강조 표시 (클릭 하지 말고), hello를 클릭 하 고 **새로 고침** 단추입니다.
* Hello 컴퓨터를 준비 하는 경우 복제를 사용 하면 hello 프로세스 서버 hello 모바일 서비스에 자동으로 설치 합니다.


**이제 다음과 같이 복제를 활성화합니다.**

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다. 처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 자격 증명 모음 tooenable 복제 hello에에서 있습니다.
2. Hello에 **소스** 블레이드 > **소스**선택, hello 구성 서버입니다.
3. **컴퓨터 형식**에서 **가상 컴퓨터** 또는 **물리적 컴퓨터**를 선택합니다.
4. **vCenter/vSphere 하이퍼바이저**를 hello vSphere 호스트를 관리 하는 hello vCenter 서버를 선택 하거나 hello 호스트를 선택 합니다. 이 설정은 물리적 컴퓨터를 복제하는 경우에는 관련이 없습니다.
5. Hello 프로세스 서버를 선택 합니다. 모든 추가 프로세스 서버를 만들지 않은 경우이 hello 구성 서버 hello 이름이 됩니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. **대상** hello 구독 및 가상 컴퓨터를 조치할 toocreate hello 저장할 hello 리소스 그룹을 선택 합니다. Toouse (기본 또는 리소스 관리) Azure에서 가상 컴퓨터를 조치할 hello에 대 한 원하는 hello 배포 모델을 선택 합니다.
7. 데이터 복제를 위한 toouse 원하는 hello Azure 저장소 계정을 선택 합니다. 다음 사항에 유의하세요.

   * 프리미엄 또는 표준 저장소 계정을 선택할 수 있습니다. 프리미엄 계정을 선택 하는 경우 진행 중인 복제 로그에 대 한 추가 표준 저장소 계정을 toospecify를 해야 합니다. 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
   * 원하는 toouse 해야 하는 것 보다 다른 저장소 계정 하나를 만들 수 있습니다*자습서에서 설명한는 관리자가 리소스를 사용 하 여 저장소 계정을 만들기 위한 자리 표시자 링크*합니다. 리소스 관리자를 사용 하 여 저장소 계정을 toocreate 클릭 **새로 만들기**합니다. 수행 하려는 경우 toocreate hello 일반 모델을 사용 하 여 저장소 계정, [hello Azure 포털에서에서](../storage/common/storage-create-storage-account.md)합니다.

8. 장애 조치 후 생성 하는 경우 선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm이 연결 됩니다. hello에에서 있어야 hello hello와 동일한 지역 복구 서비스 자격 증명 모음입니다. 선택 **선택한 컴퓨터에 지금 구성**, tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다. 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다. 네트워크를 설정 하지 않은 경우 너무[만드세요](#set-up-an-azure-network)합니다. 리소스 관리자를 사용 하는 네트워크 toocreate 클릭 **새로 만들기**합니다. Hello 일반 모델을 사용 하는 네트워크 toocreate을 원하는 경우 [hello Azure 포털에서에서](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다. 해당하는 경우 서브넷을 선택합니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. **가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다. 복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. **속성** > **속성 구성**을 선택 하는 hello 프로세스 서버 tooautomatically 사용한 hello 계정 hello 머신에서 hello 모바일 서비스를 설치 합니다.  
11. 기본적으로 모든 디스크가 복제됩니다. 복제에서 디스크를 tooexclude 클릭 **모든 디스크** tooreplicate 원하는 디스크의 선택을 취소 합니다.  그런 후 **OK**를 클릭합니다. 나중에 추가 속성을 설정할 수 있습니다. 디스크 제외에 대해 [자세히 알아보세요](site-recovery-exclude-disk.md).

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. **복제 설정을** > **복제 설정을 구성**, 복제 정책을 선택 되어 올바른 해당 hello를 확인 합니다. **설정** > **복제 정책** > 정책 이름 > **설정 편집**에서 복제 정책을 수정할 수 있습니다. Tooa 정책을 적용 하는 변경 내용이 적용 된 tooreplicating 및 새 컴퓨터 됩니다.
13. 사용 하도록 설정 **다중 VM 일관성** toogather 컴퓨터를 복제 그룹으로 사용할 hello 그룹의 이름을 지정 하는 경우. 그런 후 **OK**를 클릭합니다. 다음 사항에 유의하세요.

    * 복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.
    * 워크로드를 미러링하도록 VM 및 물리적 서버를 함께 수집하는 것이 좋습니다. 워크 로드 성능에 영향을 줄 수 다중 VM 일관성이 사용 하도록 설정 하 고 컴퓨터가 hello를 실행 하는 경우에 사용 해야 동일한 작업 및 일관성에 필요 합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. **복제 사용**을 클릭합니다. Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **설정** > **작업** > **사이트 복구 작업이**. Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.

> [!NOTE]
> 밀어넣기 설치 hello 모바일 서비스 구성 요소는 설치에 대 한 hello 컴퓨터를 준비 하는 경우 보호가 사용 됩니다. Hello 후 보호 작업을 시작 하는 hello 컴퓨터 정책 또는 실패에 구성 요소가 설치 되어 있습니다. 필요한 toomanually hello 실패 후 각 컴퓨터를 다시 시작 합니다. Hello hello 보호를 다시 시작 후 작업 다시 시작 하 고 초기 복제가 발생 합니다.
>
>

## <a name="view-and-manage-vm-properties"></a>VM 속성 보기 및 관리

Hello 원본 컴퓨터의 hello 속성을 확인 하는 것이 좋습니다. 해당 hello Azure VM 이름을 준수 해야 기억 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.

1. 클릭 **설정** > **복제 항목** >, 및 select hello 컴퓨터입니다. hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.
2. **속성**및 복제를 볼 수 있습니다에 대 한 장애 조치 정보 hello VM입니다.
3. **계산 및 네트워크** > **속성 계산**, hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다. Azure 요구 사항에 hello 이름 toocomply 해야 할 경우 수정 합니다.
    ![복제 활성화](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  컴퓨터가 사후 장애 조치(failover)에 속할 [리소스 그룹](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines)을 선택할 수 있습니다. 장애 조치(failover) 전에 언제든지 이 설정을 변경할 수 있습니다. 컴퓨터의 보호 설정을 끊긴다는 다음 hello 컴퓨터 tooa 다른 리소스 그룹을 마이그레이션하는 경우 post 장애 조치 합니다.
5. 선택할 수는 [가용성 집합](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) 컴퓨터 필요한 toobe 하나의 게시의 일부가 될 경우 장애 조치 합니다. 가용성 집합을 선택할 때는 다음에 유의하세요.

    * 리소스 그룹 가용성 집합 지정 속하는 toohello만 나열 됩니다.  
    * 다른 가상 네트워크를 사용하는 컴퓨터는 동일한 가용성 집합에 속할 수 없습니다.
    * 동일한 크기의 가상 컴퓨터만 같은 가용성 집합의 일부가 될 수 있습니다.
5. 보고 하 고 hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 정보를 추가할 수도 있습니다.
6. **디스크**, hello 운영 체제를 확인할 수 있습니다 및 데이터 디스크에 hello VM에 복제 됩니다.

### <a name="network-adapters-and-ip-addressing"></a>네트워크 어댑터 및 IP 주소 지정 

- Hello 대상 IP 주소를 설정할 수 있습니다. 주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다. 장애 조치에 사용할 수 없는 주소를 설정 하는 경우에 hello 장애 조치 작동 하지 않습니다. hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.
- 네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.
    - Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
    - Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.
    - 예를 들어 원본 컴퓨터에 네트워크 어댑터가 두 개 및 4 hello 대상 컴퓨터 크기 지원로 hello 대상 컴퓨터는 두 개의 어댑터를 포함 합니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.
    - Hello 가상 컴퓨터에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.
    - Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.
   



## <a name="common-issues"></a>일반적인 문제

* 각 디스크의 크기는 1TB 미만이어야 합니다.
* 기본 디스크 및 동적 아님 디스크 hello OS 디스크 여야 합니다.
* 가상 컴퓨터를 사용 하는 세대 2/UEFI에 대 한 hello 운영 체제 제품군은 Windows를 이어야 하며 부팅 디스크 300GB 미만 이어야 합니다.

## <a name="next-steps"></a>다음 단계

시도할 수 hello 보호 완료 되 면 [장애 조치](site-recovery-failover.md) toocheck 여부 응용 프로그램 Azure에서 또는 제공 하지 않습니다.

Toodisable 보호 하려는 경우를 어떻게 너무 확인[등록 및 보호 설정 정리](site-recovery-manage-registration-and-protection.md)
