---
title: "Azure에서 Ubuntu Linux VHD 만들기 및 업로드"
description: "Ubuntu Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="1ee88-103">Azure용 Ubuntu 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="1ee88-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="1ee88-104">공식 Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="1ee88-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="1ee88-105">이제 Ubuntu는 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)에서 다운로드할 수 있도록 공식 Azure VHD를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="1ee88-106">Azure에 대해 특수한 사용자 고유의 Ubuntu 이미지를 빌드해야 하는 경우 아래 수동 절차 대신 이러한 알려진 작업 VHD를 시작하고 필요에 따라 사용자 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="1ee88-107">최신 이미지 릴리스는 항상 다음 위치에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="1ee88-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1ee88-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="1ee88-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1ee88-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="1ee88-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="1ee88-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ee88-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1ee88-111">Prerequisites</span></span>
<span data-ttu-id="1ee88-112">이 문서에서는 가상 하드 디스크에 Ubuntu Linux 운영 체제를 이미 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="1ee88-113">.vhd 파일을 만드는 여러 도구가 있습니다(예: Hyper-V와 같은 가상화 솔루션).</span><span class="sxs-lookup"><span data-stu-id="1ee88-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="1ee88-114">자세한 내용은 [Hyper-V 역할 설치 및 가상 시스템 구성](http://technet.microsoft.com/library/hh846766.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ee88-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="1ee88-115">**Ubuntu 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="1ee88-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="1ee88-116">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ee88-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1ee88-117">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="1ee88-118">Hyper-V 관리자 또는 convert-vhd cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="1ee88-119">Linux 시스템 설치 시에는 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="1ee88-120">이렇게 하면 특히 문제 해결을 위해 OS 디스크를 다른 VM에 연결해야 하는 경우 복제된 VM과 LVM 이름이 충돌하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="1ee88-121">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="1ee88-122">OS 디스크에 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1ee88-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="1ee88-123">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="1ee88-124">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="1ee88-125">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="1ee88-126">수동 단계</span><span class="sxs-lookup"><span data-stu-id="1ee88-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="1ee88-127">Azure에 대해 고유한 사용자 지정 Ubuntu 이미지를 만들기 전에 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)에서 미리 빌드되고 테스트된 이미지를 사용하는 것을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="1ee88-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="1ee88-128">Hyper-V 관리자의 가운데 창에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="1ee88-129">**연결** 을 클릭하여 가상 컴퓨터 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="1ee88-130">Ubuntu의 Azure 리포지토리를 사용하도록 이미지의 현재 리포지토리를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="1ee88-131">단계는 Ubuntu 버전에 따라 약간씩 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="1ee88-132">`/etc/apt/sources.list`를 편집하기 전에 백업을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="1ee88-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="1ee88-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="1ee88-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="1ee88-136">이제 Ubuntu Azure 이미지는 *하드웨어 지원* (HWE) 커널을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="1ee88-137">다음 명령을 실행하여 운영 체제를 최신 커널로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="1ee88-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="1ee88-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="1ee88-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="1ee88-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="1ee88-141">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="1ee88-141">**See also:**</span></span>
    - [<span data-ttu-id="1ee88-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="1ee88-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="1ee88-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="1ee88-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="1ee88-144">Azure용 커널 매개 변수를 추가로 포함하려면 Grub의 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="1ee88-145">이 작업을 수행하려면 `/etc/default/grub`을 텍스트 편집기에서 열고 `GRUB_CMDLINE_LINUX_DEFAULT` 변수를 찾거나 필요한 경우 추가하여 다음 매개 변수가 포함되도록 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="1ee88-146">이 파일을 저장하고 닫은 다음 `sudo update-grub`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="1ee88-147">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 기술 지원에서 문제를 디버깅하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="1ee88-148">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="1ee88-149">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-149">This is usually the default.</span></span>

7. <span data-ttu-id="1ee88-150">Azure Linux 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="1ee88-151">`walinuxagent` 패키지는 `NetworkManager` 및 `NetworkManager-gnome` 패키지가 설치되어 있는 경우 이러한 패키지를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="1ee88-152">다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제하고 Azure에서 프로비전할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="1ee88-153">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1ee88-154">이제 Linux VHD를 Azure에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ee88-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ee88-155">Next steps</span></span>
<span data-ttu-id="1ee88-156">이제 Ubuntu Linux 가상 하드 디스크를 사용하여 Azure에서 새 가상 컴퓨터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ee88-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="1ee88-157">.vhd 파일을 Azure에 처음으로 업로드하는 경우 [Linux 운영 체제를 포함하는 가상 하드 디스크 만들기 및 업로드](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)에서 2단계 및 3단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ee88-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="1ee88-158">참조</span><span class="sxs-lookup"><span data-stu-id="1ee88-158">References</span></span>
<span data-ttu-id="1ee88-159">Ubuntu 하드웨어 지원(HWE) 커널</span><span class="sxs-lookup"><span data-stu-id="1ee88-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="1ee88-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="1ee88-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="1ee88-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="1ee88-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

