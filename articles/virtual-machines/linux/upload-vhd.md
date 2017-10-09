---
title: "aaaUpload 또는 Azure CLI 2.0을 사용 하 여 사용자 지정 Linux VM 복사 | Microsoft Docs"
description: "업로드 하거나 복사할 hello 리소스 관리자 배포 모델 및 hello Azure CLI 2.0을 사용 하 여 사용자 지정된 가상 컴퓨터"
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
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="6b224-103">Azure CLI 2.0 hello로 사용자 지정 디스크에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="6b224-104">이 문서에서는 어떻게 tooupload 사용자 지정 된 가상 하드 디스크 (VHD) 또는 복사는 Azure에서 기존 VHD hello 사용자 지정 디스크에서 새 Linux 가상 컴퓨터 (Vm)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="6b224-105">설치 하 고 Linux 배포판 tooyour 요구 사항을 구성 하 고 다음 해당 VHD를 사용 하 여 수 tooquickly 새 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="6b224-106">원할 경우 toocreate 여러 Vm 사용자 지정 된 디스크에서 VM 또는 VHD에서 이미지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="6b224-107">자세한 내용은 참조 [hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지를 만드는](tutorial-custom-images.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="6b224-108">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-108">You have two options:</span></span>
* [<span data-ttu-id="6b224-109">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="6b224-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="6b224-110">기존 Azure VM 복사</span><span class="sxs-lookup"><span data-stu-id="6b224-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="6b224-111">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="6b224-111">Quick commands</span></span>

<span data-ttu-id="6b224-112">사용 하 여 새 VM을 만들 때 [az vm 만들기](/cli/azure/vm#create) 사용자 지정 또는 특수 한 디스크에서 있습니다 **연결** hello 디스크 (--os-디스크 연결)는 사용자 지정 또는 마켓플레이스 이미지를 지정 하는 대신 (-이미지).</span><span class="sxs-lookup"><span data-stu-id="6b224-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="6b224-113">hello 다음 예제에서는 V *myVM* hello를 사용 하 여 관리 하는 명명 된 디스크 *myManagedDisk* 사용자 지정 된 VHD에서 만든:</span><span class="sxs-lookup"><span data-stu-id="6b224-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="6b224-114">요구 사항</span><span class="sxs-lookup"><span data-stu-id="6b224-114">Requirements</span></span>
<span data-ttu-id="6b224-115">toocomplete hello 필요한 다음 단계를:</span><span class="sxs-lookup"><span data-stu-id="6b224-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="6b224-116">Azure에서 사용하기 위해 준비된 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="6b224-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="6b224-117">hello [준비 hello VM](#prepare-the-vm) 이 문서의 단원에 어떻게 toofind distro 설치에 대 한 정보 hello 필요 하면 toobe 수 tooconnect 및 Azure에서 제대로 VM toowork hello에 대 한 Azure Linux 에이전트 (waagent) SSH를 사용 하 여 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="6b224-118">기존 VHD 파일 hello [Linux Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (참조 또는 [비 보증 배포판에 대 한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 형식의 가상 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="6b224-119">VM 및 VHD toocreate 존재 하는 여러 도구:</span><span class="sxs-lookup"><span data-stu-id="6b224-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="6b224-120">설치 및 구성 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD 이미지 형식으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="6b224-121">필요한 경우 **qemu-img convert**를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="6b224-122">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6b224-123">Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="6b224-124">VM을 만들 때 hello 형식으로 VHD를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="6b224-125">필요한 경우 사용 하 여 VHDX 디스크 tooVHD 변환할 수 있습니다 [qemu img 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 hello [CONVERT-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b224-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="6b224-126">또한 Azure에서는 tooconvert 필요 하므로 동적 Vhd를 업로드 이러한 디스크 toostatic Vhd 업로드 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="6b224-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="6b224-127">와 같은 도구를 사용할 수 있습니다 [GO에 대 한 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure 업로드 프로세스 중 tooconvert 동적 디스크.</span><span class="sxs-lookup"><span data-stu-id="6b224-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="6b224-128">Hello 최신 있는지 확인 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="6b224-129">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6b224-130">예제 매개 변수 이름에는 *myResourceGroup*, *mystorageaccount* 및 *mydisks*가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="6b224-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="6b224-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="6b224-132">Hello VM 준비</span><span class="sxs-lookup"><span data-stu-id="6b224-132">Prepare hello VM</span></span>

<span data-ttu-id="6b224-133">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="6b224-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="6b224-134">다음 문서는 hello 어떻게 tooprepare hello Azure에서 지원 되는 다양 한 Linux 배포를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="6b224-135">CentOS 기반 배포</span><span class="sxs-lookup"><span data-stu-id="6b224-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="6b224-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6b224-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="6b224-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-139">SLES 및 openSUSE</span><span class="sxs-lookup"><span data-stu-id="6b224-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6b224-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="6b224-141">기타 - 보증되지 않는 배포</span><span class="sxs-lookup"><span data-stu-id="6b224-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="6b224-142">또한 hello를 참조 하십시오. [Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes) 보다 일반적인 방법에 대 한 azure Linux 이미지를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6b224-143">hello [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) tooVMs Linux를 실행 하 여 지원 버전에서 지정 된 대로 hello 구성 세부 정보를 사용 하는 분포를 지지 하는 hello 중 하나에 적용 됩니다. [Azure 보증에 Linux 분포](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="6b224-144">옵션 1: VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="6b224-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="6b224-145">로컬 컴퓨터에서 실행 중이거나 다른 클라우드에서 내보낸 사용자 지정된 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="6b224-146">tooupload hello VHD tooa 저장소가 필요한 toouse hello VHD toocreate 새 Azure VM 계정 및 hello VHD에서에서 관리 되는 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="6b224-147">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-147">Create a resource group</span></span>

<span data-ttu-id="6b224-148">사용자 지정 디스크를 업로드 하 고 Vm을 만들 하기 전에 먼저 toocreate 인 리소스 그룹과 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="6b224-149">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치: [Azure 관리 되는 디스크 개요](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6b224-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="6b224-150">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-150">Create a storage account</span></span>

<span data-ttu-id="6b224-151">[az storage account create](/cli/azure/storage/account#create)를 사용하여 사용자 지정 디스크 및 VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="6b224-152">hello 다음 예제에서는 저장소 계정인 *mystorageaccount* 이전에 만든 hello 리소스 그룹에서:</span><span class="sxs-lookup"><span data-stu-id="6b224-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="6b224-153">저장소 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="6b224-153">List storage account keys</span></span>
<span data-ttu-id="6b224-154">Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="6b224-155">이러한 액세스 키에는 쓰기 작업을 수행 하는 같은 toohello 저장소 계정에 인증할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="6b224-156">에 대해 자세히 알아보세요 [toostorage 여기에 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="6b224-157">Hello 액세스 키를 보면 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="6b224-158">만든 hello 저장소 계정에 대 한 hello 액세스 키 보기:</span><span class="sxs-lookup"><span data-stu-id="6b224-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="6b224-159">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="6b224-160">메모 **key1** 됩니다 사용할 toointeract hello 다음 단계에서 저장소 계정과 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="6b224-161">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-161">Create a storage container</span></span>
<span data-ttu-id="6b224-162">동일한 방식으로 다른 디렉터리 toologically 만드는 hello에 로컬 파일 시스템을 구성 하 고, 디스크 저장소 계정 tooorganize 내 컨테이너를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="6b224-163">저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="6b224-164">[az storage container create](/cli/azure/storage/container#create)를 사용하여 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="6b224-165">hello 다음 예에서는 라는 컨테이너를 만듭니다 *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="6b224-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="6b224-166">Hello VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="6b224-166">Upload hello VHD</span></span>
<span data-ttu-id="6b224-167">이제 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 사용자 지정 디스크 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="6b224-168">업로드하고 사용자 지정 디스크를 페이지 Blob으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="6b224-169">다음 경로 toohello 로컬 컴퓨터에 사용자 지정 디스크 hello 및 액세스 키, hello 이전 단계에서 만든 hello 컨테이너를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="6b224-170">VHD 업로드 hello 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="6b224-171">관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-171">Create a managed disk</span></span>


<span data-ttu-id="6b224-172">Hello VHD를 사용 하 여에서 관리 되는 디스크를 만들 [az 디스크 만들기](/cli/azure/disk#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="6b224-173">hello 다음 예제에서는 관리 되는 디스크 이름은 *myManagedDisk* 라는 저장소 계정 및 컨테이너 tooyour 업로드 한 VHD hello에서:</span><span class="sxs-lookup"><span data-stu-id="6b224-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="6b224-174">옵션 2: 기존 VM 복사</span><span class="sxs-lookup"><span data-stu-id="6b224-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="6b224-175">만들 수도 있습니다 hello 사용자 지정 된 VM에 Azure와 hello OS 디스크를 복사 하 고 새 VM toocreate tooa 연결 다른 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="6b224-176">테스트에 문제가 있지만 여러 새 Vm에 대 한 기존 Azure VM toouse hello 모델로 하려는 경우 실제로 만들어야는 **이미지** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="6b224-177">기존 Azure VM에서 이미지 만들기에 대 한 자세한 내용은 참조 [hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="6b224-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="6b224-178">스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-178">Create a snapshot</span></span>

<span data-ttu-id="6b224-179">이 예에서는 *myResourceGroup*이라는 리소스 그룹에 *myVM*이라는 VM의 스냅숏을 만들고 *osDiskSnapshot*이라는 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="6b224-180">Hello 관리 되는 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-180">Create hello managed disk</span></span>

<span data-ttu-id="6b224-181">Hello 스냅숏에서 새 관리 되는 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="6b224-182">Hello 스냅숏의 hello ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="6b224-183">이 예제에서는 hello 스냅숏 이름은 *osDiskSnapshot* hello에 속해 *myResourceGroup* 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="6b224-184">Hello 관리 되는 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-184">Create hello managed disk.</span></span> <span data-ttu-id="6b224-185">이 예제에서는 스냅숏에서 *myManagedDisk*라는 관리 디스크를 만들고 이는 표준 저장소에서 128GB 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="6b224-186">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6b224-186">Create hello VM</span></span>

<span data-ttu-id="6b224-187">이제를 사용 하 여 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 및 연결 (--os-디스크 연결) hello hello 운영 체제 디스크와 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="6b224-188">hello 다음 예제에서는 V *myNewVM* hello 관리를 사용 하 여 업로드 된 VHD에서 만든 디스크:</span><span class="sxs-lookup"><span data-stu-id="6b224-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="6b224-189">Hello VM에 수 tooSSH 있어야 hello 자격 증명을 사용 하 여 hello 소스 VM에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6b224-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b224-190">Next steps</span></span>
<span data-ttu-id="6b224-191">사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6b224-192">너무 필요가 있습니다[데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="6b224-193">Tooaccess 해야 하는 Vm에서 실행 하는 응용 프로그램의 경우 반드시 너무[포트와 끝점을 열어야](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b224-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

