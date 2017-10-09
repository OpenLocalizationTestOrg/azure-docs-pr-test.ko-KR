---
title: "사용자 지정 Linux 이미지를 Azure CLI 1.0과 함께 aaaUpload | Microsoft Docs"
description: "페이지를 만들고 가상 하드 디스크 (VHD) tooAzure hello 리소스 관리자 배포 모델 및 hello Azure CLI 1.0을 사용 하 여 사용자 지정 Linux 이미지를 사용 하 여 업로드 합니다."
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
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="ad5eb-103">업로드 하 고 hello Azure CLI 1.0을 사용 하 여 사용자 지정 디스크 이미지에서 Linux VM을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="ad5eb-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="ad5eb-104">이 문서에는 사용 하 여 가상 하드 디스크 (VHD) tooAzure tooupload hello 리소스 관리자 배포 모델 및 Linux Vm의 경우이 사용자 지정 이미지를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="ad5eb-105">이 기능은 tooinstall 사용 하면 구성 Linux 배포판 tooyour 요구 하 고 다음 해당 VHD를 사용 하 여 tooquickly Azure 가상 컴퓨터 (Vm)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ad5eb-106">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="ad5eb-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="ad5eb-107">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="ad5eb-108">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="ad5eb-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ad5eb-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="ad5eb-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ad5eb-110">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="ad5eb-110">Quick commands</span></span>
<span data-ttu-id="ad5eb-111">Tooquickly 해야 할 경우 hello 작업을 수행, 다음 섹션의 세부 정보 hello hello 기본 명령을 tooupload VM tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="ad5eb-112">각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="ad5eb-113">확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="ad5eb-114">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ad5eb-115">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="ad5eb-116">먼저 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-116">First, create a resource group.</span></span> <span data-ttu-id="ad5eb-117">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUs` 위치:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="ad5eb-118">저장소 계정 toohold 가상 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="ad5eb-119">hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="ad5eb-120">저장소 계정에 대 한 hello 선택 키를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="ad5eb-121">`key1`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="ad5eb-122">가져온 hello 저장소 키를 사용 하 여 저장소 계정 내에서 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="ad5eb-123">hello 다음 예에서는 라는 컨테이너를 만듭니다 `myimages` hello 저장소 키 값을 사용 하 여 `key1`:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="ad5eb-124">마지막으로 만든 VHD toohello 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="ad5eb-125">Hello 로컬 경로 tooyour VHD 지정 아래 `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="ad5eb-126">이제 [Resource Manager 템플릿을 사용하여](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)업로드된 가상 디스크에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="ad5eb-127">Hello URI tooyour 디스크를 지정 하 여 hello CLI를 사용할 수도 있습니다 (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="ad5eb-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="ad5eb-128">hello 다음 예제에서는 V `myVM` 이전에 업로드 하는 hello 가상 디스크를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="ad5eb-129">hello 대상 저장소 계정에 가상 디스크를 업로드 하는 위치와 같은 hello toobe 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="ad5eb-130">모든 hello hello에 필요한 추가 매개 변수, 또한 toospecify, 필요에 대 한 프롬프트에 응답 또는 `azure vm create` 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="ad5eb-131">자세한 내용은 hello에 대 한 [CLI 리소스 관리자 매개 변수를 사용할 수 있는](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="ad5eb-132">요구 사항</span><span class="sxs-lookup"><span data-stu-id="ad5eb-132">Requirements</span></span>
<span data-ttu-id="ad5eb-133">toocomplete hello 필요한 다음 단계를:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="ad5eb-134">**.Vhd 파일에 설치 된 Linux 운영 체제** -설치 프로그램 [Linux Azure 보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (참조 또는 [비 보증 배포판에 대 한 정보](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD에서에서 가상 디스크 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="ad5eb-135">VM 및 VHD toocreate 존재 하는 여러 도구:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="ad5eb-136">설치 및 구성 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD 이미지 형식으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="ad5eb-137">필요한 경우 `qemu-img convert`를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="ad5eb-138">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ad5eb-139">Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ad5eb-140">VM을 만들 때 hello 형식으로 VHD를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="ad5eb-141">필요한 경우 사용 하 여 VHDX 디스크 tooVHD 변환할 수 있습니다 [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="ad5eb-142">또한 Azure에서는 tooconvert 필요 하므로 동적 Vhd를 업로드 이러한 디스크 toostatic Vhd 업로드 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="ad5eb-143">와 같은 도구를 사용할 수 있습니다 [GO에 대 한 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure 업로드 프로세스 중 tooconvert 동적 디스크.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="ad5eb-144">사용자 지정 이미지에서 만들어진 Vm에에서 상주해 야 hello 동일 hello 이미지 자체와 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="ad5eb-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="ad5eb-145">사용자 지정 이미지와 Vm을 만든된 저장소 계정 및 컨테이너 toohold 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="ad5eb-146">모든 VM을 만든 후 이미지를 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="ad5eb-147">확인 했는지 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 에 로그인 하 고 리소스 관리자 모드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="ad5eb-148">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ad5eb-149">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myimages`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="ad5eb-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="ad5eb-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="ad5eb-151">Hello 이미지 toobe 업로드 준비</span><span class="sxs-lookup"><span data-stu-id="ad5eb-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="ad5eb-152">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="ad5eb-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="ad5eb-153">다음 문서는 hello 어떻게 tooprepare hello Azure에서 지원 되는 다양 한 Linux 배포를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="ad5eb-154">**[CentOS 기반 배포](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-158">**[SLES 및 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ad5eb-160">**[기타 - 보증되지 않는 배포](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ad5eb-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="ad5eb-161">또한 hello를 참조 하십시오.  **[Linux 설치 참고 사항](create-upload-generic.md#general-linux-installation-notes)**  보다 일반적인 방법에 대 한 azure Linux 이미지를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="ad5eb-162">hello [Azure 플랫폼 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) tooVMs Linux를 실행 하 여 지원 버전에서 지정 된 대로 hello 구성 세부 정보를 사용 하는 분포를 지지 하는 hello 중 하나에 적용 됩니다. [Azure 보증에 Linux 분포](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="ad5eb-163">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-163">Create a resource group</span></span>
<span data-ttu-id="ad5eb-164">리소스 그룹 논리적으로 결합 하도록 모든 hello Azure 리소스 toosupport hello 가상 네트워킹 및 저장소와 같은 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="ad5eb-165">[여기서 Azure 리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ad5eb-166">사용자 지정 디스크 이미지를 업로드 하 고 Vm을 만들 하기 전에 먼저 toocreate 리소스 그룹을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="ad5eb-167">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUS` 위치:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="ad5eb-168">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-168">Create a storage account</span></span>
<span data-ttu-id="ad5eb-169">VM은 저장소 계정 내에서 페이지 blob으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="ad5eb-170">[여기서 Azure Blob 저장소](../../storage/common/storage-introduction.md#blob-storage)에 대해 자세히 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="ad5eb-171">사용자 지정 디스크 이미지 및 VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="ad5eb-172">에 사용자 지정 디스크 이미지 필요 toobe에서 만드는 모든 Vm 이미지와 동일한 저장소 계정을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="ad5eb-173">hello 다음 예제에서는 라는 저장소 계정을 `mystorageaccount` 이전에 만든 hello 리소스 그룹에:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="ad5eb-174">저장소 계정 키 나열</span><span class="sxs-lookup"><span data-stu-id="ad5eb-174">List storage account keys</span></span>
<span data-ttu-id="ad5eb-175">Azure는 각 저장소 계정에 대해 두 개의 512 비트 선택키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="ad5eb-176">이러한 액세스 키에는 쓰기 작업 toocarry 같은 toohello 저장소 계정에 인증할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="ad5eb-177">에 대해 자세히 알아보세요 [toostorage 여기에 액세스 관리](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="ad5eb-178">Hello로 선택 키를 볼 수 있습니다 `azure storage account keys list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="ad5eb-179">만든 hello 저장소 계정에 대 한 hello 액세스 키 보기:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="ad5eb-180">hello 출력은 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="ad5eb-181">메모 `key1` 됩니다 사용할 toointeract hello 다음 단계에서 저장소 계정과 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="ad5eb-182">저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-182">Create a storage container</span></span>
<span data-ttu-id="ad5eb-183">동일한 방식으로 다른 디렉터리 toologically 만드는 hello에 로컬 파일 시스템 구성, 가상 디스크 및 이미지 저장소 계정 tooorganize 내 컨테이너를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="ad5eb-184">저장소 계정에 포함할 수 있는 컨테이너의 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="ad5eb-185">hello 다음 예에서는 라는 컨테이너를 만듭니다 `myimages`, hello 이전 단계에서 얻은 hello 선택 키 지정 (`key1`):</span><span class="sxs-lookup"><span data-stu-id="ad5eb-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="ad5eb-186">VHD를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-186">Upload VHD</span></span>
<span data-ttu-id="ad5eb-187">이제 사용자 지정 디스크 이미지를 실제로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="ad5eb-188">VM이 사용하는 모든 가상 디스크를 통해 사용자 지정 디스크 이미지를 페이지 Blob으로 업로드하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="ad5eb-189">다음 로컬 컴퓨터의 경로 toohello 사용자 지정 디스크 이미지를 hello 및 액세스 키, hello 이전 단계에서 만든 hello 컨테이너를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="ad5eb-190">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-190">Create VM from custom image</span></span>
<span data-ttu-id="ad5eb-191">사용자 지정 디스크 이미지에서 Vm을 만들 때 hello URI toohello 디스크 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="ad5eb-192">사용자 지정 디스크 이미지가 저장 되어 있는 대상 저장소 계정 일치 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="ad5eb-193">Hello Azure CLI 또는 리소스 관리자 JSON 템플릿을 사용 하 여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="ad5eb-194">Hello Azure CLI를 사용 하 여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="ad5eb-195">Hello 지정 `--image-urn` hello로 매개 변수 `azure vm create` 명령 toopoint tooyour 사용자 지정 디스크 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="ad5eb-196">되도록 `--storage-account-name` 일치 hello 사용자 지정 디스크 이미지가 저장 되는 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="ad5eb-197">Hello 동일한 컨테이너 사용자 지정 디스크 이미지 toostore hello 대로 Vm toouse를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="ad5eb-198">있는지 toocreate는 다른 컨테이너에서 hello 확인 같은 방식으로 이전 단계에서 사용자 지정 디스크 이미지를 업로드 하기 전에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="ad5eb-199">hello 다음 예제에서는 V `myVM` 사용자 지정 디스크 이미지에서:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="ad5eb-200">모든 hello hello에 필요한 추가 매개 변수, 여전히 toospecify, 필요에 대 한 프롬프트에 응답 또는 `azure vm create` 가상 네트워크, 공용 IP 주소, 사용자 이름 및 SSH 키와 같은 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="ad5eb-201">Hello에 대 한 자세한 [CLI 리소스 관리자 매개 변수를 사용할 수 있는](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="ad5eb-202">JSON 템플릿을 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5eb-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="ad5eb-203">Azure 리소스 관리자 템플릿은 toobuild 원하는 hello 환경을 정의 하는 개체 JSON (JavaScript Notation) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="ad5eb-204">hello 템플릿 계산, 네트워크 등 toodifferent 리소스 공급자에서 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="ad5eb-205">기존 템플릿을 사용하거나 직접 템플릿을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="ad5eb-206">[Resource Manager 및 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="ad5eb-207">Hello 내 `Microsoft.Compute/virtualMachines` 있는 서식 파일의 공급자는 `storageProfile` 노드 VM에 대 한 hello 구성 세부 정보를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="ad5eb-208">hello 두 주요 매개 변수 tooedit는 hello `image` 및 `vhd` tooyour 사용자 지정 디스크 이미지와 새 VM의 가상 디스크를 가리키는 Uri입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="ad5eb-209">hello 다음 사용자 지정 디스크 이미지를 사용 하기 위한 hello JSON의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="ad5eb-210">사용할 수 있습니다 [사용자 지정 이미지에서 VM이 기존 템플릿 toocreate](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) 에 대 한 읽기 또는 [사용자 지정 Azure 리소스 관리자 템플릿을 만들어](../../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="ad5eb-211">Hello를 사용 하 여 Vm에 구성 된 템플릿을 있으면 만들면 `azure group deployment create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="ad5eb-212">Hello를 사용 하 여 hello JSON 서식 파일의 URI를 지정 `--template-uri` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="ad5eb-213">컴퓨터에 로컬로 저장 된 JSON 파일이 있는 경우에 hello을 사용할 수 있습니다 `--template-file` 매개 변수 대신:</span><span class="sxs-lookup"><span data-stu-id="ad5eb-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="ad5eb-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad5eb-214">Next steps</span></span>
<span data-ttu-id="ad5eb-215">사용자 지정 가상 디스크를 준비하고 업로드한 후 [Resource Manager 및 템플릿 사용하기](../../azure-resource-manager/resource-group-overview.md)에 관해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ad5eb-216">너무 필요가 있습니다[데이터 디스크 추가](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="ad5eb-217">Tooaccess 해야 하는 Vm에서 실행 하는 응용 프로그램의 경우 반드시 너무[포트와 끝점을 열어야](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5eb-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

