---
title: "Azure에서 Linux Vm에 대 한 유지 관리를 다시 시작 aaaVM | Microsoft Docs"
description: "Linux 가상 컴퓨터의 VM 다시 시작 유지 관리에 대해 다룹니다."
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a><span data-ttu-id="fa17d-103">VM 다시 시작 유지 관리</span><span class="sxs-lookup"><span data-stu-id="fa17d-103">VM restarting maintenance</span></span>

<span data-ttu-id="fa17d-104">Vm에 기본 인프라 tooplanned 유지 관리 toohello 인해 다시 부팅 되는 몇 가지 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-104">There are few cases where your VMs are rebooted due tooplanned maintenance toohello underlying infrastructure.</span></span> <span data-ttu-id="fa17d-105">Azure에서 호스트 Vm의 가용성을 주의깊게 toothe 되 고, hello 다음 toouse 있습니다 수 이제 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-105">Being impactful toothe availability of your VMs hosted in Azure, hello following are now available for you toouse:</span></span>

-   <span data-ttu-id="fa17d-106">알림이는 hello 영향 전에 30 일 이내에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-106">Notification sent at least 30 days before hello impact.</span></span>

-   <span data-ttu-id="fa17d-107">각 VM 당 가시성 toohello 유지 관리 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-107">Visibility toohello maintenance windows per each VM.</span></span>

-   <span data-ttu-id="fa17d-108">유연성 및 hello 정확한 시간에 Vm에 영향을 주는 유지 관리에 대 한 설정에서 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-108">Flexibility and control in setting hello exact time for maintenance to impact your VMs.</span></span>

<span data-ttu-id="fa17d-109">Microsoft Azure의 유지 관리는 반복적으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-109">Maintenance in Microsoft Azure is scheduled in iterations.</span></span> <span data-ttu-id="fa17d-110">초기 반복 순서 tooreduce hello 위험 출시 된 새로운 수정 및 기능에 관련 된 작은 범위가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-110">Initial iterations have smaller scope in order tooreduce hello risk involved in rolling out new fixes and capabilities.</span></span> <span data-ttu-id="fa17d-111">후기 반복에서 구현 여러 영역에 걸쳐 있을 수 있습니다 (되지 hello에서에서 동일한 지역 쌍).</span><span class="sxs-lookup"><span data-stu-id="fa17d-111">Later iterations may span multiple regions (never from hello same region pair).</span></span> <span data-ttu-id="fa17d-112">VM은 단일 유지 관리 반복에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-112">A VM is included in a single maintenance iteration.</span></span> <span data-ttu-id="fa17d-113">반복이 중단되면 나머지 VM은 미래의 다른 반복에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-113">If an iteration is aborted, remaining VMs are included in another, future, iteration.</span></span>

<span data-ttu-id="fa17d-114">hello 계획 된 유지 관리 반복은 두 단계: Pre-emptive 유지 관리 기간 및 예약 된 유지 관리 기간.</span><span class="sxs-lookup"><span data-stu-id="fa17d-114">hello planned maintenance iteration has two phases: Pre-emptive Maintenance Window and a Scheduled-Maintenance Window.</span></span>

<span data-ttu-id="fa17d-115">hello **Pre-emptive 유지 관리 기간** Vm에 대 한 hello 유연성 tooinitiate hello 관리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-115">hello **Pre-emptive Maintenance Window** provides you with hello flexibility tooinitiate hello maintenance on your VMs.</span></span> <span data-ttu-id="fa17d-116">이러한 작업을 통해 Vm에는 영향을 확인, 시퀀스 hello 업데이트와 유지 되 고 각 VM 간의 hello 시간 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-116">By doing so, you can determine when your VMs are impacted, hello sequence of hello update, and hello time between each VM being maintained.</span></span> <span data-ttu-id="fa17d-117">각 VM toosee 유지 관리에 대 한 계획 되어 있는지 여부를 쿼리하고 수 마지막 요청이 시작 된 유지 관리의 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-117">You can query each VM toosee whether it is planned for maintenance and check hello result of your last initiated maintenance request.</span></span>

