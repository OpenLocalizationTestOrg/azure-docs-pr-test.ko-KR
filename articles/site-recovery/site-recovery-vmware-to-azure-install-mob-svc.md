---
title: "모바일 서비스(VMware/Azure 물리적 서버) 설치 | Microsoft Docs"
description: "온-프레미스 컴퓨터를 보호하기 위해 모바일 서비스 에이전트를 설치하는 방법을 알아봅니다."
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="81b3d-103">모바일 서비스(VMware/Azure 물리적 서버) 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="81b3d-104">Azure Site Recovery 모바일 서비스는 컴퓨터에서 데이터 쓰기를 캡처하여 프로세스 서버로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="81b3d-105">Azure에 복제하려는 모든 컴퓨터에 모바일 서비스(VMware VM 또는 물리적 서버)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="81b3d-106">다음 방법을 사용하여 보호하려는 서버에 모바일 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="81b3d-107">System Center Configuration Manager와 같은 소프트웨어 배포 도구를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="81b3d-108">Azure Automation 및 자동화 DSC(필요한 상태 구성)를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="81b3d-109">GUI(그래픽 사용자 인터페이스)를 사용하여 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="81b3d-110">명령 프롬프트에서 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="81b3d-111">Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="81b3d-112">9.7.0.0 버전부터 모바일 서비스 설치 관리자는 Windows 가상 컴퓨터에 사용 가능한 최신 [Azure VM 에이전트](../virtual-machines/windows/extensions-features.md#azure-vm-agent)도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="81b3d-113">컴퓨터가 Azure로 장애 조치되는 경우에는 VM 확장 사용에 대한 에이전트 설치 필수 조건을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81b3d-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="81b3d-114">Prerequisites</span></span>
<span data-ttu-id="81b3d-115">서버에 모바일 서비스를 수동으로 설치하기 전에 이러한 필수 조건 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="81b3d-116">구성 서버에 로그인한 후 관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="81b3d-117">디렉터리를 Bin 폴더로 변경하고 암호 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="81b3d-118">암호 파일을 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="81b3d-119">이 파일은 모바일 서비스를 설치하는 동안 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="81b3d-120">지원되는 모든 운영 체제에 대한 모바일 서비스 설치 관리자는 %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="81b3d-121">모바일 서비스 설치 관리자와 운영 체제 매핑</span><span class="sxs-lookup"><span data-stu-id="81b3d-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="81b3d-122">설치 관리자 파일 템플릿 이름</span><span class="sxs-lookup"><span data-stu-id="81b3d-122">Installer file template name</span></span>| <span data-ttu-id="81b3d-123">운영 체제</span><span class="sxs-lookup"><span data-stu-id="81b3d-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="81b3d-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="81b3d-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="81b3d-125">Windows Server 2008 R2 SP1(64비트)</span><span class="sxs-lookup"><span data-stu-id="81b3d-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="81b3d-126">Windows Server 2012(64비트)</span><span class="sxs-lookup"><span data-stu-id="81b3d-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="81b3d-127">Windows Server 2012 R2(64비트)</span><span class="sxs-lookup"><span data-stu-id="81b3d-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="81b3d-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="81b3d-129">RHEL(Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="81b3d-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="81b3d-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="81b3d-132">RHEL(Red Hat Enterprise Linux) 7.1, 7.2(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="81b3d-133">CentOS 7.0, 7.1, 7.2(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="81b3d-134">CentOs 7.3(마이그레이션만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="81b3d-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="81b3d-136">SUSE Linux Enterprise Server 11 SP3(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="81b3d-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="81b3d-138">SUSE Linux Enterprise Server 11 SP4(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="81b3d-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="81b3d-140">Oracle Enterprise Linux 6.4, 6.5(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="81b3d-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="81b3d-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="81b3d-142">Ubuntu Linux 14.04(64비트만 해당)</span><span class="sxs-lookup"><span data-stu-id="81b3d-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="81b3d-143">GUI를 사용하여 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="81b3d-144">**구성 서버**를 사용하여 Azure 구독/지역 간에 **Azure IaaS 가상 컴퓨터**를 복제하는 경우 **명령줄 기반 설치 메서드를 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="81b3d-145">명령 프롬프트에서 수동으로 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="81b3d-146">Windows 컴퓨터에서 명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="81b3d-147">Linux 컴퓨터에서 명령줄 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="81b3d-148">Azure Site Recovery에서 강제 설치를 사용하여 모바일 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="81b3d-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="81b3d-149">Site Recovery를 사용하여 모바일 서비스의 강제 설치를 수행하려면 모든 대상 컴퓨터가 다음 필수 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="81b3d-150">모바일 서비스를 설치한 후 Azure Portal에서 **복제** 단추를 선택하여 이러한 VM 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="81b3d-151">Windows Server 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="81b3d-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="81b3d-152">Windows Server 컴퓨터에서 모바일 서비스를 제거하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="81b3d-153">GUI를 사용하여 제거</span><span class="sxs-lookup"><span data-stu-id="81b3d-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="81b3d-154">제어판에서 **프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="81b3d-155">**Microsoft Azure Site Recovery 모바일 서비스/마스터 대상 서버**를 선택한 다음 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="81b3d-156">명령 프롬프트에서 제거</span><span class="sxs-lookup"><span data-stu-id="81b3d-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="81b3d-157">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="81b3d-158">모바일 서비스를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="81b3d-159">Linux 컴퓨터에서 모바일 서비스 제거</span><span class="sxs-lookup"><span data-stu-id="81b3d-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="81b3d-160">Linux 서버에서 **루트** 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="81b3d-161">터미널에서 /user/local/ASR로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="81b3d-162">모바일 서비스를 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81b3d-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
