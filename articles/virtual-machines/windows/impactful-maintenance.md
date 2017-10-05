---
title: "Azure에서 강력한 Windows VM 유지 관리 | Microsoft Docs"
description: "Windows 가상 컴퓨터를 강력하게 유지 관리합니다."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 75cd4d567deb98e5d2498dc607b43dae483f1c94
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a><span data-ttu-id="e89e4-103">강력한 가상 컴퓨터 유지 관리</span><span class="sxs-lookup"><span data-stu-id="e89e4-103">Impactful maintenance for virtual machines</span></span>

<span data-ttu-id="e89e4-104">기본 인프라에 대한 계획된 유지 관리로 인해 VM이 다시 부팅되는 경우는 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-104">There are few cases where your VMs are rebooted due to planned maintenance to the underlying infrastructure.</span></span> <span data-ttu-id="e89e4-105">Azure에서 호스팅되는 VM의 가용성에 큰 영향을 미치기 때문에 다음 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-105">Being impactful to the availability of your VMs hosted in Azure, the following are now available for you to use:</span></span>

-   <span data-ttu-id="e89e4-106">영향을 미치기 최소 30일 전에 전송되는 알림.</span><span class="sxs-lookup"><span data-stu-id="e89e4-106">Notification sent at least 30 days before the impact.</span></span>

-   <span data-ttu-id="e89e4-107">VM당 유지 관리 기간에 대한 정보.</span><span class="sxs-lookup"><span data-stu-id="e89e4-107">Visibility to the maintenance windows per each VM.</span></span>

-   <span data-ttu-id="e89e4-108">유지 관리가 VM에 영향을 미치는 정확한 시간을 유연하게 설정 및 제어.</span><span class="sxs-lookup"><span data-stu-id="e89e4-108">Flexibility and control in setting the exact time for maintenance to impact your VMs.</span></span>

<span data-ttu-id="e89e4-109">Microsoft Azure의 유지 관리는 반복적으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-109">Maintenance in Microsoft Azure is scheduled in iterations.</span></span> <span data-ttu-id="e89e4-110">초기 반복에서는 새로운 픽스와 기능을 롤아웃하는 데 관련된 위험을 줄이기 위해 범위가 더 작습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-110">Initial iterations have smaller scope in order to reduce the risk involved in rolling out new fixes and capabilities.</span></span> <span data-ttu-id="e89e4-111">이후 반복은 여러 지역으로 확장될 수 있습니다(결코 동일한 지역 쌍에서 확장되지 않음).</span><span class="sxs-lookup"><span data-stu-id="e89e4-111">Later iterations may span multiple regions (never from the same region pair).</span></span> <span data-ttu-id="e89e4-112">VM은 단일 유지 관리 반복에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-112">A VM is included in a single maintenance iteration.</span></span> <span data-ttu-id="e89e4-113">반복이 중단되면 나머지 VM은 미래의 다른 반복에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-113">If an iteration is aborted, remaining VMs are included in another, future, iteration.</span></span>

<span data-ttu-id="e89e4-114">계획된 유지 관리 반복에는 두 단계, 즉 선점형 유지 관리 기간과 예약된 유지 관리 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-114">The planned maintenance iteration has two phases: Pre-emptive Maintenance Window and a Scheduled-Maintenance Window.</span></span>

<span data-ttu-id="e89e4-115">**선점형 유지 관리 기간**은 VM에서 유지 관리를 시작할 수 있는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-115">The **Pre-emptive Maintenance Window** provides you with the flexibility to initiate the maintenance on your VMs.</span></span> <span data-ttu-id="e89e4-116">이렇게 하면 VM에 영향을 미치는 시기, 업데이트 순서 및 각 VM을 유지 관리하는 간격을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-116">By doing so, you can determine when your VMs are impacted, the sequence of the update, and the time between each VM being maintained.</span></span> <span data-ttu-id="e89e4-117">각 VM을 쿼리하여 유지 관리하도록 계획되어 있는지 확인하고 마지막으로 시작한 유지 관리 요청의 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-117">You can query each VM to see whether it is planned for maintenance and check the result of your last initiated maintenance request.</span></span>

