---
title: "aaaAbout 디스크 및 Microsoft Azure Linux vm의 Vhd | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터에 대 한 디스크 및 Vhd의 hello 기본 사항에 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a><span data-ttu-id="527e4-103">Azure Linux VM용 디스크 및 VHD 정보</span><span class="sxs-lookup"><span data-stu-id="527e4-103">About disks and VHDs for Azure Linux VMs</span></span>
<span data-ttu-id="527e4-104">다른 컴퓨터와 마찬가지로 Azure의 가상 컴퓨터 위치 toostore 운영 체제 디스크, 응용 프로그램 및 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-104">Just like any other computer, virtual machines in Azure use disks as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="527e4-105">모든 Azure 가상 컴퓨터는 적어도 2개의 디스크(Linux 운영 체제 디스크 및 임시 디스크)를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-105">All Azure virtual machines have at least two disks – a Linux operating system disk and a temporary disk.</span></span> <span data-ttu-id="527e4-106">hello 운영 체제 디스크는 이미지에서 만들어지고 hello 운영 체제 디스크와 hello 이미지가 실제로 가상 하드 디스크 (Vhd)는 Azure 저장소 계정에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-106">hello operating system disk is created from an image, and both hello operating system disk and hello image are actually virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="527e4-107">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="527e4-108">이 문서에서는 hello hello 디스크에 대 한 서로 다른 사용에 설명 하 고 만들고 사용할 수 있는 디스크의 hello 다른 형식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-108">In this article, we will talk about hello different uses for hello disks, and then discuss hello different types of disks you can create and use.</span></span> <span data-ttu-id="527e4-109">이 문서는 [Windows 가상 컴퓨터](storage-about-disks-and-vhds-windows.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-109">This article is also available for [Windows virtual machines](storage-about-disks-and-vhds-windows.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="527e4-110">VM에서 사용되는 디스크</span><span class="sxs-lookup"><span data-stu-id="527e4-110">Disks used by VMs</span></span>

<span data-ttu-id="527e4-111">Hello 디스크 hello Vm에서 어떻게 사용 되는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-111">Let's take a look at how hello disks are used by hello VMs.</span></span>

## <a name="operating-system-disk"></a><span data-ttu-id="527e4-112">운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="527e4-112">Operating system disk</span></span>
<span data-ttu-id="527e4-113">모든 가상 컴퓨터는 하나의 연결된 운영 체제 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="527e4-114">이 디스크는 SATA 드라이브로 등록되며 기본적으로 /dev/sda라는 레이블이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-114">It's registered as a SATA drive and is labeled /dev/sda by default.</span></span> <span data-ttu-id="527e4-115">이 디스크의 최대 용량은 2048기가바이트(GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

## <a name="temporary-disk"></a><span data-ttu-id="527e4-116">임시 디스크</span><span class="sxs-lookup"><span data-stu-id="527e4-116">Temporary disk</span></span>
<span data-ttu-id="527e4-117">각 VM에는 임시 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="527e4-118">hello 임시 디스크 응용 프로그램 및 프로세스에 대 한 단기 저장소를 제공 하며 페이지 또는 스왑 파일과 같은 데이터를 의도 한 tooonly 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-118">hello temporary disk provides short-term storage for applications and processes and is intended tooonly store data such as page or swap files.</span></span> <span data-ttu-id="527e4-119">Hello 임시 디스크에 데이터를 하는 동안 손실 될 수 있습니다는 [유지 관리 이벤트](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) 되거나 있습니다 [VM을 다시 배포](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-119">Data on hello temporary disk may be lost during a [maintenance event](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="527e4-120">Hello VM의 표준 다시 부팅 하는 동안 hello 데이터 hello 임시 드라이브에 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-120">During a standard reboot of hello VM, hello data on hello temporary drive should persist.</span></span>

<span data-ttu-id="527e4-121">Linux 가상 컴퓨터에서 hello 디스크는 일반적으로 **/개발/sdb** 서식이 지정 되 고 너무 탑재**/mnt** hello Azure Linux 에이전트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-121">On Linux virtual machines, hello disk is typically **/dev/sdb** and is formatted and mounted too**/mnt** by hello Azure Linux Agent.</span></span> <span data-ttu-id="527e4-122">hello 임시 디스크의 hello 크기 hello 가상 컴퓨터의 hello 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-122">hello size of hello temporary disk varies, based on hello size of hello virtual machine.</span></span> <span data-ttu-id="527e4-123">자세한 내용은 [Linux 가상 컴퓨터의 크기](../virtual-machines/linux/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="527e4-123">For more information, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>

<span data-ttu-id="527e4-124">Azure hello 임시 디스크를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [hello 임시 드라이브를 Microsoft Azure 가상 컴퓨터 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="527e4-124">For more information on how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="data-disk"></a><span data-ttu-id="527e4-125">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="527e4-125">Data disk</span></span>
<span data-ttu-id="527e4-126">데이터 디스크는 VHD tooa 연결 된 가상 컴퓨터 toostore 응용 프로그램 데이터 또는 기타 필요한 데이터를 tookeep입니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-126">A data disk is a VHD that's attached tooa virtual machine toostore application data, or other data you need tookeep.</span></span> <span data-ttu-id="527e4-127">데이터 디스크는 SCSI 드라이브로 등록되며 사용자가 선택한 문자로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-127">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="527e4-128">각 데이터 디스크의 최대 용량은 4095GB입니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-128">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="527e4-129">hello hello 가상 컴퓨터의 크기를 결정 tooit 및 hello 유형의 저장소를 사용할 수 있습니다에 연결한 데이터 디스크 수 toohost hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="527e4-129">hello size of hello virtual machine determines how many data disks you can attach tooit and hello type of storage you can use toohost hello disks.</span></span>

> [!NOTE]
> <span data-ttu-id="527e4-130">가상 컴퓨터 용량에 대한 자세한 내용은 [Linux 가상 컴퓨터에 대한 크기](../virtual-machines/linux/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="527e4-130">For more details about virtual machines capacities, see [Sizes for Linux virtual machines](../virtual-machines/linux/sizes.md).</span></span>
> 

<span data-ttu-id="527e4-131">Azure는 사용자가 이미지에서 가상 컴퓨터를 만들 때 운영 체제 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-131">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="527e4-132">데이터 디스크를 포함 하는 이미지를 사용 하는 경우 Azure hello 데이터 디스크 때도 만들어집니다 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-132">If you use an image that includes data disks, Azure also creates hello data disks when it creates hello virtual machine.</span></span> <span data-ttu-id="527e4-133">그렇지 않으면 hello 가상 컴퓨터를 만든 후 데이터 디스크 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-133">Otherwise, you add data disks after you create hello virtual machine.</span></span>

<span data-ttu-id="527e4-134">언제 든 지 데이터 디스크 tooa 가상 컴퓨터에서 추가 **연결** hello 디스크 toohello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="527e4-134">You can add data disks tooa virtual machine at any time, by **attaching** hello disk toohello virtual machine.</span></span> <span data-ttu-id="527e4-135">사용자를 위해 만드는 하나는 Azure 또는 업로드 하거나 tooyour 저장소 계정에 복사 된 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-135">You can use a VHD that you've uploaded or copied tooyour storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="527e4-136">데이터 디스크 연결 하는 hello VHD 파일 hello VM에 계속 연결 되어 있는 동안 저장소에서 삭제할 수 없게 '임대' hello VHD에 배치 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-136">Attaching a data disk associates hello VHD file with hello VM, by placing a 'lease' on hello VHD so it can't be deleted from storage while it's still attached.</span></span>

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a><span data-ttu-id="527e4-137">문제 해결</span><span class="sxs-lookup"><span data-stu-id="527e4-137">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="527e4-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="527e4-138">Next steps</span></span>
* <span data-ttu-id="527e4-139">[디스크 연결](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd VM 용 추가 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-139">[Attach a disk](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd additional storage for your VM.</span></span>
* <span data-ttu-id="527e4-140">중복성에 대해 [소프트웨어 RAID를 구성](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-140">[Configure software RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for redundancy.</span></span>
* <span data-ttu-id="527e4-141">[Linux 가상 컴퓨터를 캡처](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)하여 추가 VM을 신속하게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527e4-141">[Capture a Linux virtual machine](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) so you can quickly deploy additional VMs.</span></span>

