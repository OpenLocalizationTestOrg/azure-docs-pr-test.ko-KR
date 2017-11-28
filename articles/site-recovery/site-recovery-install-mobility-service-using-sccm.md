---
title: "소프트웨어 배포 도구를 사용하여 Azure Site Recovery에 대한 모바일 서비스 설치 자동화 | Microsoft Docs"
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
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="92750-103">소프트웨어 배포 도구를 사용하여 모바일 서비스 설치 자동화</span><span class="sxs-lookup"><span data-stu-id="92750-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="92750-104">이 문서에서는 **9.9.4510.1** 이상 버전을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="92750-105">이 문서에서는 System Center Configuration Manager를 사용하여 데이터 센터에서 Azure Site Recovery 모바일 서비스를 배포하는 방법의 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="92750-106">Configuration Manager 같은 소프트웨어 배포 도구를 사용하면 다음과 같은 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="92750-107">소프트웨어 업데이트에 대한 계획된 유지 관리 시간에 새로 설치 및 업그레이드 배포 예약</span><span class="sxs-lookup"><span data-stu-id="92750-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="92750-108">동시에 수백 대의 서버에 대규모로 배포</span><span class="sxs-lookup"><span data-stu-id="92750-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="92750-109">이 문서에서는 System Center Configuration Manager 2012 R2를 사용하여 배포 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="92750-110">[Azure Automation 및 필요한 상태 구성](site-recovery-automate-mobility-service-install.md)을 사용하여 모바일 서비스 설치를 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92750-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="92750-111">Prerequisites</span></span>
1. <span data-ttu-id="92750-112">Configuration Manager 같은 소프트웨어 배포 도구가 사용자 환경에 이미 배포되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="92750-113">Site Recovery를 사용하여 보호하려는 모든 **Windows Servers**와 모든 **Linux Servers**에 각각 하나씩, 총 두 개의 [장치 컬렉션](https://technet.microsoft.com/library/gg682169.aspx)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92750-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="92750-114">Site Recovery에 이미 구성 서버가 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="92750-115">Configuration Manager 서버가 액세스할 수 있는 보안 네트워크 파일 공유(서버 메시지 블록 공유)가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="92750-116">Windows를 실행하는 컴퓨터에 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="92750-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="92750-117">이 문서에서는 구성 서버의 IP 주소가 192.168.3.121이고 보안 네트워크 파일 공유가 \\\ContosoSecureFS\MobilityServiceInstallers인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="92750-118">1단계: 배포 준비</span><span class="sxs-lookup"><span data-stu-id="92750-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="92750-119">네트워크 공유에 폴더를 만들고 이름을 **MobSvcWindows**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="92750-120">구성 서버에 로그인하고 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="92750-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="92750-121">다음 명령을 실행하여 암호 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="92750-122">네트워크 공유에서 **MobSvc.passphrase** 파일을 **MobSvcWindows** 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="92750-123">다음 명령을 실행하여 구성 서버의 설치 관리자 리포지토리를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="92750-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="92750-124">네트워크 공유에서 **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe**를 **MobSvcWindows** 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="92750-125">다음 코드를 복사하여 **MobSvcWindows** 폴더에 **install.bat**으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92750-126">이 스크립트의 [CSIP] 자리 표시자를 구성 서버 IP 주소의 실제 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92750-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="92750-127">2단계: 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="92750-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="92750-128">Configuration Manager 콘솔에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="92750-129">**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="92750-130">**패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="92750-131">이름, 설명, 제조업체, 언어, 버전에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="92750-132">**이 패키지는 원본 파일을 포함합니다** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="92750-133">**찾아보기**를 클릭하고 설치 관리자가 저장된 네트워크 공유를 선택합니다(\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="92750-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="92750-135">**만들려는 프로그램 유형 선택** 페이지에서 **표준 프로그램**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="92750-137">**이 표준 프로그램에 대한 정보 지정** 페이지에서 다음 입력을 제공하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="92750-138">(다른 입력은 해당 기본값을 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="92750-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="92750-139">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="92750-139">**Parameter name**</span></span> | <span data-ttu-id="92750-140">**값**</span><span class="sxs-lookup"><span data-stu-id="92750-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="92750-141">이름</span><span class="sxs-lookup"><span data-stu-id="92750-141">Name</span></span> | <span data-ttu-id="92750-142">Microsoft Azure Mobility Service(Windows) 설치</span><span class="sxs-lookup"><span data-stu-id="92750-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="92750-143">명령 줄</span><span class="sxs-lookup"><span data-stu-id="92750-143">Command line</span></span> | <span data-ttu-id="92750-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="92750-144">install.bat</span></span> |
  | <span data-ttu-id="92750-145">프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-145">Program can run</span></span> | <span data-ttu-id="92750-146">사용자 로그온 여부</span><span class="sxs-lookup"><span data-stu-id="92750-146">Whether or not a user is logged on</span></span> |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="92750-148">다음 페이지에서 대상 운영 체제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="92750-149">모바일 서비스는 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2에만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="92750-151">마법사를 완료하려면 **다음**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="92750-152">스크립트는 모바일 서비스 에이전트의 새로 설치 및 이미 설치된 에이전트의 업데이트를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="92750-153">3단계: 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="92750-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="92750-154">Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭하고 **콘텐츠 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="92750-155">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="92750-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="92750-156">패키지를 복사할 위치에 **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="92750-157">마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-157">Complete the wizard.</span></span> <span data-ttu-id="92750-158">그러면 패키지가 지정된 배포 지점에 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="92750-159">패키지 배포 작업이 완료되면 패키지를 마우스 오른쪽 단추로 클릭하고 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="92750-160">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="92750-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="92750-161">필수 구성 요소 섹션에서 만든 Widows Server 장치 컬렉션을 배포의 대상 컬렉션으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="92750-163">**콘텐츠 대상 지정** 페이지에서 **배포 지점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="92750-164">**이 소프트웨어를 배포하는 방법을 제어하는 설정 지정** 페이지에서 목적이 **필수**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="92750-166">**이 배포에 대한 일정 지정** 페이지에서 일정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="92750-167">자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92750-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="92750-168">**배포 지점** 페이지에서 데이터 센터 요구 사항에 따라 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="92750-169">그런 다음 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="92750-170">불필요한 재부팅을 방지하려면 매월 유지 관리 시간 또는 소프트웨어 업데이트 시간에 패키지 설치를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="92750-171">Configuration Manager 콘솔을 사용하여 배포 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="92750-172">**모니터링** > **배포** > *[패키지 이름]*으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![배포를 모니터링하는 Configuration Manager 옵션의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="92750-174">Linux를 실행하는 컴퓨터에 모바일 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="92750-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="92750-175">이 문서에서는 구성 서버의 IP 주소가 192.168.3.121이고 보안 네트워크 파일 공유가 \\\ContosoSecureFS\MobilityServiceInstallers인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="92750-176">1단계: 배포 준비</span><span class="sxs-lookup"><span data-stu-id="92750-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="92750-177">네트워크 공유에 폴더를 만들고 이름을 **MobSvcLinux**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="92750-178">구성 서버에 로그인하고 관리자 권한 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="92750-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="92750-179">다음 명령을 실행하여 암호 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="92750-180">네트워크 공유에서 **MobSvc.passphrase** 파일을 **MobSvcLinux** 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="92750-181">다음 명령을 실행하여 구성 서버에서 설치 관리자 리포지토리를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="92750-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="92750-182">네트워크 공유에서 다음 파일을 **MobSvcLinux** 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="92750-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="92750-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92750-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92750-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92750-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92750-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92750-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="92750-189">아래 코드를 복사하여 **MobSvcLinux** 폴더에 **install_linux.sh**로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="92750-190">이 스크립트의 [CSIP] 자리 표시자를 구성 서버 IP 주소의 실제 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="92750-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="92750-191">2단계: 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="92750-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="92750-192">Configuration Manager 콘솔에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="92750-193">**소프트웨어 라이브러리** > **응용 프로그램 관리** > **패키지**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="92750-194">**패키지**를 마우스 오른쪽 단추로 클릭하고 **패키지 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="92750-195">이름, 설명, 제조업체, 언어, 버전에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="92750-196">**이 패키지는 원본 파일을 포함합니다** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="92750-197">**찾아보기**를 클릭하고 설치 관리자가 저장된 네트워크 공유를 선택합니다(\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="92750-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="92750-199">**만들려는 프로그램 유형 선택** 페이지에서 **표준 프로그램**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="92750-201">**이 표준 프로그램에 대한 정보 지정** 페이지에서 다음 입력을 제공하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="92750-202">(다른 입력은 해당 기본값을 사용할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="92750-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="92750-203">**매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="92750-203">**Parameter name**</span></span> | <span data-ttu-id="92750-204">**값**</span><span class="sxs-lookup"><span data-stu-id="92750-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="92750-205">이름</span><span class="sxs-lookup"><span data-stu-id="92750-205">Name</span></span> | <span data-ttu-id="92750-206">Microsoft Azure Mobility Service(Linux) 설치</span><span class="sxs-lookup"><span data-stu-id="92750-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="92750-207">명령 줄</span><span class="sxs-lookup"><span data-stu-id="92750-207">Command line</span></span> | <span data-ttu-id="92750-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="92750-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="92750-209">프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-209">Program can run</span></span> | <span data-ttu-id="92750-210">사용자 로그온 여부</span><span class="sxs-lookup"><span data-stu-id="92750-210">Whether or not a user is logged on</span></span> |

  ![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="92750-212">다음 페이지에서 **모든 플랫폼에서 이 프로그램 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="92750-213">![패키지 및 프로그램 만들기 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="92750-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="92750-214">마법사를 완료하려면 **다음**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="92750-215">스크립트는 모바일 서비스 에이전트의 새로 설치 및 이미 설치된 에이전트의 업데이트를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="92750-216">3단계: 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="92750-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="92750-217">Configuration Manager 콘솔에서 패키지를 마우스 오른쪽 단추로 클릭하고 **콘텐츠 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="92750-218">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="92750-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="92750-219">패키지를 복사할 위치에 **[배포 지점](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="92750-220">마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-220">Complete the wizard.</span></span> <span data-ttu-id="92750-221">그러면 패키지가 지정된 배포 지점에 복제를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="92750-222">패키지 배포 작업이 완료되면 패키지를 마우스 오른쪽 단추로 클릭하고 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="92750-223">![Configuration Manager 콘솔의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="92750-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="92750-224">전제 조건 섹션에서 만든 Linux Server 장치 컬렉션을 배포의 대상 컬렉션으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="92750-226">**콘텐츠 대상 지정** 페이지에서 **배포 지점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="92750-227">**이 소프트웨어를 배포하는 방법을 제어하는 설정 지정** 페이지에서 목적이 **필수**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![소프트웨어 배포 마법사의 스크린샷](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="92750-229">**이 배포에 대한 일정 지정** 페이지에서 일정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="92750-230">자세한 내용은 [패키지 일정 예약](https://technet.microsoft.com/library/gg682178.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="92750-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="92750-231">**배포 지점** 페이지에서 데이터 센터 요구 사항에 따라 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="92750-232">그런 다음 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-232">Then complete the wizard.</span></span>

<span data-ttu-id="92750-233">사용자가 구성한 일정에 따라 Linux Server 장치 컬렉션에 모바일 서비스가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="92750-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="92750-234">모바일 서비스를 설치하는 다른 방법</span><span class="sxs-lookup"><span data-stu-id="92750-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="92750-235">다음은 모바일 서비스를 설치하는 다른 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="92750-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="92750-236">GUI를 사용한 수동 설치</span><span class="sxs-lookup"><span data-stu-id="92750-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="92750-237">명령줄을 사용한 수동 설치</span><span class="sxs-lookup"><span data-stu-id="92750-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="92750-238">구성 서버를 사용한 푸시 설치</span><span class="sxs-lookup"><span data-stu-id="92750-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="92750-239">Azure Automation 및 필요한 상태 구성을 사용한 자동화된 설치</span><span class="sxs-lookup"><span data-stu-id="92750-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="92750-240">모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="92750-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="92750-241">모바일 서비스를 제거하는 Configuration Manager 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="92750-242">이렇게 하려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92750-242">Use the following script to do so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92750-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92750-243">Next steps</span></span>
<span data-ttu-id="92750-244">이제 가상 컴퓨터의 [보호를 활성화](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications)할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="92750-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