<span data-ttu-id="fa17d-118">hello **예약 된 유지 관리 기간** 때 Azure hello 유지 관리를 위해 Vm에 예약 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-118">hello **Scheduled Maintenance Window** is when Azure has scheduled your VMs for hello maintenance.</span></span> <span data-ttu-id="fa17d-119">다음에 나오는 선점형 유지 관리 기간을이 기간 동안 hello 유지 관리 기간을 쿼리할 수 있지만 더 이상 수 tooorchestrate hello 유지 관리 될 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-119">During this time window, which follows the pre-emptive maintenance window, you can still query for hello maintenance window, but no longer be able tooorchestrate hello maintenance.</span></span>

## <a name="availability-considerations-during-planned-maintenance"></a><span data-ttu-id="fa17d-120">계획된 유지 관리 기간의 가용성 고려 사항</span><span class="sxs-lookup"><span data-stu-id="fa17d-120">Availability considerations during planned maintenance</span></span> 

### <a name="paired-regions"></a><span data-ttu-id="fa17d-121">쌍을 이루는 지역</span><span class="sxs-lookup"><span data-stu-id="fa17d-121">Paired regions</span></span>

<span data-ttu-id="fa17d-122">각 Azure 영역의 다른 영역 hello 내와 쌍을 이루는 동일한 지역, 지역 쌍을 함께 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-122">Each Azure region is paired with another region within hello same geography, together making a regional pair.</span></span> <span data-ttu-id="fa17d-123">유지 관리를 실행할 때 Azure는 해당 쌍의 단일 영역에 가상 컴퓨터 인스턴스 hello만 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-123">When executing maintenance, Azure will only update hello Virtual Machine instances in a single region of its pair.</span></span> <span data-ttu-id="fa17d-124">예를 들어 hello 북 중미의 가상 컴퓨터를 업데이트할 때 Azure 업데이트 되지 것입니다: 미국 중남부에서 모든 가상 컴퓨터 hello에서 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-124">For example, when updating hello Virtual Machines in North Central US, Azure will not update any Virtual Machines in South Central US at hello same time.</span></span> <span data-ttu-id="fa17d-125">이는 별도의 다른 시간에 예약하여 지역 간의 장애 조치(failover) 또는 부하 분산을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-125">This will be scheduled at a separate time, enabling failover or load balancing between regions.</span></span> <span data-ttu-id="fa17d-126">그러나 다른 영역에서 유지 관리 유럽 북부 수와 같은 hello 동일 미국 동부로 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-126">However, other regions such as North Europe can be under maintenance at hello same time as East US.</span></span>
<span data-ttu-id="fa17d-127">[Azure 지역 쌍](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="fa17d-127">Read more about [Azure region pairs](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span></span>

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a><span data-ttu-id="fa17d-128">단일 인스턴스 VM과 가용성 집합 또는 VM 확장 집합의 차이</span><span class="sxs-lookup"><span data-stu-id="fa17d-128">Single instance VMs vs. availability set or VM scale set</span></span>

<span data-ttu-id="fa17d-129">Azure에서 가상 컴퓨터를 사용 하 여 작업을 배포할 때는 Vm hello 가용성 집합 순서 tooprovide 고가용성 tooyour 응용 프로그램 내에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-129">When deploying a workload using virtual machines in Azure, you can create hello VMs within an availability set in order tooprovide high availability tooyour application.</span></span> <span data-ttu-id="fa17d-130">이 구성을 통해 가동 중단 또는 유지 관리 이벤트 중에도 하나 이상의 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-130">This configuration ensures that during either an outage or maintenance events, at least one virtual machine is available.</span></span>

<span data-ttu-id="fa17d-131">가용성 집합 내에서 개별 Vm too20 업데이트 도메인을 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-131">Within an availability set, individual VMs are spread across up too20 update domains.</span></span> <span data-ttu-id="fa17d-132">계획된 유지 관리 동안에는 단일 업데이트 도메인만 지정된 시간에 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-132">During planned maintenance, only a single update domain is impacted at any given time.</span></span> <span data-ttu-id="fa17d-133">계획 된 유지 관리 하는 동안 영향 받고 업데이트 도메인의 hello 순서 순차적으로 진행 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-133">hello order of update domains being impacted may not proceed sequentially during planned maintenance.</span></span> <span data-ttu-id="fa17d-134">단일 인스턴스 Vm (가용성 집합의 일부가 아님), 즉 다음 없는 방식으로 toopredict 하거나와 함께 Vm 수는 영향을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-134">For single instance VMs (not part of availability set), there is no way toopredict or determine which and how many VMs are impacted together.</span></span>

<span data-ttu-id="fa17d-135">가상 컴퓨터 크기 집합 toodeploy 하는 Azure 계산 리소스를 사용 하면 되 고 단일 리소스로 동일한 Vm 집합이 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-135">Virtual machine scale sets are an Azure compute resource that enables you toodeploy and manage a set of identical VMs as a single resource.</span></span>
<span data-ttu-id="fa17d-136">hello 크기 집합 비슷한 보장 tooan 가용성 업데이트 도메인의 형태로 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-136">hello scale set provides similar guarantees tooan availability set in the form of update domains.</span></span> 

<span data-ttu-id="fa17d-137">고가용성을 위해 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 참조 [ *Windows 가상 컴퓨터의 가용성을 hello 관리*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-137">For more information about configuring your virtual machines for high availability, see [*Manage hello availability of your Windows virtual machines*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="scheduled-events"></a><span data-ttu-id="fa17d-138">예약된 이벤트</span><span class="sxs-lookup"><span data-stu-id="fa17d-138">Scheduled events</span></span>

<span data-ttu-id="fa17d-139">메타 데이터 서비스를 azure 가상 컴퓨터가 Azure에서 호스트에 대 한 정보를 toodiscover 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-139">Azure Metadata Service enables you toodiscover information about your Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="fa17d-140">예약 된 이벤트가 예정 된 이벤트에 대 한 화면 정보 노출 hello 범주 중 하나 (예를 들어 다시 부팅) 응용 프로그램을 준비 하 고 제한할 수 있도록 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-140">Scheduled Events, one of hello exposed categories, surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span>

<span data-ttu-id="fa17d-141">예약 된 이벤트에 대 한 자세한 내용은 참조 너무[Azure 메타 데이터 서비스-예약 된 이벤트](../virtual-machines-scheduled-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-141">For more information about scheduled events, refer too[Azure Metadata Service - Scheduled Events](../virtual-machines-scheduled-events.md).</span></span>

## <a name="maintenance-discovery-and-notifications"></a><span data-ttu-id="fa17d-142">유지 관리 검색 및 알림</span><span class="sxs-lookup"><span data-stu-id="fa17d-142">Maintenance discovery and notifications</span></span>

<span data-ttu-id="fa17d-143">유지 관리 일정이 표시 toocustomers 개별 Vm의 hello 수준에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-143">Maintenance schedule is visible toocustomers at hello level of individual VMs.</span></span> <span data-ttu-id="fa17d-144">Azure를 사용 하면 포털, API, PowerShell 또는 CLI tooquery 선점형 및 예약 된 유지 관리 기간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-144">You can use Azure portal, API, PowerShell, or CLI tooquery for the pre-emptive and scheduled maintenance windows.</span></span> <span data-ttu-id="fa17d-145">또한 hello 경우에서 알림 (전자 메일)을 받을 가능성이 있는 hello 프로세스 중 하나 (이상)의 Vm에는 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-145">In addition, expect to receive a notification (email) in hello case where one (or more) of your VMs are impacted during hello process.</span></span>

<span data-ttu-id="fa17d-146">선점형 유지 관리 및 예약된 유지 관리 단계는 모두 알림으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-146">Both pre-emptive maintenance and scheduled maintenance phases begin with a notification.</span></span> <span data-ttu-id="fa17d-147">Azure 구독 당 단일 알림 tooreceive가 있기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-147">Expect tooreceive a single notification per Azure subscription.</span></span> <span data-ttu-id="fa17d-148">기본적으로 toohello 구독의 관리자 및 공동 관리자 hello 알림이 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-148">hello notification is sent toohello subscription’s admin and co-admin by default.</span></span> <span data-ttu-id="fa17d-149">또한 유지 관리 알림을 hello 대상 그룹을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-149">You can also configure hello audience for the maintenance notification.</span></span>

### <a name="view-hello-maintenance-window-in-hello-portal"></a><span data-ttu-id="fa17d-150">Hello 포털에서 보기 hello 유지 관리 기간</span><span class="sxs-lookup"><span data-stu-id="fa17d-150">View hello maintenance window in hello portal</span></span> 

<span data-ttu-id="fa17d-151">Hello Azure 포털을 사용할 수 있으며 유지 관리를 위해 예약 된 Vm을 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="fa17d-151">You can use hello Azure portal and look for VMs scheduled for maintenance.</span></span>

1.  <span data-ttu-id="fa17d-152">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-152">Sign in toohello Azure portal.</span></span>

2.  <span data-ttu-id="fa17d-153">클릭 하 고 hello 엽니다 **가상 컴퓨터** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-153">Click and open hello **Virtual Machines** blade.</span></span>

3.  <span data-ttu-id="fa17d-154">Hello 클릭 **열** 에서 사용 가능한 열 toochoose 목록이 tooopen hello 단추</span><span class="sxs-lookup"><span data-stu-id="fa17d-154">Click hello **Columns** button tooopen hello list of available columns toochoose from</span></span>

4.  <span data-ttu-id="fa17d-155">선택 하 고 hello 추가 **유지 관리 기간** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-155">Select and add hello **Maintenance Window** columns.</span></span> <span data-ttu-id="fa17d-156">유지 관리에 대 한 예정 된 Vm가 hello 유지 관리 기간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-156">VMs that are scheduled for maintenance have hello maintenance windows surfaced.</span></span> <span data-ttu-id="fa17d-157">a에 대한 유지 관리가 완료되거나 중단되면 유지 관리 기간이 더 이상 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-157">Once maintenance is completed or aborted for a, the maintenance window is no longer be presented.</span></span>

### <a name="query-maintenance-details-using-hello-azure-api"></a><span data-ttu-id="fa17d-158">Hello Azure API를 사용 하 여 유지 관리 정보를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-158">Query maintenance details using hello Azure API</span></span>

<span data-ttu-id="fa17d-159">사용 하 여 hello [VM API 정보를 가져올](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) hello 인스턴스 toodiscover hello 유지 관리 세부 정보 보기에는 개별 VM 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-159">Use hello [get VM information API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) and look for hello instance view toodiscover hello maintenance details on an individual VM.</span></span> <span data-ttu-id="fa17d-160">hello 응답 hello 요소 다음에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-160">hello response includes hello following elements:</span></span>

  - <span data-ttu-id="fa17d-161">isCustomerInitiatedMaintenanceAllowed: 이제 hello VM에서 선점형 재배포를 시작할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-161">isCustomerInitiatedMaintenanceAllowed: Indicates whether you can now initiate pre-emptive redeploy on hello VM.</span></span>

  - <span data-ttu-id="fa17d-162">preMaintenanceWindowStartTime: hello hello 선점형 유지 관리 기간의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-162">preMaintenanceWindowStartTime: hello start time of hello pre-emptive maintenance window.</span></span>

  - <span data-ttu-id="fa17d-163">preMaintenanceWindowEndTime: hello hello 선점형 유지 관리 기간의 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-163">preMaintenanceWindowEndTime: hello end time of hello pre-emptive maintenance window.</span></span> <span data-ttu-id="fa17d-164">이 시간 이후이 VM으로 수 tooinitiate 유지 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-164">After this time, you will no longer be able tooinitiate maintenance on this VM.</span></span>
    
  - <span data-ttu-id="fa17d-165">maintenanceWindowStartTime: hello VM 영향을 받을 때 hello 예약 된 유지 관리 기간의 시간을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-165">maintenanceWindowStartTime: hello start time of hello scheduled maintenance window when your VM are impacted.</span></span>

  - <span data-ttu-id="fa17d-166">maintenanceWindowEndTime: hello hello 예약 된 유지 관리 기간의 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-166">maintenanceWindowEndTime: hello end time of hello scheduled maintenance window.</span></span>
  
  - <span data-ttu-id="fa17d-167">lastOperationResultCode: hello 마지막 재배포 유지 관리 작업의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-167">lastOperationResultCode: hello result of your last Maintenance-Redeploy operation.</span></span>
 
  - <span data-ttu-id="fa17d-168">lastOperationMessage: 마지막 재배포 유지 관리 작업의 hello 결과 설명 하는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-168">lastOperationMessage:  Message describing hello result of your last Maintenance-Redeploy operation.</span></span>


## <a name="pre-emptive-redeploy"></a><span data-ttu-id="fa17d-169">선점형 다시 배포</span><span class="sxs-lookup"><span data-stu-id="fa17d-169">Pre-emptive redeploy</span></span>

<span data-ttu-id="fa17d-170">선점형 재배포 작업이 Azure에서 적용 된 tooyour Vm을 유지 관리 하는 hello 유연성 toocontrol hello 시간을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-170">Pre-emptive redeploy action provides hello flexibility toocontrol hello time when maintenance is applied tooyour VMs in Azure.</span></span> <span data-ttu-id="fa17d-171">계획 된 유지 관리를 다시 부팅 하 여 Vm toobe 각각에 대 한 정확한 시간 hello 결정할 수 있습니다 선점형 유지 관리 기간으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-171">Planned maintenance begins with a pre-emptive maintenance window where you can decide on hello exact time for each of your VMs toobe rebooted.</span></span> <span data-ttu-id="fa17d-172">이러한 기능이 유용한 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-172">The following are use cases where such a functionality is useful:</span></span>

-   <span data-ttu-id="fa17d-173">유지 관리 요구 toobe hello 최종 사용자와 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-173">Maintenance need toobe coordinated with hello end customer.</span></span>

-   <span data-ttu-id="fa17d-174">Azure에서 제공 하는 hello 예약 된 유지 관리 기간이 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-174">hello scheduled maintenance window offered by Azure is not sufficient.</span></span>
    <span data-ttu-id="fa17d-175">Toobe 요일 hello 가장 바쁜 시간에 발생 하는 hello 창 또는 너무 길어서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-175">It could be that hello window happens toobe on hello busiest time of the week or it is too long.</span></span>

-   <span data-ttu-id="fa17d-176">다중 인스턴스 또는 다중 계층 응용 프로그램에 대 한 두 개의 Vm 또는 특정 순서 toofollow 사이의 시간이 충분 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-176">For multi-instance or multi-tier applications, you need sufficient time between two VMs or a certain sequence toofollow.</span></span>

<span data-ttu-id="fa17d-177">VM에서 선점형 재배포에 대 한 호출 hello VM tooan 이미 노드를 업데이트 하 고 다음 공급 다시에 모든 구성 옵션 및 관련된 리소스 그대로 유지 하 고 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-177">When you call for pre-emptive redeploy on a VM, it moves hello VM tooan already updated node and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="fa17d-178">이렇게 하면 임시 디스크 hello 손실 되며 동적 IP 주소와 연결 된 동안에 가상 네트워크 인터페이스 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-178">While doing so, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span>

<span data-ttu-id="fa17d-179">선점형 다시 배포는 VM당 한 번만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-179">Pre-emptive redeploy is enabled once per VM.</span></span> <span data-ttu-id="fa17d-180">Hello 프로세스 중 오류가 발생 하는 hello 작업이 중단 되 면 VM은 영향을 받지 hello 이므로 hello 계획 된 유지 관리 반복에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-180">If there is an error during hello process, hello operation is aborted, hello VM is not impacted and it is excluded from hello planned maintenance iteration.</span></span> <span data-ttu-id="fa17d-181">새 일정에 나중에 접속 선택한 새 기회 tooschedule 및 시퀀스 hello 영향을 Vm에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa17d-181">You will be contacted in a later time with a new schedule and offered a new opportunity tooschedule and sequence hello impact on your VMs.</span></span>
