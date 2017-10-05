---
title: "Azure에서 CentOS 기반 Linux VHD 만들기 및 업로드"
description: "CentOS 기반 Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="bcc68-103">Azure용 CentOS 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="bcc68-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="bcc68-104">Azure용 CentOS 6.x 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="bcc68-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="bcc68-105">Azure용 CentOS 7.0 이상 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="bcc68-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="bcc68-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bcc68-106">Prerequisites</span></span>
<span data-ttu-id="bcc68-107">이 문서에서는 가상 하드 디스크에 CentOS 또는 그와 비슷한 파생 Linux 운영 체제를 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="bcc68-108">.vhd 파일을 만드는 여러 도구가 있습니다(예: Hyper-V와 같은 가상화 솔루션).</span><span class="sxs-lookup"><span data-stu-id="bcc68-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="bcc68-109">자세한 내용은 [Hyper-V 역할 설치 및 가상 시스템 구성](http://technet.microsoft.com/library/hh846766.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcc68-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="bcc68-110">**CentOS 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="bcc68-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="bcc68-111">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcc68-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="bcc68-112">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="bcc68-113">Hyper-V 관리자 또는 convert-vhd cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="bcc68-114">VirtualBox를 사용하면 디스크를 만들 때 기본적으로 동적 할당되지 않고 **고정 크기**가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="bcc68-115">Linux 시스템 설치 시에는 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 *좋습니다*.</span><span class="sxs-lookup"><span data-stu-id="bcc68-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="bcc68-116">이렇게 하면 특히 문제 해결을 위해 OS 디스크를 다른 VM에 연결해야 하는 경우 복제된 VM과 LVM 이름이 충돌하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="bcc68-117">데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="bcc68-118">UDF 파일 시스템 탑재에 대한 커널 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="bcc68-119">Azure에서 처음 부팅 시 프로비저닝 구성이 게스트에 연결된 UDF 형식의 미디어를 통해 Linux VM에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="bcc68-120">Azure Linux 에이전트는 해당 구성을 읽고 VM을 프로비전하기 위해 UDF 파일 시스템을 탑재할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="bcc68-121">2.6.37 버전 미만의 Linux 커널은 VM 크기가 더 클 때 Hyper-V에서 NUMA를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="bcc68-122">이 문제는 주로 업스트림 Red Hat 2.6.32 커널을 사용하는 이전 배포에 영향을 주며 RHEL 6.6(kernel-2.6.32-504)에서는 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="bcc68-123">2.6.37보다 오래된 사용자 지정 커널 또는 2.6.32-504보다 오래된 RHEL 기반 커널을 실행하는 시스템의 경우 grub.conf의 커널 명령줄에 부트 매개 변수 `numa=off`</span><span class="sxs-lookup"><span data-stu-id="bcc68-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="bcc68-124">자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcc68-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="bcc68-125">OS 디스크에 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bcc68-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="bcc68-126">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="bcc68-127">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bcc68-128">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="bcc68-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="bcc68-129">CentOS 6.x</span></span>

1. <span data-ttu-id="bcc68-130">Hyper-V 관리자에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="bcc68-131">**연결** 을 클릭하여 가상 컴퓨터의 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="bcc68-132">CentOS 6에서 NetworkManager는 Azure Linux 에이전트 작동을 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="bcc68-133">다음 명령을 실행하여 이 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="bcc68-134">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="bcc68-135">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="bcc68-136">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bcc68-137">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="bcc68-138">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="bcc68-139">Azure 데이터 센터 내에서 호스트되는 OpenLogic 미러를 사용하려면 `/etc/yum.repos.d/CentOS-Base.repo` 파일을 다음 리포지토리로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="bcc68-140">그러면 Azure Linux 에이전트와 같은 추가 패키지가 포함된 **[openlogic]** 리포지토리도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="bcc68-141">이 가이드의 나머지 부분에서는 최소한 `[openlogic]` 리포지토리를 사용한다고 가정합니다. 아래 단계에서는 이 리포지토리를 사용하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="bcc68-142">/etc/yum.conf에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="bcc68-143">다음 명령을 실행하여 현재 yum 메타데이터를 지우고 최신 패키지로 시스템을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="bcc68-144">이전 버전의 CentOS에 대한 이미지를 만드는 경우가 아니면 모든 패키지를 최신으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="bcc68-145">이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="bcc68-146">(선택 사항) LIS(Linux 통합 서비스)용 드라이버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="bcc68-147">이 단계는 CentOS 6.3 및 이전 버전의 경우는 **필수**이고 최신 릴리스의 경우는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="bcc68-148">또는 [LIS 다운로드 페이지](https://go.microsoft.com/fwlink/?linkid=403033)의 수동 설치 지침에 따르고 VM에 RPM을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="bcc68-149">Azure Linux 에이전트 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="bcc68-150">WALinuxAgent 패키지는 3단계에서 설명한 대로 NetworkManager 및 NetworkManager-gnome 패키지가 아직 제거되지 않은 경우 이러한 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="bcc68-151">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bcc68-152">이 작업을 수행하려면 `/boot/grub/menu.lst` 를 텍스트 편집기에서 열고 기본 커널이 다음 매개 변수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="bcc68-153">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="bcc68-154">위의 작업을 수행하는 동시에 다음 매개 변수도 *제거* 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="bcc68-155">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="bcc68-156">원하는 경우에는 `crashkernel` 옵션을 구성한 상태로 유지할 수도 있지만 이 매개 변수를 사용하는 경우 VM에서 사용 가능한 메모리의 양이 128MB 이상 감소하므로 VM 크기가 작은 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="bcc68-157">또한 CentOS 6.5 및 이전 버전에서는 커널 매개 변수 `numa=off`를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="bcc68-158">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcc68-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="bcc68-159">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bcc68-160">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-160">This is usually the default.</span></span>

