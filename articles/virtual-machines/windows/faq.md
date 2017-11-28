---
title: "Azure의 Windows VM에 대한 FAQ | Microsoft Docs"
description: "리소스 관리자 모델을 사용하여 만든 Windows 가상 컴퓨터에 대해 가장 일반적인 질문 중 일부에 대한 답변을 제공합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: 64354c0064d3602c5d214d687cbc6bf73415f831
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a><span data-ttu-id="8d7f0-103">Windows 가상 컴퓨터에 대한 자주 묻는 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8d7f0-103">Frequently asked question about Windows Virtual Machines</span></span>
<span data-ttu-id="8d7f0-104">이 문서에서는 Azure에서 리소스 관리자 배포 모델을 사용하여 만든 Windows 가상 컴퓨터에 대한 일부 일반적인 질문을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-104">This article addresses some common questions about Windows virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="8d7f0-105">이 항목의 Linux 버전에 대해서는 [Linux 가상 컴퓨터에 대한 자주 묻는 질문과 대답](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8d7f0-105">For the Linux version of this topic, see [Frequently asked question about Linux Virtual Machines](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="8d7f0-106">Azure VM에서 무엇을 실행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="8d7f0-107">모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="8d7f0-108">Azure에서 Microsoft 서버 소프트웨어 실행을 위한 지원 정책에 대한 자세한 내용은 [Azure 가상 컴퓨터에 대한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="8d7f0-108">For information about the support policy for running Microsoft server software in Azure, see [Microsoft server software support for Azure Virtual Machines](https://support.microsoft.com/kb/2721672)</span></span>

<span data-ttu-id="8d7f0-109">Windows 7, Windows 8.1 및 Windows 10의 특정 버전은 MSDN Azure 혜택 구독자와 MSDN 개발 및 테스트 종량제 구독자가 개발 및 테스트 작업을 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-109">Certain versions of Windows 7, Windows 8.1, and Windows 10 are available to MSDN Azure benefit subscribers and MSDN Dev and Test Pay-As-You-Go subscribers, for development and test tasks.</span></span> <span data-ttu-id="8d7f0-110">지침과 제한 사항을 포함한 자세한 내용은 [MSDN 구독자를 위한 Windows 클라이언트 이미지](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-110">For details, including instructions and limitations, see [Windows Client images for MSDN subscribers](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).</span></span> 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="8d7f0-111">가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-111">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="8d7f0-112">각 데이터 디스크의 최대 용량은 1 TB 입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-112">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="8d7f0-113">사용할 수 있는 데이터 디스크의 수는 가상 컴퓨터의 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-113">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="8d7f0-114">자세한 내용은 [가상 컴퓨터의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-114">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="8d7f0-115">Azure Managed Disks는 데이터 영구 저장을 위해 Azure Virtual Machines와 함께 사용할 수 있는 새로운 디스크 저장소 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-115">Azure Managed Disks are the new and recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data.</span></span> <span data-ttu-id="8d7f0-116">각 가상 컴퓨터와 함께 여러 Managed Disks를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-116">You can use multiple Managed Disks with each Virtual Machine.</span></span> <span data-ttu-id="8d7f0-117">Managed Disks는 프리미엄 Managed Disks와 표준 Managed Disks 등 내구성이 뛰어난 두 가지 저장소 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-117">Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.</span></span> <span data-ttu-id="8d7f0-118">가격 책정 정보는 [Managed Disks 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-118">For pricing information, see [Managed Disks Pricing](https://azure.microsoft.com/pricing/details/managed-disks).</span></span>

<span data-ttu-id="8d7f0-119">Azure Stroage 계정은 운영 체제 디스크 및 모든 데이터 디스크에 대한 저장소도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-119">Azure storage accounts can also provide storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="8d7f0-120">각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-120">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="8d7f0-121">가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-121">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="8d7f0-122">나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-122">How can I access my virtual machine?</span></span>
<span data-ttu-id="8d7f0-123">RDP(원격 데스크톱 연결)를 사용하여 Windows VM에 대한 원격 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-123">Establish a remote connection using Remote Desktop Connection (RDP) for a Windows VM.</span></span> <span data-ttu-id="8d7f0-124">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-124">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8d7f0-125">서버가 원격 데스크톱 서비스 세션 호스트로 구성되지 않으면 최대 2개의 동시 연결이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-125">A maximum of two concurrent connections are supported, unless the server is configured as a Remote Desktop Services session host.</span></span>  

<span data-ttu-id="8d7f0-126">원격 데스크톱에 문제가 있는 경우 [Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-126">If you’re having problems with Remote Desktop, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="8d7f0-127">Hyper-V에 친숙한 경우 VMConnect와 유사한 도구를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-127">If you’re familiar with Hyper-V, you might be looking for a tool similar to VMConnect.</span></span> <span data-ttu-id="8d7f0-128">가상 컴퓨터에 대한 콘솔 액세스가 지원되지 않으므로 Azure는 유사한 도구를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-128">Azure doesn’t offer a similar tool because console access to a virtual machine isn’t supported.</span></span>

## <a name="can-i-use-the-temporary-disk-the-d-drive-by-default-to-store-data"></a><span data-ttu-id="8d7f0-129">임시 디스크(기본적으로 D: 드라이브)를 사용하여 데이터를 저장할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-129">Can I use the temporary disk (the D: drive by default) to store data?</span></span>
<span data-ttu-id="8d7f0-130">데이터를 저장하는 데 임시 디스크를 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-130">Don’t use the temporary disk to store data.</span></span> <span data-ttu-id="8d7f0-131">해당 드라이브는 임시 저장소일 뿐이므로 복구할 수 없는 데이터가 손실될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-131">It is only temporary storage, so you would risk losing data that can’t be recovered.</span></span> <span data-ttu-id="8d7f0-132">Virtual Machine가 다른 호스트로 이동하면 데이터가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-132">Data loss can occur when the virtual machine moves to a different host.</span></span> <span data-ttu-id="8d7f0-133">가상 컴퓨터 크기를 조정하고, 호스트를 업데이트 하거나, 호스트의 하드웨어가 실패하는 경우가, 가상 컴퓨터가 이동할 수 있는 몇 가지 이유가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-133">Resizing a virtual machine, updating the host, or a hardware failure on the host are some of the reasons a virtual machine might move.</span></span>

<span data-ttu-id="8d7f0-134">D: 드라이브 문자를 사용해야 하는 응용 프로그램이 있는 경우 드라이브 문자를 재할당하여 임시 디스크가 D: 외의 다른 드라이브 문자를 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-134">If you have an application that needs to use the D: drive letter, you can reassign drive letters so that the temporary disk uses something other than D:.</span></span> <span data-ttu-id="8d7f0-135">지침에 대한 자세한 내용은 [Windows 임시 디스크의 드라이브 문자 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-135">For instructions, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>


## <a name="how-can-i-change-the-drive-letter-of-the-temporary-disk"></a><span data-ttu-id="8d7f0-136">임시 디스크의 드라이브 문자 변경을 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-136">How can I change the drive letter of the temporary disk?</span></span>
<span data-ttu-id="8d7f0-137">페이지 파일을 이동하고 드라이브 문자를 다시 할당하여 드라이브 문자를 변경할 수는 있지만, 이렇게 하려면 관련 단계를 특정 순서에 따라 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-137">You can change the drive letter by moving the page file and reassigning drive letters, but you need to make sure you do the steps in a specific order.</span></span> <span data-ttu-id="8d7f0-138">지침에 대한 자세한 내용은 [Windows 임시 디스크의 드라이브 문자 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-138">For instructions, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="can-i-add-an-existing-vm-to-an-availability-set"></a><span data-ttu-id="8d7f0-139">가용성 집합에 기존 VM을 추가할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-139">Can I add an existing VM to an availability set?</span></span>
<span data-ttu-id="8d7f0-140">아니요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-140">No.</span></span> <span data-ttu-id="8d7f0-141">VM이 가용성 집합에 속하려면 집합 내에서 VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-141">If you want your VM to be part of an availability set, you need to create the VM within the set.</span></span> <span data-ttu-id="8d7f0-142">현재는 VM을 만든 이후에 가용성 집합에 추가하는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-142">There currently isn't a way to add a VM to an availability set after it has been created.</span></span>

## <a name="can-i-upload-a-virtual-machine-to-azure"></a><span data-ttu-id="8d7f0-143">가상 컴퓨터를 Azure에 업로드할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-143">Can I upload a virtual machine to Azure?</span></span>
<span data-ttu-id="8d7f0-144">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-144">Yes.</span></span> <span data-ttu-id="8d7f0-145">자세한 내용은 [온-프레미스 VM을 Azure로 마이그레이션](on-prem-to-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-145">For instructions, see [Migrating on-premises VMs to Azure](on-prem-to-azure.md).</span></span>

## <a name="can-i-resize-the-os-disk"></a><span data-ttu-id="8d7f0-146">OS 디스크의 크기를 조정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-146">Can I resize the OS disk?</span></span>
<span data-ttu-id="8d7f0-147">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-147">Yes.</span></span> <span data-ttu-id="8d7f0-148">자세한 내용은 [Azure 리소스 그룹에서 가상 컴퓨터의 OS 드라이브를 확장하는 방법](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-148">For instructions, see [How to expand the OS drive of a Virtual Machine in an Azure Resource Group](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="8d7f0-149">기존 Azure VM을 복사 또는 복제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-149">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="8d7f0-150">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-150">Yes.</span></span> <span data-ttu-id="8d7f0-151">관리되는 이미지를 사용하여 가상 컴퓨터의 이미지를 만든 후 이 이미지를 사용하여 여러 VM을 새로 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-151">Using managed images, you can create an image of a virtual machine and then use the image to build multiple new VMs.</span></span> <span data-ttu-id="8d7f0-152">자세한 내용은 [VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-152">For instructions, see [Create a custom image of a VM](tutorial-custom-images.md).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="8d7f0-153">Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-153">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>

<span data-ttu-id="8d7f0-154">캐나다 중부 및 캐나다 동부의 새로운 두 지역은 기존의 Azure 구독에 대한 가상 컴퓨터 만들기에 자동으로 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-154">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="8d7f0-155">가상 컴퓨터가 Azure 포털을 통해 Azure Resource Manager를 사용하는 다른 지역에 배포될 때 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-155">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="8d7f0-156">가상 컴퓨터가 다른 Azure 지역에 배포된 후 새로운 지역은 다음 가상 컴퓨터에 대해 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-156">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="does-azure-support-linux-vms"></a><span data-ttu-id="8d7f0-157">Azure에서 Linux VM을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-157">Does Azure support Linux VMs?</span></span>
<span data-ttu-id="8d7f0-158">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-158">Yes.</span></span> <span data-ttu-id="8d7f0-159">사용해 보기 위해 Linux VM을 신속하게 만들려면 [포털을 사용하여 Azure에서 Linux VM 만들기](../linux/quick-create-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-159">To quickly create a Linux VM to try out, see [Create a Linux VM on Azure using the Portal](../linux/quick-create-portal.md).</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="8d7f0-160">VM을 만든 후에 NIC를 추가할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-160">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="8d7f0-161">예, 이제 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-161">Yes, this is now possible.</span></span> <span data-ttu-id="8d7f0-162">먼저 VM에 대한 할당 취소를 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-162">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="8d7f0-163">그런 다음 NIC를 추가하거나 제거할 수 있습니다(VM에 있는 마지막 NIC가 아닌 경우).</span><span class="sxs-lookup"><span data-stu-id="8d7f0-163">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="8d7f0-164">컴퓨터 이름 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-164">Are there any computer name requirements?</span></span>
<span data-ttu-id="8d7f0-165">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-165">Yes.</span></span> <span data-ttu-id="8d7f0-166">컴퓨터 이름은 15자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-166">The computer name can be a maximum of 15 characters in length.</span></span> <span data-ttu-id="8d7f0-167">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-167">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="8d7f0-168">리소스 그룹 이름에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-168">Are there any resource group name requirements?</span></span>
<span data-ttu-id="8d7f0-169">예.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-169">Yes.</span></span> <span data-ttu-id="8d7f0-170">리소스 그룹 이름은 90자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-170">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="8d7f0-171">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-171">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="8d7f0-172">VM을 만들 때의 사용자 이름 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-172">What are the username requirements when creating a VM?</span></span>

<span data-ttu-id="8d7f0-173">사용자 이름은 20자까지 지정할 수 있으며 마침표(".")로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-173">Usernames can be a maximum of 20 characters in length and cannot end in a period (".").</span></span> 


<span data-ttu-id="8d7f0-174">다음 사용자 이름은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-174">The following usernames are not allowed:</span></span>
<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-175">administrator</span><span class="sxs-lookup"><span data-stu-id="8d7f0-175">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-176">관리자</span><span class="sxs-lookup"><span data-stu-id="8d7f0-176">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-177">사용자</span><span class="sxs-lookup"><span data-stu-id="8d7f0-177">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-178">user1</span><span class="sxs-lookup"><span data-stu-id="8d7f0-178">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-179">test</span><span class="sxs-lookup"><span data-stu-id="8d7f0-179">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-180">user2</span><span class="sxs-lookup"><span data-stu-id="8d7f0-180">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-181">test1</span><span class="sxs-lookup"><span data-stu-id="8d7f0-181">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-182">user3</span><span class="sxs-lookup"><span data-stu-id="8d7f0-182">user3</span></span></td>
    </tr>    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-183">admin1</span><span class="sxs-lookup"><span data-stu-id="8d7f0-183">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-184">1</span><span class="sxs-lookup"><span data-stu-id="8d7f0-184">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-185">123</span><span class="sxs-lookup"><span data-stu-id="8d7f0-185">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-186">a</span><span class="sxs-lookup"><span data-stu-id="8d7f0-186">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-187">actuser</span><span class="sxs-lookup"><span data-stu-id="8d7f0-187">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="8d7f0-188">adm</span><span class="sxs-lookup"><span data-stu-id="8d7f0-188">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-189">admin2</span><span class="sxs-lookup"><span data-stu-id="8d7f0-189">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-190">aspnet</span><span class="sxs-lookup"><span data-stu-id="8d7f0-190">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-191">backup</span><span class="sxs-lookup"><span data-stu-id="8d7f0-191">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-192">console</span><span class="sxs-lookup"><span data-stu-id="8d7f0-192">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-193">david</span><span class="sxs-lookup"><span data-stu-id="8d7f0-193">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-194">guest</span><span class="sxs-lookup"><span data-stu-id="8d7f0-194">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-195">john</span><span class="sxs-lookup"><span data-stu-id="8d7f0-195">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-196">owner</span><span class="sxs-lookup"><span data-stu-id="8d7f0-196">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-197">root</span><span class="sxs-lookup"><span data-stu-id="8d7f0-197">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-198">server</span><span class="sxs-lookup"><span data-stu-id="8d7f0-198">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-199">sql</span><span class="sxs-lookup"><span data-stu-id="8d7f0-199">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-200">support</span><span class="sxs-lookup"><span data-stu-id="8d7f0-200">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-201">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="8d7f0-201">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-202">sys</span><span class="sxs-lookup"><span data-stu-id="8d7f0-202">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="8d7f0-203">test2</span><span class="sxs-lookup"><span data-stu-id="8d7f0-203">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-204">test3</span><span class="sxs-lookup"><span data-stu-id="8d7f0-204">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-205">user4</span><span class="sxs-lookup"><span data-stu-id="8d7f0-205">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="8d7f0-206">user5</span><span class="sxs-lookup"><span data-stu-id="8d7f0-206">user5</span></span></td>
    </tr>
</table>

## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="8d7f0-207">VM을 만들 때의 암호 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="8d7f0-207">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="8d7f0-208">암호는 12~123자 사이로 지정해야 하며 다음의 4가지 복잡성 요구 사항 중 3가지를 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d7f0-208">Passwords must be 12 - 123 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="8d7f0-209">소문자 포함</span><span class="sxs-lookup"><span data-stu-id="8d7f0-209">Have lower characters</span></span>
* <span data-ttu-id="8d7f0-210">대문자 포함</span><span class="sxs-lookup"><span data-stu-id="8d7f0-210">Have upper characters</span></span>
* <span data-ttu-id="8d7f0-211">숫자 포함</span><span class="sxs-lookup"><span data-stu-id="8d7f0-211">Have a digit</span></span>
* <span data-ttu-id="8d7f0-212">특수 문자 포함(정규식 일치 [\W_])</span><span class="sxs-lookup"><span data-stu-id="8d7f0-212">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="8d7f0-213">사용할 수 없는 암호:</span><span class="sxs-lookup"><span data-stu-id="8d7f0-213">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td>abc@123 </td>
        <td><span data-ttu-id="8d7f0-214">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="8d7f0-214">P@$$w0rd</span></span> </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td><span data-ttu-id="8d7f0-215">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="8d7f0-215">Pa$$word</span></span> </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td><span data-ttu-id="8d7f0-216">Password!</span><span class="sxs-lookup"><span data-stu-id="8d7f0-216">Password!</span></span> </td>
        <td><span data-ttu-id="8d7f0-217">Password1</span><span class="sxs-lookup"><span data-stu-id="8d7f0-217">Password1</span></span> </td>
        <td><span data-ttu-id="8d7f0-218">Password22</span><span class="sxs-lookup"><span data-stu-id="8d7f0-218">Password22</span></span> </td>
        <td><span data-ttu-id="8d7f0-219">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="8d7f0-219">iloveyou!</span></span> </td>
    </tr>
</table>
