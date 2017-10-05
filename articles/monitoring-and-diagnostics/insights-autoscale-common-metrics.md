---
title: "Azure Monitor 자동 크기 조정 공용 메트릭 | Microsoft Docs"
description: "클라우드 서비스, 가상 컴퓨터 및 웹앱의 자동 크기 조정에 일반적으로 사용되는 메트릭에 대해 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 240a230d09680672ccd5316470a87d047fab9fd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a><span data-ttu-id="4fc37-103">Azure Monitor 자동 크기 조정 공용 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-103">Azure Monitor autoscaling common metrics</span></span>
<span data-ttu-id="4fc37-104">Azure Monitor 자동 크기 조정을 사용하여 원격 분석 데이터(메트릭)에 따라 실행 중인 인스턴트 수를 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-104">Azure Monitor autoscaling allows you to scale the number of running instances up or down, based on telemetry data (metrics).</span></span> <span data-ttu-id="4fc37-105">이 문서에서는 사용하고자 하는 공용 메트릭에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-105">This document describes common metrics that you might want to use.</span></span> <span data-ttu-id="4fc37-106">Cloud Services 및 서버 팜용 Azure Portal에서 크기를 조정할 리소스의 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-106">In the Azure portal  for Cloud Services and Server Farms, you can choose the metric of the resource to scale by.</span></span> <span data-ttu-id="4fc37-107">그러나 크기를 조정하기 위해 여러 리소스에서 임의 메트릭을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-107">However, you can also choose any metric from a different resource to scale by.</span></span>

<span data-ttu-id="4fc37-108">Azure Monitor 자동 크기 조정은 [가상 컴퓨터 확장 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/) 및 [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/)에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-108">Azure Monitor autoscale applies only to [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="4fc37-109">다른 Azure 서비스에는 다른 크기 조정 방법이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-109">Other Azure services use different scaling methods.</span></span>

## <a name="compute-metrics-for-resource-manager-based-vms"></a><span data-ttu-id="4fc37-110">Resource Manager 기반 VM용 메트릭 계산</span><span class="sxs-lookup"><span data-stu-id="4fc37-110">Compute metrics for Resource Manager-based VMs</span></span>
<span data-ttu-id="4fc37-111">기본적으로 Resource Manager 기반 Virtual Machines 및 Virtual Machine Scale Sets는 기본(호스트 수준) 메트릭을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-111">By default, Resource Manager-based Virtual Machines and Virtual Machine Scale Sets emit basic (host-level) metrics.</span></span> <span data-ttu-id="4fc37-112">또한 Azure VM 및 VMSS용 진단 데이터 수집을 구성하면 Azure 진단 확장은 게스트 OS 성능 카운터(일반적으로 "게스트 OS 메트릭"이라고 함)도 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-112">In addition, when you configure diagnostics data collection for an Azure VM and VMSS,  the Azure diagnostic extension also emits guest-OS performance counters (commonly known as "guest-OS metrics").</span></span>  <span data-ttu-id="4fc37-113">자동 크기 조정 규칙에서 이러한 모든 메트릭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-113">You use all these metrics in autoscale rules.</span></span>

<span data-ttu-id="4fc37-114">`Get MetricDefinitions` API/PoSH/CLI를 사용하여 VMSS 리소스에 사용할 수 있는 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-114">You can use the `Get MetricDefinitions` API/PoSH/CLI to view the metrics available for your VMSS resource.</span></span>

<span data-ttu-id="4fc37-115">VM 규모 집합을 사용 중인데 특정 메트릭이 목록에 표시되지 않는 경우, 이는 진단 확장에서 *사용하지 않도록 설정*되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-115">If you're using VM scale sets and you don't see a particular metric listed, then it is likely *disabled* in your diagnostics extension.</span></span>

<span data-ttu-id="4fc37-116">특정 메트릭이 원하는 빈도로 샘플링 또는 전송되고 있지 않은 경우 진단 구성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-116">If a particular metric is not being sampled or transferred at the frequency you want, you can update the diagnostics configuration.</span></span>

