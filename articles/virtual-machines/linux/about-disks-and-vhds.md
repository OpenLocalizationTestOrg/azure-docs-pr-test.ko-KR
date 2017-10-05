---
title: "Microsoft Azure Linux VM에 대한 디스크 및 VHD 정보 | Microsoft Docs"
description: "Azure의 Linux 가상 컴퓨터용 디스크 및 VHD의 기본 사항에 대해 알아봅니다."
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
ms.openlocfilehash: be5f09af275142590ec6ade02562e914d5726e08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a><span data-ttu-id="4daea-103">Azure Linux VM용 디스크 및 VHD 정보</span><span class="sxs-lookup"><span data-stu-id="4daea-103">About disks and VHDs for Azure Linux VMs</span></span>
<span data-ttu-id="4daea-104">다른 컴퓨터와 마찬가지로, Azure에서 가상 컴퓨터는 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="4daea-105">모든 Azure 가상 컴퓨터는 적어도 2개의 디스크(Linux 운영 체제 디스크 및 임시 디스크)를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-105">All Azure virtual machines have at least two disks – a Linux operating system disk and a temporary disk.</span></span> <span data-ttu-id="4daea-106">운영 체제 디스크는 이미지에서 만들어지며, 운영 체제 디스크 및 이미지 모두는 실제로 Azure 저장소 계정에 저장된 가상 하드 디스크(VHD)입니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-106">The operating system disk is created from an image, and both the operating system disk and the image are actually virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="4daea-107">가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="4daea-108">이 문서에서는 디스크의 여러 가지 사용법에 대해 설명한 후 사용자가 만들고 사용할 수 있는 다양한 디스크 형식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="4daea-109">이 문서는 [Windows 가상 컴퓨터](../windows/about-disks-and-vhds.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-109">This article is also available for [Windows virtual machines](../windows/about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="4daea-110">VM에서 사용되는 디스크</span><span class="sxs-lookup"><span data-stu-id="4daea-110">Disks used by VMs</span></span>

<span data-ttu-id="4daea-111">VM에서 디스크를 사용하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-111">Let's take a look at how the disks are used by the VMs.</span></span>

## <a name="operating-system-disk"></a><span data-ttu-id="4daea-112">운영 체제 디스크</span><span class="sxs-lookup"><span data-stu-id="4daea-112">Operating system disk</span></span>
<span data-ttu-id="4daea-113">모든 가상 컴퓨터는 하나의 연결된 운영 체제 디스크를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="4daea-114">이 디스크는 SATA 드라이브로 등록되며 기본적으로 /dev/sda라는 레이블이 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-114">It's registered as a SATA drive and is labeled /dev/sda by default.</span></span> <span data-ttu-id="4daea-115">이 디스크의 최대 용량은 2048기가바이트(GB)입니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

## <a name="temporary-disk"></a><span data-ttu-id="4daea-116">임시 디스크</span><span class="sxs-lookup"><span data-stu-id="4daea-116">Temporary disk</span></span>
<span data-ttu-id="4daea-117">각 VM에는 임시 디스크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="4daea-118">이러한 임시 디스크는 응용 프로그램 및 프로세스에 대한 단기 저장소를 제공하며 페이지 또는 스왑 파일과 같은 데이터 저장에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="4daea-119">임시 디스크의 데이터는 [유지 관리 이벤트](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) 또는 [VM을 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)할 때 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-119">Data on the temporary disk may be lost during a [maintenance event](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4daea-120">VM의 표준 다시 부팅 동안 임시 드라이브의 데이터가 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="4daea-121">Linux 가상 컴퓨터에서 디스크는 일반적으로 **/dev/sdb**이며, Azure Linux 에이전트에 의해 **/mnt**로 포맷되고 마운트됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-121">On Linux virtual machines, the disk is typically **/dev/sdb** and is formatted and mounted to **/mnt** by the Azure Linux Agent.</span></span> <span data-ttu-id="4daea-122">임시 디스크의 크기는 가상 컴퓨터의 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-122">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="4daea-123">자세한 내용은 [Linux 가상 컴퓨터의 크기](../windows/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4daea-123">For more information, see [Sizes for Linux virtual machines](../windows/sizes.md).</span></span>

<span data-ttu-id="4daea-124">Azure에서 임시 디스크를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 가상 컴퓨터에서의 임시 드라이브 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="4daea-124">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="data-disk"></a><span data-ttu-id="4daea-125">데이터 디스크 </span><span class="sxs-lookup"><span data-stu-id="4daea-125">Data disk</span></span>
<span data-ttu-id="4daea-126">데이터 디스크는 응용 프로그램 데이터 또는 사용자가 보존해야 하는 기타 데이터를 저장하기 위해 가상 컴퓨터에 연결된 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-126">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="4daea-127">데이터 디스크는 SCSI 드라이브로 등록되며 사용자가 선택한 문자로 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-127">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="4daea-128">각 데이터 디스크의 최대 용량은 4095GB입니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-128">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="4daea-129">가상 컴퓨터의 크기에 따라 사용자가 해당 가상 컴퓨터에 연결할 수 있는 데이터의 디스크의 용량과 디스크를 호스트하기 위해 사용할 수 있는 저장소 유형이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-129">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="4daea-130">가상 컴퓨터 용량에 대한 자세한 내용은 [Linux 가상 컴퓨터에 대한 크기](../windows/sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4daea-130">For more details about virtual machines capacities, see [Sizes for Linux virtual machines](../windows/sizes.md).</span></span>
> 

<span data-ttu-id="4daea-131">Azure는 사용자가 이미지에서 가상 컴퓨터를 만들 때 운영 체제 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-131">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="4daea-132">사용자가 데이터 디스크를 포함하는 이미지를 사용하는 경우, Azure는 가상 컴퓨터를 만들 때, 데이터 디스크도 함께 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-132">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="4daea-133">그렇지 않은 경우, 가상 컴퓨터를 만든 후에 데이터 디스크를 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="4daea-133">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="4daea-134">사용자는 언제든지 가상 컴퓨터에 디스크를 **연결** 하여 해당 가상 컴퓨터에 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-134">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="4daea-135">사용자는 자신의 저장소 계정 또는 Azure가 사용자 본인을 위해 만든 계정에 업로드하거나 복사한 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-135">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="4daea-136">데이터 디스크를 추가하면 VHD 파일과 VM이 연결되며, 해당 VHD에서 "임대"를 설정하여 해당 VHD가 연결되어 있는 동안 저장소에서 파일이 삭제되지 않게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-136">Attaching a data disk associates the VHD file with the VM, by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a><span data-ttu-id="4daea-137">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4daea-137">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="4daea-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4daea-138">Next steps</span></span>
* <span data-ttu-id="4daea-139">[디스크를 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 하여 VM에 다른 저장소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-139">[Attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="4daea-140">중복성에 대해 [소프트웨어 RAID를 구성](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-140">[Configure software RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for redundancy.</span></span>
* <span data-ttu-id="4daea-141">[Linux 가상 컴퓨터를 캡처](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)하여 추가 VM을 신속하게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4daea-141">[Capture a Linux virtual machine](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) so you can quickly deploy additional VMs.</span></span>

