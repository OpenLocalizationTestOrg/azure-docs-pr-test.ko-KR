---
title: "Azure CLI 2.0을 사용하여 사용자 지정 Linux 디스크 업로드 | Microsoft Docs"
description: "Resource Manager 배포 모델 및 Azure CLI 2.0을 사용하여 Azure에 VHD(가상 하드 디스크) 만들기 및 업로드"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9159960af396e89f373da711e0cc46fdd996ab83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="876b5-103">Azure CLI 2.0을 사용하여 사용자 지정 디스크에서 Linux VM 업로드 및 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="876b5-104">이 문서에서는 Azure CLI 2.0을 사용하여 VHD(가상 하드 디스크)를 Azure Storage 계정에 업로드하고 이 사용자 지정 디스크에서 Linux VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-104">This article shows you how to upload a virtual hard disk (VHD) to an Azure storage account with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="876b5-105">[Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="876b5-106">이 기능을 사용하면 Linux 배포판을 요구에 맞게 설치 및 구성하고 해당 VHD를 사용하여 Azure 가상 컴퓨터 (Vm)를 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="876b5-107">이 항목에서는 최종 VHD에 대한 저장소 계정을 사용하지만 [Managed Disks](upload-vhd.md)를 사용하여 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-107">This topic uses storage accounts for the final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="876b5-108">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="876b5-108">Quick commands</span></span>
<span data-ttu-id="876b5-109">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 Azure에 VHD를 업로드하는 기본 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="876b5-109">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="876b5-110">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#requirements) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="876b5-110">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="876b5-111">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="876b5-112">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="876b5-113">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `mydisks`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="876b5-114">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="876b5-115">다음 예제에서는 `WestUs` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="876b5-116">[az storage account create](/cli/azure/storage/account#create)를 사용하여 가상 디스크를 보유할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-116">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="876b5-117">다음 예제에서는 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="876b5-118">[az storage account keys list](/cli/azure/storage/account/keys#list)를 사용하여 저장소 계정에 대한 액세스 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="876b5-119">`key1`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="876b5-120">[az storage container create](/cli/azure/storage/container#create)를 사용하여 획득한 저장소 키를 사용하여 저장소 계정 내에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="876b5-121">다음 예제에서는 `key1`의 저장소 키 값을 사용하여 `mydisks`라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="876b5-122">마지막으로 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 만든 컨테이너에 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="876b5-123">`/path/to/disk/mydisk.vhd` 아래에 VHD의 로컬 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="876b5-124">[az vm create](/cli/azure/vm#create)를 사용하여 디스크에 대한 URI를 지정합니다(`--image`).</span><span class="sxs-lookup"><span data-stu-id="876b5-124">Specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="876b5-125">다음 예제에서는 이전에 업로드한 가상 디스크를 사용하여 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-125">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="876b5-126">대상 저장소 계정은 가상 디스크를 업로드한 곳과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-126">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="876b5-127">또한 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 **az vm create** 명령이 필요로 하는 모든 추가 매개 변수를 지정하거나 프롬프트에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-127">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="876b5-128">[사용 가능한 CLI Resource Manager 매개 변수](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-128">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="876b5-129">요구 사항</span><span class="sxs-lookup"><span data-stu-id="876b5-129">Requirements</span></span>
<span data-ttu-id="876b5-130">다음 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-130">To complete the following steps, you need:</span></span>