<span data-ttu-id="4fc37-117">위 경우 중 하나가 해당되면 PowerShell에 대한 [PowerShell을 사용하여 Windows를 실행하는 가상 컴퓨터에서 Azure 진단을 사용하도록 설정](../virtual-machines/windows/ps-extensions-diagnostics.md)을 검토하여 메트릭을 사용하도록 Azure VM 진단 확장을 구성 및 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-117">If either preceding case is true, then review [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) about PowerShell to configure and update your Azure VM Diagnostics extension to enable the metric.</span></span> <span data-ttu-id="4fc37-118">이 문서에는 샘플 진단 구성 파일도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-118">That article also includes a sample diagnostics configuration file.</span></span>

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a><span data-ttu-id="4fc37-119">Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-119">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>
<span data-ttu-id="4fc37-120">기본적으로 Windows 및 Linux 인스턴스 모두 Azure VM 및 VMSS용으로 다음 호스트 수준 메트릭을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-120">The following host-level metrics are emitted by default for Azure VM and VMSS in both Windows and Linux instances.</span></span> <span data-ttu-id="4fc37-121">이러한 메트릭은 Azure VM을 설명하지만 게스트 VM에 설치된 에이전트를 통하는 대신 Azure VM 호스트에서 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-121">These metrics describe your Azure VM, but are collected from the Azure VM host rather than via agent installed on the guest VM.</span></span> <span data-ttu-id="4fc37-122">자동 크기 조정 규칙에서 이러한 메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-122">You may use these metrics in autoscaling rules.</span></span>

