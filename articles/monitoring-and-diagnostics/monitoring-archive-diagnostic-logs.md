---
title: "Azure 진단 로그 보관 | Microsoft Docs"
description: "저장소 계정에 장기 보존을 위해 Azure 진단 로그를 보관하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: dbc5f89001dcb6cd1ab061cb0a9632e4e5d2c1c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="22ed9-103">Azure 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="22ed9-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="22ed9-104">이 문서에서는 Azure Portal, PowerShell Cmdlet, CLI 또는 REST API를 사용하여 저장소 계정에서 [Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md)를 보관하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="22ed9-105">이 옵션은 감사, 정적 분석 또는 백업을 위해 옵션 보존 정책으로 진단 로그를 유지하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-105">This option is useful if you would like to retain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="22ed9-106">설정을 구성하는 사용자가 두 구독에 대한 적절한 RBAC 액세스를 가진 경우 저장소 계정은 로그를 내보내는 리소스와 동일한 구독을 가지고 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22ed9-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22ed9-107">Prerequisites</span></span>
<span data-ttu-id="22ed9-108">시작하기 전에 진단 로그를 보관할 수 있는 [저장소 계정을 만들어야](../storage/storage-create-storage-account.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md) to which you can archive your diagnostic logs.</span></span> <span data-ttu-id="22ed9-109">모니터링 데이터에 대한 액세스를 보다 잘 제어할 수 있도록 다른 비 모니터링 데이터가 저장된 기존 저장소 계정을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="22ed9-110">그러나 저장소 계정에 대한 활동 로그 및 진단 메트릭을 보관하는 경우 중앙 위치에서 모든 모니터링 데이터를 유지하도록 진단 로그에 대해 해당 저장소 계정을 사용하는 것이 합리적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your diagnostic logs as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="22ed9-111">사용하는 저장소 계정은 Blob 저장소 계정이 아닌 범용 저장소 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="22ed9-112">진단 설정</span><span class="sxs-lookup"><span data-stu-id="22ed9-112">Diagnostic settings</span></span>
<span data-ttu-id="22ed9-113">다음 방법 중 하나를 사용하여 진단 로그를 보관하려면 특정 리소스에 대한 **진단 설정**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-113">To archive your diagnostic logs using any of the methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="22ed9-114">리소스에 대한 진단 설정은 대상에 전송되는 로그 및 메트릭 데이터의 범주를 정의합니다(저장소 계정, Event Hubs 네임스페이스 또는 Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="22ed9-114">A diagnostic setting for a resource defines the categories of logs and metric data sent to a destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="22ed9-115">또한 저장소 계정에 저장되는 각 로그 범주 및 메트릭 데이터의 이벤트에 대한 보존 정책(보존할 일 수)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-115">It also defines the retention policy (number of days to retain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="22ed9-116">보존 정책이 0으로 설정된 경우 해당 로그 범주에 대한 이벤트는 무기한으로(즉, 영원히) 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span></span> <span data-ttu-id="22ed9-117">그렇지 않은 경우 보존 정책은 1에서 2147483647 사이의 숫자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="22ed9-118">[진단 설정에 대한 자세한 내용은 여기에서 확인할 수 있습니다](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="22ed9-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="22ed9-119">보존 정책은 매일 적용되므로 하루의 마지막에(UTC) 보존 정책이 지난 날의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="22ed9-120">예를 들어, 하루의 보존 정책이 있는 경우 오늘 날짜가 시작될 때 하루 전의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-the-portal"></a><span data-ttu-id="22ed9-121">포털을 사용하여 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="22ed9-121">Archive diagnostic logs using the portal</span></span>
1. <span data-ttu-id="22ed9-122">포털에서 Azure Monitor로 이동하고 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure Monitor의 모니터링 섹션](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="22ed9-124">필요에 따라 리소스 그룹 또는 리소스 종류를 기준으로 목록을 필터링합니다. 그런 다음 진단 설정을 지정하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="22ed9-125">선택한 리소스에 설정이 없는 경우, 설정을 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="22ed9-126">“진단 켜기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-126">Click "Turn on diagnostics."</span></span>

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="22ed9-128">리소스에 기존 설정이 있는 경우 이 리소스에 이미 구성된 설정의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="22ed9-129">“진단 설정 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-129">Click "Add diagnostic setting."</span></span>

   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="22ed9-131">설정에 이름을 지정하고  **계정에 내보내기** 확인란을 선택한 다음 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-131">Give your setting a name and check the box for **Export to Storage Account**, then select a storage account.</span></span> <span data-ttu-id="22ed9-132">필요에 따라 **보존(일)** 슬라이더를 사용하여 이러한 로그를 유지할 일 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-132">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span></span> <span data-ttu-id="22ed9-133">0일의 보존은 로그를 무기한 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-133">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="22ed9-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-135">Click **Save**.</span></span>

<span data-ttu-id="22ed9-136">몇 분 후 새 설정이 이 리소스에 대한 설정 목록에 표시되고, 새 이벤트 데이터가 생성되는 즉시 진단 로그가 해당 저장소 계정에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-136">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are archived to that storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="22ed9-137">Azure PowerShell을 통한 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="22ed9-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="22ed9-138">속성</span><span class="sxs-lookup"><span data-stu-id="22ed9-138">Property</span></span> | <span data-ttu-id="22ed9-139">필수</span><span class="sxs-lookup"><span data-stu-id="22ed9-139">Required</span></span> | <span data-ttu-id="22ed9-140">설명</span><span class="sxs-lookup"><span data-stu-id="22ed9-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22ed9-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="22ed9-141">ResourceId</span></span> |<span data-ttu-id="22ed9-142">예</span><span class="sxs-lookup"><span data-stu-id="22ed9-142">Yes</span></span> |<span data-ttu-id="22ed9-143">진단 설정을 설정하려는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-143">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="22ed9-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="22ed9-144">StorageAccountId</span></span> |<span data-ttu-id="22ed9-145">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-145">No</span></span> |<span data-ttu-id="22ed9-146">진단 로그를 저장할 저장소 계정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-146">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="22ed9-147">범주</span><span class="sxs-lookup"><span data-stu-id="22ed9-147">Categories</span></span> |<span data-ttu-id="22ed9-148">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-148">No</span></span> |<span data-ttu-id="22ed9-149">활성화할 로그 범주의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-149">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="22ed9-150">사용</span><span class="sxs-lookup"><span data-stu-id="22ed9-150">Enabled</span></span> |<span data-ttu-id="22ed9-151">예</span><span class="sxs-lookup"><span data-stu-id="22ed9-151">Yes</span></span> |<span data-ttu-id="22ed9-152">이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="22ed9-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="22ed9-153">RetentionEnabled</span></span> |<span data-ttu-id="22ed9-154">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-154">No</span></span> |<span data-ttu-id="22ed9-155">이 리소스에 대한 보존 정책 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="22ed9-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="22ed9-156">RetentionInDays</span></span> |<span data-ttu-id="22ed9-157">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-157">No</span></span> |<span data-ttu-id="22ed9-158">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="22ed9-159">0 값은 로그를 무기한 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-159">A value of zero stores the logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-the-cross-platform-cli"></a><span data-ttu-id="22ed9-160">플랫폼 간 CLI를 통한 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="22ed9-160">Archive diagnostic logs via the Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="22ed9-161">속성</span><span class="sxs-lookup"><span data-stu-id="22ed9-161">Property</span></span> | <span data-ttu-id="22ed9-162">필수</span><span class="sxs-lookup"><span data-stu-id="22ed9-162">Required</span></span> | <span data-ttu-id="22ed9-163">설명</span><span class="sxs-lookup"><span data-stu-id="22ed9-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22ed9-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="22ed9-164">resourceId</span></span> |<span data-ttu-id="22ed9-165">예</span><span class="sxs-lookup"><span data-stu-id="22ed9-165">Yes</span></span> |<span data-ttu-id="22ed9-166">진단 설정을 설정하려는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-166">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="22ed9-167">storageId</span><span class="sxs-lookup"><span data-stu-id="22ed9-167">storageId</span></span> |<span data-ttu-id="22ed9-168">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-168">No</span></span> |<span data-ttu-id="22ed9-169">진단 로그를 저장할 Storage 계정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-169">Resource ID of the Storage Account to which diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="22ed9-170">범주</span><span class="sxs-lookup"><span data-stu-id="22ed9-170">categories</span></span> |<span data-ttu-id="22ed9-171">아니요</span><span class="sxs-lookup"><span data-stu-id="22ed9-171">No</span></span> |<span data-ttu-id="22ed9-172">활성화할 로그 범주의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-172">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="22ed9-173">사용</span><span class="sxs-lookup"><span data-stu-id="22ed9-173">enabled</span></span> |<span data-ttu-id="22ed9-174">예</span><span class="sxs-lookup"><span data-stu-id="22ed9-174">Yes</span></span> |<span data-ttu-id="22ed9-175">이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-the-rest-api"></a><span data-ttu-id="22ed9-176">REST API를 통한 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="22ed9-176">Archive diagnostic logs via the REST API</span></span>
<span data-ttu-id="22ed9-177">Azure Monitor REST API를 사용하여 진단 설정을 설정할 수는 방법에 대한 내용은 [이 문서를 참조](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings)하세요.</span><span class="sxs-lookup"><span data-stu-id="22ed9-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="22ed9-178">저장소 계정의 진단 로그 스키마</span><span class="sxs-lookup"><span data-stu-id="22ed9-178">Schema of diagnostic logs in the storage account</span></span>
<span data-ttu-id="22ed9-179">보관을 설정한 후 활성화한 로그 범주 중 하나에서 이벤트가 발생하는 즉시 저장소 계정에 저장소 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-179">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span></span> <span data-ttu-id="22ed9-180">컨테이너 내의 Blob은 진단 로그 및 활동 로그와 동일한 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-180">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span></span> <span data-ttu-id="22ed9-181">해당 Blob의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-181">The structure of these blobs is:</span></span>

> <span data-ttu-id="22ed9-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="22ed9-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="22ed9-183">또는 더 간단하게</span><span class="sxs-lookup"><span data-stu-id="22ed9-183">Or, more simply,</span></span>

> <span data-ttu-id="22ed9-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="22ed9-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="22ed9-185">예를 들어 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="22ed9-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="22ed9-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="22ed9-187">각 PT1H.json Blob은 Blob URL에 지정된 시간 내에서 발생한 이벤트의 JSON Blob을 포함합니다(예: h=12).</span><span class="sxs-lookup"><span data-stu-id="22ed9-187">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="22ed9-188">현재 시간 동안 이벤트는 발생하는 순서대로 PT1H.json 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-188">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="22ed9-189">진단 로그 이벤트는 시간당 개별 Blob으로 나뉘므로 분 값(m=00)은 항상 00입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-189">The minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="22ed9-190">PT1H.json 파일 내에서 각 이벤트는 이 형식에 따라 "레코드" 배열에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-190">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="22ed9-191">요소 이름</span><span class="sxs-lookup"><span data-stu-id="22ed9-191">Element name</span></span> | <span data-ttu-id="22ed9-192">설명</span><span class="sxs-lookup"><span data-stu-id="22ed9-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22ed9-193">실시간</span><span class="sxs-lookup"><span data-stu-id="22ed9-193">time</span></span> |<span data-ttu-id="22ed9-194">이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-194">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="22ed9-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="22ed9-195">resourceId</span></span> |<span data-ttu-id="22ed9-196">영향을 받는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-196">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="22ed9-197">operationName</span><span class="sxs-lookup"><span data-stu-id="22ed9-197">operationName</span></span> |<span data-ttu-id="22ed9-198">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-198">Name of the operation.</span></span> |
| <span data-ttu-id="22ed9-199">카테고리</span><span class="sxs-lookup"><span data-stu-id="22ed9-199">category</span></span> |<span data-ttu-id="22ed9-200">이벤트의 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-200">Log category of the event.</span></span> |
| <span data-ttu-id="22ed9-201">properties</span><span class="sxs-lookup"><span data-stu-id="22ed9-201">properties</span></span> |<span data-ttu-id="22ed9-202">이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="22ed9-203">해당 속성의 속성 및 사용은 리소스에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ed9-203">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="22ed9-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22ed9-204">Next steps</span></span>
* [<span data-ttu-id="22ed9-205">분석을 위한 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="22ed9-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="22ed9-206">Event Hubs 네임스페이스로 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="22ed9-206">Stream diagnostic logs to an Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="22ed9-207">진단 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="22ed9-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
