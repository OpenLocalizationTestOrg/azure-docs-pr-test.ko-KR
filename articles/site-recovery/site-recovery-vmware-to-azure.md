---
title: VMware Vm tooAzure aaaReplicate | Microsoft Docs
description: "VMware Vm tooAzure 저장소에서 실행 되는 작업을 복제 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-overview
ms.openlocfilehash: f800e7d8a3b59a86809a995748eacf87630a1713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-tooazure-with-site-recovery"></a>사이트 복구와 VMware 가상 컴퓨터 tooAzure 복제

> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmware-to-azure.md)
> * [Azure 클래식](site-recovery-vmware-to-azure-classic.md)


이 문서에서는 어떻게 tooreplicate 온-프레미스 VMware 가상 컴퓨터 tooAzure, hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

원하면 toomigrate VMware Vm tooAzure (장애 조치만), 읽기 [이 여기서](site-recovery-migrate-to-azure.md) toolearn 더 합니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="deployment-steps"></a>배포 단계

여기에 사용자의 할 toodo:

1. 필수 조건 및 제한 사항을 확인합니다.
2. Azure 네트워크 및 저장소 계정을 설정합니다.
3. Hello 온-프레미스 컴퓨터를 준비 hello 구성 서버로 toodeploy 원하는 합니다.
4. Vm의 자동 검색 하 고 필요에 따라 hello 모바일 서비스의 강제 설치에 대 한 toobe에 사용 되는 VMware 계정을 준비 합니다.
4. Recovery Services 자격 증명 모음을 만듭니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.
5. 원본, 대상 및 복제 설정을 지정합니다.
6. Hello 모바일 서비스를 배포 하려는 tooreplicate Vm에서 합니다.
7. Hello Vm에 대 한 복제를 사용 하도록 설정 합니다.
7. 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

## <a name="prerequisites"></a>필수 조건

