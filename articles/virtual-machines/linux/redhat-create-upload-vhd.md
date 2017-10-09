---
title: "aaaCreate 및 Red Hat Enterprise Linux VHD를 Azure에서 사용 하기 위해 업로드 | Microsoft Docs"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD) Red Hat Linux 운영 체제를 포함 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="affe1-103">Azure용 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="affe1-104">이 문서에서는 살펴보겠습니다 어떻게 tooprepare Azure에서 사용 하기 위해 Red Hat Enterprise Linux (RHEL) 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="affe1-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="affe1-105">이 문서에 설명 된 RHEL hello 버전은 6.7 + 및 7.1 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="affe1-106">이 문서에서 설명 하는 준비에 대 한 hello 하이퍼바이저는 Hyper-v, 커널 기반 가상 컴퓨터 (KVM) 및 VMware입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="affe1-107">Red Hat 클라우드 액세스 프로그램에 참여하기 위한 자격 요구 사항에 대한 자세한 내용은 [Red Hat 클라우드 액세스 웹 사이트](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) 및 [Azure에서 실행 중인 RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="affe1-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="affe1-108">Hyper-V 관리자에서 Red Hat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="affe1-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="affe1-109">Prerequisites</span></span>
<span data-ttu-id="affe1-110">이 섹션에서는 hello Red Hat 웹 사이트와 설치 된 hello RHEL 이미지 tooa 가상 하드 디스크 (VHD)에서 ISO 파일을 이미 얻은 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="affe1-111">방법에 대 한 자세한 내용은 toouse Hyper-v 관리자는 운영 체제 이미지 tooinstall 참조 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="affe1-112">**RHEL 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="affe1-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="affe1-113">Azure는 hello VHDX 형식을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="affe1-114">Azure는 고정 VHD만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="affe1-115">Hyper-v 관리자 tooconvert hello 디스크 tooVHD 형식을 사용할 수 있습니다 또는 hello convert vhd cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="affe1-116">VirtualBox를 사용 하는 경우 선택 **고정 크기** 달리 toohello 기본 hello 디스크를 만드는 경우 옵션을 동적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="affe1-117">Azure에서는 1세대 가상 컴퓨터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="affe1-118">1 세대 가상 컴퓨터와 tooa 고정 크기 디스크를 동적 확장 VHDX toohello VHD 파일 형식에서 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="affe1-119">가상 컴퓨터의 세대는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="affe1-120">자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 하나요?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="affe1-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="affe1-121">hello VHD에 대 한 허용 되는 hello 최대 크기는 1, 023 GB입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="affe1-122">Hello Linux 운영 체제를 설치할 때 사용 하는 논리 볼륨 관리자 (LVM) 보다는 표준 파티션을 대부분의 설치에 대 한 hello 기본값 이기도 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="affe1-123">이 사례는 tooattach 운영 체제 디스크 tooanother 동일한 가상 컴퓨터 문제 해결을 위해 필요한 경우에 특히 복제 된 가상 컴퓨터와 LVM 이름 충돌을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="affe1-124">데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="affe1-125">UDF(범용 디스크 형식) 파일 시스템을 탑재하기 위한 커널 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="affe1-126">연결 된 toohello 게스트, hello UDF로 포맷 된 미디어에 있는 첫 번째 부팅 시 hello 프로 비전 구성 toohello Linux 가상 컴퓨터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="affe1-127">hello Azure Linux 에이전트는 해당 구성을 수 toomount hello UDF 파일 시스템 tooread 수 하 고 hello 가상 컴퓨터 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="affe1-128">Hello Linux 커널의 이전 버전은 2.6.37 보다 더 큰 가상 컴퓨터 크기와 비균일 메모리 액세스 (NUMA)를 Hyper-v에서 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="affe1-129">이 문제를 주로 영향 업스트림 hello를 사용 하는 이전 배포 Red Hat 2.6.32 커널 RHEL 6.6 (커널 2.6.32 504)에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="affe1-130">사용자 지정 커널을 실행 하는 시스템 2.6.37 보다 오래 된 또는 2.6.32-504 보다 오래 된 RHEL 기반 커널 hello를 설정 해야 `numa=off` grub.conf에 hello 커널 명령줄에서 부트 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="affe1-131">자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="affe1-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="affe1-132">스왑 파티션을 hello 운영 체제 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="affe1-133">hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="affe1-134">이 대 한 자세한 내용은 단계를 수행 하는 hello에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="affe1-135">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="affe1-136">Hyper-V 관리자에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="affe1-137">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="affe1-138">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="affe1-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="affe1-139">RHEL 6에서 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="affe1-140">Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="affe1-141">만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="affe1-142">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="affe1-143">Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="affe1-144">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="affe1-145">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="affe1-146">Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="affe1-147">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-148">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="affe1-149">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-150">toodo 열려이 수정 작업 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="affe1-151">Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="affe1-152">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="affe1-153">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="affe1-154">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-155">이 매개 변수 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 줄어든다는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="affe1-156">이 구성은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="affe1-157">6.5 및 이전 RHEL hello 설정 해야 `numa=off` 커널 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="affe1-158">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="affe1-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="affe1-159">해당 hello 보안 셸 (SSH) 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="affe1-160">/Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="affe1-161">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="affe1-162">설치 hello WALinuxAgent 패키지 3 단계에서 이미 제거 되지 않은 경우 NetworkManager hello 및 NetworkManager gnome 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="affe1-163">Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="affe1-164">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-165">로컬 리소스 디스크 임시 디스크가 고 hello 가상 컴퓨터 프로 비전 해제 하는 경우 비워야 수는 해당 hello를 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-166">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후 /etc/waagent.conf에 매개 변수를 적절 하 게 뒤 hello를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="affe1-167">구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="affe1-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="affe1-168">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="affe1-169">Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="affe1-170">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="affe1-171">Hyper-V 관리자에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="affe1-172">Hyper-v 관리자에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="affe1-173">클릭 **연결** tooopen hello 가상 컴퓨터에 대 한 콘솔 창.</span><span class="sxs-lookup"><span data-stu-id="affe1-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="affe1-174">만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="affe1-175">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="affe1-176">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="affe1-177">Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="affe1-178">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-179">toodo 열려이 수정 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="affe1-180">예:</span><span class="sxs-lookup"><span data-stu-id="affe1-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="affe1-181">Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="affe1-182">이 구성은 Nic 동안 hello 새 RHEL 7 명명 규칙 하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="affe1-183">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="affe1-184">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="affe1-185">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-186">이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="affe1-187">완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="affe1-188">해당 hello SSH 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="affe1-189">수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="affe1-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="affe1-190">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-191">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="affe1-192">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="affe1-193">Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="affe1-194">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-195">Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-196">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="affe1-197">Toounregister hello 구독 하려는 경우에 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="affe1-198">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="affe1-199">Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="affe1-200">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="affe1-201">KVM에서 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="affe1-202">KVM에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="affe1-203">Hello Red Hat 웹 사이트에서의 RHEL 6 hello KVM 이미지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="affe1-204">루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-204">Set a root password.</span></span>

    <span data-ttu-id="affe1-205">암호화 된 암호를 생성 하 고 hello hello 명령의 출력을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="affe1-206">guestfish 루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="affe1-207">변경 hello 두 번째 필드에서 hello 루트 사용자의 "!!"</span><span class="sxs-lookup"><span data-stu-id="affe1-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="affe1-208">toohello 암호화 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="affe1-209">KVM에서 hello qcow2 이미지에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="affe1-210">Hello 디스크 종류를 너무 설정**qcow2**, 너무 hello 가상 네트워크 인터페이스 장치 모델을 설정 하 고**virtio**합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="affe1-211">그런 다음 hello 가상 컴퓨터를 시작 하 고 루트로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="affe1-212">만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="affe1-213">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="affe1-214">Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="affe1-215">이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="affe1-216">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="affe1-217">Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="affe1-218">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-219">toodo이이 구성에서는 열기 `/boot/grub/menu.lst` 텍스트 편집기에서 해당 hello 기본 커널 hello 매개 변수 뒤에 포함 되 게 및:</span><span class="sxs-lookup"><span data-stu-id="affe1-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="affe1-220">Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="affe1-221">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="affe1-222">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="affe1-223">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-224">이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="affe1-225">6.5 및 이전 RHEL hello 설정 해야 `numa=off` 커널 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="affe1-226">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="affe1-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="affe1-227">Hyper-v 모듈 tooinitramfs를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="affe1-228">편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="affe1-229">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="affe1-230">Cloud-Init을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="affe1-231">해당 hello SSH 서버를 설치 및 부팅 시 toostart를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="affe1-232">/Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="affe1-233">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-234">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="affe1-235">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="affe1-236">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-237">Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-238">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후 수정에 대 한 매개 변수 뒤 hello **/etc/waagent.conf** 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="affe1-239">구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="affe1-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="affe1-240">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="affe1-241">KVM에 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="affe1-242">Hello qcow2 이미지 toohello VHD 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="affe1-243">먼저 hello 이미지 tooraw 형식을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="affe1-244">Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="affe1-245">그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:</span><span class="sxs-lookup"><span data-stu-id="affe1-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="affe1-246">Hello 원시 디스크 tooa 변환 고정 크기의 VHD:</span><span class="sxs-lookup"><span data-stu-id="affe1-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="affe1-247">KVM에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="affe1-248">Hello Red Hat 웹 사이트에서의 RHEL 7 hello KVM 이미지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="affe1-249">이 절차는 hello 예로 RHEL 7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="affe1-250">루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-250">Set a root password.</span></span>

    <span data-ttu-id="affe1-251">암호화 된 암호를 생성 하 고 hello hello 명령의 출력을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="affe1-252">guestfish 루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="affe1-253">변경 hello 두 번째 필드에서 루트 사용자의 "!!"</span><span class="sxs-lookup"><span data-stu-id="affe1-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="affe1-254">toohello 암호화 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="affe1-255">KVM에서 hello qcow2 이미지에서 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="affe1-256">Hello 디스크 종류를 너무 설정**qcow2**, 너무 hello 가상 네트워크 인터페이스 장치 모델을 설정 하 고**virtio**합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="affe1-257">그런 다음 hello 가상 컴퓨터를 시작 하 고 루트로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="affe1-258">만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="affe1-259">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="affe1-260">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="affe1-261">Red Hat 구독 tooenable 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="affe1-262">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-263">toodo이이 구성에서는 열기 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="affe1-264">예:</span><span class="sxs-lookup"><span data-stu-id="affe1-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="affe1-265">이 명령은 또한 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 하면 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="affe1-266">hello 명령 Nic 동안 RHEL 7 명명 규칙을 새 hello 하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="affe1-267">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="affe1-268">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="affe1-269">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-270">이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="affe1-271">완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="affe1-272">Hyper-V 모듈을 initramfs에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="affe1-273">`/etc/dracut.conf` 을 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="affe1-274">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="affe1-275">Cloud-Init을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="affe1-276">해당 hello SSH 서버를 설치 및 부팅 시 toostart를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="affe1-277">/Etc/ssh/sshd_config tooinclude hello 다음 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="affe1-278">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-279">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="affe1-280">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="affe1-281">Hello waagent 서비스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="affe1-282">Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="affe1-283">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-284">Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-285">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="affe1-286">구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="affe1-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="affe1-287">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="affe1-288">KVM에 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="affe1-289">Hello qcow2 이미지 toohello VHD 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="affe1-290">먼저 hello 이미지 tooraw 형식을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="affe1-291">Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="affe1-292">그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:</span><span class="sxs-lookup"><span data-stu-id="affe1-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="affe1-293">Hello 원시 디스크 tooa 변환 고정 크기의 VHD:</span><span class="sxs-lookup"><span data-stu-id="affe1-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="affe1-294">VMware에서 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="affe1-295">필수 조건</span><span class="sxs-lookup"><span data-stu-id="affe1-295">Prerequisites</span></span>
