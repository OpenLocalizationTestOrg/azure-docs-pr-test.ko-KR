---
title: "Microsoft Azure Windows VM에 대한 디스크 및 VHD 정보 | Microsoft Docs"
description: "Azure의 Windows 가상 컴퓨터용 디스크 및 VHD의 기본 사항에 대해 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 34a4d8fa176484fbadb1b385d794cada5be607c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="f4d71-103">Azure Windows VM용 디스크 및 VHD 정보</span><span class="sxs-lookup"><span data-stu-id="f4d71-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="f4d71-104">다른 컴퓨터와 마찬가지로, Azure에서 가상 컴퓨터는 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="f4d71-105">모든 Azure 가상 컴퓨터는 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="f4d71-106">운영 체제 디스크는 이미지에서 만들어지며, 운영 체제 디스크 및 이미지 모두는 Azure 저장소 계정에 저장된 VHD(가상 하드 디스크)입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="f4d71-107">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="f4d71-108">이 문서에서는 디스크의 여러 가지 사용법에 대해 설명한 후 사용자가 만들고 사용할 수 있는 다양한 디스크 형식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="f4d71-109">이 문서는 [Linux 가상 컴퓨터](storage-about-disks-and-vhds-linux.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-109">This article is also available for [Linux virtual machines](storage-about-disks-and-vhds-linux.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="f4d71-110">VM에서 사용되는 디스크</span><span class="sxs-lookup"><span data-stu-id="f4d71-110">Disks used by VMs</span></span>

<span data-ttu-id="f4d71-111">VM에서 디스크를 사용하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="f4d71-112">운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="f4d71-112">Operating system disk</span></span>
<span data-ttu-id="f4d71-113">모든 가상 컴퓨터는 하나의 연결된 운영 체제 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="f4d71-114">이 디스크는 SATA 드라이브로 등록되며 기본적으로 C 드라이브로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="f4d71-115">이 디스크의 최대 용량은 2048기가바이트(GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="f4d71-116">임시 디스크</span><span class="sxs-lookup"><span data-stu-id="f4d71-116">Temporary disk</span></span>
<span data-ttu-id="f4d71-117">각 VM에는 임시 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="f4d71-118">이러한 임시 디스크는 응용 프로그램 및 프로세스에 대한 단기 저장소를 제공하며 페이지 또는 스왑 파일과 같은 데이터 저장에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="f4d71-119">임시 디스크의 데이터는 [유지 관리 이벤트](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) 또는 [VM을 다시 배포](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)할 때 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-119">Data on the temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f4d71-120">VM의 표준 다시 부팅 동안 임시 드라이브의 데이터가 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="f4d71-121">이 디스크는 일시적으로 D: 드라이브로 레이블이 지정되며 pagefile.sys를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="f4d71-122">이 디스크를 다른 드라이브 문자로 다시 매핑하려면 [Windows 임시 디스크의 드라이브 문자 변경](../virtual-machines/windows/change-drive-letter.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4d71-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md).</span></span> <span data-ttu-id="f4d71-123">임시 디스크의 크기는 가상 컴퓨터의 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="f4d71-124">자세한 내용은 [Windows 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4d71-124">For more information, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>

<span data-ttu-id="f4d71-125">Azure에서 임시 디스크를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 가상 컴퓨터에서의 임시 드라이브 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="f4d71-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="f4d71-126">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="f4d71-126">Data disk</span></span>
<span data-ttu-id="f4d71-127">데이터 디스크는 응용 프로그램 데이터 또는 사용자가 보존해야 하는 기타 데이터를 저장하기 위해 가상 컴퓨터에 연결된 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="f4d71-128">데이터 디스크는 SCSI 드라이브로 등록되며 사용자가 선택한 문자로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="f4d71-129">각 데이터 디스크의 최대 용량은 4095GB입니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="f4d71-130">가상 컴퓨터의 크기에 따라 사용자가 해당 가상 컴퓨터에 연결할 수 있는 데이터의 디스크의 용량과 디스크를 호스트하기 위해 사용할 수 있는 저장소 유형이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="f4d71-131">가상 컴퓨터 용량에 대한 자세한 내용은 [Windows 가상 컴퓨터에 대한 크기](../virtual-machines/windows/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4d71-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](../virtual-machines/windows/sizes.md).</span></span>
> 

<span data-ttu-id="f4d71-132">Azure는 사용자가 이미지에서 가상 컴퓨터를 만들 때 운영 체제 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="f4d71-133">사용자가 데이터 디스크를 포함하는 이미지를 사용하는 경우, Azure는 가상 컴퓨터를 만들 때, 데이터 디스크도 함께 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="f4d71-134">그렇지 않은 경우, 가상 컴퓨터를 만든 후에 데이터 디스크를 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4d71-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="f4d71-135">사용자는 언제든지 가상 컴퓨터에 디스크를 **연결** 하여 해당 가상 컴퓨터에 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="f4d71-136">사용자는 자신의 저장소 계정 또는 Azure가 사용자 본인을 위해 만든 계정에 업로드하거나 복사한 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="f4d71-137">데이터 디스크를 추가하면 VHD 파일과 VM이 연결되며, 해당 VHD에서 "임대"를 설정하여 해당 VHD가 연결되어 있는 동안 저장소에서 파일이 삭제되지 않게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="f4d71-138">권장: 관리되지 않은 표준 디스크와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="f4d71-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="f4d71-139">관리되지 않는 표준 디스크(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="f4d71-140">TRIM은 디스크에서 사용되지 않는 블록을 삭제하므로 실제로 사용 중인 저장소에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="f4d71-141">큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="f4d71-142">TRIM 설정을 확인하도록 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="f4d71-143">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="f4d71-144">명령이 0을 반환하는 경우 TRIM이 올바르게 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="f4d71-145">1을 반환하는 경우, 다음 명령을 실행하여 TRIM을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="f4d71-146">참고: Trim은 Windows Server 2012/Windows 8 이상부터 지원됩니다. [새로운 API를 통해 앱에서 저장소 미디어에 "TRIM 및 매핑 해제" 힌트를 보내도록 허용](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4d71-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="f4d71-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4d71-147">Next steps</span></span>
* <span data-ttu-id="f4d71-148">[디스크를 연결](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 하여 VM에 다른 저장소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-148">[Attach a disk](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="f4d71-149">[Windows 임시 디스크의 드라이브 문자 변경](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4d71-149">[Change the drive letter of the Windows temporary disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

