---
title: "Azure에서 Linux VHD aaaDownload | Microsoft Docs"
description: "Hello Azure CLI를 사용 하 여 Linux VHD를 다운로드 하 고 hello Azure 포털."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="47c2e-103">Azure에서 Linux VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="47c2e-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="47c2e-104">이 문서에서는 설명 어떻게 toodownload는 [Linux 가상 하드 디스크 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure CLI 및 Azure 포털에서 사용 하 여 Azure 파일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="47c2e-105">사용 하 여 Azure에서 가상 컴퓨터 (Vm) [디스크](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 장소 toostore 운영 체제, 응용 프로그램 및 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="47c2e-106">모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="47c2e-107">처음 hello 운영 체제 디스크는 이미지에서 생성 하 고 hello 운영 체제 디스크와 hello 이미지는 Vhd는 Azure 저장소 계정에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="47c2e-108">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="47c2e-109">아직 수행하지 않았다면 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="47c2e-110">Hello VM 중지</span><span class="sxs-lookup"><span data-stu-id="47c2e-110">Stop hello VM</span></span>

<span data-ttu-id="47c2e-111">연결 되어 있는 경우 Azure에서 VHD를 다운로드할 수 없는 tooa VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="47c2e-112">Toostop hello VM toodownload VHD 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="47c2e-113">Toouse로 VHD를 원하는 경우는 [이미지](tutorial-custom-images.md) toocreate 다른 Vm 새 디스크로 toodeprovision 필요 하 고이 hello에 포함 된 hello 운영 체제를 일반화 파일 및 hello VM을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="47c2e-114">toouse hello VHD에 대 한 기존 VM 또는 데이터 디스크의 새 인스턴스를 디스크로 toostop 및 해야 hello VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="47c2e-115">toouse 다른 Vm VHD 이미지 toocreate로 hello 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="47c2e-116">SSH, hello 계정 이름 및 hello hello VM tooconnect tooit 공용 IP 주소 사용 하며 프로 비전 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="47c2e-117">안녕하세요 + 사용자 매개 변수는 또한 hello 마지막 프로 비전 된 사용자 계정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="47c2e-118">Toohello VM에에서 계정 자격 증명, 동작 하는 경우이 생략 + user 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="47c2e-119">hello 다음 예제에서는 hello 마지막 프로 비전 된 사용자 계정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="47c2e-120">Tooyour 된 Azure 계정 로그인 [az 로그인](https://docs.microsoft.com/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="47c2e-121">중지 하 고 hello VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="47c2e-122">Hello VM을 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="47c2e-123">toouse hello VHD를 디스크로 기존 VM 또는 데이터 디스크의 새 인스턴스를 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="47c2e-124">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="47c2e-125">Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="47c2e-126">Hello VM hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="47c2e-127">Hello VM에 대 한 hello 블레이드에서 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="47c2e-129">SAS URL 생성</span><span class="sxs-lookup"><span data-stu-id="47c2e-129">Generate SAS URL</span></span>

<span data-ttu-id="47c2e-130">toogenerate 해야 toodownload hello VHD 파일에는 [공유 액세스 서명 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL입니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="47c2e-131">Hello URL 생성 될 때 만료 시간 toohello URL이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="47c2e-132">Hello VM에 대 한 hello 블레이드의 hello 메뉴를 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="47c2e-133">VM hello에 대 한 hello 운영 체제 디스크를 선택한 다음 클릭 **내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="47c2e-134">**URL 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-134">Click **Generate URL**.</span></span>

    ![URL 생성](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="47c2e-136">VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="47c2e-136">Download VHD</span></span>

1.  <span data-ttu-id="47c2e-137">생성 된 hello URL에서 다운로드 hello VHD 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="47c2e-139">Tooclick 할 수 있습니다 **저장** hello 브라우저 toostart hello 다운로드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="47c2e-140">hello VHD 파일에 대 한 기본 이름은 hello *abcd*합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Hello 브라우저에서 저장을 클릭 합니다.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="47c2e-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47c2e-142">Next steps</span></span>

- <span data-ttu-id="47c2e-143">너무 방법에 대해 알아봅니다[업로드 하 고 Azure CLI 2.0 hello로 사용자 지정 디스크에서 Linux VM을 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="47c2e-144">[Azure 디스크 hello Azure CLI 관리](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="47c2e-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

