---
title: "NSG에 대한 작업, 이벤트 및 카운터 모니터링 | Microsoft Docs"
description: "NSG에 대한 카운터, 이벤트 및 작업 로깅을 사용하도록 설정하는 방법에 대해 알아보기"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="37c92-103">NSG(네트워크 보안 그룹)에 대한 로그 분석</span><span class="sxs-lookup"><span data-stu-id="37c92-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="37c92-104">NSG에 대한 다음 진단 로그 범주를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="37c92-105">**이벤트:** VM 및 MAC 주소 기반 인스턴스 역할에 적용된 NSG 규칙에 대한 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="37c92-106">이러한 규칙에 대한 상태는 60초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="37c92-107">**규칙 카운터:** 트래픽을 허용하거나 거부하기 위해 각 NSG 규칙이 적용된 횟수에 대한 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="37c92-108">진단 로그는 Azure Resource Manager 배포 모델을 통해 배포된 NSG에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="37c92-109">클래식 배포 모델을 통해 배포된 NSG에 대해 진단 로깅을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="37c92-110">두 모델의 이해를 돕기 위해 [Azure 배포 모델 이해](../resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37c92-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="37c92-111">활동 로깅(이전의 감사 또는 작업 로그)은 Azure 배포 모델 중 하나를 통해 만든 NSG에 대해 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="37c92-112">활동 로그의 NSG 내에서 완료된 작업을 확인하려면 다음과 같은 리소스 유형을 포함하는 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="37c92-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="37c92-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="37c92-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="37c92-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="37c92-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="37c92-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="37c92-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="37c92-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="37c92-117">활동 로그에 대한 자세한 내용을 보려면 [Azure 활동 로그 개요](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) 문서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="37c92-118">진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="37c92-118">Enable diagnostic logging</span></span>

<span data-ttu-id="37c92-119">진단 로깅은 데이터를 수집하려는 *각* NSG에 대해 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="37c92-120">[Azure 진단 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서는 진단 로그를 보낼 수 있는 위치를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="37c92-121">기존 NSG가 없는 경우 [네트워크 보안 그룹 만들기](virtual-networks-create-nsg-arm-pportal.md) 문서의 단계를 완료하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="37c92-122">다음 방법 중 하나를 사용하여 NSG 진단 로깅을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="37c92-123">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="37c92-123">Azure portal</span></span>

<span data-ttu-id="37c92-124">로깅을 활성화하는 데 포털을 사용하려면 [포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="37c92-125">**더 많은 서비스**를 클릭한 다음 *네트워크 보안 그룹*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="37c92-126">로깅을 활성화하려는 NSG를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="37c92-127">[포털에서 진단 로그 사용](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서의 비 계산 리소스에 대한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="37c92-128">**NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** 또는 두 범주의 로그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="37c92-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37c92-129">PowerShell</span></span>

<span data-ttu-id="37c92-130">PowerShell을 사용하여 로깅을 활성화하려면 [PowerShell을 통해 진단 로그 사용](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="37c92-131">문서에서 명령을 입력하기 전에 다음 정보를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="37c92-132">다음 [텍스트]를 적절하게 대체한 다음 명령 `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`을 입력하여 `-ResourceId` 매개 변수에 사용할 값을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="37c92-133">명령의 ID 출력은 */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="37c92-134">로그 범주에서 데이터를 수집하려는 경우 문서에서 명령의 끝에 `-Categories [category]`를 추가합니다. 범주는 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*입니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="37c92-135">`-Categories` 매개 변수를 사용하지 않는 경우 데이터 컬렉션은 두 로그 범주에 대해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="37c92-136">Azure CLI(명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="37c92-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="37c92-137">CLI를 사용하여 로깅을 활성화하려면 [CLI를 통해 진단 로그 사용](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="37c92-138">문서에서 명령을 입력하기 전에 다음 정보를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="37c92-139">다음 [텍스트]를 적절하게 대체한 다음 명령 `azure network nsg show [resource-group-name] [nsg-name]`을 입력하여 `-ResourceId` 매개 변수에 사용할 값을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="37c92-140">명령의 ID 출력은 */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="37c92-141">로그 범주에서 데이터를 수집하려는 경우 문서에서 명령의 끝에 `-Categories [category]`를 추가합니다. 범주는 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*입니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="37c92-142">`-Categories` 매개 변수를 사용하지 않는 경우 데이터 컬렉션은 두 로그 범주에 대해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="37c92-143">기록된 데이터</span><span class="sxs-lookup"><span data-stu-id="37c92-143">Logged data</span></span>

<span data-ttu-id="37c92-144">JSON 형식 데이터는 두 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="37c92-145">각 로그 형식에 대해 기록된 특정 데이터는 다음 섹션에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="37c92-146">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="37c92-146">Event log</span></span>
<span data-ttu-id="37c92-147">이 로그는 MAC 주소에 따라 VM 및 클라우드 서비스 역할 인스턴스에 적용될 NSG 규칙에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="37c92-148">다음 예제 데이터는 각 이벤트에 대해 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="37c92-149">규칙 카운터 로그</span><span class="sxs-lookup"><span data-stu-id="37c92-149">Rule counter log</span></span>

<span data-ttu-id="37c92-150">이 로그는 리소스에 적용되는 각 규칙에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="37c92-151">다음 예제 데이터는 규칙이 적용될 때마다 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="37c92-152">로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="37c92-152">View and analyze logs</span></span>

<span data-ttu-id="37c92-153">활동 로그 데이터를 보는 방법을 알아보려면 [Azure 활동 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="37c92-154">진단 로그 데이터를 보는 방법을 알아보려면 [Azure 진단 로그 개요](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="37c92-155">Log Analytics에 진단 데이터를 보내는 경우 향상된 통찰력을 위해 [Azure 네트워크 보안 그룹 분석](../log-analytics/log-analytics-azure-networking-analytics.md)(미리 보기) 관리 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c92-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