* <span data-ttu-id="876b5-131">**.vhd 파일에 설치된 Linux 운영 체제** - 가상 디스크에 VHD 형식으로 [Azure 보증 Linux 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(또는 [보증되지 않는 배포에 대한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 참조)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="876b5-132">VM과 VHD를 만드는 도구는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-132">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="876b5-133">[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM)을 설치 및 구성하고 VHD를 이미지 형식으로 사용하도록 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="876b5-134">필요한 경우 `qemu-img convert`를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="876b5-135">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="876b5-136">새 VHDX 형식은 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-136">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="876b5-137">VM을 만들 때 VHD를 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-137">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="876b5-138">필요하다면 [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet을 사용하여 VHDX 디스크를 VHD로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-138">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="876b5-139">그뿐 아니라 Azure는 동적 VHD 업로드를 지원하지 않으므로 업로드하기 전에 이러한 디스크를 정적 VHD로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-139">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="876b5-140">Azure로 업로딩하는 과정 중에 [GO용 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) 와 같은 도구를 사용하여 동적 디스크를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="876b5-141">사용자 지정 디스크에서 생성된 VM은 디스크 자체와 동일한 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-141">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="876b5-142">사용자 지정 디스크와 생성된 VM을 모두 저장할 저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-142">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="876b5-143">모든 VM을 만든 후 디스크를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="876b5-144">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-144">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="876b5-145">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-145">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="876b5-146">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `mydisks`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="876b5-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="876b5-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="876b5-148">업로드할 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="876b5-148">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="876b5-149">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="876b5-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="876b5-150">다음 문서에서는 Azure에서 지원되는 다양한 Linux 배포를 준비하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-150">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="876b5-151">**[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-155">**[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="876b5-157">**[기타 - 보증되지 않는 배포](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="876b5-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="876b5-158">또한 Azure용 Linux 이미지를 준비하는 방법에 대한 일반적인 추가 팁은 **[Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="876b5-158">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="876b5-159">[Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 '지원되는 버전'에 지정된 대로 보증 배포판 중 하나가 구성 세부 정보와 함께 사용되는 경우에만 Linux를 실행하는 VM에 [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-159">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="876b5-160">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-160">Create a resource group</span></span>
<span data-ttu-id="876b5-161">리소스 그룹은 가상 네트워킹 및 저장소와 같은 가상 컴퓨터를 지원하기 위해 논리적으로 모든 Azure 리소스를 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-161">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="876b5-162">리소스 그룹에 대한 자세한 내용은 [리소스 그룹 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="876b5-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="876b5-163">사용자 지정 디스크를 업로드하고 VM을 만들기 전에 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-163">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="876b5-164">다음 예제에서는 `westus` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-164">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="876b5-165">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-165">Create a storage account</span></span>

<span data-ttu-id="876b5-166">[az storage account create](/cli/azure/storage/account#create)를 사용하여 사용자 지정 디스크 및 VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="876b5-167">사용자 지정 디스크에서 관리되지 않는 디스크를 만든 모든 VM은 그 디스크와 동일한 저장소 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-167">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> 

<span data-ttu-id="876b5-168">다음 예제에서는 이전에 만든 리소스 그룹에 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-168">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="876b5-169">저장소 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="876b5-169">List storage account keys</span></span>
<span data-ttu-id="876b5-170">Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="876b5-171">이러한 선택키는 쓰기 작업을 수행할 때와 같이 저장소 계정에 인증할 때에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-171">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="876b5-172">[여기서 저장소에 대한 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-172">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="876b5-173">[az storage account keys list](/cli/azure/storage/account/keys#list)를 사용하여 액세스 키를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-173">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="876b5-174">만든 저장소 계정에 대한 선택키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-174">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="876b5-175">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-175">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="876b5-176">다음 단계에서 저장소 계정과 상호 작용하는 데 사용할 수 있도록 `key1` 을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-176">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="876b5-177">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-177">Create a storage container</span></span>
<span data-ttu-id="876b5-178">로컬 파일 시스템을 논리적으로 구성하기 위해 서로 다른 디렉터리를 만드는 것과 같은 방식으로 디스크를 구성하기 위해 저장소 계정 내에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-178">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="876b5-179">저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="876b5-180">[az storage container create](/cli/azure/storage/container#create)를 사용하여 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="876b5-181">다음 예제에서는 `mydisks`라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-181">The following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="876b5-182">VHD를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-182">Upload VHD</span></span>
<span data-ttu-id="876b5-183">이제 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 사용자 지정 디스크 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="876b5-184">업로드하고 사용자 지정 디스크를 페이지 Blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="876b5-185">로컬 컴퓨터에 있는 사용자 지정 디스크에 선택키, 이전 단계에서 만든 컨테이너, 경로를 차례로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-185">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-the-vm"></a><span data-ttu-id="876b5-186">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="876b5-186">Create the VM</span></span>
<span data-ttu-id="876b5-187">관리되지 않는 디스크로 VM을 만들려면 [az vm create](/cli/azure/vm#create)를 사용하여 디스크(`--image`)에 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-187">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="876b5-188">다음 예제에서는 이전에 업로드한 가상 디스크를 사용하여 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-188">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="876b5-189">[az vm create](/cli/azure/vm#create)를 사용하여 `--image` 매개 변수가 사용자 지정 디스크를 가리키도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-189">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="876b5-190">`--storage-account`가 사용자 지정 디스크가 저장된 저장소 계정과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-190">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="876b5-191">사용자 지정 디스크와 동일한 컨테이너를 사용하여 VM을 저장할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-191">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="876b5-192">사용자 지정 디스크를 업로드하기 전에 이전 단계와 동일한 방식으로 모든 추가 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-192">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="876b5-193">다음 예제에서는 사용자 지정 디스크에서 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-193">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="876b5-194">또한 사용자 이름 및 SSH 키와 같은 **az vm create** 명령이 필요로 하는 모든 추가 매개 변수를 지정하거나 프롬프트에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-194">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="876b5-195">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="876b5-195">Resource Manager template</span></span>
<span data-ttu-id="876b5-196">Azure Resource Manager 템플릿은 구축하려는 환경을 정의하는 JSON (JavaScript Notation) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="876b5-197">템플릿은 계산 또는 네트워크과 같은 다양한 리소스 공급자로 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-197">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="876b5-198">기존 템플릿을 사용하거나 직접 템플릿을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="876b5-199">[Resource Manager 및 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="876b5-200">템플릿의 `Microsoft.Compute/virtualMachines` 공급자 내에 VM에 대한 구성 세부 정보를 포함하는 `storageProfile` 노드가 있게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-200">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="876b5-201">편집할 두 가지 주요 매개 변수는 사용자 지정 디스크와 새 VM의 가상 디스크를 가리키는 `image`과 `vhd` URI입니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-201">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="876b5-202">다음은 사용자 지정 디스크 사용에 대한 JSON의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-202">The following shows an example of the JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="876b5-203">[사용자 지정 이미지에서 VM을 만드는 데 이 기존 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)을 사용할 수 있거나 [고유한 Azure Resource Manager 템플릿 만들기](../../azure-resource-manager/resource-group-authoring-templates.md)에 관해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-203">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="876b5-204">템플릿을 구성했으면 [az group deployment create](/cli/azure/group/deployment#create)를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="876b5-205">`--template-uri` 매개 변수를 사용하여 JSON 템플릿의 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-205">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="876b5-206">컴퓨터에 로컬로 저장된 JSON 파일이 있다면 `--template-file` 매개 변수를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-206">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="876b5-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="876b5-207">Next steps</span></span>
<span data-ttu-id="876b5-208">사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="876b5-209">또한 새 Vm에 [데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 고려할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-209">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="876b5-210">응용 프로그램이 액세스해야 할 Vm에서 실행되고 있다면 반드시 [포트 및 끝점 열기](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="876b5-210">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

