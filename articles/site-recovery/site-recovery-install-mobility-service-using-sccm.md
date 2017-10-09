---
title: "소프트웨어 배포 도구를 사용 하 여 Azure Site Recovery에 대 한 모바일 서비스 설치 aaaAutomate | Microsoft Docs"
description: "이 문서에서는 System Center Configuration Manager 같은 소프트웨어 배포 도구를 사용하여 모바일 서비스 설치를 자동화하는 방법을 안내합니다."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>소프트웨어 배포 도구를 사용하여 모바일 서비스 설치 자동화

>[!IMPORTANT]
이 문서에서는 **9.9.4510.1** 이상 버전을 사용한다고 가정합니다.

이 문서는 데이터 센터에서 System Center Configuration Manager toodeploy hello Azure Site Recovery 모바일 서비스 사용 방법의 예가 나와 있습니다. Configuration Manager 같은 소프트웨어 배포 도구를 사용 하 여 hello 장점 뒤에 있습니다.
* 소프트웨어 업데이트에 대한 계획된 유지 관리 시간에 새로 설치 및 업그레이드 배포 예약
* 서버 배포 toohundreds를 동시에 크기 조정


> [!NOTE]
> 이 문서에서는 System Center Configuration Manager 2012 R2 toodemonstrate hello 배포 활동을 사용 합니다. [Azure Automation 및 필요한 상태 구성](site-recovery-automate-mobility-service-install.md)을 사용하여 모바일 서비스 설치를 자동화할 수도 있습니다.

