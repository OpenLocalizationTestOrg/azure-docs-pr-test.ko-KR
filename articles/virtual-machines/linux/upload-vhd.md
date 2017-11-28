---
title: "Azure CLI 2.0으로 사용자 지정 Linux VM 업로드 또는 복사 | Microsoft Docs"
description: "Resource Manager 배포 모델 및 Azure CLI 2.0을 사용하여 사용자 지정된 가상 컴퓨터 업로드 및 복사"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 7c297725c26ea6c44403a10ecdcc3542f89f10b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="e1bf8-103">Azure CLI 2.0을 사용하여 사용자 지정 디스크에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="e1bf8-104">이 문서에서는 사용자 지정된 VHD(가상 하드 디스크)를 업로드하거나 Azure에서 기존 VHD를 복사하고 사용자 지정 디스크에서 새 Linux VM(가상 컴퓨터)을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="e1bf8-105">Linux 배포판을 요구에 맞게 설치 및 구성한 다음 해당 VHD를 사용하여 새 Azure 가상 컴퓨터를 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="e1bf8-106">사용자 지정된 디스크에서 여러 VM을 만들려는 경우 VM 또는 VHD에서 이미지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="e1bf8-107">자세한 내용은 [CLI를 사용하여 Azure VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="e1bf8-108">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-108">You have two options:</span></span>
* [<span data-ttu-id="e1bf8-109">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="e1bf8-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="e1bf8-110">기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="e1bf8-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="e1bf8-111">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="e1bf8-111">Quick commands</span></span>

<span data-ttu-id="e1bf8-112">사용자 지정된 또는 특수한 디스크에서 [az vm create](/cli/azure/vm#create)를 사용하여 새 VM을 만들 때 사용자 지정 또는 마켓플레이스 이미지(--image)를 지정하는 대신 디스크(--attach-os-disk)를 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="e1bf8-113">다음 예제에서는 사용자 지정된 VHD에서 만들어진 *myManagedDisk*라는 관리 디스크를 사용하여 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="e1bf8-114">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e1bf8-114">Requirements</span></span>
<span data-ttu-id="e1bf8-115">다음 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="e1bf8-116">Azure에서 사용하기 위해 준비된 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="e1bf8-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="e1bf8-117">이 문서의 [VM 준비](#prepare-the-vm) 섹션은 Azure에서 제대로 작동하고 SSH를 사용하여 연결하기 위해 VM에 필요한 Azure Linux 에이전트(waagent) 설치에 대한 배포판 특정 정보를 찾는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="e1bf8-118">기존 [Azure 보증 Linux 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 VHD 형식으로 가상 디스크에 VHD 파일(또는 [보증되지 않는 배포에 대한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 참조)</span><span class="sxs-lookup"><span data-stu-id="e1bf8-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="e1bf8-119">VM과 VHD를 만드는 도구는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="e1bf8-120">[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM)을 설치 및 구성하고 VHD를 이미지 형식으로 사용하도록 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="e1bf8-121">필요한 경우 **qemu-img convert**를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="e1bf8-122">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e1bf8-123">새 VHDX 형식은 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="e1bf8-124">VM을 만들 때 VHD를 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="e1bf8-125">필요하다면 [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet을 사용하여 VHDX 디스크를 VHD로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="e1bf8-126">그뿐 아니라 Azure는 동적 VHD 업로드를 지원하지 않으므로 업로드하기 전에 이러한 디스크를 정적 VHD로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="e1bf8-127">Azure로 업로딩하는 과정 중에 [GO용 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) 와 같은 도구를 사용하여 동적 디스크를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="e1bf8-128">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e1bf8-129">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e1bf8-130">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *mydisks*가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="e1bf8-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e1bf8-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="e1bf8-132">VM 준비</span><span class="sxs-lookup"><span data-stu-id="e1bf8-132">Prepare the VM</span></span>

<span data-ttu-id="e1bf8-133">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="e1bf8-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="e1bf8-134">다음 문서에서는 Azure에서 지원되는 다양한 Linux 배포를 준비하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="e1bf8-135">CentOS 기반 배포</span><span class="sxs-lookup"><span data-stu-id="e1bf8-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="e1bf8-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="e1bf8-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="e1bf8-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-139">SLES 및 openSUSE</span><span class="sxs-lookup"><span data-stu-id="e1bf8-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1bf8-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e1bf8-141">기타 - 보증되지 않는 배포</span><span class="sxs-lookup"><span data-stu-id="e1bf8-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="e1bf8-142">또한 Azure용 Linux 이미지를 준비하는 방법에 대한 일반적인 추가 팁은 [Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e1bf8-143">[Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)의 '지원되는 버전'에 지정된 대로 보증 배포판 중 하나가 구성 세부 정보와 함께 사용되는 경우에만 Linux를 실행하는 VM에 [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="e1bf8-144">옵션 1: VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="e1bf8-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="e1bf8-145">로컬 컴퓨터에서 실행 중이거나 다른 클라우드에서 내보낸 사용자 지정된 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="e1bf8-146">VHD를 사용하여 새 Azure VM을 만들려면 저장소 계정에 VHD를 업로드하고 VHD에서 관리 디스크를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="e1bf8-147">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-147">Create a resource group</span></span>

<span data-ttu-id="e1bf8-148">사용자 지정 디스크를 업로드하고 VM을 만들기 전에 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="e1bf8-149">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다. [Azure Managed Disks 개요](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e1bf8-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="e1bf8-150">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-150">Create a storage account</span></span>

<span data-ttu-id="e1bf8-151">[az storage account create](/cli/azure/storage/account#create)를 사용하여 사용자 지정 디스크 및 VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="e1bf8-152">다음 예제에서는 이전에 만든 리소스 그룹에 *mystorageaccount*라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="e1bf8-153">저장소 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="e1bf8-153">List storage account keys</span></span>
<span data-ttu-id="e1bf8-154">Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="e1bf8-155">이러한 선택키는 쓰기 작업을 수행할 때와 같이 저장소 계정에 인증할 때에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="e1bf8-156">[여기서 저장소에 대한 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="e1bf8-157">[az storage account keys list](/cli/azure/storage/account/keys#list)를 사용하여 액세스 키를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="e1bf8-158">만든 저장소 계정에 대한 선택키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="e1bf8-159">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="e1bf8-160">다음 단계에서 저장소 계정과 상호 작용하는 데 사용할 수 있도록 **key1**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="e1bf8-161">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-161">Create a storage container</span></span>
<span data-ttu-id="e1bf8-162">로컬 파일 시스템을 논리적으로 구성하기 위해 서로 다른 디렉터리를 만드는 것과 같은 방식으로 디스크를 구성하기 위해 저장소 계정 내에 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="e1bf8-163">저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="e1bf8-164">[az storage container create](/cli/azure/storage/container#create)를 사용하여 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="e1bf8-165">다음 예제에서는 *mydisks*라는 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="e1bf8-166">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="e1bf8-166">Upload the VHD</span></span>
<span data-ttu-id="e1bf8-167">이제 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 사용자 지정 디스크 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="e1bf8-168">업로드하고 사용자 지정 디스크를 페이지 Blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="e1bf8-169">로컬 컴퓨터에 있는 사용자 지정 디스크에 선택키, 이전 단계에서 만든 컨테이너, 경로를 차례로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="e1bf8-170">VHD를 업로드하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="e1bf8-171">관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-171">Create a managed disk</span></span>


<span data-ttu-id="e1bf8-172">[az disk create](/cli/azure/disk#create)를 사용하여 VHD에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="e1bf8-173">다음 예제에서는 다음과 같은 이름을 지정한 저장소 계정 및 컨테이너에 업로드한 VHD에서 *myManagedDisk*라는 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="e1bf8-174">옵션 2: 기존 VM 복사</span><span class="sxs-lookup"><span data-stu-id="e1bf8-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="e1bf8-175">Azure에서 사용자 지정된 VM을 만든 다음 OS 디스크를 복사하고 새 VM에 연결하여 다른 복사본을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="e1bf8-176">테스트에는 문제가 없지만 여러 새 VM에 대한 모델로 기존 Azure VM을 사용하려는 경우 **이미지**를 실제로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="e1bf8-177">기존 Azure VM에서 이미지 만들기에 대한 자세한 내용은 [CLI를 사용하여 Azure VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="e1bf8-178">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-178">Create a snapshot</span></span>

<span data-ttu-id="e1bf8-179">이 예에서는 *myResourceGroup*이라는 리소스 그룹에 *myVM*이라는 VM의 스냅숏을 만들고 *osDiskSnapshot*이라는 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="e1bf8-180">관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-180">Create the managed disk</span></span>

<span data-ttu-id="e1bf8-181">스냅숏에서 새 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="e1bf8-182">스냅숏의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="e1bf8-183">이 예제에서 스냅숏 이름은 *osDiskSnapshot*이며 *myResourceGroup* 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="e1bf8-184">관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-184">Create the managed disk.</span></span> <span data-ttu-id="e1bf8-185">이 예제에서는 스냅숏에서 *myManagedDisk*라는 관리 디스크를 만들고 이는 표준 저장소에서 128GB 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="e1bf8-186">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e1bf8-186">Create the VM</span></span>

<span data-ttu-id="e1bf8-187">이제 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들고 OS 디스크로 관리 디스크를 연결(--attach-os-disk)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="e1bf8-188">다음 예제에서는 업로드된 VHD에서 만들어진 관리 디스크를 사용하여 *myNewVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="e1bf8-189">원본 VM에서 자격 증명을 사용하여 VM으로 SSH할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e1bf8-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1bf8-190">Next steps</span></span>
<span data-ttu-id="e1bf8-191">사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e1bf8-192">또한 새 Vm에 [데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 고려할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="e1bf8-193">응용 프로그램이 액세스해야 할 Vm에서 실행되고 있다면 반드시 [포트 및 끝점 열기](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1bf8-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

