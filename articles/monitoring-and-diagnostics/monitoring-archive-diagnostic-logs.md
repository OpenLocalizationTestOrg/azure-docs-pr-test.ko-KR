---
title: "Azure 진단 로그 aaaArchive | Microsoft Docs"
description: "어떻게 tooarchive 프로그램 Azure 로그 진단 로그를 저장소 계정에 대 한 장기 보존을 위해에 대해 알아봅니다."
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
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="5f2e7-103">Azure 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="5f2e7-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="5f2e7-104">CLI hello Azure 포털, PowerShell Cmdlet을 사용 하거나 REST API tooarchive 하는 방법 알아보겠습니다이 문서에서는 프로그램 [Azure 진단 로그](monitoring-overview-of-diagnostic-logs.md) 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, CLI, or REST API tooarchive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="5f2e7-105">이 옵션은 감사, 정적 분석 또는 백업에 대 한 선택적 보존 정책을 사용 하 여 진단 기록 tooretain 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-105">This option is useful if you would like tooretain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="5f2e7-106">저장소 계정 hello이 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 리소스와 같은 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-106">hello storage account does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f2e7-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5f2e7-107">Prerequisites</span></span>
<span data-ttu-id="5f2e7-108">시작 하기 전에 해야 너무[저장소 계정 만들기](../storage/storage-create-storage-account.md) toowhich 진단 로그를 보관할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-108">Before you begin, you need too[create a storage account](../storage/storage-create-storage-account.md) toowhich you can archive your diagnostic logs.</span></span> <span data-ttu-id="5f2e7-109">Toomonitoring 데이터 액세스를 더 잘 제어할 수 있도록에 저장 된 다른, 비 모니터링 데이터가 있는 기존 저장소 계정을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="5f2e7-110">그러나 또한 보관 하는 경우 작업 로그 및 진단 메트릭은 tooa 저장소 계정, 사항이 감지 toouse 해당 저장소 계정에 진단 로그에 tookeep 모든 모니터링 데이터를 중앙 위치에.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-110">However, if you are also archiving your Activity Log and diagnostic metrics tooa storage account, it may make sense toouse that storage account for your diagnostic logs as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="5f2e7-111">hello 사용 하는 저장소 계정에는 일반적인 용도의 스토리지 계정, blob 저장소 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="5f2e7-112">진단 설정</span><span class="sxs-lookup"><span data-stu-id="5f2e7-112">Diagnostic settings</span></span>
<span data-ttu-id="5f2e7-113">tooarchive 아래 hello 방법 중 하나를 사용 하 여 진단 로그, 설정한 한 **진단 설정** 특정 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-113">tooarchive your diagnostic logs using any of hello methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="5f2e7-114">메트릭 데이터 전송 (저장소 계정, 이벤트 허브 네임 스페이스 또는 로그 분석) tooa 대상 및 리소스에 대 한 진단 설정을 hello 범주의 로그를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-114">A diagnostic setting for a resource defines hello categories of logs and metric data sent tooa destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="5f2e7-115">또한 각 로그 범주와 저장소 계정에 저장 된 메트릭 데이터의 이벤트에 대 한 hello 보존 정책 (tooretain 일 수)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-115">It also defines hello retention policy (number of days tooretain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="5f2e7-116">Toozero 보존 정책이 설정 되어 해당 로그 범주에 대 한 이벤트는 무기한 저장 (즉, toosay 영원히).</span><span class="sxs-lookup"><span data-stu-id="5f2e7-116">If a retention policy is set toozero, events for that log category are stored indefinitely (that is toosay, forever).</span></span> <span data-ttu-id="5f2e7-117">그렇지 않은 경우 보존 정책은 1에서 2147483647 사이의 숫자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="5f2e7-118">[진단 설정에 대한 자세한 내용은 여기에서 확인할 수 있습니다](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="5f2e7-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="5f2e7-119">보존 정책이 적용 된 매일 많으면 hello 때 종료 시간 (UTC)는 이제 hello 보존 정책을 불가능 hello 날짜 로부터 기록 되므로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="5f2e7-120">예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="5f2e7-121">Hello 포털을 사용 하 여 진단 로그를 보관</span><span class="sxs-lookup"><span data-stu-id="5f2e7-121">Archive diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="5f2e7-122">Hello 포털 tooAzure 모니터를 탐색 하 고 클릭 **진단 설정**</span><span class="sxs-lookup"><span data-stu-id="5f2e7-122">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Azure Monitor의 모니터링 섹션](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="5f2e7-124">필요에 따라 리소스 그룹 또는 리소스 유형으로 hello 목록을 필터링 하려는 진단 설정 tooset hello 리소스 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-124">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="5f2e7-125">선택한 hello 리소스에 설정이 없는 있으면 증명된 toocreate 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-125">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="5f2e7-126">“진단 켜기”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-126">Click "Turn on diagnostics."</span></span>

   ![진단 설정 추가 - 기존 설정 없음](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="5f2e7-128">Hello 리소스에 대 한 기존 설정을 없을 경우이 리소스에서 이미 구성 되어 있는 설정 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-128">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="5f2e7-129">“진단 설정 추가”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-129">Click "Add diagnostic setting."</span></span>

   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="5f2e7-131">사용자 설정 이름을 지정 하 고 hello 확인란에 대 한 **tooStorage 계정 내보내기**, 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-131">Give your setting a name and check hello box for **Export tooStorage Account**, then select a storage account.</span></span> <span data-ttu-id="5f2e7-132">Hello를 사용 하 여 다양 한 일 tooretain 이러한 로그를 필요에 따라 설정 **보존 (일)** 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-132">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders.</span></span> <span data-ttu-id="5f2e7-133">0 일의 보존 hello 로그를 무기한으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-133">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![진단 설정 추가 - 기존 설정](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="5f2e7-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-135">Click **Save**.</span></span>

<span data-ttu-id="5f2e7-136">몇 분 후 hello 새 설정이이 리소스에 대 한 설정의 목록에 표시 되며 진단 로그 보관 된 toothat 저장소 계정으로 새 이벤트 데이터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-136">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are archived toothat storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="5f2e7-137">Azure PowerShell을 통한 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="5f2e7-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="5f2e7-138">속성</span><span class="sxs-lookup"><span data-stu-id="5f2e7-138">Property</span></span> | <span data-ttu-id="5f2e7-139">필수</span><span class="sxs-lookup"><span data-stu-id="5f2e7-139">Required</span></span> | <span data-ttu-id="5f2e7-140">설명</span><span class="sxs-lookup"><span data-stu-id="5f2e7-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f2e7-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="5f2e7-141">ResourceId</span></span> |<span data-ttu-id="5f2e7-142">예</span><span class="sxs-lookup"><span data-stu-id="5f2e7-142">Yes</span></span> |<span data-ttu-id="5f2e7-143">진단 설정을 tooset 원하는 hello 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-143">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="5f2e7-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="5f2e7-144">StorageAccountId</span></span> |<span data-ttu-id="5f2e7-145">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-145">No</span></span> |<span data-ttu-id="5f2e7-146">Hello 저장소 계정 toowhich 진단 로그의 리소스 ID는 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-146">Resource ID of hello Storage Account toowhich Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="5f2e7-147">범주</span><span class="sxs-lookup"><span data-stu-id="5f2e7-147">Categories</span></span> |<span data-ttu-id="5f2e7-148">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-148">No</span></span> |<span data-ttu-id="5f2e7-149">쉼표로 구분 된 목록 로그 범주 tooenable입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-149">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="5f2e7-150">사용</span><span class="sxs-lookup"><span data-stu-id="5f2e7-150">Enabled</span></span> |<span data-ttu-id="5f2e7-151">예</span><span class="sxs-lookup"><span data-stu-id="5f2e7-151">Yes</span></span> |<span data-ttu-id="5f2e7-152">이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="5f2e7-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="5f2e7-153">RetentionEnabled</span></span> |<span data-ttu-id="5f2e7-154">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-154">No</span></span> |<span data-ttu-id="5f2e7-155">이 리소스에 대한 보존 정책 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="5f2e7-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="5f2e7-156">RetentionInDays</span></span> |<span data-ttu-id="5f2e7-157">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-157">No</span></span> |<span data-ttu-id="5f2e7-158">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="5f2e7-159">값이 0 hello 로그를 무기한으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-159">A value of zero stores hello logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a><span data-ttu-id="5f2e7-160">플랫폼 간 CLI hello 통해 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="5f2e7-160">Archive diagnostic logs via hello Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="5f2e7-161">속성</span><span class="sxs-lookup"><span data-stu-id="5f2e7-161">Property</span></span> | <span data-ttu-id="5f2e7-162">필수</span><span class="sxs-lookup"><span data-stu-id="5f2e7-162">Required</span></span> | <span data-ttu-id="5f2e7-163">설명</span><span class="sxs-lookup"><span data-stu-id="5f2e7-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5f2e7-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="5f2e7-164">resourceId</span></span> |<span data-ttu-id="5f2e7-165">예</span><span class="sxs-lookup"><span data-stu-id="5f2e7-165">Yes</span></span> |<span data-ttu-id="5f2e7-166">진단 설정을 tooset 원하는 hello 리소스의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-166">Resource ID of hello resource on which you want tooset a diagnostic setting.</span></span> |
| <span data-ttu-id="5f2e7-167">storageId</span><span class="sxs-lookup"><span data-stu-id="5f2e7-167">storageId</span></span> |<span data-ttu-id="5f2e7-168">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-168">No</span></span> |<span data-ttu-id="5f2e7-169">Hello 저장소 계정 toowhich 진단 로그의 리소스 ID는 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-169">Resource ID of hello Storage Account toowhich diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="5f2e7-170">범주</span><span class="sxs-lookup"><span data-stu-id="5f2e7-170">categories</span></span> |<span data-ttu-id="5f2e7-171">아니요</span><span class="sxs-lookup"><span data-stu-id="5f2e7-171">No</span></span> |<span data-ttu-id="5f2e7-172">쉼표로 구분 된 목록 로그 범주 tooenable입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-172">Comma-separated list of log categories tooenable.</span></span> |
| <span data-ttu-id="5f2e7-173">사용</span><span class="sxs-lookup"><span data-stu-id="5f2e7-173">enabled</span></span> |<span data-ttu-id="5f2e7-174">예</span><span class="sxs-lookup"><span data-stu-id="5f2e7-174">Yes</span></span> |<span data-ttu-id="5f2e7-175">이 리소스에 대한 진단 활성화 여부를 나타내는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a><span data-ttu-id="5f2e7-176">Hello REST API를 통해 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="5f2e7-176">Archive diagnostic logs via hello REST API</span></span>
<span data-ttu-id="5f2e7-177">[이 문서를 참조 하십시오.](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) hello Azure 모니터 REST API를 사용 하 여 진단 설정을 설정 하는 방법에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using hello Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="5f2e7-178">Hello 저장소 계정에 진단 로그의 스키마</span><span class="sxs-lookup"><span data-stu-id="5f2e7-178">Schema of diagnostic logs in hello storage account</span></span>
<span data-ttu-id="5f2e7-179">한 아카이브를 설정한 후 사용 하도록 설정한 hello 로그 범주 중 하나에서 이벤트가 발생 하는 즉시 hello 저장소 계정에서 저장소 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-179">Once you have set up archival, a storage container is created in hello storage account as soon as an event occurs in one of hello log categories you have enabled.</span></span> <span data-ttu-id="5f2e7-180">hello 컨테이너 내 blob hello 진단 로그에서 동일한 형식 hello 및 hello 활동 로그를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-180">hello blobs within hello container follow hello same format across Diagnostic Logs and hello Activity Log.</span></span> <span data-ttu-id="5f2e7-181">이러한 blob의 hello 구조는.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-181">hello structure of these blobs is:</span></span>

> <span data-ttu-id="5f2e7-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5f2e7-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5f2e7-183">또는 더 간단하게</span><span class="sxs-lookup"><span data-stu-id="5f2e7-183">Or, more simply,</span></span>

> <span data-ttu-id="5f2e7-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5f2e7-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5f2e7-185">예를 들어 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="5f2e7-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5f2e7-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5f2e7-187">각 PT1H.json blob hello blob URL에 지정 된 hello 시간 이내에 발생 한 이벤트의 JSON blob에 포함 (예를 들어, h = 12).</span><span class="sxs-lookup"><span data-stu-id="5f2e7-187">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (for example, h=12).</span></span> <span data-ttu-id="5f2e7-188">현재 시간 hello 하는 동안 이벤트는 나타나는 순서 대로 추가 toohello PT1H.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-188">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="5f2e7-189">분 값 hello (m 00 =)는 항상 00, 이후 진단 로그 이벤트 1 시간 마다 각 blob으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-189">hello minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="5f2e7-190">Hello PT1H.json 파일 내에서 각 이벤트는이 형식에 따라 레코드"hello" 배열에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-190">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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

| <span data-ttu-id="5f2e7-191">요소 이름</span><span class="sxs-lookup"><span data-stu-id="5f2e7-191">Element name</span></span> | <span data-ttu-id="5f2e7-192">설명</span><span class="sxs-lookup"><span data-stu-id="5f2e7-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f2e7-193">실시간</span><span class="sxs-lookup"><span data-stu-id="5f2e7-193">time</span></span> |<span data-ttu-id="5f2e7-194">Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-194">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="5f2e7-195">resourceId</span><span class="sxs-lookup"><span data-stu-id="5f2e7-195">resourceId</span></span> |<span data-ttu-id="5f2e7-196">Hello의 리소스 ID 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-196">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="5f2e7-197">operationName</span><span class="sxs-lookup"><span data-stu-id="5f2e7-197">operationName</span></span> |<span data-ttu-id="5f2e7-198">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-198">Name of hello operation.</span></span> |
| <span data-ttu-id="5f2e7-199">카테고리</span><span class="sxs-lookup"><span data-stu-id="5f2e7-199">category</span></span> |<span data-ttu-id="5f2e7-200">Hello 이벤트의 로그 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-200">Log category of hello event.</span></span> |
| <span data-ttu-id="5f2e7-201">properties</span><span class="sxs-lookup"><span data-stu-id="5f2e7-201">properties</span></span> |<span data-ttu-id="5f2e7-202">설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (예: 사전).</span><span class="sxs-lookup"><span data-stu-id="5f2e7-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="5f2e7-203">hello 속성 및 해당 속성의 사용 현황 hello 리소스에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-203">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5f2e7-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f2e7-204">Next steps</span></span>
* [<span data-ttu-id="5f2e7-205">분석을 위한 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="5f2e7-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="5f2e7-206">스트림 진단 tooan 이벤트 허브 네임 스페이스를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2e7-206">Stream diagnostic logs tooan Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="5f2e7-207">진단 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5f2e7-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
