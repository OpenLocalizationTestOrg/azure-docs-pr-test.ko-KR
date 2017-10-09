---
title: Hyper-v Vm tooAzure aaaReplicate | Microsoft Docs
description: "설명 방법을 tooorchestrate 복제, 장애 조치 및 복구의 온-프레미스 하이퍼-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a>Hyper-v 가상 컴퓨터 (VMM 없음) tooAzure Azure Site Recovery를 사용 하 여 Azure 포털 hello로 복제

> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-hyper-v-site-to-azure.md)
> * [Azure 클래식](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

이 문서에서는 어떻게 tooreplicate 온-프레미스 Hyper-v 가상 컴퓨터 tooAzure 설명를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서. 이 배포에서는 Hyper-V VM이 System Center VMM(Virtual Machine Manager)을 통해 관리되지 않습니다.

이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

자세한 내용을 보려면 toomigrate 컴퓨터 tooAzure 장애 복구) (제외 하려는 경우 [이 여기서](site-recovery-migrate-to-azure.md)합니다.



## <a name="deployment-steps"></a>배포 단계

Hello 문서 toocomplete 다음 배포 단계를 따릅니다.

1. [자세한 내용은](site-recovery-components.md#hyper-v-to-azure) 이 배포에 대 한 hello 아키텍처에 대 한 합니다. 또한 Site Recovery에서 Hyper-V 복제가 작동하는 방식을 [알아봅니다](site-recovery-hyper-v-azure-architecture.md).
2. 필수 조건 및 제한 사항을 확인합니다.
3. Azure 네트워크 및 저장소 계정을 설정합니다.
4. Hyper-V 호스트를 준비합니다.
5. Recovery Services 자격 증명 모음을 만듭니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.
6. 원본 설정을 지정합니다. Hello Hyper-v 호스트를 포함 하는 Hyper-v 사이트를 만들고 hello 사이트 hello 자격 증명 모음에 등록 합니다. Hello Hyper-v 호스트에 hello Azure Site Recovery Provider 및 hello Microsoft 복구 서비스 에이전트를 설치 합니다.
7. 대상 및 복제 설정을 지정합니다.
8. Hello Vm에 대 한 복제를 사용 하도록 설정 합니다.
9. 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.



## <a name="prerequisites"></a>필수 조건


**요구 사항** | **세부 정보** |
--- | --- |
**Azure** | [Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.
**온-프레미스 서버** | [자세한 내용은](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) hello 온-프레미스 Hyper-v 호스트에 대 한 요구 사항에 대 한 합니다.
**온-프레미스 Hyper-V VM** | Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
**Azure URL** | Hyper-v 호스트 toothese Url에 액세스할 필요:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.<br/></br> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.<br/></br> West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.



## <a name="prepare-for-deployment"></a>배포 준비

tooprepare 배포 해야 합니다.

1. [Azure 네트워크를 설정](#set-up-an-azure-network) 합니다.
2. [Azure 저장소 계정을 설정](#set-up-an-azure-storage-account) 합니다.
3. [Hello Hyper-v 호스트를 준비](#prepare-the-hyper-v-hosts) tooensure hello 액세스할 수 있는 Url 필요 합니다.

### <a name="set-up-an-azure-network"></a>Azure 네트워크를 설정

Azure 네트워크 설정 Hello Azure Vm은 연결 된 tooa 네트워크 장애 조치 후 만들어지도록이 필요 합니다.

* hello 네트워크 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
* Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한, hello Azure 네트워크에서 설정한 [Resource Manager 모드](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), 또는 [클래식 모드](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.
* 시작하기 전에 네트워크를 설정하는 것이 좋습니다. Toodo 필요 하지 않으면 사이트 복구 배포 시이 있습니다.
- Site Recovery에 의해 사용 되는 저장소 계정 수 없습니다 [이동](../azure-resource-manager/resource-group-move-resources.md) hello 동일 하지만, 또는 간에, 서로 다른 구독 내에서.


### <a name="set-up-an-azure-storage-account"></a>Azure 저장소 계정을 설정

- 표준/프리미엄 Azure 저장소 계정 toohold 데이터 tooAzure 복제 해야 합니다. [프리미엄 저장소](../storage/storage-premium-storage.md) 계속 높게 IO 성능과 짧은 대기 시간 toohost IO가 많은 작업을 필요로 하는 가상 컴퓨터에 대해 일반적으로 사용 됩니다.
- Toouse 프리미엄 계정 toostore 복제 된 데이터를 캡처 지속적인 tooon 온-프레미스 데이터를 변경 표준 저장소 계정을 toostore 복제 로그를 제공 해야 합니다.
- Hello 리소스 모델에 따라 원하는 toouse 장애 조치 Azure Vm에 대 한에서 계정을 설정한 [Resource Manager 모드](../storage/storage-create-storage-account.md), 또는 [클래식 모드](../storage/storage-create-storage-account-classic-portal.md)합니다.
- 시작하기 전에 저장소 계정을 설정하는 것이 좋습니다. 그렇지 않으면 toodo 해야 사이트 복구 배포 시이 있습니다. hello 계정은 hello에 있어야 hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.
- 저장소 계정에서 사용 되는 사이트 복구 hello 내의 리소스 그룹 동일 이동할 수 없습니다, 구독 또는 다른 구독에서.


### <a name="prepare-hello-hyper-v-hosts"></a>Hello Hyper-v 호스트를 준비 합니다.

* Hello Hyper-v 호스트 hello를 충족 하는지 확인 [필수 구성 요소](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)합니다.
- Hello 호스트 필요한 hello Url에 액세스할 수 있는지 확인 합니다.


## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기** > **모니터링 + 관리** > **Backup 및 Site Recovery(OMS)**를 클릭합니다.  

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. **이름**, 이름 tooidentify hello 자격 증명 모음을 지정 합니다. 구독이 두 개 이상인 경우 그 중에서 하나를 선택합니다.

4. [새 리소스 그룹을 만들거나](../azure-resource-manager/resource-group-template-deploy-portal.md) 기존 리소스 그룹을 선택하고 Azure 지역을 지정합니다. 컴퓨터는 복제 된 toothis 영역 됩니다. 지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.

5. Tooquickly 액세스 hello 자격 증명 모음 대시보드 hello에서 클릭 **Pin toodashboard**, 클릭 하 고 **만들기**합니다.

    ![새 자격 증명 모음](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

hello에 hello 새 자격 증명 모음 표시 **대시보드** > **모든 리소스** 목록으로 이동한에 주 hello **복구 서비스 자격 증명 모음** 블레이드입니다.



## <a name="select-hello-protection-goal"></a>Hello 보호 목표를 선택 합니다.

대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.

1. Hello에 **복구 서비스 자격 증명 모음**선택, hello 자격 증명 모음입니다.
2. **시작**에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 차례로 클릭합니다.

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. **보호 목표**선택, **tooAzure**, 선택 하 고 **Hyper-v와 함께 예,**합니다. 선택 **아니요** tooconfirm VMM을 사용 하지 않는다고 합니다. 그런 후 **OK**를 클릭합니다.

    ![목표 선택](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

Hello 하이퍼-V 사이트를 설정 하 고, Hyper-v 호스트에 hello Azure Site Recovery Provider 및 hello Azure 복구 서비스 에이전트를 설치 하 고 및 hello 사이트 hello 자격 증명 모음에 등록 합니다.

1. **인프라 준비**에서 **원본**을 클릭합니다. 새 Hyper-v 사이트에 Hyper-v 호스트 또는 클러스터에 대 한 컨테이너로 tooadd 클릭 **+ Hyper-v 사이트**합니다.

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. **만들 Hyper-v 사이트**, hello 사이트에 대 한 이름을 지정 합니다. 그런 후 **OK**를 클릭합니다. 이제 작성 하 고 클릭 하 여 hello 사이트를 선택 **+ Hyper-v 서버** tooadd 서버 toohello 사이트입니다.

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. **서버 추가** > **서버 형식**에 **Hyper-V 서버**가 표시되는지 확인합니다.

    - Tooadd hello를 준수 하는 것이 원하는 hello Hyper-v server에 해당 하는지 확인 한 [필수 구성 요소](#on-premises-prerequisites), 및가 수 tooaccess hello 지정 된 Url입니다.
    - Hello Azure Site Recovery Provider 설치 파일을 다운로드 합니다. 이 파일 tooinstall hello 공급자를 실행 하 고 각 Hyper-v 호스트에서 복구 서비스 에이전트 hello 합니다.

    ![원본 설정](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Hello 공급자 및 에이전트 설치

1. Toohello 하이퍼-V 사이트를 추가 각 호스트에서 hello 공급자 설치 파일을 실행 했습니다. Hyper-V 클러스터에 설치하는 경우 각 클러스터 노드에서 설치 프로그램을 실행합니다. 각 Hyper-V 클러스터 노드를 설치하고 등록하면 노드 간 마이그레이션에서도 VM이 안전하게 보호됩니다.
2. Microsoft Update 정책에 따라 공급자 업데이트가 설치되도록 **Microsoft Update**에서 업데이트를 선택할 수 있습니다.
3. **설치**, 수락 하거나 hello 기본 공급자 설치 위치를 수정 하 고 클릭 **설치**합니다.
4. **자격 증명 모음 설정을**, 클릭 **찾아보기** tooselect hello 자격 증명 모음 키 파일을 다운로드 합니다. Hello Azure Site Recovery 구독 hello 자격 증명 모음 이름을 지정 하 고 hello 하이퍼-V 사이트 toowhich hello Hyper-v 서버가 속하는 키를 누릅니다.

    ![서버 등록](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. **프록시 설정을**, Hyper-v 호스트에서 실행 중인 공급자를 통해 tooAzure 사이트 복구를 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.

    * Hello 공급자 tooconnect 직접 선택 하려면 **tooAzure Site Recovery 프록시 없이 직접 연결**합니다.
    * 기존 프록시 인증 필요 hello 공급자 연결에 대 한 사용자 지정 프록시 toouse를 원하는 경우 선택 **연결에서 프록시 서버를 사용 하 여 사이트 복구 tooAzure**합니다.
    * 프록시를 사용하는 경우:
        - Hello 주소, 포트 및 자격 증명을 지정 합니다.
        - Hello에 설명 된 있는지 hello Url 확인 [필수 구성 요소](#prerequisites) hello 프록시를 통해 허용 됩니다.

    ![인터넷](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. 설치를 마친 후 클릭 **등록** tooregister hello 서버 hello 자격 증명 모음에 있습니다.

    ![설치 위치](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. 등록 완료 되 면 hello Hyper-v 서버에서 메타 데이터를 Azure Site Recovery에서 검색 되 고 hello 서버에 표시 되 **사이트 복구 인프라** > **Hyper-v 호스트**합니다.


## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정

복제에 대 한 hello Azure 저장소 계정을 지정 하 고 hello Azure 네트워크 toowhich Azure Vm 장애 조치 후 연결 합니다.

1. **인프라 준비** > **대상**을 클릭합니다.
2. Hello 구독 및 장애 조치 후 toocreate hello Azure Vm 만들려는 hello 리소스 그룹을 선택 합니다. Hello 배포 선택 hello Vm에 대 한 Azure (기본 또는 리소스 관리)에서 toouse 되도록 모델입니다.

3. Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.

    - 저장소 계정에 없으면 클릭 **+ 저장소** toocreate 리소스 관리자 기반 계정 인라인 합니다. [저장소 요구 사항](site-recovery-prereq.md#azure-requirements)을 읽어 보세요.
    - Azure 네트워크를 설정 하지 않은 경우 클릭 **+ 네트워크** toocreate 리소스 관리자 기반 네트워크 인라인 합니다.

    ![저장소](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a>복제 설정 구성

1. 새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.

    ![네트워크](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. **만들기 및 연결 정책**에서 정책 이름을 지정합니다.
3. **복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.

    > [!NOTE]
    > 두 번째 30 주파수 toopremium 저장소를 복제할 때 지원 되지 않습니다. hello 제한 프리미엄 저장소에서 지 원하는 (100) blob 당 스냅숏 hello 수로 결정 됩니다. [자세히 알아봅니다](../storage/storage-premium-storage.md#snapshots-and-copy-blob).

4. **복구 지점 보존**, 시간 길이 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다. Vm 수 tooany 지점 창 내에서 복구 합니다.
5. **앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다.

    - Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다.
    - 응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다.
    - 응용 프로그램 일치 스냅숏을 사용할 경우 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능이 저하 됩니다. 설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.

6. **초기 복제 시작 시간**때 toostart hello 초기 복제를 지정 합니다. hello 복제 하므로 tooschedule 해도 인터넷 대역폭을 통해 발생 사용 중인 시간 외 것입니다. 그런 후 **OK**를 클릭합니다.

    ![복제 정책](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

새 정책을 만들 때 자동으로 hello Hyper-v 사이트와 연결 되어 있습니다. Hyper-v 사이트 (및 그 안에 hello Vm)에서 여러 복제 정책을 연결할 수 있습니다 **복제** > 정책 이름 > **Hyper-v 사이트 연결**합니다.

## <a name="capacity-planning"></a>용량 계획

기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다.

사이트 복구를 사용 하는 용량 플래너 toohelp 계산, 네트워킹 및 저장소에 대 한 hello 오른쪽 리소스를 할당 합니다. 사용자 지정 된 숫자 값을 hello 작업 수준에서 hello 플래너를 Vm, 디스크 및 저장소는 평균 수에 따라 예상에 대 한 빠른 모드에서 detailed 모드에서 실행할 수 있습니다. 시작하기 전에 다음을 수행해야 합니다.

* VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.
* 복제 된 데이터에 대 한 hello 매일 변경 (변동) 속도 예측 합니다. Hello를 사용할 수 있습니다 [Hyper-v 복제본 용량 플래너](https://www.microsoft.com/download/details.aspx?id=39057) toohelp이 작업을 수행 합니다.

1. 클릭 **다운로드** toodownload hello 도구를 한 다음를 실행 합니다. [Hello 문서 읽기](site-recovery-capacity-planner.md) hello 도구와 함께 제공 되는 합니다.
2. 완료 되 면 선택 **예** 에 **hello Capacity Planner를 실행 한**?

   ![용량 계획](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

[네트워크 대역폭 제어](#network-bandwidth-considerations)에 대해 자세히 알아보기



## <a name="enable-replication"></a>복제 활성화

시작 하기 전에 Azure 사용자 계정에 필요한 hello에 있는지 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.

다음과 같이 VM에 대해 복제를 활성화합니다.          

1. **응용 프로그램 복제** > **원본**을 클릭합니다. 처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 tooenable 복제 합니다.

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. **소스**선택, hello 하이퍼-V 사이트입니다. 그런 후 **OK**를 클릭합니다.
3. **대상**hello toouse Azure (기본 또는 리소스 관리)에서 장애 조치 후 원하는 장애 조치 모델을 hello 자격 증명 모음 구독을 선택 합니다.
4. 원하는 toouse hello 저장소 계정을 선택 합니다. Toouse 원하는 계정을 없는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-storage-account)합니다. 그런 후 **OK**를 클릭합니다.
5. 선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm 장애 조치 만들 때 연결 됩니다.

    - tooapply hello 네트워크 설정을 tooall 컴퓨터 사용 하도록 설정 하면 복제를 위해 선택 **선택한 컴퓨터에 지금 구성**합니다.
    - 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다.
    - Toouse 원하는 네트워크를 설정 하지 않은 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-network)합니다. 해당하는 경우 서브넷을 선택합니다. 그런 후 **OK**를 클릭합니다.

   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. **가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다. 복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. **속성** > **속성 구성**OS 디스크 hello을 hello 선택한 Vm에 대 한 hello 운영 체제를 선택 합니다.
8. 해당 hello Azure VM 이름 (대상 이름)을 준수 확인 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
9. 기본적으로 모든 hello 디스크 hello VM의 복제를 위해 선택 하지만 디스크 tooexclude 지울 수 있습니다 이러한.
    - Tooexclude 디스크 tooreduce 복제 대역폭을 할 수 있습니다. 예를 들어 임시 데이터로 tooreplicate 디스크 원하지 않을 수 있습니다 또는 (예: pagefile.sys 또는 Microsoft SQL Server tempdb)가 새로 고쳐질 때마다 컴퓨터나 응용 프로그램 데이터를 다시 시작 합니다. Hello 디스크 선택을 취소 하 여 hello 디스크 복제에서 제외할 수 있습니다.
    - 기본 디스크만 제외할 수 있습니다. OS 디스크는 제외할 수 없습니다.
    - 동적 디스크는 제외하지 않는 것이 좋습니다. Site Recovery는 게스트 VM 내의 가상 하드 디스크가 기본 디스크인지 아니면 동적 디스크인지 식별할 수 없습니다. 모든 종속 동적 볼륨 디스크 제외 되지 않으면 hello VM 장애 조치, 되 고 hello 해당 디스크에 액세스할 수 없게 하는 경우 실패 한 디스크 hello 보호 된 동적 디스크가 표시 됩니다.
        - 복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다. Tooadd 원하는 디스크를 제외 하거나, hello VM toodisable 보호 해야 하 고 다시 설정 합니다.
        - Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다. 예를 들어 세 디스크 실패 하 고 Azure VM에 직접 두 개 만든 경우 Azure tooHyper-V에서 다시 hello 세 디스크만 장애 조치 된 장애 됩니다. 장애 복구 또는 Hyper-v tooAzure에서 역방향 복제를 수동으로 만든 디스크를 포함할 수 없습니다.
        - 응용 프로그램 toooperate에 필요한 디스크를 제외 하면 후 장애 조치 tooAzure 해야 toocreate Azure 때문에 해당 hello 복제 응용 프로그램에서 수동으로 실행할 수 있습니다. 또는 Azure 자동화 hello 컴퓨터의 장애 조치 중 toocreate hello 디스크 복구 계획을 통합할 수 있습니다.

10. 클릭 **확인** toosave 변경 합니다. 나중에 추가 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. **복제 설정을** > **복제 설정을 구성**, hello Vm 보호 된 원하는 tooapply hello 복제 정책을 선택 합니다. 그런 후 **OK**를 클릭합니다. hello 복제 정책을 수정할 수 있습니다 **복제 정책** > 정책 이름 > **설정 편집**합니다. 적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.


   ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **작업** > **사이트 복구 작업이**합니다. Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.

### <a name="view-and-manage-vm-properties"></a>VM 속성 보기 및 관리

Hello 원본 컴퓨터의 hello 속성을 확인 하는 것이 좋습니다.

1. **보호 된 항목**, 클릭 **복제 항목**, 및 select hello 컴퓨터입니다.

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. **속성**및 복제를 볼 수 있습니다에 대 한 장애 조치 정보 hello VM입니다.

    ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. **계산 및 네트워크** > **속성 계산**, hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다. Azure 요구 사항에 hello 이름 toocomply 해야 할 경우 수정 합니다. 또한 보고 및 hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 정보를 수정할 수 있습니다. 참고 hello 다음.

   * Hello 대상 IP 주소를 설정할 수 있습니다. 주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다. 장애 조치에 사용할 수 없는 주소를 설정 하는 경우 hello 장애 조치가 실패 합니다. hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.
   * 네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.

     * Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
     * Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.
     * 예를 들어 원본 컴퓨터에 네트워크 어댑터가 두 개 및 4 hello 대상 컴퓨터 크기 지원로 hello 대상 컴퓨터는 두 개의 어댑터를 포함 합니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.     
     * Hello VM에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.
     * Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.

     ![복제 활성화](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. **디스크**, hello 운영 체제를 확인할 수 있습니다 및 데이터 디스크에 hello VM에 복제 됩니다.

#### <a name="managed-disks"></a>관리 디스크

**계산 및 네트워크** > **속성 계산**, 마이그레이션 tooAzure에서 관리 하는 디스크 tooyour 컴퓨터 tooattach hello VM에 대 한 너무 "Yes" 설정 "디스크 관리 되는 사용"을 설정할 수 있습니다. 관리 되는 디스크 hello VM 디스크와 연결 된 hello 저장소 계정을 관리 하 여 Azure IaaS Vm에 대 한 디스크 관리를 간소화 합니다. [Managed Disks에 대한 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - 관리 되는 디스크는 장애 조치 tooAzure에 대해서만 생성 되 고 연결 된 toohello 가상 컴퓨터입니다. 보호를 사용 하도록 설정 하면, 온-프레미스 컴퓨터의에서 데이터를 tooreplicate toostorage 계정을 계속 됩니다.
   Hello 리소스 관리자 배포 모델을 사용 하 여 배포 된 가상 컴퓨터에 대해서만 관리 하는 디스크를 만들 수 있습니다.

  > [!NOTE]
  > 관리 되는 디스크를 사용 하 여 컴퓨터에 대 한 장애 복구 Azure tooon 온-프레미스 Hyper-v 환경에서 현재 지원 되지 않습니다. "디스크 관리 되는 사용" 너무 "예"로 설정 toomigrate이 컴퓨터 tooAzure를 가져오려는 경우에 합니다.

   - 너무 "Yes" "디스크 관리 되는 사용"을 설정 하는 경우 가용성 집합에만 hello 리소스 그룹의 "디스크 관리 되는 사용" 집합과 너무 "Yes" 것을 선택할 수입니다. 즉, 관리 되는 디스크와 가상 컴퓨터 "디스크 관리를 사용 하 여" 속성이 설정 된 가용성 집합의 일부가 너무 "Yes" 수만 있습니다. "디스크 관리를 사용 하 여" 속성이 설정 된 장애 조치 시 의도 toouse 관리 되는 디스크에 따라 가용성 집합을 만드는 있는지 확인 합니다. 마찬가지로, 설정 하는 경우 "디스크 관리 되는 사용" 너무 "No", "디스크 관리 되는 사용" 속성이 너무 "아니요"를 설정 하는 hello 리소스 그룹에만 가용성 집합은 선택할 수 있는 것입니다. [Managed Disks와 가용성 집합에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Hello 저장소 계정 복제에 사용 되는 시간에 언제 든 지 저장소 서비스 암호화로 암호화 된, 장애 조치 중에 관리 되는 디스크를 만들 실패 합니다. 유지할 수 있습니다 설정 "디스크 관리 되는 사용" 너무 "No" 장애 조치를 다시 시도 또는 hello 가상 컴퓨터에 대 한 보호를 사용 하지 않도록 설정 하 고 저장소 서비스 암호화 시간에서 언제 든 지 사용할 수 없는 tooa 저장소 계정을 보호 합니다.
  > [저장소 서비스를 암호화 및 Managed Disks에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Hello 배포 테스트

tootest hello 배포는 단일 가상 컴퓨터 또는 하나 이상의 가상 컴퓨터를 포함 하는 복구 계획에 대 한 테스트 장애 조치를 실행할 수 있습니다.

### <a name="before-you-start"></a>시작하기 전에

 - Tooconnect tooAzure Vm을 원하는 경우에 대 한 자세한 내용은 RDP를 사용 하 여 장애 조치 후 [tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)합니다.
 - 테스트 환경에서 Active Directory 및 DNS toocopy 필요한 toofully 테스트 합니다. [자세히 알아봅니다](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행

1. 단일 컴퓨터를 통해 toofail에서 **복제 항목**, hello VM을 클릭 > **+ 테스트 장애 조치** 아이콘입니다.
2. 복구를 통해 toofail 계획 **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다. 복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.
3. **테스트 장애 조치**선택, 장애 조치 발생 후 hello Azure 네트워크 toowhich Azure Vm 연결 됩니다.
4. 클릭 **확인** toobegin hello 장애 조치 합니다. Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **작업** > **사이트 복구 작업이**합니다.
5. Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 해야 합니다.
6. 연결에 대 한 장애 조치 후 준비 수 tooconnect toohello Azure VM이 있어야 합니다.
7. 완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. **노트** 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.

자세한 내용은 hello를 읽을 [테스트 장애 조치 tooAzure](site-recovery-test-failover-to-azure.md) 문서.



## <a name="monitor-hello-deployment"></a>모니터 hello 배포

Hello 구성 설정, 상태 및 사이트 복구 배포에 대 한 상태를 모니터링 합니다.

1. Hello 자격 증명 모음 이름 tooaccess hello 클릭 **Essentials** 대시보드 합니다. 이 대시보드에서 Site Recovery 작업, 복제 상태, 복구 계획, 서버 상태 및 이벤트를 추적할 수 있습니다.  

    ![Essentials](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. Hello에 **상태** 타일 hello 지난 24 시간 동안 hello에서 Site Recovery에 의해 발생 한 이벤트 및 문제를 발생 하는 사이트 서버를 모니터링할 수 있습니다. Essentials tooshow hello 타일 및 다른 사이트 복구 및 백업 자격 증명 모음은 hello 상태를 포함 하는 가장 유용한 tooyou 된 레이아웃을 사용자 지정할 수 있습니다.
3. 관리 하 고 hello에 대 한 복제를 모니터링할 수 **복제 항목**, **복구 계획**, 및 **사이트 복구 작업이** 타일입니다. **작업** > **Site Recovery 작업**에서 작업을 자세히 살펴볼 수 있습니다.

## <a name="command-line-provider-and-agent-installation"></a>명령줄 공급자 및 에이전트 설치

hello Azure 사이트 복구 공급자 및 에이전트 설치할 수도 있습니다 hello 다음 명령줄을 사용 하 여 합니다. 이 메서드는 Server Core에 대 한 Windows Server 2012 r 2에서 사용 되는 tooinstall hello 공급자 수 있습니다.

1. Hello 공급자 설치 파일과 등록 키 tooa 폴더를 다운로드 합니다. 예: C:\ASR.
2. 상승된 된 명령 프롬프트에서 이러한 명령을 tooextract hello 공급자 설치 관리자를 실행 합니다.

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. 이 명령은 tooinstall hello 구성 요소를 실행 합니다.

            C:\ASR> setupdr.exe /i
4. 그런 다음 hello 자격 증명 모음에 이러한 명령을 tooregister hello 서버를 실행 합니다.

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
여기서,

* **/ 자격 증명**:는 hello 등록 키 파일의 위치를 가리키는 hello 위치를 지정 하는 필수 매개 변수  
* **/ FriendlyName**: hello Azure Site Recovery 포털에 표시 되는 hello Hyper-v 호스트 서버 hello 이름에 대 한 필수 매개 변수입니다.
* **/proxyAddress**: hello hello 프록시 서버의 주소를 지정 하는 선택적 매개 변수입니다.
* **/proxyport** : hello hello 프록시 서버의 포트를 지정 하는 선택적 매개 변수입니다.
* **/proxyUsername**: (프록시에 인증이 필요) 하는 경우 hello 프록시 사용자 이름을 지정 하는 선택적 매개 변수입니다.
* **/proxyPassword**:를 지정 하는 선택적 매개 변수 (프록시에 인증이 필요) 하는 경우 프록시 서버 hello에 인증 하기 위해 암호를 hello 합니다.


## <a name="network-bandwidth-considerations"></a>네트워크 대역폭 고려 사항
Hello를 사용할 수 있습니다 [Hyper-v 용량 계획 도구](site-recovery-capacity-planner.md) toocalculate hello 대역폭 (초기 복제와 델타) 복제에 필요 합니다. toocontrol hello 양 복제용 대역폭 사용의 몇 가지 옵션을 사용할 수 있습니다.

* **대역폭 제한**: tooAzure를 복제 하는 Hyper-v 트래픽이 특정 Hyper-v 호스트를 통과 합니다. Hello 호스트 서버에서 대역폭을 제한할 수 있습니다.
* **대역폭을 조정**: 몇 가지 레지스트리 키를 사용 하 여 복제에 사용 되는 hello 대역폭에 영향을 줄 수 있습니다.

### <a name="throttle-bandwidth"></a>대역폭 제한
1. Hello Microsoft Azure 백업 MMC 스냅인 hello Hyper-v 호스트 서버에서 엽니다. 기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.
3. Hello에 **제한** 탭 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**, 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다. 유효 범위는 512 Kbps too102 Mbps 초당에서.

    ![대역폭 제한](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다. 다음은 샘플입니다.

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.

### <a name="influence-network-bandwidth"></a>네트워크 대역폭에 영향
1. 너무 hello 레지스트리 이동**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.
   * 복제 디스크에서 tooinfluence hello 대역폭 트래픽을 수정 hello 값 hello **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.
   * hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.
2. hello 기본값은 4입니다. "Overprovisioned" 네트워크에서 이러한 레지스트리 키 hello 기본값에서 변경 되어야 합니다. 최대 hello은 32입니다. 트래픽 toooptimize hello 값을 모니터링 합니다.

## <a name="next-steps"></a>다음 단계

초기 복제가 완료 되 면 hello 배포를 테스트 한 후에 hello 필요할 때 장애 조치를 호출할 수 있습니다. [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 방법과 toorun 해당 합니다.
