---
title: "Red Hat Enterprise Linux VHD 만들기 및 Azure에서 사용하도록 업로드 | Microsoft Docs"
description: "RedHat Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="cfdd7-103">Azure용 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="cfdd7-104">이 문서에서는 Azure용 RHEL(Red Hat Enterprise Linux) 가상 컴퓨터를 준비하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="cfdd7-105">이 문서에 설명되어 있는 RHEL의 버전은 6.7+ 및 7.1+입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="cfdd7-106">이 문서에서 다룰 준비에 대한 하이퍼바이저는 Hyper-V, KVM(커널 기반 가상 컴퓨터) 및 VMware입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="cfdd7-107">Red Hat 클라우드 액세스 프로그램에 참여하기 위한 자격 요구 사항에 대한 자세한 내용은 [Red Hat 클라우드 액세스 웹 사이트](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) 및 [Azure에서 실행 중인 RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="cfdd7-108">Hyper-V 관리자에서 Red Hat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cfdd7-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cfdd7-109">Prerequisites</span></span>
<span data-ttu-id="cfdd7-110">이 섹션은 RedHat 웹 사이트에서 ISO 파일을 확보했으며 VHD(가상 하드 디스크)에 RHEL 이미지를 이미 설치한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="cfdd7-111">Hyper-V 관리자를 사용하여 운영 체제 이미지를 설치하는 방법에 대한 자세한 내용은 [Hyper-V 역할 설치 및 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="cfdd7-112">**RHEL 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="cfdd7-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="cfdd7-113">Azure는 VHDX 형식을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="cfdd7-114">Azure는 고정 VHD만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="cfdd7-115">Hyper-V 관리자를 사용하여 디스크를 VHD 형식으로 변환하거나, convert-vhd cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="cfdd7-116">VirtualBox를 사용하는 경우 디스크를 만들 때 기본 동적 할다 옵션과 달리 **고정 크기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="cfdd7-117">Azure에서는 1세대 가상 컴퓨터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="cfdd7-118">VHDX에서 VHD 파일 형식으로, 동적 확장에서 고정된 크기의 디스크로 1세대 가상 컴퓨터를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="cfdd7-119">가상 컴퓨터의 세대는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="cfdd7-120">자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 하나요?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="cfdd7-121">VHD에 허용되는 최대 크기는 1,023GB입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="cfdd7-122">Linux 운영 체제를 설치하는 경우 설치 기본값인 경우가 많은 LVM(논리 볼륨 관리자)이 아닌 표준 파티션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="cfdd7-123">이 방법은 특히 문제 해결을 위해 운영 체제 디스크를 다른 동일한 가상 컴퓨터에 연결해야 하는 경우, 복제된 가상 컴퓨터와 LVM 이름이 충돌하는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="cfdd7-124">데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="cfdd7-125">UDF(범용 디스크 형식) 파일 시스템을 탑재하기 위한 커널 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="cfdd7-126">Azure에서 처음 부팅 시 게스트에 연결된 UDF 형식 미디어는 프로비저닝 구성을 Linux 가상 컴퓨터에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="cfdd7-127">Azure Linux 에이전트는 해당 구성을 읽고 가상 컴퓨터를 프로비전하기 위해 UDF 파일 시스템을 탑재할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="cfdd7-128">2.6.37 이전의 Linux 커널 버전은 가상 컴퓨터 크기가 더 큰 Hyper-V에서 NUMA(비균일 메모리 액세스)를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="cfdd7-129">이 문제는 주로 업스트림 Red Hat 2.6.32 커널을 사용하는 이전 배포에 영향을 주며 RHEL 6.6(kernel-2.6.32-504)에서는 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="cfdd7-130">2.6.37보다 오래된 사용자 지정 커널 또는 2.6.32-504보다 오래된 RHEL 기반 커널을 실행하는 시스템의 경우 grub.conf의 커널 명령줄에 부트 매개 변수 `numa=off`를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="cfdd7-131">자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="cfdd7-132">운영 체제 디스크에서는 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="cfdd7-133">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="cfdd7-134">여기에 대한 자세한 내용은 다음 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="cfdd7-135">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="cfdd7-136">Hyper-V 관리자에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="cfdd7-137">Hyper-V 관리자에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="cfdd7-138">**연결** 을 클릭하여 가상 컴퓨터의 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="cfdd7-139">RHEL 6에서 NetworkManager는 Azure Linux 에이전트 작동을 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="cfdd7-140">다음 명령을 실행하여 이 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="cfdd7-141">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="cfdd7-142">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="cfdd7-143">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 이동(또는 제거)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="cfdd7-144">이러한 규칙은 Microsoft Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="cfdd7-145">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="cfdd7-146">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="cfdd7-147">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-148">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="cfdd7-149">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-150">이 수정 작업을 수행하려면 `/boot/grub/menu.lst`를 텍스트 편집기에서 열고 기본 커널이 다음 매개 변수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="cfdd7-151">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="cfdd7-152">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="cfdd7-153">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="cfdd7-154">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-155">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="cfdd7-156">이 구성은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="cfdd7-157">또한 RHEL 6.5 및 이전 버전에서는 커널 매개 변수 `numa=off`를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="cfdd7-158">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="cfdd7-159">SSH(보안 셸) 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다. 이것이 일반적으로 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="cfdd7-160">다음 줄을 포함하도록 /etc/ssh/sshd_config를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="cfdd7-161">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="cfdd7-162">WALinuxAgent 패키지를 설치하면 3단계에서 NetworkManager 및 NetworkManager-gnome 패키지를 아직 제거하지 않은 경우 이러한 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="cfdd7-163">운영 체제 디스크에 스왑 공간을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="cfdd7-164">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-165">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-166">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="cfdd7-167">다음 명령을 실행하여 (필요한 경우) 구독에 대한 등록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="cfdd7-168">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="cfdd7-169">Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="cfdd7-170">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="cfdd7-171">Hyper-V 관리자에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="cfdd7-172">Hyper-V 관리자에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="cfdd7-173">**연결** 을 클릭하여 가상 컴퓨터의 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="cfdd7-174">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="cfdd7-175">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="cfdd7-176">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="cfdd7-177">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="cfdd7-178">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-179">이렇게 수정하려면 텍스트 편집기에서 `/etc/default/grub`를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="cfdd7-180">예:</span><span class="sxs-lookup"><span data-stu-id="cfdd7-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="cfdd7-181">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="cfdd7-182">이 구성은 NIC에 대한 새 RHEL 7 명명 규칙도 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="cfdd7-183">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="cfdd7-184">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cfdd7-185">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-186">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다. 이 방식은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="cfdd7-187">`/etc/default/grub`편집을 완료한 후에 다음 명령을 실행하여 grub 구성을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="cfdd7-188">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다. 이것이 일반적으로 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="cfdd7-189">다음 줄을 포함하도록 `/etc/ssh/sshd_config` 을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="cfdd7-190">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-191">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="cfdd7-192">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="cfdd7-193">운영 체제 디스크에 스왑 공간을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="cfdd7-194">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-195">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-196">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) `/etc/waagent.conf`에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="cfdd7-197">구독에 대한 등록을 해제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="cfdd7-198">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="cfdd7-199">Hyper-V 관리자에서 **작업** > **종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="cfdd7-200">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="cfdd7-201">KVM에서 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="cfdd7-202">KVM에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="cfdd7-203">Red Hat 웹 사이트에서 RHEL 6의 KVM 이미지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="cfdd7-204">루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-204">Set a root password.</span></span>

    <span data-ttu-id="cfdd7-205">암호화된 암호를 생성하고 명령 출력을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="cfdd7-206">guestfish 루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="cfdd7-207">루트 사용자의 두 번째 필드를 “!!”에서</span><span class="sxs-lookup"><span data-stu-id="cfdd7-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="cfdd7-208">암호화된 암호로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-208">to the encrypted password.</span></span>

3. <span data-ttu-id="cfdd7-209">qcow2 이미지에서 KVM에 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="cfdd7-210">디스크 형식을 **qcow2**로 설정하고 가상 네트워크 인터페이스 장치 모델을 **virtio**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="cfdd7-211">그 후 가상 컴퓨터를 시작하고 루트로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="cfdd7-212">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="cfdd7-213">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="cfdd7-214">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 이동(또는 제거)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="cfdd7-215">이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="cfdd7-216">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="cfdd7-217">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="cfdd7-218">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-219">이 구성을 수행하려면 `/boot/grub/menu.lst`를 텍스트 편집기에서 열고 기본 커널이 다음 매개 변수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="cfdd7-220">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="cfdd7-221">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="cfdd7-222">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cfdd7-223">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-224">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다. 이 방식은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="cfdd7-225">또한 RHEL 6.5 및 이전 버전에서는 커널 매개 변수 `numa=off`를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="cfdd7-226">Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="cfdd7-227">Hyper-V 모듈을 initramfs에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="cfdd7-228">`/etc/dracut.conf`를 편집하고 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="cfdd7-229">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="cfdd7-230">Cloud-Init을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="cfdd7-231">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="cfdd7-232">다음 줄을 포함하도록 /etc/ssh/sshd_config를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="cfdd7-233">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-234">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="cfdd7-235">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="cfdd7-236">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-237">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-238">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) **/etc/waagent.conf**에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="cfdd7-239">다음 명령을 실행하여 (필요한 경우) 구독에 대한 등록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="cfdd7-240">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="cfdd7-241">KVM의 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="cfdd7-242">qcow2 이미지를 VHD 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="cfdd7-243">우선 이미지를 원시 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="cfdd7-244">원시 이미지의 크기가 1MB로 정렬되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="cfdd7-245">그렇지 않은 경우 1MB에 맞게 크기를 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="cfdd7-246">원시 디스크를 고정 크기 VHD로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="cfdd7-247">KVM에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="cfdd7-248">Red Hat 웹 사이트에서 RHEL 7의 KVM 이미지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="cfdd7-249">이 절차에서는 RHEL 7을 예제로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="cfdd7-250">루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-250">Set a root password.</span></span>

    <span data-ttu-id="cfdd7-251">암호화된 암호를 생성하고 명령 출력을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="cfdd7-252">guestfish 루트 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="cfdd7-253">루트 사용자의 두 번째 필드를 “!!”에서</span><span class="sxs-lookup"><span data-stu-id="cfdd7-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="cfdd7-254">암호화된 암호로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-254">to the encrypted password.</span></span>

