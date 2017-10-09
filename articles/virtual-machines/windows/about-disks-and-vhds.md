---
title: "aaaAbout 디스크 및 Microsoft Azure Windows vm의 Vhd | Microsoft Docs"
description: "디스크와 Azure의 가상 컴퓨터 Vhd에 대 한 Windows hello 기본 사항에 알아봅니다."
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
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="db9e2-103">Azure Windows VM용 디스크 및 VHD 정보</span><span class="sxs-lookup"><span data-stu-id="db9e2-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="db9e2-104">다른 컴퓨터와 마찬가지로 Azure의 가상 컴퓨터 위치 toostore 운영 체제 디스크, 응용 프로그램 및 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="db9e2-105">모든 Azure 가상 컴퓨터는 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="db9e2-106">hello 운영 체제 디스크와 hello 이미지는 Azure 저장소 계정에 저장 된 가상 하드 디스크 (Vhd)와 hello 운영 체제 디스크는 이미지에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="db9e2-107">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="db9e2-108">이 문서에서는 hello hello 디스크에 대 한 서로 다른 사용에 설명 하 고 만들고 사용할 수 있는 디스크의 hello 다른 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="db9e2-109">이 문서는 [Linux 가상 컴퓨터](about-disks-and-vhds.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="db9e2-110">VM에서 사용되는 디스크</span><span class="sxs-lookup"><span data-stu-id="db9e2-110">Disks used by VMs</span></span>

<span data-ttu-id="db9e2-111">Hello 디스크 hello Vm에서 어떻게 사용 되는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="db9e2-112">운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="db9e2-112">Operating system disk</span></span>
<span data-ttu-id="db9e2-113">모든 가상 컴퓨터는 하나의 연결된 운영 체제 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="db9e2-114">SATA 드라이브로 등록 되어 있으며 기본적으로 hello c: 드라이브로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-114">It's registered as a SATA drive and labeled as hello C: drive by default.</span></span> <span data-ttu-id="db9e2-115">이 디스크의 최대 용량은 2048기가바이트(GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="db9e2-116">임시 디스크</span><span class="sxs-lookup"><span data-stu-id="db9e2-116">Temporary disk</span></span>
<span data-ttu-id="db9e2-117">각 VM에는 임시 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="db9e2-118">hello 임시 디스크 응용 프로그램 및 프로세스에 대 한 단기 저장소를 제공 하며 페이지 또는 스왑 파일과 같은 데이터를 의도 한 tooonly 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="db9e2-119">Hello 임시 디스크에 데이터를 하는 동안 손실 될 수 있습니다는 [유지 관리 이벤트](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) 되거나 있습니다 [VM을 다시 배포](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-119">Data on hello temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="db9e2-120">Hello VM의 표준 다시 부팅 하는 동안 hello 데이터 hello 임시 드라이브에 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="db9e2-121">임시 디스크 hello pagefile.sys를 저장 하는 데 사용 하 고 기본적으로 d: 드라이브 hello로 레이블이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-121">hello temporary disk is labeled as hello D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="db9e2-122">tooremap이 디스크 tooa 다른 드라이브 문자 참조 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-122">tooremap this disk tooa different drive letter, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="db9e2-123">hello 임시 디스크의 hello 크기 hello 가상 컴퓨터의 hello 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-123">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="db9e2-124">자세한 내용은 [Windows 가상 컴퓨터 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db9e2-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="db9e2-125">Azure hello 임시 디스크를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [hello 임시 드라이브를 Microsoft Azure 가상 컴퓨터 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="db9e2-125">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="db9e2-126">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="db9e2-126">Data disk</span></span>
<span data-ttu-id="db9e2-127">데이터 디스크는 VHD tooa 연결 된 가상 컴퓨터 toostore 응용 프로그램 데이터 또는 기타 필요한 데이터를 tookeep입니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-127">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="db9e2-128">데이터 디스크는 SCSI 드라이브로 등록되며 사용자가 선택한 문자로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="db9e2-129">각 데이터 디스크의 최대 용량은 4095GB입니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="db9e2-130">hello hello 가상 컴퓨터의 크기를 결정 tooit 및 hello 유형의 저장소를 사용할 수 있습니다에 연결한 데이터 디스크 수 toohost hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="db9e2-130">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="db9e2-131">가상 컴퓨터 용량에 대한 자세한 내용은 [Windows 가상 컴퓨터에 대한 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db9e2-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="db9e2-132">Azure는 사용자가 이미지에서 가상 컴퓨터를 만들 때 운영 체제 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="db9e2-133">데이터 디스크를 포함 하는 이미지를 사용 하는 경우 Azure hello 데이터 디스크 때도 만들어집니다 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-133">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="db9e2-134">그렇지 않으면 hello 가상 컴퓨터를 만든 후 데이터 디스크 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-134">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="db9e2-135">언제 든 지 데이터 디스크 tooa 가상 컴퓨터에서 추가 **연결** hello 디스크 toohello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="db9e2-135">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="db9e2-136">사용자를 위해 만드는 하나는 Azure 또는 업로드 하거나 tooyour 저장소 계정에 복사 된 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-136">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="db9e2-137">데이터 디스크 연결 하는 hello VHD 파일 hello VM ' 임대 ' hello VHD에 아직 연결 되어 있는 동안 저장소에서 삭제할 수 없게 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-137">Attaching a data disk associates hello VHD file with hello VM by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="db9e2-138">권장: 관리되지 않은 표준 디스크와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="db9e2-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="db9e2-139">관리되지 않는 표준 디스크(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="db9e2-140">TRIM 실제로 사용 하는 저장소에 대 한만 청구 됩니다 하므로 hello 디스크에 사용 하지 않는 블록을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-140">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="db9e2-141">큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="db9e2-142">이 명령은 toocheck hello 트림 설정을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-142">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="db9e2-143">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="db9e2-144">Hello 명령이 0을 반환 하는 경우 TRIM 올바르게 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-144">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="db9e2-145">1을 반환 하는 경우 다음 명령을 tooenable TRIM hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-145">If it returns 1, run hello following command tooenable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="db9e2-146">참고: Windows Server 2012부터 트림 지원은 / Windows 8 이상에서 참조 참조 [새 API 앱 toosend "TRIM 및 매핑 해제" 힌트 toostorage 미디어를 통해](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints)합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps toosend "TRIM and Unmap" hints toostorage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="db9e2-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db9e2-147">Next steps</span></span>
* <span data-ttu-id="db9e2-148">[디스크 연결](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd VM 용 추가 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="db9e2-149">[변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 응용 프로그램 데이터에 대 한 hello d: 드라이브를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="db9e2-149">[Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use hello D: drive for data.</span></span>

