---
title: "Azure의 Linux VM에 대한 질문과 대답 | Microsoft Docs"
description: "리소스 관리자 모델을 사용하여 만든 Linux 가상 컴퓨터에 대해 가장 일반적인 질문 중 일부에 대한 답변을 제공합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0e06d21bd0b6ef807f38e41dcd50c9cd715607a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="7f17b-103">Linux 가상 컴퓨터에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="7f17b-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="7f17b-104">이 문서에서는 Azure에서 Resource Manager 배포 모델을 사용하여 만든 Linux 가상 컴퓨터에 대한 일반적인 질문을 일부 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="7f17b-105">이 항목의 Windows 버전에 대해서는 [Windows 가상 컴퓨터에 대한 질문과 대답](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="7f17b-106">Azure VM에서 무엇을 실행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7f17b-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="7f17b-107">모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="7f17b-108">자세한 내용은 [Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="7f17b-109">가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7f17b-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="7f17b-110">각 데이터 디스크의 최대 용량은 1 TB 입니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="7f17b-111">사용할 수 있는 데이터 디스크의 수는 가상 컴퓨터의 크기에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="7f17b-112">자세한 내용은 [Virtual Machines의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7f17b-113">Azure 저장소 계정은 운영 체제 디스크 및 모든 데이터 디스크에 대한 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="7f17b-114">각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="7f17b-115">가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="7f17b-116">나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7f17b-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="7f17b-117">Virtual Machine에 로그온하려면 SSH(보안 셸)를 사용하여 원격 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="7f17b-118">[Windows에서](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [Linux 및 Mac에서](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 연결하는 방법은 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7f17b-119">기본적으로, SSH는 최대 10개의 동시 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="7f17b-120">구성 파일을 편집하여 이 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="7f17b-121">문제가 있는 경우 [SSH(Secure Shell) 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="7f17b-122">임시 디스크(/dev/sdb1)를 데이터 저장에 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="7f17b-123">임시 디스크(/dev/sdb1)를 데이터 저장에 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="7f17b-124">임시 디스크는 임시 저장소로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-124">It is only there for temporary storage.</span></span> <span data-ttu-id="7f17b-125">복구할 수 없는 데이터는 손실될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="7f17b-126">기존 Azure VM을 복사 또는 복제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="7f17b-127">예.</span><span class="sxs-lookup"><span data-stu-id="7f17b-127">Yes.</span></span> <span data-ttu-id="7f17b-128">자세한 내용은 [Resource Manager 배포 모델에서 Linux 가상 컴퓨터의 복사본을 만드는 방법](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="7f17b-129">Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="7f17b-130">캐나다 중부 및 캐나다 동부의 새로운 두 지역은 기존의 Azure 구독에 대한 가상 컴퓨터 만들기에 자동으로 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="7f17b-131">가상 컴퓨터가 Azure 포털을 통해 Azure Resource Manager를 사용하는 다른 지역에 배포될 때 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="7f17b-132">가상 컴퓨터가 다른 Azure 지역에 배포된 후 새로운 지역은 다음 가상 컴퓨터에 대해 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="7f17b-133">VM을 만든 후에 NIC를 추가할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="7f17b-134">예, 이제 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-134">Yes, this is now possible.</span></span> <span data-ttu-id="7f17b-135">먼저 VM에 대한 할당 취소를 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="7f17b-136">그런 다음 NIC를 추가하거나 제거할 수 있습니다(VM에 있는 마지막 NIC가 아닌 경우).</span><span class="sxs-lookup"><span data-stu-id="7f17b-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="7f17b-137">컴퓨터 이름 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="7f17b-138">예.</span><span class="sxs-lookup"><span data-stu-id="7f17b-138">Yes.</span></span> <span data-ttu-id="7f17b-139">컴퓨터 이름은 64자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="7f17b-140">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="7f17b-141">리소스 그룹 이름에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="7f17b-142">예.</span><span class="sxs-lookup"><span data-stu-id="7f17b-142">Yes.</span></span> <span data-ttu-id="7f17b-143">리소스 그룹 이름은 90자까지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-143">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="7f17b-144">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7f17b-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="7f17b-145">VM을 만들 때의 사용자 이름 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-145">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="7f17b-146">사용자 이름은 1~64자 사이로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="7f17b-147">다음 사용자 이름은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-147">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-148">administrator</span><span class="sxs-lookup"><span data-stu-id="7f17b-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-149">관리자</span><span class="sxs-lookup"><span data-stu-id="7f17b-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-150">사용자</span><span class="sxs-lookup"><span data-stu-id="7f17b-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-151">user1</span><span class="sxs-lookup"><span data-stu-id="7f17b-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-152">test</span><span class="sxs-lookup"><span data-stu-id="7f17b-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-153">user2</span><span class="sxs-lookup"><span data-stu-id="7f17b-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-154">test1</span><span class="sxs-lookup"><span data-stu-id="7f17b-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-155">user3</span><span class="sxs-lookup"><span data-stu-id="7f17b-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-156">admin1</span><span class="sxs-lookup"><span data-stu-id="7f17b-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-157">1</span><span class="sxs-lookup"><span data-stu-id="7f17b-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-158">123</span><span class="sxs-lookup"><span data-stu-id="7f17b-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-159">a</span><span class="sxs-lookup"><span data-stu-id="7f17b-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-160">actuser</span><span class="sxs-lookup"><span data-stu-id="7f17b-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="7f17b-161">adm</span><span class="sxs-lookup"><span data-stu-id="7f17b-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-162">admin2</span><span class="sxs-lookup"><span data-stu-id="7f17b-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="7f17b-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-164">backup</span><span class="sxs-lookup"><span data-stu-id="7f17b-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-165">console</span><span class="sxs-lookup"><span data-stu-id="7f17b-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-166">david</span><span class="sxs-lookup"><span data-stu-id="7f17b-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-167">guest</span><span class="sxs-lookup"><span data-stu-id="7f17b-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-168">john</span><span class="sxs-lookup"><span data-stu-id="7f17b-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-169">owner</span><span class="sxs-lookup"><span data-stu-id="7f17b-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-170">root</span><span class="sxs-lookup"><span data-stu-id="7f17b-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-171">server</span><span class="sxs-lookup"><span data-stu-id="7f17b-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-172">sql</span><span class="sxs-lookup"><span data-stu-id="7f17b-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-173">support</span><span class="sxs-lookup"><span data-stu-id="7f17b-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="7f17b-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-175">sys</span><span class="sxs-lookup"><span data-stu-id="7f17b-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="7f17b-176">test2</span><span class="sxs-lookup"><span data-stu-id="7f17b-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-177">test3</span><span class="sxs-lookup"><span data-stu-id="7f17b-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-178">user4</span><span class="sxs-lookup"><span data-stu-id="7f17b-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="7f17b-179">user5</span><span class="sxs-lookup"><span data-stu-id="7f17b-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="7f17b-180">VM을 만들 때의 암호 요구 사항은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="7f17b-180">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="7f17b-181">암호는 6~72자 사이로 지정해야 하며 다음의 4가지 복잡성 요구 사항 중 3가지를 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f17b-181">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="7f17b-182">소문자 포함</span><span class="sxs-lookup"><span data-stu-id="7f17b-182">Have lower characters</span></span>
* <span data-ttu-id="7f17b-183">대문자 포함</span><span class="sxs-lookup"><span data-stu-id="7f17b-183">Have upper characters</span></span>
* <span data-ttu-id="7f17b-184">숫자 포함</span><span class="sxs-lookup"><span data-stu-id="7f17b-184">Have a digit</span></span>
* <span data-ttu-id="7f17b-185">특수 문자 포함(정규식 일치 [\W_])</span><span class="sxs-lookup"><span data-stu-id="7f17b-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="7f17b-186">사용할 수 없는 암호:</span><span class="sxs-lookup"><span data-stu-id="7f17b-186">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="7f17b-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="7f17b-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="7f17b-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="7f17b-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="7f17b-189">Password!</span><span class="sxs-lookup"><span data-stu-id="7f17b-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="7f17b-190">Password1</span><span class="sxs-lookup"><span data-stu-id="7f17b-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="7f17b-191">Password22</span><span class="sxs-lookup"><span data-stu-id="7f17b-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="7f17b-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="7f17b-192">iloveyou!</span></span></td>
    </tr>
</table>