- [<span data-ttu-id="4fc37-123">Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-123">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [<span data-ttu-id="4fc37-124">Resource Manager 기반 Windows 및 Linux VM Scale Sets용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-124">Host metrics for Resource Manager-based Windows and Linux VM Scale Sets</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a><span data-ttu-id="4fc37-125">게스트 OS 메트릭 Resource Manager 기반 Windows VM</span><span class="sxs-lookup"><span data-stu-id="4fc37-125">Guest OS metrics Resource Manager-based Windows VMs</span></span>
<span data-ttu-id="4fc37-126">Azure에서 VM을 만들 때 진단 확장을 사용하여 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-126">When you create a VM in Azure, diagnostics is enabled by using the Diagnostics extension.</span></span> <span data-ttu-id="4fc37-127">진단 확장을 사용하여 VM 내에서 가져온 메트릭 집합을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-127">The diagnostics extension emits a set of metrics taken from inside of the VM.</span></span> <span data-ttu-id="4fc37-128">즉, 기본적으로 내보내지 않도록 메트릭의 자동 크기 조정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-128">This means you can autoscale off of metrics that are not emitted by default.</span></span>

<span data-ttu-id="4fc37-129">PowerShell에서 다음 명령을 사용하여 메트릭 목록을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-129">You can generate a list of the metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="4fc37-130">다음 메트릭에 대한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-130">You can create an alert for the following metrics:</span></span>

| <span data-ttu-id="4fc37-131">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="4fc37-131">Metric Name</span></span> | <span data-ttu-id="4fc37-132">단위</span><span class="sxs-lookup"><span data-stu-id="4fc37-132">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="4fc37-133">\Processor(_Total)\% 프로세서 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-133">\Processor(_Total)\% Processor Time</span></span> |<span data-ttu-id="4fc37-134">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-134">Percent</span></span> |
| <span data-ttu-id="4fc37-135">\Processor(_Total)\% 시스템 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-135">\Processor(_Total)\% Privileged Time</span></span> |<span data-ttu-id="4fc37-136">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-136">Percent</span></span> |
| <span data-ttu-id="4fc37-137">\Processor(_Total)\% 사용자 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-137">\Processor(_Total)\% User Time</span></span> |<span data-ttu-id="4fc37-138">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-138">Percent</span></span> |
| <span data-ttu-id="4fc37-139">\Processor Information(_Total)\Processor Frequency</span><span class="sxs-lookup"><span data-stu-id="4fc37-139">\Processor Information(_Total)\Processor Frequency</span></span> |<span data-ttu-id="4fc37-140">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-140">Count</span></span> |
| <span data-ttu-id="4fc37-141">\System\Processes</span><span class="sxs-lookup"><span data-stu-id="4fc37-141">\System\Processes</span></span> |<span data-ttu-id="4fc37-142">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-142">Count</span></span> |
| <span data-ttu-id="4fc37-143">\Process(_Total)\Thread Count</span><span class="sxs-lookup"><span data-stu-id="4fc37-143">\Process(_Total)\Thread Count</span></span> |<span data-ttu-id="4fc37-144">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-144">Count</span></span> |
| <span data-ttu-id="4fc37-145">\Process(_Total)\Handle Count</span><span class="sxs-lookup"><span data-stu-id="4fc37-145">\Process(_Total)\Handle Count</span></span> |<span data-ttu-id="4fc37-146">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-146">Count</span></span> |
| <span data-ttu-id="4fc37-147">\Memory\% 사용 중인 커밋된 바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-147">\Memory\% Committed Bytes In Use</span></span> |<span data-ttu-id="4fc37-148">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-148">Percent</span></span> |
| <span data-ttu-id="4fc37-149">\Memory\Available Bytes</span><span class="sxs-lookup"><span data-stu-id="4fc37-149">\Memory\Available Bytes</span></span> |<span data-ttu-id="4fc37-150">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-150">Bytes</span></span> |
| <span data-ttu-id="4fc37-151">\Memory\Committed Bytes</span><span class="sxs-lookup"><span data-stu-id="4fc37-151">\Memory\Committed Bytes</span></span> |<span data-ttu-id="4fc37-152">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-152">Bytes</span></span> |
| <span data-ttu-id="4fc37-153">\Memory\Commit Limit</span><span class="sxs-lookup"><span data-stu-id="4fc37-153">\Memory\Commit Limit</span></span> |<span data-ttu-id="4fc37-154">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-154">Bytes</span></span> |
| <span data-ttu-id="4fc37-155">\Memory\Pool Paged Bytes</span><span class="sxs-lookup"><span data-stu-id="4fc37-155">\Memory\Pool Paged Bytes</span></span> |<span data-ttu-id="4fc37-156">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-156">Bytes</span></span> |
| <span data-ttu-id="4fc37-157">\Memory\Pool Nonpaged Bytes</span><span class="sxs-lookup"><span data-stu-id="4fc37-157">\Memory\Pool Nonpaged Bytes</span></span> |<span data-ttu-id="4fc37-158">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-158">Bytes</span></span> |
| <span data-ttu-id="4fc37-159">\PhysicalDisk(_Total)\% 디스크 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-159">\PhysicalDisk(_Total)\% Disk Time</span></span> |<span data-ttu-id="4fc37-160">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-160">Percent</span></span> |
| <span data-ttu-id="4fc37-161">\PhysicalDisk(_Total)\% 디스크 읽기 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-161">\PhysicalDisk(_Total)\% Disk Read Time</span></span> |<span data-ttu-id="4fc37-162">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-162">Percent</span></span> |
| <span data-ttu-id="4fc37-163">\PhysicalDisk(_Total)\% 디스크 쓰기 시간</span><span class="sxs-lookup"><span data-stu-id="4fc37-163">\PhysicalDisk(_Total)\% Disk Write Time</span></span> |<span data-ttu-id="4fc37-164">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-164">Percent</span></span> |
| <span data-ttu-id="4fc37-165">\PhysicalDisk(_Total)\디스크 전송/초</span><span class="sxs-lookup"><span data-stu-id="4fc37-165">\PhysicalDisk(_Total)\Disk Transfers/sec</span></span> |<span data-ttu-id="4fc37-166">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-166">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-167">\PhysicalDisk(_Total)\Disk Reads/sec</span><span class="sxs-lookup"><span data-stu-id="4fc37-167">\PhysicalDisk(_Total)\Disk Reads/sec</span></span> |<span data-ttu-id="4fc37-168">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-168">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-169">\PhysicalDisk(_Total)\Disk Writes/sec</span><span class="sxs-lookup"><span data-stu-id="4fc37-169">\PhysicalDisk(_Total)\Disk Writes/sec</span></span> |<span data-ttu-id="4fc37-170">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-170">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="4fc37-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span></span> |<span data-ttu-id="4fc37-172">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-172">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="4fc37-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span></span> |<span data-ttu-id="4fc37-174">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-174">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="4fc37-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span></span> |<span data-ttu-id="4fc37-176">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-176">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-177">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="4fc37-177">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="4fc37-178">디스크 큐 길이</span><span class="sxs-lookup"><span data-stu-id="4fc37-178">Disk Queue Length</span></span> |<span data-ttu-id="4fc37-179">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-179">Count</span></span> |
| <span data-ttu-id="4fc37-180">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="4fc37-180">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="4fc37-181">디스크 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="4fc37-181">Disk Read Queue Length</span></span> |<span data-ttu-id="4fc37-182">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-182">Count</span></span> |
| <span data-ttu-id="4fc37-183">\PhysicalDisk(_Total)\Avg.</span><span class="sxs-lookup"><span data-stu-id="4fc37-183">\PhysicalDisk(_Total)\Avg.</span></span> <span data-ttu-id="4fc37-184">디스크 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="4fc37-184">Disk Write Queue Length</span></span> |<span data-ttu-id="4fc37-185">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-185">Count</span></span> |
| <span data-ttu-id="4fc37-186">\LogicalDisk(_Total)\% 사용 가능한 공간</span><span class="sxs-lookup"><span data-stu-id="4fc37-186">\LogicalDisk(_Total)\% Free Space</span></span> |<span data-ttu-id="4fc37-187">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-187">Percent</span></span> |
| <span data-ttu-id="4fc37-188">\LogicalDisk(_Total)\Free Megabytes</span><span class="sxs-lookup"><span data-stu-id="4fc37-188">\LogicalDisk(_Total)\Free Megabytes</span></span> |<span data-ttu-id="4fc37-189">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-189">Count</span></span> |

### <a name="guest-os-metrics-linux-vms"></a><span data-ttu-id="4fc37-190">게스트 OS 메트릭 Linux VM</span><span class="sxs-lookup"><span data-stu-id="4fc37-190">Guest OS metrics Linux VMs</span></span>
<span data-ttu-id="4fc37-191">Azure에서 VM을 만들 때 진단 확장을 사용하여 기본적으로 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-191">When you create a VM in Azure, diagnostics is enabled by default by using Diagnostics extension.</span></span>

<span data-ttu-id="4fc37-192">PowerShell에서 다음 명령을 사용하여 메트릭 목록을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-192">You can generate a list of the metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 <span data-ttu-id="4fc37-193">다음 메트릭에 대한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-193">You can create an alert for the following metrics:</span></span>

| <span data-ttu-id="4fc37-194">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="4fc37-194">Metric Name</span></span> | <span data-ttu-id="4fc37-195">단위</span><span class="sxs-lookup"><span data-stu-id="4fc37-195">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="4fc37-196">\Memory\AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4fc37-196">\Memory\AvailableMemory</span></span> |<span data-ttu-id="4fc37-197">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-197">Bytes</span></span> |
| <span data-ttu-id="4fc37-198">\Memory\PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="4fc37-198">\Memory\PercentAvailableMemory</span></span> |<span data-ttu-id="4fc37-199">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-199">Percent</span></span> |
| <span data-ttu-id="4fc37-200">\Memory\UsedMemory</span><span class="sxs-lookup"><span data-stu-id="4fc37-200">\Memory\UsedMemory</span></span> |<span data-ttu-id="4fc37-201">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-201">Bytes</span></span> |
| <span data-ttu-id="4fc37-202">\Memory\PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="4fc37-202">\Memory\PercentUsedMemory</span></span> |<span data-ttu-id="4fc37-203">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-203">Percent</span></span> |
| <span data-ttu-id="4fc37-204">\Memory\PercentUsedByCache</span><span class="sxs-lookup"><span data-stu-id="4fc37-204">\Memory\PercentUsedByCache</span></span> |<span data-ttu-id="4fc37-205">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-205">Percent</span></span> |
| <span data-ttu-id="4fc37-206">\Memory\PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="4fc37-206">\Memory\PagesPerSec</span></span> |<span data-ttu-id="4fc37-207">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-207">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-208">\Memory\PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="4fc37-208">\Memory\PagesReadPerSec</span></span> |<span data-ttu-id="4fc37-209">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-209">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-210">\Memory\PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="4fc37-210">\Memory\PagesWrittenPerSec</span></span> |<span data-ttu-id="4fc37-211">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-211">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-212">\Memory\AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4fc37-212">\Memory\AvailableSwap</span></span> |<span data-ttu-id="4fc37-213">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-213">Bytes</span></span> |
| <span data-ttu-id="4fc37-214">\Memory\PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="4fc37-214">\Memory\PercentAvailableSwap</span></span> |<span data-ttu-id="4fc37-215">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-215">Percent</span></span> |
| <span data-ttu-id="4fc37-216">\Memory\UsedSwap</span><span class="sxs-lookup"><span data-stu-id="4fc37-216">\Memory\UsedSwap</span></span> |<span data-ttu-id="4fc37-217">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-217">Bytes</span></span> |
| <span data-ttu-id="4fc37-218">\Memory\PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="4fc37-218">\Memory\PercentUsedSwap</span></span> |<span data-ttu-id="4fc37-219">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-219">Percent</span></span> |
| <span data-ttu-id="4fc37-220">\Processor\PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-220">\Processor\PercentIdleTime</span></span> |<span data-ttu-id="4fc37-221">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-221">Percent</span></span> |
| <span data-ttu-id="4fc37-222">\Processor\PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-222">\Processor\PercentUserTime</span></span> |<span data-ttu-id="4fc37-223">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-223">Percent</span></span> |
| <span data-ttu-id="4fc37-224">\Processor\PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-224">\Processor\PercentNiceTime</span></span> |<span data-ttu-id="4fc37-225">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-225">Percent</span></span> |
| <span data-ttu-id="4fc37-226">\Processor\PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-226">\Processor\PercentPrivilegedTime</span></span> |<span data-ttu-id="4fc37-227">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-227">Percent</span></span> |
| <span data-ttu-id="4fc37-228">\Processor\PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-228">\Processor\PercentInterruptTime</span></span> |<span data-ttu-id="4fc37-229">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-229">Percent</span></span> |
| <span data-ttu-id="4fc37-230">\Processor\PercentDPCTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-230">\Processor\PercentDPCTime</span></span> |<span data-ttu-id="4fc37-231">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-231">Percent</span></span> |
| <span data-ttu-id="4fc37-232">\Processor\PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-232">\Processor\PercentProcessorTime</span></span> |<span data-ttu-id="4fc37-233">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-233">Percent</span></span> |
| <span data-ttu-id="4fc37-234">\Processor\PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-234">\Processor\PercentIOWaitTime</span></span> |<span data-ttu-id="4fc37-235">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-235">Percent</span></span> |
| <span data-ttu-id="4fc37-236">\PhysicalDisk\BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-236">\PhysicalDisk\BytesPerSecond</span></span> |<span data-ttu-id="4fc37-237">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-237">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-238">\PhysicalDisk\ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-238">\PhysicalDisk\ReadBytesPerSecond</span></span> |<span data-ttu-id="4fc37-239">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-239">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-240">\PhysicalDisk\WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-240">\PhysicalDisk\WriteBytesPerSecond</span></span> |<span data-ttu-id="4fc37-241">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="4fc37-241">BytesPerSecond</span></span> |
| <span data-ttu-id="4fc37-242">\PhysicalDisk\TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-242">\PhysicalDisk\TransfersPerSecond</span></span> |<span data-ttu-id="4fc37-243">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-243">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-244">\PhysicalDisk\ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-244">\PhysicalDisk\ReadsPerSecond</span></span> |<span data-ttu-id="4fc37-245">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-245">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-246">\PhysicalDisk\WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="4fc37-246">\PhysicalDisk\WritesPerSecond</span></span> |<span data-ttu-id="4fc37-247">초당 개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-247">CountPerSecond</span></span> |
| <span data-ttu-id="4fc37-248">\PhysicalDisk\AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-248">\PhysicalDisk\AverageReadTime</span></span> |<span data-ttu-id="4fc37-249">초</span><span class="sxs-lookup"><span data-stu-id="4fc37-249">Seconds</span></span> |
| <span data-ttu-id="4fc37-250">\PhysicalDisk\AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-250">\PhysicalDisk\AverageWriteTime</span></span> |<span data-ttu-id="4fc37-251">초</span><span class="sxs-lookup"><span data-stu-id="4fc37-251">Seconds</span></span> |
| <span data-ttu-id="4fc37-252">\PhysicalDisk\AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="4fc37-252">\PhysicalDisk\AverageTransferTime</span></span> |<span data-ttu-id="4fc37-253">초</span><span class="sxs-lookup"><span data-stu-id="4fc37-253">Seconds</span></span> |
| <span data-ttu-id="4fc37-254">\PhysicalDisk\AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="4fc37-254">\PhysicalDisk\AverageDiskQueueLength</span></span> |<span data-ttu-id="4fc37-255">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-255">Count</span></span> |
| <span data-ttu-id="4fc37-256">\NetworkInterface\BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="4fc37-256">\NetworkInterface\BytesTransmitted</span></span> |<span data-ttu-id="4fc37-257">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-257">Bytes</span></span> |
| <span data-ttu-id="4fc37-258">\NetworkInterface\BytesReceived</span><span class="sxs-lookup"><span data-stu-id="4fc37-258">\NetworkInterface\BytesReceived</span></span> |<span data-ttu-id="4fc37-259">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-259">Bytes</span></span> |
| <span data-ttu-id="4fc37-260">\NetworkInterface\PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="4fc37-260">\NetworkInterface\PacketsTransmitted</span></span> |<span data-ttu-id="4fc37-261">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-261">Count</span></span> |
| <span data-ttu-id="4fc37-262">\NetworkInterface\PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="4fc37-262">\NetworkInterface\PacketsReceived</span></span> |<span data-ttu-id="4fc37-263">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-263">Count</span></span> |
| <span data-ttu-id="4fc37-264">\NetworkInterface\BytesTotal</span><span class="sxs-lookup"><span data-stu-id="4fc37-264">\NetworkInterface\BytesTotal</span></span> |<span data-ttu-id="4fc37-265">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-265">Bytes</span></span> |
| <span data-ttu-id="4fc37-266">\NetworkInterface\TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="4fc37-266">\NetworkInterface\TotalRxErrors</span></span> |<span data-ttu-id="4fc37-267">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-267">Count</span></span> |
| <span data-ttu-id="4fc37-268">\NetworkInterface\TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="4fc37-268">\NetworkInterface\TotalTxErrors</span></span> |<span data-ttu-id="4fc37-269">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-269">Count</span></span> |
| <span data-ttu-id="4fc37-270">\NetworkInterface\TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="4fc37-270">\NetworkInterface\TotalCollisions</span></span> |<span data-ttu-id="4fc37-271">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-271">Count</span></span> |

## <a name="commonly-used-web-server-farm-metrics"></a><span data-ttu-id="4fc37-272">일반적으로 사용되는 웹(서버 팜) 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-272">Commonly used Web (Server Farm) metrics</span></span>
<span data-ttu-id="4fc37-273">Http 큐 길이와 같이 공용 웹 서버 메트릭을 기반으로 자동 크기 조정을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-273">You can also perform autoscale based on common web server metrics such as the Http queue length.</span></span> <span data-ttu-id="4fc37-274">메트릭 이름은 **HttpQueueLength**입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-274">It's metric name is **HttpQueueLength**.</span></span>  <span data-ttu-id="4fc37-275">다음 섹션에는 사용 가능한 서버 팜(웹앱) 메트릭이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-275">The following section lists available server farm (Web Apps) metrics.</span></span>

### <a name="web-apps-metrics"></a><span data-ttu-id="4fc37-276">웹앱 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-276">Web Apps metrics</span></span>
<span data-ttu-id="4fc37-277">PowerShell에서 다음 명령을 사용하여 웹앱 메트릭 목록을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-277">You can generate a list of the Web Apps metrics by using the following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="4fc37-278">다음 메트릭에 대한 경고를 만들거나 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-278">You can alert on or scale by these metrics.</span></span>

| <span data-ttu-id="4fc37-279">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="4fc37-279">Metric Name</span></span> | <span data-ttu-id="4fc37-280">단위</span><span class="sxs-lookup"><span data-stu-id="4fc37-280">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="4fc37-281">CpuPercentage</span><span class="sxs-lookup"><span data-stu-id="4fc37-281">CpuPercentage</span></span> |<span data-ttu-id="4fc37-282">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-282">Percent</span></span> |
| <span data-ttu-id="4fc37-283">MemoryPercentage</span><span class="sxs-lookup"><span data-stu-id="4fc37-283">MemoryPercentage</span></span> |<span data-ttu-id="4fc37-284">백분율</span><span class="sxs-lookup"><span data-stu-id="4fc37-284">Percent</span></span> |
| <span data-ttu-id="4fc37-285">DiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="4fc37-285">DiskQueueLength</span></span> |<span data-ttu-id="4fc37-286">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-286">Count</span></span> |
| <span data-ttu-id="4fc37-287">HttpQueueLength</span><span class="sxs-lookup"><span data-stu-id="4fc37-287">HttpQueueLength</span></span> |<span data-ttu-id="4fc37-288">개수</span><span class="sxs-lookup"><span data-stu-id="4fc37-288">Count</span></span> |
| <span data-ttu-id="4fc37-289">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="4fc37-289">BytesReceived</span></span> |<span data-ttu-id="4fc37-290">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-290">Bytes</span></span> |
| <span data-ttu-id="4fc37-291">BytesSent</span><span class="sxs-lookup"><span data-stu-id="4fc37-291">BytesSent</span></span> |<span data-ttu-id="4fc37-292">바이트</span><span class="sxs-lookup"><span data-stu-id="4fc37-292">Bytes</span></span> |

## <a name="commonly-used-storage-metrics"></a><span data-ttu-id="4fc37-293">일반적으로 사용되는 저장소 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-293">Commonly used Storage metrics</span></span>
<span data-ttu-id="4fc37-294">저장소 큐의 메시지 수인 저장소 큐 길이의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-294">You can scale by Storage queue length, which is the number of messages in the storage queue.</span></span> <span data-ttu-id="4fc37-295">저장소 큐 길이는 특수한 메트릭이고 임계값은 인스턴스당 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-295">Storage queue length is a special metric and the threshold is the number of messages per instance.</span></span> <span data-ttu-id="4fc37-296">예를 들어 인스턴스가 두 개이고 임계값이 100으로 설정된 경우 큐에서 총 메시지 수가 200일 때 크기가 조정됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-296">For example, if there are two instances and if the threshold is set to 100, scaling occurs when the total number of messages in the queue is 200.</span></span> <span data-ttu-id="4fc37-297">인스턴스당 메시지는 100개, 120개 및 80개, 또는 최대 200개 이상을 추가하는 임의의 기타 조합이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-297">That can be 100 messages per instance, 120 and 80, or any other combination that adds up to 200 or more.</span></span>

<span data-ttu-id="4fc37-298">Azure Portal의 **설정** 블레이드에서 이 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-298">Configure this setting in the Azure portal in the **Settings** blade.</span></span> <span data-ttu-id="4fc37-299">VM Scale Sets의 경우 *metricName*을 *ApproximateMessageCount*로 사용하고 저장소 큐 ID를 *metricResourceUri*로 전달하도록 Resource Manager 템플릿에서 자동 크기 조정 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-299">For VM scale sets, you can update the Autoscale setting in the Resource Manager template to use *metricName* as *ApproximateMessageCount* and pass the ID of the storage queue as *metricResourceUri*.</span></span>

<span data-ttu-id="4fc37-300">예를 들어 클래식 저장소 계정을 사용하면 자동 크기 조정 설정 metricTrigger는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-300">For example, with a Classic Storage Account the autoscale setting metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

<span data-ttu-id="4fc37-301">(클래식이 아닌) 저장소 계정의 경우 metricTrigger는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-301">For a (non-classic) storage account, the metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a><span data-ttu-id="4fc37-302">자주 사용되는 서비스 버스 메트릭</span><span class="sxs-lookup"><span data-stu-id="4fc37-302">Commonly used Service Bus metrics</span></span>
<span data-ttu-id="4fc37-303">서비스 버스 큐의 메시지 수인 서비스 버스 큐 길이의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-303">You can scale by Service Bus queue length, which is the number of messages in the Service Bus queue.</span></span> <span data-ttu-id="4fc37-304">Service Bus 큐 길이는 특수한 메트릭이고 임계값은 인스턴스당 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-304">Service Bus queue length is a special metric and the threshold is the number of messages per instance.</span></span> <span data-ttu-id="4fc37-305">예를 들어 인스턴스가 두 개이고 임계값이 100으로 설정된 경우 큐에서 총 메시지 수가 200일 때 크기가 조정됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-305">For example, if there are two instances and if the threshold is set to 100, scaling occurs when the total number of messages in the queue is 200.</span></span> <span data-ttu-id="4fc37-306">인스턴스당 메시지는 100개, 120개 및 80개, 또는 최대 200개 이상을 추가하는 임의의 기타 조합이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-306">That can be 100 messages per instance, 120 and 80, or any other combination that adds up to 200 or more.</span></span>

<span data-ttu-id="4fc37-307">VM Scale Sets의 경우 *metricName*을 *ApproximateMessageCount*로 사용하고 저장소 큐 ID를 *metricResourceUri*로 전달하도록 Resource Manager 템플릿에서 자동 크기 조정 설정을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-307">For VM scale sets, you can update the Autoscale setting in the Resource Manager template to use *metricName* as *ApproximateMessageCount* and pass the ID of the storage queue as *metricResourceUri*.</span></span>

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> <span data-ttu-id="4fc37-308">서비스 버스의 경우 리소스 그룹 개념이 없지만 Azure Resource Manager가 지역마다 기본 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-308">For Service Bus, the resource group concept does not exist but Azure Resource Manager creates a default resource group per region.</span></span> <span data-ttu-id="4fc37-309">리소스 그룹은 일반적으로 'Default-ServiceBus-[region]' 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-309">The resource group is usually in the 'Default-ServiceBus-[region]' format.</span></span> <span data-ttu-id="4fc37-310">예를 들어 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' 등입니다.</span><span class="sxs-lookup"><span data-stu-id="4fc37-310">For example, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.</span></span>
>
>
