---
title: "aaaCreate Linux VHD tooAzure 업로드 | Microsoft Docs"
description: "만들기 및 업로드는 Azure 가상 하드 디스크 (VHD) hello 클래식 배포 모델을 사용 하 여 hello Linux 운영 체제를 포함 하는"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="80db3-103">만들고 해당 Contains hello Linux 운영 체제 가상 하드 디스크를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="80db3-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="80db3-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="80db3-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="80db3-107">또한 [Azure Resource Manager를 사용하여 사용자 지정 디스크 이미지를 업로드](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="80db3-108">이 문서에서는 toocreate 및 업로드 가상 하드 디스크 (VHD)으로 사용할 수 있도록 Azure에서 가상 컴퓨터 toocreate 이미지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="80db3-109">Tooprepare hello 운영 체제 toocreate 사용할 수 있도록 여러 가상 컴퓨터에 따라 방법 해당 이미지에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="80db3-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="80db3-110">Prerequisites</span></span>
<span data-ttu-id="80db3-111">이 문서에서는 다음 항목 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="80db3-112">**.Vhd 파일에 설치 된 Linux 운영 체제** -설치 프로그램 [Linux Azure 보증 배포판](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (참조 또는 [비 보증 배포판에 대 한 정보](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa 가상 디스크 hello VHD 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="80db3-113">VM 및 VHD toocreate 존재 하는 여러 도구:</span><span class="sxs-lookup"><span data-stu-id="80db3-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="80db3-114">설치 및 구성 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 또는 [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD 이미지 형식으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="80db3-115">필요한 경우 `qemu-img convert`를 사용하여 [이미지를 변환](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="80db3-116">또한 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 또는 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx)에서 Hyper-V를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="80db3-117">Azure의 hello 새로운 VHDX 형식은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="80db3-118">VM을 만들 때 hello 형식으로 VHD를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="80db3-119">필요한 경우 사용 하 여 VHDX 디스크 tooVHD 변환할 수 있습니다 [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 또는 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80db3-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="80db3-120">또한 Azure에서는 tooconvert 필요 하므로 동적 Vhd를 업로드 이러한 디스크 toostatic Vhd 업로드 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="80db3-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="80db3-121">와 같은 도구를 사용할 수 있습니다 [GO에 대 한 Azure VHD 유틸리티](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure 업로드 프로세스 중 tooconvert 동적 디스크.</span><span class="sxs-lookup"><span data-stu-id="80db3-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="80db3-122">**Azure 명령줄 인터페이스** -설치 hello 최신 [Azure 명령줄 인터페이스](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="80db3-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="80db3-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="80db3-124">1 단계: hello 이미지 toobe 업로드 준비</span><span class="sxs-lookup"><span data-stu-id="80db3-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="80db3-125">Azure에서는 다양한 Linux 배포를 지원합니다( [보증 배포판](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)참조).</span><span class="sxs-lookup"><span data-stu-id="80db3-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="80db3-126">다음 문서는 hello 어떻게 tooprepare hello Azure에서 지원 되는 다양 한 Linux 배포 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="80db3-127">Hello hello 가이드에 나와 있는 단계를 완료 한 후 여기로 돌아와서 VHD 파일을 준비 tooupload tooAzure 있으면:</span><span class="sxs-lookup"><span data-stu-id="80db3-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="80db3-128">**[CentOS 기반 배포](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-132">**[SLES 및 openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="80db3-134">**[기타 - 보증되지 않는 배포](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="80db3-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="80db3-135">Azure 플랫폼 SLA hello 적용 Linux OS hello 중 하나로 보증 배포판 하는 경우에 지원 버전에서 지정 된 대로 구성 세부 정보 hello와 함께 사용 되는 hello를 실행 하는 toovirtual 컴퓨터 [Azure-Endorsed 배포판의 Linux ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80db3-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="80db3-136">모든 Linux 배포판 hello Azure 이미지 갤러리에는 hello 필요한 구성으로 보증 배포판입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="80db3-137">또한 hello를 참조 하십시오.  **[Linux 설치 참고 사항](../create-upload-generic.md#general-linux-installation-notes)**  보다 일반적인 방법에 대 한 azure Linux 이미지를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="80db3-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="80db3-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="80db3-139">2 단계: hello 연결 tooAzure 준비</span><span class="sxs-lookup"><span data-stu-id="80db3-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="80db3-140">Hello 클래식 배포 모델에 hello Azure CLI를 사용 하 고 있는지 확인 하십시오 (`azure config mode asm`), tooyour 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="80db3-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="80db3-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="80db3-142">3 단계: hello 이미지 tooAzure 업로드</span><span class="sxs-lookup"><span data-stu-id="80db3-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="80db3-143">저장소 계정 tooupload 프로그램 VHD 파일을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="80db3-144">기존 저장소 계정을 선택하거나 [새 계정을 만들 수 있습니다](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="80db3-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="80db3-145">다음 명령을 hello를 사용 하 여 hello Azure CLI tooupload hello 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="80db3-146">앞의 예에서 hello:</span><span class="sxs-lookup"><span data-stu-id="80db3-146">In hello previous example:</span></span>

* <span data-ttu-id="80db3-147">**BlobStorageURL** toouse 계획 hello 저장소 계정에 대 한 hello url</span><span class="sxs-lookup"><span data-stu-id="80db3-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="80db3-148">**YourImagesFolder** 은 blob 저장소 내의 컨테이너 hello toostore 이미지</span><span class="sxs-lookup"><span data-stu-id="80db3-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="80db3-149">**VHDName** 포털 tooidentify hello 가상 하드 디스크에 표시 되는 hello 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="80db3-150">**PathToVHDFile** 는 hello 전체 경로 컴퓨터에 hello.vhd 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="80db3-151">다음 명령을 hello는 전체 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="80db3-152">4 단계: hello 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="80db3-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="80db3-153">사용 하 여 VM을 만들 `azure vm create` hello에 동일한 방식으로 일반 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="80db3-154">Hello 이전 단계에서 이미지를 지정한 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="80db3-155">다음 예제는 hello를 사용 하 여 hello **myImage** hello 이전 단계에서 지정 된 이미지 이름.</span><span class="sxs-lookup"><span data-stu-id="80db3-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="80db3-156">toocreate Vm에 직접 자신의 사용자 이름 + 암호, 위치, DNS 이름 및 이미지 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80db3-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80db3-157">Next steps</span></span>
<span data-ttu-id="80db3-158">자세한 내용은 참조 [hello Azure 클래식 배포 모델에 대 한 Azure CLI 참조](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="80db3-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
