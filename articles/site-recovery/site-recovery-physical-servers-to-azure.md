---
title: "물리적 서버 tooAzure aaaReplicate | Microsoft Docs"
description: "어떻게 toodeploy Azure Site Recovery tooorchestrate 복제, 장애 조치 및 복구를 온-프레미스 Windows/Linux 물리적 서버의 tooAzure hello Azure 포털을 사용 하 여 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a>사이트 복구를 사용 하 여 물리적 컴퓨터 tooAzure 복제


이 문서에서는 어떻게 tooreplicate 온-프레미스 물리적 컴퓨터 tooAzure hello Azure 포털의에서 hello Azure Site Recovery 서비스를 사용 하 여 설명 합니다.

원하면 toomigrate 물리적 컴퓨터 tooAzure (장애 조치만), 읽기 [Site Recovery와 tooAzure 마이그레이션할](site-recovery-migrate-to-azure.md) toolearn 더 합니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="prerequisites"></a>필수 조건

**지원 요구 사항** | **세부 정보**
--- | ---
**Azure** | [Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.
**온-프레미스 구성 서버** | Windows Server 2012 R2 이상이 실행되는 온-프레미스 컴퓨터(물리적 또는 VMware VM). 사이트 복구 배포 하는 동안 hello 구성 서버를 설정 합니다.<br/><br/> 기본적으로 hello 프로세스 서버와 마스터 대상 서버도이 컴퓨터에 설치 됩니다. 수직 확장, 별도 프로세스 서버를 할 수 있고 hello 갖고 hello 구성 서버와 동일한 요구 사항이 있습니다.<br/><br/> 이러한 구성 요소에 대 한 자세한 [hello 소스 환경 설정](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)합니다.
**온-프레미스 VM** | 원하는 tooreplicate를 실행 해야 하는 컴퓨터는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
**URL** | 구성 서버 hello toothese Url에 액세스 해야 합니다.<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure 허용 하는지 확인 합니다.<br/></br> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 hello HTTPS (443) 포트입니다.<br/></br> West US (액세스 제어 및 id 관리에 사용) 및 hello 귀하의 구독 한 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.<br/><br/> 이 URL hello MySQL 다운로드에 대 한 허용: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi 합니다.
**모바일 서비스** | 이 서비스는 설치 tooreplicate 하려는 각 컴퓨터에 있습니다.

## <a name="limitations"></a>제한 사항

**제한 사항** | **세부 정보**
--- | ---
**Azure** | 저장소 및 네트워크 계정은 hello에 있어야 hello 자격 증명 모음과 동일한 지역입니다.<br/><br/> 프리미엄 저장소 계정을 사용 하는 경우 또한 해야 표준 계정 toostore 복제 로그를 저장 합니다.<br/><br/> Toopremium 계정 중앙 및 남 인도에 복제할 수 없습니다.
**온-프레미스 구성 서버** | VMware VM에 hello 구성 서버를 설치 하는 경우 VM 어댑터 유형을 hello VMXNET3 이어야 합니다. 그렇지 않은 경우 [이 업데이트를 설치하세요.](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> VMware VM을 사용하는 경우 vSphere PowerCLI 6.0을 설치해야 합니다.<br/><br> hello 컴퓨터는 도메인 컨트롤러일 하지 않아야 합니다.<br/><br/> hello 컴퓨터에 고정 IP 주소를 해야 합니다.<br/><br/> hello 호스트 이름은 15 자 여야 합니다, 운영 체제 hello 영어에 있어야 합니다.
**복제된 컴퓨터** | [Azure VM 제한 사항](site-recovery-prereq.md#azure-requirements)을 확인합니다.<br/><br/> 동일한 작업 toobe 복구 hello를 실행 하는 컴퓨터를 매핑함으로써 tooenable 다중 VM 일관성을 원하는 함께 tooa 일관 된 데이터를 가리키고 20004 hello 컴퓨터에서 포트를 열어야 합니다.<br/><br/> 특정 유형의 [Linux 저장소](site-recovery-support-matrix-to-azure.md#support-for-storage)가 지원됩니다.
**장애 복구** | Azure tooa 물리적 컴퓨터에서 다시 실패할 수 없습니다. Toobe 수 toofail 백 tooon 온-프레미스 장애 조치 후 원하는 백 tooa VMware VM 실패할 수 있도록 VMware 환경이 필요 합니다.


## <a name="set-up-azure"></a>Azure 설정

1. [Azure 네트워크를 설정합니다](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

      a. Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.

      b. Azure [Resource Manager](../resource-manager-deployment-model.md) 또는 클래식 모드에서 네트워크를 설정할 수 있습니다.

2. 복제 데이터를 저장할 [Azure Storage 계정](../storage/storage-create-storage-account.md#create-a-storage-account)을 설정합니다.

    a. hello 계정 표준 수 또는 [프리미엄](../storage/storage-premium-storage.md)합니다.

    b. Resource Manager 또는 클래식 모드에서 계정을 설정할 수 있습니다.

## <a name="prepare-hello-configuration-server"></a>Hello 구성 서버를 준비 합니다.

1. 온-프레미스 물리적 서버 또는 VMware VM에 Windows Server 2012 R2 이상을 설치합니다.

2. Hello 컴퓨터에 나열 된 액세스 toohello Url에 있는지 확인 [필수 구성 요소](#prerequisites)합니다.

## <a name="prepare-for-mobility-service-installation"></a>모바일 서비스 설치 준비

Toopush hello 이동성 서비스 tooa 물리적 컴퓨터를 하려면 hello 프로세스 서버 tooaccess hello 컴퓨터에서 사용할 수 있는 계정이 필요 합니다. hello 계정은 hello 강제 설치에 대해서만 사용 됩니다. 도메인 또는 로컬 계정을 사용할 수 있습니다.

  - Windows 도메인 계정을 사용 하지 않는 경우 필요 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 합니다. toodo 아래 hello 레지스트리에서이 **찾아**, hello DWORD 항목을 추가 **LocalAccountTokenFilterPolicy**, 값이 1 인 합니다. 명령줄 인터페이스에서 Windows 용 tooadd hello 레지스트리 항목을 원하는 경우 다음을 입력 합니다.

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - Linux 용 hello 계정은 hello 원본 Linux 서버에 루트 사용자 이어야 합니다.


## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a>Hello 보호 목표를 선택 합니다.

기능 선택 tooreplicate를 tooreplicate 하려는 위치 및 원하는 합니다.

1. **복구 서비스 자격 증명 모음** > **자격 증명 모음**을 클릭합니다.
2. Hello에 **리소스** 메뉴를 클릭 하 여 **사이트 복구** > **인프라 준비** > **보호 목표**.

    ![목표 선택](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. **보호 목표**선택, **tooAzure** > **하지 가상화 된 / 기타**합니다.


## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

Hello 구성 서버를 설정 하 고 hello 자격 증명 모음에 등록 한 다음 Vm을 검색 합니다.

1. **Site Recovery** > **인프라 준비** > **원본**을 클릭합니다.
2. 구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.

    ![원본 설정](./media/site-recovery-vmware-to-azure/set-source1.png)

3. **서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.
4. Hello 다운로드 **Site Recovery 통합 설치** 설치 파일입니다.
5. Hello 다운로드 **자격 증명 모음 등록 키**합니다. 통합 설치를 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

   ![원본 설정](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Site Recovery 통합 설치 프로그램 실행

시작 하기 전에 다음 hello지 않습니다.

- 간단한 비디오 개요 보기 (비디오 hello tooreplicate VMware Vm 되지만 hello 처리 하는 방법을 설명 물리적 컴퓨터 복제에 대 한 것과 비슷합니다.)

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- Hello 구성 서버 컴퓨터에서 해당 hello 시스템 시계와 동기화 되었는지 확인 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)합니다. 15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.
- Hello 구성 서버 컴퓨터에 로컬 관리자로 설치 프로그램을 실행 합니다.
- Hello 컴퓨터에서 TLS 1.0을 사용할 수 있는지 확인 합니다.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> hello 구성 서버를 설치할 수도 있습니다 [hello 명령줄에서](http://aka.ms/installconfigsrv)합니다.


## <a name="set-up-hello-target-environment"></a>Hello 대상 환경 설정

Hello 대상 환경 설정 하기 전에 확인 했는지 toomake는 [Azure 저장소 계정 및 네트워크](#set-up-azure)합니다.

1. 클릭 **인프라 준비** > **대상**, 선택 hello toouse를 원하는 Azure 구독 및 합니다.
2. 대상 배포 모델이 Resource Manager인지, 클래식인지 지정합니다.
3. 사이트 복구 toomake 호환 되는 Azure 저장소 계정 및 네트워크를 하나 이상 있는지 확인 합니다.

   ![대상](./media/site-recovery-vmware-to-azure/gs-target.png)

4. 저장소 계정 또는 네트워크를 만들지 않은 경우 클릭 **저장소 계정 추가** 또는 **+ 네트워크** toocreate 리소스 관리자 계정 또는 네트워크 인라인 합니다.

## <a name="set-up-replication-settings"></a>복제 설정 지정

시작하기 전에 간단한 비디오 개요 보기 (비디오 hello tooreplicate VMware Vm 되지만 hello 처리 하는 방법을 설명 물리적 컴퓨터 복제에 대 한 것과 비슷합니다.)

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. 새 복제 정책을 toocreate 클릭 **사이트 복구 인프라** > **복제 정책** > **+ 복제 정책**합니다.
2. **복제 정책 만들기**에서 정책 이름을 지정합니다.
3. **RPO 임계값**, hello RPO 제한을 지정 합니다. 이 값은 데이터 복구 지점 생성 횟수를 지정합니다. 연속 복제가 이 제한을 초과하면 경고가 생성됩니다.
4. **복구 지점 보존**, 기간 (시간)에 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다. 복제 된 Vm 수 tooany 지점 창에서 복구 합니다. Too24를 시간 보존 컴퓨터 toopremium 복제 된 저장소에 지원 됩니다. Too72를 시간 보존 컴퓨터 toostandard 복제 된 저장소에 지원 됩니다.
5. **앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다. 클릭 **확인** toocreate hello 정책입니다.

    ![복제 정책](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. 새 정책을 만들 때 자동으로 hello 구성 서버와 연결 되어 있습니다. 기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다. 예를 들어 hello 복제 정책 인지 **rep 정책**, hello 장애 복구 정책은 **장애 복구 rep-정책**합니다. 이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.  


## <a name="plan-capacity"></a>용량 계획

1. 기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다. [자세히 알아보기](site-recovery-plan-capacity-vmware.md).
2. 용량 계획을 마쳤으면 **용량 계획을 완료하셨습니까?**에서 **예**를 선택합니다.

   ![용량 계획](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>복제용 VM 준비

Tooreplicate 원하는 모든 컴퓨터에는 hello 이동성 서비스가 설치 되어 있어야 합니다. 여러 가지 방법으로 hello 모바일 서비스를 설치할 수 있습니다.

- Hello 프로세스 서버에서 강제 설치로 hello 서비스를 설치 합니다. 이 메서드가 사전 toouse에 tooprepare 컴퓨터가 있어야 합니다.
- Azure 자동화 필요한 상태 구성 또는 System Center Configuration Manager와 같은 배포 도구를 사용 하 여 hello 서비스를 설치 합니다.
- Hello 서비스를 수동으로 설치 합니다.

[자세히 알아봅니다](site-recovery-vmware-to-azure-install-mob-svc.md).


## <a name="enable-replication"></a>복제 활성화

시작하기 전에 다음을 수행합니다.

- Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.
- 를 추가 하거나 Vm을 수정할 때이 지나야 too15 분 또는 더 이상을 하 고 변경 내용 tootake 효과 대 한 hello 포털에서 tooappear 합니다.
- Vm에 대 한 hello 마지막으로 검색 한 시간을 확인할 수 있습니다 **구성 서버** > **마지막 연락처에서**합니다.
- hello에 예약 된 검색, 강조 표시 hello 구성 서버에 대 한 대기 하지 않고 Vm tooadd (클릭 하지 말고)를 클릭 하 고 **새로 고침**합니다.
- 강제 설치에 대 한 VM 준비 된 경우 복제를 사용 하도록 설정 하면 프로세스 서버 hello가 자동으로 hello 모바일 서비스를 설치 합니다.
- 간단한 비디오 개요 보기 (비디오 hello tooreplicate VMware Vm 되지만 hello 처리 하는 방법을 설명 물리적 컴퓨터 복제에 대 한 것과 비슷합니다.)

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. 디스크를 복제에서 제외할 수 있습니다. 예를 들어 임시 데이터로 tooreplicate 디스크 원하지 않을 수 있습니다 또는 각각에 새로 고쳐지는 데이터는 시스템 또는 응용 프로그램 다시 시작 (예를 들어 pagefile.sys 또는 SQL Server tempdb) 시간입니다.

### <a name="replicate-vms"></a>VM 복제

1. **응용 프로그램 복제** > **원본**을 클릭합니다.
2. **원본**에서 **온-프레미스**를 선택합니다.
3. **소스 위치**선택, hello 구성 서버 이름입니다.
4. **컴퓨터 형식**에서 **물리적 컴퓨터**를 선택합니다.
5. **프로세스 서버**, hello 프로세스 서버를 선택 합니다. 모든 추가 프로세스 서버를 만들지 않은 경우이 서버는 hello 구성 서버. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-physical-to-azure/chooseVM.png)

6. **대상**선택, hello **구독** 및 hello **리소스 그룹** 장애 조치 후 toocreate hello Azure Vm 만들려는 합니다. Hello 배포 선택 toouse Azure에서 원하는 모델 (클래식 또는 리소스 관리자) hello 실패 한 Vm에 대 한 합니다.

7. 데이터 복제를 위한 toouse 원하는 hello Azure 저장소 계정을 선택 합니다. Toouse를 이미 설정한 계정을 사용 하지 않으려는 경우 새를 만들 수 있습니다.

8. 선택 hello **Azure 네트워크** 및 **서브넷** 장애 조치 후 toowhich Azure Vm에 연결 합니다. 선택 **선택한 컴퓨터에 지금 구성** tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다. 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다. Toouse 기존 네트워크를 사용 하지 않으려는 경우 하나를 만들 수 있습니다.

    ![복제 활성화](./media/site-recovery-physical-to-azure/targetsettings.png)

9. **물리적 컴퓨터**, 클릭 **+ 물리적 컴퓨터** hello 입력 **이름** 및 **IP 주소**합니다. Hello 운영 체제를 선택 하려는 tooreplicate hello 컴퓨터의 합니다. 컴퓨터 검색 되 고 hello 목록에 표시 될 때까지 몇 분 걸립니다.

    ![복제 활성화](./media/site-recovery-physical-to-azure/machineselect.png)

10. **속성** > **속성 구성**선택, hello 계정 toobe hello 프로세스 서버 tooautomatically에서 사용 하는 hello 머신에서 hello 모바일 서비스를 설치 합니다.
11. 기본적으로 모든 디스크가 복제됩니다. 클릭 **모든 디스크**, tooreplicate 원하는 디스크의 선택을 취소 합니다. 그런 후 **OK**를 클릭합니다. 나중에 추가 VM 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/site-recovery-physical-to-azure/configprop.png)

12. **복제 설정을** > **복제 설정을 구성**, 복제 정책을 선택 되어 올바른 해당 hello를 확인 합니다. 정책을 수정 하면 변경 내용이 적용 된 toohello 컴퓨터와 toonew 컴퓨터를 복제 됩니다.
13. 사용 하도록 설정 **다중 VM 일관성** toogather 컴퓨터를 복제 그룹으로 사용할 hello 그룹의 이름을 지정 하는 경우. 그런 후 **OK**를 클릭합니다. 다음 사항에 유의하세요.

    a. 복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.

    b. 워크로드를 미러링하도록 VM 및 물리적 서버를 함께 수집하는 것이 좋습니다. 다중 VM 일관성을 사용하면 워크로드 성능에 영향을 줄 수 있습니다. 컴퓨터가 있는 경우 실행 hello 같은 작업 부하 및 일관성이 필요한만 사용 해야 합니다.

    ![복제 활성화](./media/site-recovery-physical-to-azure/policy.png)

14. **복제 사용**을 클릭합니다. Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **설정** > **작업** > **사이트 복구 작업이**. Hello 후 **보호 완료** hello 컴퓨터가 장애 조치에 대해 준비 되었는지, 작업을 실행 합니다.

복제를 활성화 한 후 강제 설치를 설정 하는 경우 hello 모바일 서비스 설치 됩니다. Hello 모바일 서비스 푸시 컴퓨터에 설치 되 면 보호 작업을 시작 하 고 실패 합니다. 필요한 toomanually hello 오류가 발생 한 후 각 컴퓨터를 다시 시작 합니다. Hello 보호 작업을 다시 시작 하 고 초기 복제가 발생 합니다.


### <a name="view-and-manage-azure-vm-properties"></a>Azure VM 속성 보기 및 관리

Hello VM 속성을 확인 하 고 필요한 변경 내용을 확인 하는 것이 좋습니다.

1. 클릭 **복제 항목**, 및 select hello 컴퓨터입니다. hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.
2. **속성**및 복제를 볼 수 있습니다에 대 한 장애 조치 정보 hello VM입니다.
3. **계산 및 네트워크** > **속성 계산**, hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다. 수정 된 hello 이름 toocomply [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 하는 경우.
4. Toohello Azure VM에 할당 된 hello 대상 네트워크, 서브넷 및 IP 주소에 대 한 설정을 수정 합니다.

    a. Hello 대상 IP 주소를 설정할 수 있습니다.

    b.  주소를 제공 하지 않으면 hello 실패 한 컴퓨터는 DHCP를 사용 합니다.

    c. 장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.

    d. hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.

    e. 네트워크 어댑터의 hello 수 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.

     - Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 hello 대상 컴퓨터 크기에 허용 된 어댑터의 hello 개수 보다 작거나 같은 다른 이름으로 hello 경우 hello 대상에 hello hello 소스와 같은 수의 어댑터.
     - Hello hello 원본 가상 컴퓨터에 대 한 어댑터 수가 초과 hello 대상 크기에 대 한 허용 되는 hello 수 경우 hello 대상 크기의 최대는 데 사용 됩니다.
     - 예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 hello 대상 컴퓨터에 두 개의 어댑터가 있습니다. Hello 원본 컴퓨터에 두 개의 어댑터가 지원 hello 대상 크기를 지 원하는 하나만 표시 되지만 hello 대상 컴퓨터에 어댑터가 하나 뿐입니다.     
   - 모든 연결 toohello hello 가상 컴퓨터 네트워크 어댑터가 여러 개 있는 경우 동일한 네트워크입니다.
   - Hello 가상 컴퓨터에 여러 네트워크 어댑터 경우 hello 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure VM의에서 네트워크 어댑터입니다.
5. **디스크**, hello VM 운영 체제 및 복제 된 hello 데이터 디스크를 볼 수 있습니다.

## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행

모든 항목을 설정한 후에 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다. 시작하기 전에 간단한 동영상 개요를 봅니다.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. 단일 컴퓨터를 통해 toofail에서 **설정** > **복제 항목**, 클릭 **테스트 장애 조치**합니다.

    ![테스트 장애 조치(Failover)](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. 복구를 통해 toofail 계획 **설정** > **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다. 복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.  
3. **테스트 장애 조치**선택, hello Azure 네트워크 toowhich Azure Vm 장애 조치가 발생 한 후에 연결 되어 있습니다.
4. 클릭 **확인** toobegin hello 장애 조치 합니다. Hello VM tooopen 해당 속성을 클릭 하 여 또는 hello를 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **설정** > **작업**  >  **사이트 복구 작업이**합니다.
5. Hello 장애 조치 완료 되 면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 합니다.
6. 경우 있습니다 [장애 조치 이후 연결에 대 한 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), 수 tooconnect toohello Azure VM 수 있어야 합니다.
7. 을 마친 후 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. **노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 이 단계는 테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.

자세한 내용은 참조 hello [테스트 장애 조치 tooAzure](site-recovery-test-failover-to-azure.md) 문서.

## <a name="next-steps"></a>다음 단계

한 후 복제 가져오고 hello 복제 된 데이터에서 만들어진 경우 중단이 발생 한 장애 조치 tooAzure, 및 Azure Vm을 실행 합니다. 작업 및 Azure에서 응용 프로그램 toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패할 때까지 액세스할 수 있습니다.

- [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 방법과 toorun 해당 합니다.
- 컴퓨터를 복제하고 장애 복구하는 대신 마이그레이션하는 경우 [여기를 참조하세요](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- 물리적 컴퓨터를 복제 하는 경우 장애 복구 tooa VMware 환경에만 할 수 있습니다. [장애 복구(failback)에 대해 자세히 읽어보세요](site-recovery-failback-azure-to-vmware.md).

## <a name="third-party-software-notices-and-information"></a>타사 소프트웨어 통지 및 정보
Do Not Translate or Localize

hello 소프트웨어 및 펌웨어에서 실행 중인 hello Microsoft 제품 또는 서비스 기반으로 하거나 통합 hello의 자료 (통칭 "제 3 자 코드") 아래에 나열 된 프로젝트입니다. Microsoft는 hello hello 제 3 자 코드의 원 작 자가 없습니다. hello 원본 저작권 표시 및 라이선스, Microsoft는 이러한 제 3 자 코드를 받은 아래 명시 설정 됩니다.

A 섹션의 hello 정보에는 제 3 자 코드 아래에 나열 된 hello 프로젝트에서 구성 요소 관련입니다. Such licenses and information are provided for informational purposes only. 이 제 3 자 코드에서 Microsoft의 소프트웨어 사용 약관 hello Microsoft 제품 또는 서비스에 대 한 Microsoft에서 relicensed tooyou 되 고 있습니다.  

hello 정보 섹션 B에 대해 시도 하는 사용 가능한 tooyou microsoft hello 원래 라이선스 조건에 따라 제 3 자 코드 구성 요소 관련입니다.

hello에 hello 전체 파일을 찾을 수 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=529428)합니다. Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.
