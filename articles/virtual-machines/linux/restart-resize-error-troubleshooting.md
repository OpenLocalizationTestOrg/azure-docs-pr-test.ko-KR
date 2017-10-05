---
title: "Azure의 VM 재시작 또는 크기 조정 문제 | Microsoft Docs"
description: "Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="15258-103">Azure에서 기존 Linux VM 재시작 또는 크기 조정 관련 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="15258-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="15258-104">중지된 Azure 가상 컴퓨터(VM)를 시작하거나, 기존 Azure AM의 크기를 조정하려다 접하는 일반적인 오류는 할당 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="15258-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="15258-105">이런 오류는 클러스터나 지역에 사용할 수 있는 리소스가 없거나 요청한 VM 크기를 지원할 수 없을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="15258-106">활동 로그 선택</span><span class="sxs-lookup"><span data-stu-id="15258-106">Collect activity logs</span></span>
<span data-ttu-id="15258-107">문제 해결을 시작하려면 문제와 관련된 오류를 파악하기 위해 활동 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="15258-108">다음 링크에는 프로세스에 대한 자세한 내용이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15258-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="15258-109">배포 작업 보기</span><span class="sxs-lookup"><span data-stu-id="15258-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="15258-110">활동 로그를 보고 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="15258-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="15258-111">문제: 중지된 VM 시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="15258-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="15258-112">중지된 VM을 시작하려는데 할당 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="15258-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="15258-113">원인</span><span class="sxs-lookup"><span data-stu-id="15258-113">Cause</span></span>
<span data-ttu-id="15258-114">중지된 VM을 시작하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="15258-115">하지만, 클러스터에 요청을 수행하는 데 사용할 여유 공간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15258-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="15258-116">해결 방법</span><span class="sxs-lookup"><span data-stu-id="15258-116">Resolution</span></span>
* <span data-ttu-id="15258-117">가용성 집합의 VM을 모두 중지하고 각각의 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="15258-118">**리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="15258-119">VM을 모두 중지한 후에, 중지된 각각의 VM을 선택하고 시작을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="15258-120">나중에 다시 시작 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="15258-121">문제: 기존 VM 재시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="15258-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="15258-122">기존 VM의 크기를 조정하려는데 할당 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="15258-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="15258-123">원인</span><span class="sxs-lookup"><span data-stu-id="15258-123">Cause</span></span>
<span data-ttu-id="15258-124">VM 크기를 조정하기 위한 요청은 클라우드 서비스를 호스트하는 원본 클러스터에서 시도되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="15258-125">하지만, 클러스터가 요청한 VM 크기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15258-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="15258-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="15258-126">Resolution</span></span>
* <span data-ttu-id="15258-127">더 작은 VM 크기를 사용하여 요청을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="15258-128">요청한 VM의 크기를 변경할 수 없으면:</span><span class="sxs-lookup"><span data-stu-id="15258-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="15258-129">가용성 집합의 VM을 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="15258-130">**리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="15258-131">VM을 모두 중지한 후에, 원하는 VM을 더 크게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="15258-132">크기가 조정된 VM을 선택하고 **시작**을 클릭한 다음 중지된 각각의 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="15258-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15258-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15258-133">Next steps</span></span>
<span data-ttu-id="15258-134">Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15258-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

