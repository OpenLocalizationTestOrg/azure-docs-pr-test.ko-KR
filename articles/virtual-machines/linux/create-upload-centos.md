---
title: "aaaCreate 및 Azure에서 Linux CentOS 기반 VHD 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) CentOS 기반 Linux 운영 체제를 포함 합니다."
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
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="c4267-103">Azure용 CentOS 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="c4267-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="c4267-104">Azure용 CentOS 6.x 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="c4267-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="c4267-105">Azure용 CentOS 7.0 이상 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="c4267-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="c4267-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4267-106">Prerequisites</span></span>
<span data-ttu-id="c4267-107">이 문서는 CentOS 이미 설치한 것으로 가정 (또는 유사한 파생물) Linux 운영 체제 tooa 가상 하드 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="c4267-108">여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="c4267-109">자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="c4267-110">**CentOS 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="c4267-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="c4267-111">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4267-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="c4267-112">hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="c4267-113">Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="c4267-114">VirtualBox를 사용 하는 경우 선택 하는 것이 즉 **고정 크기** 으로 반대로 toohello 기본 hello 디스크를 만들 때 동적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="c4267-115">hello Linux 시스템을 설치할 때 *권장* LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="c4267-116">OS 디스크 연결 toobe tooanother 해야 합니다. 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 방지 합니다이 문제 해결을 위해 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="c4267-117">데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="c4267-118">UDF 파일 시스템 탑재에 대한 커널 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="c4267-119">첫 번째 부팅 Azure hello에-프로비저닝 구성 toohello Linux VM은 연결 된 toohello 게스트 UDF로 포맷 된 미디어를 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="c4267-120">hello Azure Linux 에이전트는 해당 구성을 수 toomount hello UDF 파일 시스템 tooread 수 하 고 hello VM을 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="c4267-121">2.6.37 버전 미만의 Linux 커널은 VM 크기가 더 클 때 Hyper-V에서 NUMA를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="c4267-122">이 문제를 주로 영향 업스트림 hello를 사용 하 여 이전 분포 Red Hat 2.6.32 커널 RHEL 6.6 (커널 2.6.32 504)에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="c4267-123">2.6.32-504 설정 해야 하는 보다 2.6.37, 다음 보다 오래 된 사용자 지정 커널 또는 이전 RHEL 기반 커널을 실행 하는 시스템 부팅 매개 변수를 hello `numa=off` hello 커널 grub.conf의 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="c4267-124">자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4267-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="c4267-125">스왑 파티션을 hello OS 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c4267-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="c4267-126">hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="c4267-127">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="c4267-128">모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="c4267-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="c4267-129">CentOS 6.x</span></span>

