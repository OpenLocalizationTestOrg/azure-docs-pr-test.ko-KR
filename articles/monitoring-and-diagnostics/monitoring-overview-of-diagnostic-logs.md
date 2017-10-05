---
title: "Azure 진단 로그 | Microsoft Docs"
description: "Azure 진단 로그란 무엇이고 Azure 리소스 내에서 발생하는 이벤트를 파악하는 데 어떻게 사용할 수 있는지 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="80895-103">Azure 리소스에서 로그 데이터 수집 및 소비</span><span class="sxs-lookup"><span data-stu-id="80895-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="80895-104">Azure 리소스 진단 로그란?</span><span class="sxs-lookup"><span data-stu-id="80895-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="80895-105">**Azure 리소스 수준 진단 로그**는 해당 리소스의 작업에 대한 풍부하고 빈번한 데이터를 제공하는 리소스에서 내보낸 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="80895-106">이러한 로그의 내용은 리소스 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="80895-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="80895-107">예를 들어 네트워크 보안 그룹 규칙 카운터와 Key Vault 감사는 리소스 로그의 두 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="80895-108">리소스 수준 진단 로그는 [활동 로그](monitoring-overview-activity-logs.md)와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="80895-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="80895-109">활동 로그는 가상 컴퓨터 만들기나 논리 앱 삭제 등, Resource Manager를 사용하여 구독에서 리소스에 대해 수행된 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="80895-110">활동 로그는 구독 수준 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="80895-111">리소스 수준 진단 로그는 Key Vault에서 암호 가져오기 등과 같이 리소스 자체에서 수행된 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="80895-112">리소스 수준 진단 로그도 게스트 OS 수준 진단 로그와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="80895-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="80895-113">게스트 OS 진단 로그는 가상 컴퓨터나 다른 지원되는 리소스 유형 안에서 실행되는 에이전트가 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="80895-114">리소스 수준 진단 로그는 에이전트가 필요하지 않으며 Azure 플랫폼 자체에서 리소스 특정 데이터를 수집하고, 게스트 OS 수준 진단 로그는 가상 컴퓨터에서 실행되는 운영 체제 및 응용 프로그램에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="80895-115">일부 리소스만 여기서 설명하는 새로운 형식의 리소스 진단 로그를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="80895-116">이 문서는 리소스 유형에서 새로운 리소스 수준 진단 로그에 지원하는 나열된 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="80895-117">리소스 진단 로그와 다른 로그 유형 비교</span><span class="sxs-lookup"><span data-stu-id="80895-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="80895-118">리소스 수준 진단 로그로 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="80895-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="80895-119">리소스 수준 진단 로그를 통해 수행할 수 있는 몇 가지 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![리소스 진단 로그의 논리적 배치](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="80895-121">감사 또는 수동 검사를 위해 [**저장소 계정**](monitoring-archive-diagnostic-logs.md)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="80895-122">**리소스 진단 설정**을 사용하여 보존 기간(일)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="80895-123">[타사 서비스 또는 사용자 지정 분석 솔루션(예: PowerBI)으로 수집을 위해 **Event Hubs**로 스트림](monitoring-stream-diagnostic-logs-to-event-hubs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="80895-124">[OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="80895-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="80895-125">로그를 내보내는 것과 동일한 구독에 위치하지 않는 저장소 계정 또는 Event Hubs 네임스페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="80895-126">설정을 구성하는 사용자에게는 두 구독에 대한 적절한 RBAC 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="80895-127">리소스 진단 설정</span><span class="sxs-lookup"><span data-stu-id="80895-127">Resource diagnostic settings</span></span>
<span data-ttu-id="80895-128">리소스 진단 설정을 사용하여 비-계산 리소스에 대한 리소스 진단 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="80895-129">리소스 제어를 위한 **리소스 진단 설정**은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="80895-130">리소스 진단 로그 및 메트릭을 보내는 위치(Storage 계정, Event Hubs 및/또는 OMS Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="80895-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="80895-131">전송되는 로그 범주 및 메트릭 데이터의 전송 여부.</span><span class="sxs-lookup"><span data-stu-id="80895-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="80895-132">각 로그 항목을 저장소 계정에 유지해야 하는 기간.</span><span class="sxs-lookup"><span data-stu-id="80895-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="80895-133">보존이 0일이라는 것은 로그가 영원히 보관된다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="80895-134">그렇지 않은 경우 값은 1에서 2147483647 사이의 숫자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="80895-135">보존 정책이 설정되었지만 저장소 계정에 로그를 저장할 수 없는 경우(예를 들어 Event Hubs 또는 OMS 옵션만 선택한 경우) 보존 정책은 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="80895-136">보존 정책은 매일 적용되므로 하루의 마지막에(UTC) 보존 정책이 지난 날의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="80895-137">예를 들어, 하루의 보존 정책이 있는 경우 오늘 날짜가 시작될 때 하루 전의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="80895-138">이러한 설정은 Azure Portal에서 리소스에 대한 진단 설정을 통해, Azure PowerShell 및 CLI 명령을 통해 또는 [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)를 통해 쉽게 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="80895-139">Compute 리소스(예: VM 또는 Service Fabric)의 게스트 OS 레이어에 대한 진단 로그 및 메트릭에서는 [출력의 구성 및 선택을 위한 별도의 메커니즘](../azure-diagnostics.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="80895-140">리소스 진단 로그의 컬렉션을 사용하도록 설정하는 방법 </span><span class="sxs-lookup"><span data-stu-id="80895-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="80895-141">[리소스 관리자 템플릿에서 리소스 만들기의 일부로](./monitoring-enable-diagnostic-logs-using-template.md) 또는 포털에서 해당 리소스의 페이지에서 리소스를 만든 후 리소스 진단 로그의 컬렉션을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="80895-142">또한 Azure PowerShell 또는 CLI 명령을 사용하거나 Azure Monitor REST API를 사용하여 언제든지 컬렉션을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="80895-143">이러한 지침은 모든 리소스에 직접 적용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="80895-144">특정 리소스 형식에 적용할 수 있는 특수한 단계를 알아보려면 이 페이지 맨 아래에 있는 스키마 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80895-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="80895-145">포털에서 리소스 진단 로그 컬렉션 활성화</span><span class="sxs-lookup"><span data-stu-id="80895-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="80895-146">특정 리소스로 이동하거나 Azure Monitor로 이동하여 리소스를 만든 후 Azure Portal에서 리소스 진단 로그의 컬렉션을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="80895-147">Azure Monitor를 통해 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="80895-148">[Azure Portal](http://portal.azure.com)에서 Azure Monitor로 이동하고 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure Monitor의 모니터링 섹션](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="80895-150">필요에 따라 리소스 그룹 또는 리소스 종류를 기준으로 목록을 필터링합니다. 그런 다음 진단 설정을 지정하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="80895-151">선택한 리소스에 설정이 없는 경우, 설정을 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="80895-152">“진단 켜기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-152">Click "Turn on diagnostics."</span></span>

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="80895-154">리소스에 기존 설정이 있는 경우 이 리소스에 이미 구성된 설정의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="80895-155">“진단 설정 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-155">Click "Add diagnostic setting."</span></span>

   ![진단 설정 추가 - 기존 설정](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="80895-157">설정에 이름을 지정하고, 데이터를 보낼 각 대상에 대한 확인란을 선택하고, 각 대상에 사용되는 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="80895-158">필요에 따라 **보존(일)** 슬라이더를 사용하여 이러한 로그를 유지할 일 수를 설정합니다(저장소 계정 대상에만 적용됨).</span><span class="sxs-lookup"><span data-stu-id="80895-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="80895-159">0일의 보존은 로그를 무기한 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="80895-161">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-161">Click **Save**.</span></span>

<span data-ttu-id="80895-162">몇 분 후 새 설정이 이 리소스에 대한 설정 목록에 표시되고, 새 이벤트 데이터가 생성되는 즉시 진단 로그가 지정된 대상에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="80895-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="80895-163">PowerShell을 통한 리소스 진단 로그 컬렉션 활성화</span><span class="sxs-lookup"><span data-stu-id="80895-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="80895-164">Azure PowerShell에서 리소스 진단 로그 컬렉션을 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="80895-165">저장소 계정에서 진단 로그의 저장소를 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="80895-166">저장소 계정 ID는 로그를 보낼 저장소 계정에 대한 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="80895-167">이벤트 허브로의 진단 로그 스트리밍을 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="80895-168">서비스 버스 규칙 ID는 `{Service Bus resource ID}/authorizationrules/{key name}` 형식의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="80895-169">진단 로그를 Log Analytics 작업 영역으로 보낼 수 있게 하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="80895-170">다음 명령을 사용하여 Log Analytics 작업 공간의 리소스 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="80895-171">이러한 매개 변수를 결합하여 여러 출력 옵션을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="80895-172">CLI를 통해 리소스 진단 로그 컬렉션 활성화</span><span class="sxs-lookup"><span data-stu-id="80895-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="80895-173">Azure CLI를 통해 리소스 진단 로그 컬렉션을 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="80895-174">저장소 계정에서 진단 로그의 저장소를 사용하도록 설정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="80895-175">저장소 계정 ID는 로그를 보낼 저장소 계정에 대한 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="80895-176">이벤트 허브로의 진단 로그 스트리밍을 활성화하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="80895-177">서비스 버스 규칙 ID는 `{Service Bus resource ID}/authorizationrules/{key name}` 형식의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="80895-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="80895-178">진단 로그를 Log Analytics 작업 영역으로 보낼 수 있게 하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="80895-179">이러한 매개 변수를 결합하여 여러 출력 옵션을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="80895-180">REST API를 통해 리소스 진단 로그 컬렉션 활성화</span><span class="sxs-lookup"><span data-stu-id="80895-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="80895-181">Azure Monitor REST API를 사용하여 진단 설정을 변경하려면 [이 문서](https://msdn.microsoft.com/library/azure/dn931931.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80895-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="80895-182">포털에서 리소스 진단 설정 관리</span><span class="sxs-lookup"><span data-stu-id="80895-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="80895-183">리소스를 모두 진단 설정으로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80895-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="80895-184">포털에서 **모니터**로 이동하여 **진단 설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="80895-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![포털의 진단 로그 블레이드](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="80895-186">모니터 섹션을 찾기 위해 “더 많은 서비스”를 클릭해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="80895-187">여기에서 진단 설정을 지원하는 모든 리소스를 보고 필터링하여 진단을 사용하도록 설정했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="80895-188">드릴다운하여 여러 설정이 리소스에 설정되어 있는지 확인하고, 데이터가 이동하는 저장소 계정, Event Hubs 네임스페이스 및/또는 Log Analytics 작업 영역을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![포털의 진단 로그 결과](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="80895-190">진단 설정을 추가하면 진단 설정 뷰가 표시되고, 여기에서 선택한 리소스에 대한 진단 설정을 활성화, 비활성화 또는 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80895-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="80895-191">리소스 진단 로그에 대해 지원되는 서비스, 범주 및 스키마</span><span class="sxs-lookup"><span data-stu-id="80895-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="80895-192">지원되는 서비스 및 해당 서비스에서 사용되는 로그 범주 및 스키마에 대한 전체 목록은 [이 문서를 참조](monitoring-diagnostic-logs-schema.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="80895-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80895-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80895-193">Next steps</span></span>

* [<span data-ttu-id="80895-194">**Event Hubs**로 리소스 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="80895-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="80895-195">Azure Monitor REST API를 사용하여 리소스 진단 설정 변경</span><span class="sxs-lookup"><span data-stu-id="80895-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="80895-196">Azure Storage에서 Log Analytics를 사용하여 로그 분석</span><span class="sxs-lookup"><span data-stu-id="80895-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