15. <span data-ttu-id="bcc68-161">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="bcc68-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="bcc68-162">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bcc68-163">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bcc68-164">Azure Linux 에이전트를 설치한 후(이전 단계 참조) `/etc/waagent.conf` 에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="bcc68-165">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="bcc68-166">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bcc68-167">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="bcc68-168">CentOS 7.0 이상</span><span class="sxs-lookup"><span data-stu-id="bcc68-168">CentOS 7.0+</span></span>
<span data-ttu-id="bcc68-169">**CentOS 7 및 유사한 파생 버전의 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="bcc68-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="bcc68-170">Azure용으로 CentOS 7 가상 컴퓨터를 준비하는 작업은 CentOS 6과 매우 비슷하지만 다음과 같은 몇 가지 중요한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="bcc68-171">NetworkManager 패키지가 더 이상 Azure Linux 에이전트와 충돌하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="bcc68-172">이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="bcc68-173">이제 GRUB2가 기본 부팅 로더로 사용되므로 커널 매개 변수를 편집하는 절차가 변경되었습니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="bcc68-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="bcc68-174">이제 XFS가 기본 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-174">XFS is now the default file system.</span></span> <span data-ttu-id="bcc68-175">원하는 경우에는 ext4 파일 시스템도 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="bcc68-176">**구성 단계**</span><span class="sxs-lookup"><span data-stu-id="bcc68-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="bcc68-177">Hyper-V 관리자에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="bcc68-178">**연결** 을 클릭하여 가상 컴퓨터의 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="bcc68-179">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="bcc68-180">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="bcc68-181">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bcc68-182">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="bcc68-183">Azure 데이터 센터 내에서 호스트되는 OpenLogic 미러를 사용하려면 `/etc/yum.repos.d/CentOS-Base.repo` 파일을 다음 리포지토리로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="bcc68-184">그러면 Azure Linux 에이전트의 패키지가 포함된 **[openlogic]** 리포지토리도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="bcc68-185">이 가이드의 나머지 부분에서는 최소한 `[openlogic]` 리포지토리를 사용한다고 가정합니다. 아래 단계에서는 이 리포지토리를 사용하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="bcc68-186">다음 명령을 실행하여 현재 yum 메타데이터를 지우고 모든 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="bcc68-187">이전 버전의 CentOS에 대한 이미지를 만드는 경우가 아니면 모든 패키지를 최신으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="bcc68-188">이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="bcc68-189">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bcc68-190">이렇게 하려면 텍스트 편집기에서 `/etc/default/grub`를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="bcc68-191">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="bcc68-192">NIC에 대한 새 CentOS 7 명명 규칙도 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="bcc68-193">위의 작업을 수행하는 동시에 다음 매개 변수도 *제거* 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="bcc68-194">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="bcc68-195">원하는 경우에는 `crashkernel` 옵션을 구성한 상태로 유지할 수도 있지만 이 매개 변수를 사용하는 경우 VM에서 사용 가능한 메모리의 양이 128MB 이상 감소하므로 VM 크기가 작은 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="bcc68-196">위의 설명에 따라 `/etc/default/grub` 편집을 완료한 후에는 다음 명령을 실행하여 grub 구성을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="bcc68-197">**VMWare VirtualBox 또는 KVM**에서 이미지를 빌드하는 경우 Hyper-V 드라이버가 initramfs에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="bcc68-198">`/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="bcc68-199">initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="bcc68-200">Azure Linux 에이전트 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="bcc68-201">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="bcc68-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="bcc68-202">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bcc68-203">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bcc68-204">Azure Linux 에이전트를 설치한 후(이전 단계 참조) `/etc/waagent.conf` 에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="bcc68-205">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="bcc68-206">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bcc68-207">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcc68-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcc68-208">Next steps</span></span>
<span data-ttu-id="bcc68-209">이제 CentOS Linux 가상 하드 디스크를 사용하여 Azure에서 새 가상 컴퓨터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc68-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="bcc68-210">.vhd 파일을 Azure에 처음으로 업로드하는 경우 [Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에서 2단계 및 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcc68-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

