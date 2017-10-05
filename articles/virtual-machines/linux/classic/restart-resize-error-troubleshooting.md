---
title: "VM 재시작 또는 크기 조정 문제 | Microsoft Docs"
description: "Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="ae065-103">Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ae065-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae065-104">클래식</span><span class="sxs-lookup"><span data-stu-id="ae065-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="ae065-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="ae065-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="ae065-106">중지된 Azure 가상 컴퓨터(VM)를 시작하거나, 기존 Azure AM의 크기를 조정하려다 접하는 일반적인 오류는 할당 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="ae065-107">이런 오류는 클러스터나 지역에 사용할 수 있는 리소스가 없거나 요청한 VM 크기를 지원할 수 없을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ae065-108">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ae065-109">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ae065-110">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ae065-111">Resource Manager 버전은 [여기](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae065-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="ae065-112">감사 로그 수집</span><span class="sxs-lookup"><span data-stu-id="ae065-112">Collect audit logs</span></span>
<span data-ttu-id="ae065-113">문제 해결을 시작하려면 문제와 관련된 오류를 파악하기 위해 감사 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="ae065-114">Azure Portal에서 **찾아보기** > **가상 컴퓨터** > *Linux 가상 컴퓨터* > **설정** > **감사 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="ae065-115">문제: 중지된 VM 시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="ae065-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="ae065-116">중지된 VM을 시작하려는데 할당 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="ae065-117">원인</span><span class="sxs-lookup"><span data-stu-id="ae065-117">Cause</span></span>
<span data-ttu-id="ae065-118">중지된 VM을 시작하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="ae065-119">하지만, 클러스터에 요청을 수행하는 데 사용할 여유 공간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="ae065-120">해결 방법</span><span class="sxs-lookup"><span data-stu-id="ae065-120">Resolution</span></span>
* <span data-ttu-id="ae065-121">새 클라우드 서비스를 만들어서 지역 또는 지역 기반 가상 네트워크와 연결하지만 선호도 그룹과는 연결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="ae065-122">중지된 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="ae065-123">디스크를 사용하여 새 클라우드 서비스에 VM을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="ae065-124">다시 만든 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-124">Start the re-created VM.</span></span>

<span data-ttu-id="ae065-125">새 클라우드 서비스를 만들려다 오류가 발생하면, 나중에 다시 시도하거나 클라우드 서비스의 지역을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae065-126">새 클라우드 서비스는 새로운 이름과 VIP를 갖게 되므로, 기존 클라우드 서비스의 해당 정보를 사용하는 모든 종속성에 대해 해당 정보를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="ae065-127">문제: 기존 VM 재시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="ae065-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="ae065-128">기존 VM의 크기를 조정하려는데 할당 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="ae065-129">원인</span><span class="sxs-lookup"><span data-stu-id="ae065-129">Cause</span></span>
<span data-ttu-id="ae065-130">VM 크기를 조정하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="ae065-131">하지만, 클러스터가 요청한 VM 크기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="ae065-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="ae065-132">Resolution</span></span>
<span data-ttu-id="ae065-133">요청한 VM 크기를 줄이고 크기 조정 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="ae065-134">**모두 찾아보기** > **가상 컴퓨터(클래식)** > *사용자의 가상 컴퓨터* > **설정** > **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="ae065-135">자세한 단계는 [가상 컴퓨터 크기 조정](https://msdn.microsoft.com/library/dn168976.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae065-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="ae065-136">VM 크기를 줄이는 것이 가능하지 않으면, 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="ae065-137">새 클라우드 서비스를 만들어서, 선호도 그룹에 연결되지 않도록 하고 선호도 그룹에 연결된 가상 네트워크와 연결되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="ae065-138">그 안에 큰 규모의 VM을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="ae065-139">모든 VM을 동일한 클라우드 서비스로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="ae065-140">기존 클라우드 서비스가 지역 기반 가상 네트워크와 연결된 경우, 새 클라우드 서비스를 기존 가상 네트워크에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="ae065-141">기존 클라우드 서비스가 지역 기반 가상 네트워크에 연결되지 않은 경우에는, 기존 클라우드 서비스의 VM을 삭제하고 디스크에서 새 클라우드 서비스에 VM을 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="ae065-142">하지만, 새 클라우드 서비스가 새 이름과 VIP를 갖게 되므로, 기존 클라우드 서비스에 이 정보를 사용하는 모든 종속성에 대해 해당 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae065-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae065-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae065-143">Next steps</span></span>
<span data-ttu-id="ae065-144">Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae065-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