<span data-ttu-id="affe1-296">이 섹션은 VMWare에 RHEL 가상 컴퓨터가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="affe1-297">VMware에서 운영 체제 참조 하는 tooinstall 방법에 대 한 세부 정보에 대 한 [VMware 게스트 운영 체제 설치 가이드](http://partnerweb.vmware.com/GOSIG/home.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="affe1-298">Hello Linux 운영 체제를 설치할 때 사용 하는 LVM 보다는 표준 파티션을 대부분의 설치에 대 한 hello 기본값 이기도 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="affe1-299">운영 체제 디스크 문제 해결을 위해 연결 된 toobe tooanother 가상 컴퓨터를 현재까지 있어야 하는 경우에 특히 복제 된 가상 컴퓨터와 LVM 이름 충돌을 피해 야 할이 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="affe1-300">원하는 경우에는 데이터 디스크에서 LVM 또는 RAID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="affe1-301">스왑 파티션을 hello 운영 체제 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="affe1-302">Hello Linux 에이전트 toocreate hello 일시적인 리소스 디스크의 스왑 파일을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="affe1-303">다음에 나오는 hello 단계에서이 대 한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="affe1-304">Hello 가상 하드 디스크를 만들 때 선택 **저장소 가상 디스크를 단일 파일로**합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="affe1-305">VMWare에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="affe1-306">RHEL 6에서 NetworkManager hello Azure Linux 에이전트와 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="affe1-307">Hello 다음 명령을 실행 하 여이 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="affe1-308">라는 파일을 만들어 **네트워크** hello /etc/sysconfig/포함 된 디렉터리에서 다음 텍스트를 hello:</span><span class="sxs-lookup"><span data-stu-id="affe1-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="affe1-309">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="affe1-310">Hello udev 규칙 tooavoid hello 이더넷 인터페이스에 대 한 정적 규칙을 생성 이동 (또는 제거) 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="affe1-311">이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="affe1-312">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="affe1-313">Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="affe1-314">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-315">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="affe1-316">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-317">toodo이,이 오픈 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="affe1-318">예:</span><span class="sxs-lookup"><span data-stu-id="affe1-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="affe1-319">Toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 이렇게 하면 문제를 디버깅 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="affe1-320">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="affe1-321">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="affe1-322">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-323">이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="affe1-324">Hyper-v 모듈 tooinitramfs를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="affe1-325">편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="affe1-326">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="affe1-327">해당 hello SSH 서버를 설치 및 hello 기본 설정인 일반적으로 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="affe1-328">수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="affe1-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="affe1-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="affe1-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="affe1-330">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="affe1-331">Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="affe1-332">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-333">Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-334">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="affe1-335">구독 등록 취소 hello (필요한 경우) hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="affe1-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="affe1-336">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="affe1-337">Hello 가상 컴퓨터를 종료 하 고 hello VMDK 파일 tooa.vhd 파일로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="affe1-338">먼저 hello 이미지 tooraw 형식을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="affe1-339">Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="affe1-340">그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:</span><span class="sxs-lookup"><span data-stu-id="affe1-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="affe1-341">Hello 원시 디스크 tooa 변환 고정 크기의 VHD:</span><span class="sxs-lookup"><span data-stu-id="affe1-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="affe1-342">VMWare에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="affe1-343">만들기 또는 편집 hello `/etc/sysconfig/network` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="affe1-344">만들기 또는 편집 hello `/etc/sysconfig/network-scripts/ifcfg-eth0` 파일을 찾아 텍스트 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="affe1-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="affe1-345">확인 hello 다음 명령을 실행 하 여 hello 네트워크 서비스 부팅 시간에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="affe1-346">Red Hat 구독 tooenable hello 설치 hello RHEL 저장소에서 패키지의 hello 다음 명령을 실행 하 여 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="affe1-347">Azure에 대 한 프로그램 grub 구성 tooinclude 추가 커널 매개 변수에서 hello 커널 부팅 줄을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="affe1-348">toodo 열려이 수정 `/etc/default/grub` 텍스트 편집기 및 편집 hello `GRUB_CMDLINE_LINUX` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="affe1-349">예:</span><span class="sxs-lookup"><span data-stu-id="affe1-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="affe1-350">이 구성은 갖는지도 toohello 첫 번째 직렬 포트, Azure를 지원할 수 있는 모든 콘솔 메시지가 전송 되도록 지원 문제를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="affe1-351">또한 Nic 동안 RHEL 7 명명 규칙을 새 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="affe1-352">또한 매개 변수 뒤 hello를 제거 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="affe1-353">그래픽 도구 및 자동 부팅 toohello 직렬 포트에 보내 모든 hello 로그 toobe를 원하는 위치로 클라우드 환경에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="affe1-354">Hello에 두면 `crashkernel` 원하는 경우 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="affe1-355">이 매개 변수 줄어든다는 hello 사용 가능한 메모리 양은 128MB 이상의 hello 가상 컴퓨터에서 더 작은 가상 컴퓨터 크기에 문제가 될 수 있는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="affe1-356">완료 한 후 편집 `/etc/default/grub`실행 hello 명령 toorebuild hello grub 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="affe1-357">Hyper-v 모듈 tooinitramfs를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="affe1-358">`/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="affe1-359">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="affe1-360">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="affe1-361">이 설정은 일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-361">This setting is usually hello default.</span></span> <span data-ttu-id="affe1-362">수정 `/etc/ssh/sshd_config` 다음 줄 tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="affe1-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="affe1-363">hello WALinuxAgent 패키지 `WALinuxAgent-<version>`, toohello Red Hat extras 리포지토리 밀어넣은 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="affe1-364">Hello 다음 명령을 실행 하 여 hello extras 저장소 사용:</span><span class="sxs-lookup"><span data-stu-id="affe1-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="affe1-365">Hello 다음 명령을 실행 하 여 hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="affe1-366">Hello 운영 체제 디스크에서 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="affe1-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="affe1-367">hello Azure Linux 에이전트 hello 로컬 리소스 디스크 hello 가상 컴퓨터가 Azure에서 프로 비전 된 후 연결 된 toohello 가상 컴퓨터를 사용 하 여 스왑 공간을 자동으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="affe1-368">Note hello 로컬 리소스 디스크는 임시 디스크 및 hello 가상 컴퓨터가 프로 비전 해제 된 비울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="affe1-369">Hello 이전 단계에서 hello Azure Linux 에이전트를 설치한 후에 매개 변수 뒤 hello 수정 `/etc/waagent.conf` 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="affe1-370">Toounregister hello 구독 하려는 경우에 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="affe1-371">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="affe1-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="affe1-372">Hello 가상 컴퓨터를 종료 하 고 hello VMDK 파일 toohello VHD 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="affe1-373">먼저 hello 이미지 tooraw 형식을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="affe1-374">Hello hello 원시 이미지 크기는 1MB에 정렬 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="affe1-375">그렇지 않은 경우에 1MB와 hello 크기 tooalign 올림:</span><span class="sxs-lookup"><span data-stu-id="affe1-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="affe1-376">Hello 원시 디스크 tooa 변환 고정 크기의 VHD:</span><span class="sxs-lookup"><span data-stu-id="affe1-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="affe1-377">자동으로 kickstart 파일을 사용하여 ISO에서 Red Hat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="affe1-378">kickstart 파일에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="affe1-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="affe1-379">Hello 다음 콘텐츠를 포함 하는 뿐 파일 만들고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="affe1-380">활용 설치에 대 한 자세한 참조 hello [활용 설치 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="affe1-381">Hello 설치 시스템 액세스할 수 있는 hello 활용 파일을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="affe1-382">Hyper-V 관리자에서 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="affe1-383">Hello에 **가상 하드 디스크 연결** 페이지에서 **나중에 가상 하드 디스크 연결**, 및 새 가상 컴퓨터 마법사 완료 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="affe1-384">Hello 가상 컴퓨터 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="affe1-385">a.</span><span class="sxs-lookup"><span data-stu-id="affe1-385">a.</span></span>  <span data-ttu-id="affe1-386">새 가상 하드 디스크 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="affe1-387">있는지 tooselect 확인 **VHD 형식** 및 **고정 크기**합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="affe1-388">b.</span><span class="sxs-lookup"><span data-stu-id="affe1-388">b.</span></span>  <span data-ttu-id="affe1-389">Hello 설치 ISO toohello DVD 드라이브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="affe1-390">c.</span><span class="sxs-lookup"><span data-stu-id="affe1-390">c.</span></span>  <span data-ttu-id="affe1-391">CD에서 hello BIOS tooboot를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="affe1-392">Hello 가상 컴퓨터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-392">Start hello virtual machine.</span></span> <span data-ttu-id="affe1-393">Hello 설치 가이드에 표시 되 면 키를 눌러 **탭** tooconfigure hello 부팅 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="affe1-394">Enter `inst.ks=<hello location of hello kickstart file>` hello 부팅 옵션 및 키를 눌러 hello 끝 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="affe1-395">Hello 설치 toofinish 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="affe1-396">완료 되 면 hello 가상 컴퓨터 종료 됩니다. 자동으로.</span><span class="sxs-lookup"><span data-stu-id="affe1-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="affe1-397">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="affe1-398">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="affe1-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="affe1-399">비 Hyper-v 하이퍼바이저를 사용 하는 경우 초기 RAM 디스크 hello에에서 hello Hyper-v 드라이버를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="affe1-400">경우에 따라 Linux 설치 관리자가 포함 되지 않을 수 hello 드라이버 Hyper-v에 대 한 hello 초기 RAM 디스크 (initrd 또는 initramfs)에서 Linux Hyper-v 환경에서 실행 되 고 있는지를 검색 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="affe1-401">다른 가상화 (즉, Virtualbox, Xen 등)의 시스템 tooprepare Linux 이미지를 사용 하는 경우 적어도 hv_vmbus hello toorebuild initrd tooensure 할 수 있습니다 및 hv_storvsc 커널 모듈 hello 초기 RAM 디스크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="affe1-402">이것은 알려진된 문제 이상 hello 업스트림 Red Hat 배포를 기반으로 하는 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="affe1-403">tooresolve이이 문제는 Hyper-v 모듈 tooinitramfs를 추가 하 고 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="affe1-404">편집 `/etc/dracut.conf`, hello 다음 콘텐츠를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="affe1-405">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="affe1-406">자세한 내용은 hello 정보에 대 한 참조 [initramfs 다시 작성](https://access.redhat.com/solutions/1958)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="affe1-407">다음 단계</span><span class="sxs-lookup"><span data-stu-id="affe1-407">Next steps</span></span>
<span data-ttu-id="affe1-408">사용자는 이제 준비 toouse Azure에서 Red Hat Enterprise Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="affe1-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="affe1-409">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="affe1-410">Red Hat Enterprise Linux toorun는 hello 하이퍼바이저에 대 한 자세한 내용은 인증에 대 한 참조 [hello Red Hat 웹 사이트](https://access.redhat.com/certified-hypervisors)합니다.</span><span class="sxs-lookup"><span data-stu-id="affe1-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
