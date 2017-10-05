---
title: "Azure에서 SUSE Linux VHD 만들기 및 업로드"
description: "SUSE Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: c829f5d9a90b4260c6f41b2d9e511a0c6cb48f18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="02fe9-103">Azure용 SLES 또는 openSUSE 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="02fe9-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="02fe9-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02fe9-104">Prerequisites</span></span>
<span data-ttu-id="02fe9-105">이 문서에서는 가상 하드 디스크에 SUSE 또는 openSUSE Linux 운영 체제를 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="02fe9-106">.vhd 파일을 만드는 여러 도구가 있습니다(예: Hyper-V와 같은 가상화 솔루션).</span><span class="sxs-lookup"><span data-stu-id="02fe9-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="02fe9-107">자세한 내용은 [Hyper-V 역할 설치 및 가상 시스템 구성](http://technet.microsoft.com/library/hh846766.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="02fe9-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="02fe9-108">SLES/openSUSE 설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="02fe9-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="02fe9-109">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02fe9-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="02fe9-110">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="02fe9-111">Hyper-V 관리자 또는 convert-vhd cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="02fe9-112">Linux 시스템 설치 시에는 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="02fe9-113">이렇게 하면 특히 문제 해결을 위해 OS 디스크를 다른 VM에 연결해야 하는 경우 복제된 VM과 LVM 이름이 충돌하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="02fe9-114">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="02fe9-115">OS 디스크에 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="02fe9-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="02fe9-116">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="02fe9-117">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="02fe9-118">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="02fe9-119">SUSE Studio 사용</span><span class="sxs-lookup"><span data-stu-id="02fe9-119">Use SUSE Studio</span></span>
<span data-ttu-id="02fe9-120">[SUSE Studio](http://www.susestudio.com) 에서는 Azure와 Hyper-V용 SLES 및 openSUSE 이미지를 쉽게 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="02fe9-121">고유한 SLES 및 openSUSE 이미지를 사용자 지정할 때는 이 방식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="02fe9-122">또한 SUSE는 [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007)에 SLES용 BYOS(Bring Your Own Subscription) 이미지도 게시하므로 VHD를 직접 작성하는 대신 이 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="02fe9-123">SUSE Linux Enterprise Server 11 SP4 준비</span><span class="sxs-lookup"><span data-stu-id="02fe9-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="02fe9-124">Hyper-V 관리자의 가운데 창에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="02fe9-125">**연결** 을 클릭하여 가상 컴퓨터 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="02fe9-126">업데이트를 다운로드하고 패키지를 설치할 수 있도록 SUSE Linux Enterprise 시스템을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="02fe9-127">모든 최신 패치로 시스템을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="02fe9-128">SLES 리포지토리에서 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="02fe9-129">chkconfig에서 waagent가 "on"으로 설정되어 있는지 확인하고 그렇지 않으면 자동 시작을 위해 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="02fe9-130">waagent 서비스가 실행 중인지 확인하고 그렇지 않으면 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="02fe9-131">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02fe9-132">이 작업을 수행하려면 "/boot/grub/menu.lst"를 텍스트 편집기에서 열고 다음 매개 변수가 기본 커널에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="02fe9-133">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="02fe9-134">/boot/grub/menu.lst 및 /etc/fstab 둘 다 디스크 ID(by-id) 대신 해당 UUID(by-uuid)를 사용하는 디스크를 참조하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="02fe9-135">디스크 UUID 가져오기</span><span class="sxs-lookup"><span data-stu-id="02fe9-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="02fe9-136">/dev/disk/by-id/를 사용하는 경우 적절한 by-uuid 값으로 /boot/grub/menu.lst 및 /etc/fstab를 모두 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="02fe9-137">변경 전</span><span class="sxs-lookup"><span data-stu-id="02fe9-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="02fe9-138">변경 후</span><span class="sxs-lookup"><span data-stu-id="02fe9-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="02fe9-139">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="02fe9-140">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="02fe9-141">"/etc/sysconfig/network/dhcp" 파일을 편집하여 `DHCLIENT_SET_HOSTNAME` 매개 변수를 다음과 같이 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="02fe9-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="02fe9-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="02fe9-143">"/etc/sudoers"에서 다음 줄이 있으면 주석 처리하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="02fe9-144">Defaults targetpw # 대상 사용자의 암호를 요구합니다. 즉, root ALL ALL=(ALL) ALL # WARNING!</span><span class="sxs-lookup"><span data-stu-id="02fe9-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="02fe9-145">'Defaults targetpw'와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="02fe9-146">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="02fe9-147">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-147">This is usually the default.</span></span>
14. <span data-ttu-id="02fe9-148">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="02fe9-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="02fe9-149">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="02fe9-150">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="02fe9-151">Azure Linux 에이전트를 설치한 후(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="02fe9-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## 참고: 이것을 필요한 대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="02fe9-153">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="02fe9-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="02fe9-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="02fe9-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="02fe9-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="02fe9-156">logout</span><span class="sxs-lookup"><span data-stu-id="02fe9-156">logout</span></span>
16. <span data-ttu-id="02fe9-157">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="02fe9-158">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="02fe9-159">openSUSE 13.1+ 준비</span><span class="sxs-lookup"><span data-stu-id="02fe9-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="02fe9-160">Hyper-V 관리자의 가운데 창에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="02fe9-161">**연결** 을 클릭하여 가상 컴퓨터 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="02fe9-162">셸에서 '`zypper lr`' 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="02fe9-163">이 명령에서 다음과 유사한 출력이 반환되는 경우 리포지토리가 예상대로 구성된 것입니다. 이 경우 아무 것도 조정할 필요가 없습니다(버전 번호는 다를 수 있음).</span><span class="sxs-lookup"><span data-stu-id="02fe9-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="02fe9-164">명령이 "정의된 리포지토리가 없습니다..."를 반환하면 다음 명령을 사용하여 해당 리포지토리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="02fe9-165">그런 다음 '`zypper lr`' 명령을 다시 실행하여 리포지토리가 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="02fe9-166">관련된 업데이트 리포지토리 중 하나가 사용되도록 설정되어 있지 않은 경우 다음 명령을 사용하여 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="02fe9-167">커널을 사용 가능한 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="02fe9-168">또는 모든 최신 패치로 시스템을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="02fe9-169">Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="02fe9-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="02fe9-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="02fe9-171">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="02fe9-172">이 작업을 수행하려면 "/boot/grub/menu.lst"를 텍스트 편집기에서 열고 다음 매개 변수가 기본 커널에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="02fe9-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="02fe9-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="02fe9-174">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="02fe9-175">또한 커널 부팅 줄에 다음 매개 변수가 있는 경우 해당 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="02fe9-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="02fe9-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="02fe9-177">"/etc/sysconfig/network/dhcp" 파일을 편집하여 `DHCLIENT_SET_HOSTNAME` 매개 변수를 다음과 같이 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="02fe9-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="02fe9-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="02fe9-179">**중요:** "/etc/sudoers"에서 다음 줄이 있으면 주석 처리하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="02fe9-180">Defaults targetpw # 대상 사용자의 암호를 요구합니다. 즉, root ALL ALL=(ALL) ALL # WARNING!</span><span class="sxs-lookup"><span data-stu-id="02fe9-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="02fe9-181">'Defaults targetpw'와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="02fe9-182">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="02fe9-183">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-183">This is usually the default.</span></span>
10. <span data-ttu-id="02fe9-184">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="02fe9-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="02fe9-185">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="02fe9-186">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="02fe9-187">Azure Linux 에이전트를 설치한 후(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="02fe9-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## 참고: 이것을 필요한 대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="02fe9-189">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="02fe9-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="02fe9-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="02fe9-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="02fe9-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="02fe9-192">logout</span><span class="sxs-lookup"><span data-stu-id="02fe9-192">logout</span></span>
12. <span data-ttu-id="02fe9-193">시작할 때 Azure Linux 에이전트가 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="02fe9-194">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="02fe9-195">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02fe9-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02fe9-196">Next steps</span></span>
<span data-ttu-id="02fe9-197">이제 SUSE Linux 가상 하드 디스크를 사용하여 Azure에서 새 가상 컴퓨터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02fe9-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="02fe9-198">.vhd 파일을 Azure에 처음으로 업로드하는 경우 [Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에서 2단계 및 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02fe9-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

