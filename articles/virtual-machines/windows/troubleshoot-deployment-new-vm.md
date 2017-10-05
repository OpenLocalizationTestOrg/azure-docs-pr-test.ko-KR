---
title: "Azure에서 Windows VM 배포 문제 해결 | Microsoft Docs"
description: "Azure에서 새 Windows 가상 컴퓨터 생성 시 Resource Manager 배포 문제 해결"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 86795ba6eab3505a3d539e4fc4e032bdeecc2e78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="1b1d0-103">Azure에서 새 Windows VM 생성 시 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1b1d0-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="1b1d0-104">주요 문제</span><span class="sxs-lookup"><span data-stu-id="1b1d0-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="1b1d0-105">VM 배포 문제 및 질문은 [Azure에서 Windows 가상 컴퓨터 배포 문제 해결](troubleshoot-deploy-vm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="1b1d0-106">활동 로그 선택</span><span class="sxs-lookup"><span data-stu-id="1b1d0-106">Collect activity logs</span></span>
<span data-ttu-id="1b1d0-107">문제 해결을 시작하려면 문제와 관련된 오류를 파악하기 위해 활동 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="1b1d0-108">다음 링크에는 수행할 프로세스에 대한 자세한 내용이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="1b1d0-109">배포 작업 보기</span><span class="sxs-lookup"><span data-stu-id="1b1d0-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="1b1d0-110">활동 로그를 보고 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="1b1d0-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="1b1d0-111">**Y:** OS가 일반화된 Windows인 경우, 일반화된 설정을 사용하여 업로드되거나 캡처되고, 오류는 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-111">**Y:** If the OS is Windows generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="1b1d0-112">마찬가지로 OS가 특수화된 Windows인 경우, 특수화된 설정을 사용하여 업로드되거나 캡처되고, 오류는 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-112">Similarly, if the OS is Windows specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="1b1d0-113">**업로드 오류:**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-113">**Upload Errors:**</span></span>

<span data-ttu-id="1b1d0-114">**N<sup>1</sup>:** OS가 일반화된 Windows이고 특수화된 것으로 업로드된다면, VM이 OOBE 화면에서 중단되면서 프로비전 시간 초과 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-114">**N<sup>1</sup>:** If the OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with the VM stuck at the OOBE screen.</span></span>

<span data-ttu-id="1b1d0-115">**N<sup>2</sup>:** OS가 특수화된 Windows이고 일반화된 것으로 업로드된다면, 새 VM이 원래 컴퓨터 이름, 사용자 이름 및 암호로 실행되기 때문에 VM이 OOBE 화면에서 중단되면서 프로비전 실패 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-115">**N<sup>2</sup>:** If the OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with the VM stuck at the OOBE screen because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="1b1d0-116">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-116">**Resolution**</span></span>

<span data-ttu-id="1b1d0-117">이 두 가지 오류를 모두 해결하려면, OS와 같은 설정(일반화/특수화)으로, [Add-AzureRmVhd를 사용하여 원본 VHD를 업로드](https://msdn.microsoft.com/library/mt603554.aspx)합니다(온-프레미스에 있는).</span><span class="sxs-lookup"><span data-stu-id="1b1d0-117">To resolve both these errors, use [Add-AzureRmVhd to upload the original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="1b1d0-118">일반화된 것으로 업로드하려면, 먼저 sysprep을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-118">To upload as generalized, remember to run sysprep first.</span></span>

<span data-ttu-id="1b1d0-119">**캡처 오류:**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-119">**Capture Errors:**</span></span>

<span data-ttu-id="1b1d0-120">**N<sup>3</sup>:** OS가 일반화된 Windows이고 특수화된 것으로 캡처된다면, 원본 VM이 일반화된 것으로 표시되어 사용할 수 없기 때문에 프로비전 시간 초과 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-120">**N<sup>3</sup>:** If the OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="1b1d0-121">**N<sup>4</sup>:** OS가 특수화된 Windows이고 일반화된 것으로 캡처된다면, 새 VM이 원래 컴퓨터 이름, 사용자 이름 및 암호로 실행되기 때문에 프로비전 실패 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-121">**N<sup>4</sup>:** If the OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username, and password.</span></span> <span data-ttu-id="1b1d0-122">또한, 원본 VM이 일반화된 것으로 표시되기 때문에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="1b1d0-123">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-123">**Resolution**</span></span>

<span data-ttu-id="1b1d0-124">이 두 가지 오류를 모두 해결하려면, 현재 이미지를 포털에서 제거하고, OS와 같은 설정(일반화/특수화)으로 [현재 VHD에서 다시 캡처](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="1b1d0-125">문제: 사용자 지정/갤러리/마켓플레이스 이미지, 할당 오류</span><span class="sxs-lookup"><span data-stu-id="1b1d0-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="1b1d0-126">이 오류는 요청되는 VM 크기를 지원할 수 없거나 요청을 수용할 여유 공간이 없는 클러스터에 새 VM 요청이 고정된 상황에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="1b1d0-127">**원인 1:** 클러스터가 요청한 VM 크기를 지원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="1b1d0-128">**해결 방법 1:**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-128">**Resolution 1:**</span></span>

* <span data-ttu-id="1b1d0-129">더 작은 VM 크기를 사용하여 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="1b1d0-130">요청한 VM의 크기를 변경할 수 없으면:</span><span class="sxs-lookup"><span data-stu-id="1b1d0-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="1b1d0-131">가용성 집합의 VM을 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="1b1d0-132">**리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="1b1d0-133">VM을 모두 중지한 후에, 원하는 크기로 VM을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="1b1d0-134">먼저 VM을 시작한 후에 중지된 각각의 VM을 선택하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="1b1d0-135">**원인 2:** 클러스터에 여유 리소스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="1b1d0-136">**해결 방법 2:**</span><span class="sxs-lookup"><span data-stu-id="1b1d0-136">**Resolution 2:**</span></span>

* <span data-ttu-id="1b1d0-137">요청을 나중에 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="1b1d0-138">새 VM이 다른 가용성 집합의 일부가 될 수 있다면</span><span class="sxs-lookup"><span data-stu-id="1b1d0-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="1b1d0-139">다른 가용성 집합(동일한 지역의)에 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="1b1d0-140">새 VM을 동일한 가상 네트워크에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b1d0-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b1d0-141">Next steps</span></span>
<span data-ttu-id="1b1d0-142">중지된 Windows VM을 시작하거나 Azure에서 기존 Windows VM의 크기를 조정할 때 문제가 발생하면 [Azure의 기존 Windows 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b1d0-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

