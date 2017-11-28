---
title: "다시 시작 하거나 크기 조정 문제 aaaVM | Microsoft Docs"
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
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="f6f4b-103">Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f6f4b-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6f4b-104">클래식</span><span class="sxs-lookup"><span data-stu-id="f6f4b-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="f6f4b-105">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="f6f4b-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="f6f4b-106">Toostart 중지 된 Azure 가상 컴퓨터 (VM)를 시도 하거나 기존 Azure VM의 크기를 조정할 때 발생 하는 hello 일반적인 오류는 할당 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="f6f4b-107">이 오류는 hello 클러스터 또는 지역 중 하나에 없는 사용 가능한 리소스 또는 없습니다 지원 hello v M 크기를 요청 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f6f4b-108">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f6f4b-109">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f6f4b-110">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f6f4b-111">Hello 리소스 관리자 버전에 대 한 참조 [여기](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="f6f4b-112">감사 로그 수집</span><span class="sxs-lookup"><span data-stu-id="f6f4b-112">Collect audit logs</span></span>
<span data-ttu-id="f6f4b-113">문제 해결, toostart 수집 hello 감사 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="f6f4b-114">Hello Azure 포털에서에서 클릭 **찾아보기** > **가상 컴퓨터** > *Linux 가상 컴퓨터*  >   **설정** > **감사 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="f6f4b-115">문제: 중지된 VM 시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="f6f4b-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="f6f4b-116">Toostart 중지 된 VM을 시도 하지만 할당에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f6f4b-117">원인</span><span class="sxs-lookup"><span data-stu-id="f6f4b-117">Cause</span></span>
<span data-ttu-id="f6f4b-118">toostart hello VM을 중지 하는 hello 요청에 toobe hello 클라우드 서비스를 호스팅하는 hello 원본 클러스터에 시도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f6f4b-119">그러나 hello 클러스터 여유 공간이 사용 가능한 toofulfill hello 요청은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="f6f4b-120">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f6f4b-120">Resolution</span></span>
* <span data-ttu-id="f6f4b-121">새 클라우드 서비스를 만들어서 지역 또는 지역 기반 가상 네트워크와 연결하지만 선호도 그룹과는 연결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="f6f4b-122">삭제 hello VM을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="f6f4b-123">Hello 디스크를 사용 하 여 hello 새 클라우드 서비스에 VM hello를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="f6f4b-124">시작 hello VM을 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-124">Start hello re-created VM.</span></span>

<span data-ttu-id="f6f4b-125">Toocreate 새 클라우드 서비스는 동안 오류가 발생 합니다 나중에 다시 시도 하거나 다른 곳으로 hello 클라우드 서비스에 대 한 hello 영역을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6f4b-126">hello 새 클라우드 서비스는 없으므로 새 이름 및 VIP를 hello 기존 클라우드 서비스에 대 한 해당 정보를 사용 하는 모든 hello 종속성에 대 한 정보를 toochange를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="f6f4b-127">문제: 기존 VM 재시작 시 오류</span><span class="sxs-lookup"><span data-stu-id="f6f4b-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="f6f4b-128">Tooresize 기존 VM을 시도 하지만 할당에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f6f4b-129">원인</span><span class="sxs-lookup"><span data-stu-id="f6f4b-129">Cause</span></span>
<span data-ttu-id="f6f4b-130">tooresize hello VM에 toobe hello 요청 했으나 hello 원본 클러스터에서 해당 호스트 hello 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="f6f4b-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f6f4b-131">그러나 hello 클러스터를 지원 하지 않는 요청 된 VM 크기 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="f6f4b-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f6f4b-132">Resolution</span></span>
<span data-ttu-id="f6f4b-133">줄일 hello v M 크기를 요청 하 고 요청을 조정 하는 재시도 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="f6f4b-134">**모두 찾아보기** > **가상 컴퓨터(클래식)** > *사용자의 가상 컴퓨터* > **설정** > **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="f6f4b-135">자세한 내용은 참조 [hello 가상 컴퓨터 크기를 조정한](https://msdn.microsoft.com/library/dn168976.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="f6f4b-136">가능한 tooreduce hello VM 크기가 없는 경우 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="f6f4b-137">연결 된 tooan 선호도 그룹이 아닙니다 실행 하 고 있는 연결 된 tooan 선호도 그룹은 가상 네트워크와 연결 되지 않은 새 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="f6f4b-138">그 안에 큰 규모의 VM을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="f6f4b-139">모든 Vm을 통합할 수 hello에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="f6f4b-140">기존 클라우드 서비스와 영역 기반 가상 네트워크와 연결 된 경우에 hello 새 클라우드 서비스 toohello 기존 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="f6f4b-141">Hello 기존 클라우드 서비스 영역 기반 가상 네트워크에 연결 되어 있으면 다음 hello 기존 클라우드 서비스에 대 한 Vm toodelete hello에 있고 hello 해당 디스크에서 새 클라우드 서비스에서 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="f6f4b-142">그러나 것이 중요 한 tooremember hello 새 클라우드 서비스 들이 있는 새 이름 및 VIP를 tooupdate 해야 하므로 현재 hello 기존 클라우드 서비스에 대 한이 정보를 사용 하는 모든 hello 종속성에 대 한 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f4b-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6f4b-143">Next steps</span></span>
<span data-ttu-id="f6f4b-144">Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6f4b-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

