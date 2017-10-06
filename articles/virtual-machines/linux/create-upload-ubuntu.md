---
title: "aaaCreate 및 Ubuntu Linux VHD를 사용 하 여 Azure에 업로드"
description: "Toocreate 알아보고 업로드는 Azure 가상 하드 디스크 (VHD)는 Ubuntu Linux 운영 체제를 포함 합니다."
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
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="f4277-103">Azure용 Ubuntu 가상 컴퓨터 준비</span><span class="sxs-lookup"><span data-stu-id="f4277-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="f4277-104">공식 Ubuntu 클라우드 이미지</span><span class="sxs-lookup"><span data-stu-id="f4277-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="f4277-105">이제 Ubuntu는 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/)에서 다운로드할 수 있도록 공식 Azure VHD를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="f4277-106">그 아래 hello 수동 절차를 사용 하지 않고 toobuild 특수 Ubuntu 이미지 Azure에 필요한 경우 이러한 알려진와 권장된 toostart Vhd 작업 이며 필요에 따라 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="f4277-107">항상 hello 다음 위치에서 hello 최신 이미지 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="f4277-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="f4277-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="f4277-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="f4277-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="f4277-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="f4277-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4277-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4277-111">Prerequisites</span></span>
<span data-ttu-id="f4277-112">이 문서는 Ubuntu Linux 운영 체제 tooa 가상 하드 디스크로 이미 설치한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="f4277-113">여러 도구 toocreate.vhd 파일을 예를 들어 Hyper-v와 같은 가상화 솔루션 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="f4277-114">자세한 내용은 [hello Hyper-v 역할을 설치 하 고 가상 컴퓨터 구성](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="f4277-115">**Ubuntu 설치 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="f4277-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="f4277-116">Azure용 Linux를 준비하는 방법에 대한 추가 팁은 [일반 Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4277-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="f4277-117">hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="f4277-118">Hyper-v 관리자를 사용 하 여 hello 디스크 tooVHD 형식을 변환 하거나 convert vhd cmdlet hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="f4277-119">Hello Linux 시스템을 설치할 때 LVM (종종 대부분의 설치에 대 한 hello 기본값) 보다는 표준 파티션을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="f4277-120">OS 필요 없는 연결 toobe tooanother VM에 대 한 디스크 문제 해결 하는 경우에 특히 복제 된 Vm과 LVM 이름 충돌을 피해 야 할이.</span><span class="sxs-lookup"><span data-stu-id="f4277-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="f4277-121">원하는 경우에는 데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="f4277-122">스왑 파티션을 hello OS 디스크에 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="f4277-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="f4277-123">hello Linux 에이전트 구성된 toocreate hello 일시적인 리소스 디스크의 스왑 파일 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="f4277-124">이 대 한 자세한 내용은 아래 hello 단계에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="f4277-125">모든 hello Vhd 크기를 1MB의 배수인가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="f4277-126">수동 단계</span><span class="sxs-lookup"><span data-stu-id="f4277-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="f4277-127">Toocreate 시도 하기 전에 Azure에서 사용자 고유의 사용자 지정 Ubuntu 이미지를 고려 하십시오 hello를 사용 하 여 미리 처음 빌드되고 테스트에서 이미지 [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="f4277-128">Hyper-v 관리자의 가운데 창 hello hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="f4277-129">클릭 **연결** hello 가상 컴퓨터에 대 한 tooopen hello 창.</span><span class="sxs-lookup"><span data-stu-id="f4277-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="f4277-130">Hello 현재 저장소에서 Azure hello 이미지 toouse Ubuntu 리포지토리를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="f4277-131">hello 단계 hello Ubuntu 버전에 따라 약간 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="f4277-132">편집 하기 전에 `/etc/apt/sources.list`, 것이 권장 toomake 백업:</span><span class="sxs-lookup"><span data-stu-id="f4277-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="f4277-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="f4277-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="f4277-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="f4277-136">hello Ubuntu Azure 이미지는 이제 다음과 같습니다. hello *하드웨어 사용* 커널 (HWE).</span><span class="sxs-lookup"><span data-stu-id="f4277-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="f4277-137">Hello 다음 명령을 실행 하 여 hello 운영 체제 toohello 최신 커널을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="f4277-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="f4277-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="f4277-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="f4277-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="f4277-141">**참고 항목:**</span><span class="sxs-lookup"><span data-stu-id="f4277-141">**See also:**</span></span>
    - [<span data-ttu-id="f4277-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="f4277-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="f4277-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="f4277-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="f4277-144">Azure 용 hello 커널 부팅 줄 Grub tooinclude 추가 커널 매개 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="f4277-145">이 열려 toodo `/etc/default/grub` 텍스트 편집기에서 호출 하는 hello 변수를 찾을 `GRUB_CMDLINE_LINUX_DEFAULT` (또는 필요에 따라 추가) 하 고 매개 변수 뒤 tooinclude hello 편집:</span><span class="sxs-lookup"><span data-stu-id="f4277-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="f4277-146">이 파일을 저장하고 닫은 다음 `sudo update-grub`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="f4277-147">이렇게 하면 모든 콘솔 메시지 toohello 첫 번째 직렬 포트를 Azure 기술 지원 문제 디버깅에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="f4277-148">해당 hello SSH 서버를 설치 및 부팅 시 toostart을 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="f4277-149">일반적으로 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-149">This is usually hello default.</span></span>

7. <span data-ttu-id="f4277-150">Hello Azure Linux 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="f4277-151">hello `walinuxagent` 패키지 hello 제거 될 수 있습니다 `NetworkManager` 및 `NetworkManager-gnome` 패키지 설치 되어 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="f4277-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="f4277-152">Hello 명령을 toodeprovision hello 가상 컴퓨터를 다음을 실행 하 고 Azure에서 프로 비전 하기 위한 준비:</span><span class="sxs-lookup"><span data-stu-id="f4277-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="f4277-153">Hyper-V 관리자에서 **작업 -> 종료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="f4277-154">Linux VHD 준비 toobe 업로드 tooAzure 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4277-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4277-155">Next steps</span></span>
<span data-ttu-id="f4277-156">사용자는 이제 준비 toouse Azure의 Ubuntu Linux 가상 하드 디스크 toocreate 새 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f4277-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="f4277-157">인 경우 hello hello.vhd 파일 tooAzure를 업로드 하는 처음 2와 3 단계 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4277-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="f4277-158">참조</span><span class="sxs-lookup"><span data-stu-id="f4277-158">References</span></span>
<span data-ttu-id="f4277-159">Ubuntu 하드웨어 지원(HWE) 커널</span><span class="sxs-lookup"><span data-stu-id="f4277-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="f4277-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span><span class="sxs-lookup"><span data-stu-id="f4277-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="f4277-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span><span class="sxs-lookup"><span data-stu-id="f4277-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

