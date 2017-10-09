---
title: "Azure에서 Windows VHD aaaDownload | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 Windows VHD를 다운로드 합니다."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="34f5d-103">Azure에서 Windows VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="34f5d-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="34f5d-104">이 문서에서는 설명 어떻게 toodownload는 [Windows 가상 하드 디스크 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 사용 하 여 Azure에서 파일 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="34f5d-105">사용 하 여 Azure에서 가상 컴퓨터 (Vm) [디스크](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 장소 toostore 운영 체제, 응용 프로그램 및 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="34f5d-106">모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="34f5d-107">처음 hello 운영 체제 디스크는 이미지에서 생성 하 고 hello 운영 체제 디스크와 hello 이미지는 Vhd는 Azure 저장소 계정에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="34f5d-108">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="34f5d-109">Hello VM 중지</span><span class="sxs-lookup"><span data-stu-id="34f5d-109">Stop hello VM</span></span>

<span data-ttu-id="34f5d-110">연결 되어 있는 경우 Azure에서 VHD를 다운로드할 수 없는 tooa VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="34f5d-111">Toostop hello VM toodownload VHD 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="34f5d-112">Toouse로 VHD를 원하는 경우는 [이미지](tutorial-custom-images.md) toocreate 사용 하면 새 디스크와 다른 Vm에 [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello 파일에 포함 된 운영 체제 hello 및 hello VM을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="34f5d-113">toouse hello VHD에 대 한 기존 VM 또는 데이터 디스크의 새 인스턴스를 디스크로 toostop 및 해야 hello VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="34f5d-114">toouse 다른 Vm VHD 이미지 toocreate로 hello 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="34f5d-115">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="34f5d-116">[Toohello VM 연결](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="34f5d-117">Hello VM에서 관리자 권한으로 명령 프롬프트 창을 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="34f5d-118">Hello 디렉터리도 변경*%windir%\system32\sysprep* sysprep.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="34f5d-119">Hello 시스템 준비 도구 대화 상자에서 선택 **입력 시스템을 기본 OOBE (Experience)**, 있는지 확인 하 고 **일반화** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="34f5d-120">종료 옵션에서 **종료**를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="34f5d-121">toouse hello VHD를 디스크로 기존 VM 또는 데이터 디스크의 새 인스턴스를 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="34f5d-122">Hello Azure 포털에서에서 hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="34f5d-123">Hello VM hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="34f5d-124">Hello VM에 대 한 hello 블레이드에서 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="34f5d-126">SAS URL 생성</span><span class="sxs-lookup"><span data-stu-id="34f5d-126">Generate SAS URL</span></span>

<span data-ttu-id="34f5d-127">toogenerate 해야 toodownload hello VHD 파일에는 [공유 액세스 서명 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL입니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="34f5d-128">Hello URL 생성 될 때 만료 시간 toohello URL이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="34f5d-129">Hello VM에 대 한 hello 블레이드의 hello 메뉴를 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="34f5d-130">VM hello에 대 한 hello 운영 체제 디스크를 선택한 다음 클릭 **내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="34f5d-131">Hello URL의 hello 만료 시간을 너무 설정*36000*합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="34f5d-132">**URL 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-132">Click **Generate URL**.</span></span>

    ![URL 생성](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="34f5d-134">hello 만료 시간 toodownload hello 큰 VHD 파일에서 Windows Server 운영 체제에 대 한 충분 한 시간 hello 기본 tooprovide에서 증가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="34f5d-135">Windows Server 운영 체제 tootake hello 연결 방식에 따라 몇 시간 toodownload를 포함 하는 VHD 파일을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="34f5d-136">데이터 디스크에 대 한 VHD를 다운로드 하는 경우 hello 기본 시간은 충분 한입니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="34f5d-137">VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="34f5d-137">Download VHD</span></span>

1.  <span data-ttu-id="34f5d-138">생성 된 hello URL에서 다운로드 hello VHD 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="34f5d-140">Tooclick 할 수 있습니다 **저장** hello 브라우저 toostart hello 다운로드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="34f5d-141">hello VHD 파일에 대 한 기본 이름은 hello *abcd*합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Hello 브라우저에서 저장을 클릭 합니다.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="34f5d-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34f5d-143">Next steps</span></span>

- <span data-ttu-id="34f5d-144">너무 방법에 대해 알아봅니다[업로드할 VHD 파일 tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="34f5d-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="34f5d-145">[저장소 계정의 비관리 디스크에서 관리 디스크를 만듭니다](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34f5d-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="34f5d-146">[PowerShell을 사용하여 Azure 디스크를 관리합니다](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34f5d-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

