---
title: "Oracle Linux VHD 만들기 및 업로드 | Microsoft Docs"
description: "Oracle Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="5797e-103">Azure용 Oracle Linux 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="5797e-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="5797e-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5797e-104">Prerequisites</span></span>
<span data-ttu-id="5797e-105">이 문서에서는 가상 하드 디스크에 Oracle Linux 운영 체제를 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="5797e-106">.vhd 파일을 만드는 여러 도구가 있습니다(예: Hyper-V와 같은 가상화 솔루션).</span><span class="sxs-lookup"><span data-stu-id="5797e-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="5797e-107">자세한 내용은 [Hyper-V 역할 설치 및 가상 시스템 구성](http://technet.microsoft.com/library/hh846766.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5797e-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="5797e-108">Oracle Linux 설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="5797e-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="5797e-109">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5797e-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="5797e-110">Oracle Red Hat 호환 커널 및 해당 UEK3(Unbreakable Enterprise Kernel)은 모두 Hyper-V 및 Azure에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="5797e-111">최상의 결과를 얻으려면 Oracle Linux VHD를 준비할 때 최신 커널로 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="5797e-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="5797e-112">Oracle의 UEK2는 필수 드라이버를 포함하지 않으므로 Hyper-V 및 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="5797e-113">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="5797e-114">Hyper-V 관리자 또는 convert-vhd cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="5797e-115">Linux 시스템 설치 시에는 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="5797e-116">이렇게 하면 특히 문제 해결을 위해 OS 디스크를 다른 VM에 연결해야 하는 경우 복제된 VM과 LVM 이름이 충돌하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="5797e-117">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="5797e-118">2.6.37보다 낮은 Linux 커널 버전의 버그 때문에 더 큰 VM 크기에서는 NUMA가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="5797e-119">이 문제는 주로 업스트림 Red Hat 2.6.32 커널을 사용하는 분산에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="5797e-120">Azure Linux 에이전트(waagent)를 수동으로 설치하면 Linux 커널의 GRUB 구성에서 NUMA가 자동으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="5797e-121">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="5797e-122">OS 디스크에 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5797e-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="5797e-123">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="5797e-124">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="5797e-125">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="5797e-126">`Addons` 리포지토리가 사용되도록 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="5797e-127">파일 `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux)를 편집하고 이 파일의 **[ol6_addons]** 또는 **[ol7_addons]** 아래에서 줄 `enabled=0`을 `enabled=1`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="5797e-128">Oracle Linux 6.4 이상</span><span class="sxs-lookup"><span data-stu-id="5797e-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="5797e-129">가상 컴퓨터를 Azure에서 실행하려면 운영 체제에서 특정 구성 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="5797e-130">Hyper-V 관리자의 가운데 창에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="5797e-131">**연결** 을 클릭하여 가상 컴퓨터 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="5797e-132">다음 명령을 실행하여 NetworkManager를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="5797e-133">**참고:** 패키지가 아직 설치되어 있지 않은 경우 이 명령이 실패하고 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="5797e-134">예상된 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-134">This is expected.</span></span>
4. <span data-ttu-id="5797e-135">다음 텍스트가 포함된 **network** in the `/etc/sysconfig/` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="5797e-136">다음 텍스트가 포함된 **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="5797e-137">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="5797e-138">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="5797e-139">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="5797e-140">다음 명령을 실행하여 python-pyasn1을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="5797e-141">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="5797e-142">이 작업을 수행하려면 "/boot/grub/menu.lst"를 텍스트 편집기에서 열고 다음 매개 변수가 기본 커널에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="5797e-143">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="5797e-144">이 경우 Oracle Red Hat 호환 커널의 버그로 인해 NUMA가 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="5797e-145">위의 작업을 수행하는 동시에 다음 매개 변수도 *제거* 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="5797e-146">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="5797e-147">원하는 경우에는 `crashkernel` 옵션을 구성한 상태로 유지할 수도 있지만 이 매개 변수를 사용하는 경우 VM에서 사용 가능한 메모리의 양이 128MB 이상 감소하므로 VM 크기가 작은 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="5797e-148">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="5797e-149">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-149">This is usually the default.</span></span>
11. <span data-ttu-id="5797e-150">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="5797e-151">최신 버전은 2.0.15입니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="5797e-152">WALinuxAgent 패키지를 설치하면 NetworkManager 및 NetworkManager-gnome 패키지가 2단계에서 설명된 대로 아직 제거되지 않은 경우 이러한 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="5797e-153">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5797e-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="5797e-154">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="5797e-155">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="5797e-156">Azure Linux 에이전트를 설치한 후(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="5797e-157">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="5797e-158">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="5797e-159">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="5797e-160">Oracle Linux 7.0</span><span class="sxs-lookup"><span data-stu-id="5797e-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="5797e-161">**Oracle Linux 7의 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="5797e-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="5797e-162">Azure용으로 Oracle Linux 7 가상 컴퓨터를 준비하는 작업은 Oracle Linux 6과 매우 비슷하지만 다음과 같은 몇 가지 중요한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="5797e-163">Red Hat 호환 커널과 Oracle의 UEK3은 모두 Azure에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="5797e-164">UEK3 커널을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="5797e-165">NetworkManager 패키지가 더 이상 Azure Linux 에이전트와 충돌하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="5797e-166">이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="5797e-167">이제 GRUB2가 기본 부팅 로더로 사용되므로 커널 매개 변수를 편집하는 절차가 변경되었습니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="5797e-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="5797e-168">이제 XFS가 기본 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-168">XFS is now the default file system.</span></span> <span data-ttu-id="5797e-169">원하는 경우에는 ext4 파일 시스템도 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="5797e-170">**구성 단계**</span><span class="sxs-lookup"><span data-stu-id="5797e-170">**Configuration steps**</span></span>

1. <span data-ttu-id="5797e-171">Hyper-V 관리자에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="5797e-172">**연결** 을 클릭하여 가상 컴퓨터의 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="5797e-173">다음 텍스트가 포함된 **network** in the `/etc/sysconfig/` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="5797e-174">다음 텍스트가 포함된 **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="5797e-175">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="5797e-176">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="5797e-177">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="5797e-178">다음 명령을 실행하여 python-pyasn1 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="5797e-179">다음 명령을 실행하여 현재 yum 메타데이터를 지우고 모든 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="5797e-180">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="5797e-181">이렇게 하려면 텍스트 편집기에서 "/etc/default/grub"를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="5797e-182">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="5797e-183">NIC에 대한 새 OEL 7 명명 규칙도 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="5797e-184">위의 작업을 수행하는 동시에 다음 매개 변수도 *제거* 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="5797e-185">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="5797e-186">원하는 경우에는 `crashkernel` 옵션을 구성한 상태로 유지할 수도 있지만 이 매개 변수를 사용하는 경우 VM에서 사용 가능한 메모리의 양이 128MB 이상 감소하므로 VM 크기가 작은 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="5797e-187">위의 설명에 따라 "/etc/default/grub" 편집을 완료한 후에는 다음 명령을 실행하여 grub 구성을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="5797e-188">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="5797e-189">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-189">This is usually the default.</span></span>
12. <span data-ttu-id="5797e-190">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="5797e-191">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="5797e-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="5797e-192">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="5797e-193">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="5797e-194">Azure Linux 에이전트를 설치한 후(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="5797e-195">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="5797e-196">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="5797e-197">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5797e-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5797e-198">Next steps</span></span>
<span data-ttu-id="5797e-199">이제 Oracle Linux .vhd를 사용하여 Azure에서 새 가상 컴퓨터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5797e-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="5797e-200">.vhd 파일을 Azure에 처음으로 업로드하는 경우 [Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에서 2단계 및 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5797e-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