<span data-ttu-id="e89e4-118">**예약된 유지 관리 기간**은 Azure에서 VM을 유지 관리하도록 예약한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-118">The **Scheduled Maintenance Window** is when Azure has scheduled your VMs for the maintenance.</span></span> <span data-ttu-id="e89e4-119">선점형 유지 관리 기간 뒤에 오는 이 기간 동안 유지 관리 기간을 계속 쿼리할 수 있지만, 더 이상 유지 관리를 오케스트레이션할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-119">During this time window, which follows the pre-emptive maintenance window, you can still query for the maintenance window, but no longer be able to orchestrate the maintenance.</span></span>

## <a name="availability-considerations-during-planned-maintenance"></a><span data-ttu-id="e89e4-120">계획된 유지 관리 동안의 가용성 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e89e4-120">Availability Considerations during Planned Maintenance</span></span> 

### <a name="paired-regions"></a><span data-ttu-id="e89e4-121">쌍을 이루는 지역</span><span class="sxs-lookup"><span data-stu-id="e89e4-121">Paired Regions</span></span>

<span data-ttu-id="e89e4-122">각 Azure 지역은 동일한 지리적 위치 내의 다른 지역과 쌍을 이루어 함께 지역 쌍을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-122">Each Azure region is paired with another region within the same geography, together making a regional pair.</span></span> <span data-ttu-id="e89e4-123">유지 관리를 실행할 때 Azure는 단일 지역의 해당 쌍이 되는 가상 컴퓨터 인스턴스만 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-123">When executing maintenance, Azure will only update the Virtual Machine instances in a single region of its pair.</span></span> <span data-ttu-id="e89e4-124">예를 들어 미국 중북부에 있는 가상 컴퓨터를 업데이트할 때 Azure는 미국 중남부의 가상 컴퓨터를 동시에 업데이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-124">For example, when updating the Virtual Machines in North Central US, Azure will not update any Virtual Machines in South Central US at the same time.</span></span> <span data-ttu-id="e89e4-125">이는 별도의 다른 시간에 예약하여 지역 간의 장애 조치(failover) 또는 부하 분산을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-125">This will be scheduled at a separate time, enabling failover or load balancing between regions.</span></span> <span data-ttu-id="e89e4-126">그러나 북유럽 등의 다른 지역은 미국 동부와 동시에 유지 관리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-126">However, other regions such as North Europe can be under maintenance at the same time as East US.</span></span>
<span data-ttu-id="e89e4-127">[Azure 지역 쌍](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e89e4-127">Read more about [Azure region pairs](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span></span>

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a><span data-ttu-id="e89e4-128">단일 인스턴스 Vm vs입니다. 가용성 집합 또는 VM 크기 집합</span><span class="sxs-lookup"><span data-stu-id="e89e4-128">Single Instance VMs vs. Availability Set or VM scale set</span></span>

<span data-ttu-id="e89e4-129">Azure에서 가상 컴퓨터를 사용하여 워크로드를 배포할 때 응용 프로그램에 고가용성을 제공하기 위해 가용성 집합 내에 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-129">When deploying a workload using virtual machines in Azure, you can create the VMs within an availability set in order to provide high availability to your application.</span></span> <span data-ttu-id="e89e4-130">이 구성을 통해 가동 중단 또는 유지 관리 이벤트 중에도 하나 이상의 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-130">This configuration ensures that during either an outage or maintenance events, at least one virtual machine is available.</span></span>

<span data-ttu-id="e89e4-131">가용성 집합 내에서 개별 VM은 최대 20개의 업데이트 도메인에 걸쳐 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-131">Within an availability set, individual VMs are spread across up to 20 update domains.</span></span> <span data-ttu-id="e89e4-132">계획된 유지 관리 동안에는 단일 업데이트 도메인만 지정된 시간에 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-132">During planned maintenance, only a single update domain is impacted at any given time.</span></span> <span data-ttu-id="e89e4-133">영향을 받는 업데이트 도메인의 순서는 계획된 유지 관리 동안 순차적으로 진행되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-133">The order of update domains being impacted may not proceed sequentially during planned maintenance.</span></span> <span data-ttu-id="e89e4-134">단일 인스턴스 VM(가용성 집합의 일부가 아님)의 경우 얼마나 많은 VM이 함께 영향을 받는지 예측하거나 결정할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-134">For single instance VMs (not part of availability set), there is no way to predict or determine which and how many VMs are impacted together.</span></span>

<span data-ttu-id="e89e4-135">가상 컴퓨터 확장 집합은 동일한 VM 집합을 단일 리소스로 배포하고 관리할 수 있게 하는 Azure 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-135">Virtual machine scale sets are an Azure compute resource that enables you to deploy and manage a set of identical VMs as a single resource.</span></span>
<span data-ttu-id="e89e4-136">확장 집합은 업데이트 도메인의 형태로 가용성 집합에 유사한 보증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-136">The scale set provides similar guarantees to an availability set in the form of update domains.</span></span> 

<span data-ttu-id="e89e4-137">고가용성을 위해 가상 컴퓨터를 구성하는 방법에 대한 자세한 내용은 [*Windows 가상 컴퓨터의 가용성 관리*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e89e4-137">For more information about configuring your virtual machines for high availability, see [*Manage the availability of your Windows virtual machines*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="scheduled-events"></a><span data-ttu-id="e89e4-138">예약된 이벤트</span><span class="sxs-lookup"><span data-stu-id="e89e4-138">Scheduled Events</span></span>

<span data-ttu-id="e89e4-139">Azure Metadata Service를 사용하면 Azure에서 호스팅되는 Virtual Machine에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-139">Azure Metadata Service enables you to discover information about your Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="e89e4-140">공개된 범주 중 하나인 Scheduled Events는 예정된 이벤트(예: 다시 부팅)에 대한 정보를 나타내므로 응용 프로그램에서 이벤트를 준비하고 중단을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-140">Scheduled Events, one of the exposed categories, surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span>

<span data-ttu-id="e89e4-141">예약된 이벤트에 대한 자세한 내용은 [Azure 메타데이터 서비스 - 예약된 이벤트](../virtual-machines-scheduled-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e89e4-141">For more information about scheduled events, refer to [Azure Metadata Service - Scheduled Events](../virtual-machines-scheduled-events.md).</span></span>

## <a name="maintenance-discovery-and-notifications"></a><span data-ttu-id="e89e4-142">유지 관리 검색 및 알림</span><span class="sxs-lookup"><span data-stu-id="e89e4-142">Maintenance Discovery and Notifications</span></span>

<span data-ttu-id="e89e4-143">유지 관리 일정은 개별 VM 수준에서 고객에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-143">Maintenance schedule is visible to customers at the level of individual VMs.</span></span> <span data-ttu-id="e89e4-144">Azure Portal, API, PowerShell 또는 CLI를 사용하여 선점형 및 예약된 유지 관리 기간을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-144">You can use Azure portal, API, PowerShell, or CLI to query for the pre-emptive and scheduled maintenance windows.</span></span> <span data-ttu-id="e89e4-145">또한 프로세스 중에 하나 이상의 VM에 영향을 줄 경우 알림(전자 메일)을 받을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-145">In addition, expect to receive a notification (email) in the case where one (or more) of your VMs are impacted during the process.</span></span>

<span data-ttu-id="e89e4-146">선점형 유지 관리 및 예약된 유지 관리 단계는 모두 알림으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-146">Both pre-emptive maintenance and scheduled maintenance phases begin with a notification.</span></span> <span data-ttu-id="e89e4-147">Azure 구독당 하나의 알림을 받을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-147">Expect to receive a single notification per Azure subscription.</span></span> <span data-ttu-id="e89e4-148">알림은 기본적으로 구독의 관리자 및 공동 관리자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-148">The notification is sent to the subscription’s admin and co-admin by default.</span></span> <span data-ttu-id="e89e4-149">또한 유지 관리 알림의 대상을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-149">You can also configure the audience for the maintenance notification.</span></span>

### <a name="view-the-maintenance-window-in-the-portal"></a><span data-ttu-id="e89e4-150">포털에서 유지 관리 기간 보기</span><span class="sxs-lookup"><span data-stu-id="e89e4-150">View the Maintenance Window in the portal</span></span> 

<span data-ttu-id="e89e4-151">Azure Portal을 사용하여 유지 관리하도록 예약된 VM을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-151">You can use the Azure portal and look for VMs scheduled for maintenance.</span></span>

1.  <span data-ttu-id="e89e4-152">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-152">Sign in to the Azure portal.</span></span>

2.  <span data-ttu-id="e89e4-153">**Virtual Machines** 블레이드를 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-153">Click and open the **Virtual Machines** blade.</span></span>

3.  <span data-ttu-id="e89e4-154">**열** 단추를 클릭하여 선택할 수 있는 사용 가능한 열 목록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-154">Click the **Columns** button to open the list of available columns to choose from</span></span>

4.  <span data-ttu-id="e89e4-155">**유지 관리 기간** 열을 선택하고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-155">Select and add the **Maintenance Window** columns.</span></span> <span data-ttu-id="e89e4-156">유지 관리하도록 예약된 VM에는 유지 관리 기간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-156">VMs that are scheduled for maintenance have the maintenance windows surfaced.</span></span> <span data-ttu-id="e89e4-157">a에 대한 유지 관리가 완료되거나 중단되면 유지 관리 기간이 더 이상 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-157">Once maintenance is completed or aborted for a, the maintenance window is no longer be presented.</span></span>

### <a name="query-maintenance-details-using-the-azure-api"></a><span data-ttu-id="e89e4-158">Azure API를 사용하여 유지 관리 세부 정보 쿼리</span><span class="sxs-lookup"><span data-stu-id="e89e4-158">Query maintenance details using the Azure API</span></span>

<span data-ttu-id="e89e4-159">[VM 정보 가져오기 API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get)를 사용하여 인스턴스 보기를 찾아 개별 VM의 유지 관리 세부 사항을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-159">Use the [get VM information API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) and look for the instance view to discover the maintenance details on an individual VM.</span></span> <span data-ttu-id="e89e4-160">응답에는 다음과 같은 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-160">The response includes the following elements:</span></span>

  - <span data-ttu-id="e89e4-161">isCustomerInitiatedMaintenanceAllowed: 이제 VM에서 선점형 다시 배포를 시작할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-161">isCustomerInitiatedMaintenanceAllowed: Indicates whether you can now initiate pre-emptive redeploy on the VM.</span></span>

  - <span data-ttu-id="e89e4-162">preMaintenanceWindowStartTime: 선점형 유지 관리 기간의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-162">preMaintenanceWindowStartTime: The start time of the pre-emptive maintenance window.</span></span>

  - <span data-ttu-id="e89e4-163">preMaintenanceWindowEndTime: 선점형 유지 관리 기간의 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-163">preMaintenanceWindowEndTime: The end time of the pre-emptive maintenance window.</span></span> <span data-ttu-id="e89e4-164">이 시간 이후에는 이 VM에 대한 유지 관리를 더 이상 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-164">After this time, you will no longer be able to initiate maintenance on this VM.</span></span>
    
  - <span data-ttu-id="e89e4-165">maintenanceWindowStartTime: VM에 영향을 미칠 때 예약된 유지 관리 기간의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-165">maintenanceWindowStartTime: The start time of the scheduled maintenance window when your VM are impacted.</span></span>

  - <span data-ttu-id="e89e4-166">maintenanceWindowEndTime: 예약된 유지 관리 기간의 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-166">maintenanceWindowEndTime: The end time of the scheduled maintenance window.</span></span>
  
  - <span data-ttu-id="e89e4-167">lastOperationResultCode: 마지막 유지 관리 - 다시 배포 작업의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-167">lastOperationResultCode: The result of your last Maintenance-Redeploy operation.</span></span>
 
  - <span data-ttu-id="e89e4-168">lastOperationMessage: 마지막 유지 관리 - 다시 배포 작업의 결과를 설명하는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-168">lastOperationMessage:  Message describing the result of your last Maintenance-Redeploy operation.</span></span>

## <a name="pre-emptive-redeploy"></a><span data-ttu-id="e89e4-169">선점형 다시 배포</span><span class="sxs-lookup"><span data-stu-id="e89e4-169">Pre-emptive Redeploy</span></span>

<span data-ttu-id="e89e4-170">선점형 다시 배포 작업은 Azure에서 VM에 유지 관리가 적용되는 시간을 제어할 수 있는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-170">Pre-emptive redeploy action provides the flexibility to control the time when maintenance is applied to your VMs in Azure.</span></span> <span data-ttu-id="e89e4-171">계획된 유지 관리는 각 VM을 재부팅하는 정확한 시간을 결정할 수 있는 선점형 유지 관리 기간에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-171">Planned maintenance begins with a pre-emptive maintenance window where you can decide on the exact time for each of your VMs to be rebooted.</span></span> <span data-ttu-id="e89e4-172">이러한 기능이 유용한 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-172">The following are use cases where such a functionality is useful:</span></span>

-   <span data-ttu-id="e89e4-173">유지 관리를 최종 고객과 함께 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-173">Maintenance need to be coordinated with the end customer.</span></span>

-   <span data-ttu-id="e89e4-174">Azure에서 제공하는 예약된 유지 관리 기간이 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-174">The scheduled maintenance window offered by Azure is not sufficient.</span></span>
    <span data-ttu-id="e89e4-175">유지 관리 기간이 일주일 중 가장 바쁜 시간과 겹치거나 너무 길 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-175">It could be that the window happens to be on the busiest time of the week or it is too long.</span></span>

-   <span data-ttu-id="e89e4-176">다중 인스턴스 또는 다중 계층 응용 프로그램의 경우 두 VM 간에 충분한 시간이 필요하거나 특정 시퀀스를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-176">For multi-instance or multi-tier applications, you need sufficient time between two VMs or a certain sequence to follow.</span></span>

<span data-ttu-id="e89e4-177">VM에 대한 선점형 다시 배포를 요청하는 경우 VM을 이미 업데이트된 노드로 이동한 다음 전원을 다시 켜서 모든 구성 옵션과 관련 리소스를 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-177">When you call for pre-emptive redeploy on a VM, it moves the VM to an already updated node and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="e89e4-178">이렇게 하면 임시 디스크가 손실되고 가상 네트워크 인터페이스와 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-178">While doing so, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span>

<span data-ttu-id="e89e4-179">선점형 다시 배포는 VM당 한 번만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-179">Pre-emptive redeploy is enabled once per VM.</span></span> <span data-ttu-id="e89e4-180">프로세스 중에 오류가 발생하면 작업이 중단되고 VM은 영향을 받지 않으며 계획된 유지 관리 반복에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-180">If there is an error during the process, the operation is aborted, the VM is not impacted and it is excluded from the planned maintenance iteration.</span></span> <span data-ttu-id="e89e4-181">이후에 사용자에게 연락하여 새로운 일정을 알려주고 VM에 대한 영향을 예약하고 순서를 지정할 수 있는 새로운 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e89e4-181">You will be contacted in a later time with a new schedule and offered a new opportunity to schedule and sequence the impact on your VMs.</span></span>