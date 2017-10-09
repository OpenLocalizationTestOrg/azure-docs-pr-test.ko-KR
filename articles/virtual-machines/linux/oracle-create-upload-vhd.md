---
title: "aaaCreate 및 Oracle Linux VHD 업로드 | Microsoft Docs"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD)는 Oracle Linux 운영 체제를 포함 합니다."
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
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="204a6-103">Azure용 Oracle Linux 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="204a6-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="204a6-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="204a6-104">Prerequisites</span></span>
<span data-ttu-id="204a6-105">이 문서는 Oracle Linux 운영 체제 tooa 가상 하드 디스크로 이미 설치한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="204a6-106">여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="204a6-107">자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="204a6-108">Oracle Linux 설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="204a6-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="204a6-109">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="204a6-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="204a6-110">Oracle Red Hat 호환 커널 및 해당 UEK3(Unbreakable Enterprise Kernel)은 모두 Hyper-V 및 Azure에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="204a6-111">최상의 결과 있는지 tooupdate toohello 최신 커널 Oracle Linux VHD를 준비 하는 동안 모니터링할 하십시오.</span><span class="sxs-lookup"><span data-stu-id="204a6-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="204a6-112">Oracle의 UEK2 hello 필요한 드라이버를 포함 하지 않는 Hyper-v와 Azure에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="204a6-113">hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="204a6-114">Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="204a6-115">Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="204a6-116">OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이.</span><span class="sxs-lookup"><span data-stu-id="204a6-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="204a6-117">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="204a6-118">NUMA는 2.6.37 아래 Linux 커널 버전의 tooa 버그 때문에 더 큰 VM 크기에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="204a6-119">이 문제를 주로 영향을 미치는 분포를 사용 하 여 hello 업스트림 Red Hat 2.6.32 커널 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="204a6-120">(Waagent) hello Azure Linux 에이전트를 수동으로 설치는 자동으로 Linux 커널 hello에 대 한 hello GRUB 구성에서 NUMA를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="204a6-121">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="204a6-122">스왑 파티션을 hello OS 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="204a6-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="204a6-123">hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="204a6-124">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="204a6-125">모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="204a6-126">해당 hello 있는지 확인 `Addons` 리포지토리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="204a6-127">Hello 파일을 편집 `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), hello 줄을 변경 하 고 `enabled=0` 너무`enabled=1` 아래 **[ol6_addons]** 또는 **[ol7_addons]** 이 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="204a6-128">Oracle Linux 6.4 이상</span><span class="sxs-lookup"><span data-stu-id="204a6-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="204a6-129">Azure에서 가상 컴퓨터 toorun hello에 대 한 hello 운영 체제에서 특정 구성 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="204a6-130">Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="204a6-131">클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.</span><span class="sxs-lookup"><span data-stu-id="204a6-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="204a6-132">NetworkManager hello 다음 명령을 실행 하 여 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="204a6-133">**참고:** hello 패키지 아직 설치 되지 않은 오류 메시지와 함께이 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="204a6-134">예상된 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-134">This is expected.</span></span>
4. <span data-ttu-id="204a6-135">라는 파일을 만들어 **네트워크** hello에 `/etc/sysconfig/` hello 텍스트 다음 포함 된 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="204a6-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="204a6-136">라는 파일을 만들어 **ifcfg eth0** hello에 `/etc/sysconfig/network-scripts/` hello 텍스트 다음 포함 된 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="204a6-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="204a6-137">Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="204a6-138">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="204a6-139">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="204a6-140">Python pyasn1 hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="204a6-141">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="204a6-142">이 열린 toodo "/ boot/grub/menu.lst" 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:</span><span class="sxs-lookup"><span data-stu-id="204a6-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="204a6-143">또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="204a6-144">Oracle의 Red Hat 호환 커널에서 tooa 버그 인해 NUMA 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="204a6-145">또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="204a6-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="204a6-146">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="204a6-147">hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="204a6-148">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="204a6-149">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-149">This is usually hello default.</span></span>
11. <span data-ttu-id="204a6-150">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="204a6-151">hello 최신 버전은 2.0.15입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="204a6-152">설치 hello WALinuxAgent 패키지는 hello NetworkManager 제거 및 NetworkManager gnome 패키지는 제거 되지 않은 경우 이미 설명 된 대로 2 단계에서 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="204a6-153">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="204a6-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="204a6-154">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="204a6-155">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="204a6-156">Hello Azure Linux 에이전트를 설치한 후 (이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:</span><span class="sxs-lookup"><span data-stu-id="204a6-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="204a6-157">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="204a6-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="204a6-158">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="204a6-159">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="204a6-160">Oracle Linux 7.0</span><span class="sxs-lookup"><span data-stu-id="204a6-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="204a6-161">**Oracle Linux 7의 변경 내용**</span><span class="sxs-lookup"><span data-stu-id="204a6-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="204a6-162">하지만 Oracle Linux 7 가상 컴퓨터를 준비 하 고 Azure에 대 한 매우 유사 몇 가지 중요 한 차이점이 주목할 만한 Linux 6, tooOracle은입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="204a6-163">Red Hat 호환 커널 hello 및 Oracle의 UEK3 모두 Azure에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="204a6-164">hello UEK3 커널 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="204a6-165">hello NetworkManager 패키지 더 이상 hello Azure Linux 에이전트와 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="204a6-166">이 패키지는 기본적으로 설치되며 제거하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="204a6-167">이제 커널 매개 변수를 편집 하기 위해 hello 절차 (아래 참조) 변경 된 하므로 기본 부팅 로더를 hello GRUB2 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="204a6-168">XFS는 hello 기본 파일 시스템 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-168">XFS is now hello default file system.</span></span> <span data-ttu-id="204a6-169">원하는 경우에 여전히 hello ext4 파일 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="204a6-170">**구성 단계**</span><span class="sxs-lookup"><span data-stu-id="204a6-170">**Configuration steps**</span></span>

