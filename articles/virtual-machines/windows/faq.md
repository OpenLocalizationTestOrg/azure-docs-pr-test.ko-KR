---
title: "Azure의 Windows Vm에 대 한 aaaFAQ | Microsoft Docs"
description: "Hello hello 리소스 관리자 모델을 사용 하 여 만든 Windows 가상 컴퓨터에 대 한 일반적인 질문과 대답 toosome를 제공 합니다."
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
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a><span data-ttu-id="dcfe7-103">Windows 가상 컴퓨터에 대한 자주 묻는 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="dcfe7-103">Frequently asked question about Windows Virtual Machines</span></span>
<span data-ttu-id="dcfe7-104">이 문서 hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Windows 가상 컴퓨터에 대 한 몇 가지 일반적인 질문을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-104">This article addresses some common questions about Windows virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="dcfe7-105">이 항목의 hello Linux 버전을 참조 하십시오. [질문 Linux 가상 컴퓨터에 대 한 질문과 대답](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="dcfe7-105">For hello Linux version of this topic, see [Frequently asked question about Linux Virtual Machines](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="dcfe7-106">Azure VM에서 무엇을 실행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="dcfe7-107">모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="dcfe7-108">Azure에서 실행 중인 Microsoft 서버 소프트웨어에 대 한 지원 정책 hello에 대 한 정보를 참조 하십시오. [Azure 가상 컴퓨터에 대 한 Microsoft 서버 소프트웨어 지원](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="dcfe7-108">For information about hello support policy for running Microsoft server software in Azure, see [Microsoft server software support for Azure Virtual Machines](https://support.microsoft.com/kb/2721672)</span></span>

