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
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="91092-103">(VMware 또는 물리적 tooAzure) Mobility Service 설치</span><span class="sxs-lookup"><span data-stu-id="91092-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="91092-104">Azure Site Recovery 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="91092-105">원하는 tooreplicate tooAzure 모바일 서비스 tooevery 컴퓨터 (VMware VM 또는 실제 서버)를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="91092-106">모바일 서비스 toohello 서버 hello 다음 메서드를 사용 하 여 tooprotect 되도록 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91092-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="91092-107">System Center Configuration Manager와 같은 소프트웨어 배포 도구를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="91092-108">Azure Automation 및 자동화 DSC(필요한 상태 구성)를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="91092-109">Hello 그래픽 사용자 인터페이스 (GUI)를 사용 하 여 모바일 서비스를 수동으로 설치</span><span class="sxs-lookup"><span data-stu-id="91092-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="91092-110">명령 프롬프트에서 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="91092-111">Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="91092-112">Windows 가상 컴퓨터 (Vm)에 9.7.0.0, 버전부터 hello 모바일 서비스 설치 관리자도 설치 hello 최신 사용 가능한 [Azure VM 에이전트](../virtual-machines/windows/extensions-features.md#azure-vm-agent)합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="91092-113">TooAzure 조치는 컴퓨터가 실패할 경우 hello 컴퓨터 hello 에이전트 설치 모든 VM 확장을 사용 하기 위한 필수 구성 요소를 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91092-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91092-114">Prerequisites</span></span>
<span data-ttu-id="91092-115">서버에 모바일 서비스를 수동으로 설치하기 전에 이러한 필수 조건 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="91092-116">Tooyour 구성 서버에 서명 하 고 관리자 권한으로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91092-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="91092-117">Hello 디렉터리 toohello bin 폴더를 변경 하 고 암호 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91092-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="91092-118">Hello 암호 파일을 안전한 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="91092-119">Hello 모바일 서비스 설치 중 hello 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="91092-120">지원 되는 모든 운영 체제에 대 한 모바일 서비스 설치 관리자는 hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91092-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="91092-121">모바일 서비스 설치 관리자와 운영 체제 매핑</span><span class="sxs-lookup"><span data-stu-id="91092-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="91092-122">설치 관리자 파일 템플릿 이름</span><span class="sxs-lookup"><span data-stu-id="91092-122">Installer file template name</span></span>| <span data-ttu-id="91092-123">운영 체제</span><span class="sxs-lookup"><span data-stu-id="91092-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="91092-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="91092-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="91092-125">Windows Server 2008 R2 SP1(64비트)</span><span class="sxs-lookup"><span data-stu-id="91092-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="91092-126">Windows Server 2012(64비트)</span><span class="sxs-lookup"><span data-stu-id="91092-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="91092-127">Windows Server 2012 R2(64비트)</span><span class="sxs-lookup"><span data-stu-id="91092-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="91092-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="91092-129">RHEL(Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="91092-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="91092-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="91092-132">RHEL(Red Hat Enterprise Linux) 7.1, 7.2(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="91092-133">CentOS 7.0, 7.1, 7.2(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="91092-134">CentOs 7.3(마이그레이션만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="91092-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="91092-136">SUSE Linux Enterprise Server 11 SP3(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="91092-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="91092-138">SUSE Linux Enterprise Server 11 SP4(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="91092-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="91092-140">Oracle Enterprise Linux 6.4, 6.5(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="91092-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="91092-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="91092-142">Ubuntu Linux 14.04(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="91092-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="91092-143">Hello GUI를 사용 하 여 모바일 서비스를 수동으로 설치</span><span class="sxs-lookup"><span data-stu-id="91092-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="91092-144">사용 하는 경우는 **구성 서버** tooreplicate **Azure IaaS 가상 컴퓨터** 하나의 Azure 구독/지역 tooanother 다음에서 **hello 명령줄 기반된 설치를 사용 하 여**  메서드</span><span class="sxs-lookup"><span data-stu-id="91092-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="91092-145">명령 프롬프트에서 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="91092-146">Windows 컴퓨터에서 명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="91092-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="91092-147">Linux 컴퓨터에서 명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="91092-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="91092-148">Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="91092-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="91092-149">Site Recovery를 사용 하 여 모바일 서비스의 강제 설치 toodo 모든 대상 컴퓨터 hello 다음 필수 구성 요소를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="91092-150">Hello Azure 포털에서에서 모바일 서비스를 설치한 후 선택 hello **복제** 단추 toostart 이러한 Vm을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="91092-151">Windows Server 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="91092-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="91092-152">Hello 메서드 toouninstall 모바일 서비스는 Windows Server 컴퓨터에서 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="91092-153">Hello GUI를 사용 하 여 제거</span><span class="sxs-lookup"><span data-stu-id="91092-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="91092-154">제어판에서 **프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="91092-155">**Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버**를 선택한 다음 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="91092-156">명령 프롬프트에서 제거</span><span class="sxs-lookup"><span data-stu-id="91092-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="91092-157">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="91092-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="91092-158">toouninstall 모바일 서비스 hello 다음 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="91092-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="91092-159">Linux 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="91092-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="91092-160">Linux 서버에서 **루트** 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="91092-161">종료, 너무/사용자/로컬/ASR을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="91092-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="91092-162">toouninstall 모바일 서비스 hello 다음 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="91092-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