## <a name="prerequisites"></a>필수 조건
1. Configuration Manager 같은 소프트웨어 배포 도구가 사용자 환경에 이미 배포되어 있어야 합니다.
  두 개 만든 [장치 컬렉션](https://technet.microsoft.com/library/gg682169.aspx), 모든에 대해 하나씩 **Windows 서버**, 용이고 다른 하나는 모든 **Linux 서버**, 사이트 복구를 사용 하 여 tooprotect 되도록 합니다.
3. Site Recovery에 이미 구성 서버가 등록되어 있어야 합니다.
4. 보안 네트워크 파일 공유 (서버 메시지 블록 공유) hello Configuration Manager 서버에서 액세스할 수 있는 합니다.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Windows를 실행하는 컴퓨터에 모바일 서비스 배포
> [!NOTE]
> 이 문서를 있다고 가정 hello 구성 서버 IP 주소 hello 192.168.3.121, 고 hello 보안 네트워크 파일 공유 위치가 \\\ContosoSecureFS\MobilityServiceInstallers 합니다.

### <a name="step-1-prepare-for-deployment"></a>1단계: 배포 준비
1. Hello 네트워크 공유에 폴더를 만들고 이름을 **MobSvcWindows**합니다.
2. Tooyour 구성 서버에 로그인 하 고 관리 명령 프롬프트를 엽니다.
3. Hello 명령을 toogenerate 암호 파일을 다음을 실행 합니다.

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. 복사 hello **MobSvc.passphrase** hello에 파일을 **MobSvcWindows** 네트워크 공유 폴더입니다.
5. Hello 다음 명령을 실행 하 여 hello 구성 서버에서 toohello installer 저장소를 이동 합니다.

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. 복사 hello  **Microsoft ASR\_UA\_*버전*\_Windows\_GA\_*날짜* \_ Release.exe** toohello **MobSvcWindows** 네트워크 공유 폴더입니다.
7. 코드를 다음 hello를 복사 하 고로 저장 **install.bat** hello에 **MobSvcWindows** 폴더입니다.

   > [!NOTE]
   > 구성 서버 IP 주소 hello hello 실제 값으로이 스크립트의 hello [CSIP] 자리 표시자를 대체 합니다.

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a>2단계: 패키지 만들기

1. Tooyour Configuration Manager 콘솔에 로그인 합니다.
2. 너무 찾아보기**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**합니다.
3. **패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.
4. Hello 이름, 설명, 제조업체, 언어 및 버전에 대 한 값을 제공 합니다.
5. 선택 hello **이 패키지 원본 파일이** 확인란 합니다.
6. 클릭 **찾아보기**와 hello installer 저장 된 select hello 네트워크 공유 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. Hello에 **toocreate 않겠다고 선택 hello 프로그램 유형** 페이지에서 **표준 프로그램**를 클릭 하 고 **다음**합니다.

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Hello에 **이 표준 프로그램에 대 한 정보를 지정** 페이지 hello 다음 입력을 제공 하 고 클릭 **다음**합니다. (hello 다른 입력 수 기본값을 사용 합니다.)

  | **매개 변수 이름** | **값** |
  |--|--|
  | 이름 | Microsoft Azure Mobility Service(Windows) 설치 |
  | 명령 줄 | install.bat |
  | 프로그램을 실행할 수 있습니다. | 사용자 로그온 여부 |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. Hello 다음 페이지에서 hello 대상 운영 체제를 선택 합니다. 모바일 서비스는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2에만 설치할 수 있습니다.

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. toocomplete hello 마법사 클릭 **다음** 두 번입니다.


> [!NOTE]
> hello 스크립트는 모두 새 모바일 서비스 에이전트 설치를 지원 하 고 이미 설치 되어 있는 tooagents를 업데이트 합니다.

### <a name="step-3-deploy-hello-package"></a>3 단계: hello 패키지 배포
1. Hello Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **콘텐츠 배포**합니다.
  ![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. 선택 hello  **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich에 hello 패키지 복사 해야 합니다.
3. 전체 hello 마법사입니다. hello 패키지 한 다음 시작 toohello 복제 배포 지점을 지정 합니다.
4. Hello 패키지 배포를 완료 한 후 hello 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포**합니다.
  ![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. 배포에 대 한 hello 대상 컬렉션으로 hello 전제 조건 섹션에서 만든 hello Windows Server 장치 컬렉션을 선택 합니다.

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. Hello에 **hello 콘텐츠 대상 지정** 페이지에서 프로그램 **배포 지점**합니다.
7. Hello에 **이 소프트웨어를 배포 하는 방법을 지정 설정 toocontrol** 페이지, hello 목적 인지 확인 **필요한**합니다.

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Hello에 **이 배포에 대 한 hello 일정 지정** 페이지에서 일정을 지정 합니다. 자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.
9. Hello에 **배포 지점** 페이지에서 데이터 센터의 toohello 요구에 따라 hello 속성을 구성 합니다. Hello 마법사를 완료 합니다.

> [!TIP]
> 불필요 한 tooavoid 재부팅 월별 유지 관리 기간 또는 소프트웨어 업데이트 기간 동안 일정 hello 패키지 설치 됩니다.

Hello Configuration Manager 콘솔을 사용 하 여 hello 배포 진행률을 모니터링할 수 있습니다. 너무 이동**모니터링** > **배포** > *[패키지 이름]*합니다.

  ![Configuration Manager의 스크린 샷 옵션 toomonitor 배포](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Linux를 실행하는 컴퓨터에 모바일 서비스 배포
> [!NOTE]
> 이 문서를 있다고 가정 hello 구성 서버 IP 주소 hello 192.168.3.121, 고 hello 보안 네트워크 파일 공유 위치가 \\\ContosoSecureFS\MobilityServiceInstallers 합니다.

### <a name="step-1-prepare-for-deployment"></a>1단계: 배포 준비
1. Hello 네트워크 공유에 폴더를 만들고로 이름을 **MobSvcLinux**합니다.
2. Tooyour 구성 서버에 로그인 하 고 관리 명령 프롬프트를 엽니다.
3. Hello 명령을 toogenerate 암호 파일을 다음을 실행 합니다.

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. 복사 hello **MobSvc.passphrase** hello에 파일을 **MobSvcLinux** 네트워크 공유 폴더입니다.
5. Hello 명령을 실행 하 여 hello 구성 서버에서 toohello installer 저장소를 이동 합니다.

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. 복사 hello 다음 파일 toohello **MobSvcLinux** 네트워크 공유에 폴더:
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. 코드를 다음 hello를 복사 하 고로 저장 **install_linux.sh** hello에 **MobSvcLinux** 폴더입니다.
   > [!NOTE]
   > 구성 서버 IP 주소 hello hello 실제 값으로이 스크립트의 hello [CSIP] 자리 표시자를 대체 합니다.

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a>2단계: 패키지 만들기

1. Tooyour Configuration Manager 콘솔에 로그인 합니다.
2. 너무 찾아보기**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**합니다.
3. **패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.
4. Hello 이름, 설명, 제조업체, 언어 및 버전에 대 한 값을 제공 합니다.
5. 선택 hello **이 패키지 원본 파일이** 확인란 합니다.
6. 클릭 **찾아보기**와 hello installer 저장 된 select hello 네트워크 공유 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. Hello에 **toocreate 않겠다고 선택 hello 프로그램 유형** 페이지에서 **표준 프로그램**를 클릭 하 고 **다음**합니다.

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Hello에 **이 표준 프로그램에 대 한 정보를 지정** 페이지 hello 다음 입력을 제공 하 고 클릭 **다음**합니다. (hello 다른 입력 수 기본값을 사용 합니다.)

    | **매개 변수 이름** | **값** |
  |--|--|
  | 이름 | Microsoft Azure Mobility Service(Linux) 설치 |
  | 명령 줄 | ./install_linux.sh |
  | 프로그램을 실행할 수 있습니다. | 사용자 로그온 여부 |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. Hello 다음 페이지에서 선택 **모든 플랫폼에서이 프로그램 실행**합니다.
  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. toocomplete hello 마법사 클릭 **다음** 두 번입니다.

> [!NOTE]
> hello 스크립트는 모두 새 모바일 서비스 에이전트 설치를 지원 하 고 이미 설치 되어 있는 tooagents를 업데이트 합니다.

### <a name="step-3-deploy-hello-package"></a>3 단계: hello 패키지 배포
1. Hello Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **콘텐츠 배포**합니다.
  ![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. 선택 hello  **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich에 hello 패키지 복사 해야 합니다.
3. 전체 hello 마법사입니다. hello 패키지 한 다음 시작 toohello 복제 배포 지점을 지정 합니다.
4. Hello 패키지 배포를 완료 한 후 hello 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포**합니다.
  ![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Hello 배포에 대 한 hello 대상 컬렉션으로 hello 전제 조건 섹션에서 만든 Linux 서버 장치 컬렉션을 선택 합니다.

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. Hello에 **hello 콘텐츠 대상 지정** 페이지에서 프로그램 **배포 지점**합니다.
7. Hello에 **이 소프트웨어를 배포 하는 방법을 지정 설정 toocontrol** 페이지, hello 목적 인지 확인 **필요한**합니다.

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Hello에 **이 배포에 대 한 hello 일정 지정** 페이지에서 일정을 지정 합니다. 자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.
9. Hello에 **배포 지점** 페이지에서 데이터 센터의 toohello 요구에 따라 hello 속성을 구성 합니다. Hello 마법사를 완료 합니다.

모바일 서비스는 hello 구성한 toohello 일정에 따라 Linux 서버 장치 컬렉션에 설치 됩니다.

## <a name="other-methods-tooinstall-mobility-service"></a>다른 메서드 tooinstall 모바일 서비스
다음은 모바일 서비스를 설치하는 다른 옵션입니다.
* [GUI를 사용한 수동 설치](http://aka.ms/mobsvcmanualinstall)
* [명령줄을 사용한 수동 설치](http://aka.ms/mobsvcmanualinstallcli)
* [구성 서버를 사용한 푸시 설치](http://aka.ms/pushinstall)
* [Azure Automation 및 필요한 상태 구성을 사용한 자동화된 설치](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>모바일 서비스 제거
Configuration Manager 패키지 toouninstall 모바일 서비스를 만들 수 있습니다. 따라서 스크립트 toodo 다음 hello를 사용 합니다.

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a>다음 단계
이제 준비가 너무[보호 사용](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) 가상 컴퓨터에 대 한 합니다.
