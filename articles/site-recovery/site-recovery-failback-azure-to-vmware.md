---
title: "VMware Vm Azure tooon 온-프레미스에서 aaaFailback | Microsoft Docs"
description: "VMware Vm 및 물리적 서버 tooAzure의 장애 조치 후 뒤로 toohello 온-프레미스 사이트 실패 하는 방법을 알아봅니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 5a47337f-89a9-43e8-8fdc-7da373c0fb0f
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: ruturajd
ms.openlocfilehash: 258f5a55252083135b2040e5a235fa1ffbf3b9d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-toohello-on-premises-site"></a>뒤로 VMware 가상 컴퓨터 및 물리적 서버 toohello 온-프레미스 사이트 실패


이 문서에서는 설명 방법을 toofailback Azure Azure toohello 온-프레미스 사이트에서 가상 컴퓨터. Hello 지침에 따라 여기 준비가 toofail 다시 VMware 가상 컴퓨터 또는 물리적 서버를 Windows 또는 Linux이를 사용 하 여 컴퓨터를 다시 보호 한 후 [참조](site-recovery-how-to-reprotect.md)합니다.

>[!NOTE]
>클래식 Azure 포털 hello를 사용 하는 경우 언급 tooinstructions를 참조 하십시오 [여기](site-recovery-failback-azure-to-vmware-classic.md) 향상 된 VMware tooAzure 아키텍처에 대 한 및 [여기](site-recovery-failback-azure-to-vmware-classic-legacy.md) hello 레거시 아키텍처에 대 한

## <a name="overview"></a>개요
이 섹션의 hello 다이어그램이이 시나리오에 대 한 hello 장애 복구 아키텍처를 보여 줍니다.

프로세스 서버 hello는 온-프레미스 Azure express 경로 연결을 사용 하는 경우이 아키텍처를 사용 합니다.

![ExpressRoute 아키텍처 다이어그램](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)

프로세스 서버를 Azure에 hello 보유 경우 VPN 또는 express 경로 연결을이 아키텍처를 사용 하 여:

![VPN 아키텍처 다이어그램](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)

포트 및 hello 장애 복구 아키텍처 다이어그램의 전체 목록은, toohello 이미지 다음을 참조 하세요.