1. <span data-ttu-id="c4267-130">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="c4267-131">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="c4267-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="c4267-132">CentOS 6의 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="c4267-133">Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="c4267-134">Hello 파일 만들기 또는 편집 `/etc/sysconfig/network` hello 텍스트 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="c4267-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="c4267-135">Hello 파일 만들기 또는 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 텍스트 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="c4267-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="c4267-136">Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="c4267-137">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="c4267-138">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="c4267-139">Hello Azure 데이터 센터 내에 호스팅되는 toouse hello OpenLogic 미러를 원하는 경우 hello 바꿉니다 `/etc/yum.repos.d/CentOS-Base.repo` 저장소 다음 hello로는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="c4267-140">Hello도 추가 **[openlogic]** hello Azure Linux 에이전트와 같은 추가 패키지를 포함 하는 저장소:</span><span class="sxs-lookup"><span data-stu-id="c4267-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

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
    <span data-ttu-id="c4267-141">hello이 가이드의 나머지 부분 가정 사용 하는 hello 이상 `[openlogic]` 리포지토리 사용된 tooinstall hello Azure Linux 에이전트 아래 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="c4267-142">다음 줄 too/etc/yum.conf hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="c4267-143">Hello 명령 tooclear hello 현재 yum 메타 데이터 및 업데이트 hello 시스템 hello 최신 패키지와 함께 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="c4267-144">CentOS의 이전 버전에 대 한 이미지를 만드는 경우가 아니면 모든 hello tooupdate toohello를 최신 패키지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="c4267-145">이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="c4267-146">(선택 사항) Linux Integration Services (LIS) hello에 대 한 hello 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="c4267-147">hello 단계는 **필요한** CentOS 6.3 및 이전 버전 및 이후 릴리스에 대 한 선택 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="c4267-148">Hello에서 hello 수동 설치 지침을 따를 수 또는 [LIS 다운로드 페이지](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="c4267-149">Hello Azure Linux 에이전트 및 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="c4267-150">hello WALinuxAgent 패키지는 제거 되지 않은 경우 이미 3 단계에 설명 된 대로 NetworkManager hello 및 NetworkManager gnome 패키지 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="c4267-151">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="c4267-152">toodo이,이 오픈 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="c4267-153">또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="c4267-154">또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="c4267-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="c4267-155">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="c4267-156">hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="c4267-157">CentOS 6.5 및 이전 버전도 hello 커널 매개 변수를 설정 해야 `numa=off`합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="c4267-158">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4267-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="c4267-159">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="c4267-160">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-160">This is usually hello default.</span></span>

15. <span data-ttu-id="c4267-161">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c4267-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="c4267-162">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="c4267-163">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="c4267-164">Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조)의 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게:</span><span class="sxs-lookup"><span data-stu-id="c4267-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="c4267-165">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="c4267-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="c4267-166">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="c4267-167">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="c4267-168">CentOS 7.0 이상</span><span class="sxs-lookup"><span data-stu-id="c4267-168">CentOS 7.0+</span></span>
<span data-ttu-id="c4267-169">**CentOS 7 및 유사한 파생 버전의 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="c4267-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="c4267-170">그러나 몇 가지 중요 한 차이점이 주목할 만한 매우 유사한 tooCentOS 6는 CentOS 7 가상 컴퓨터를 Azure에 대 한 준비:</span><span class="sxs-lookup"><span data-stu-id="c4267-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="c4267-171">hello NetworkManager 패키지 더 이상 hello Azure Linux 에이전트와 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="c4267-172">이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="c4267-173">이제 커널 매개 변수를 편집 하기 위해 hello 절차 (아래 참조) 변경 된 하므로 기본 부팅 로더를 hello GRUB2 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="c4267-174">XFS는 hello 기본 파일 시스템 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-174">XFS is now hello default file system.</span></span> <span data-ttu-id="c4267-175">원하는 경우에 여전히 hello ext4 파일 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="c4267-176">**구성 단계**</span><span class="sxs-lookup"><span data-stu-id="c4267-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="c4267-177">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="c4267-178">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="c4267-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="c4267-179">Hello 파일 만들기 또는 편집 `/etc/sysconfig/network` hello 텍스트 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="c4267-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="c4267-180">Hello 파일 만들기 또는 편집 `/etc/sysconfig/network-scripts/ifcfg-eth0` hello 텍스트 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="c4267-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="c4267-181">Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="c4267-182">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="c4267-183">Hello Azure 데이터 센터 내에 호스팅되는 toouse hello OpenLogic 미러를 원하는 경우 hello 바꿉니다 `/etc/yum.repos.d/CentOS-Base.repo` 저장소 다음 hello로는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="c4267-184">Hello도 추가 **[openlogic]** hello Azure Linux 에이전트에 대 한 패키지를 포함 하는 저장소:</span><span class="sxs-lookup"><span data-stu-id="c4267-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="c4267-185">hello이 가이드의 나머지 부분 가정 사용 하는 hello 이상 `[openlogic]` 리포지토리 사용된 tooinstall hello Azure Linux 에이전트 아래 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="c4267-186">Hello 명령 tooclear hello 현재 yum 메타 데이터를 다음를 실행 하 고 모든 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="c4267-187">CentOS의 이전 버전에 대 한 이미지를 만드는 경우가 아니면 모든 hello tooupdate toohello를 최신 패키지 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="c4267-188">이 명령을 실행한 후 다시 부팅해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="c4267-189">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="c4267-190">toodo이,이 오픈 `/etc/default/grub` 텍스트 편집기 및 편집 hello에 `GRUB_CMDLINE_LINUX` 예를 들어 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="c4267-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="c4267-191">또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="c4267-192">또한 Nic 동안 CentOS 7 명명 규칙을 새 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="c4267-193">또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="c4267-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="c4267-194">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="c4267-195">hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="c4267-196">완료 되 면 편집 `/etc/default/grub` 당 위에서 실행 같은 명령 toorebuild hello grub 구성이 hello:</span><span class="sxs-lookup"><span data-stu-id="c4267-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="c4267-197">Hello 이미지에서 작성 하는 경우 **VMWare, VirtualBox 또는 KVM:** 확인 hello Hyper-v 드라이버 hello initramfs에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="c4267-198">`/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="c4267-199">Hello initramfs 다시 작성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c4267-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="c4267-200">Hello Azure Linux 에이전트 및 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="c4267-201">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c4267-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="c4267-202">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="c4267-203">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="c4267-204">Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조)의 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게:</span><span class="sxs-lookup"><span data-stu-id="c4267-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="c4267-205">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="c4267-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="c4267-206">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="c4267-207">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4267-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4267-208">Next steps</span></span>
<span data-ttu-id="c4267-209">사용자는 이제 준비 toouse Azure에서 CentOS Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c4267-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="c4267-210">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4267-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

