---
title: "aaaFail hello 클래식 레거시 포털에서 Azure에서 VMware Vm을 백업 | Microsoft Docs"
description: "이 문서에서는 toofail 백 된 VMware 가상 컴퓨터를 Azure Site Recovery와 tooAzure를 복제 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a>뒤로 VMware 가상 컴퓨터와 물리적 서버를 Azure Site Recovery (레거시)와 Azure tooVMware 실패
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-failback-azure-to-vmware.md)
> * [Azure 클래식 포털](site-recovery-failback-azure-to-vmware-classic.md)
> * [Azure 클래식 포털(레거시)](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

이 문서에서 설명 하는 방법을 toofail 백 VMware 가상 컴퓨터와 온-프레미스에서 복제 한 후 Azure tooyour 온-프레미스 사이트에서 Windows/Linux 물리적 서버의 사이트 tooAzure를 사용 하 여 [Azure Site Recovery?](site-recovery-overview.md)합니다.

여기서는 이전 구성을 설명하며 새 자격 증명 모음에 사용하면 안 됩니다.

## <a name="architecture"></a>아키텍처
이 다이어그램은 hello 장애 조치 및 장애 복구 시나리오를 나타냅니다. hello 파란색 선은 장애 조치 중 사용 되는 hello 연결입니다. hello 빨간색 선은 장애 복구 중 사용 되는 hello 연결입니다. 화살표가 있는 hello 줄 hello 살펴봅니다 인터넷 합니다.

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a>시작하기 전에
* VMware VM 또는 물리적 서버를 통해 실패해야 하며 Azure에서 실행해야 합니다.
* 뒤로 VMware 가상 컴퓨터와 Windows/Linux 물리적 서버 hello 온-프레미스 기본 사이트에서 Azure tooVMware 가상 컴퓨터를 실패만 할 수 하는 점에 유의 해야 합니다.  물리적 컴퓨터를 다시 실패 하는, 장애 조치 tooAzure 변환 tooan Azure VM 및 장애 복구 tooVMware tooa VMware VM 변환 됩니다.

장애 복구를 설정하는 방법은 다음과 같습니다.

1. **장애 복구 구성 요소를 설정**: tooset vContinuum 서버를 필요한 온-프레미스, Azure에서 VM toohello 구성 서버를 가리키도록 합니다. 또한 Azure VM toosend 데이터 백 toohello 온-프레미스 마스터 대상 서버와 프로세스 서버를 설정 합니다. Hello 장애 조치를 처리 하는 hello 구성 서버와 hello 프로세스 서버를 등록 합니다. 온-프레미스 마스터 대상 서버를 설치합니다. Windows 마스터 대상 서버가 필요한 경우 vContinuum을 설치하면 자동으로 설정됩니다. Tooset 해야 Linux 해야 할 경우 별도 서버에서 수동으로 해당 작업을 합니다.
2. **보호 및 장애 복구를 사용 하도록 설정**: hello 구성 요소를 설정한 후 vContinuum 해야 tooenable 보호 장애 조치 Azure Vm에 대 한 합니다. Hello Vm에 준비 검사를 실행 하 고 Azure tooyour 온-프레미스 사이트에서 장애 조치를 실행 합니다. 장애 복구 완료 된 후 복제 tooAzure 시작 되도록 온-프레미스 컴퓨터 해제 합니다.

## <a name="step-1-install-vcontinuum-on-premises"></a>1단계: 온-프레미스에 vContinuum 설치
Tooinstall vContinuum 서버 온-프레미스 필요 하 고 toohello 구성 서버를 가리키도록 합니다.

1. [VContinuum을 다운로드합니다](http://go.microsoft.com/fwlink/?linkid=526305).
2. 다음 다운로드 hello [vContinuum 업데이트](http://go.microsoft.com/fwlink/?LinkID=533813) 버전입니다.
3. Hello vContinuum의 최신 버전을 설치 합니다. Hello에 **시작** 페이지 **다음**합니다.
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. Hello hello 마법사의 첫 번째 페이지에서 hello CX 서버 IP 주소 및 hello CX 서버 포트를 지정 합니다. **HTTPS 사용**을 선택합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. Hello에 hello 구성 서버 IP 주소를 찾고 **대시보드** hello 구성 서버에서 Azure VM의 탭 합니다.
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. HTTPS hello 구성 서버 hello에 공용 포트를 찾을 **끝점** hello 구성 서버에서 Azure VM의 탭 합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. Hello에 **CS 암호 세부 정보** 페이지 hello 구성 서버를 등록 하는 경우 아래로 명시 hello 암호를 지정 합니다. 기억 하지 못하는 것 체크 인 **c:\\Program Files (x86)\\InMage 시스템\\개인\\connection.passphrase** hello 구성 서버 VM에 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. Hello에 **대상 위치 선택** 페이지 지정 tooinstall hello vContinuum 서버 하 고 클릭 **설치**합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. 설치가 완료되면 vContinuum을 시작할 수 있습니다.
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a>2단계: Azure에 프로세스 서버 설치
Azure의 hello Vm hello 데이터 백 tooan 온-프레미스 마스터 대상 서버에 보낼 수 있도록 Azure에 프로세스 서버 tooinstall을 해야 합니다.

1. Hello에 **구성 서버** 새 프로세스 서버를 azure에서 선택 tooadd 페이지.

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. 관리자 권한으로 프로세스 서버 이름 및 이름 및 암호 tooconnect toohello 가상 컴퓨터를 지정 합니다. Hello 구성 서버 toowhich tooregister hello 프로세스 서버를 선택 합니다. Hello 해야 동일한 서버 tooprotect 사용 중이 고 가상 컴퓨터를 장애 조치 합니다.
3. Azure hello 지정 네트워크에 있는 hello에 프로세스 서버 배포 해야 합니다. 동일한 hello 것 hello 구성 서버와 네트워크입니다. 선택한 서브넷에서 고유한 IP 주소를 지정하고 배포를 시작합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. 작업은 트리거된 toodeploy hello 프로세스 서버.

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. Azure의 hello 프로세스 서버를 배포한 후 지정한 hello 자격 증명을 사용 하 여 hello 서버에 로그인 할 수 있습니다. Hello 프로세스 서버를 등록 hello에 hello를 등록 하는 동일한 방식으로 온-프레미스 프로세스 서버입니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> 장애 복구 하는 동안 등록 된 hello 서버는 사이트 복구에서 VM 속성에서 표시 되지 않습니다. Hello 아래에 표시 된다는 **서버** 을 등록 하는 hello 구성 서버 toowhich 탭 합니다. 약 10-15 분 프로세스를 hello 될 때까지 걸리는 서버 hello 탭에 나타납니다.
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a>3단계: 온-프레미스에 마스터 대상 서버 설치
원본 가상 컴퓨터 운영 체제에 따라 해야 tooinstall는 Linux 또는 Windows 마스터 대상 서버 온-프레미스 합니다.

### <a name="deploy-a-windows-master-target-server"></a>Windows 마스터 대상 서버 배포
Windows 마스터 대상은 이미 vContinuum 설정에 포함되어 있습니다. 마스터 서버 hello에도 배포 된 hello vContinuum를 설치한 경우 동일한 컴퓨터와 구성 서버가 등록 된 toohello 합니다.

1. toobegin 배포는 빈 만들 온-프레미스 toorecover hello Azure에서 Vm에 원하는 hello ESX 호스트의 컴퓨터.
2. 두 개 이상의 디스크가 연결 toohello VM – 하나 hello 운영 체제에 사용 되는 다른 hello hello 보존 드라이브에 사용 되 확인 하십시오.
3. Hello 운영 체제를 설치 합니다.
4. Hello vContinuum hello 서버에 설치 합니다. 이 또한 hello 마스터 대상 서버 설치를 완료 합니다.

### <a name="deploy-a-linux-master-target-server"></a>Linux 마스터 대상 서버 배포
1. toobegin 배포는 빈 만들 온-프레미스 toorecover hello Azure에서 Vm에 원하는 hello ESX 호스트의 컴퓨터.
2. 두 개 이상의 디스크가 연결 toohello VM – 하나 hello 운영 체제에 사용 되는 다른 hello hello 보존 드라이브에 사용 되 확인 하십시오.
3. Hello Linux 운영 체제를 설치 합니다. Linux 마스터 대상 시스템 hello 루트 또는 보존 저장소 공간에 대 한 LVM를 사용 해야 합니다. Linux 마스터 대상 서버를 사용 하는 기본적으로 tooavoid LVM 파티션/디스크가 검색을 구성 합니다.
4. 만들 수 있는 파티션은 다음과 같습니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. Hello 마스터 대상 설치를 시작 하기 전에 hello 아래 사후 설치 단계를 수행 합니다.

#### <a name="post-os-installation-steps"></a>사후 OS 설치 단계
각 Linux 가상 컴퓨터에서 SCSI 하드 디스크에 대 한 tooget hello SCSI ID hello 매개 변수 "디스크를 사용 하도록 설정 EnableUUID = TRUE "다음과 같습니다.

1. 가상 컴퓨터를 종료합니다.
2. Hello 왼쪽 패널에서 hello VM 항목을 마우스 오른쪽 단추로 클릭 > **설정 편집**합니다.
3. Hello 클릭 **옵션** 탭 합니다. **고급\>일반 항목** > **구성 매개 변수**를 선택합니다. hello **구성 매개 변수** hello 컴퓨터 종료 될 때이 옵션은 사용할 수만 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. **disk.EnableUUID** 가 있는 행이 존재하는지 확인합니다. 너무 설정 된 경우**False** 너무 설정한 다음**True** (하지 대/소문자 구분). 경우 존재 하며 tootrue 설정를 클릭 **취소** 및가 부팅한 후 hello 게스트 운영 체제 내의 hello SCSI 명령을 테스트 합니다. 존재하지 않는 경우 **행 추가**를 클릭합니다.
5. 디스크를 추가 합니다. Hello에 EnableUUID **이름** 열입니다. 해당 값을 TRUE로 설정합니다. 큰따옴표로 함께 값 위에 hello를 추가 하지 마십시오.

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a>다운로드 하 여 hello 추가 패키지 설치
참고: hello 시스템에 다운로드 하 고 hello 추가 패키지를 설치 하기 전에 인터넷 연결이 있는지 확인 합니다.

\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools

이 명령은 CentOS 6.6 저장소에서 이러한 15개의 패키지를 다운로드 및 설치:

bc-1.06.95-1.el6.x86\_64.rpm

busybox-1.15.1-20.el6.x86\_64.rpm

elfutils-libs-0.158-3.2.el6.x86\_64.rpm

kexec-tools-2.0.0-280.el6.x86\_64.rpm

lsscsi-0.23-2.el6.x86\_64.rpm

lzo-2.03-3.1.el6\_5.1.x86\_64.rpm

perl-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm

perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm

perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm

perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm

perl-version-0.77-136.el6\_6.1.x86\_64.rpm

rsync-3.0.6-12.el6.x86\_64.rpm

snappy-1.1.0-1.el6.x86\_64.rpm

wget-1.12-5.el6\_6.1.x86\_64.rpm

이전 tooprotection을 대상으로 hello 원본 컴퓨터가 사용 하는 경우 Reiser 또는 XFS filesystem hello 루트 또는 부팅 장치에 대 한 다음 패키지를 다운로드 하 고 Linux 마스터에 설치 해야 합니다.

\# cd /usr/local

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm>

\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm>

\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm

\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm>

\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm

#### <a name="apply-custom-configuration-changes"></a>사용자 지정 구성 변경 내용 적용
이러한 변경 내용을 적용 하기 전에 hello 이전 단원을 완료 한 후 다음이 단계를 수행 했는지 확인 합니다.

1. 운영 체제를 새로 만든 hello RHEL 6 64 통합 에이전트 이진 toohello를 복사 합니다.
2. 이 명령은 toountar hello 이진 실행: **tar-zxvf \<파일 이름\>**
3. 실행이 명령 toogive 권한을: \# **chmod 755./ApplyCustomChanges.sh**
4. Hello 스크립트 실행:  **\# ./ApplyCustomChanges.sh**합니다. Hello 서버의 hello 스크립트를 한 번만 실행 됩니다. Hello 스크립트를 실행 한 후 hello 서버를 다시 시작 합니다.

### <a name="install-hello-linux-server"></a>Hello Linux 서버 설치
1. [다운로드](http://go.microsoft.com/fwlink/?LinkID=529757) hello 설치 파일입니다.
2. Hello 파일 toohello sftp 클라이언트 유틸리티를 사용 하 여를 사용 하 여 Linux 마스터 대상 가상 컴퓨터를 복사 합니다. Hello Linux 마스터 대상 가상 컴퓨터에 로그온 하 고 제공된 된 링크에서 wget toodownload hello 설치 패키지를 사용할 수 또는
3. Hello Linux 마스터 대상 가상 컴퓨터 사용 하 여 서버에 로그온 된 ssh 사용자가 선택한 클라이언트
4. 연결 되어 있는 경우 Azure toohello입니다 VPN 연결을 통해 Linux 마스터 대상 서버를 배포 하면 다음이 가상 컴퓨터에서 찾을 수 있는 hello 서버에 대 한 내부 IP 주소를 사용 하 여 네트워크 **대시보드** 탭 및 포트 22 tooconnect toohello Linux 마스터 대상 서버 보안 셸을 사용 하 여 합니다.
5. 공용 인터넷 연결을 통해 toohello Linux 마스터 대상 서버 hello Linux 마스터 대상 서버 공용 가상 IP 주소를 사용 하 여 연결 하는 경우 (hello 가상 컴퓨터에서 **대시보드** 탭) 공용 끝점 hello 및 생성에 대 한 ssh toologin toohello Linux servder.
6. Hello 파일을 실행 하 여 hello gzipped Linux 마스터 대상 서버 설치 관리자 tar 보관 파일에서 추출: *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64"* hello 디렉터리에서 하는 hello 설치 관리자 파일을 포함합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. 하면 추출 된 hello 설치 관리자 파일 tooa 다른 디렉터리를 변경 하는 경우 hello tar 보관의 toohello 디렉터리 toowhich hello 내용은 추출 되었습니다. 이 디렉터리 경로에서 “sudo ./install.sh”를 실행합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. 메시지 표시 toochoose 주 역할을 선택 하는 경우 **2 (마스터 대상)**합니다. 기본값으로 hello 다른 대화형 설치 옵션을 유지 합니다.
9. 설치 toocontinue 및 hello 호스트 구성 인터페이스 tooappear 될 때까지 기다립니다. hello hello Linux 마스터 대상 서버에 대 한 호스트 구성 유틸리티는 명령줄 유틸리티입니다. 하지 않는 창 크기를 조정 hello ssh 클라이언트 유틸리티. 사용 하 여 hello 화살표 키 tooselect hello **Global** 옵션 및 키를 눌러 키보드에서 입력 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. Hello 필드에 **IP** hello 구성 서버 hello 내부 IP 주소를 입력 (hello에서 찾을 수 있습니다 **대시보드** hello 구성 서버 VM의 탭) ENTER 키를 누릅니다. **포트**에 **22**를 입력하고 ENTER 키를 누릅니다.
11. **HTTPS 사용**을 **예**로 두고 ENTER 키를 누릅니다.
12. Hello hello 구성 서버에서 생성 된 암호를 입력 합니다. PUTTY 클라이언트가 Windows 컴퓨터 toossh toohello Linux 가상 컴퓨터에서 사용 하 여 hello 클립보드 내용의 toopaste hello Shift + Insert를 사용할 수 있습니다. Hello 암호 toohello 로컬 클립보드 Ctrl + C를 사용 하 여 복사 하 고 Shift + Insert toopaste를 사용할 것입니다. ENTER 키를 누릅니다.
13. 오른쪽 화살표 키 toonavigate tooquit hello를 사용 하 고 ENTER 키를 누릅니다. 설치 toocomplete 될 때까지 기다립니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

어떤 이유로 tooregister 장애 경우 Linux 마스터 대상 서버 toohello 구성 서버 할 수 있는 다시 (먼저 필요 함 tooset 액세스 권한을 toothis /usr/local/ASR/Vx/bin/hostconfigcli에서 호스트 구성 유틸리티를 실행 하 여 디렉터리 chmod을 슈퍼 사용자로 실행 하 여).

#### <a name="validate-master-target-registration"></a>마스터 대상 등록의 유효성 검사
해당 hello를 확인할 수 있습니다. 마스터 대상 서버가 성공적으로 등록 되었습니다. Azure Site Recovery 자격 증명 모음에 구성 서버 toohello > **구성 서버** > **서버 세부 정보**합니다.

> [!NOTE]
> 이 마스터 대상 구성이 감지 되지 않지만 hello 때문 hello 마스터 대상 서버를 등록 하 여 가상 컴퓨터를 hello 구성 오류가 발생 하면 삭제 된 Azure에서 또는 끝점이 제대로 구성 되지 않은 후 hello Azure dndpoints 하 여 hello 마스터 대상 Azure에 배포 되 면이 제한이 적용 되지 않습니다는 온-프레미스 마스터 대상 서버 온-프레미스에 대 한 합니다. 장애 복구에 영향을 주지 않으며 이러한 오류는 무시할 수 있습니다.
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a>4 단계: hello 가상 컴퓨터 toohello 온-프레미스 사이트를 보호 합니다.
장애 복구 전에 tooprotect Vm toohello 온-프레미스 사이트를 해야 합니다.

### <a name="before-you-begin"></a>시작하기 전에
VM이 장애 조치 되 tooAzure 하려면 추가 임시 드라이브 페이지 파일에 추가 됩니다. 이것은 이미 페이지 파일 전용 드라이브를 가지고 있을 수도 있으므로 일반적으로 장애 조치된 VM에서 필요로 하지 않는 추가 드라이브입니다. 역방향 hello 가상 컴퓨터 보호를 시작 하기 전에 보호 되지 않는 것이 드라이브는 오프 라인을 확인 해야 합니다. 다음과 같이 수행합니다.

1. 컴퓨터 관리를 열고 hello 디스크가 온라인 상태이 고 연결 된 toohello 컴퓨터 나열 되도록 저장소 관리를 선택 합니다.
2. Hello 임시 디스크 toohello 연결 된 컴퓨터를 선택 하 고 선택 toobring 오프 합니다.

### <a name="protect-hello-vms"></a>Hello Vm 보호
1. Hello Azure 포털에서에서 이러한 장애 조치 하는 hello 가상 컴퓨터 tooensure hello 상태를 검사 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. 컴퓨터에 vContinuum을 시작합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. 클릭 **새 보호 그룹** hello 작업 시스템 유형을 선택 하 고는
4. Hello 선택 hello를 여는 새 창에서 **OS 유형이** > **자세한 정보 얻기** 원하는 toofail 다시 hello Vm에 대 한 합니다. **주 서버 세부 정보**, 식별 하 고 선택 hello tooprotect 가상 컴퓨터. Vm 장애 조치 전에 있었던 hello vCenter 호스트 이름 아래에 나열 됩니다.
5. 가상 컴퓨터 tooprotect 선택 (및 그 이미 장애 조치를 취한 tooAzure) 하는 경우 팝업 창이 hello 가상 컴퓨터에 대 한 두 개의 항목을 제공 합니다. Hello 구성 서버 hello 등록 하는 가상 컴퓨터 tooit의 두 인스턴스를 검색 하는 때문입니다. Hello 온-프레미스 VM 보호할 수 있도록 hello 올바른 VM tooremove hello 항목이 필요 합니다. tooidentify hello 올바른 Azure VM 항목 여기을 hello Azure VM 및 이동 tooC:\Program 파일 (x86) \Microsoft Azure Site Recovery\Application Data\etc에 로그인 할 수 있습니다. Hello 파일 drscout.conf 식별 hello 호스트 id입니다. Hello vContinuum 대화 상자에서 VM hello hello 호스트 ID를 발견 하면를 hello 항목을 유지 합니다. 다른 모든 항목을 삭제합니다. tooselect hello 해결 VM tooits IP 주소를 참조할 수 있습니다. hello IP 주소 범위 온-프레미스는 온-프레미스 VM hello 됩니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. Hello vCenter server에서 hello 가상 컴퓨터를 중지 합니다. Hello Vm 온-프레미스를 삭제할 수 있습니다.
7. Hello 온-프레미스 MT 서버 toowhich tooprotect hello Vm 원하는 지정 합니다. toodo이 toohello vCenter 서버 toowhich 원하는 toofail 다시 연결 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. 마스터 대상 서버 선택 hello hello 호스트 toowhich에 따라 원하는 toorecover hello VM입니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. 각 hello 가상 컴퓨터에 대 한 hello 복제 옵션을 제공 합니다. toodo tooselect hello 복구 쪽 데이터 저장소가 toowhich hello Vm 복구 될 것이 필요 합니다. hello 표에서 tooprovide 각 VM에 필요한 hello 다양 한 옵션을 요약 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | **옵션** | **옵션이 권장하는 값** |
   | --- | --- |
   |  프로세스 서버 IP 주소 |Azure에 배포 된 hello 프로세스 서버 선택 |
   |  보존 크기(MB) | |
   |  보존 값 |1 |
   |  날짜/시간 |일 |
   |  일관성 간격 |1 |
   |  대상 데이터 저장소를 선택합니다. |안녕 hello 복구 사이트에서 사용할 수 있는 데이터 저장소. hello 데이터 저장소 공간이 충분 하 고 사용 가능한 toohello ESX 호스트 toorestore hello 가상 컴퓨터를 원하는 수 해야 합니다. |
10. 가 tooon 온-프레미스 사이트 장애 조치 후 가상 컴퓨터를 hello 속성을 설정 하는 hello를 구성 합니다. hello 속성은 다음 표에 hello에 요약 되어 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | **속성** | **세부 정보** |
    | --- | --- |
    | 네트워크 구성 |검색 각 네트워크 어댑터를 선택 하 고 클릭 **변경** hello 가상 컴퓨터에 대 한 tooconfigure hello 장애 복구 IP 주소입니다. |
    | 하드웨어 구성 |Hello CPU 및 hello VM에 대 한 hello 메모리를 지정 합니다. 설정이 적용된 tooall hello tooprotect 고치려는 Vm 수 있습니다. tooidentify hello hello CPU 및 메모리에 대 한 올바른 값, toohello IAAS Vm 역할 크기를 참조 하 고 hello 코어 수와 할당 된 메모리를 확인할 수 있습니다. |
    | 표시 이름 |장애 복구 tooon 프레미스 후 hello vCenter 재고 표시 hello 가상 컴퓨터를 바꿀 수 있습니다. hello 기본 이름은 hello 가상 컴퓨터 컴퓨터 호스트 이름이입니다. tooidentify hello VM 이름 hello 보호 그룹의 VM 목록 toohello 참조할 수 있습니다. |
    | NAT 구성 |아래에 자세히 설명합니다. |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a>NAT 설정 구성
1. hello 가상 컴퓨터의 보호 tooenable, 두 개의 통신 채널이 설정 toobe가 필요 합니다. 첫 번째 채널 hello hello 가상 컴퓨터 사이 hello 프로세스 서버입니다. 이 채널 hello VM에서에서 hello 데이터를 수집 하 고 있는 다음 보내는 데이터 toohello 마스터 대상 서버 hello toohello 프로세스 서버 보냅니다. Hello 프로세스 서버와 보호 된 hello 가상 컴퓨터 toobe hello에 있는 경우 동일한 Azure 가상 네트워크 하면 toouse NAT 설정이 필요 하지 않습니다. 그렇지 않으면 NAT 설정을 지정합니다. Azure의 hello 프로세스 서버 hello 공용 IP 주소를 봅니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. hello 프로세스 서버와 마스터 대상 서버 hello hello 두 번째 채널은입니다. 옵션 toouse NAT hello 또는 기반 VPN 연결을 사용 하 여 또는 hello를 통해 통신 하는지 여부에 따라 결정 인터넷 합니다. VPN을 사용하는 경우 NAt를 선택하지 마십시오. 인터넷 연결을 사용하는 경우만 선택합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. 지정 된 대로 hello 온-프레미스 가상 컴퓨터를 삭제 하지 않은 및 있다면 hello 데이터 저장소 실패 백 toostill hello 이전 VMDK tooensure 해야 해당 hello 장애 복구 VM 가져옵니다 생성 새 위치에. toodo 선택이 hello **고급** 설정 하 고 대체 폴더 toorestore tooin 지정 **폴더 이름이 설정**합니다. 다른 옵션 기본 설정으로 hello를 둡니다. Hello 폴더 이름 설정 tooall hello 서버에 적용 됩니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. 준비 확인을 실행할 hello 가상 컴퓨터가 준비 toobe 있는지 tooensure 백 tooon 온-프레미스를 보호 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. 될 때까지 기다렸다가 toocomplete 합니다. 모든 Vm에 성공적으로 있으면 hello 보호 계획에 대 한 이름을 지정할 수 있습니다. 클릭 **보호** toobegin 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. vContinuum에서 진행률을 모니터링할 수 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. Hello 단계를 수행한 후 **보호 계획을 활성화** 완료 hello Site Recovery 포털에서 VM 보호를 모니터링할 수 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. Hello VM에서을 클릭 하 고 진행 상황을 모니터링 hello 정확한 상태를 볼 수 있습니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a>Hello 장애 복구 계획 준비
Hello 응용 프로그램 실패 한 뒤로 toohello 온-프레미스 사이트를 언제 든 지 있을 수 있도록 vContinuum를 사용 하 여 장애 복구 계획을 준비할 수 있습니다. 이러한 복구 계획은 사이트 복구에서 매우 유사한 toohello 복구 계획입니다.

1. vContinuum을 시작하고 **계획 관리** > **복구**를 선택합니다. Vm 동안 사용 되는 toofail 된 모든 hello 계획의 목록을 볼 수 있습니다. Hello를 사용할 수 있습니다 toorecover 계획 동일 합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. Hello 보호 계획 및 모든 hello toorecover에 Vm 선택 합니다. 각 VM을 선택 하면 hello 대상 ESX 서버와 hello 원본 VM 디스크를 포함 한 자세한 정보를 볼 수 있습니다. 클릭 **다음** toobegin 복구 마법사 hello 및 toorecover 원하는 hello Vm을 선택 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. 여러 옵션에 따라 복구할 수는 있지만 사용 하는 것이 좋습니다 **최신 태그** 선택 **모든 Vm에 대 한 적용** hello 가상 컴퓨터에서 최신 데이터를 hello tooensure 사용 됩니다.
4. Hello 실행 **준비 상태를 확인 합니다.** Hello 오른쪽 매개 변수는 구성 된 tooenable VM 복구 하는 경우 체크 인 됩니다. 클릭 **다음** if 모든 hello 검사가 성공 합니다. 그렇지 않은 경우 hello 로그를 확인 하 고 hello 오류를 해결 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. **VM 구성** hello 복구 설정을 올바르게 설정 되어 있는지 확인 합니다. 해야 할 경우 hello VM 설정은 변경할 수 있습니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. 복구 하 고 복구 순서를 지정 하는 가상 컴퓨터의 hello 목록을 검토 합니다. 참고 hello 컴퓨터 호스트 이름을 사용 하 여 Vm을 나열 됩니다. 어려운 toomap hello 컴퓨터 호스트 이름 toohello 가상 컴퓨터 수 있습니다.
   toomap hello 이름, 가상 컴퓨터 이동 toohello **대시보드** hello VM 호스트 이름이 Azure와 검사 합니다.

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. 계획 이름을 지정하고 **나중에 복구**를 선택합니다. 권장 toorecover 나중 hello 초기 보호 완료 될 수 있습니다.
8. 클릭 **복구** toosave hello 계획 또는 트리거 hello 복구 toorecover 이제 이상 하지을 선택한 경우. Hello 계획의 저장 된 경우 복구 상태 toosee hello를 확인할 수 있습니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a>가상 컴퓨터 복구
Hello 계획의 만들어진 후에 hello 가상 컴퓨터를 복구할 수 있습니다. 해당 hello 가상 검사 수행 전에 컴퓨터는 동기화를 완료 했습니다. 복제 상태 확인이 표시 되 면 hello 보호 완료 되 고 hello RPO 임계값을 충족 하는 것입니다. Hello VM 속성에서 상태를 확인할 수 있습니다.

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

Hello Azure 가상 컴퓨터 전에 해제 hello 복구를 시작 합니다. 이렇게 하면 분할 브레인 없는 않으며 사용자가 hello 응용 프로그램의 복사본 하나에 액세스할 됩니다.

1. 계획을 저장 하는 hello를 시작 합니다. VContinuum 선택 **모니터** hello 계획 합니다. 이 실행 된 모든 hello 계획을 나열 합니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. 선택 hello 계획 **복구** 클릭 **시작**합니다. 복구를 모니터링할 수 있습니다. Vm 다시 설정 된 후에 toothem vCenter에 연결할 수 있습니다.

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a>장애 복구 후에 다시 tooAzure 보호
장애 복구 완료 된 후 해도 좋을 것 tooprotect hello 가상 컴퓨터 다시 합니다. 다음과 같이 수행합니다.

1. Hello 가상 컴퓨터가 온-프레미스 작업 하는 응용 프로그램에는 연결할 수 있는지 확인 합니다.
2. Hello Azure Site Recovery 포털에서 hello 가상 컴퓨터를 선택 하 고 삭제 합니다. Hello 가상 컴퓨터의 toodisable hello 보호를 선택 합니다. 이렇게 하면는 hello Vm은 더 이상 보호 합니다.
3. Azure의 hello 장애 조치 Azure 가상 컴퓨터를 삭제 합니다.
4. Hello vSpehere에서 이전 가상 컴퓨터를 삭제 합니다. 이들은 이전에 장애 조치 tooAzure hello Vm입니다.
5. Hello Site Recovery 포털에서 hello 최근에 장애 조치 하는 Vm을 보호 합니다. 보호 하는 추가할 수 있습니다 tooa 복구 계획 합니다.

## <a name="next-steps"></a>다음 단계
* [에 대 한 읽기](site-recovery-vmware-to-azure-classic.md) VMware 가상 컴퓨터 및 물리적 서버 tooAzure hello 향상 된 배포를 사용 하 여 복제 합니다.