<span data-ttu-id="dcfe7-109">특정 버전의 Windows 7, Windows 8.1 및 Windows 10은 사용할 수 있는 tooMSDN Azure 혜택 구독자 및 개발 및 테스트 작업에 대 한 MSDN 개발 및 테스트 종 량 제 구독자입니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-109">Certain versions of Windows 7, Windows 8.1, and Windows 10 are available tooMSDN Azure benefit subscribers and MSDN Dev and Test Pay-As-You-Go subscribers, for development and test tasks.</span></span> <span data-ttu-id="dcfe7-110">지침과 제한 사항을 포함한 자세한 내용은 [MSDN 구독자를 위한 Windows 클라이언트 이미지](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-110">For details, including instructions and limitations, see [Windows Client images for MSDN subscribers](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).</span></span> 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="dcfe7-111">가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-111">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="dcfe7-112">각 데이터 디스크는 too1 TB를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-112">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="dcfe7-113">데이터 디스크를 사용할 수 있습니다 hello 수 hello hello 가상 컴퓨터 크기에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-113">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="dcfe7-114">자세한 내용은 [Virtual Machines의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-114">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="dcfe7-115">Azure 관리 되는 디스크에는 hello 새롭고 권장 디스크 제공 하는 저장소 사용 하기 위해 Azure 가상 컴퓨터 데이터의 영구 저장소에 대 한 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-115">Azure Managed Disks are hello new and recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data.</span></span> <span data-ttu-id="dcfe7-116">각 가상 컴퓨터와 함께 여러 Managed Disks를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-116">You can use multiple Managed Disks with each Virtual Machine.</span></span> <span data-ttu-id="dcfe7-117">Managed Disks는 프리미엄 Managed Disks와 표준 Managed Disks 등 내구성이 뛰어난 두 가지 저장소 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-117">Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.</span></span> <span data-ttu-id="dcfe7-118">가격 책정 정보는 [Managed Disks 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-118">For pricing information, see [Managed Disks Pricing](https://azure.microsoft.com/pricing/details/managed-disks).</span></span>

<span data-ttu-id="dcfe7-119">Azure 저장소 계정 hello 운영 체제 디스크 및 데이터 디스크에 대 한 저장소를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-119">Azure storage accounts can also provide storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="dcfe7-120">각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-120">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="dcfe7-121">가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-121">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="dcfe7-122">나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-122">How can I access my virtual machine?</span></span>
<span data-ttu-id="dcfe7-123">RDP(원격 데스크톱 연결)를 사용하여 Windows VM에 대한 원격 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-123">Establish a remote connection using Remote Desktop Connection (RDP) for a Windows VM.</span></span> <span data-ttu-id="dcfe7-124">자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-124">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dcfe7-125">원격 데스크톱 서비스 세션 호스트로 hello 서버를 구성 하지 않으면 두 개의 동시 연결이 최대 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-125">A maximum of two concurrent connections are supported, unless hello server is configured as a Remote Desktop Services session host.</span></span>  

<span data-ttu-id="dcfe7-126">원격 데스크톱에 문제가 있는 경우 참조 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-126">If you’re having problems with Remote Desktop, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="dcfe7-127">Hyper-v에 익숙한 경우 도구 비슷한 tooVMConnect에 대 한 보고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-127">If you’re familiar with Hyper-V, you might be looking for a tool similar tooVMConnect.</span></span> <span data-ttu-id="dcfe7-128">Azure 콘솔 액세스 tooa 가상 컴퓨터에서 지원 되지 않으므로 유사한 도구를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-128">Azure doesn’t offer a similar tool because console access tooa virtual machine isn’t supported.</span></span>

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a><span data-ttu-id="dcfe7-129">Hello 임시 디스크 (d: 드라이브 기본적으로 hello) toostore 데이터를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-129">Can I use hello temporary disk (hello D: drive by default) toostore data?</span></span>
<span data-ttu-id="dcfe7-130">Hello 임시 디스크 toostore 데이터를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-130">Don’t use hello temporary disk toostore data.</span></span> <span data-ttu-id="dcfe7-131">해당 드라이브는 임시 저장소일 뿐이므로 복구할 수 없는 데이터가 손실될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-131">It is only temporary storage, so you would risk losing data that can’t be recovered.</span></span> <span data-ttu-id="dcfe7-132">Hello 가상 컴퓨터가 tooa 다른 호스트를 이동 하는 경우 데이터 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-132">Data loss can occur when hello virtual machine moves tooa different host.</span></span> <span data-ttu-id="dcfe7-133">가상 컴퓨터 크기 조정, hello 이유 가상 컴퓨터를 이동할 수 있는 몇 가지는 hello 호스트 또는 hello 호스트에서 하드웨어 오류를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-133">Resizing a virtual machine, updating hello host, or a hardware failure on hello host are some of hello reasons a virtual machine might move.</span></span>

<span data-ttu-id="dcfe7-134">Toouse hello d: 드라이브 문자가 필요 하는 응용 프로그램의 경우에 사용할 수 있도록 hello 임시 디스크 이외의 노드 d: 드라이브 문자를 재할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-134">If you have an application that needs toouse hello D: drive letter, you can reassign drive letters so that hello temporary disk uses something other than D:.</span></span> <span data-ttu-id="dcfe7-135">자세한 내용은 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-135">For instructions, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a><span data-ttu-id="dcfe7-136">Hello 임시 디스크의 hello 드라이브 문자를 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-136">How can I change hello drive letter of hello temporary disk?</span></span>
<span data-ttu-id="dcfe7-137">Hello 페이지 파일을 이동 하 여 hello 드라이브 문자 및 재할당 드라이브 문자를 변경할 수는 있지만 toomake 있는지 단계는 특정 순서로 hello 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-137">You can change hello drive letter by moving hello page file and reassigning drive letters, but you need toomake sure you do hello steps in a specific order.</span></span> <span data-ttu-id="dcfe7-138">자세한 내용은 [변경 hello Windows 임시 디스크의 드라이브 문자를 hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-138">For instructions, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a><span data-ttu-id="dcfe7-139">기존 VM tooan 가용성 집합을 추가할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-139">Can I add an existing VM tooan availability set?</span></span>
<span data-ttu-id="dcfe7-140">아니요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-140">No.</span></span> <span data-ttu-id="dcfe7-141">가용성 집합의 VM toobe 파트를 표시할 경우 hello 집합 내에서 VM toocreate hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-141">If you want your VM toobe part of an availability set, you need toocreate hello VM within hello set.</span></span> <span data-ttu-id="dcfe7-142">현재 방식으로 tooadd 만들어진 후에 설정할 VM tooan 가용성 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-142">There currently isn't a way tooadd a VM tooan availability set after it has been created.</span></span>

## <a name="can-i-upload-a-virtual-machine-tooazure"></a><span data-ttu-id="dcfe7-143">가상 컴퓨터 tooAzure를 업로드할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-143">Can I upload a virtual machine tooAzure?</span></span>
<span data-ttu-id="dcfe7-144">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-144">Yes.</span></span> <span data-ttu-id="dcfe7-145">자세한 내용은 [마이그레이션 온-프레미스 Vm tooAzure](on-prem-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-145">For instructions, see [Migrating on-premises VMs tooAzure](on-prem-to-azure.md).</span></span>

## <a name="can-i-resize-hello-os-disk"></a><span data-ttu-id="dcfe7-146">Hello OS 디스크 크기 조정 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-146">Can I resize hello OS disk?</span></span>
<span data-ttu-id="dcfe7-147">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-147">Yes.</span></span> <span data-ttu-id="dcfe7-148">자세한 내용은 [어떻게 tooexpand hello Azure 리소스 그룹에 가상 컴퓨터의 운영 체제 드라이브](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-148">For instructions, see [How tooexpand hello OS drive of a Virtual Machine in an Azure Resource Group](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="dcfe7-149">기존 Azure VM을 복사 또는 복제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-149">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="dcfe7-150">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-150">Yes.</span></span> <span data-ttu-id="dcfe7-151">관리 되는 이미지를 사용 하 여 하면 가상 컴퓨터의 이미지 만들고 사용 하 여 hello 이미지 toobuild 여러 새 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-151">Using managed images, you can create an image of a virtual machine and then use hello image toobuild multiple new VMs.</span></span> <span data-ttu-id="dcfe7-152">자세한 내용은 [VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-152">For instructions, see [Create a custom image of a VM](tutorial-custom-images.md).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="dcfe7-153">Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-153">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>

<span data-ttu-id="dcfe7-154">캐나다 중앙 및 캐나다 동부 hello 두 개의 새 영역 기존 Azure 구독에 대 한 가상 컴퓨터 만들기에 자동으로 등록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-154">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="dcfe7-155">이 등록을 통해 가상 컴퓨터를 배포할 때 자동으로 수행 되며 hello Azure 포털 tooany Azure 리소스 관리자를 사용 하 여 다른 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-155">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="dcfe7-156">후 가상 컴퓨터는 배포 된 tooany 다른 Azure 지역 hello 새 영역 이후 가상 컴퓨터에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-156">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="does-azure-support-linux-vms"></a><span data-ttu-id="dcfe7-157">Azure에서 Linux VM을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-157">Does Azure support Linux VMs?</span></span>
<span data-ttu-id="dcfe7-158">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-158">Yes.</span></span> <span data-ttu-id="dcfe7-159">tooquickly 만들 참조 아웃 Linux VM tootry [hello 포털을 사용 하 여 Azure에서 Linux VM을 만들](../linux/quick-create-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-159">tooquickly create a Linux VM tootry out, see [Create a Linux VM on Azure using hello Portal](../linux/quick-create-portal.md).</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="dcfe7-160">만든 후 NIC toomy VM 추가 합니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-160">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="dcfe7-161">예, 이제 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-161">Yes, this is now possible.</span></span> <span data-ttu-id="dcfe7-162">hello VM 첫 번째 요구 toobe 중지 할당 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-162">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="dcfe7-163">그런 다음 추가 하거나 NIC를 제거할 수 있습니다 (경우가 아니라면 hello VM에서 마지막 NIC hello).</span><span class="sxs-lookup"><span data-stu-id="dcfe7-163">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="dcfe7-164">컴퓨터 이름 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-164">Are there any computer name requirements?</span></span>
<span data-ttu-id="dcfe7-165">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-165">Yes.</span></span> <span data-ttu-id="dcfe7-166">hello 컴퓨터 이름은 길이가 15 자까지 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-166">hello computer name can be a maximum of 15 characters in length.</span></span> <span data-ttu-id="dcfe7-167">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-167">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="dcfe7-168">리소스 그룹 이름에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-168">Are there any resource group name requirements?</span></span>
<span data-ttu-id="dcfe7-169">예.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-169">Yes.</span></span> <span data-ttu-id="dcfe7-170">hello 리소스 그룹 이름은 최대 90 자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-170">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="dcfe7-171">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-171">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="dcfe7-172">VM을 만들 때 hello username 요구 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-172">What are hello username requirements when creating a VM?</span></span>

<span data-ttu-id="dcfe7-173">사용자 이름은 20자까지 지정할 수 있으며 마침표(".")로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-173">Usernames can be a maximum of 20 characters in length and cannot end in a period (".").</span></span> 


<span data-ttu-id="dcfe7-174">사용자 이름은 다음 hello 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-174">hello following usernames are not allowed:</span></span>
<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-175">관리자 역할</span><span class="sxs-lookup"><span data-stu-id="dcfe7-175">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-176">관리자</span><span class="sxs-lookup"><span data-stu-id="dcfe7-176">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-177">사용자</span><span class="sxs-lookup"><span data-stu-id="dcfe7-177">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-178">user1</span><span class="sxs-lookup"><span data-stu-id="dcfe7-178">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-179">test</span><span class="sxs-lookup"><span data-stu-id="dcfe7-179">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-180">user2</span><span class="sxs-lookup"><span data-stu-id="dcfe7-180">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-181">test1</span><span class="sxs-lookup"><span data-stu-id="dcfe7-181">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-182">user3</span><span class="sxs-lookup"><span data-stu-id="dcfe7-182">user3</span></span></td>
    </tr>    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-183">admin1</span><span class="sxs-lookup"><span data-stu-id="dcfe7-183">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-184">1</span><span class="sxs-lookup"><span data-stu-id="dcfe7-184">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-185">123</span><span class="sxs-lookup"><span data-stu-id="dcfe7-185">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-186">a</span><span class="sxs-lookup"><span data-stu-id="dcfe7-186">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-187">actuser</span><span class="sxs-lookup"><span data-stu-id="dcfe7-187">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="dcfe7-188">adm</span><span class="sxs-lookup"><span data-stu-id="dcfe7-188">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-189">admin2</span><span class="sxs-lookup"><span data-stu-id="dcfe7-189">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-190">aspnet</span><span class="sxs-lookup"><span data-stu-id="dcfe7-190">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-191">backup</span><span class="sxs-lookup"><span data-stu-id="dcfe7-191">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-192">console</span><span class="sxs-lookup"><span data-stu-id="dcfe7-192">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-193">david</span><span class="sxs-lookup"><span data-stu-id="dcfe7-193">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-194">guest</span><span class="sxs-lookup"><span data-stu-id="dcfe7-194">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-195">john</span><span class="sxs-lookup"><span data-stu-id="dcfe7-195">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-196">owner</span><span class="sxs-lookup"><span data-stu-id="dcfe7-196">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-197">root</span><span class="sxs-lookup"><span data-stu-id="dcfe7-197">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-198">server</span><span class="sxs-lookup"><span data-stu-id="dcfe7-198">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-199">sql</span><span class="sxs-lookup"><span data-stu-id="dcfe7-199">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-200">support</span><span class="sxs-lookup"><span data-stu-id="dcfe7-200">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-201">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="dcfe7-201">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-202">sys</span><span class="sxs-lookup"><span data-stu-id="dcfe7-202">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="dcfe7-203">test2</span><span class="sxs-lookup"><span data-stu-id="dcfe7-203">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-204">test3</span><span class="sxs-lookup"><span data-stu-id="dcfe7-204">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-205">user4</span><span class="sxs-lookup"><span data-stu-id="dcfe7-205">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="dcfe7-206">user5</span><span class="sxs-lookup"><span data-stu-id="dcfe7-206">user5</span></span></td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="dcfe7-207">VM을 만들 때 hello 암호 요구 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="dcfe7-207">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="dcfe7-208">암호는 12 123 자가 하 여야 하 고 4 복잡성 요구 사항을 준수 하는 hello 부족 3 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-208">Passwords must be 12 - 123 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="dcfe7-209">소문자 포함</span><span class="sxs-lookup"><span data-stu-id="dcfe7-209">Have lower characters</span></span>
* <span data-ttu-id="dcfe7-210">대문자 포함</span><span class="sxs-lookup"><span data-stu-id="dcfe7-210">Have upper characters</span></span>
* <span data-ttu-id="dcfe7-211">숫자 포함</span><span class="sxs-lookup"><span data-stu-id="dcfe7-211">Have a digit</span></span>
* <span data-ttu-id="dcfe7-212">특수 문자 포함(정규식 일치 [\W_])</span><span class="sxs-lookup"><span data-stu-id="dcfe7-212">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="dcfe7-213">암호를 다음 hello 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dcfe7-213">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td>abc@123 </td>
        <td><span data-ttu-id="dcfe7-214">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="dcfe7-214">P@$$w0rd</span></span> </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td><span data-ttu-id="dcfe7-215">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="dcfe7-215">Pa$$word</span></span> </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td><span data-ttu-id="dcfe7-216">Password!</span><span class="sxs-lookup"><span data-stu-id="dcfe7-216">Password!</span></span> </td>
        <td><span data-ttu-id="dcfe7-217">Password1</span><span class="sxs-lookup"><span data-stu-id="dcfe7-217">Password1</span></span> </td>
        <td><span data-ttu-id="dcfe7-218">Password22</span><span class="sxs-lookup"><span data-stu-id="dcfe7-218">Password22</span></span> </td>
        <td><span data-ttu-id="dcfe7-219">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="dcfe7-219">iloveyou!</span></span> </td>
    </tr>
</table>
