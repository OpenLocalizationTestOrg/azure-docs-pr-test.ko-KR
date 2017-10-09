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
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="c168a-103">소프트웨어 배포 도구를 사용하여 모바일 서비스 설치 자동화</span><span class="sxs-lookup"><span data-stu-id="c168a-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="c168a-104">이 문서에서는 **9.9.4510.1** 이상 버전을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="c168a-105">이 문서는 데이터 센터에서 System Center Configuration Manager toodeploy hello Azure Site Recovery 모바일 서비스 사용 방법의 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="c168a-106">Configuration Manager 같은 소프트웨어 배포 도구를 사용 하 여 hello 장점 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="c168a-107">소프트웨어 업데이트에 대한 계획된 유지 관리 시간에 새로 설치 및 업그레이드 배포 예약</span><span class="sxs-lookup"><span data-stu-id="c168a-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="c168a-108">서버 배포 toohundreds를 동시에 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c168a-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="c168a-109">이 문서에서는 System Center Configuration Manager 2012 R2 toodemonstrate hello 배포 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="c168a-110">[Azure Automation 및 필요한 상태 구성](site-recovery-automate-mobility-service-install.md)을 사용하여 모바일 서비스 설치를 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c168a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c168a-111">Prerequisites</span></span>
1. <span data-ttu-id="c168a-112">Configuration Manager 같은 소프트웨어 배포 도구가 사용자 환경에 이미 배포되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="c168a-113">두 개 만든 [장치 컬렉션](https://technet.microsoft.com/library/gg682169.aspx), 모든에 대해 하나씩 **Windows 서버**, 용이고 다른 하나는 모든 **Linux 서버**, 사이트 복구를 사용 하 여 tooprotect 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="c168a-114">Site Recovery에 이미 구성 서버가 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="c168a-115">보안 네트워크 파일 공유 (서버 메시지 블록 공유) hello Configuration Manager 서버에서 액세스할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="c168a-116">Windows를 실행하는 컴퓨터에 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="c168a-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="c168a-117">이 문서를 있다고 가정 hello 구성 서버 IP 주소 hello 192.168.3.121, 고 hello 보안 네트워크 파일 공유 위치가 \\\ContosoSecureFS\MobilityServiceInstallers 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="c168a-118">1단계: 배포 준비</span><span class="sxs-lookup"><span data-stu-id="c168a-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="c168a-119">Hello 네트워크 공유에 폴더를 만들고 이름을 **MobSvcWindows**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="c168a-120">Tooyour 구성 서버에 로그인 하 고 관리 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="c168a-121">Hello 명령을 toogenerate 암호 파일을 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="c168a-122">복사 hello **MobSvc.passphrase** hello에 파일을 **MobSvcWindows** 네트워크 공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="c168a-123">Hello 다음 명령을 실행 하 여 hello 구성 서버에서 toohello installer 저장소를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="c168a-124">복사 hello  **Microsoft ASR\_UA\_*버전*\_Windows\_GA\_*날짜* \_ Release.exe** toohello **MobSvcWindows** 네트워크 공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="c168a-125">코드를 다음 hello를 복사 하 고로 저장 **install.bat** hello에 **MobSvcWindows** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c168a-126">구성 서버 IP 주소 hello hello 실제 값으로이 스크립트의 hello [CSIP] 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="c168a-127">2단계: 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c168a-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="c168a-128">Tooyour Configuration Manager 콘솔에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="c168a-129">너무 찾아보기**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="c168a-130">**패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="c168a-131">Hello 이름, 설명, 제조업체, 언어 및 버전에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="c168a-132">선택 hello **이 패키지 원본 파일이** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="c168a-133">클릭 **찾아보기**와 hello installer 저장 된 select hello 네트워크 공유 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="c168a-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="c168a-135">Hello에 **toocreate 않겠다고 선택 hello 프로그램 유형** 페이지에서 **표준 프로그램**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="c168a-137">Hello에 **이 표준 프로그램에 대 한 정보를 지정** 페이지 hello 다음 입력을 제공 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="c168a-138">(hello 다른 입력 수 기본값을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="c168a-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="c168a-139">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="c168a-139">**Parameter name**</span></span> | <span data-ttu-id="c168a-140">**값**</span><span class="sxs-lookup"><span data-stu-id="c168a-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="c168a-141">이름</span><span class="sxs-lookup"><span data-stu-id="c168a-141">Name</span></span> | <span data-ttu-id="c168a-142">Microsoft Azure Mobility Service(Windows) 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="c168a-143">명령 줄</span><span class="sxs-lookup"><span data-stu-id="c168a-143">Command line</span></span> | <span data-ttu-id="c168a-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="c168a-144">install.bat</span></span> |
  | <span data-ttu-id="c168a-145">프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-145">Program can run</span></span> | <span data-ttu-id="c168a-146">사용자 로그온 여부</span><span class="sxs-lookup"><span data-stu-id="c168a-146">Whether or not a user is logged on</span></span> |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="c168a-148">Hello 다음 페이지에서 hello 대상 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="c168a-149">모바일 서비스는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2에만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="c168a-151">toocomplete hello 마법사 클릭 **다음** 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="c168a-152">hello 스크립트는 모두 새 모바일 서비스 에이전트 설치를 지원 하 고 이미 설치 되어 있는 tooagents를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="c168a-153">3 단계: hello 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="c168a-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="c168a-154">Hello Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **콘텐츠 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="c168a-155">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="c168a-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="c168a-156">선택 hello  **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich에 hello 패키지 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="c168a-157">전체 hello 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-157">Complete hello wizard.</span></span> <span data-ttu-id="c168a-158">hello 패키지 한 다음 시작 toohello 복제 배포 지점을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="c168a-159">Hello 패키지 배포를 완료 한 후 hello 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="c168a-160">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="c168a-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="c168a-161">배포에 대 한 hello 대상 컬렉션으로 hello 전제 조건 섹션에서 만든 hello Windows Server 장치 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="c168a-163">Hello에 **hello 콘텐츠 대상 지정** 페이지에서 프로그램 **배포 지점**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="c168a-164">Hello에 **이 소프트웨어를 배포 하는 방법을 지정 설정 toocontrol** 페이지, hello 목적 인지 확인 **필요한**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="c168a-166">Hello에 **이 배포에 대 한 hello 일정 지정** 페이지에서 일정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="c168a-167">자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c168a-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="c168a-168">Hello에 **배포 지점** 페이지에서 데이터 센터의 toohello 요구에 따라 hello 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="c168a-169">Hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="c168a-170">불필요 한 tooavoid 재부팅 월별 유지 관리 기간 또는 소프트웨어 업데이트 기간 동안 일정 hello 패키지 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="c168a-171">Hello Configuration Manager 콘솔을 사용 하 여 hello 배포 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="c168a-172">너무 이동**모니터링** > **배포** > *[패키지 이름]*합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Configuration Manager의 스크린 샷 옵션 toomonitor 배포](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="c168a-174">Linux를 실행하는 컴퓨터에 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="c168a-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="c168a-175">이 문서를 있다고 가정 hello 구성 서버 IP 주소 hello 192.168.3.121, 고 hello 보안 네트워크 파일 공유 위치가 \\\ContosoSecureFS\MobilityServiceInstallers 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="c168a-176">1단계: 배포 준비</span><span class="sxs-lookup"><span data-stu-id="c168a-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="c168a-177">Hello 네트워크 공유에 폴더를 만들고로 이름을 **MobSvcLinux**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="c168a-178">Tooyour 구성 서버에 로그인 하 고 관리 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="c168a-179">Hello 명령을 toogenerate 암호 파일을 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="c168a-180">복사 hello **MobSvc.passphrase** hello에 파일을 **MobSvcLinux** 네트워크 공유 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="c168a-181">Hello 명령을 실행 하 여 hello 구성 서버에서 toohello installer 저장소를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="c168a-182">복사 hello 다음 파일 toohello **MobSvcLinux** 네트워크 공유에 폴더:</span><span class="sxs-lookup"><span data-stu-id="c168a-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="c168a-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="c168a-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="c168a-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="c168a-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="c168a-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="c168a-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c168a-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="c168a-189">코드를 다음 hello를 복사 하 고로 저장 **install_linux.sh** hello에 **MobSvcLinux** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="c168a-190">구성 서버 IP 주소 hello hello 실제 값으로이 스크립트의 hello [CSIP] 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="c168a-191">2단계: 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c168a-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="c168a-192">Tooyour Configuration Manager 콘솔에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="c168a-193">너무 찾아보기**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="c168a-194">**패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="c168a-195">Hello 이름, 설명, 제조업체, 언어 및 버전에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="c168a-196">선택 hello **이 패키지 원본 파일이** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="c168a-197">클릭 **찾아보기**와 hello installer 저장 된 select hello 네트워크 공유 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="c168a-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="c168a-199">Hello에 **toocreate 않겠다고 선택 hello 프로그램 유형** 페이지에서 **표준 프로그램**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="c168a-201">Hello에 **이 표준 프로그램에 대 한 정보를 지정** 페이지 hello 다음 입력을 제공 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="c168a-202">(hello 다른 입력 수 기본값을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="c168a-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="c168a-203">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="c168a-203">**Parameter name**</span></span> | <span data-ttu-id="c168a-204">**값**</span><span class="sxs-lookup"><span data-stu-id="c168a-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="c168a-205">이름</span><span class="sxs-lookup"><span data-stu-id="c168a-205">Name</span></span> | <span data-ttu-id="c168a-206">Microsoft Azure Mobility Service(Linux) 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="c168a-207">명령 줄</span><span class="sxs-lookup"><span data-stu-id="c168a-207">Command line</span></span> | <span data-ttu-id="c168a-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="c168a-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="c168a-209">프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-209">Program can run</span></span> | <span data-ttu-id="c168a-210">사용자 로그온 여부</span><span class="sxs-lookup"><span data-stu-id="c168a-210">Whether or not a user is logged on</span></span> |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="c168a-212">Hello 다음 페이지에서 선택 **모든 플랫폼에서이 프로그램 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="c168a-213">![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="c168a-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="c168a-214">toocomplete hello 마법사 클릭 **다음** 두 번입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="c168a-215">hello 스크립트는 모두 새 모바일 서비스 에이전트 설치를 지원 하 고 이미 설치 되어 있는 tooagents를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="c168a-216">3 단계: hello 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="c168a-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="c168a-217">Hello Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **콘텐츠 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="c168a-218">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="c168a-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="c168a-219">선택 hello  **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich에 hello 패키지 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="c168a-220">전체 hello 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-220">Complete hello wizard.</span></span> <span data-ttu-id="c168a-221">hello 패키지 한 다음 시작 toohello 복제 배포 지점을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="c168a-222">Hello 패키지 배포를 완료 한 후 hello 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="c168a-223">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="c168a-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="c168a-224">Hello 배포에 대 한 hello 대상 컬렉션으로 hello 전제 조건 섹션에서 만든 Linux 서버 장치 컬렉션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="c168a-226">Hello에 **hello 콘텐츠 대상 지정** 페이지에서 프로그램 **배포 지점**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="c168a-227">Hello에 **이 소프트웨어를 배포 하는 방법을 지정 설정 toocontrol** 페이지, hello 목적 인지 확인 **필요한**합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="c168a-229">Hello에 **이 배포에 대 한 hello 일정 지정** 페이지에서 일정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="c168a-230">자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c168a-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="c168a-231">Hello에 **배포 지점** 페이지에서 데이터 센터의 toohello 요구에 따라 hello 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="c168a-232">Hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-232">Then complete hello wizard.</span></span>

<span data-ttu-id="c168a-233">모바일 서비스는 hello 구성한 toohello 일정에 따라 Linux 서버 장치 컬렉션에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="c168a-234">다른 메서드 tooinstall 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="c168a-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="c168a-235">다음은 모바일 서비스를 설치하는 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="c168a-236">GUI를 사용한 수동 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="c168a-237">명령줄을 사용한 수동 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="c168a-238">구성 서버를 사용한 푸시 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="c168a-239">Azure Automation 및 필요한 상태 구성을 사용한 자동화된 설치</span><span class="sxs-lookup"><span data-stu-id="c168a-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="c168a-240">모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="c168a-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="c168a-241">Configuration Manager 패키지 toouninstall 모바일 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="c168a-242">따라서 스크립트 toodo 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c168a-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c168a-243">Next steps</span></span>
<span data-ttu-id="c168a-244">이제 준비가 너무[보호 사용](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c168a-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
