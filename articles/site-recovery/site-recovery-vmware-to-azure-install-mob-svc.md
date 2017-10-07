---
title: "모바일 서비스 (VMware 또는 물리적 tooAzure) aaaInstall | Microsoft Docs"
description: "어떻게 tooinstall hello 모바일 서비스 에이전트가 tooprotect 온-프레미스 컴퓨터에 알아봅니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>(VMware 또는 물리적 tooAzure) Mobility Service 설치
Azure Site Recovery 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버로 전달 합니다. 원하는 tooreplicate tooAzure 모바일 서비스 tooevery 컴퓨터 (VMware VM 또는 실제 서버)를 배포 합니다. 모바일 서비스 toohello 서버 hello 다음 메서드를 사용 하 여 tooprotect 되도록 배포할 수 있습니다.


* [System Center Configuration Manager와 같은 소프트웨어 배포 도구를 사용하여 모바일 서비스 설치](site-recovery-install-mobility-service-using-sccm.md)
* [Azure Automation 및 자동화 DSC(필요한 상태 구성)를 사용하여 모바일 서비스 설치](site-recovery-automate-mobility-service-install.md)
* [Hello 그래픽 사용자 인터페이스 (GUI)를 사용 하 여 모바일 서비스를 수동으로 설치](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [명령 프롬프트에서 수동으로 모바일 서비스 설치](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Windows 가상 컴퓨터 (Vm)에 9.7.0.0, 버전부터 hello 모바일 서비스 설치 관리자도 설치 hello 최신 사용 가능한 [Azure VM 에이전트](../virtual-machines/windows/extensions-features.md#azure-vm-agent)합니다. TooAzure 조치는 컴퓨터가 실패할 경우 hello 컴퓨터 hello 에이전트 설치 모든 VM 확장을 사용 하기 위한 필수 구성 요소를 충족 합니다.

## <a name="prerequisites"></a>필수 조건
서버에 모바일 서비스를 수동으로 설치하기 전에 이러한 필수 조건 단계를 완료합니다.
1. Tooyour 구성 서버에 서명 하 고 관리자 권한으로 명령 프롬프트 창을 엽니다.
2. Hello 디렉터리 toohello bin 폴더를 변경 하 고 암호 파일을 만듭니다.

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Hello 암호 파일을 안전한 위치에 저장 합니다. Hello 모바일 서비스 설치 중 hello 파일을 사용 합니다.
4. 지원 되는 모든 운영 체제에 대 한 모바일 서비스 설치 관리자는 hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 폴더에 있습니다.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>모바일 서비스 설치 관리자와 운영 체제 매핑

| 설치 관리자 파일 템플릿 이름| 운영 체제 |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1(64비트) </br> Windows Server 2012(64비트) </br> Windows Server 2012 R2(64비트) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| RHEL(Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | RHEL(Red Hat Enterprise Linux) 7.1, 7.2(64비트만 해당) </br> CentOS 7.0, 7.1, 7.2(64비트만 해당)</br> CentOs 7.3(마이그레이션만 해당) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3(64비트만 해당)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4(64비트만 해당)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5(64비트만 해당)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04(64비트만 해당)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Hello GUI를 사용 하 여 모바일 서비스를 수동으로 설치

>[!IMPORTANT]
> 사용 하는 경우는 **구성 서버** tooreplicate **Azure IaaS 가상 컴퓨터** 하나의 Azure 구독/지역 tooanother 다음에서 **hello 명령줄 기반된 설치를 사용 하 여**  메서드

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>명령 프롬프트에서 수동으로 모바일 서비스 설치

### <a name="command-line-installation-on-a-windows-computer"></a>Windows 컴퓨터에서 명령줄 설치
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Linux 컴퓨터에서 명령줄 설치
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치
Site Recovery를 사용 하 여 모바일 서비스의 강제 설치 toodo 모든 대상 컴퓨터 hello 다음 필수 구성 요소를 충족 해야 합니다.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Hello Azure 포털에서에서 모바일 서비스를 설치한 후 선택 hello **복제** 단추 toostart 이러한 Vm을 보호 합니다.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Windows Server 컴퓨터에서 모바일 서비스 제거
Hello 메서드 toouninstall 모바일 서비스는 Windows Server 컴퓨터에서 다음 중 하나를 사용 합니다.

### <a name="uninstall-by-using-hello-gui"></a>Hello GUI를 사용 하 여 제거
1. 제어판에서 **프로그램**을 선택합니다.
2. **Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버**를 선택한 다음 **제거**를 선택합니다.

### <a name="uninstall-at-a-command-prompt"></a>명령 프롬프트에서 제거
1. 관리자로 명령 프롬프트 창을 엽니다.
2. toouninstall 모바일 서비스 hello 다음 명령을 실행 하는 중:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Linux 컴퓨터에서 모바일 서비스 제거
1. Linux 서버에서 **루트** 사용자로 로그인합니다.
2. 종료, 너무/사용자/로컬/ASR을 이동 합니다.
3. toouninstall 모바일 서비스 hello 다음 명령을 실행 하는 중:

```
uninstall.sh -Y
```
