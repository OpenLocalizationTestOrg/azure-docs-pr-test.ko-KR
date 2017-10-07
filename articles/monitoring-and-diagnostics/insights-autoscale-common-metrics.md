---
title: "모니터 자동 크기 조정에 대 한 일반 메트릭 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a><span data-ttu-id="abb4a-103">Azure Monitor 자동 크기 조정 공용 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-103">Azure Monitor autoscaling common metrics</span></span>
<span data-ttu-id="abb4a-104">Azure 모니터의 자동 크기 조정이 있습니다 tooscale hello 실행 중인 인스턴스 수를를 위 또는 아래로 원격 분석 데이터 (메트릭)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-104">Azure Monitor autoscaling allows you tooscale hello number of running instances up or down, based on telemetry data (metrics).</span></span> <span data-ttu-id="abb4a-105">이 문서에서는 공통 메트릭을 toouse 알았으므로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-105">This document describes common metrics that you might want toouse.</span></span> <span data-ttu-id="abb4a-106">Azure 포털 클라우드 서비스 및 서버 팜 hello에 하 여 hello 리소스 tooscale의 hello 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-106">In hello Azure portal  for Cloud Services and Server Farms, you can choose hello metric of hello resource tooscale by.</span></span> <span data-ttu-id="abb4a-107">그러나 하 여 다른 리소스 tooscale에서 모든 메트릭을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-107">However, you can also choose any metric from a different resource tooscale by.</span></span>