1. <span data-ttu-id="204a6-171">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="204a6-172">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="204a6-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="204a6-173">라는 파일을 만들어 **네트워크** hello에 `/etc/sysconfig/` hello 텍스트 다음 포함 된 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="204a6-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="204a6-174">라는 파일을 만들어 **ifcfg eth0** hello에 `/etc/sysconfig/network-scripts/` hello 텍스트 다음 포함 된 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="204a6-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="204a6-175">Udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙 생성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="204a6-176">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="204a6-177">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="204a6-178">Hello 다음 명령을 실행 하 여 hello pyasn1 python 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="204a6-179">Hello 명령 tooclear hello 현재 yum 메타 데이터를 다음를 실행 하 고 모든 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="204a6-180">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="204a6-181">이 열려 "/ 등/기본/grub" toodo 텍스트 편집기 및 편집 hello에 `GRUB_CMDLINE_LINUX` 예를 들어 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="204a6-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="204a6-182">또한 이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="204a6-183">또한 Nic 동안 OEL 7 명명 규칙을 새 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="204a6-184">또한 위의 toohello, 것이 좋습니다 너무*제거* 매개 변수 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="204a6-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="204a6-185">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="204a6-186">hello `crashkernel` 옵션이 수 있습니다, 원하는 경우 구성 하는 왼쪽 이지만이 매개 변수 감소할 hello hello 128MB 이상의 VM에서에서 사용 가능한 메모리 크기는 hello 더 작은 VM 크기에 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="204a6-187">편집 "/ 등/기본/grub" 완료 되 면 당 위에서 실행 같은 명령 toorebuild hello grub 구성이 hello:</span><span class="sxs-lookup"><span data-stu-id="204a6-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="204a6-188">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="204a6-189">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-189">This is usually hello default.</span></span>
12. <span data-ttu-id="204a6-190">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="204a6-191">Hello OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="204a6-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="204a6-192">hello Azure Linux 에이전트 Azure에서 프로 비전 한 후 연결 된 toohello VM은 hello 로컬 리소스 디스크를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="204a6-193">해당 하는 hello 로컬 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="204a6-194">Hello Azure Linux 에이전트를 설치한 후 (hello 이전 단계 참조) hello /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 수정:</span><span class="sxs-lookup"><span data-stu-id="204a6-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="204a6-195">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="204a6-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="204a6-196">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="204a6-197">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="204a6-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="204a6-198">Next steps</span></span>
<span data-ttu-id="204a6-199">사용자는 이제 준비 toouse Azure에서 Oracle Linux.vhd toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="204a6-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="204a6-200">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="204a6-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