![모든 포트의 장애 조치-장애 복구 목록](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

TooAzure를 통해 실패 한 후에 3 단계로 뒤로 tooyour 온-프레미스 사이트를 실패:

* **1 단계**: 온-프레미스 사이트에서 실행 되는 백 toohello VMware Vm 복제 시작 되도록 hello Azure Vm을 다시 보호 합니다.
* **2 단계**: Azure Vm이 온-프레미스 사이트 복제 tooyour, 후 실행할 장애 조치 toofail 다시 Azure에서.
* **3 단계**: tooAzure 복제 시작 되도록 장애 온-프레미스 Vm 백업할 hello를 다시 보호 데이터에 실패 한 다시 합니다.

### <a name="fail-back-toohello-original-location-or-an-alternate-location"></a>뒤로 toohello 원래 위치 또는 대체 위치 실패
뒤로 toohello 못하는 장애 조치 VMware VM 후 온-프레미스 아직 있는 경우 VM을 원본 동일 합니다. 이 시나리오에서는 hello 델타만 다시 장애 됩니다.

장애 복구 tooa는 항상 실제 서버 보다 실패 한 경우 새 VMware VM입니다. 물리적 컴퓨터를 장애 복구하기 전에 다음 사항에 유의하세요.
* Azure tooVMware에서 다시 장애 조치 되는 보호 되는 물리적 컴퓨터를 가상 컴퓨터로 다시 옵니다. Windows Server 2008 R2 SP1 물리적 컴퓨터를 보호 하 고 장애 조치 tooAzure, 하는 경우를 다시 장애 수 수 없습니다. 가상 컴퓨터를 온-프레미스를 시작 하는 Windows Server 2008 R2 SP1 컴퓨터 수 toofail 백 됩니다.
* 마스터 대상 서버를 하나 이상 검색할 수 있는지 확인 하십시오. hello 함께 toofail 해야 하는 필수 ESX/ESXi 호스트를 백업 합니다.

뒤로 toohello 실패 하면 원래 VM hello 다음이 필요 합니다.

* Hello VM을 관리 되는 vCenter 서버에 의해 hello 마스터 대상 ESX 호스트 있어야 액세스 toohello Vm 데이터 저장소.
* Hello VM ESX 호스트에 표시 되지만 vCenter에 의해 관리 되지 hello 하드 디스크의 hello VM에에서 있어야 hello MT의 호스트에서 액세스할 수 있는 데이터 저장소입니다.
* VM ESX 호스트에 vCenter를 사용 하지 않는 경우 다시 보호 하기 전에 hello MT의 hello ESX 호스트의 검색을 완료 해야 합니다. 물리적 서버도 장애 복구하는 경우 적용됩니다.
* (경우 hello 온-프레미스 VM이 있는) 하는 또 다른 옵션은 toodelete는 장애 복구를 수행 하기 전에 것입니다. 그런 다음 장애 복구 hello hello 마스터 대상 ESX 호스트와 동일한 호스트에 새 VM을 만듭니다.

Hello 데이터를 복구 된 toohello 백 tooan 대체 위치를 실패 하는 경우 동일한 데이터 저장소 및 hello hello 온-프레미스 마스터 대상 서버에서 사용 하는 것과 동일한 ESX 호스트입니다.

## <a name="prerequisites"></a>필수 조건
* 물리적 서버 및 toofail 다시 VMware Vm을 VMware 환경이 필요 합니다. 뒤로 tooa 실패 한 실제 서버 지원 되지 않습니다.
* 다시 toofail 만들었어야 Azure 네트워크 처음 보호를 설정 합니다. 장애 복구 hello Azure에서에서 VPN 또는 express 경로 연결이 필요한는 hello Azure Vm 네트워크는 온-프레미스 사이트 위치에 toohello 합니다.
* Hello toofail 원하는 Vm vCenter 서버에서 관리 tooare을 백업 하는 경우 vCenter 서버에 Vm의 검색에 필요한 hello 권한이 있는지 확인 합니다. 자세한 내용은 참조 [복제 VMware 가상 컴퓨터 및 Azure 사이트 복구와 실제 서버 tooAzure](site-recovery-vmware-to-azure-classic.md)합니다.
* 스냅숏이 VM에 있는 경우 다시 보호에 실패합니다. Hello 스냅숏 또는 hello 디스크를 삭제할 수 있습니다.
* 장애 복구하기 전에 다음 구성 요소를 만듭니다.
  * **Azure에 프로세스 서버 만들기**: 이 구성 요소는 장애 복구 중에 만들고 계속 실행하는 Azure VM입니다. 장애 복구 완료 된 후 VM hello를 삭제할 수 있습니다.
  * **마스터 대상 서버 만들기**: hello 마스터 대상 서버 장애 복구 데이터를 송수신 합니다. 온-프레미스를 만든 hello 관리 서버에는 기본적으로 설치 된 마스터 대상 서버를 있습니다. 그러나 장애 트래픽의 hello 볼륨에 따라 toocreate 별도 마스터 대상 서버 장애 복구 할 수 있습니다.
  * linux에서 실행 되는 추가 마스터 대상 서버 toocreate 나중에 설명 된 대로 hello 마스터 대상 서버를 설치 하기 전에 hello Linux VM를 설정 합니다.
* 장애 복구를 수행할 때 구성 서버가 온-프레미스에 있어야 합니다. 장애 복구 하는 동안 hello 가상 컴퓨터는 hello 구성 서버 데이터베이스에 존재 해야 합니다. Hello 구성 서버를 데이터베이스에 들어 없는 VM 장애 복구에 성공할 수 없습니다. 따라서 서버의 예약된 정기 백업을 수행해야 합니다. Toorestore 해야 재해를 사용 하 여 해당 장애 복구 작동 하므로 같은 IP 주소는 hello 합니다.
* Hello disk.enableUUID=true 설정에서 설정 **구성 매개 변수** hello 마스터의 VM VMware에서 대상으로 합니다. 이 행이 존재하지 않는 경우 추가합니다. 이 설정은 올바르게 탑재 되어 있도록 필요한 tooprovide 일관성 있는 범용 고유 식별자 (UUID) toohello 가상 컴퓨터 디스크 (VMDK) 파일입니다.
* 유의 해야는 "마스터 대상 서버에 저장소 vMotioned 될 수 없습니다" hello 장애 복구 toofail을 일으킬 수 있는 조건입니다. hello 디스크 사용 가능한 tooit 적용 하지 않는 것 이므로 VM hello 수립 수 없습니다.
* Hello 마스터 대상 서버 보존 드라이브 라는 드라이브를 추가 합니다. 디스크를 추가 하 고 hello 드라이브를 포맷 합니다.

## <a name="failback-policy"></a>장애 복구 정책
tooreplicate 백 tooon 온-프레미스, 장애 복구 정책이 필요합니다. hello 정책 정방향 정책을 만들고 hello 구성 서버에 자동으로 연결 될 때 자동으로 만들어집니다. 편집할 수는 없습니다. hello 정책 hello 복제 설정을 뒤에 있습니다.

* RPO 임계값 = 15분
* 복구 지점 보존 기간 = 24시간
* 앱 일치 스냅숏 빈도 = 60분

 ![Hello 장애 복구 정책의 복제 설정](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

## <a name="set-up-a-process-server-in-azure"></a>Azure에서 프로세스 서버 설정
Hello Azure Vm hello 데이터 백 toohello 온-프레미스 마스터 대상 서버에 보낼 수 있도록 Azure에서 프로세스 서버를 설치 합니다.

클래식 리소스 그룹으로 가상 컴퓨터를 보호 하는 경우 (즉, Azure에서 VM 복구 hello hello 클래식 배포 모델을 사용 하 여 만든 VM) 인 Azure 사용 하는 프로세스 서버가 필요 합니다. Hello hello 배포 유형으로 Azure 리소스 관리자와 Vm을 복구한 경우 hello 프로세스 서버 hello 배포 유형으로 리소스 관리자를 있어야 합니다. hello 배포 유형을 선택 하 여 hello Azure 배포 하는 가상 네트워크 hello 프로세스 서버를 합니다.

1. **자격 증명 모음** > **설정** > **사이트 복구 인프라** (아래 **관리**) > **구성 서버** (아래 **에 대 한 VMware와 물리적 컴퓨터**)을 선택 hello 구성 서버입니다.
2. **프로세스 서버**를 클릭합니다.

  ![프로세스 서버 단추](./media/site-recovery-failback-azure-to-vmware-classic/add-processserver.png)
3. Toodeploy 선택와 프로세스 서버 hello **장애 Azure에서 프로세스 서버 배포**합니다.
4. Hello Vm을 복구한 hello 구독을 선택 합니다.
5. Hello hello Vm을 복구한 Azure 네트워크를 선택 합니다. 프로세스 서버 요구 toobe hello hello Vm을 복구 하 고 hello 프로세스 서버 통신할 수 있도록 동일한 네트워크의 번호입니다.
6. 선택한 경우에 *클래식 배포 모델* hello Azure 마켓플레이스를 통해 VM 네트워크를 만들고 다음 그 안에 hello 프로세스 서버를 설치 합니다.

 ![hello "프로세스 서버 추가" 창](./media/site-recovery-failback-azure-to-vmware-classic/add-classic.png)

 Hello 프로세스 서버를 만들 때는 주의 기울여야 toohello 다음 비용을 지불 합니다.
 * hello hello 이미지 이름이 *Microsoft Azure 사이트 복구 프로세스 서버 V2*합니다. 선택 **클래식** hello 배포 모델입니다.

       ![Select "Classic" as hello Process Server deployment model](./media/site-recovery-failback-azure-to-vmware-classic/templatename.png)
 * 설치에 hello 프로세스 서버에 따라 toohello 지침 [복제 VMware 가상 컴퓨터 및 Azure 사이트 복구와 실제 서버 tooAzure](site-recovery-vmware-to-azure-classic.md)합니다.
7. Hello를 선택 하는 경우 *리소스 관리자* Azure 네트워크, hello 다음 정보를 제공 하 여 hello 프로세스 서버를 배포 합니다.

  * hello toodeploy hello 서버를 원하는 hello 리소스 그룹 이름
  * hello 서버 hello 이름
  * 사용자 이름 및 로그인 toohello 서버에 사용할 암호
  * toodeploy hello 서버를 원하는 hello 저장소 계정
  * hello 서브넷과 tooconnect tooit 원하는 hello 네트워크 인터페이스
   >[!NOTE]
   >직접 만들 해야 [네트워크 인터페이스](../virtual-network/virtual-networks-multiple-nics.md) (NIC) hello 프로세스 서버를 배포 하는 동안 선택 합니다.

    ![Hello "프로세스 서버 추가" 대화 상자에서 정보를 입력 합니다.](./media/site-recovery-failback-azure-to-vmware-classic/psinputsadd.png)

8. **확인**을 클릭합니다. 이 작업을 hello 프로세스 서버 설치 하는 동안 리소스 관리자 배포 유형을 가상 컴퓨터를 만드는 작업을 트리거합니다. tooregister hello 서버 toohello 구성 서버를 내부의 실행된 hello 설치 hello 지침에 따라 VM hello [복제 VMware 가상 컴퓨터 및 Azure 사이트 복구와 실제 서버 tooAzure](site-recovery-vmware-to-azure-classic.md)합니다. 작업 toodeploy hello 프로세스 서버도 트리거됩니다.

  hello 프로세스 서버에 나열 되어 hello **구성 서버** > **서버 관련** > **프로세스 서버** 탭 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware-new/pslistingincs.png)

    > [!NOTE]
    > hello 프로세스 서버 표시 되지 않으면 아래 **VM 속성**합니다. Hello에만 표시 되 고 **서버** hello 관리 서버에 등록 된 탭입니다. 프로세스 서버 tooappear hello에 대 한 10 too15 분 걸릴 수 있습니다.


## <a name="set-up-hello-master-target-server-on-premises"></a>Hello 마스터 대상 서버 온-프레미스 설정
마스터 대상 서버 hello hello 장애 복구 데이터를 받습니다. hello 서버는 hello 온-프레미스 관리 서버에 자동으로 설치 됩니다. 하지만 너무 많은 데이터 다시 실패 하는, tooset 추가 마스터 대상 서버를 할 수 있습니다. tooset를 마스터 대상 서버 온-프레미스, 다음 hello지 않습니다.

> [!NOTE]
> linux 마스터 대상 서버를 tooset toohello 다음 절차를 건너뜁니다. 마스터 대상 OS hello 대로 CentOS 6.6 최소 운영 체제를 사용 합니다.

1. Windows hello 마스터 대상 서버를 설정 하는 경우 hello에 hello 마스터 대상 서버를 설치 하는 VM에서 hello 빠른 시작 페이지를 엽니다.
2. Hello Azure Site Recovery 통합 설치 마법사에 대 한 hello 설치 파일을 다운로드 합니다.
3. Hello 설치 프로그램을 실행 및에 **시작 하기 전에**선택, **배포 아웃 추가 프로세스 서버 tooscale 추가**합니다.
4. Hello에서 마법사를 완료 하는 hello 때 수행한 동일한 방식으로 있습니다 [hello 관리 서버 설정](site-recovery-vmware-to-azure-classic.md)합니다. Hello에 **구성 서버 세부 정보** 페이지 hello 마스터 대상 서버의 hello IP 주소를 지정 하 고 암호 tooaccess hello VM을 입력 합니다.

### <a name="set-up-a-linux-vm-as-hello-master-target-server"></a>Linux VM hello 마스터 대상 서버로 설정
Linux VM으로 hello 마스터 대상 서버를 실행 하는 hello 관리 서버를 tooset hello CentOS 6.6 최소 운영 체제를 설치 합니다. 다음으로, 각 SCSI 하드 디스크에 대 한 hello SCSI Id를 검색할 몇 가지 추가 패키지를 설치 하 고 일부 사용자 지정 변경 내용을 적용 합니다.

#### <a name="install-centos-66"></a>CentOS 6.6 설치

1. Hello 관리 서버의 VM hello CentOS 6.6 최소 운영 체제를 설치 합니다. DVD 드라이브에 ISO hello를 유지 하 고 hello 시스템 부팅 합니다. Hello 미디어 테스트를 건너뜁니다. 선택 **영어 (미국)** hello 언어로 선택 **기본 저장 장치**, 중요 한 데이터가 없는 경우 하드 드라이브 hello 확인을 클릭 **예**, 모든 데이터는 무시 합니다. Hello 관리 서버의 hello 호스트 이름을 입력 하 고 hello 서버 네트워크 어댑터를 선택 합니다.  Hello에 **편집 시스템** 대화 상자에서 **자동으로 연결**를 추가한 다음 정적 IP 주소, 네트워크 및 DNS 설정을 추가 합니다. 표준 시간대를 지정합니다. tooaccess hello 관리 서버 hello 루트 암호를 입력 합니다.
2. 원하는 설치의 유형을 묻는 경우 선택 **사용자 지정 레이아웃 만들기** hello 파티션으로 합니다. **다음**을 누릅니다. **무료**를 선택하고 **만들기**를 클릭합니다. **FS 유형:** **ext4**를 사용하여 **/**,  **/var/crash** 및 **/home partitions**를 만듭니다. Hello 스왑 파티션으로 만들 **FS 유형: 스왑**합니다.
3. 기존 장치가 발견되면 경고 메시지가 표시됩니다. 클릭 **형식** tooformat hello 드라이브로 hello 파티션 설정 합니다. 클릭 **쓰기 변경 toodisk** tooapply hello 파티션 변경 합니다.
4. 선택 **부팅 로더가 설치** > **다음** hello 루트 파티션에 tooinstall hello 부트 로더 합니다.
5. Hello 설치가 완료 되 면 클릭 **재부팅**합니다.

#### <a name="retrieve-hello-scsi-ids"></a>Hello SCSI Id 검색

1. Hello 설치 후 hello VM에서에서 각 SCSI 하드 디스크에 대 한 hello SCSI Id를 검색 합니다. 따라서 toodo hello 관리 서버 VM 종료 합니다. VMware에서 VM 속성 hello hello VM 항목 마우스 오른쪽 단추로 클릭 > **설정 편집** > **옵션**합니다.
2. **고급** > **일반 항목**을 선택한 다음 **구성 매개 변수**를 클릭합니다. Hello 컴퓨터가 실행 중일 때에이 옵션은 사용할 수 없습니다. Hello 옵션 toobe를 사용할 수 있는에 대 한 hello 컴퓨터를 종료 해야 합니다.
3. Hello 다음 중 하나를 수행 합니다.
 * 행 경우 hello **디스크. EnableUUID** 있는 hello 값 너무 설정 되어 있는지 확인**True** (대/소문자 구분). Hello 값 tooTrue 이미 설정 되어 있는 경우 취소 하 고 부팅 된 후 게스트 운영 체제 내의 hello SCSI 명령을 테스트할 수 있습니다.
 * 행 경우 hello **디스크. EnableUUID** 존재를 클릭 하지 **행 추가**, 다음 hello로 추가 **True** 값입니다. 큰따옴표는 사용하지 마세요.

#### <a name="install-additional-packages"></a>추가 패키지 설치
추가 패키지를 다운로드하여 설치합니다.

1. Hello 마스터 대상 서버에 연결 된 toohello 인터넷 인지 확인 합니다.
2. 이 명령을 실행 하는 hello CentOS 리포지토리에서 15 패키지를 설치 및 toodownload: `# yum install –y xfsprogs perl lsscsi rsync wget kexec-tools`합니다.
3. 보호 하려는 hello 원본 컴퓨터 Linux는 Reiser를 실행 하는 또는 XFS hello 루트 또는 부팅 장치에 대 한 시스템 파일을 다운로드 하 고 다음과 같이 추가 패키지 설치:

   * \# cd /usr/local
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm)
   * \# wget [http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm](http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm)
   * \# rpm –ivh kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm
   * \# wget [http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm](http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_65.rpm)
   * \# rpm –ivh xfsprogs-3.1.1-16.el6.x86_64.rpm
   * \#yum 장치-매퍼-다중 경로 (hello 마스터 대상 서버에 있는 필수 tooenable 다중 경로 패키지)를 설치 합니다.

