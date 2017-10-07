---
title: "hello Azure 포털에에서 저장소 메트릭을 aaaEnabling | Microsoft Docs"
description: "방법에 대 한 저장소 메트릭을 tooenable hello Blob, 큐, 테이블 및 파일 서비스"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="e9343-103">저장소 메트릭 설정 및 메트릭 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="e9343-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="e9343-104">개요</span><span class="sxs-lookup"><span data-stu-id="e9343-104">Overview</span></span>
<span data-ttu-id="e9343-105">새 저장소 계정을 만들 때 기본적으로 저장소 메트릭을 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="e9343-106">어느 hello를 사용 하 여 모니터링을 구성할 수 있습니다 [Azure 클래식 포털](https://manage.windowsazure.com), Windows PowerShell 또는 저장소 API 통해 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-106">You can configure monitoring using either hello [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="e9343-107">저장소 메트릭을 사용 하도록 설정 하면 hello 데이터에 대 한 보존 기간을 선택 해야 합니다:이 기간 결정 기간 hello 저장소에 대 한 서비스가 hello 메트릭 및 필요한 toostore 공간 있습니다 hello에 대 한 요금을 보관 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-107">When you enable Storage Metrics, you must choose a retention period for hello data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="e9343-108">일반적으로 분 메트릭에 필요한 hello 중요 한 추가 공간 때문에 시간 메트릭 보다 분 메트릭에 대 한 짧은 보존 기간을 사용 해야 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="e9343-109">충분 한 시간 tooanalyze hello 데이터가 있어야 하 고 오프 라인 분석 이나 보고를 위해 tookeep 모든 메트릭을 다운로드 한 보존 기간을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="e9343-110">저장소 계정에서 메트릭 데이터를 다운로드할 때도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a><span data-ttu-id="e9343-111">어떻게 tooenable 저장소 메트릭을 사용 하 여 hello Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="e9343-111">How tooenable Storage metrics using hello Azure Classic Portal</span></span>
<span data-ttu-id="e9343-112">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 저장소 계정 toocontrol 저장소 통계에 대 한 hello 구성 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-112">In hello [Azure Classic Portal](https://manage.windowsazure.com), you use hello Configure page for a storage account toocontrol Storage Metrics.</span></span> <span data-ttu-id="e9343-113">모니터링의 경우 Blob, 테이블 및 큐에 대해 일 단위 보존 기간과 수준을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="e9343-114">각각의 경우에서 hello 수준은 hello 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-114">In each case, hello level is one of hello following:</span></span>

* <span data-ttu-id="e9343-115">해제 - 메트릭이 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="e9343-116">최소-저장소 메트릭이 기본 집합을 수신/송신, 가용성, 대기 시간 및 hello Blob, 테이블 및 큐 서비스에 대해 집계 된 성공 비율과 같은 메트릭 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for hello Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="e9343-117">-자세한 정보는 전체 집합을 포함 하는 메트릭을 저장소 메트릭 수집에는 각 저장소 API 작업에 대 한 동일한 메트릭을 hello, 또한 toohello 서비스 수준 메트릭.</span><span class="sxs-lookup"><span data-stu-id="e9343-117">Verbose — Storage Metrics collects a full set of metrics that includes hello same metrics for each storage API operation, in addition toohello service-level metrics.</span></span> <span data-ttu-id="e9343-118">세부 정보 표시 메트릭을 사용하면 응용 프로그램 작업 중 발생하는 문제를 더 면밀하게 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="e9343-119">Hello Azure 클래식 포털을 현재 사용 수는 없습니다; 저장소 계정의 tooconfigure 분 메트릭 PowerShell을 사용 하 여 분 메트릭을 사용 하도록 설정 해야 하거나 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-119">Note that hello Azure Classic Portal does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-storage-metrics-using-powershell"></a><span data-ttu-id="e9343-120">어떻게 PowerShell을 사용 하 여 tooenable 저장소 메트릭을</span><span class="sxs-lookup"><span data-stu-id="e9343-120">How tooenable Storage metrics using PowerShell</span></span>
<span data-ttu-id="e9343-121">Hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 현재 설정을 사용 하 여 저장소 계정의 저장소 메트릭을 하 여 로컬 컴퓨터 tooconfigure에서 PowerShell을 사용 하는 hello cmdlet Set-azurestorageservicemetricsproperty toochange hello 현재 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="e9343-122">저장소 메트릭을 제어 하는 hello cmdlet 매개 변수 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="e9343-123">MetricsType - 사용 가능한 값은 Hour 및 Minute입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="e9343-124">ServiceType: 사용 가능한 값은 Blob, Queue, Table입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="e9343-125">MetricsLevel 가능한 값은 없음 (hello Azure 클래식 포털에서에서 해당 tooOff) 서비스 (hello Azure 클래식 포털에서에서 해당 tooMinimal) 및 ServiceAndApi (hello Azure 클래식 포털에서에서 해당 tooVerbose).</span><span class="sxs-lookup"><span data-stu-id="e9343-125">MetricsLevel possible values are None (equivalent tooOff in hello Azure Classic Portal), Service (equivalent tooMinimal in hello Azure Classic Portal), and ServiceAndApi (equivalent tooVerbose in hello Azure Classic Portal).</span></span>

<span data-ttu-id="e9343-126">예를 들어 hello 다음 명령을 전환 하는 분 hello hello 보존 기간으로 기본 저장소 계정의 blob 서비스에 대 한 메트릭을 설정 toofive (일):</span><span class="sxs-lookup"><span data-stu-id="e9343-126">For example, hello following command switches on minute metrics for hello blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="e9343-127">hello 다음 명령은 검색 hello 현재 시간 메트릭 수준 및 보존 기간 기본 저장소 계정의 blob 서비스 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="e9343-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="e9343-128">어떻게 tooconfigure Azure 구독과 Azure PowerShell cmdlet toowork hello 방법을 tooselect hello 기본 저장소 계정 및 toouse 하는 방법에 대 한 정보를 참조 하세요.: [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="e9343-129">어떻게 tooenable 저장소 메트릭 프로그래밍 방식으로</span><span class="sxs-lookup"><span data-stu-id="e9343-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="e9343-130">다음 C# 조각은 hello 방법을 tooenable 메트릭 및 사용 하 여 hello Blob 서비스에 대 한 로깅을 hello 저장소 클라이언트 라이브러리 for.net 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="e9343-131">저장소 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="e9343-131">Viewing Storage metrics</span></span>
<span data-ttu-id="e9343-132">저장소 메트릭 toomonitor 저장소 계정을 구성 하면 hello 메트릭을 저장소 계정의 잘 알려진 테이블 집합에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-132">When you have configured Storage Metrics toomonitor your storage account, it records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="e9343-133">차트에서 제공 하는 hello tooview hello 시간 메트릭 Azure 클래식 포털에서에서 저장소 계정에 대 한 hello 모니터 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-133">You can use hello Monitor page for your storage account in hello Azure Classic Portal tooview hello hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="e9343-134">Hello Azure 클래식 포털에서에서이 페이지에서는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-134">On this page in hello Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="e9343-135">Hello 차트에서 메트릭을 tooplot 어떤 선택 (사용 가능한 메트릭 hello 선택에 따라 달라 집니다 hello 구성 페이지에서 hello 서비스에 대 한 최소 또는 자세한 정보 표시 모니터링을 선택 여부).</span><span class="sxs-lookup"><span data-stu-id="e9343-135">Select which metrics tooplot on hello chart (hello choice of available metrics will depend on whether you chose verbose or minimal monitoring for hello service on hello Configure page).</span></span>
* <span data-ttu-id="e9343-136">Hello 차트에 표시 된 hello 메트릭에 대 한 hello 시간 범위를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-136">Select hello time range for hello metrics displayed on hello chart.</span></span>
* <span data-ttu-id="e9343-137">Toouse 절대 또는 상대 배율을 tooplot hello 메트릭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-137">Choose toouse an absolute or relative scale tooplot hello metrics.</span></span>
* <span data-ttu-id="e9343-138">전자 메일 경고 toonotify 구성 특정 메트릭이 특정 값에 도달할 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-138">Configure email alerts toonotify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="e9343-139">장기 저장 또는 tooanalyze toodownload hello 메트릭을 하려는 경우 로컬로 toouse 도구 필요 것인지 아니면 tooread hello 테이블 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need toouse a tool or write some code tooread hello tables.</span></span> <span data-ttu-id="e9343-140">Hello 분석을 위해 분 메트릭을 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-140">You must download hello minute metrics for analysis.</span></span> <span data-ttu-id="e9343-141">hello 테이블 이름으로 직접 액세스할 수 있지만 저장소 계정의 모든 hello 테이블을 나열 하는 경우 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-141">hello tables do not appear if you list all hello tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="e9343-142">많은 타사 저장소 검색 도구는 이러한 테이블 중 파악 하 고 tooview를 사용 하면는 직접 (hello 블로그 게시물을 참조 [Microsoft Azure 저장소 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) 사용 가능한 도구 목록은).</span><span class="sxs-lookup"><span data-stu-id="e9343-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly (see hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="e9343-143">시간 메트릭</span><span class="sxs-lookup"><span data-stu-id="e9343-143">Hourly metrics</span></span>
* <span data-ttu-id="e9343-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e9343-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e9343-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e9343-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="e9343-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e9343-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="e9343-147">분 메트릭</span><span class="sxs-lookup"><span data-stu-id="e9343-147">Minute metrics</span></span>
* <span data-ttu-id="e9343-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e9343-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e9343-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e9343-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="e9343-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e9343-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="e9343-151">용량</span><span class="sxs-lookup"><span data-stu-id="e9343-151">Capacity</span></span>
* <span data-ttu-id="e9343-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="e9343-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="e9343-153">해당이 테이블에 대 한 hello 스키마의 전체 세부 정보를 찾을 수 있습니다 [저장소 분석 통계 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-153">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="e9343-154">hello 아래 샘플 행만 사용할 수 있는, hello 열의 하위 집합을 표시 하지만 저장소 메트릭이 이러한 메트릭을 저장 하는 hello 방법의 몇 가지 중요 한 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-154">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="e9343-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e9343-155">PartitionKey</span></span> | <span data-ttu-id="e9343-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="e9343-156">RowKey</span></span> | <span data-ttu-id="e9343-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e9343-157">Timestamp</span></span> | <span data-ttu-id="e9343-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="e9343-158">TotalRequests</span></span> | <span data-ttu-id="e9343-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="e9343-159">TotalBillableRequests</span></span> | <span data-ttu-id="e9343-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="e9343-160">TotalIngress</span></span> | <span data-ttu-id="e9343-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="e9343-161">TotalEgress</span></span> | <span data-ttu-id="e9343-162">Availability</span><span class="sxs-lookup"><span data-stu-id="e9343-162">Availability</span></span> | <span data-ttu-id="e9343-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="e9343-163">AverageE2ELatency</span></span> | <span data-ttu-id="e9343-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="e9343-164">AverageServerLatency</span></span> | <span data-ttu-id="e9343-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="e9343-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e9343-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e9343-166">20140522T1100</span></span> |<span data-ttu-id="e9343-167">user;All</span><span class="sxs-lookup"><span data-stu-id="e9343-167">user;All</span></span> |<span data-ttu-id="e9343-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e9343-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e9343-169">7</span><span class="sxs-lookup"><span data-stu-id="e9343-169">7</span></span> |<span data-ttu-id="e9343-170">7</span><span class="sxs-lookup"><span data-stu-id="e9343-170">7</span></span> |<span data-ttu-id="e9343-171">4003</span><span class="sxs-lookup"><span data-stu-id="e9343-171">4003</span></span> |<span data-ttu-id="e9343-172">46801</span><span class="sxs-lookup"><span data-stu-id="e9343-172">46801</span></span> |<span data-ttu-id="e9343-173">100</span><span class="sxs-lookup"><span data-stu-id="e9343-173">100</span></span> |<span data-ttu-id="e9343-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="e9343-174">104.4286</span></span> |<span data-ttu-id="e9343-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="e9343-175">6.857143</span></span> |<span data-ttu-id="e9343-176">100</span><span class="sxs-lookup"><span data-stu-id="e9343-176">100</span></span> |
| <span data-ttu-id="e9343-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e9343-177">20140522T1100</span></span> |<span data-ttu-id="e9343-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="e9343-178">user;QueryEntities</span></span> |<span data-ttu-id="e9343-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="e9343-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="e9343-180">5</span><span class="sxs-lookup"><span data-stu-id="e9343-180">5</span></span> |<span data-ttu-id="e9343-181">5</span><span class="sxs-lookup"><span data-stu-id="e9343-181">5</span></span> |<span data-ttu-id="e9343-182">2694</span><span class="sxs-lookup"><span data-stu-id="e9343-182">2694</span></span> |<span data-ttu-id="e9343-183">45951</span><span class="sxs-lookup"><span data-stu-id="e9343-183">45951</span></span> |<span data-ttu-id="e9343-184">100</span><span class="sxs-lookup"><span data-stu-id="e9343-184">100</span></span> |<span data-ttu-id="e9343-185">143.8</span><span class="sxs-lookup"><span data-stu-id="e9343-185">143.8</span></span> |<span data-ttu-id="e9343-186">7.8</span><span class="sxs-lookup"><span data-stu-id="e9343-186">7.8</span></span> |<span data-ttu-id="e9343-187">100</span><span class="sxs-lookup"><span data-stu-id="e9343-187">100</span></span> |
| <span data-ttu-id="e9343-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e9343-188">20140522T1100</span></span> |<span data-ttu-id="e9343-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="e9343-189">user;QueryEntity</span></span> |<span data-ttu-id="e9343-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e9343-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e9343-191">1</span><span class="sxs-lookup"><span data-stu-id="e9343-191">1</span></span> |<span data-ttu-id="e9343-192">1</span><span class="sxs-lookup"><span data-stu-id="e9343-192">1</span></span> |<span data-ttu-id="e9343-193">538</span><span class="sxs-lookup"><span data-stu-id="e9343-193">538</span></span> |<span data-ttu-id="e9343-194">633</span><span class="sxs-lookup"><span data-stu-id="e9343-194">633</span></span> |<span data-ttu-id="e9343-195">100</span><span class="sxs-lookup"><span data-stu-id="e9343-195">100</span></span> |<span data-ttu-id="e9343-196">3</span><span class="sxs-lookup"><span data-stu-id="e9343-196">3</span></span> |<span data-ttu-id="e9343-197">3</span><span class="sxs-lookup"><span data-stu-id="e9343-197">3</span></span> |<span data-ttu-id="e9343-198">100</span><span class="sxs-lookup"><span data-stu-id="e9343-198">100</span></span> |
| <span data-ttu-id="e9343-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e9343-199">20140522T1100</span></span> |<span data-ttu-id="e9343-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="e9343-200">user;UpdateEntity</span></span> |<span data-ttu-id="e9343-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e9343-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e9343-202">1</span><span class="sxs-lookup"><span data-stu-id="e9343-202">1</span></span> |<span data-ttu-id="e9343-203">1</span><span class="sxs-lookup"><span data-stu-id="e9343-203">1</span></span> |<span data-ttu-id="e9343-204">771</span><span class="sxs-lookup"><span data-stu-id="e9343-204">771</span></span> |<span data-ttu-id="e9343-205">217</span><span class="sxs-lookup"><span data-stu-id="e9343-205">217</span></span> |<span data-ttu-id="e9343-206">100</span><span class="sxs-lookup"><span data-stu-id="e9343-206">100</span></span> |<span data-ttu-id="e9343-207">9</span><span class="sxs-lookup"><span data-stu-id="e9343-207">9</span></span> |<span data-ttu-id="e9343-208">6</span><span class="sxs-lookup"><span data-stu-id="e9343-208">6</span></span> |<span data-ttu-id="e9343-209">100</span><span class="sxs-lookup"><span data-stu-id="e9343-209">100</span></span> |

<span data-ttu-id="e9343-210">이 분 메트릭 데이터를 사용 하 여 hello 파티션 키는 분 해상도에서 hello 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-210">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="e9343-211">hello 행 키 hello 유형의 hello 행에 저장 된 정보를 식별 하 고 두 가지 정보, hello 액세스 유형 및 hello 요청 종류의 조각으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-211">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="e9343-212">hello 액세스 형식은 사용자 또는 시스템, 여기서 사용자 tooall 사용자 요청 toohello 저장소 서비스를 참조 하 고 시스템 참조 toorequests Storage Analytics에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-212">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="e9343-213">hello 요청 형식은 모두 있는 경우에에서는 요약 행 않거나 hello QueryEntity 또는 UpdateEntity 같은 특정 API를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-213">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="e9343-214">위의 모든 hello hello 예제 데이터 수를 기록 합니다 (오전 11시 시작) 하는 1 분 동안의 너무 hello QueryEntities 요청 플러스 hello QueryEntity 요청 수를 더한 hello UpdateEntity 요청 수를 합 tooseven는 hello 총에 표시 되는 hello user: All 행입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-214">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="e9343-215">마찬가지로, hello 평균 종단 간 대기 시간 104.4286 hello 사용자: 모든 행을 계산 하 여 얻을 수 있습니다 ((143.8 * 5) + 3 + 9) / 7입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-215">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="e9343-216">저장소 메트릭의 hello 동작 저장소 서비스의 모든 중요 한 변경 내용을 알릴 자동으로 수 있도록 hello 모니터 페이지에 hello Azure 클래식 포털에서에서 경고를 설정을 고려해 야 합니다. 를 사용 하면 저장소 탐색기 도구 toodownload이 메트릭 데이터를 분리 된 형식에서에 Microsoft Excel tooanalyze hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-216">You should consider setting up alerts in hello Azure Classic Portal on hello Monitor page so that Storage Metrics can automatically notify you of any important changes in hello behavior of your storage services.If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="e9343-217">Hello 블로그 게시물을 참조 [Microsoft Azure 저장소 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) 사용 가능한 저장소 탐색기 도구 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-217">See hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="e9343-218">프로그래밍 방식으로 메트릭 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="e9343-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="e9343-219">hello는 다음과 같습니다 hello 분 범위의 분 메트릭에 액세스 하 고 hello 결과 콘솔 창에에서 표시 하는 샘플 C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-219">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="e9343-220">Azure 저장소 라이브러리 버전 4 hello 저장소에 hello 메트릭 테이블에 액세스를 간소화 하 CloudAnalyticsClient 클래스를 포함 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-220">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="e9343-221">저장소 메트릭 사용 시 발생하는 요금</span><span class="sxs-lookup"><span data-stu-id="e9343-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="e9343-222">쓰기 요청 toocreate 메트릭의 테이블 엔터티를 hello 표준 요금이 적용 가능한 tooall Azure 저장소 작업에는 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-222">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="e9343-223">클라이언트 toometrics 데이터 읽기 및 삭제 요청도 표준 요율로 청구 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-223">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="e9343-224">데이터 보존 정책을 구성한 경우에는 Azure 저장소에서 이전 메트릭 데이터를 삭제할 때 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="e9343-225">그러나 분석 데이터를 삭제 하면 계정 hello 삭제 작업에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-225">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="e9343-226">hello 메트릭 테이블에서 사용 하는 hello 용량을 기준으로 청구할 수도: hello 다음 tooestimate hello 양을 메트릭 데이터를 저장 하는 데 사용 되는 용량을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-226">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="e9343-227">다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약과 API 수준 요약 모두 사용 하도록 설정한 경우 약 148KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="e9343-228">다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약만 사용 하도록 설정한 경우 약 12KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="e9343-229">hello blob에 대 한 용량 표에서 두 개의 행 (사용자는 로그에서 제외 된) 제공 매일 추가:이이 테이블의 모든 날 hello 크기가 증가 하 여 tooapproximately를 300 바이트 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9343-229">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9343-230">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="e9343-230">Next steps:</span></span>
[<span data-ttu-id="e9343-231">저장소 분석 로깅 사용 및 로그 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="e9343-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
