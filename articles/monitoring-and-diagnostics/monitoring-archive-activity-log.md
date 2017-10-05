---
title: "Azure 활동 로그 보관 | Microsoft Docs"
description: "저장소 계정에 장기 보존을 위해 Azure 활동 로그를 보관하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="0409a-103">Azure 활동 로그 보관</span><span class="sxs-lookup"><span data-stu-id="0409a-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="0409a-104">이 문서에서는 Azure 포털, PowerShell Cmdlet 또는 플랫폼 간 CLI를 사용하여 저장소 계정에서 [**Azure 활동 로그**](monitoring-overview-activity-logs.md)를 보관하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="0409a-105">이 옵션은 감사, 정적 분석 또는 백업을 위해 활동 로그를 90일 이상(보존 정책에 대해 모든 권한으로) 유지하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="0409a-106">90일 이내로 이벤트를 보관해야 하는 경우 활동 로그는 보관 활성화 없이 Azure 플랫폼에 90일 동안 보관되므로 저장소 계정에 보관을 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0409a-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0409a-107">Prerequisites</span></span>
<span data-ttu-id="0409a-108">시작하기 전에 활동 로그를 보관하려면 [저장소 계정을 만들](../storage/common/storage-create-storage-account.md#create-a-storage-account) 어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="0409a-109">모니터링 데이터에 대한 액세스를 보다 잘 제어할 수 있도록 다른 비 모니터링 데이터가 저장된 기존 저장소 계정을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="0409a-110">그러나 저장소 계정에 대한 진단 로그 및 메트릭을 보관하는 경우 중앙 위치에서 모든 모니터링 데이터를 유지하도록 활동 로그에 대해 해당 저장소 계정을 사용하는 것이 합리적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="0409a-111">사용하는 저장소 계정은 Blob 저장소 계정이 아닌 범용 저장소 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="0409a-112">설정을 구성하는 사용자가 두 구독에 대한 적절한 RBAC 액세스를 가진 경우 저장소 계정은 로그를 내보내는 구독과 동일한 구독을 가지고 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="0409a-113">로그 프로필</span><span class="sxs-lookup"><span data-stu-id="0409a-113">Log Profile</span></span>
<span data-ttu-id="0409a-114">다음 방법 중 하나를 사용하여 활동 로그를 보관하려면 구독에 대해 **로그 프로필** 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="0409a-115">로그 프로필은 저장 또는 스트리밍되는 이벤트 및 출력(저장소 계정 및/또는 이벤트 허브)의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="0409a-116">또한 저장소 계정에 저장되는 이벤트에 대한 보존 정책(보존할 일 수)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="0409a-117">보존 정책이 0으로 설정된 경우 이벤트 무기한으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="0409a-118">그렇지 않으면 1에서 2147483647 사이의 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="0409a-119">보존 정책은 매일 적용되므로 하루의 마지막에(UTC) 보존 정책이 지난 날의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="0409a-120">예를 들어, 하루의 보존 정책이 있는 경우 오늘 날짜가 시작될 때 하루 전의 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="0409a-121">[여기에서 로그 프로필에 대한 자세한 내용을 확인할 수 있습니다](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="0409a-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="0409a-122">포털을 사용하여 활동 로그 보관</span><span class="sxs-lookup"><span data-stu-id="0409a-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="0409a-123">포털의 왼쪽 탐색에서 **활동 로그** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="0409a-124">활동 로그에 대한 링크가 보이지 않으면 **더 많은 서비스** 링크를 먼저 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![활동 로그 블레이드로 이동](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="0409a-126">블레이드 맨 위에서 **내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-126">At the top of the blade, click **Export**.</span></span>
   
    ![내보내기 단추 클릭](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="0409a-128">표시되는 블레이드에서 **저장소 계정에 내보내기** 에 대한 상자를 선택하고 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![저장소 계정 설정](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="0409a-130">슬라이더 또는 텍스트 상자를 사용하여 저장소 계정에 활동 로그 이벤트를 보관해야 할 일 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="0409a-131">데이터를 저장소 계정에 무기한으로 유지하려는 경우 이 숫자를 0으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="0409a-132">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="0409a-133">PowerShell을 통해 활동 로그 보관</span><span class="sxs-lookup"><span data-stu-id="0409a-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="0409a-134">속성</span><span class="sxs-lookup"><span data-stu-id="0409a-134">Property</span></span> | <span data-ttu-id="0409a-135">필수</span><span class="sxs-lookup"><span data-stu-id="0409a-135">Required</span></span> | <span data-ttu-id="0409a-136">설명</span><span class="sxs-lookup"><span data-stu-id="0409a-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0409a-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="0409a-137">StorageAccountId</span></span> |<span data-ttu-id="0409a-138">아니요</span><span class="sxs-lookup"><span data-stu-id="0409a-138">No</span></span> |<span data-ttu-id="0409a-139">활동 로그를 저장할 저장소 계정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="0409a-140">위치</span><span class="sxs-lookup"><span data-stu-id="0409a-140">Locations</span></span> |<span data-ttu-id="0409a-141">예</span><span class="sxs-lookup"><span data-stu-id="0409a-141">Yes</span></span> |<span data-ttu-id="0409a-142">활동 로그 이벤트를 수집할 쉼표로 구분된 지역 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="0409a-143">[이 페이지를 방문](https://azure.microsoft.com/en-us/regions)하거나 [Azure 관리 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)를 사용하여 모든 지역의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="0409a-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="0409a-144">RetentionInDays</span></span> |<span data-ttu-id="0409a-145">예</span><span class="sxs-lookup"><span data-stu-id="0409a-145">Yes</span></span> |<span data-ttu-id="0409a-146">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="0409a-147">0 값은 로그를 무기한(영원히) 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="0409a-148">범주</span><span class="sxs-lookup"><span data-stu-id="0409a-148">Categories</span></span> |<span data-ttu-id="0409a-149">예</span><span class="sxs-lookup"><span data-stu-id="0409a-149">Yes</span></span> |<span data-ttu-id="0409a-150">수집할 쉼표로 구분된 이벤트 범주 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="0409a-151">가능한 값은 쓰기, 삭제 및 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="0409a-152">CLI를 통해 활동 로그 보관</span><span class="sxs-lookup"><span data-stu-id="0409a-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="0409a-153">속성</span><span class="sxs-lookup"><span data-stu-id="0409a-153">Property</span></span> | <span data-ttu-id="0409a-154">필수</span><span class="sxs-lookup"><span data-stu-id="0409a-154">Required</span></span> | <span data-ttu-id="0409a-155">설명</span><span class="sxs-lookup"><span data-stu-id="0409a-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0409a-156">name</span><span class="sxs-lookup"><span data-stu-id="0409a-156">name</span></span> |<span data-ttu-id="0409a-157">예</span><span class="sxs-lookup"><span data-stu-id="0409a-157">Yes</span></span> |<span data-ttu-id="0409a-158">로그 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-158">Name of your log profile.</span></span> |
| <span data-ttu-id="0409a-159">storageId</span><span class="sxs-lookup"><span data-stu-id="0409a-159">storageId</span></span> |<span data-ttu-id="0409a-160">아니요</span><span class="sxs-lookup"><span data-stu-id="0409a-160">No</span></span> |<span data-ttu-id="0409a-161">활동 로그를 저장할 저장소 계정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="0409a-162">위치</span><span class="sxs-lookup"><span data-stu-id="0409a-162">locations</span></span> |<span data-ttu-id="0409a-163">예</span><span class="sxs-lookup"><span data-stu-id="0409a-163">Yes</span></span> |<span data-ttu-id="0409a-164">활동 로그 이벤트를 수집할 쉼표로 구분된 지역 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="0409a-165">[이 페이지를 방문](https://azure.microsoft.com/en-us/regions)하거나 [Azure 관리 REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx)를 사용하여 모든 지역의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="0409a-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="0409a-166">retentionInDays</span></span> |<span data-ttu-id="0409a-167">예</span><span class="sxs-lookup"><span data-stu-id="0409a-167">Yes</span></span> |<span data-ttu-id="0409a-168">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="0409a-169">0 값은 로그를 무기한(영원히) 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="0409a-170">범주</span><span class="sxs-lookup"><span data-stu-id="0409a-170">categories</span></span> |<span data-ttu-id="0409a-171">예</span><span class="sxs-lookup"><span data-stu-id="0409a-171">Yes</span></span> |<span data-ttu-id="0409a-172">수집할 쉼표로 구분된 이벤트 범주 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="0409a-173">가능한 값은 쓰기, 삭제 및 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="0409a-174">활동 로그의 저장소 스키마</span><span class="sxs-lookup"><span data-stu-id="0409a-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="0409a-175">보관을 설정한 후 활동 로그 이벤트가 발생하는 즉시 저장소 계정에 저장소 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="0409a-176">컨테이너 내의 Blob은 활동 로그 및 진단 로그와 동일한 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="0409a-177">해당 Blob의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="0409a-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="0409a-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="0409a-179">예를 들어 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="0409a-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="0409a-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="0409a-181">각 PT1H.json Blob은 Blob URL에 지정된 시간 내에서 발생한 이벤트의 JSON Blob을 포함합니다(예: h=12).</span><span class="sxs-lookup"><span data-stu-id="0409a-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="0409a-182">현재 시간 동안 이벤트는 발생하는 순서대로 PT1H.json 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="0409a-183">활동 로그 이벤트는 시간당 개별 Blob으로 나뉘므로 분 값(m=00)은 항상 00입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="0409a-184">PT1H.json 파일 내에서 각 이벤트는 이 형식에 따라 "레코드" 배열에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="0409a-185">요소 이름</span><span class="sxs-lookup"><span data-stu-id="0409a-185">Element name</span></span> | <span data-ttu-id="0409a-186">설명</span><span class="sxs-lookup"><span data-stu-id="0409a-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0409a-187">실시간</span><span class="sxs-lookup"><span data-stu-id="0409a-187">time</span></span> |<span data-ttu-id="0409a-188">이벤트에 해당하는 요청을 처리한 Azure 서비스에 의해 이벤트가 생성된 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="0409a-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="0409a-189">resourceId</span></span> |<span data-ttu-id="0409a-190">영향을 받는 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="0409a-191">operationName</span><span class="sxs-lookup"><span data-stu-id="0409a-191">operationName</span></span> |<span data-ttu-id="0409a-192">작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-192">Name of the operation.</span></span> |
| <span data-ttu-id="0409a-193">카테고리</span><span class="sxs-lookup"><span data-stu-id="0409a-193">category</span></span> |<span data-ttu-id="0409a-194">작업의 범주</span><span class="sxs-lookup"><span data-stu-id="0409a-194">Category of the action, eg.</span></span> <span data-ttu-id="0409a-195">(예: 쓰기, 읽기, 작업)</span><span class="sxs-lookup"><span data-stu-id="0409a-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="0409a-196">resultType</span><span class="sxs-lookup"><span data-stu-id="0409a-196">resultType</span></span> |<span data-ttu-id="0409a-197">결과의 형식</span><span class="sxs-lookup"><span data-stu-id="0409a-197">The type of the result, eg.</span></span> <span data-ttu-id="0409a-198">(예: 성공, 실패, 시작)</span><span class="sxs-lookup"><span data-stu-id="0409a-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="0409a-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="0409a-199">resultSignature</span></span> |<span data-ttu-id="0409a-200">리소스 종류에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="0409a-201">durationMS</span><span class="sxs-lookup"><span data-stu-id="0409a-201">durationMs</span></span> |<span data-ttu-id="0409a-202">밀리초 단위의 작업 기간</span><span class="sxs-lookup"><span data-stu-id="0409a-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="0409a-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="0409a-203">callerIpAddress</span></span> |<span data-ttu-id="0409a-204">가용성을 기반으로 작업, UPN 클레임 또는 SPN 클레임을 수행한 사용자의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="0409a-205">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="0409a-205">correlationId</span></span> |<span data-ttu-id="0409a-206">일반적으로 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="0409a-207">동일한 uber 작업에 속하는 correlationId를 공유하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="0409a-208">ID</span><span class="sxs-lookup"><span data-stu-id="0409a-208">identity</span></span> |<span data-ttu-id="0409a-209">권한 부여 및 클레임을 설명하는 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="0409a-210">권한 부여</span><span class="sxs-lookup"><span data-stu-id="0409a-210">authorization</span></span> |<span data-ttu-id="0409a-211">이벤트의 RBAC 속성 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="0409a-212">일반적으로 "action", "role" 및 "scope" 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="0409a-213">level</span><span class="sxs-lookup"><span data-stu-id="0409a-213">level</span></span> |<span data-ttu-id="0409a-214">이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-214">Level of the event.</span></span> <span data-ttu-id="0409a-215">다음 값 중 하나: “Critical”, “Error”, “Warning”, “Informational” 및 “Verbose”</span><span class="sxs-lookup"><span data-stu-id="0409a-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="0409a-216">location</span><span class="sxs-lookup"><span data-stu-id="0409a-216">location</span></span> |<span data-ttu-id="0409a-217">발생하는 위치의 지역(또는 전역)입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="0409a-218">properties</span><span class="sxs-lookup"><span data-stu-id="0409a-218">properties</span></span> |<span data-ttu-id="0409a-219">이벤트에 대한 세부 정보를 설명하는 `<Key, Value>` 쌍의 집합(즉, 사전)입니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="0409a-220">해당 속성의 속성 및 사용은 리소스에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0409a-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0409a-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0409a-221">Next steps</span></span>
* [<span data-ttu-id="0409a-222">분석을 위한 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="0409a-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="0409a-223">활동 로그를 이벤트 허브로 스트리밍</span><span class="sxs-lookup"><span data-stu-id="0409a-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="0409a-224">활동 로그에 대한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="0409a-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

