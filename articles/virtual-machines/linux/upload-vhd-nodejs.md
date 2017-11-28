---
title: "Azure CLI 1.0으로 사용자 지정 Linux 이미지 업로드 | Microsoft Docs"
description: "Resource Manager 배포 모델 및 Azure CLI 1.0을 사용하여 사용자 지정 Linux 이미지로 Azure에 VHD(가상 하드 디스크)를 만들고 업로드합니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="e42c0-103">Azure CLI 1.0을 사용하여 사용자 지정 디스크 이미지에서 Linux VM 업로드 및 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="e42c0-104">이 문서에서는 Resource Manager 배포 모델을 사용하여 VHD(가상 하드 디스크)를 Azure에 업로드하고 이 사용자 지정 이미지에서 Linux VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="e42c0-105">이 기능을 사용하면 Linux 배포판을 요구에 맞게 설치 및 구성하고 해당 VHD를 사용하여 Azure 가상 컴퓨터 (Vm)를 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e42c0-106">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="e42c0-106">CLI versions to complete the task</span></span>
<span data-ttu-id="e42c0-107">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="e42c0-108">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="e42c0-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e42c0-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="e42c0-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e42c0-110">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="e42c0-110">Quick commands</span></span>
<span data-ttu-id="e42c0-111">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 Azure에 VM을 업로드하는 기본 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e42c0-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="e42c0-112">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#requirements) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e42c0-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="e42c0-113">[Azure CLI 1.0](../../cli-install-nodejs.md)에 로그인하여 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e42c0-114">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e42c0-115">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="e42c0-116">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-116">First, create a resource group.</span></span> <span data-ttu-id="e42c0-117">다음 예제에서는 `WestUs` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="e42c0-118">가상 디스크를 보유할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="e42c0-119">다음 예제에서는 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="e42c0-120">저장소 계정의 선택키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-120">List the access keys for your storage account.</span></span> <span data-ttu-id="e42c0-121">`key1`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="e42c0-122">획득한 저장소 키를 사용하여 저장소 계정 내에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="e42c0-123">다음 예제에서는 `key1`의 저장소 키 값을 사용하여 `myimages`라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="e42c0-124">마지막으로, 만든 컨테이너에 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="e42c0-125">`/path/to/disk/mydisk.vhd` 아래에 VHD의 로컬 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="e42c0-126">이제 [Resource Manager 템플릿을 사용하여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)업로드된 가상 디스크에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="e42c0-127">또한 다음과 같이 디스크에 대한 URI(`--image-urn`)를 지정하여 CLI를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="e42c0-128">다음 예제에서는 이전에 업로드한 가상 디스크를 사용하여 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="e42c0-129">대상 저장소 계정은 가상 디스크를 업로드한 곳과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="e42c0-130">또한 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 `azure vm create` 명령이 필요로 하는 모든 추가 매개 변수를 지정하거나 프롬프트에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="e42c0-131">[사용 가능한 CLI Resource Manager 매개 변수](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="e42c0-132">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e42c0-132">Requirements</span></span>
<span data-ttu-id="e42c0-133">다음 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="e42c0-134">**.vhd 파일에 설치된 Linux 운영 체제** - 가상 디스크에 VHD 형식으로 [Azure 보증 Linux 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(또는 [보증되지 않는 배포에 대한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 참조)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="e42c0-135">VM과 VHD를 만드는 도구는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="e42c0-136">[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM)을 설치 및 구성하고 VHD를 이미지 형식으로 사용하도록 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="e42c0-137">필요한 경우 `qemu-img convert`를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="e42c0-138">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e42c0-139">새 VHDX 형식은 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="e42c0-140">VM을 만들 때 VHD를 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="e42c0-141">필요하다면 [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet을 사용하여 VHDX 디스크를 VHD로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="e42c0-142">그뿐 아니라 Azure는 동적 VHD 업로드를 지원하지 않으므로 업로드하기 전에 이러한 디스크를 정적 VHD로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="e42c0-143">Azure로 업로딩하는 과정 중에 [GO용 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) 와 같은 도구를 사용하여 동적 디스크를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="e42c0-144">사용자 지정 이미지에서 생성된 VM은 이미지 자체와 동일한 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="e42c0-145">사용자 지정 이미지와 생성된 VM을 모두 저장할 저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="e42c0-146">모든 VM을 만든 후 이미지를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="e42c0-147">[Azure CLI 1.0](../../cli-install-nodejs.md)에 로그인하여 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e42c0-148">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e42c0-149">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="e42c0-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e42c0-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="e42c0-151">업로드할 이미지 준비</span><span class="sxs-lookup"><span data-stu-id="e42c0-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="e42c0-152">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="e42c0-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="e42c0-153">다음 문서에서는 Azure에서 지원되는 다양한 Linux 배포를 준비하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="e42c0-154">**[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-158">**[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e42c0-160">**[기타 - 보증되지 않는 배포](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e42c0-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="e42c0-161">또한 Azure용 Linux 이미지를 준비하는 방법에 대한 일반적인 추가 팁은 **[Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e42c0-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e42c0-162">[Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 '지원되는 버전'에 지정된 대로 보증 배포판 중 하나가 구성 세부 정보와 함께 사용되는 경우에만 Linux를 실행하는 VM에 [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="e42c0-163">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-163">Create a resource group</span></span>
<span data-ttu-id="e42c0-164">리소스 그룹은 가상 네트워킹 및 저장소와 같은 가상 컴퓨터를 지원하기 위해 논리적으로 모든 Azure 리소스를 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="e42c0-165">[여기서 Azure 리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e42c0-166">사용자 지정 디스크 이미지를 업로드하고 VM을 만들기 전에 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="e42c0-167">다음 예제에서는 `WestUS` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e42c0-168">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-168">Create a storage account</span></span>
<span data-ttu-id="e42c0-169">VM은 저장소 계정 내에서 페이지 blob으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="e42c0-170">[여기서 Azure Blob 저장소](../../storage/common/storage-introduction.md#blob-storage)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="e42c0-171">사용자 지정 디스크 이미지 및 VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="e42c0-172">사용자 지정 디스크 이미지에서 만든 모든 VM는 그 이미지와 동일한 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="e42c0-173">다음 예제에서는 이전에 만든 리소스 그룹에 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="e42c0-174">저장소 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="e42c0-174">List storage account keys</span></span>
<span data-ttu-id="e42c0-175">Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="e42c0-176">이러한 선택키는 쓰기 작업을 수행할 때와 같이 저장소 계정에 인증할 때에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="e42c0-177">[여기서 저장소에 대한 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="e42c0-178">`azure storage account keys list` 명령을 사용하여 선택키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="e42c0-179">만든 저장소 계정에 대한 선택키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="e42c0-180">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="e42c0-181">다음 단계에서 저장소 계정과 상호 작용하는 데 사용할 수 있도록 `key1` 을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="e42c0-182">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-182">Create a storage container</span></span>
<span data-ttu-id="e42c0-183">로컬 파일 시스템을 논리적으로 구성하기 위해 서로 다른 디렉터리를 만드는 것과 같은 방식으로 가상 디스크 및 이미지를 구성하기 위해 저장소 계정 내에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="e42c0-184">저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="e42c0-185">다음 예제에서는 이전 단계에서 얻은 선택키(`key1`)를 지정하여 `myimages`라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="e42c0-186">VHD를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-186">Upload VHD</span></span>
<span data-ttu-id="e42c0-187">이제 사용자 지정 디스크 이미지를 실제로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="e42c0-188">VM이 사용하는 모든 가상 디스크를 통해 사용자 지정 디스크 이미지를 페이지 Blob으로 업로드하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="e42c0-189">선택키 및 이전 단계에서 만든 컨테이너를 지정한 후, 로컬 컴퓨터에 있는 사용자 지정 디스크 이미지의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="e42c0-190">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-190">Create VM from custom image</span></span>
<span data-ttu-id="e42c0-191">사용자 지정 디스크 이미지에서 VM을 만들 때 디스크 이미지에 대한 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="e42c0-192">대상 저장소 계정이 사용자 지정 디스크 이미지가 저장된 저장소 계정과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="e42c0-193">Azure CLI 또는 Resource Manager JSON 템플릿을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="e42c0-194">Azure CLI를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="e42c0-195">`azure vm create` 명령을 사용하여 `--image-urn` 매개 변수가 사용자 지정 디스크 이미지를 가리키도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="e42c0-196">`--storage-account-name` 사용자 지정 디스크 이미지가 저장된 저장소 계정와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="e42c0-197">사용자 지정 디스크 이미지와 같은 컨테이너를 사용하여 VM을 저장할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="e42c0-198">사용자 지정 디스크 이미지를 업로드하기 전에 이전 단계와 동일한 방식으로 모든 추가 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="e42c0-199">다음 예제에서는 사용자 지정 디스크 이미지에서 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="e42c0-200">또한 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 `azure vm create` 명령이 필요로 하는 모든 추가 매개 변수를 지정하거나 프롬프트에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="e42c0-201">[사용 가능한 CLI Resource Manager 매개 변수](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="e42c0-202">JSON 템플릿을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e42c0-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="e42c0-203">Azure Resource Manager 템플릿은 구축하려는 환경을 정의하는 JSON (JavaScript Notation) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="e42c0-204">템플릿은 계산 또는 네트워크과 같은 다양한 리소스 공급자로 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="e42c0-205">기존 템플릿을 사용하거나 직접 템플릿을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="e42c0-206">[Resource Manager 및 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="e42c0-207">템플릿의 `Microsoft.Compute/virtualMachines` 공급자 내에 VM에 대한 구성 세부 정보를 포함하는 `storageProfile` 노드가 있게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="e42c0-208">편집할 두 가지 주요 매개 변수는 사용자 지정 디스크 이미지와 새 VM의 가상 디스크를 가리키는 `image`과 `vhd` URI입니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="e42c0-209">다음은 사용자 지정 디스크 이미지 사용에 대한 JSON의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-209">The following shows an example of the JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="e42c0-210">[사용자 지정 이미지에서 VM을 만드는 데 이 기존 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)을 사용할 수 있거나 [고유한 Azure Resource Manager 템플릿 만들기](../../azure-resource-manager/resource-group-authoring-templates.md)에 관해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="e42c0-211">템플릿을 구성했다면 `azure group deployment create` 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="e42c0-212">`--template-uri` 매개 변수를 사용하여 JSON 템플릿의 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="e42c0-213">컴퓨터에 로컬로 저장된 JSON 파일이 있다면 `--template-file` 매개 변수를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="e42c0-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e42c0-214">Next steps</span></span>
<span data-ttu-id="e42c0-215">사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e42c0-216">또한 새 Vm에 [데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 고려할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="e42c0-217">응용 프로그램이 액세스해야 할 Vm에서 실행되고 있다면 반드시 [포트 및 끝점 열기](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c0-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

