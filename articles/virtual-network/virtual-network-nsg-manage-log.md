---
title: "aaaMonitor 작업, 이벤트 및 Nsg에 대 한 카운터 | Microsoft Docs"
description: "자세한 내용은 방법 tooenable 카운터, 이벤트 및 Nsg에 대 한 작업 로깅"
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
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="ad632-103">NSG(네트워크 보안 그룹)에 대한 로그 분석</span><span class="sxs-lookup"><span data-stu-id="ad632-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="ad632-104">Nsg에 대 한 진단 로그 범주를 수행 하는 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="ad632-105">**이벤트:** 어떤 NSG에 대 한 규칙은 적용 된 tooVMs 및 MAC 주소에 따라 인스턴스 역할 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="ad632-106">이러한 규칙에 대 한 hello 상태 60 초 마다 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="ad632-107">**규칙 카운터:** Contains 항목 각 NSG 횟수에 대 한 규칙을 적용 된 toodeny 되었거나 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="ad632-108">진단 로그는 hello Azure 리소스 관리자 배포 모델을 통해 배포 된 Nsg 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ad632-109">Nsg hello 클래식 배포 모델을 통해 배포에 대 한 진단 로깅을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="ad632-110">더 잘 이해 hello 두 모델의,에 대 한 참조 hello [이해 Azure 배포 모델](../resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="ad632-111">활동 로깅(이전의 감사 또는 작업 로그)은 Azure 배포 모델 중 하나를 통해 만든 NSG에 대해 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="ad632-112">리소스 유형에 따라 hello를 포함 하는 항목에 대 한 모양 hello 활동 로그에 Nsg에 어떤 작업을 완료 된 toodetermine:</span><span class="sxs-lookup"><span data-stu-id="ad632-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="ad632-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="ad632-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="ad632-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="ad632-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="ad632-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="ad632-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="ad632-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="ad632-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="ad632-117">읽기 hello [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) 활동 로그에 대 한 자세한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="ad632-118">진단 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="ad632-118">Enable diagnostic logging</span></span>

<span data-ttu-id="ad632-119">에 대 한 진단 로깅을 활성화 해야 *각* NSG 원하는 toocollect 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="ad632-120">hello [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 진단 로그를 보낼 수 있는 문서에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="ad632-121">전체 hello hello의 단계를 기존 NSG가 없는 경우 [네트워크 보안 그룹 만들기](virtual-networks-create-nsg-arm-pportal.md) 문서 toocreate 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="ad632-122">NSG 진단 hello 메서드를 다음 중 하나를 사용 하 여 로깅을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="ad632-123">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ad632-123">Azure portal</span></span>

<span data-ttu-id="ad632-124">toouse hello 포털 tooenable 로깅, 로그인 toohello [포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad632-125">**더 많은 서비스**를 클릭한 다음 *네트워크 보안 그룹*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="ad632-126">Hello에 대 한 로깅을 tooenable 원하는 NSG를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="ad632-127">hello 비계산 리소스에 대 한 hello 지침에 따라 [hello 포털에서 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="ad632-128">**NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** 또는 두 범주의 로그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="ad632-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad632-129">PowerShell</span></span>

<span data-ttu-id="ad632-130">로깅, toouse PowerShell tooenable hello 지침 hello에 따라 [PowerShell 통해 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="ad632-131">Hello 정보 hello 아티클에서 명령을 입력할 수 있도록 하기 전에 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="ad632-132">Hello에 대 한 hello 값 toouse를 확인할 수 있습니다 `-ResourceId` hello 다음 [텍스트]를 적절 하 게 다음 hello 명령 입력을 대체 하 여 매개 변수 `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="ad632-133">hello 명령에서 hello ID 출력은 너무 유사*/subscriptions/ [구독 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="ad632-134">Toocollect 데이터 로그 범주를 원하는 경우 추가 `-Categories [category]` toohello 범주는 하나 hello 문서의 hello 명령 끝 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="ad632-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="ad632-135">Hello를 사용 하지 않으면 `-Categories` 범주 로그 둘 다에 대 한 데이터 컬렉션 매개 변수를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="ad632-136">Azure CLI(명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="ad632-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="ad632-137">toouse CLI tooenable 로깅 hello, hello 지침 hello에 따라 [CLI 통해 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="ad632-138">Hello 정보 hello 아티클에서 명령을 입력할 수 있도록 하기 전에 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="ad632-139">Hello에 대 한 hello 값 toouse를 확인할 수 있습니다 `-ResourceId` hello 다음 [텍스트]를 적절 하 게 다음 hello 명령 입력을 대체 하 여 매개 변수 `azure network nsg show [resource-group-name] [nsg-name]`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="ad632-140">hello 명령에서 hello ID 출력은 너무 유사*/subscriptions/ [구독 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="ad632-141">Toocollect 데이터 로그 범주를 원하는 경우 추가 `-Categories [category]` toohello 범주는 하나 hello 문서의 hello 명령 끝 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="ad632-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="ad632-142">Hello를 사용 하지 않으면 `-Categories` 범주 로그 둘 다에 대 한 데이터 컬렉션 매개 변수를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="ad632-143">기록된 데이터</span><span class="sxs-lookup"><span data-stu-id="ad632-143">Logged data</span></span>

<span data-ttu-id="ad632-144">JSON 형식 데이터는 두 로그에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="ad632-145">각 로그 형식에 대해 작성 된 hello 특정 데이터 hello 다음 섹션에에서 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="ad632-146">이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="ad632-146">Event log</span></span>
<span data-ttu-id="ad632-147">이 로그에는 어떤 NSG에 대 한 규칙은 적용 된 tooVMs과는 클라우드 서비스 역할 인스턴스를 기반으로 MAC 주소 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="ad632-148">다음 예에서는 데이터 hello 각 이벤트에 대해 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-148">hello following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="ad632-149">규칙 카운터 로그</span><span class="sxs-lookup"><span data-stu-id="ad632-149">Rule counter log</span></span>

<span data-ttu-id="ad632-150">이 로그는 각 규칙을 적용 tooresources에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="ad632-151">hello 다음 예제에서는 데이터 때마다 기록 됩니다는 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-151">hello following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="ad632-152">로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="ad632-152">View and analyze logs</span></span>

<span data-ttu-id="ad632-153">toolearn tooview 활동 데이터를 기록 하는 방법을 읽고 hello [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="ad632-154">toolearn 방법 tooview 진단 로그 데이터를 읽을 hello [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ad632-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="ad632-155">진단 데이터 tooLog 분석을 보내면 hello를 사용할 수 있습니다 [Azure 네트워크 보안 그룹 분석](../log-analytics/log-analytics-azure-networking-analytics.md) 향상 된 insights (미리 보기) 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ad632-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
