---
title: "Azure에서 다시 시작 하거나 크기를 조정할 aaaVM 발급 | Microsoft Docs"
description: "Azure의 기존 Windows 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="e0175-103">Azure에서 기존 Windows VM 재시작 또는 크기 조정 관련 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e0175-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="e0175-104">Toostart 중지 된 Azure 가상 컴퓨터 (VM)를 시도 하거나 기존 Azure VM의 크기를 조정할 때 발생 하는 hello 일반적인 오류는 할당 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="e0175-105">이 오류는 hello 클러스터 또는 지역 중 하나에 없는 사용 가능한 리소스 또는 없습니다 지원 hello v M 크기를 요청 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="e0175-106">활동 로그 선택</span><span class="sxs-lookup"><span data-stu-id="e0175-106">Collect activity logs</span></span>
<span data-ttu-id="e0175-107">문제 해결, toostart 수집 hello 활동 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="e0175-108">hello 프로세스에 대 한 자세한 정보를 포함 하는 링크를 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="e0175-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="e0175-109">배포 작업 보기</span><span class="sxs-lookup"><span data-stu-id="e0175-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="e0175-110">Azure 활동 로그 toomanage 보기 리소스</span><span class="sxs-lookup"><span data-stu-id="e0175-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="e0175-111">문제: 중지된 VM 시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="e0175-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="e0175-112">Toostart 중지 된 VM을 시도 하지만 할당에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e0175-113">원인</span><span class="sxs-lookup"><span data-stu-id="e0175-113">Cause</span></span>
<span data-ttu-id="e0175-114">toostart hello VM을 중지 하는 hello 요청에 toobe hello 클라우드 서비스를 호스팅하는 hello 원본 클러스터에 시도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="e0175-115">그러나 hello 클러스터 여유 공간이 사용 가능한 toofulfill hello 요청은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="e0175-116">해결 방법</span><span class="sxs-lookup"><span data-stu-id="e0175-116">Resolution</span></span>
* <span data-ttu-id="e0175-117">모든 hello hello 가용성의 Vm을 설정 하 고 각 VM을 다시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="e0175-118">**리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e0175-119">모든 Vm 중지 hello 중지 hello Vm의 각 선택 하 고 시작을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="e0175-120">나중에 hello를 다시 시작 요청을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="e0175-121">문제: 기존 VM 재시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="e0175-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="e0175-122">Tooresize 기존 VM을 시도 하지만 할당에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e0175-123">원인</span><span class="sxs-lookup"><span data-stu-id="e0175-123">Cause</span></span>
<span data-ttu-id="e0175-124">tooresize hello VM에 toobe hello 요청 했으나 hello 원본 클러스터에서 해당 호스트 hello 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e0175-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="e0175-125">그러나 hello 클러스터를 지원 하지 않는 요청 된 VM 크기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="e0175-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="e0175-126">Resolution</span></span>
* <span data-ttu-id="e0175-127">더 작은 VM 크기를 사용 하 여 hello 요청을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e0175-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="e0175-128">Hello 크기인 요청한 경우 hello VM을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="e0175-129">Hello 가용성 집합에 있는 모든 hello Vm을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="e0175-130">**리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e0175-131">결국 hello 가상 컴퓨터를 중지, 원하는 hello VM tooa 더 큰 크기의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="e0175-132">Select hello 크기를 조정 VM 및 클릭 **시작**, 각 시작의 hello Vm 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0175-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0175-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0175-133">Next steps</span></span>
<span data-ttu-id="e0175-134">Azure에서 새 Windows VM을 만들 때 문제가 발생하면 [Azure에서 새 Windows 가상 컴퓨터 생성 관련 배포 문제 해결](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0175-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

