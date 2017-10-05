---
title: "Azure에서 Linux VHD 만들기 및 업로드"
description: "Linux 운영 체제가 포함된 Azure VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: ccadf55c492c097ef96f25e469dbf36fc87b6102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="information-for-non-endorsed-distributions"></a><span data-ttu-id="3faef-103">보증되지 않는 배포에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="3faef-103">Information for Non-Endorsed Distributions</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3faef-104">[보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 중 하나를 사용하는 경우에만 Linux OS를 실행하는 가상 컴퓨터에 Azure 플랫폼 SLA가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-104">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the [endorsed distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) is used.</span></span> <span data-ttu-id="3faef-105">Azure 이미지 갤러리에 제공된 모든 Linux 배포는 필요한 구성이 포함된 보증 배포판입니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-105">All Linux distributions that are provided in the Azure image gallery are endorsed distributions with the required configuration.</span></span>

* [<span data-ttu-id="3faef-106">Azure의 Linux - 보증 배포판</span><span class="sxs-lookup"><span data-stu-id="3faef-106">Linux on Azure - Endorsed Distributions</span></span>](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="3faef-107">Microsoft Azure의 Linux 이미지 지원</span><span class="sxs-lookup"><span data-stu-id="3faef-107">Support for Linux images in Microsoft Azure</span></span>](https://support.microsoft.com/kb/2941892)

<span data-ttu-id="3faef-108">Azure에서 실행되는 모든 배포가 플랫폼에서 올바르게 실행되려면 여러 가지 필수 구성 요소가 충족되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-108">All distributions running on Azure will need to meet a number of prerequisites to have a chance to properly run on the platform.</span></span>  <span data-ttu-id="3faef-109">모든 배포는 서로 다르므로 이 문서에는 모든 필수 구성 요소가 포함되어 있지는 않습니다. 아래 기준이 모두 충족되어도 플랫폼에서 올바르게 실행되도록 하려면 여전히 Linux 시스템을 상당히 조정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-109">This article is by no means comprehensive as every distribution is different; and it is quite possible that even if you meet all the criteria below you will still need to significantly tweak your Linux system to ensure that it properly runs on the platform.</span></span>

<span data-ttu-id="3faef-110">따라서 가능한 경우 [Azure 보증 배포판의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 중 하나를 사용하여 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-110">It is for this reason that we recommend that you start with one of our [Linux on Azure Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when possible.</span></span> <span data-ttu-id="3faef-111">다음 문서에서는 Azure에서 지원되는 다양한 Linux 보증 배포판을 준비하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-111">The following articles will guide you through how to prepare the various endorsed Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="3faef-112">**[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-112">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3faef-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-113">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3faef-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-114">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3faef-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-115">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3faef-116">**[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-116">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="3faef-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="3faef-117">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="3faef-118">이 문서의 나머지 부분에서는 Azure에서 Linux 배포를 실행하기 위한 일반 지침을 주로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-118">The rest of this article will focus on general guidance for running your Linux distribution on Azure.</span></span>

## <a name="general-linux-installation-notes"></a><span data-ttu-id="3faef-119">일반 Linux 설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="3faef-119">General Linux Installation Notes</span></span>
* <span data-ttu-id="3faef-120">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-120">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="3faef-121">Hyper-V 관리자 또는 convert-vhd cmdlet을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-121">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="3faef-122">VirtualBox를 사용하면 디스크를 만들 때 기본적으로 동적 할당되지 않고 **고정 크기**가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-122">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="3faef-123">Azure에서는 1세대 가상 컴퓨터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-123">Azure only supports generation 1 virtual machines.</span></span> <span data-ttu-id="3faef-124">VHDX에서 VHD 파일 형식으로, 동적 확장에서 고정된 크기의 디스크로 1세대 가상 컴퓨터를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-124">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed sized disk.</span></span> <span data-ttu-id="3faef-125">하지만 가상 컴퓨터의 세대를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-125">But you can't change a virtual machine's generation.</span></span> <span data-ttu-id="3faef-126">자세한 내용은 [Hyper-V에 1 또는 2세대 가상 컴퓨터를 만들어야 합니까?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3faef-126">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span></span>
* <span data-ttu-id="3faef-127">VHD에 허용되는 최대 크기는 1,023GB입니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-127">The maximum size allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="3faef-128">Linux 시스템 설치 시에는 LVM(설치 기본값인 경우가 많음)이 아닌 표준 파티션을 사용하는 것이 *좋습니다*.</span><span class="sxs-lookup"><span data-stu-id="3faef-128">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="3faef-129">이렇게 하면 특히 문제 해결을 위해 OS 디스크를 다른 VM에 연결해야 하는 경우 복제된 VM과 LVM 이름이 충돌하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-129">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="3faef-130">데이터 디스크에서 [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-130">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="3faef-131">UDF 파일 시스템 탑재에 대한 커널 지원이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-131">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="3faef-132">Azure에서 처음 부팅 시 프로비저닝 구성이 게스트에 연결된 UDF 형식의 미디어를 통해 Linux VM에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-132">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="3faef-133">Azure Linux 에이전트는 해당 구성을 읽고 VM을 프로비전하기 위해 UDF 파일 시스템을 탑재할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-133">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="3faef-134">2.6.37 버전 미만의 Linux 커널은 VM 크기가 더 클 때 Hyper-V에서 NUMA를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-134">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="3faef-135">이 문제는 주로 업스트림 Red Hat 2.6.32 커널을 사용하는 이전 배포에 영향을 주며 RHEL 6.6(kernel-2.6.32-504)에서는 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-135">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="3faef-136">2.6.37보다 오래된 사용자 지정 커널 또는 2.6.32-504보다 오래된 RHEL 기반 커널을 실행하는 시스템의 경우 grub.conf의 커널 명령줄에 부트 매개 변수 `numa=off`</span><span class="sxs-lookup"><span data-stu-id="3faef-136">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="3faef-137">자세한 내용은 Red Hat [KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3faef-137">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="3faef-138">OS 디스크에 스왑 파티션을 구성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3faef-138">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="3faef-139">임시 리소스 디스크에서 스왑 파일을 만들도록 Linux 에이전트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-139">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="3faef-140">여기에 대한 자세한 내용은 아래 단계에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-140">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="3faef-141">모든 VHD 크기는 1MB의 배수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-141">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="installing-kernel-modules-without-hyper-v"></a><span data-ttu-id="3faef-142">Hyper-V 없이 커널 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="3faef-142">Installing kernel modules without Hyper-V</span></span>
<span data-ttu-id="3faef-143">Azure는 Hyper-V 하이퍼바이저에서 실행되므로 Azure에서 Linux를 실행하려면 특정 커널 모듈이 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-143">Azure runs on the Hyper-V hypervisor, so Linux requires that certain kernel modules are installed in order to run in Azure.</span></span> <span data-ttu-id="3faef-144">Hyper-V 외부에서 만든 VM이 있는 경우 Linux 설치 관리자는 Hyper-V 환경을 실행 중임을 감지하지 않는 한 초기 ramdisk(initrd 또는 initramfs)에 Hyper-V용 드라이버를 포함하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-144">If you have a VM that was created outside of Hyper-V, the Linux installers may not include the drivers for Hyper-V in the initial ramdisk (initrd or initramfs) unless it detects that it is running an a Hyper-V environment.</span></span> <span data-ttu-id="3faef-145">다른 가상화 시스템(예: Virtualbox, KVM 등)을 사용하여 Linux 이미지를 준비할 경우 초기 ramdisk에서 최소한 `hv_vmbus` 및 `hv_storvsc` 커널 모듈을 사용할 수 있도록 initrd를 다시 작성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-145">When using a different virtualization system (i.e. Virtualbox, KVM, etc.) to prepare your Linux image, you may need to rebuild the initrd to ensure that at least the `hv_vmbus` and `hv_storvsc` kernel modules are available on the initial ramdisk.</span></span>  <span data-ttu-id="3faef-146">이는 적어도 업스트림 Red Hat 배포를 기반으로 하는 시스템의 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-146">This is a known issue at least on systems based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="3faef-147">initrd 또는 initramfs 이미지를 다시 작성하는 메커니즘은 배포에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-147">The mechanism for rebuilding the initrd or initramfs image may vary depending on the distribution.</span></span> <span data-ttu-id="3faef-148">올바른 절차는 현재 배포의 설명서를 참조하거나 지원 담당자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="3faef-148">Please consult your distribution's documentation or support for the proper procedure.</span></span>  <span data-ttu-id="3faef-149">다음은 `mkinitrd` 유틸리티를 사용하여 initrd를 다시 작성하는 방법에 대한 한 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-149">Here is one example for how to rebuild the initrd using the `mkinitrd` utility:</span></span>

<span data-ttu-id="3faef-150">먼저 기존 initrd 이미지를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-150">First, back up the existing initrd image:</span></span>

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

<span data-ttu-id="3faef-151">다음으로 `hv_vmbus` 및 `hv_storvsc` 커널 모듈을 사용하여 initrd를 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-151">Next, rebuild the initrd with the `hv_vmbus` and `hv_storvsc` kernel modules:</span></span>

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a><span data-ttu-id="3faef-152">VHD 크기 조정</span><span class="sxs-lookup"><span data-stu-id="3faef-152">Resizing VHDs</span></span>
<span data-ttu-id="3faef-153">Azure의 VHD 이미지는 가상 크기가 1MB 단위로 조정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-153">VHD images on Azure must have a virtual size aligned to 1MB.</span></span>  <span data-ttu-id="3faef-154">일반적으로 Hyper-V를 사용하여 만든 VHD는 이미 올바르게 조정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-154">Typically, VHDs created using Hyper-V should already be aligned correctly.</span></span>  <span data-ttu-id="3faef-155">VHD가 올바르게 조정되어 있지 않으면 VHD에서 *이미지* 를 만들 때 다음과 유사한 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-155">If the VHD is not aligned correctly then you may receive an error message similar to the following when you attempt to create an *image* from your VHD:</span></span>

    "The VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. The size must be a whole number (in MBs).”

<span data-ttu-id="3faef-156">이 문제를 해결하려면 Hyper-V 관리자 콘솔 또는 [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet을 사용하여 VM 크기를 조정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-156">To remedy this you can resize the VM using either the Hyper-V Manager console or the [Resize-VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet.</span></span>  <span data-ttu-id="3faef-157">Windows 환경에서 실행 중이지 않은 경우 qemu-img를 사용하여 VHD를 변환(필요한 경우)하고 크기를 조정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-157">If you are not running in a Windows environment then it is recommended to use qemu-img to convert (if needed) and resize the VHD.</span></span>

> [!NOTE]
> <span data-ttu-id="3faef-158">VHD 형식이 잘못 지정되는 qemu-img 버전 >=2.2.1에 알려진 버그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-158">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span></span> <span data-ttu-id="3faef-159">이 문제는 QEMU 2.6에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-159">The issue has been fixed in QEMU 2.6.</span></span> <span data-ttu-id="3faef-160">qemu-img 2.2.0 이하 버전을 사용하거나 2.6 이상으로 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-160">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span></span> <span data-ttu-id="3faef-161">참조: https://bugs.launchpad.net/qemu/+bug/1490611</span><span class="sxs-lookup"><span data-stu-id="3faef-161">Reference: https://bugs.launchpad.net/qemu/+bug/1490611.</span></span>
> 
> 

1. <span data-ttu-id="3faef-162">`qemu-img` 또는 `vbox-manage`와 같은 도구를 사용하여 직접 VHD 크기를 조정하면 VHD가 부팅되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-162">Resizing the VHD directly using tools such as `qemu-img` or `vbox-manage` may result in an unbootable VHD.</span></span>  <span data-ttu-id="3faef-163">따라서 먼저 VHD를 원시 디스크 이미지로 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-163">So it is recommended to first convert the VHD to a RAW disk image.</span></span>  <span data-ttu-id="3faef-164">VM 이미지가 이미 원시 디스크 이미지로 만들어진 경우(KVM과 같은 일부 하이퍼바이저의 경우 기본값)에는 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-164">If the VM image was already created as RAW disk image (the default for some Hypervisors such as KVM) then you may skip this step:</span></span>
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. <span data-ttu-id="3faef-165">가상 크기가 1MB 단위로 조정되도록 디스크 이미지의 필요한 크기를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-165">Calculate the required size of the disk image to ensure that the virtual size is aligned to 1MB.</span></span>  <span data-ttu-id="3faef-166">다음 bash 셸 스크립트를 사용하여 이 작업을 간편하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-166">The following bash shell script can assist with this.</span></span>  <span data-ttu-id="3faef-167">이 스크립트에서는 "`qemu-img info`"를 사용하여 디스크 이미지의 가상 크기를 확인한 후 다음 1MB로 크기를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-167">The script uses "`qemu-img info`" to determine the virtual size of the disk image and then calculates the size to the next 1MB:</span></span>
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. <span data-ttu-id="3faef-168">위 스크립트에 설정된 대로 $rounded_size를 사용하여 원시 디스크의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-168">Resize the raw disk using $rounded_size as set in the above script:</span></span>
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. <span data-ttu-id="3faef-169">이제 원시 디스크를 고정 크기 VHD로 다시 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-169">Now, convert the RAW disk back to a fixed-size VHD:</span></span>
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   <span data-ttu-id="3faef-170">또는, qemu 버전 **2.6 +**는 `force_size` 옵션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-170">Or, with qemu version **2.6+** include the `force_size` option:</span></span>

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a><span data-ttu-id="3faef-171">Linux 커널 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3faef-171">Linux Kernel Requirements</span></span>
<span data-ttu-id="3faef-172">Hyper-V 및 Azure용 LIS(Linux 통합 서비스) 드라이버는 업스트림 Linux 커널로 직접 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-172">The Linux Integration Services (LIS) drivers for Hyper-V and Azure are contributed directly to the upstream Linux kernel.</span></span> <span data-ttu-id="3faef-173">최신 Linux 커널 버전(예: 3.x)을 포함하는 대부분의 배포에서는 이러한 드라이버가 이미 제공되거나 이러한 드라이버의 백 포트 버전이 커널과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-173">Many distributions that include a recent Linux kernel version (i.e. 3.x) will have these drivers available already, or otherwise provide backported versions of these drivers with their kernels.</span></span>  <span data-ttu-id="3faef-174">이러한 드라이버는 업스트림 커널에서 새로운 수정 사항과 기능이 적용되어 지속적으로 업데이트되므로 가능하면 이러한 수정 사항과 업데이트를 포함하는 [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 을 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-174">These drivers are constantly being updated in the upstream kernel with new fixes and features, so when possible it is recommended to run an [endorsed distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that will include these fixes and updates.</span></span>

<span data-ttu-id="3faef-175">Red Hat Enterprise Linux 버전 **6.0-6.3**의 변형을 실행하는 경우에는 Hyper-V용 최신 LIS 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-175">If you are running a variant of Red Hat Enterprise Linux versions **6.0-6.3**, then you will need to install the latest LIS drivers for Hyper-V.</span></span> <span data-ttu-id="3faef-176">드라이버는 [이 위치](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-176">The drivers can be found [at this location](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409).</span></span> <span data-ttu-id="3faef-177">RHEL **6.4 이상** 및 파생 버전에서는 LIS 드라이버가 커널에 이미 포함되어 있으므로 Azure에서 해당 시스템을 실행하기 위해 추가 설치 패키지가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-177">As of RHEL **6.4+** (and derivatives) the LIS drivers are already included with the kernel and so no additional installation packages are needed to run those systems on Azure.</span></span>

<span data-ttu-id="3faef-178">사용자 지정 커널이 필요한 경우, 최신 커널 버전(예: **3.8 이상**)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-178">If a custom kernel is required, it is recommended to use a more recent kernel version (i.e. **3.8+**).</span></span> <span data-ttu-id="3faef-179">자체 커널을 유지 관리하는 배포나 공급업체의 경우, 업스트림 커널에서 사용자 지정 커널로 LIS 드라이버를 정기적으로 백포팅하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-179">For those distributions or vendors who maintain their own kernel, some effort will be required to regularly backport the LIS drivers from the upstream kernel to your custom kernel.</span></span>  <span data-ttu-id="3faef-180">비교적 최신 커널 버전을 이미 실행 중이더라도 LIS 드라이버의 업스트림 수정 사항을 계속 추적하여 필요한 경우 백포팅하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-180">Even if you are already running a relatively recent kernel version, it is highly recommended to keep track of any upstream fixes in the LIS drivers and backport those as needed.</span></span> <span data-ttu-id="3faef-181">LIS 드라이버 원본 파일의 위치는 Linux 커널 원본 트리의 [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) 파일에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-181">The location of the LIS driver source files is available in the [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) file in the Linux kernel source tree:</span></span>

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

<span data-ttu-id="3faef-182">최소한 다음과 같은 패치를 적용하지 않으면 Azure에서 문제가 발생하는 것으로 확인되었으므로 커널에 해당 패치가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-182">At a very minimum, the absence of the following patches have been known to cause problems on Azure and so these must be included in the kernel.</span></span> <span data-ttu-id="3faef-183">이 목록에는 모든 배포에 대해 완전한 전체 정보가 포함되어 있지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-183">This list is by no means exhaustive or complete for all distributions:</span></span>

* [<span data-ttu-id="3faef-184">ata_piix: 기본적으로 Hyper-V 드라이버로 디스크 연기</span><span class="sxs-lookup"><span data-stu-id="3faef-184">ata_piix: defer disks to the Hyper-V drivers by default</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [<span data-ttu-id="3faef-185">storvsc: RESET 경로의 전송 중인 패킷용 계정</span><span class="sxs-lookup"><span data-stu-id="3faef-185">storvsc: Account for in-transit packets in the RESET path</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [<span data-ttu-id="3faef-186">storvsc: WRITE_SAME을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3faef-186">storvsc: avoid usage of WRITE_SAME</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [<span data-ttu-id="3faef-187">storvsc: RAID 및 가상 호스트 어댑터 드라이버에 대한 WRITE SAME 해제</span><span class="sxs-lookup"><span data-stu-id="3faef-187">storvsc: Disable WRITE SAME for RAID and virtual host adapter drivers</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [<span data-ttu-id="3faef-188">storvsc: NULL 포인터 역참조 수정</span><span class="sxs-lookup"><span data-stu-id="3faef-188">storvsc: NULL pointer dereference fix</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [<span data-ttu-id="3faef-189">storvsc: 링 버퍼 오류로 I/O가 중지됨</span><span class="sxs-lookup"><span data-stu-id="3faef-189">storvsc: ring buffer failures may result in I/O freeze</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [<span data-ttu-id="3faef-190">scsi_sysfs: __scsi_remove_device 이중 실행 방지</span><span class="sxs-lookup"><span data-stu-id="3faef-190">scsi_sysfs: protect against double execution of __scsi_remove_device</span></span>](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="the-azure-linux-agent"></a><span data-ttu-id="3faef-191">Azure Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="3faef-191">The Azure Linux Agent</span></span>
<span data-ttu-id="3faef-192">Azure에서 Linux 가상 컴퓨터를 올바르게 프로비전하려면 [Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-192">The [Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) is required to properly provision a Linux virtual machine in Azure.</span></span> <span data-ttu-id="3faef-193">[Linux Agent GitHub 리포지토리](https://github.com/Azure/WALinuxAgent)에서 최신 버전을 가져오거나 문제를 보고하거나 끌어오기 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-193">You can get the latest version, file issues or submit pull requests at the [Linux Agent GitHub repo](https://github.com/Azure/WALinuxAgent).</span></span>

* <span data-ttu-id="3faef-194">Linux 에이전트는 Apache 2.0 라이선스 하에서 릴리스되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-194">The Linux agent is released under the Apache 2.0 license.</span></span> <span data-ttu-id="3faef-195">대부분의 배포에서는 에이전트의 RPM 또는 deb 패키지가 이미 제공되므로 매우 간편하게 이러한 패키지를 설치 및 업데이트할 수 있는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-195">Many distributions already provide RPM or deb packages for the agent, and so in some cases this can be installed and updated with little effort.</span></span>
* <span data-ttu-id="3faef-196">Azure Linux 에이전트를 사용하려면 Python v2.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-196">The Azure Linux Agent requires Python v2.6+.</span></span>
* <span data-ttu-id="3faef-197">또한 에이전트에는 python-pyasn1 모듈도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-197">The agent also requires the python-pyasn1 module.</span></span> <span data-ttu-id="3faef-198">대부분의 배포에서는 이 모듈이 설치 가능한 별도의 패키지로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-198">Most distributions provide this as a separate package that can be installed.</span></span>
* <span data-ttu-id="3faef-199">Azure Linux 에이전트가 NetworkManager와 호환되지 않는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-199">In some cases the Azure Linux Agent may not be compatible with NetworkManager.</span></span> <span data-ttu-id="3faef-200">배포를 통해 제공되는 RPM/Deb 패키지는 대부분 NetworkManager를 waagent 패키지에 대한 충돌 항목으로 구성하므로 Linux 에이전트 패키지 설치 시 NetworkManager가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-200">Many of the RPM/Deb packages provided by distributions configure NetworkManager as a conflict to the waagent package, and thus will uninstall NetworkManager when you install the Linux agent package.</span></span>

## <a name="general-linux-system-requirements"></a><span data-ttu-id="3faef-201">일반 Linux 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3faef-201">General Linux System Requirements</span></span>

* <span data-ttu-id="3faef-202">다음 매개 변수를 포함하려면 GRUB 또는 GRUB2의 커널 부팅 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-202">Modify the kernel boot line in GRUB or GRUB2 to include the following parameters.</span></span> <span data-ttu-id="3faef-203">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-203">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues:</span></span>
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    <span data-ttu-id="3faef-204">이렇게 하면 모든 콘솔 메시지가 첫 번째 직렬 포트로 전송되므로 Azure 지원에서 문제를 디버깅하는 데에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-204">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
  
    <span data-ttu-id="3faef-205">위의 작업을 수행하는 동시에 다음 매개 변수도 있는 경우 *제거* 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-205">In addition to the above, it is recommended to *remove* the following parameters if they exist:</span></span>
  
        rhgb quiet crashkernel=auto
  
    <span data-ttu-id="3faef-206">모든 로그를 직렬 포트로 보내려는 클라우드 환경에서는 그래픽 및 자동 부팅 기능이 효율적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-206">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="3faef-207">원하는 경우에는 `crashkernel` 옵션을 구성한 상태로 유지할 수도 있지만 이 매개 변수를 사용하는 경우 VM에서 사용 가능한 메모리의 양이 128MB 이상 감소하므로 VM 크기가 작은 경우 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-207">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

* <span data-ttu-id="3faef-208">Azure Linux 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="3faef-208">Installing the Azure Linux Agent</span></span>
  
    <span data-ttu-id="3faef-209">Azure에서 Linux 이미지를 프로비전하려면 Azure Linux 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-209">The Azure Linux Agent is required for provisioning a Linux image on Azure.</span></span>  <span data-ttu-id="3faef-210">대부분의 배포에서는 에이전트를 RPM 또는 Deb 패키지로 제공합니다. 패키지의 이름은 보통 'WALinuxAgent' 또는 'walinuxagent'입니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-210">Many distributions provide the agent as an RPM or Deb package (the package is typically called 'WALinuxAgent' or 'walinuxagent').</span></span>  <span data-ttu-id="3faef-211">[Linux 에이전트 가이드](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 단계를 수행하여 에이전트를 수동으로 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-211">The agent can also be installed manually by following the steps in the [Linux Agent Guide](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

* <span data-ttu-id="3faef-212">SSH 서버가 설치되어 부팅 시 시작되도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-212">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="3faef-213">보통 SSH 서버는 기본적으로 이와 같이 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-213">This is usually the default.</span></span>

* <span data-ttu-id="3faef-214">OS 디스크에 스왑 공간을 만들지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3faef-214">Do not create swap space on the OS disk</span></span>
  
    <span data-ttu-id="3faef-215">Azure Linux 에이전트는 Azure에서 프로비전한 후 VM에 연결된 로컬 리소스 디스크를 사용하여 자동으로 스왑 공간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-215">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="3faef-216">로컬 리소스 디스크는 *임시* 디스크이며 VM의 프로비전을 해제할 때 비워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-216">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="3faef-217">Azure Linux 에이전트를 설치한 후(이전 단계 참조) /etc/waagent.conf에서 다음 매개 변수를 적절하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-217">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

* <span data-ttu-id="3faef-218">마지막 단계로 다음 명령을 실행하여 가상 컴퓨터의 프로비전을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-218">As a final step, run the following commands to deprovision the virtual machine:</span></span>
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > <span data-ttu-id="3faef-219">Virtualbox에서 'waagent-force-deprovision'을 실행한 후 다음 오류가 표시될 수 있습니다. `[Errno 5] Input/output error`</span><span class="sxs-lookup"><span data-stu-id="3faef-219">On Virtualbox you may see the following error after running 'waagent -force -deprovision': `[Errno 5] Input/output error`.</span></span> <span data-ttu-id="3faef-220">이 오류 메시지는 중요하지 않으므로 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-220">This error message is not critical and can be ignored.</span></span>
  > 
  > 

* <span data-ttu-id="3faef-221">그런 다음 가상 컴퓨터를 종료하고 VHD를 Azure에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3faef-221">You will then need to shut down the virtual machine and upload the VHD to Azure.</span></span>