**지원 요구 사항** | **세부 정보**
--- | ---
**Azure** | [Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.
**온-프레미스 구성 서버** | Windows Server 2012 R2 이상을 실행하는 VMware VM이 필요합니다. Site Recovery를 배포하는 동안 이 서버를 설정합니다.<br/><br/> 기본 hello 프로세스에 의해 서버 및 마스터 대상 서버 에서도이 VM에 설치 됩니다. 수직 확장, 별도 프로세스 서버를 할 수 있고 hello 갖고 hello 구성 서버와 동일한 요구 사항이 있습니다.<br/><br/> [여기](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)에서 이러한 구성 요소에 대해 자세히 알아보기
**온-프레미스 VMware 서버** | 최신 업데이트가 포함된 6.0, 5.5, 5.1을 실행하는 하나 이상의 VMware vSphere 서버. 서버 hello hello 구성 서버 (또는 별도 프로세스 서버)와 동일한 네트워크에 있어야 합니다.<br/><br/> VCenter 서버 toomanage 실행 하는 호스트를, 6.0 또는 5.5 hello 최신 업데이트로 좋습니다. 버전 6.0을 배포하는 경우 5.5에서 사용할 수 있는 기능만 지원됩니다.
**온-프레미스 VM** | Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다. VM에서 VMware 도구가 실행되어야 합니다.
**URL** | 구성 서버 hello toothese Url에 액세스 해야 합니다.<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.<br/></br> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.<br/></br> West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.<br/><br/> 이 URL hello MySQL 다운로드에 대 한 허용: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi 합니다.
**모바일 서비스** | 모든 복제된 VM에 설치




## <a name="limitations"></a>제한 사항

**제한 사항** | **세부 정보**
--- | ---
**Azure** | 저장소 및 네트워크 계정은 hello에 있어야 hello 자격 증명 모음과 동일한 지역<br/><br/> 프리미엄 저장소 계정을 사용 하는 경우 또한 해야 표준 계정 toostore 복제 로그를 저장 합니다.<br/><br/> Toopremium 계정 중앙 및 남 인도에 복제할 수 없습니다.
**온-프레미스 구성 서버** | VMware VM 어댑터 유형은 VMXNET3이어야 합니다. 그렇지 않은 경우 [이 업데이트를 설치하세요.](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> vSphere PowerCLI 6.0을 설치해야 합니다.<br/><br> hello 컴퓨터는 도메인 컨트롤러일 하지 않아야 합니다. hello 컴퓨터에 고정 IP 주소를 해야 합니다.<br/><br/> hello 호스트 이름은 15 자 여야 합니다, 운영 체제 영어에 있어야 합니다.
**VMware** | vCenter 6.0에서는 5.5 기능만 지원됩니다. Site Recovery에서는 교차 vCenter vMotion, 가상 볼륨 및 저장소 DRS와 같은 새로운 vCenter 및 vSphere 6.0 기능을 지원하지 않습니다.
**VM** | [Azure VM 제한 사항](site-recovery-prereq.md#azure-requirements) 확인<br/><br/> 암호화된 디스크를 사용하는 VM 또는 UEFI/EFI 부팅을 사용하는 VM은 복제할 수 없습니다.<br/><br> 공유 디스크 클러스터는 지원되지 않습니다. Hello 소스가 VM에서 NIC 팀을 가진 경우 변환 tooa 장애 조치 후 NIC를 단일 합니다.<br/><br/> Vm에 iSCSI 디스크 있으면 사이트 복구 변환 tooa VHD 파일 장애 조치 후 합니다. Hello Azure VM으로 hello iSCSI 대상에 연결할 수 경우 tooit를 연결 하 고 괄호와 hello VHD에 게 표시 합니다. 이 경우 hello iSCSI 대상 연결을 끊습니다.<br/><br/> 동일한 작업 toobe 복구 hello를 실행 하는 Vm 수 있는 tooenable 다중 VM 일관성을 원하는 함께 tooa 일관 된 데이터를 가리키고 20004 hello VM에서 포트를 열어야 합니다.<br/><br/> Windows는 hello C 드라이브에 설치 되어야 합니다. 기본 및 동적 아님 hello OS 디스크 여야 합니다. 데이터 디스크 hello 동적일 수 있습니다.<br/><br/> Vm에서 Linux /etc/hosts 파일에는 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목이 없어야 합니다. 호스트 이름, 탑재 지점, 장치 이름, 시스템 경로 및 파일 이름 hello (/ 등; /usr)만 영어에 있어야 합니다.<br/><br/> 특정 유형의 [Linux 저장소](site-recovery-support-matrix-to-azure.md#support-for-storage)가 지원됩니다.<br/><br/>만들거나 설정 **disk.enableUUID=true** hello VM 설정에서 합니다. 올바르게를 탑재 하 고만 델타 변경 내용을 전체 복제 하지 않고 장애 복구 하는 동안 전송된 백 tooon 온-프레미스 있도록 일관 된 UUID toohello VMDK를 제공 합니다.

## <a name="set-up-azure"></a>Azure 설정

1. [Azure 네트워크를 설정합니다](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    - Azure VM은 장애 조치 후 처음 만들 때 이 네트워크에 배치됩니다.
    - [리소스 관리자](../resource-manager-deployment-model.md) 또는 클래식 모드에서 네트워크를 설정할 수 있습니다.

2. 복제 데이터를 저장할 [Azure Storage 계정](../storage/storage-create-storage-account.md#create-a-storage-account)을 설정합니다.
    - hello 계정 표준 수 또는 [프리미엄](../storage/storage-premium-storage.md)합니다.
    - 리소스 관리자 또는 클래식 모드에서 계정을 설정할 수 있습니다.

3. [계정을 준비](#prepare-for-automatic-discovery-and-push-installation) hello vCenter 서버나 vSphere 호스트에 있으므로 해당 사이트 복구 자동 검색할 수 있는 VMware Vm입니다.

## <a name="prepare-hello-configuration-server"></a>Hello 구성 서버를 준비 합니다.

1. Windows Server 2012 R2 이상을 VMware VM에 설치합니다.
2. Hello VM에 나열 된 액세스 toohello Url에 있는지 확인 [필수 구성 요소](#prerequisites)합니다.
3. [VMware vSphere PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1)을 설치합니다.


## <a name="prepare-for-automatic-discovery-and-push-installation"></a>자동 검색 및 푸시 설치를 위한 준비

- **자동 검색에 대 한 계정을 준비**: hello 사이트 복구 프로세스 서버 Vm은 자동으로 검색 합니다. toodo vCenter 서버와 vSphere ESXi 호스트에 액세스할 수 있는,이 사이트 복구 요구 자격 증명입니다.

    1. toouse 전용된 계정 역할을 만듭니다 (각각 hello vCenter 수준에서 [권한을](#vmware-account-permissions)합니다. 이름을 **Azure_Site_Recovery**와 같이 지정합니다.
    2. 그런 다음 hello vSphere 호스트/vCenter 서버에 사용자를 만들고 hello 역할 toohello 사용자를 할당 합니다. Site Recovery를 배포하는 동안 이 사용자 계정을 지정합니다.

- **계정 toopush hello 모바일 서비스를 준비**: toopush hello 이동성 서비스 tooVMs 원하는 hello 프로세스 서버 tooaccess hello VM에서 사용할 수 있는 계정이 필요 합니다. hello 계정 hello 강제 설치에만 사용 됩니다. 도메인 또는 로컬 계정을 사용할 수 있습니다.

    - Windows 도메인 계정을 사용 하지 않는 경우 필요 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 합니다. 이 hello에 등록할 toodo **찾아**, hello DWORD 항목을 추가 **LocalAccountTokenFilterPolicy**, 값이 1 인 합니다.
    - Windows에서 CLI tooadd hello 레지스트리 항목을 하려는 경우 다음을 입력 합니다.``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
    - Linux 용 hello 계정은 hello 원본 Linux 서버에 루트 이어야 합니다.

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-hello-protection-goal"></a>Hello 보호 목표를 선택 합니다.

대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.

1. **Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.
2. Hello 리소스 메뉴, 클릭 **사이트 복구** > **1 단계: 인프라 준비** > **보호 목표**합니다.

    ![목표 선택](./media/site-recovery-vmware-to-azure/choose-goals.png)
3. **보호 목표**선택, **tooAzure** > **VMware vSphere 하이퍼바이저와 예,**합니다.

    ![목표 선택](./media/site-recovery-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hello 소스 환경 설정

Hello 구성 서버를 설정 하 고 hello 자격 증명 모음에 등록 한 다음 Vm을 검색 합니다.

1. **Site Recovery** > **1단계: 인프라 준비** > **원본**을 클릭합니다.
2. 구성 서버가 없는 경우 **+구성 서버**를 클릭합니다.

    ![원본 설정](./media/site-recovery-vmware-to-azure/set-source1.png)
3. **서버 추가**에서 **구성 서버**가 **서버 형식**에 표시되는지 확인합니다.
4. Hello Site Recovery 통합 설치 설치 파일을 다운로드 합니다.
5. Hello 자격 증명 모음 등록 키를 다운로드 합니다. 통합 설치를 실행할 때 이 키가 필요합니다. hello 키가 생성 한 후 5 일 동안 유효 합니다.

   ![원본 설정](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a>Site Recovery 통합 설치 프로그램 실행

수행 하기 전에 hello 다음로 시작 하 고 통합 설치 tooinstall hello 구성 서버, hello 프로세스 서버 및 마스터 대상 서버 hello 실행 합니다.
    - 간단한 동영상 개요 보기

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Hello 구성 서버 VM에서 해당 hello 시스템 시계와 동기화 되었는지 확인 한 [시간 서버](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)합니다. 서로 일치해야 합니다. 15분 빠르거나 늦은 경우 설치가 실패할 수 있습니다.
    - Hello 구성 서버 VM에서 로컬 관리자로 설치 프로그램을 실행 합니다.
    - Hello VM에서 TLS 1.0을 사용할 수 있는지 확인 합니다.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> hello 구성 서버를 설치할 수도 있습니다 [hello 명령줄에서](http://aka.ms/installconfigsrv)합니다.



### <a name="add-hello-account-for-automatic-discovery"></a>자동 검색에 대 한 hello 계정 추가

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="connect-toovmware-servers"></a>TooVMware 서버 연결

ToovSphere ESXi 호스트 또는 VMware Vm toodiscover vCenter 서버를 연결 합니다.

- Hello 서버에서 관리자 권한이 없는 계정으로 vSphere 호스트 또는 hello vCenter 서버를 추가 하는 경우 hello 계정이 이러한 권한을 사용할 수 있어야 합니다.
    - 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터, vSphere 분산 스위치 등의 권한을 사용할 수 있도록 설정해야 합니다.
    - hello vCenter 서버에 저장소 보기 권한이 필요합니다.
- VMware 서버를 추가 하면 15 분이 걸릴 수 정도 대 한 hello 포털에서 tooappear 합니다.
tooallow Azure Site Recovery toodiscover 가상 컴퓨터 사용자의 온-프레미스 환경에서 실행 해야 tooconnect VMware vCenter Server 또는 사이트 복구와 vSphere ESXi 호스트 합니다.

선택 **+ vCenter** toostart VMware vCenter server 또는 VMware vSphere ESXi 호스트를 연결 합니다.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

TooVMware 서버를 연결 하는 사이트 복구 hello를 사용 하 여 설정을 지정 하 고 Vm을 검색 합니다.

## <a name="set-up-hello-target"></a>Hello 대상 설정

Hello 대상 환경 설정 하기 전에 확인 해야는 [Azure 저장소 계정 및 네트워크](#set-up-azure)

1. 클릭 **준비 인프라** > **대상**, 선택 hello toouse를 원하는 Azure 구독 및 합니다.
2. 대상 배포 모델이 리소스 관리자 기반인지, 클래식인지 지정합니다.
3. Site Recovery가 호환되는 Azure 저장소 계정 및 네트워크가 하나 이상 있는지 확인합니다.

   ![대상](./media/site-recovery-vmware-to-azure/gs-target.png)
4. 저장소 계정 또는 네트워크를 만들지 않은 경우 클릭 **저장소 계정 추가** 또는 **+ 네트워크**, 리소스 관리자 계정 또는 네트워크 인라인 toocreate 합니다.

## <a name="set-up-replication-settings"></a>복제 설정 지정

시작하기 전에 간단한 동영상 개요를 보세요.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. 새 복제 정책을 toocreate 클릭 **사이트 복구 인프라** > **복제 정책** > **+ 복제 정책**합니다.
2. **복제 정책 만들기**에서 정책 이름을 지정합니다.
3. **RPO 임계값**, hello RPO 제한을 지정 합니다. 이 값은 데이터 복구 지점 생성 횟수를 지정합니다. 연속 복제가 이 제한을 초과하면 경고가 생성됩니다.
4. **복구 지점 보존**, 기간 (시간)에 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다. 복제 된 Vm 수 tooany 지점 창에서 복구 합니다. 시간 보존 컴퓨터에 대해서는 too24를 toopremium 저장소 및 72 시간 정도 표준 저장소를 복제 합니다.
5. **응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다. 클릭 **확인** toocreate hello 정책입니다.

    ![복제 정책](./media/site-recovery-vmware-to-azure/gs-replication2.png)
8. 새 정책을 만들 때 자동으로 hello 구성 서버와 연결 되어 있습니다. 기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다. 예를 들어 hello 복제 정책 인지 **rep 정책** hello 장애 복구 정책 됩니다 **장애 복구 rep-정책**합니다. 이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.  



## <a name="plan-capacity"></a>용량 계획

1. 기본 인프라를 설치했으니 용량 계획에 대해 생각해 보고 추가 리소스가 필요한지 파악할 수 있습니다. [자세히 알아보세요](site-recovery-plan-capacity-vmware.md)을 확인하세요.
2. 용량 계획을 마쳤으면 **용량 계획을 완료하셨습니까?**에서 **예**를 선택합니다.

   ![용량 계획](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a>복제용 VM 준비

모바일 서비스 hello tooreplicate 원하는 모든 VMware Vm에 설치 되어야 합니다. 여러 가지 방법으로 hello 모바일 서비스를 설치할 수 있습니다.

1. Hello 프로세스 서버에서 강제 설치로 설치 합니다. 이 방법이 tooprepare Vm toouse 필요합니다.
2. System Center Configuration Manager 또는 Azure Automation DSC와 같은 배포 도구를 사용하여 설치합니다.
3.  수동으로 설치합니다.

[자세히 알아보기](site-recovery-vmware-to-azure-install-mob-svc.md)


## <a name="enable-replication"></a>복제 활성화

시작하기 전에 다음을 수행합니다.

- Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.
- 를 추가 하거나 Vm을 수정할 때이 지나야 too15 분 또는 더 이상 하 고 변경 tootake 효과 대 한 hello 포털에서 tooappear 합니다.
- Vm에 대 한 hello 마지막으로 검색 한 시간을 확인할 수 있습니다 **구성 서버** > **마지막 연락처에서**합니다.
- hello에 예약 된 검색, 강조 표시 hello 구성 서버에 대 한 대기 하지 않고 Vm tooadd (클릭 하지 말고)를 클릭 하 고 **새로 고침**합니다.
- 강제 설치에 대 한 VM 준비 된 경우 복제를 사용 하도록 설정 하면 프로세스 서버 hello가 자동으로 hello 모바일 서비스를 설치 합니다.


### <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. 디스크를 복제에서 제외할 수 있습니다. 예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다.

### <a name="replicate-vms"></a>VM 복제

시작하기 전에 간단한 동영상 개요를 보세요.

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다.
2. **소스**선택, hello 구성 서버입니다.
3. **컴퓨터 형식**에서 **가상 컴퓨터**를 선택합니다.
4. **vCenter/vSphere 하이퍼바이저**를 hello vSphere 호스트를 관리 하는 hello vCenter 서버를 선택 하거나 hello 호스트를 선택 합니다.
5. Hello 프로세스 서버를 선택 합니다. 모든 추가 프로세스 서버를 만들지 않은 경우 구성 서버 hello 됩니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. **대상**리소스 그룹을 장애 조치 Vm toocreate hello 원하는 hello을 hello 구독을 선택 합니다. 장애 조치 Vm hello에 대 한 (기본 또는 리소스 관리), Azure에서 toouse 원하는 hello 배포 모델을 선택 합니다.


7. 데이터 복제를 위한 toouse 원하는 hello Azure 저장소 계정을 선택 합니다. Toouse를 이미 설정한 계정을 사용 하지 않으려는 경우 새를 만들 수 있습니다.

8. 장애 조치 후 처음 만들어질 때 선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm이 연결 됩니다. 선택 **선택한 컴퓨터에 지금 구성**, tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다. 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다. Toouse 기존 네트워크를 사용 하지 않으려는 경우 하나를 만들 수 있습니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. **가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다. 복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. **속성** > **속성 구성**을 선택 하는 hello 프로세스 서버 tooautomatically 사용한 hello 계정 hello 머신에서 hello 모바일 서비스를 설치 합니다.
11. 기본적으로 모든 디스크가 복제됩니다. 클릭 **모든 디스크** tooreplicate 원하는 디스크의 선택을 취소 합니다. 그런 후 **OK**를 클릭합니다. 나중에 추가 VM 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication6.png)
11. **복제 설정을** > **복제 설정을 구성**, 복제 정책을 선택 되어 올바른 해당 hello를 확인 합니다. 정책을 수정 하면 변경 사항이 적용 된 tooreplicating 시스템과 toonew 컴퓨터 됩니다.
12. 사용 하도록 설정 **다중 VM 일관성** toogather 컴퓨터를 복제 그룹으로 사용할 hello 그룹의 이름을 지정 하는 경우. 그런 후 **OK**를 클릭합니다. 다음 사항에 유의하세요.

    * 복제 그룹의 컴퓨터는 함께 복제되고 장애 조치(failover) 시 공유 크래시 일관성 및 앱 일치 복구 지점을 갖습니다.
    * 워크로드를 미러링하도록 VM 및 물리적 서버를 함께 수집하는 것이 좋습니다. 작업 성능에 영향을 줄 수 다중 VM 일관성이 사용 하도록 설정 하 고 컴퓨터가 hello를 실행 하는 경우에 사용 해야 동일한 작업 및 일관성에 필요 합니다.

    ![복제 활성화](./media/site-recovery-vmware-to-azure/enable-replication7.png)
13. **복제 사용**을 클릭합니다. Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **설정** > **작업** > **사이트 복구 작업이**. Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.

### <a name="view-and-manage-vm-properties"></a>VM 속성 보기 및 관리

Hello VM 속성을 확인 해야 할 변경 하는 것이 좋습니다.

1. 클릭 **복제 항목** >, 및 select hello 컴퓨터입니다. hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.
2. **속성**및 복제를 볼 수 있습니다에 대 한 장애 조치 정보 hello VM입니다.
3. **계산 및 네트워크** > **속성 계산**, hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다. 수정 된 hello 이름 toocomply [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 하는 경우.
4. Hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 설정을 수정 합니다.

   - Hello 대상 IP 주소를 설정할 수 있습니다.

    - 주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다.
    - 장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.
    - hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.

   - 네트워크 어댑터의 hello 수 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.

     - Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 hello 대상 컴퓨터 크기에 허용 된 어댑터의 hello 개수 보다 작거나 같은 다른 이름으로 hello 경우 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
     - Hello hello에 대 한 어댑터 수가 원본 가상 컴퓨터는 hello 대상 크기는 최대 사용 됩니다 hello 대상 크기에 허용 된 hello 수를 초과 합니다.
     - 예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.     
   - Hello 가상 컴퓨터에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.
   - Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.
4. **디스크**, hello VM 운영 체제를 확인할 수 있습니다 및 hello 데이터 디스크는 복제 됩니다.

#### <a name="managed-disks"></a>관리 디스크

**계산 및 네트워크** > **속성 계산**, 장애 조치 tooAzure에서 관리 하는 디스크 tooyour 컴퓨터 tooattach hello VM에 대 한 너무 "Yes" 설정 "디스크 관리 되는 사용"을 설정할 수 있습니다. 관리 되는 디스크 hello VM 디스크와 연결 된 hello 저장소 계정을 관리 하 여 Azure IaaS Vm에 대 한 디스크 관리를 간소화 합니다. [Managed Disks에 대해 자세히 알아봅니다.](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)

   - 관리 되는 디스크는 장애 조치 tooAzure에 대해서만 생성 되 고 연결 된 toohello 가상 컴퓨터입니다. 보호를 사용 하도록 설정 하면, 온-프레미스 컴퓨터의에서 데이터를 tooreplicate toostorage 계정을 계속 됩니다.  Hello 리소스 관리자 배포 모델을 사용 하 여 배포 된 가상 컴퓨터에 대해서만 관리 하는 디스크를 만들 수 있습니다.  

   - 너무 "Yes" "디스크 관리 되는 사용"을 설정 하는 경우 가용성 집합에만 hello 리소스 그룹의 "디스크 관리 되는 사용" 집합과 너무 "Yes" 것을 선택할 수입니다. 즉, 관리 되는 디스크와 가상 컴퓨터 "디스크 관리를 사용 하 여" 속성이 설정 된 가용성 집합의 일부가 너무 "Yes" 수만 있습니다. "디스크 관리를 사용 하 여" 속성이 설정 된 장애 조치 시 의도 toouse 관리 되는 디스크에 따라 가용성 집합을 만드는 있는지 확인 합니다.  마찬가지로, 설정 하는 경우 "디스크 관리 되는 사용" 너무 "No", "디스크 관리 되는 사용" 속성이 너무 "아니요"를 설정 하는 hello 리소스 그룹에만 가용성 집합은 선택할 수 있는 것입니다. [Managed Disks와 가용성 집합에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Hello 저장소 계정 복제에 사용 되는 시간에 언제 든 지 저장소 서비스 암호화로 암호화 된, 장애 조치 중에 관리 되는 디스크를 만들 실패 합니다. 유지할 수 있습니다 설정 "디스크 관리 되는 사용" 너무 "No" 장애 조치를 다시 시도 또는 hello 가상 컴퓨터에 대 한 보호를 사용 하지 않도록 설정 하 고 저장소 서비스 암호화 시간에서 언제 든 지 사용할 수 없는 tooa 저장소 계정을 보호 합니다.
  > [저장소 서비스를 암호화 및 Managed Disks에 대해 자세히 알아봅니다](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행


한 모든 항목을 설정한 후에 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다. 시작하기 전에 간단한 동영상 개요 보기
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. 단일 컴퓨터를 통해 toofail에서 **설정** > **복제 항목**, hello VM을 클릭 > **+ 테스트 장애 조치** 아이콘.

    ![테스트 장애 조치(Failover)](./media/site-recovery-vmware-to-azure/TestFailover.png)

1. 복구를 통해 toofail 계획 **설정** > **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다. 복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.  

1. **테스트 장애 조치**선택, 장애 조치 발생 후 hello Azure 네트워크 toowhich Azure Vm 연결 됩니다.

1. 클릭 **확인** toobegin hello 장애 조치 합니다. Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **설정** > **작업**  >  **사이트 복구 작업이**합니다.

1. Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 해야 합니다.

1. 경우 있습니다 [장애 조치 이후 연결에 대 한 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), 수 tooconnect toohello Azure VM 수 있어야 합니다.

1. 완료 되 면 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. **노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 테스트 장애 조치 중에 생성 된 hello Vm을 삭제 합니다.

테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).


## <a name="vmware-account-permissions"></a>VMware 계정 권한

사이트 복구 및 장애 조치 및 Vm의 장애 복구에 hello 프로세스 서버 tooautomatically 검색 Vm에 대 한 액세스 tooVMware 필요 합니다.

- **마이그레이션**: 읽기 전용 역할을 갖는 VMware 계정 적이 다시 실패 하지 않고 toomigrate VMware Vm tooAzure만 하려는 경우 사용할 수 있습니다. 이러한 역할은 장애 조치(failover)를 실행할 수 있지만 보호된 원본 컴퓨터를 종료할 수는 없습니다. 마이그레이션에서는 필요하지 않습니다.
- **Replicate/복구**: Vm 등의 전원을 켜는 toodeploy 전체 복제 (복제, 장애 조치, 장애 복구) hello 계정이 생성 및 디스크를 제거 하는 등의 작업 수 toorun 이어야 합니다.
- **자동 검색**: 최소한 읽기 전용 계정이 필요합니다.


**Task** | **필요한 계정/역할** | **권한** | **세부 정보**
--- | --- | --- | ---
**프로세스 서버가 VMware VM을 자동으로 검색** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체, toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).
**장애 조치(Failover)** | 최소한 읽기 전용 사용자 필요 | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 = 읽기 전용 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체 toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).<br/><br/> 전체 복제, 장애 조치, 장애 복구가 아닌 마이그레이션에 유용합니다.
**장애 조치 및 장애 복구** | Hello 필요한 사용 권한이 있는 역할 (Azure_Site_Recovery)을 만들고 다음 hello 역할 tooa VMware 사용자 또는 그룹을 할당 것이 좋습니다. | 데이터 센터 개체 –> 전파 tooChild 개체, 역할 Azure_Site_Recovery =<br/><br/> 데이터 저장소 -> 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트<br/><br/> 네트워크 -> 네트워크 할당<br/><br/> 리소스 할당 VM tooresource 풀->, 마이그레이션 전원이 꺼진 VM, VM의 전원이 마이그레이션<br/><br/> 태스크 -> 만들기 태스크, 업데이트 태스크<br/><br/> 가상 컴퓨터 -> 구성<br/><br/> 가상 컴퓨터 -> 상호 작용 -> 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치<br/><br/> 가상 컴퓨터 -> 인벤토리 -> 만들기, 등록, 등록 취소<br/><br/> 가상 컴퓨터 -> 프로비전 -> 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용<br/><br/> 가상 컴퓨터 -> 스냅숏 -> 스냅숏 제거 | 사용자는 데이터 센터 수준에서 할당 된 많고 hello 데이터 센터의 tooall hello 개체에 액세스 합니다.<br/><br/> toorestrict 액세스, 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체, toohello 자식 개체 (vSphere 호스트, 데이터 저장소, Vm 및 네트워크).


## <a name="next-steps"></a>다음 단계

한 후 복제 가져오고 hello 복제 된 데이터에서 만들어진 경우 중단이 발생 한 장애 조치 tooAzure, 및 Azure Vm을 실행 합니다. 작업 및 Azure에서 응용 프로그램 toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패할 때까지 액세스할 수 있습니다.

- [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.
- 컴퓨터를 복제하고 장애 복구하는 대신 마이그레이션하는 경우 [여기를 참조하세요](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [장애 복구에 대해 알아보세요](site-recovery-failback-azure-to-vmware.md), 복제 Azure Vm 및 toofail 다시 toohello 기본 온-프레미스 사이트를 백업 합니다.

## <a name="third-party-software-notices-and-information"></a>타사 소프트웨어 통지 및 정보
Do Not Translate or Localize

hello 소프트웨어 및 펌웨어에서 실행 중인 hello Microsoft 제품 또는 서비스 기반으로 하거나 통합 hello의 자료 (통칭 "제 3 자 코드") 아래에 나열 된 프로젝트입니다.  Microsoft는 hello hello 제 3 자 코드의 하지 원 작 자가 있습니다.  hello 원본 저작권 표시 및 라이선스, Microsoft는 이러한 제 3 자 코드를 받은 아래 명시 설정 됩니다.

A 섹션의 hello 정보에는 제 3 자 코드 아래에 나열 된 hello 프로젝트에서 구성 요소 관련입니다. Such licenses and information are provided for informational purposes only.  이 제 3 자 코드에서 Microsoft의 소프트웨어 사용 약관 hello Microsoft 제품 또는 서비스에 대 한 Microsoft에서 relicensed tooyou 되 고 있습니다.  

hello 정보 섹션 B에 대해 시도 하는 사용 가능한 tooyou microsoft hello 원래 라이선스 조건에 따라 제 3 자 코드 구성 요소 관련입니다.

hello 전체 파일 hello에서 발견 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=529428)합니다. Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