3. <span data-ttu-id="cfdd7-255">qcow2 이미지에서 KVM에 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="cfdd7-256">디스크 형식을 **qcow2**로 설정하고 가상 네트워크 인터페이스 장치 모델을 **virtio**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="cfdd7-257">그 후 가상 컴퓨터를 시작하고 루트로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="cfdd7-258">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="cfdd7-259">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="cfdd7-260">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="cfdd7-261">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="cfdd7-262">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-263">이렇게 구성하려면 텍스트 편집기에서 `/etc/default/grub`를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="cfdd7-264">예:</span><span class="sxs-lookup"><span data-stu-id="cfdd7-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="cfdd7-265">이 명령은 모든 콘솔 메시지를 첫 번째 직렬 포트로 전송하므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="cfdd7-266">이 명령은 NIC에 대한 새 RHEL 7 명명 규칙도 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="cfdd7-267">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="cfdd7-268">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cfdd7-269">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-270">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다. 이 방식은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="cfdd7-271">`/etc/default/grub`편집을 완료한 후에 다음 명령을 실행하여 grub 구성을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="cfdd7-272">Hyper-V 모듈을 initramfs에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="cfdd7-273">`/etc/dracut.conf` 을 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="cfdd7-274">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="cfdd7-275">Cloud-Init을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="cfdd7-276">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="cfdd7-277">다음 줄을 포함하도록 /etc/ssh/sshd_config를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="cfdd7-278">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-279">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="cfdd7-280">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="cfdd7-281">waagent 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="cfdd7-282">운영 체제 디스크에 스왑 공간을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="cfdd7-283">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-284">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-285">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) `/etc/waagent.conf`에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="cfdd7-286">다음 명령을 실행하여 (필요한 경우) 구독에 대한 등록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="cfdd7-287">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="cfdd7-288">KVM의 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="cfdd7-289">qcow2 이미지를 VHD 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="cfdd7-290">우선 이미지를 원시 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="cfdd7-291">원시 이미지의 크기가 1MB로 정렬되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="cfdd7-292">그렇지 않은 경우 1MB에 맞게 크기를 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="cfdd7-293">원시 디스크를 고정 크기 VHD로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="cfdd7-294">VMware에서 RedHat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="cfdd7-295">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cfdd7-295">Prerequisites</span></span>
<span data-ttu-id="cfdd7-296">이 섹션은 VMWare에 RHEL 가상 컴퓨터가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="cfdd7-297">VMWare에서 운영 체제를 설치하는 자세한 방법은 [VMWare 게스트 운영 체제 설치 가이드](http://partnerweb.vmware.com/GOSIG/home.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="cfdd7-298">Linux 운영 체제를 설치하는 경우 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="cfdd7-299">이 방법은 특히 문제 해결을 위해 운영 체제 디스크를 다른 가상 컴퓨터에 연결해야 하는 경우, 복제된 가상 컴퓨터와 LVM 이름이 충돌하는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="cfdd7-300">원하는 경우에는 데이터 디스크에서 LVM 또는 RAID를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="cfdd7-301">운영 체제 디스크에서는 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="cfdd7-302">Linux 에이전트를 구성하여 임시 리소스 디스크에서 스왑 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="cfdd7-303">여기에 대한 자세한 내용은 아래 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="cfdd7-304">가상 하드 디스크를 만들 때 **가상 디스크를 단일 파일로 저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="cfdd7-305">VMWare에서 RHEL 6 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="cfdd7-306">RHEL 6에서 NetworkManager는 Azure Linux 에이전트 작동을 방해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="cfdd7-307">다음 명령을 실행하여 이 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="cfdd7-308">다음 텍스트가 포함된 **network** 파일을 /etc/sysconfig/ 디렉터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="cfdd7-309">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="cfdd7-310">이더넷 인터페이스에 대한 정적 규칙을 생성하지 않도록 방지하는 udev 규칙을 이동(또는 제거)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="cfdd7-311">이러한 규칙은 Azure 또는 Hyper-V에서 가상 컴퓨터를 복제하는 경우 문제를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="cfdd7-312">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="cfdd7-313">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="cfdd7-314">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-315">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="cfdd7-316">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-317">이렇게 하려면 텍스트 편집기에서 `/etc/default/grub`를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="cfdd7-318">예:</span><span class="sxs-lookup"><span data-stu-id="cfdd7-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="cfdd7-319">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="cfdd7-320">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="cfdd7-321">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cfdd7-322">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-323">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다. 이 방식은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="cfdd7-324">Hyper-V 모듈을 initramfs에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="cfdd7-325">`/etc/dracut.conf`를 편집하고 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="cfdd7-326">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="cfdd7-327">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다. 이것이 일반적으로 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="cfdd7-328">다음 줄을 포함하도록 `/etc/ssh/sshd_config` 을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="cfdd7-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="cfdd7-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="cfdd7-330">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="cfdd7-331">운영 체제 디스크에 스왑 공간을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="cfdd7-332">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-333">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-334">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) `/etc/waagent.conf`에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="cfdd7-335">다음 명령을 실행하여 (필요한 경우) 구독에 대한 등록을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="cfdd7-336">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="cfdd7-337">가상 컴퓨터를 종료하고 VMDK 파일을 .vhd 파일로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="cfdd7-338">우선 이미지를 원시 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="cfdd7-339">원시 이미지의 크기가 1MB로 정렬되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="cfdd7-340">그렇지 않은 경우 1MB에 맞게 크기를 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="cfdd7-341">원시 디스크를 고정 크기 VHD로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="cfdd7-342">VMWare에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="cfdd7-343">파일 `/etc/sysconfig/network`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="cfdd7-344">파일 `/etc/sysconfig/network-scripts/ifcfg-eth0`를 만들거나 편집하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="cfdd7-345">다음 명령을 실행하여 부팅 시 네트워크 서비스가 시작되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="cfdd7-346">RHEL 리포지토리에서 패키지 설치를 사용하도록 다음 명령을 실행하여 Red Hat 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="cfdd7-347">Azure용 커널 매개 변수를 추가로 포함하려면 grub 구성에서 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="cfdd7-348">이렇게 수정하려면 텍스트 편집기에서 `/etc/default/grub`를 열고 `GRUB_CMDLINE_LINUX` 매개 변수를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="cfdd7-349">예:</span><span class="sxs-lookup"><span data-stu-id="cfdd7-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="cfdd7-350">이 구성은 모든 콘솔 메시지를 첫 번째 직렬 포트로 전송하므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="cfdd7-351">NIC에 대한 새 RHEL 7 명명 규칙도 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="cfdd7-352">그 밖에 다음 매개 변수를 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="cfdd7-353">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="cfdd7-354">원할 경우 `crashkernel` 옵션은 구성된 상태로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="cfdd7-355">이 매개 변수는 가상 컴퓨터의 사용 가능한 메모리 양을 128MB 이상 줄입니다. 이 방식은 좀 더 작은 가상 컴퓨터 크기에서는 문제가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="cfdd7-356">`/etc/default/grub`편집을 완료한 후에 다음 명령을 실행하여 grub 구성을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="cfdd7-357">Hyper-V 모듈을 initramfs에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="cfdd7-358">`/etc/dracut.conf`를 편집하고 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="cfdd7-359">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="cfdd7-360">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="cfdd7-361">이 설정이 일반적으로 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-361">This setting is usually the default.</span></span> <span data-ttu-id="cfdd7-362">다음 줄을 포함하도록 `/etc/ssh/sshd_config` 을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="cfdd7-363">WALinuxAgent 패키지 `WALinuxAgent-<version>`은 Red Hat 기타 리포지토리에 푸시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="cfdd7-364">다음 명령을 실행하여 기타 리포지토리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="cfdd7-365">다음 명령을 실행하여 Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="cfdd7-366">운영 체제 디스크에 스왑 공간을 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="cfdd7-367">Azure Linux 에이전트는 Azure에서 가상 컴퓨터를 프로비전한 후에 가상 컴퓨터에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="cfdd7-368">로컬 리소스 디스크는 임시 디스크이며 가상 컴퓨터의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="cfdd7-369">Azure Linux 에이전트를 설치한 후에(이전 단계 참조) `/etc/waagent.conf`에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="cfdd7-370">구독에 대한 등록을 해제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="cfdd7-371">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="cfdd7-372">가상 컴퓨터를 종료하고 VMDK 파일을 VHD 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="cfdd7-373">우선 이미지를 원시 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="cfdd7-374">원시 이미지의 크기가 1MB로 정렬되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="cfdd7-375">그렇지 않은 경우 1MB에 맞게 크기를 반올림합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="cfdd7-376">원시 디스크를 고정 크기 VHD로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="cfdd7-377">자동으로 kickstart 파일을 사용하여 ISO에서 Red Hat 기반 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="cfdd7-378">kickstart 파일에서 RHEL 7 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="cfdd7-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="cfdd7-379">다음 콘텐츠를 포함하는 kickstart 파일을 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="cfdd7-380">Kickstart 설치에 대한 자세한 내용은 [Kickstart 설치 가이드](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
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

        # Clear the MBR
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

        # Power down the machine after install
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

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
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

2. <span data-ttu-id="cfdd7-381">설치 시스템에서 액세스할 수 있는 위치에 kickstart 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="cfdd7-382">Hyper-V 관리자에서 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="cfdd7-383">**가상 하드 디스크 연결** 페이지에서 **나중에 가상 하드 디스크 연결**을 선택하고 새 가상 컴퓨터 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="cfdd7-384">가상 컴퓨터 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="cfdd7-385">a.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-385">a.</span></span>  <span data-ttu-id="cfdd7-386">새 가상 하드 디스크를 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="cfdd7-387">**VHD 형식** 및 **고정된 크기**를 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="cfdd7-388">b.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-388">b.</span></span>  <span data-ttu-id="cfdd7-389">설치 ISO를 DVD 드라이브에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="cfdd7-390">c.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-390">c.</span></span>  <span data-ttu-id="cfdd7-391">CD에서 부팅하도록 BIOS를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="cfdd7-392">가상 컴퓨터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-392">Start the virtual machine.</span></span> <span data-ttu-id="cfdd7-393">설치 가이드가 나타나면 **Tab** 키를 눌러서 부팅 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="cfdd7-394">부팅 옵션 마지막에 `inst.ks=<the location of the kickstart file>` 을 입력하고 **Enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="cfdd7-395">설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-395">Wait for the installation to finish.</span></span> <span data-ttu-id="cfdd7-396">완료되면 가상 컴퓨터가 자동으로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="cfdd7-397">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cfdd7-398">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="cfdd7-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="cfdd7-399">Hyper-V 드라이버가 Hyper-V 하이퍼바이저가 아닌 프로그램을 사용하는 경우 초기 RAM 디스크에 포함될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="cfdd7-400">경우에 따라 Linux 설치 관리자는 Hyper-V 환경에서 실행 중임을 감지하지 않는 한 초기 RAM 디스크(initrd 또는 initramfs)에 Hyper-V용 드라이버를 포함하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="cfdd7-401">다른 가상화 시스템(예: Virtualbox, Xen 등)을 사용하여 Linux 이미지를 준비할 경우 초기 RAM 디스크에서 최소한 hv_vmbus 및 hv_storvsc 커널 모듈을 사용할 수 있도록 initrd를 다시 작성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="cfdd7-402">이는 적어도 업스트림 Red Hat 배포를 기반으로 하는 시스템의 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="cfdd7-403">이 문제를 해결하려면 Hyper-V 모듈을 initramfs에 추가하고 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="cfdd7-404">`/etc/dracut.conf`를 편집하고 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="cfdd7-405">Initramfs를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="cfdd7-406">자세한 정보는 [initramfs 다시 작성](https://access.redhat.com/solutions/1958)에 대한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfdd7-407">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfdd7-407">Next steps</span></span>
<span data-ttu-id="cfdd7-408">이제 Red Hat Enterprise Linux 가상 하드 디스크를 사용하여 Azure에 새 가상 컴퓨터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="cfdd7-409">.vhd 파일을 Azure에 처음으로 업로드하는 경우 [Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에서 2단계 및 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="cfdd7-410">Red Hat Enterprise Linux를 실행하기 위해 인증된 하이퍼바이저에 대한 자세한 내용은 [Red Hat 웹 사이트](https://access.redhat.com/certified-hypervisors)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cfdd7-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
