---
title: "aaaCreate 및 SUSE Linux VHD를 Azure에 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) SUSE Linux 운영 체제를 포함 합니다."
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
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="d6d33-103">Azure용 SLES 또는 openSUSE 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="d6d33-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="d6d33-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d6d33-104">Prerequisites</span></span>
<span data-ttu-id="d6d33-105">이 문서에서는 SUSE 또는 openSUSE Linux 운영 체제 tooa 가상 하드 디스크를 이미 설치 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="d6d33-106">여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="d6d33-107">자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="d6d33-108">SLES/openSUSE 설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="d6d33-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="d6d33-109">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6d33-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="d6d33-110">hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="d6d33-111">Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="d6d33-112">Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="d6d33-113">OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이.</span><span class="sxs-lookup"><span data-stu-id="d6d33-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="d6d33-114">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="d6d33-115">스왑 파티션을 hello OS 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d6d33-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="d6d33-116">hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="d6d33-117">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="d6d33-118">모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="d6d33-119">SUSE Studio 사용</span><span class="sxs-lookup"><span data-stu-id="d6d33-119">Use SUSE Studio</span></span>
<span data-ttu-id="d6d33-120">[SUSE Studio](http://www.susestudio.com) 에서는 Azure와 Hyper-V용 SLES 및 openSUSE 이미지를 쉽게 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="d6d33-121">이 hello SLES 및 openSUSE 사용자 고유의 이미지를 사용자 지정 하기 위한 방법을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="d6d33-122">대체 toobuilding로 사용자 고유의 VHD, SUSE 엔터티에도 BYOS (Bring Your 자신의 구독의) 이미지에서 SLES에 대 한 [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="d6d33-123">SUSE Linux Enterprise Server 11 SP4 준비</span><span class="sxs-lookup"><span data-stu-id="d6d33-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="d6d33-124">Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="d6d33-125">클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.</span><span class="sxs-lookup"><span data-stu-id="d6d33-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="d6d33-126">SUSE Linux Enterprise 시스템 tooallow 등록 것 toodownload 업데이트 및 설치 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="d6d33-127">Hello 최신 패치 사용 hello 시스템을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="d6d33-128">Hello SLES 리포지토리에서 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="d6d33-129">Chkconfig에서 "에서" waagent 너무 설정 되어 있는지를 확인 하 고 그렇지 않은 경우 자동 시작에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="d6d33-130">waagent 서비스가 실행 중인지 확인하고 그렇지 않으면 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="d6d33-131">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="d6d33-132">이 열린 toodo "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:</span><span class="sxs-lookup"><span data-stu-id="d6d33-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="d6d33-133">이 방법을 사용 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="d6d33-134">해당 /boot/grub/menu.lst 및/등/fstab hello 디스크 ID (id 별) 대신 해당 UUID (uuid 여)을 사용 하 여 두 참조 hello 디스크를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="d6d33-135">디스크 UUID 가져오기</span><span class="sxs-lookup"><span data-stu-id="d6d33-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="d6d33-136">경우 /dev/disk/by-id /는 /boot/grub/menu.lst 및/등/fstab hello uuid 하 여 적절 한 값으로 업데이트 사용</span><span class="sxs-lookup"><span data-stu-id="d6d33-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="d6d33-137">변경 전</span><span class="sxs-lookup"><span data-stu-id="d6d33-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="d6d33-138">변경 후</span><span class="sxs-lookup"><span data-stu-id="d6d33-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="d6d33-139">Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="d6d33-140">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="d6d33-141">Tooedit hello 파일 좋습니다 "/ 등/sysconfig/네트워크/dhcp" hello 변경 `DHCLIENT_SET_HOSTNAME` toohello 다음 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="d6d33-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="d6d33-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="d6d33-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="d6d33-143">"/ 등/sudoers"에서 주석으로 처리 하거나 hello 있을 경우 줄을 다음를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="d6d33-144">Targetpw 기본값 즉, 루트 모든 ALL=(ALL) 모든 hello 대상 사용자의 hello 암호 # 요청 # 경고!</span><span class="sxs-lookup"><span data-stu-id="d6d33-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="d6d33-145">'Defaults targetpw'와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="d6d33-146">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="d6d33-147">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-147">This is usually hello default.</span></span>
14. <span data-ttu-id="d6d33-148">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d6d33-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="d6d33-149">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="d6d33-150">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="d6d33-151">Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:</span><span class="sxs-lookup"><span data-stu-id="d6d33-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="d6d33-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 참고:이 toowhatever toobe 필요를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="d6d33-153">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="d6d33-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="d6d33-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="d6d33-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="d6d33-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="d6d33-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="d6d33-156">logout</span><span class="sxs-lookup"><span data-stu-id="d6d33-156">logout</span></span>
16. <span data-ttu-id="d6d33-157">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d6d33-158">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="d6d33-159">openSUSE 13.1+ 준비</span><span class="sxs-lookup"><span data-stu-id="d6d33-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="d6d33-160">Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="d6d33-161">클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.</span><span class="sxs-lookup"><span data-stu-id="d6d33-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="d6d33-162">Hello 셸 hello 명령을 실행 '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="d6d33-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="d6d33-163">이 명령을 반환 하는 경우 비슷한 toohello hello 저장소 예상-조정 없이 필요한 대로 구성 된 다음을 수행 (버전 번호가 다를 수 있습니다 참고)를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="d6d33-164">Hello 명령 "저장소 정의..."를 반환 하는 경우 다음 사용 하 여 다음 명령을 tooadd hello 이러한 리포지토리:</span><span class="sxs-lookup"><span data-stu-id="d6d33-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="d6d33-165">Hello 저장소 hello 명령을 실행 하 여 추가 된 확인할 수 있습니다 '`zypper lr`' 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="d6d33-166">Hello 관련 업데이트 저장소 중 하나를 사용 하지 않는 경우 다음 명령을 사용 하 여 사용:</span><span class="sxs-lookup"><span data-stu-id="d6d33-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="d6d33-167">Hello 커널 toohello 사용 가능한 최신 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="d6d33-168">또는 모든 hello 최신 패치 tooupdate hello 시스템:</span><span class="sxs-lookup"><span data-stu-id="d6d33-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="d6d33-169">Hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="d6d33-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="d6d33-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="d6d33-171">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="d6d33-172">toodo이,이 열기 "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="d6d33-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="d6d33-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="d6d33-174">이 방법을 사용 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="d6d33-175">또한 있을 경우 hello 커널 부팅 줄에서 매개 변수 뒤 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="d6d33-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="d6d33-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="d6d33-177">Tooedit hello 파일 좋습니다 "/ 등/sysconfig/네트워크/dhcp" hello 변경 `DHCLIENT_SET_HOSTNAME` toohello 다음 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="d6d33-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="d6d33-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="d6d33-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="d6d33-179">**중요:** "/ 등/sudoers" 주석으로 처리 하거나 있을 경우 줄을 다음 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="d6d33-180">Targetpw 기본값 즉, 루트 모든 ALL=(ALL) 모든 hello 대상 사용자의 hello 암호 # 요청 # 경고!</span><span class="sxs-lookup"><span data-stu-id="d6d33-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="d6d33-181">'Defaults targetpw'와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="d6d33-182">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="d6d33-183">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-183">This is usually hello default.</span></span>
10. <span data-ttu-id="d6d33-184">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d6d33-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="d6d33-185">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="d6d33-186">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="d6d33-187">Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:</span><span class="sxs-lookup"><span data-stu-id="d6d33-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="d6d33-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048; # 참고:이 toowhatever toobe 필요를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="d6d33-189">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="d6d33-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="d6d33-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="d6d33-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="d6d33-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="d6d33-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="d6d33-192">logout</span><span class="sxs-lookup"><span data-stu-id="d6d33-192">logout</span></span>
12. <span data-ttu-id="d6d33-193">시작 시 Azure Linux 에이전트를 실행 하는 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="d6d33-194">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="d6d33-195">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6d33-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6d33-196">Next steps</span></span>
<span data-ttu-id="d6d33-197">사용자는 이제 준비 toouse Azure에서 SUSE Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="d6d33-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="d6d33-198">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6d33-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

