---
title: "Azure에서 Linux VHD 다운로드 | Microsoft Docs"
description: "Azure CLI 및 Azure Portal을 사용하여 Linux VHD를 다운로드합니다."
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="fba6b-103">Azure에서 Linux VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="fba6b-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="fba6b-104">이 문서에서는 Azure CLI 및 Azure Portal을 사용하여 Azure에서[Linux VHD(가상 하드 디스크)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 파일을 다운로드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="fba6b-105">Azure에서 VM(가상 컴퓨터)은 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 [디스크](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="fba6b-106">모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="fba6b-107">운영 체제 디스크는 초기에 이미지에서 만들어지며, 운영 체제 디스크 및 이미지는 모두 Azure Storage 계정에 저장된 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="fba6b-108">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="fba6b-109">아직 수행하지 않았다면 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="fba6b-110">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-110">Stop the VM</span></span>

<span data-ttu-id="fba6b-111">실행 중인 VM에 연결된 경우 Azure에서 VHD는 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="fba6b-112">VHD를 다운로드하려면 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="fba6b-113">VHD를 [이미지](tutorial-custom-images.md)로 사용하여 새 디스크를 사용하는 다른 VM을 만들려는 경우 파일에 포함된 운영 체제를 프로비전 해제 및 일반화하고 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="fba6b-114">VHD를 기존 VM의 새 인스턴스에 대한 디스크 또는 데이터 디스크로 사용하려면 VM을 중지하고 할당 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="fba6b-115">VHD를 다른 VM을 만들기 위한 이미지로 사용하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="fba6b-116">VM의 SSH, 계정 이름 및 공용 IP 주소를 사용하여 연결하고 프로비전 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="fba6b-117">+user 매개 변수는 마지막 프로비전된 사용자 계정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="fba6b-118">계정 자격 증명을 VM에 굽는 경우 이 +user 매개 변수를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="fba6b-119">다음 예제는 마지막 프로비전된 사용자 계정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="fba6b-120">[az login](https://docs.microsoft.com/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="fba6b-121">VM을 중지 및 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="fba6b-122">VM을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="fba6b-123">VHD를 기존 VM의 새 인스턴스에 대한 디스크 또는 데이터 디스크로 사용하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="fba6b-124">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="fba6b-125">허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="fba6b-126">목록에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="fba6b-127">VM에 대한 블레이드에서 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-127">On the blade for the VM, click **Stop**.</span></span>

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="fba6b-129">SAS URL 생성</span><span class="sxs-lookup"><span data-stu-id="fba6b-129">Generate SAS URL</span></span>

<span data-ttu-id="fba6b-130">VHD 파일을 다운로드하려면 [SAS(공유 액세스 서명)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="fba6b-131">URL이 생성될 때 만료 시간이 URL에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="fba6b-132">VM에 대한 블레이드 메뉴에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="fba6b-133">VM에 대한 운영 체제 디스크를 선택한 다음 **내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="fba6b-134">**URL 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-134">Click **Generate URL**.</span></span>

    ![URL 생성](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="fba6b-136">VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="fba6b-136">Download VHD</span></span>

1.  <span data-ttu-id="fba6b-137">생성된 URL에서 VHD 파일 다운로드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="fba6b-139">다운로드를 시작하려면 브라우저에서 **저장**을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="fba6b-140">VHD 파일에 대한 기본 이름은 *abcd*입니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-140">The default name for the VHD file is *abcd*.</span></span>

    ![브라우저에서 저장 클릭](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="fba6b-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fba6b-142">Next steps</span></span>

- <span data-ttu-id="fba6b-143">[Azure CLI 2.0을 사용하여 사용자 지정 디스크에서 Linux VM 업로드 및 만들기](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fba6b-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="fba6b-144">[Azure CLI를 사용하여 Azure 디스크를 관리합니다](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fba6b-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

