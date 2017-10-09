---
title: "Azure 활동 로그 aaaArchive hello | Microsoft Docs"
description: "Tooarchive Azure 활동 로그 하는 방법은 저장소 계정에 대 한 장기 보존을 위해에 대해 알아봅니다."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="baa56-103">Hello Azure 활동 로그를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="baa56-104">이 문서에서는 hello Azure 포털, PowerShell Cmdlet 또는 플랫폼 간 CLI tooarchive를 사용 하는 방법을 보여줍니다 프로그램 [ **Azure 활동 로그** ](monitoring-overview-activity-logs.md) 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="baa56-105">이 옵션에 대 한 hello 보존 정책에 대해 모든 권한) (있음 90 일 이상 활동 로그 분석 정적 분석 또는 백업 tooretain 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="baa56-106">Tooretain만 필요한 경우 작업 로그 이벤트를 보존할 hello Azure 플랫폼에서에서 90 일 동안 보관을 사용 하지 않고 이후 90 일 동안 개 이하인 이벤트 tooset tooa 보관 저장소 계정이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa56-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="baa56-107">Prerequisites</span></span>
<span data-ttu-id="baa56-108">시작 하기 전에 해야 너무[저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich 활동 로그를 보관할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="baa56-109">Toomonitoring 데이터 액세스를 더 잘 제어할 수 있도록에 저장 된 다른, 비 모니터링 데이터가 있는 기존 저장소 계정을 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="baa56-110">그러나 또한 보관 하는 경우 진단 로그 및 메트릭 tooa 저장소 계정, 사항이 감지 toouse 해당 저장소 계정 로그에 대 한 활동도 tookeep 모든 모니터링 데이터를 중앙 위치에.</span><span class="sxs-lookup"><span data-stu-id="baa56-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="baa56-111">hello 사용 하는 저장소 계정에는 일반적인 용도의 스토리지 계정, blob 저장소 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="baa56-112">저장소 계정 hello이 없는 toobe hello hello 설정을 구성 하는 hello 사용자에 게 적합 한 RBAC 액세스 tooboth 구독으로 로그를 내보내는 hello 구독과 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="baa56-113">로그 프로필</span><span class="sxs-lookup"><span data-stu-id="baa56-113">Log Profile</span></span>
<span data-ttu-id="baa56-114">hello 설정 tooarchive hello 아래 hello 방법 중 하나를 사용 하 여 활동 로그, **로그 프로필** 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="baa56-115">hello 로그 프로필 hello 형식의 저장 되는지 아니면 스트리밍되는지를 하는 이벤트를 정의 하 고 출력 hello-저장소 계정 및/또는 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="baa56-116">또한 저장소 계정에 저장 된 이벤트에 대 한 hello 보존 정책 (tooretain 일 수)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="baa56-117">Hello 보존 정책이 toozero 설정 되 면 이벤트 무기한 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="baa56-118">그렇지 않은 경우이 수 값을 설정할 수 tooany 1과 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="baa56-119">보존 정책이 적용 된 매일 많으면 hello 때 종료 시간 (UTC)는 이제 hello 보존 정책을 불가능 hello 날짜 로부터 기록 되므로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="baa56-120">예를 들어 1 일의 보존 정책의 설치한 경우 hello 하루의 오늘 hello 시작 부분에 hello hello 이틀 전에서에서 로그 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="baa56-121">[여기에서 로그 프로필에 대한 자세한 내용을 확인할 수 있습니다](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="baa56-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="baa56-122">보관 hello hello 포털을 사용 하 여 활동 로그</span><span class="sxs-lookup"><span data-stu-id="baa56-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="baa56-123">Hello 포털에서을 클릭 hello **활동 로그** hello 왼쪽 탐색 모음에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="baa56-124">활동 로그 hello에 대 한 링크 보이지 않으면 클릭 hello **더 서비스** 먼저 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![TooActivity 로그 블레이드를 탐색 합니다.](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="baa56-126">Hello 블레이드의 hello 위쪽 클릭 **내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Hello 내보내기 단추를 클릭 합니다.](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="baa56-128">표시 되는 hello 블레이드에서 확인란 hello에 대 한 **tooa 저장소 계정을 내보내기** 하 고 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![저장소 계정 설정](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="baa56-130">Hello 슬라이더 또는 텍스트 상자를 사용 하 여, 정의할을 저장소 계정에 이벤트 활동 로그를 보관할 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="baa56-131">데이터 무기한 hello 저장소 계정에 유지 toohave 선호 하는 경우이 숫자 toozero를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="baa56-132">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="baa56-133">Hello PowerShell 통해 활동 로그를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="baa56-134">속성</span><span class="sxs-lookup"><span data-stu-id="baa56-134">Property</span></span> | <span data-ttu-id="baa56-135">필수</span><span class="sxs-lookup"><span data-stu-id="baa56-135">Required</span></span> | <span data-ttu-id="baa56-136">설명</span><span class="sxs-lookup"><span data-stu-id="baa56-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baa56-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="baa56-137">StorageAccountId</span></span> |<span data-ttu-id="baa56-138">아니요</span><span class="sxs-lookup"><span data-stu-id="baa56-138">No</span></span> |<span data-ttu-id="baa56-139">저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="baa56-140">위치</span><span class="sxs-lookup"><span data-stu-id="baa56-140">Locations</span></span> |<span data-ttu-id="baa56-141">예</span><span class="sxs-lookup"><span data-stu-id="baa56-141">Yes</span></span> |<span data-ttu-id="baa56-142">쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="baa56-143">지역 모두의 목록을 볼 수 있습니다 [이 페이지를 방문 하 여](https://azure.microsoft.com/en-us/regions) 또는 사용 하 여 [Azure 관리 REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="baa56-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="baa56-144">RetentionInDays</span></span> |<span data-ttu-id="baa56-145">예</span><span class="sxs-lookup"><span data-stu-id="baa56-145">Yes</span></span> |<span data-ttu-id="baa56-146">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="baa56-147">Hello 로그를 무기한으로 저장 값이 0 (무제한).</span><span class="sxs-lookup"><span data-stu-id="baa56-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="baa56-148">범주</span><span class="sxs-lookup"><span data-stu-id="baa56-148">Categories</span></span> |<span data-ttu-id="baa56-149">예</span><span class="sxs-lookup"><span data-stu-id="baa56-149">Yes</span></span> |<span data-ttu-id="baa56-150">수집할 쉼표로 구분된 이벤트 범주 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="baa56-151">가능한 값은 쓰기, 삭제 및 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="baa56-152">Hello CLI 통해 활동 로그를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="baa56-153">속성</span><span class="sxs-lookup"><span data-stu-id="baa56-153">Property</span></span> | <span data-ttu-id="baa56-154">필수</span><span class="sxs-lookup"><span data-stu-id="baa56-154">Required</span></span> | <span data-ttu-id="baa56-155">설명</span><span class="sxs-lookup"><span data-stu-id="baa56-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baa56-156">name</span><span class="sxs-lookup"><span data-stu-id="baa56-156">name</span></span> |<span data-ttu-id="baa56-157">예</span><span class="sxs-lookup"><span data-stu-id="baa56-157">Yes</span></span> |<span data-ttu-id="baa56-158">로그 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-158">Name of your log profile.</span></span> |
| <span data-ttu-id="baa56-159">storageId</span><span class="sxs-lookup"><span data-stu-id="baa56-159">storageId</span></span> |<span data-ttu-id="baa56-160">아니요</span><span class="sxs-lookup"><span data-stu-id="baa56-160">No</span></span> |<span data-ttu-id="baa56-161">저장소 계정 toowhich hello 활동 로그의 리소스 ID는 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="baa56-162">위치</span><span class="sxs-lookup"><span data-stu-id="baa56-162">locations</span></span> |<span data-ttu-id="baa56-163">예</span><span class="sxs-lookup"><span data-stu-id="baa56-163">Yes</span></span> |<span data-ttu-id="baa56-164">쉼표로 구분 된 목록 하려는 toocollect 활동 로그 이벤트는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="baa56-165">지역 모두의 목록을 볼 수 있습니다 [이 페이지를 방문 하 여](https://azure.microsoft.com/en-us/regions) 또는 사용 하 여 [Azure 관리 REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="baa56-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="baa56-166">retentionInDays</span></span> |<span data-ttu-id="baa56-167">예</span><span class="sxs-lookup"><span data-stu-id="baa56-167">Yes</span></span> |<span data-ttu-id="baa56-168">이벤트를 유지해야 하는 일 수는 1에서 2147483647 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="baa56-169">값이 0 hello 로그를 무기한으로 저장 됩니다 (계속).</span><span class="sxs-lookup"><span data-stu-id="baa56-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="baa56-170">범주</span><span class="sxs-lookup"><span data-stu-id="baa56-170">categories</span></span> |<span data-ttu-id="baa56-171">예</span><span class="sxs-lookup"><span data-stu-id="baa56-171">Yes</span></span> |<span data-ttu-id="baa56-172">수집할 쉼표로 구분된 이벤트 범주 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="baa56-173">가능한 값은 쓰기, 삭제 및 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="baa56-174">저장소 스키마의 hello 활동 로그</span><span class="sxs-lookup"><span data-stu-id="baa56-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="baa56-175">설정한 후 보관, 작업 로그 이벤트가 발생 하는 즉시 저장소 컨테이너 hello 저장소 계정에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="baa56-176">hello 컨테이너 내 blob hello hello hello 활동 로그 및 진단 로그에서 동일한 형식에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="baa56-177">이러한 blob의 hello 구조는.</span><span class="sxs-lookup"><span data-stu-id="baa56-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="baa56-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="baa56-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="baa56-179">예를 들어 Blob 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="baa56-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="baa56-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="baa56-181">각 PT1H.json blob hello blob URL에 지정 된 hello 시간 이내에 발생 한 이벤트의 JSON blob에 포함 (예: h = 12).</span><span class="sxs-lookup"><span data-stu-id="baa56-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="baa56-182">현재 시간 hello 하는 동안 이벤트는 나타나는 순서 대로 추가 toohello PT1H.json 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="baa56-183">분 값 hello (m 00 =)는 항상 00, 이후 활동 로그 이벤트 1 시간 마다 각 blob으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="baa56-184">Hello PT1H.json 파일 내에서 각 이벤트는이 형식에 따라 레코드"hello" 배열에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="baa56-185">요소 이름</span><span class="sxs-lookup"><span data-stu-id="baa56-185">Element name</span></span> | <span data-ttu-id="baa56-186">설명</span><span class="sxs-lookup"><span data-stu-id="baa56-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="baa56-187">실시간</span><span class="sxs-lookup"><span data-stu-id="baa56-187">time</span></span> |<span data-ttu-id="baa56-188">Hello Azure 서비스 처리 hello에서 hello 이벤트가 생성 된 시점의 타임 스탬프는 해당 하는 hello 이벤트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="baa56-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="baa56-189">resourceId</span></span> |<span data-ttu-id="baa56-190">Hello의 리소스 ID 리소스를 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="baa56-191">operationName</span><span class="sxs-lookup"><span data-stu-id="baa56-191">operationName</span></span> |<span data-ttu-id="baa56-192">Hello 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-192">Name of hello operation.</span></span> |
| <span data-ttu-id="baa56-193">카테고리</span><span class="sxs-lookup"><span data-stu-id="baa56-193">category</span></span> |<span data-ttu-id="baa56-194">범주 hello 동작의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-194">Category of hello action, eg.</span></span> <span data-ttu-id="baa56-195">(예: 쓰기, 읽기, 작업)</span><span class="sxs-lookup"><span data-stu-id="baa56-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="baa56-196">resultType</span><span class="sxs-lookup"><span data-stu-id="baa56-196">resultType</span></span> |<span data-ttu-id="baa56-197">hello 결과의 형식 예: hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-197">hello type of hello result, eg.</span></span> <span data-ttu-id="baa56-198">(예: 성공, 실패, 시작)</span><span class="sxs-lookup"><span data-stu-id="baa56-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="baa56-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="baa56-199">resultSignature</span></span> |<span data-ttu-id="baa56-200">Hello 리소스 종류에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="baa56-201">durationMS</span><span class="sxs-lookup"><span data-stu-id="baa56-201">durationMs</span></span> |<span data-ttu-id="baa56-202">밀리초에서 hello 작업 기간</span><span class="sxs-lookup"><span data-stu-id="baa56-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="baa56-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="baa56-203">callerIpAddress</span></span> |<span data-ttu-id="baa56-204">Hello 작업, UPN 클레임 또는 SPN 클레임 가용성에 따라 수행한 hello 사용자의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="baa56-205">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="baa56-205">correlationId</span></span> |<span data-ttu-id="baa56-206">일반적으로 hello 문자열 형식의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="baa56-207">CorrelationId를 공유 하는 이벤트가 속하는지 toohello 같은 uber 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="baa56-208">ID</span><span class="sxs-lookup"><span data-stu-id="baa56-208">identity</span></span> |<span data-ttu-id="baa56-209">Hello 권한 부여 및 클레임 설명 하는 JSON blob입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="baa56-210">권한 부여</span><span class="sxs-lookup"><span data-stu-id="baa56-210">authorization</span></span> |<span data-ttu-id="baa56-211">Hello 이벤트의 RBAC 속성의 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="baa56-212">일반적으로 hello "action", "role" 및 "범위" 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="baa56-213">level</span><span class="sxs-lookup"><span data-stu-id="baa56-213">level</span></span> |<span data-ttu-id="baa56-214">Hello 이벤트의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-214">Level of hello event.</span></span> <span data-ttu-id="baa56-215">Hello 다음 값 중 하나: "Critical", "Error", "Warning", "Informational" 및 "Verbose"</span><span class="sxs-lookup"><span data-stu-id="baa56-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="baa56-216">location</span><span class="sxs-lookup"><span data-stu-id="baa56-216">location</span></span> |<span data-ttu-id="baa56-217">오류가 발생 했습니다. (또는 전역) hello 위치의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="baa56-218">properties</span><span class="sxs-lookup"><span data-stu-id="baa56-218">properties</span></span> |<span data-ttu-id="baa56-219">설정 `<Key, Value>` hello 이벤트의 hello 세부 정보를 설명 하는 쌍 (예: 사전).</span><span class="sxs-lookup"><span data-stu-id="baa56-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="baa56-220">hello 속성 및 해당 속성의 사용 현황 hello 리소스에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa56-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="baa56-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="baa56-221">Next steps</span></span>
* [<span data-ttu-id="baa56-222">분석을 위한 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="baa56-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="baa56-223">Hello 활동 로그 tooEvent 허브 스트림</span><span class="sxs-lookup"><span data-stu-id="baa56-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="baa56-224">활동 로그 hello에 대 한 자세한 내용</span><span class="sxs-lookup"><span data-stu-id="baa56-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

