---
title: "Azure에서 Windows VHD 다운로드 | Microsoft Docs"
description: "Azure Portal을 사용하여 Windows VHD를 다운로드합니다."
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="eb666-103">Azure에서 Windows VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="eb666-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="eb666-104">이 문서에서는 Azure Portal을 사용하여 Azure에서 [Windows VHD(가상 하드 디스크)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 파일을 다운로드하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="eb666-105">Azure에서 VM(가상 컴퓨터)은 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 [디스크](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="eb666-106">모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="eb666-107">운영 체제 디스크는 초기에 이미지에서 만들어지며, 운영 체제 디스크 및 이미지는 모두 Azure Storage 계정에 저장된 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="eb666-108">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="eb666-109">VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-109">Stop the VM</span></span>

<span data-ttu-id="eb666-110">실행 중인 VM에 연결된 경우 Azure에서 VHD는 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="eb666-111">VHD를 다운로드하려면 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="eb666-112">VHD를 [이미지](tutorial-custom-images.md)로 사용하여 새 디스크를 사용하는 다른 VM을 만들려는 경우 [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation)를 사용하여 파일에 포함된 운영 체제를 일반화하고 VM을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="eb666-113">VHD를 기존 VM의 새 인스턴스에 대한 디스크 또는 데이터 디스크로 사용하려면 VM을 중지하고 할당 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="eb666-114">VHD를 다른 VM을 만들기 위한 이미지로 사용하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="eb666-115">아직 로그인하지 않은 경우 [Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="eb666-116">[VM에 연결합니다](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb666-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="eb666-117">VM에서 관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="eb666-118">디렉터리를 *%windir%\system32\sysprep*로 변경한 후 sysprep.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="eb666-119">시스템 준비 도구 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="eb666-120">종료 옵션에서 **종료**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="eb666-121">VHD를 기존 VM의 새 인스턴스에 대한 디스크 또는 데이터 디스크로 사용하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="eb666-122">Azure Portal에 있는 허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="eb666-123">목록에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="eb666-124">VM에 대한 블레이드에서 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-124">On the blade for the VM, click **Stop**.</span></span>

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="eb666-126">SAS URL 생성</span><span class="sxs-lookup"><span data-stu-id="eb666-126">Generate SAS URL</span></span>

<span data-ttu-id="eb666-127">VHD 파일을 다운로드하려면 [SAS(공유 액세스 서명)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="eb666-128">URL이 생성될 때 만료 시간이 URL에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="eb666-129">VM에 대한 블레이드 메뉴에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="eb666-130">VM에 대한 운영 체제 디스크를 선택한 다음 **내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="eb666-131">URL의 만료 시간을 *36000*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="eb666-132">**URL 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-132">Click **Generate URL**.</span></span>

    ![URL 생성](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="eb666-134">Windows Server 운영 체제에 대한 큰 VHD 파일을 다운로드하는 데 충분한 시간을 제공하기 위해 만료 시간은 기본 시간에서 증가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="eb666-135">Windows Server 운영 체제를 포함하는 VHD 파일은 사용자 연결에 따라 다운로드하는 데 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="eb666-136">데이터 디스크에 대한 VHD를 다운로드하는 경우 기본 시간은 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="eb666-137">VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="eb666-137">Download VHD</span></span>

1.  <span data-ttu-id="eb666-138">생성된 URL에서 VHD 파일 다운로드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="eb666-140">다운로드를 시작하려면 브라우저에서 **저장**을 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="eb666-141">VHD 파일에 대한 기본 이름은 *abcd*입니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-141">The default name for the VHD file is *abcd*.</span></span>

    ![브라우저에서 저장 클릭](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="eb666-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb666-143">Next steps</span></span>

- <span data-ttu-id="eb666-144">[Azure로 VHD 파일 업로드](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb666-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="eb666-145">[저장소 계정의 비관리 디스크에서 관리 디스크를 만듭니다](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb666-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="eb666-146">[PowerShell을 사용하여 Azure 디스크를 관리합니다](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb666-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