#### <a name="apply-custom-changes"></a>사용자 지정 변경 내용 적용
설치 된 hello 패키지 및 hello 사후 설치 단계를 완료 한 후 hello 다음을 수행 하 여 사용자 지정 변경 내용을 적용 합니다.

1. Hello RHEL 6 64 통합 에이전트 이진 toohello VM을 복사 합니다. toountar hello 이진이 명령을 실행: `tar –zxvf <file name>`합니다.
2. 이 명령을 실행 하는 toogive 사용 권한: `# chmod 755 ./ApplyCustomChanges.sh`합니다.
3. 실행 hello 스크립트 다음: `# ./ApplyCustomChanges.sh`합니다. 한 번만 실행합니다. 성공적으로 실행 된 후 hello 서버를 다시 부팅 합니다.

## <a name="run-hello-failback"></a>Hello 장애 복구를 실행 합니다.
### <a name="reprotect-hello-azure-vms"></a>Hello Azure Vm을 다시 보호
1. **자격 증명 모음**에 **복제 항목**를 hello 장애 조치 된 VM을 마우스 오른쪽 단추로 클릭 한 다음 선택 **다시 보호**합니다.
2. Hello 블레이드에서 해당 hello 방향 보호를 확인할 수 있습니다 **Azure tooOn 프레미스** 이미 선택 되어 있습니다.
3. **마스터 대상 서버** 및 **프로세스 서버**hello 프로세스 서버로 Azure VM을 hello 온-프레미스 마스터 대상 서버를 선택 합니다.
4. 원하는 toorecover hello 디스크 선택 hello 데이터 저장소 온-프레미스에 있습니다. 이 옵션을 사용 하 여 때 hello 온-프레미스 VM 삭제 되 고 toocreate 새 디스크가 필요 합니다. Hello 디스크가 이미 존재 하지만 계속 toospecify 값을 사용 해야 하는 경우 hello 옵션을 무시 합니다.
5. 보존 드라이브 toostop hello 포인트를 사용 하 여 hello VM 복제 백 tooon 온-프레미스 시간. 여기서는 보존 드라이브에 대한 몇 가지 기준을 나열합니다. 이러한 기준 없이 hello 드라이브 hello 마스터 대상 서버에 대 한 나열 되지 않습니다.

  * 볼륨은 다른 용도(복제의 대상 등)로 사용되지 않아야 합니다.
  * 볼륨은 잠금 모드가 아니어야 합니다.
  * 볼륨은 캐시 볼륨이 아니어야 합니다. (hello 마스터 대상 설치 볼륨에 있는 존재 하지 않아야 합니다. 프로세스 서버와 마스터 hello 대상 볼륨을 사용자 지정 설치는 보존 볼륨으로 적합 합니다. 여기에서 프로세스 서버를 설치 하는 hello 및 마스터 대상 볼륨은 hello 마스터 대상 캐시 볼륨 hello.)
  * FAT 및 FAT32 볼륨 파일 시스템 형식을 hello이 아니어야 합니다.
  * hello 볼륨 용량은 0이 아닌 값 이어야 합니다.
  * Windows 용 hello 기본 보존 볼륨은 R 볼륨.
  * Linux 용 hello 기본 보존 볼륨 /mnt/retention입니다.