<span data-ttu-id="abb4a-108">Azure 모니터의 자동 크기 조정 적용만 너무[가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-108">Azure Monitor autoscale applies only too[Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="abb4a-109">다른 Azure 서비스에는 다른 크기 조정 방법이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-109">Other Azure services use different scaling methods.</span></span>

## <a name="compute-metrics-for-resource-manager-based-vms"></a><span data-ttu-id="abb4a-110">Resource Manager 기반 VM용 메트릭 계산</span><span class="sxs-lookup"><span data-stu-id="abb4a-110">Compute metrics for Resource Manager-based VMs</span></span>
<span data-ttu-id="abb4a-111">기본적으로 Resource Manager 기반 Virtual Machines 및 Virtual Machine Scale Sets는 기본(호스트 수준) 메트릭을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-111">By default, Resource Manager-based Virtual Machines and Virtual Machine Scale Sets emit basic (host-level) metrics.</span></span> <span data-ttu-id="abb4a-112">또한 Azure VM 및 VMSS에 대 한 진단 데이터 수집을 구성한 경우 Azure 진단 확장 hello 게스트 OS 성능 카운터를 (일반적으로 "게스트 OS 메트릭" 라고 함)도 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-112">In addition, when you configure diagnostics data collection for an Azure VM and VMSS,  hello Azure diagnostic extension also emits guest-OS performance counters (commonly known as "guest-OS metrics").</span></span>  <span data-ttu-id="abb4a-113">자동 크기 조정 규칙에서 이러한 모든 메트릭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-113">You use all these metrics in autoscale rules.</span></span>

<span data-ttu-id="abb4a-114">Hello를 사용할 수 있습니다 `Get MetricDefinitions` CLI PoSH/API/tooview hello 메트릭을 VMSS 리소스에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-114">You can use hello `Get MetricDefinitions` API/PoSH/CLI tooview hello metrics available for your VMSS resource.</span></span>

<span data-ttu-id="abb4a-115">VM 규모 집합을 사용 중인데 특정 메트릭이 목록에 표시되지 않는 경우, 이는 진단 확장에서 *사용하지 않도록 설정*되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-115">If you're using VM scale sets and you don't see a particular metric listed, then it is likely *disabled* in your diagnostics extension.</span></span>

<span data-ttu-id="abb4a-116">특정 메트릭에 샘플링 또는에서 전송 된 hello 빈도 되 고 있지 않습니다, hello 진단 구성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-116">If a particular metric is not being sampled or transferred at hello frequency you want, you can update hello diagnostics configuration.</span></span>

<span data-ttu-id="abb4a-117">위의 두 경우 모두 true 이면 다음 검토 [Windows를 실행 하는 가상 컴퓨터에서 PowerShell 사용 하 여 tooenable Azure 진단](../virtual-machines/windows/ps-extensions-diagnostics.md) PowerShell tooconfigure 및 업데이트에 대 한 Azure VM 진단 확장 tooenable hello 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-117">If either preceding case is true, then review [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) about PowerShell tooconfigure and update your Azure VM Diagnostics extension tooenable hello metric.</span></span> <span data-ttu-id="abb4a-118">이 문서에는 샘플 진단 구성 파일도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-118">That article also includes a sample diagnostics configuration file.</span></span>

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a><span data-ttu-id="abb4a-119">Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-119">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>
<span data-ttu-id="abb4a-120">다음 호스트 수준 메트릭 hello는 Windows와 Linux의 경우에서 Azure VM 및 VMSS 기본적으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-120">hello following host-level metrics are emitted by default for Azure VM and VMSS in both Windows and Linux instances.</span></span> <span data-ttu-id="abb4a-121">이러한 메트릭은 Azure VM에 설명 하지만 hello 게스트 VM에 설치 된 에이전트를 통해 대신 hello Azure VM 호스트에서 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-121">These metrics describe your Azure VM, but are collected from hello Azure VM host rather than via agent installed on hello guest VM.</span></span> <span data-ttu-id="abb4a-122">자동 크기 조정 규칙에서 이러한 메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-122">You may use these metrics in autoscaling rules.</span></span>

- [<span data-ttu-id="abb4a-123">Resource Manager 기반 Windows 및 Linux VM용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-123">Host metrics for Resource Manager-based Windows and Linux VMs</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [<span data-ttu-id="abb4a-124">Resource Manager 기반 Windows 및 Linux VM Scale Sets용 호스트 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-124">Host metrics for Resource Manager-based Windows and Linux VM Scale Sets</span></span>](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a><span data-ttu-id="abb4a-125">게스트 OS 메트릭 Resource Manager 기반 Windows VM</span><span class="sxs-lookup"><span data-stu-id="abb4a-125">Guest OS metrics Resource Manager-based Windows VMs</span></span>
<span data-ttu-id="abb4a-126">Azure에서 VM을 만들 진단 hello 진단 확장을 사용 하 여 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-126">When you create a VM in Azure, diagnostics is enabled by using hello Diagnostics extension.</span></span> <span data-ttu-id="abb4a-127">hello 진단 확장 hello VM 내부에서 가져온 메트릭 집합을을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-127">hello diagnostics extension emits a set of metrics taken from inside of hello VM.</span></span> <span data-ttu-id="abb4a-128">즉, 기본적으로 내보내지 않도록 메트릭의 자동 크기 조정을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-128">This means you can autoscale off of metrics that are not emitted by default.</span></span>

<span data-ttu-id="abb4a-129">다음 powershell에서 명령을 hello를 사용 하 여 hello 메트릭 목록은 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-129">You can generate a list of hello metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="abb4a-130">다음 메트릭 hello에 대 한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-130">You can create an alert for hello following metrics:</span></span>

| <span data-ttu-id="abb4a-131">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="abb4a-131">Metric Name</span></span> | <span data-ttu-id="abb4a-132">단위</span><span class="sxs-lookup"><span data-stu-id="abb4a-132">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="abb4a-133">\Processor(_Total)\% 프로세서 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-133">\Processor(_Total)\% Processor Time</span></span> |<span data-ttu-id="abb4a-134">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-134">Percent</span></span> |
| <span data-ttu-id="abb4a-135">\Processor(_Total)\% 시스템 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-135">\Processor(_Total)\% Privileged Time</span></span> |<span data-ttu-id="abb4a-136">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-136">Percent</span></span> |
| <span data-ttu-id="abb4a-137">\Processor(_Total)\% 사용자 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-137">\Processor(_Total)\% User Time</span></span> |<span data-ttu-id="abb4a-138">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-138">Percent</span></span> |
| <span data-ttu-id="abb4a-139">\Processor Information(_Total)\Processor Frequency</span><span class="sxs-lookup"><span data-stu-id="abb4a-139">\Processor Information(_Total)\Processor Frequency</span></span> |<span data-ttu-id="abb4a-140">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-140">Count</span></span> |
| <span data-ttu-id="abb4a-141">\System\Processes</span><span class="sxs-lookup"><span data-stu-id="abb4a-141">\System\Processes</span></span> |<span data-ttu-id="abb4a-142">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-142">Count</span></span> |
| <span data-ttu-id="abb4a-143">\Process(_Total)\Thread Count</span><span class="sxs-lookup"><span data-stu-id="abb4a-143">\Process(_Total)\Thread Count</span></span> |<span data-ttu-id="abb4a-144">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-144">Count</span></span> |
| <span data-ttu-id="abb4a-145">\Process(_Total)\Handle Count</span><span class="sxs-lookup"><span data-stu-id="abb4a-145">\Process(_Total)\Handle Count</span></span> |<span data-ttu-id="abb4a-146">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-146">Count</span></span> |
| <span data-ttu-id="abb4a-147">\Memory\% 사용 중인 커밋된 바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-147">\Memory\% Committed Bytes In Use</span></span> |<span data-ttu-id="abb4a-148">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-148">Percent</span></span> |
| <span data-ttu-id="abb4a-149">\Memory\Available Bytes</span><span class="sxs-lookup"><span data-stu-id="abb4a-149">\Memory\Available Bytes</span></span> |<span data-ttu-id="abb4a-150">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-150">Bytes</span></span> |
| <span data-ttu-id="abb4a-151">\Memory\Committed Bytes</span><span class="sxs-lookup"><span data-stu-id="abb4a-151">\Memory\Committed Bytes</span></span> |<span data-ttu-id="abb4a-152">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-152">Bytes</span></span> |
| <span data-ttu-id="abb4a-153">\Memory\Commit Limit</span><span class="sxs-lookup"><span data-stu-id="abb4a-153">\Memory\Commit Limit</span></span> |<span data-ttu-id="abb4a-154">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-154">Bytes</span></span> |
| <span data-ttu-id="abb4a-155">\Memory\Pool Paged Bytes</span><span class="sxs-lookup"><span data-stu-id="abb4a-155">\Memory\Pool Paged Bytes</span></span> |<span data-ttu-id="abb4a-156">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-156">Bytes</span></span> |
| <span data-ttu-id="abb4a-157">\Memory\Pool Nonpaged Bytes</span><span class="sxs-lookup"><span data-stu-id="abb4a-157">\Memory\Pool Nonpaged Bytes</span></span> |<span data-ttu-id="abb4a-158">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-158">Bytes</span></span> |
| <span data-ttu-id="abb4a-159">\PhysicalDisk(_Total)\% 디스크 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-159">\PhysicalDisk(_Total)\% Disk Time</span></span> |<span data-ttu-id="abb4a-160">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-160">Percent</span></span> |
| <span data-ttu-id="abb4a-161">\PhysicalDisk(_Total)\% 디스크 읽기 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-161">\PhysicalDisk(_Total)\% Disk Read Time</span></span> |<span data-ttu-id="abb4a-162">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-162">Percent</span></span> |
| <span data-ttu-id="abb4a-163">\PhysicalDisk(_Total)\% 디스크 쓰기 시간</span><span class="sxs-lookup"><span data-stu-id="abb4a-163">\PhysicalDisk(_Total)\% Disk Write Time</span></span> |<span data-ttu-id="abb4a-164">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-164">Percent</span></span> |
| <span data-ttu-id="abb4a-165">\PhysicalDisk(_Total)\디스크 전송/초</span><span class="sxs-lookup"><span data-stu-id="abb4a-165">\PhysicalDisk(_Total)\Disk Transfers/sec</span></span> |<span data-ttu-id="abb4a-166">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-166">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-167">\PhysicalDisk(_Total)\Disk Reads/sec</span><span class="sxs-lookup"><span data-stu-id="abb4a-167">\PhysicalDisk(_Total)\Disk Reads/sec</span></span> |<span data-ttu-id="abb4a-168">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-168">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-169">\PhysicalDisk(_Total)\Disk Writes/sec</span><span class="sxs-lookup"><span data-stu-id="abb4a-169">\PhysicalDisk(_Total)\Disk Writes/sec</span></span> |<span data-ttu-id="abb4a-170">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-170">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="abb4a-171">\PhysicalDisk(_Total)\Disk Bytes/sec</span></span> |<span data-ttu-id="abb4a-172">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-172">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="abb4a-173">\PhysicalDisk(_Total)\Disk Read Bytes/sec</span></span> |<span data-ttu-id="abb4a-174">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-174">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="abb4a-175">\PhysicalDisk(_Total)\Disk Write Bytes/sec</span></span> |<span data-ttu-id="abb4a-176">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-176">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-177">\PhysicalDisk(_Total)\Avg. 디스크 큐 길이</span><span class="sxs-lookup"><span data-stu-id="abb4a-177">\PhysicalDisk(_Total)\Avg. Disk Queue Length</span></span> |<span data-ttu-id="abb4a-178">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-178">Count</span></span> |
| <span data-ttu-id="abb4a-179">\PhysicalDisk(_Total)\Avg. 디스크 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="abb4a-179">\PhysicalDisk(_Total)\Avg. Disk Read Queue Length</span></span> |<span data-ttu-id="abb4a-180">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-180">Count</span></span> |
| <span data-ttu-id="abb4a-181">\PhysicalDisk(_Total)\Avg. 디스크 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="abb4a-181">\PhysicalDisk(_Total)\Avg. Disk Write Queue Length</span></span> |<span data-ttu-id="abb4a-182">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-182">Count</span></span> |
| <span data-ttu-id="abb4a-183">\LogicalDisk(_Total)\% 사용 가능한 공간</span><span class="sxs-lookup"><span data-stu-id="abb4a-183">\LogicalDisk(_Total)\% Free Space</span></span> |<span data-ttu-id="abb4a-184">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-184">Percent</span></span> |
| <span data-ttu-id="abb4a-185">\LogicalDisk(_Total)\Free Megabytes</span><span class="sxs-lookup"><span data-stu-id="abb4a-185">\LogicalDisk(_Total)\Free Megabytes</span></span> |<span data-ttu-id="abb4a-186">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-186">Count</span></span> |

### <a name="guest-os-metrics-linux-vms"></a><span data-ttu-id="abb4a-187">게스트 OS 메트릭 Linux VM</span><span class="sxs-lookup"><span data-stu-id="abb4a-187">Guest OS metrics Linux VMs</span></span>
<span data-ttu-id="abb4a-188">Azure에서 VM을 만들 때 진단 확장을 사용하여 기본적으로 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-188">When you create a VM in Azure, diagnostics is enabled by default by using Diagnostics extension.</span></span>

<span data-ttu-id="abb4a-189">다음 powershell에서 명령을 hello를 사용 하 여 hello 메트릭 목록은 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-189">You can generate a list of hello metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 <span data-ttu-id="abb4a-190">다음 메트릭 hello에 대 한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-190">You can create an alert for hello following metrics:</span></span>

| <span data-ttu-id="abb4a-191">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="abb4a-191">Metric Name</span></span> | <span data-ttu-id="abb4a-192">단위</span><span class="sxs-lookup"><span data-stu-id="abb4a-192">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="abb4a-193">\Memory\AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="abb4a-193">\Memory\AvailableMemory</span></span> |<span data-ttu-id="abb4a-194">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-194">Bytes</span></span> |
| <span data-ttu-id="abb4a-195">\Memory\PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="abb4a-195">\Memory\PercentAvailableMemory</span></span> |<span data-ttu-id="abb4a-196">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-196">Percent</span></span> |
| <span data-ttu-id="abb4a-197">\Memory\UsedMemory</span><span class="sxs-lookup"><span data-stu-id="abb4a-197">\Memory\UsedMemory</span></span> |<span data-ttu-id="abb4a-198">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-198">Bytes</span></span> |
| <span data-ttu-id="abb4a-199">\Memory\PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="abb4a-199">\Memory\PercentUsedMemory</span></span> |<span data-ttu-id="abb4a-200">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-200">Percent</span></span> |
| <span data-ttu-id="abb4a-201">\Memory\PercentUsedByCache</span><span class="sxs-lookup"><span data-stu-id="abb4a-201">\Memory\PercentUsedByCache</span></span> |<span data-ttu-id="abb4a-202">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-202">Percent</span></span> |
| <span data-ttu-id="abb4a-203">\Memory\PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="abb4a-203">\Memory\PagesPerSec</span></span> |<span data-ttu-id="abb4a-204">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-204">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-205">\Memory\PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="abb4a-205">\Memory\PagesReadPerSec</span></span> |<span data-ttu-id="abb4a-206">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-206">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-207">\Memory\PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="abb4a-207">\Memory\PagesWrittenPerSec</span></span> |<span data-ttu-id="abb4a-208">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-208">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-209">\Memory\AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="abb4a-209">\Memory\AvailableSwap</span></span> |<span data-ttu-id="abb4a-210">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-210">Bytes</span></span> |
| <span data-ttu-id="abb4a-211">\Memory\PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="abb4a-211">\Memory\PercentAvailableSwap</span></span> |<span data-ttu-id="abb4a-212">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-212">Percent</span></span> |
| <span data-ttu-id="abb4a-213">\Memory\UsedSwap</span><span class="sxs-lookup"><span data-stu-id="abb4a-213">\Memory\UsedSwap</span></span> |<span data-ttu-id="abb4a-214">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-214">Bytes</span></span> |
| <span data-ttu-id="abb4a-215">\Memory\PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="abb4a-215">\Memory\PercentUsedSwap</span></span> |<span data-ttu-id="abb4a-216">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-216">Percent</span></span> |
| <span data-ttu-id="abb4a-217">\Processor\PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-217">\Processor\PercentIdleTime</span></span> |<span data-ttu-id="abb4a-218">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-218">Percent</span></span> |
| <span data-ttu-id="abb4a-219">\Processor\PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-219">\Processor\PercentUserTime</span></span> |<span data-ttu-id="abb4a-220">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-220">Percent</span></span> |
| <span data-ttu-id="abb4a-221">\Processor\PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-221">\Processor\PercentNiceTime</span></span> |<span data-ttu-id="abb4a-222">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-222">Percent</span></span> |
| <span data-ttu-id="abb4a-223">\Processor\PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-223">\Processor\PercentPrivilegedTime</span></span> |<span data-ttu-id="abb4a-224">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-224">Percent</span></span> |
| <span data-ttu-id="abb4a-225">\Processor\PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-225">\Processor\PercentInterruptTime</span></span> |<span data-ttu-id="abb4a-226">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-226">Percent</span></span> |
| <span data-ttu-id="abb4a-227">\Processor\PercentDPCTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-227">\Processor\PercentDPCTime</span></span> |<span data-ttu-id="abb4a-228">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-228">Percent</span></span> |
| <span data-ttu-id="abb4a-229">\Processor\PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-229">\Processor\PercentProcessorTime</span></span> |<span data-ttu-id="abb4a-230">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-230">Percent</span></span> |
| <span data-ttu-id="abb4a-231">\Processor\PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-231">\Processor\PercentIOWaitTime</span></span> |<span data-ttu-id="abb4a-232">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-232">Percent</span></span> |
| <span data-ttu-id="abb4a-233">\PhysicalDisk\BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-233">\PhysicalDisk\BytesPerSecond</span></span> |<span data-ttu-id="abb4a-234">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-234">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-235">\PhysicalDisk\ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-235">\PhysicalDisk\ReadBytesPerSecond</span></span> |<span data-ttu-id="abb4a-236">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-236">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-237">\PhysicalDisk\WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-237">\PhysicalDisk\WriteBytesPerSecond</span></span> |<span data-ttu-id="abb4a-238">초당 바이트 수</span><span class="sxs-lookup"><span data-stu-id="abb4a-238">BytesPerSecond</span></span> |
| <span data-ttu-id="abb4a-239">\PhysicalDisk\TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-239">\PhysicalDisk\TransfersPerSecond</span></span> |<span data-ttu-id="abb4a-240">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-240">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-241">\PhysicalDisk\ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-241">\PhysicalDisk\ReadsPerSecond</span></span> |<span data-ttu-id="abb4a-242">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-242">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-243">\PhysicalDisk\WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="abb4a-243">\PhysicalDisk\WritesPerSecond</span></span> |<span data-ttu-id="abb4a-244">초당 개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-244">CountPerSecond</span></span> |
| <span data-ttu-id="abb4a-245">\PhysicalDisk\AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-245">\PhysicalDisk\AverageReadTime</span></span> |<span data-ttu-id="abb4a-246">초</span><span class="sxs-lookup"><span data-stu-id="abb4a-246">Seconds</span></span> |
| <span data-ttu-id="abb4a-247">\PhysicalDisk\AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-247">\PhysicalDisk\AverageWriteTime</span></span> |<span data-ttu-id="abb4a-248">초</span><span class="sxs-lookup"><span data-stu-id="abb4a-248">Seconds</span></span> |
| <span data-ttu-id="abb4a-249">\PhysicalDisk\AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="abb4a-249">\PhysicalDisk\AverageTransferTime</span></span> |<span data-ttu-id="abb4a-250">초</span><span class="sxs-lookup"><span data-stu-id="abb4a-250">Seconds</span></span> |
| <span data-ttu-id="abb4a-251">\PhysicalDisk\AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="abb4a-251">\PhysicalDisk\AverageDiskQueueLength</span></span> |<span data-ttu-id="abb4a-252">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-252">Count</span></span> |
| <span data-ttu-id="abb4a-253">\NetworkInterface\BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="abb4a-253">\NetworkInterface\BytesTransmitted</span></span> |<span data-ttu-id="abb4a-254">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-254">Bytes</span></span> |
| <span data-ttu-id="abb4a-255">\NetworkInterface\BytesReceived</span><span class="sxs-lookup"><span data-stu-id="abb4a-255">\NetworkInterface\BytesReceived</span></span> |<span data-ttu-id="abb4a-256">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-256">Bytes</span></span> |
| <span data-ttu-id="abb4a-257">\NetworkInterface\PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="abb4a-257">\NetworkInterface\PacketsTransmitted</span></span> |<span data-ttu-id="abb4a-258">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-258">Count</span></span> |
| <span data-ttu-id="abb4a-259">\NetworkInterface\PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="abb4a-259">\NetworkInterface\PacketsReceived</span></span> |<span data-ttu-id="abb4a-260">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-260">Count</span></span> |
| <span data-ttu-id="abb4a-261">\NetworkInterface\BytesTotal</span><span class="sxs-lookup"><span data-stu-id="abb4a-261">\NetworkInterface\BytesTotal</span></span> |<span data-ttu-id="abb4a-262">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-262">Bytes</span></span> |
| <span data-ttu-id="abb4a-263">\NetworkInterface\TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="abb4a-263">\NetworkInterface\TotalRxErrors</span></span> |<span data-ttu-id="abb4a-264">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-264">Count</span></span> |
| <span data-ttu-id="abb4a-265">\NetworkInterface\TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="abb4a-265">\NetworkInterface\TotalTxErrors</span></span> |<span data-ttu-id="abb4a-266">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-266">Count</span></span> |
| <span data-ttu-id="abb4a-267">\NetworkInterface\TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="abb4a-267">\NetworkInterface\TotalCollisions</span></span> |<span data-ttu-id="abb4a-268">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-268">Count</span></span> |

## <a name="commonly-used-web-server-farm-metrics"></a><span data-ttu-id="abb4a-269">일반적으로 사용되는 웹(서버 팜) 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-269">Commonly used Web (Server Farm) metrics</span></span>
<span data-ttu-id="abb4a-270">Hello Http 큐 길이 등 일반적인 웹 서버 메트릭을 기반으로 하는 자동 크기 조정을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-270">You can also perform autoscale based on common web server metrics such as hello Http queue length.</span></span> <span data-ttu-id="abb4a-271">메트릭 이름은 **HttpQueueLength**입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-271">It's metric name is **HttpQueueLength**.</span></span>  <span data-ttu-id="abb4a-272">다음 섹션 목록 사용 가능한 서버 팜 (웹 앱) 메트릭 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-272">hello following section lists available server farm (Web Apps) metrics.</span></span>

### <a name="web-apps-metrics"></a><span data-ttu-id="abb4a-273">웹앱 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-273">Web Apps metrics</span></span>
<span data-ttu-id="abb4a-274">다음 powershell에서 명령을 hello를 사용 하 여 hello 웹 응용 프로그램 메트릭 목록은 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-274">You can generate a list of hello Web Apps metrics by using hello following command in PowerShell.</span></span>

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="abb4a-275">다음 메트릭에 대한 경고를 만들거나 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-275">You can alert on or scale by these metrics.</span></span>

| <span data-ttu-id="abb4a-276">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="abb4a-276">Metric Name</span></span> | <span data-ttu-id="abb4a-277">단위</span><span class="sxs-lookup"><span data-stu-id="abb4a-277">Unit</span></span> |
| --- | --- |
| <span data-ttu-id="abb4a-278">CpuPercentage</span><span class="sxs-lookup"><span data-stu-id="abb4a-278">CpuPercentage</span></span> |<span data-ttu-id="abb4a-279">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-279">Percent</span></span> |
| <span data-ttu-id="abb4a-280">MemoryPercentage</span><span class="sxs-lookup"><span data-stu-id="abb4a-280">MemoryPercentage</span></span> |<span data-ttu-id="abb4a-281">백분율</span><span class="sxs-lookup"><span data-stu-id="abb4a-281">Percent</span></span> |
| <span data-ttu-id="abb4a-282">DiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="abb4a-282">DiskQueueLength</span></span> |<span data-ttu-id="abb4a-283">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-283">Count</span></span> |
| <span data-ttu-id="abb4a-284">HttpQueueLength</span><span class="sxs-lookup"><span data-stu-id="abb4a-284">HttpQueueLength</span></span> |<span data-ttu-id="abb4a-285">개수</span><span class="sxs-lookup"><span data-stu-id="abb4a-285">Count</span></span> |
| <span data-ttu-id="abb4a-286">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="abb4a-286">BytesReceived</span></span> |<span data-ttu-id="abb4a-287">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-287">Bytes</span></span> |
| <span data-ttu-id="abb4a-288">BytesSent</span><span class="sxs-lookup"><span data-stu-id="abb4a-288">BytesSent</span></span> |<span data-ttu-id="abb4a-289">바이트</span><span class="sxs-lookup"><span data-stu-id="abb4a-289">Bytes</span></span> |

## <a name="commonly-used-storage-metrics"></a><span data-ttu-id="abb4a-290">일반적으로 사용되는 저장소 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-290">Commonly used Storage metrics</span></span>
<span data-ttu-id="abb4a-291">저장소 큐 길이 hello hello 저장소 큐의 메시지 수를으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-291">You can scale by Storage queue length, which is hello number of messages in hello storage queue.</span></span> <span data-ttu-id="abb4a-292">저장소 큐 길이 특별 한 메트릭 및 hello 임계값은 hello 인스턴스 당 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-292">Storage queue length is a special metric and hello threshold is hello number of messages per instance.</span></span> <span data-ttu-id="abb4a-293">예를 들어 두 개의 인스턴스가 있는 및 hello 임계값 too100 설정 되 면 hello hello 큐에 메시지의 총 수는 200 때 발생 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-293">For example, if there are two instances and if hello threshold is set too100, scaling occurs when hello total number of messages in hello queue is 200.</span></span> <span data-ttu-id="abb4a-294">인스턴스 당 100 개의 메시지, 120 및 80, 또는 모든 기타 조합을 too200 이상의를 추가 하는 일 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-294">That can be 100 messages per instance, 120 and 80, or any other combination that adds up too200 or more.</span></span>

<span data-ttu-id="abb4a-295">이 설정은 hello hello에서 Azure 포털 구성 **설정을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-295">Configure this setting in hello Azure portal in hello **Settings** blade.</span></span> <span data-ttu-id="abb4a-296">VM 크기 집합에 대 한 리소스 관리자 템플릿 toouse hello에에서 hello 자동 크기 조정 설정을 업데이트할 수 있습니다 *metricName* 으로 *ApproximateMessageCount* 으로 hello 저장소 큐의 hello ID 전달  *metricResourceUri*합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-296">For VM scale sets, you can update hello Autoscale setting in hello Resource Manager template toouse *metricName* as *ApproximateMessageCount* and pass hello ID of hello storage queue as *metricResourceUri*.</span></span>

<span data-ttu-id="abb4a-297">예를 들어 클래식 저장소 계정을 hello로 자동 크기 조정 설정을 metricTrigger 포함:</span><span class="sxs-lookup"><span data-stu-id="abb4a-297">For example, with a Classic Storage Account hello autoscale setting metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

<span data-ttu-id="abb4a-298">(비 클래식) 저장소 계정에 대 한 hello metricTrigger 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-298">For a (non-classic) storage account, hello metricTrigger would include:</span></span>

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a><span data-ttu-id="abb4a-299">자주 사용되는 서비스 버스 메트릭</span><span class="sxs-lookup"><span data-stu-id="abb4a-299">Commonly used Service Bus metrics</span></span>
<span data-ttu-id="abb4a-300">서비스 버스 큐 길이 hello hello 서비스 버스 큐의 메시지 수를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-300">You can scale by Service Bus queue length, which is hello number of messages in hello Service Bus queue.</span></span> <span data-ttu-id="abb4a-301">서비스 버스 큐 길이 특별 한 메트릭 및 hello 임계값은 hello 인스턴스 당 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-301">Service Bus queue length is a special metric and hello threshold is hello number of messages per instance.</span></span> <span data-ttu-id="abb4a-302">예를 들어 두 개의 인스턴스가 있는 및 hello 임계값 too100 설정 되 면 hello hello 큐에 메시지의 총 수는 200 때 발생 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-302">For example, if there are two instances and if hello threshold is set too100, scaling occurs when hello total number of messages in hello queue is 200.</span></span> <span data-ttu-id="abb4a-303">인스턴스 당 100 개의 메시지, 120 및 80, 또는 모든 기타 조합을 too200 이상의를 추가 하는 일 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-303">That can be 100 messages per instance, 120 and 80, or any other combination that adds up too200 or more.</span></span>

<span data-ttu-id="abb4a-304">VM 크기 집합에 대 한 리소스 관리자 템플릿 toouse hello에에서 hello 자동 크기 조정 설정을 업데이트할 수 있습니다 *metricName* 으로 *ApproximateMessageCount* 으로 hello 저장소 큐의 hello ID 전달  *metricResourceUri*합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-304">For VM scale sets, you can update hello Autoscale setting in hello Resource Manager template toouse *metricName* as *ApproximateMessageCount* and pass hello ID of hello storage queue as *metricResourceUri*.</span></span>

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> <span data-ttu-id="abb4a-305">서비스 버스에 대 한 hello 리소스 그룹 개념 존재 하지 않는 있지만 Azure 리소스 관리자 / 지역당 기본 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-305">For Service Bus, hello resource group concept does not exist but Azure Resource Manager creates a default resource group per region.</span></span> <span data-ttu-id="abb4a-306">hello 리소스 그룹은 일반적으로 hello 'Default-ServiceBus-[region]' 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-306">hello resource group is usually in hello 'Default-ServiceBus-[region]' format.</span></span> <span data-ttu-id="abb4a-307">예를 들어 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' 등입니다.</span><span class="sxs-lookup"><span data-stu-id="abb4a-307">For example, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast' etc.</span></span>
>
>
