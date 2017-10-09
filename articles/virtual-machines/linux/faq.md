---
title: "Azure에서 Linux Vm에 대 한 질문과 aaaFrequently | Microsoft Docs"
description: "Hello hello 리소스 관리자 모델을 사용 하 여 만든 Linux 가상 컴퓨터에 대 한 일반적인 질문과 대답 toosome를 제공 합니다."
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
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="2a5b7-103">Linux 가상 컴퓨터에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="2a5b7-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="2a5b7-104">이 문서 hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Linux 가상 컴퓨터에 대 한 몇 가지 일반적인 질문을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="2a5b7-105">이 항목의 hello Windows 버전을 참조 하십시오. [질문 Windows 가상 컴퓨터에 대 한 질문과 대답](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2a5b7-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="2a5b7-106">Azure VM에서 무엇을 실행할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="2a5b7-107">모든 구독자는 Azure 가상 컴퓨터에서 서버 소프트웨어를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="2a5b7-108">자세한 내용은 [Azure 인증 배포의 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="2a5b7-109">가상 컴퓨터에 얼마나 많은 용량의 저장소를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="2a5b7-110">각 데이터 디스크는 too1 TB를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="2a5b7-111">데이터 디스크를 사용할 수 있습니다 hello 수 hello hello 가상 컴퓨터 크기에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="2a5b7-112">자세한 내용은 [Virtual Machines의 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2a5b7-113">Azure 저장소 계정을 hello 운영 체제 디스크 및 데이터 디스크에 대 한 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="2a5b7-114">각 디스크는 페이지 blob으로 저장된 .vhd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="2a5b7-115">가격 책정에 대한 자세한 내용은 [저장소 가격 세부 정보](https://azure.microsoft.com/pricing/details/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="2a5b7-116">나의 가상 컴퓨터에 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="2a5b7-117">SSH (보안 셸)를 사용 하 여 toohello 가상 컴퓨터 원격 연결 toolog를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="2a5b7-118">방법에 hello 지침을 참조 하십시오. tooconnect [Windows에서](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 또는 [Linux 및 Mac에서](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2a5b7-119">기본적으로, SSH는 최대 10개의 동시 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="2a5b7-120">Hello 구성 파일을 편집 하 여이 번호를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="2a5b7-121">문제가 있는 경우 [SSH(Secure Shell) 연결 문제 해결](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="2a5b7-122">Hello 임시 디스크 (/ 개발/sdb1) toostore 데이터를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="2a5b7-123">Hello 임시 디스크 (/ 개발/sdb1) toostore 데이터를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="2a5b7-124">임시 디스크는 임시 저장소로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-124">It is only there for temporary storage.</span></span> <span data-ttu-id="2a5b7-125">복구할 수 없는 데이터는 손실될 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="2a5b7-126">기존 Azure VM을 복사 또는 복제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="2a5b7-127">예.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-127">Yes.</span></span> <span data-ttu-id="2a5b7-128">자세한 내용은 [toocreate 복사본에서 Linux 가상 컴퓨터의 리소스 관리자 배포 모델을 hello 어떻게](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="2a5b7-129">Azure Resource Manager를 통해 캐나다 중부 및 캐나다 동부 지역이 보이지 않는 이유가 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="2a5b7-130">캐나다 중앙 및 캐나다 동부 hello 두 개의 새 영역 기존 Azure 구독에 대 한 가상 컴퓨터 만들기에 자동으로 등록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="2a5b7-131">이 등록을 통해 가상 컴퓨터를 배포할 때 자동으로 수행 되며 hello Azure 포털 tooany Azure 리소스 관리자를 사용 하 여 다른 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="2a5b7-132">후 가상 컴퓨터는 배포 된 tooany 다른 Azure 지역 hello 새 영역 이후 가상 컴퓨터에 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="2a5b7-133">만든 후 NIC toomy VM 추가 합니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="2a5b7-134">예, 이제 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-134">Yes, this is now possible.</span></span> <span data-ttu-id="2a5b7-135">hello VM 첫 번째 요구 toobe 중지 할당 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="2a5b7-136">그런 다음 추가 하거나 NIC를 제거할 수 있습니다 (경우가 아니라면 hello VM에서 마지막 NIC hello).</span><span class="sxs-lookup"><span data-stu-id="2a5b7-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="2a5b7-137">컴퓨터 이름 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="2a5b7-138">예.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-138">Yes.</span></span> <span data-ttu-id="2a5b7-139">hello 컴퓨터 이름은 최대 64 자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="2a5b7-140">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 이름 지정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="2a5b7-141">리소스 그룹 이름에 대한 요구 사항이 있나요?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="2a5b7-142">예.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-142">Yes.</span></span> <span data-ttu-id="2a5b7-143">hello 리소스 그룹 이름은 최대 90 자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="2a5b7-144">[명명 규칙 및 제한 사항](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하여 리소스 그룹에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="2a5b7-145">VM을 만들 때 hello username 요구 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="2a5b7-146">사용자 이름은 1~64자 사이로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="2a5b7-147">사용자 이름은 다음 hello 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-148">관리자 역할</span><span class="sxs-lookup"><span data-stu-id="2a5b7-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-149">관리자</span><span class="sxs-lookup"><span data-stu-id="2a5b7-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-150">사용자</span><span class="sxs-lookup"><span data-stu-id="2a5b7-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-151">user1</span><span class="sxs-lookup"><span data-stu-id="2a5b7-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-152">test</span><span class="sxs-lookup"><span data-stu-id="2a5b7-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-153">user2</span><span class="sxs-lookup"><span data-stu-id="2a5b7-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-154">test1</span><span class="sxs-lookup"><span data-stu-id="2a5b7-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-155">user3</span><span class="sxs-lookup"><span data-stu-id="2a5b7-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-156">admin1</span><span class="sxs-lookup"><span data-stu-id="2a5b7-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-157">1</span><span class="sxs-lookup"><span data-stu-id="2a5b7-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-158">123</span><span class="sxs-lookup"><span data-stu-id="2a5b7-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-159">a</span><span class="sxs-lookup"><span data-stu-id="2a5b7-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-160">actuser</span><span class="sxs-lookup"><span data-stu-id="2a5b7-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="2a5b7-161">adm</span><span class="sxs-lookup"><span data-stu-id="2a5b7-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-162">admin2</span><span class="sxs-lookup"><span data-stu-id="2a5b7-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="2a5b7-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-164">backup</span><span class="sxs-lookup"><span data-stu-id="2a5b7-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-165">console</span><span class="sxs-lookup"><span data-stu-id="2a5b7-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-166">david</span><span class="sxs-lookup"><span data-stu-id="2a5b7-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-167">guest</span><span class="sxs-lookup"><span data-stu-id="2a5b7-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-168">john</span><span class="sxs-lookup"><span data-stu-id="2a5b7-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-169">owner</span><span class="sxs-lookup"><span data-stu-id="2a5b7-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-170">root</span><span class="sxs-lookup"><span data-stu-id="2a5b7-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-171">server</span><span class="sxs-lookup"><span data-stu-id="2a5b7-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-172">sql</span><span class="sxs-lookup"><span data-stu-id="2a5b7-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-173">support</span><span class="sxs-lookup"><span data-stu-id="2a5b7-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="2a5b7-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-175">sys</span><span class="sxs-lookup"><span data-stu-id="2a5b7-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a5b7-176">test2</span><span class="sxs-lookup"><span data-stu-id="2a5b7-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-177">test3</span><span class="sxs-lookup"><span data-stu-id="2a5b7-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-178">user4</span><span class="sxs-lookup"><span data-stu-id="2a5b7-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a5b7-179">user5</span><span class="sxs-lookup"><span data-stu-id="2a5b7-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="2a5b7-180">VM을 만들 때 hello 암호 요구 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2a5b7-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="2a5b7-181">암호는 6 72 자가 하 여야 하 고 4 복잡성 요구 사항을 준수 하는 hello 부족 3 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="2a5b7-182">소문자 포함</span><span class="sxs-lookup"><span data-stu-id="2a5b7-182">Have lower characters</span></span>
* <span data-ttu-id="2a5b7-183">대문자 포함</span><span class="sxs-lookup"><span data-stu-id="2a5b7-183">Have upper characters</span></span>
* <span data-ttu-id="2a5b7-184">숫자 포함</span><span class="sxs-lookup"><span data-stu-id="2a5b7-184">Have a digit</span></span>
* <span data-ttu-id="2a5b7-185">특수 문자 포함(정규식 일치 [\W_])</span><span class="sxs-lookup"><span data-stu-id="2a5b7-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="2a5b7-186">암호를 다음 hello 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a5b7-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="2a5b7-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="2a5b7-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-189">Password!</span><span class="sxs-lookup"><span data-stu-id="2a5b7-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-190">Password1</span><span class="sxs-lookup"><span data-stu-id="2a5b7-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-191">Password22</span><span class="sxs-lookup"><span data-stu-id="2a5b7-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a5b7-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="2a5b7-192">iloveyou!</span></span></td>
    </tr>
</table>