6. hello 장애 복구 정책은 자동으로 선택 됩니다.
7. 클릭 한 후 **확인** toobegin 다시 보호 작업 tooreplicate hello Azure toohello 온-프레미스 사이트에서 VM을 시작 합니다. Hello에 hello 진행률을 추적할 수 **작업** 탭 합니다.

Toorecover tooan 대체 위치를 원하는 경우 hello 보존 드라이브 및 hello 마스터 대상 서버에 대해 구성 된 데이터 저장소를 선택 합니다. VMware Vm hello 장애 복구 보호 계획에 hello hello를 사용 하 여 뒤로 toohello 온-프레미스 사이트 실패 하는 경우 hello 마스터 대상 서버와 동일한 데이터 저장소입니다. Toorecover hello 복제본 Azure VM toohello 하려는 경우 동일한 온-프레미스 VM, hello 온-프레미스 VM은 이미 수에 hello 동일 hello 마스터 대상 서버와 데이터 저장소입니다. 온-프레미스에 VM이 없는 경우 다시 보호하는 동안 새 VM이 만들어집니다.

![Hello 드롭 다운 메뉴에서 "Azure tooon 온-프레미스"를 선택 합니다.](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

복구 계획 수준에서 다시 보호할 수도 있습니다. 복제 그룹이 있는 경우 복구 계획을 통해서만 이 복제 그룹을 다시 보호할 수 있습니다. 복구 계획을 사용 하 여 해제 하는 경우 모든 보호 된 컴퓨터에 대 한 hello 이전 값을 사용 합니다.

> [!NOTE]
> Hello로 다시 복제 그룹을 보호 해야 동일한 마스터 대상을 합니다. 다른 마스터 대상 서버를 통해 복제 그룹을 다시 보호하는 경우 이 복제 그룹에 공통된 특정 시점을 결정할 수 없습니다.

### <a name="run-a-failover-toohello-on-premises-site"></a>장애 조치 toohello 온-프레미스 사이트를 실행 합니다.
Hello VM을 다시 보호 한 후에 Azure tooon 온-프레미스에서 장애 조치를 시작할 수 있습니다.

1. Hello 복제 된 항목 페이지에서 hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **계획 되지 않은 장애 조치**합니다.
2. **확인 장애 조치**hello 장애 조치 방향 (Azure)를 확인 한 다음 toouse hello 장애 조치 (최신, hello 또는 hello 최신 응용 프로그램 일치 복구 지점)에 사용할 hello 복구 지점을 선택 합니다. 응용 프로그램 일치 복구 지점 hello 가장 최근 시점 이전 시간 내에 발생 하 고 일부 데이터가 손실 하면 키를 누릅니다.
3. 장애 조치 중 사이트 복구 hello Azure Vm을 종료합니다. 해당 장애 복구 완료 된 예상 대로 확인 한 후에 hello Azure Vm 종료 되었을 예상 대로 tooensure를 확인할 수 있습니다.

### <a name="reprotect-hello-on-premises-site"></a>Hello 온-프레미스 사이트를 다시 보호
장애 복구 완료 된 후 Azure에서 복구 Vm hello 커밋 hello 가상 컴퓨터 tooensure 삭제 됩니다. toodo 따라서 hello 보호 된 항목을 마우스 오른쪽 단추로 클릭 **커밋**합니다. 이 그러면은 Azure의 hello 이전 복구 된 가상 컴퓨터를 제거 하는 작업을 트리거합니다.

Hello 커밋 완료 되 면 데이터 hello 온-프레미스 사이트에 다시 수도 있지만 보호할 수 없습니다. 다시, toostart 복제 tooAzure 다음 hello지 않습니다.

1. **자격 증명 모음**에 **설정** > **복제 항목**, 선택한 다시 실패 하 고 클릭 hello Vm **다시보호**.
2. Hello 사용 toobe toosend 데이터 백 tooAzure 해야 하는 프로세스 서버 hello 값을 제공 합니다.
3. **확인**을 클릭합니다.

Hello 다시 보호 완료 되 면 hello VM 백 tooAzure를 복제 하 고 장애 조치를 수행할 수 있습니다.

### <a name="resolve-common-failback-issues"></a>일반적인 장애 복구 문제 해결
* 읽기 전용 사용자 vCenter 검색을 수행하고 가상 컴퓨터를 보호하면 작업에 성공하고 장애 조치가 작동합니다. 를 다시 보호 하는 동안 장애 조치 hello 데이터 저장소를 검색할 수 없으므로 실패 합니다. 증상으로 hello 데이터 저장소를 다시 보호 하는 동안 나열 표시 되지 않습니다. tooresolve이 문제를 적절 한 권한이 있는 계정으로 hello vCenter 자격 증명을 업데이트 하 고 hello 작업을 다시 시도 하십시오. 자세한 내용은 참조 [복제 VMware 가상 컴퓨터 및 물리적 서버 tooAzure Azure 사이트 복구](site-recovery-vmware-to-azure-classic.md)
* Linux VM 장애 복구 하 고 온-프레미스를 실행 하는 경우 해당 hello 네트워크 관리자 패키지 프로그램이 hello 컴퓨터에서 제거를 볼 수 있습니다. 이 제거 hello 네트워크 관리자 패키지는 Azure의 hello VM가 복구 될 때 제거 되기 때문에 발생 합니다.
* VM 고정 IP 주소로 구성 되어 있고 tooAzure 장애 조치가 시 hello IP 주소는 DHCP를 통해 획득 됩니다. 장애 조치 하면 뒤로 tooon 온-프레미스, VM hello toouse DHCP tooacquire hello IP 주소를 계속 합니다. 수동으로 toohello 컴퓨터에 로그인 하 고 필요한 경우 hello IP 주소 다시 tooa 고정 주소를 설정 합니다.
* ESXi 5.5 무료 버전 또는 vSphere 6 하이퍼바이저 무료 버전을 사용하는 경우 장애 조치는 성공하지만 장애 복구가 실패합니다. 평가판 라이선스로 업그레이드 tooeither 프로그램 tooenable 장애을 복구 합니다.
* Hello 프로세스 서버에서에서 구성 서버 hello을 연결할 수 없는 경우 포트 443에서 텔넷 toohello 구성 서버 컴퓨터에서 연결 toohello 구성 서버를 확인 합니다. Tooping hello 구성 서버 hello 프로세스 서버 컴퓨터에서 사용할 수 있습니다. 프로세스 서버 연결된 toohello 구성 서버의 경우 하트 비트가 있어야 합니다.
* Toofail 백 tooan 대체 vCenter을 시도 하는 경우에 새 사용자 vCenter가 검색 하 고 해당 hello 마스터 대상 서버는 검색도 있는지 확인 합니다. 일반적인 증상은 hello 데이터 저장소 액세스할 수 없거나 hello에 표시 되지 않는다는 **다시 보호** 대화 상자.
* 실제 온-프레미스 컴퓨터에 보호 되는 WS2008R2SP1 컴퓨터 Azure tooon 온-프레미스에서 다시 장애 할 수 없습니다.

## <a name="fail-back-with-expressroute"></a>ExpressRoute로 장애 복구
VPN 연결 또는 Azure ExpressRoute 연결을 통해 장애 복구할 수 있습니다. Toouse ExpressRoute 연결을 사용 하도록 하려는 경우에 hello 다음 note:

* ExpressRoute 연결 hello는 설정 해야 hello hello 원본 컴퓨터가 장애 조치할 tooand Azure 가상 네트워크에 Azure Vm hello 있는 hello 장애 조치 발생 후 합니다.
* 데이터는 복제 된 tooan 공용 끝점에 대 한 Azure 저장소 계정입니다. ExpressRoute 연결 toouse 사이트 복구 복제에 대 한 hello 대상 데이터 센터와 ExpressRoute에서 공용 피어 링 설정 합니다.
