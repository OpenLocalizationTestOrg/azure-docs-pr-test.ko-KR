---
title: "hello Azure 포털에에서 저장소 메트릭을 aaaEnabling | Microsoft Docs"
description: "방법에 대 한 저장소 메트릭을 tooenable hello Blob, 큐, 테이블 및 파일 서비스"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="9b1f9-103">Azure 저장소 메트릭 사용 및 메트릭 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="9b1f9-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="9b1f9-104">개요</span><span class="sxs-lookup"><span data-stu-id="9b1f9-104">Overview</span></span>
<span data-ttu-id="9b1f9-105">새 저장소 계정을 만들 때 기본적으로 저장소 메트릭을 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="9b1f9-106">Hello를 통해 모니터링을 구성할 수 [Azure 포털](https://portal.azure.com) 또는 Windows PowerShell 또는 hello 저장소 클라이언트 라이브러리 중 하나를 통해 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="9b1f9-107">Hello 메트릭 데이터에 대 한 보존 기간을 구성할 수 있습니다:이 기간 결정 기간 hello 저장소에 대 한 서비스가 hello 메트릭 및 필요한 toostore 공간 있습니다 hello에 대 한 요금을 보관 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="9b1f9-108">일반적으로 분 메트릭에 필요한 hello 중요 한 추가 공간 때문에 시간 메트릭 보다 분 메트릭에 대 한 짧은 보존 기간을 사용 해야 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="9b1f9-109">충분 한 시간 tooanalyze hello 데이터가 있어야 하 고 오프 라인 분석 이나 보고를 위해 tookeep 모든 메트릭을 다운로드 한 보존 기간을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="9b1f9-110">저장소 계정에서 메트릭 데이터를 다운로드할 때도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="9b1f9-111">어떻게 사용 하 여 tooenable 메트릭을 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9b1f9-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="9b1f9-112">Hello에 이러한 단계 tooenable 메트릭에 따라 [Azure 포털](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9b1f9-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9b1f9-113">저장소 계정 tooyour 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="9b1f9-114">선택 **진단** hello에 **메뉴** 블레이드</span><span class="sxs-lookup"><span data-stu-id="9b1f9-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="9b1f9-115">되도록 **상태** 너무 설정**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="9b1f9-116">Hello 서비스에 대 한 메트릭을 선택 hello toomonitor 판독기.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="9b1f9-117">보존 정책 tooindicate 지정 시간 tooretain 메트릭 및 로그 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="9b1f9-118">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-118">Select **Save**.</span></span>

<span data-ttu-id="9b1f9-119">해당 hello 참고 [Azure 포털](https://portal.azure.com) 현재 사용 수는 없습니다; 저장소 계정의 tooconfigure 분 메트릭 PowerShell을 사용 하 여 분 메트릭을 사용 하도록 설정 해야 하거나 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="9b1f9-120">어떻게 PowerShell을 사용 하 여 tooenable 메트릭</span><span class="sxs-lookup"><span data-stu-id="9b1f9-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="9b1f9-121">Hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 현재 설정을 사용 하 여 저장소 계정의 저장소 메트릭을 하 여 로컬 컴퓨터 tooconfigure에서 PowerShell을 사용 하는 hello cmdlet Set-azurestorageservicemetricsproperty toochange hello 현재 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="9b1f9-122">저장소 메트릭을 제어 하는 hello cmdlet 매개 변수 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="9b1f9-123">MetricsType: 사용 가능한 값은 Hour 및 Minute입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="9b1f9-124">ServiceType: 사용 가능한 값은 Blob, Queue, Table입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="9b1f9-125">MetricsLevel: 사용 가능한 값은 None, Service 및 ServiceAndApi입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="9b1f9-126">예를 들어 hello 다음 명령을 전환 하는 분 hello hello 보존 기간으로 기본 저장소 계정의 Blob 서비스에 대 한 메트릭을 설정 toofive (일):</span><span class="sxs-lookup"><span data-stu-id="9b1f9-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="9b1f9-127">hello 다음 명령은 검색 hello 현재 시간 메트릭 수준 및 보존 기간 기본 저장소 계정의 blob 서비스 hello에 대 한:</span><span class="sxs-lookup"><span data-stu-id="9b1f9-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="9b1f9-128">어떻게 tooconfigure Azure 구독과 Azure PowerShell cmdlet toowork hello 방법을 tooselect hello 기본 저장소 계정 및 toouse 하는 방법에 대 한 정보를 참조 하세요.: [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="9b1f9-129">어떻게 tooenable 저장소 메트릭 프로그래밍 방식으로</span><span class="sxs-lookup"><span data-stu-id="9b1f9-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="9b1f9-130">다음 C# 조각은 hello 방법을 tooenable 메트릭 및 사용 하 여 hello Blob 서비스에 대 한 로깅을 hello 저장소 클라이언트 라이브러리 for.net 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="9b1f9-131">저장소 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="9b1f9-131">Viewing Storage metrics</span></span>
<span data-ttu-id="9b1f9-132">저장소 계정의 저장소 분석 메트릭 toomonitor을 구성한 후 Storage Analytics는 저장소 계정의 잘 알려진 테이블 집합에 hello 메트릭의 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="9b1f9-133">Hello에서 tooview 시간 메트릭 차트를 구성할 수 있습니다 [Azure 포털](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9b1f9-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9b1f9-134">Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="9b1f9-135">선택 **메트릭** hello에 **메뉴** 블레이드 hello에 대 한 서비스 메트릭 인 tooview 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="9b1f9-136">선택 **편집** 원하는 tooconfigure hello 차트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="9b1f9-137">Hello에 **차트 편집** 블레이드, 선택 hello **시간 범위**, **차트 종류**, 및 hello 차트에 표시 하려는 hello 메트릭.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="9b1f9-138">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-138">Select **OK**</span></span>

<span data-ttu-id="9b1f9-139">Toodownload hello 메트릭을 하려는 경우 장기 저장 또는 tooanalyze에 로컬로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="9b1f9-140">이러한 테이블을 인식 하는 도구를 사용 하 여는 tooview 및 있습니다 사이트 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="9b1f9-141">Hello 테이블에 저장 하 고 사용자 지정 응용 프로그램 또는 스크립트 tooread 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="9b1f9-142">많은 타사 저장소 검색 도구는 이러한 테이블 중 파악 하 고 tooview를 사용 하면 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="9b1f9-143">사용 가능한 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1f9-144">Hello 버전 0.8.0부터 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/), 보고 및 분석 메트릭 테이블 hello를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="9b1f9-145">순서 tooaccess hello 분석 테이블 프로그래밍 방식으로 수행 메모 hello 분석 테이블 저장소 계정의 모든 hello 테이블을 나열 하는 경우 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="9b1f9-146">이름으로 직접 액세스 하거나 hello를 사용 하 여 [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello.NET 클라이언트 라이브러리 tooquery hello 테이블 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="9b1f9-147">시간 메트릭</span><span class="sxs-lookup"><span data-stu-id="9b1f9-147">Hourly metrics</span></span>
* <span data-ttu-id="9b1f9-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9b1f9-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9b1f9-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9b1f9-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="9b1f9-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9b1f9-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="9b1f9-151">분 메트릭</span><span class="sxs-lookup"><span data-stu-id="9b1f9-151">Minute metrics</span></span>
* <span data-ttu-id="9b1f9-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9b1f9-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9b1f9-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9b1f9-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="9b1f9-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9b1f9-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="9b1f9-155">용량</span><span class="sxs-lookup"><span data-stu-id="9b1f9-155">Capacity</span></span>
* <span data-ttu-id="9b1f9-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="9b1f9-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="9b1f9-157">해당이 테이블에 대 한 hello 스키마의 전체 세부 정보를 찾을 수 있습니다 [저장소 분석 통계 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="9b1f9-158">hello 아래 샘플 행만 사용할 수 있는, hello 열의 하위 집합을 표시 하지만 저장소 메트릭이 이러한 메트릭을 저장 하는 hello 방법의 몇 가지 중요 한 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="9b1f9-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="9b1f9-159">PartitionKey</span></span> | <span data-ttu-id="9b1f9-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="9b1f9-160">RowKey</span></span> | <span data-ttu-id="9b1f9-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="9b1f9-161">Timestamp</span></span> | <span data-ttu-id="9b1f9-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="9b1f9-162">TotalRequests</span></span> | <span data-ttu-id="9b1f9-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="9b1f9-163">TotalBillableRequests</span></span> | <span data-ttu-id="9b1f9-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="9b1f9-164">TotalIngress</span></span> | <span data-ttu-id="9b1f9-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="9b1f9-165">TotalEgress</span></span> | <span data-ttu-id="9b1f9-166">Availability</span><span class="sxs-lookup"><span data-stu-id="9b1f9-166">Availability</span></span> | <span data-ttu-id="9b1f9-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="9b1f9-167">AverageE2ELatency</span></span> | <span data-ttu-id="9b1f9-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="9b1f9-168">AverageServerLatency</span></span> | <span data-ttu-id="9b1f9-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="9b1f9-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9b1f9-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-170">20140522T1100</span></span> |<span data-ttu-id="9b1f9-171">user;All</span><span class="sxs-lookup"><span data-stu-id="9b1f9-171">user;All</span></span> |<span data-ttu-id="9b1f9-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9b1f9-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9b1f9-173">7</span><span class="sxs-lookup"><span data-stu-id="9b1f9-173">7</span></span> |<span data-ttu-id="9b1f9-174">7</span><span class="sxs-lookup"><span data-stu-id="9b1f9-174">7</span></span> |<span data-ttu-id="9b1f9-175">4003</span><span class="sxs-lookup"><span data-stu-id="9b1f9-175">4003</span></span> |<span data-ttu-id="9b1f9-176">46801</span><span class="sxs-lookup"><span data-stu-id="9b1f9-176">46801</span></span> |<span data-ttu-id="9b1f9-177">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-177">100</span></span> |<span data-ttu-id="9b1f9-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="9b1f9-178">104.4286</span></span> |<span data-ttu-id="9b1f9-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="9b1f9-179">6.857143</span></span> |<span data-ttu-id="9b1f9-180">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-180">100</span></span> |
| <span data-ttu-id="9b1f9-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-181">20140522T1100</span></span> |<span data-ttu-id="9b1f9-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="9b1f9-182">user;QueryEntities</span></span> |<span data-ttu-id="9b1f9-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="9b1f9-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="9b1f9-184">5</span><span class="sxs-lookup"><span data-stu-id="9b1f9-184">5</span></span> |<span data-ttu-id="9b1f9-185">5</span><span class="sxs-lookup"><span data-stu-id="9b1f9-185">5</span></span> |<span data-ttu-id="9b1f9-186">2694</span><span class="sxs-lookup"><span data-stu-id="9b1f9-186">2694</span></span> |<span data-ttu-id="9b1f9-187">45951</span><span class="sxs-lookup"><span data-stu-id="9b1f9-187">45951</span></span> |<span data-ttu-id="9b1f9-188">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-188">100</span></span> |<span data-ttu-id="9b1f9-189">143.8</span><span class="sxs-lookup"><span data-stu-id="9b1f9-189">143.8</span></span> |<span data-ttu-id="9b1f9-190">7.8</span><span class="sxs-lookup"><span data-stu-id="9b1f9-190">7.8</span></span> |<span data-ttu-id="9b1f9-191">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-191">100</span></span> |
| <span data-ttu-id="9b1f9-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-192">20140522T1100</span></span> |<span data-ttu-id="9b1f9-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="9b1f9-193">user;QueryEntity</span></span> |<span data-ttu-id="9b1f9-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9b1f9-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9b1f9-195">1</span><span class="sxs-lookup"><span data-stu-id="9b1f9-195">1</span></span> |<span data-ttu-id="9b1f9-196">1</span><span class="sxs-lookup"><span data-stu-id="9b1f9-196">1</span></span> |<span data-ttu-id="9b1f9-197">538</span><span class="sxs-lookup"><span data-stu-id="9b1f9-197">538</span></span> |<span data-ttu-id="9b1f9-198">633</span><span class="sxs-lookup"><span data-stu-id="9b1f9-198">633</span></span> |<span data-ttu-id="9b1f9-199">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-199">100</span></span> |<span data-ttu-id="9b1f9-200">3</span><span class="sxs-lookup"><span data-stu-id="9b1f9-200">3</span></span> |<span data-ttu-id="9b1f9-201">3</span><span class="sxs-lookup"><span data-stu-id="9b1f9-201">3</span></span> |<span data-ttu-id="9b1f9-202">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-202">100</span></span> |
| <span data-ttu-id="9b1f9-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-203">20140522T1100</span></span> |<span data-ttu-id="9b1f9-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="9b1f9-204">user;UpdateEntity</span></span> |<span data-ttu-id="9b1f9-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9b1f9-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9b1f9-206">1</span><span class="sxs-lookup"><span data-stu-id="9b1f9-206">1</span></span> |<span data-ttu-id="9b1f9-207">1</span><span class="sxs-lookup"><span data-stu-id="9b1f9-207">1</span></span> |<span data-ttu-id="9b1f9-208">771</span><span class="sxs-lookup"><span data-stu-id="9b1f9-208">771</span></span> |<span data-ttu-id="9b1f9-209">217</span><span class="sxs-lookup"><span data-stu-id="9b1f9-209">217</span></span> |<span data-ttu-id="9b1f9-210">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-210">100</span></span> |<span data-ttu-id="9b1f9-211">9</span><span class="sxs-lookup"><span data-stu-id="9b1f9-211">9</span></span> |<span data-ttu-id="9b1f9-212">6</span><span class="sxs-lookup"><span data-stu-id="9b1f9-212">6</span></span> |<span data-ttu-id="9b1f9-213">100</span><span class="sxs-lookup"><span data-stu-id="9b1f9-213">100</span></span> |

<span data-ttu-id="9b1f9-214">이 분 메트릭 데이터를 사용 하 여 hello 파티션 키는 분 해상도에서 hello 시간을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="9b1f9-215">hello 행 키 hello 유형의 hello 행에 저장 된 정보를 식별 하 고 두 가지 정보, hello 액세스 유형 및 hello 요청 종류의 조각으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="9b1f9-216">hello 액세스 형식은 사용자 또는 시스템, 여기서 사용자 tooall 사용자 요청 toohello 저장소 서비스를 참조 하 고 시스템 참조 toorequests Storage Analytics에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="9b1f9-217">hello 요청 형식은 모두 있는 경우에에서는 요약 행 않거나 hello QueryEntity 또는 UpdateEntity 같은 특정 API를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="9b1f9-218">위의 모든 hello hello 예제 데이터 수를 기록 합니다 (오전 11시 시작) 하는 1 분 동안의 너무 hello QueryEntities 요청 플러스 hello QueryEntity 요청 수를 더한 hello UpdateEntity 요청 수를 합 tooseven는 hello 총에 표시 되는 hello user: All 행입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="9b1f9-219">마찬가지로, hello 평균 종단 간 대기 시간 104.4286 hello 사용자: 모든 행을 계산 하 여 얻을 수 있습니다 ((143.8 * 5) + 3 + 9) / 7입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="9b1f9-220">메트릭 알림</span><span class="sxs-lookup"><span data-stu-id="9b1f9-220">Metrics alerts</span></span>
<span data-ttu-id="9b1f9-221">Hello에서 경고를 설정 해야 [Azure 포털](https://portal.azure.com) 하도록 저장소 메트릭을 자동으로 알릴 수 저장소 서비스의 hello 동작의 주요 변경 내용.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="9b1f9-222">를 사용 하면 저장소 탐색기 도구 toodownload이 메트릭 데이터를 분리 된 형식에서에 Microsoft Excel tooanalyze hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="9b1f9-223">사용 가능한 저장소 탐색기 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="9b1f9-224">Hello에 경고를 구성할 수 있습니다 **규칙 경고** 액세스할 수 있는 블레이드 **모니터링** hello 저장소 계정 메뉴 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b1f9-225">저장소 이벤트와 시간 또는 분 메트릭 데이터에 해당 하는 hello 기록 되는 시간 사이의 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="9b1f9-226">분 메트릭의 hello 경우에서 데이터의 몇 분 정도 한 번에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="9b1f9-227">현재 분 hello에 대 한 hello 트랜잭션을으로 집계 되 고 이전 분의 tootransactions를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="9b1f9-228">이 경우 hello 경고 서비스는 hello에 대 한 모든 사용 가능한 메트릭 데이터 있을 수 없습니다 예기치 않게 발생 tooalerts를 야기할 수 있는 경고 간격을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="9b1f9-229">프로그래밍 방식으로 메트릭 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="9b1f9-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="9b1f9-230">hello는 다음과 같습니다 hello 분 범위의 분 메트릭에 액세스 하 고 hello 결과 콘솔 창에에서 표시 하는 샘플 C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="9b1f9-231">Azure 저장소 라이브러리 버전 4 hello 저장소에 hello 메트릭 테이블에 액세스를 간소화 하 CloudAnalyticsClient 클래스를 포함 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="9b1f9-232">저장소 메트릭 사용 시 발생하는 요금</span><span class="sxs-lookup"><span data-stu-id="9b1f9-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="9b1f9-233">쓰기 요청 toocreate 메트릭의 테이블 엔터티를 hello 표준 요금이 적용 가능한 tooall Azure 저장소 작업에는 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="9b1f9-234">클라이언트 toometrics 데이터 읽기 및 삭제 요청도 표준 요율로 청구 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="9b1f9-235">데이터 보존 정책을 구성한 경우에는 Azure 저장소에서 이전 메트릭 데이터를 삭제할 때 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="9b1f9-236">그러나 분석 데이터를 삭제 하면 계정 hello 삭제 작업에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="9b1f9-237">hello 메트릭 테이블에서 사용 하는 hello 용량을 기준으로 청구할 수도: hello 다음 tooestimate hello 양을 메트릭 데이터를 저장 하는 데 사용 되는 용량을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="9b1f9-238">다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약과 API 수준 요약 모두 사용 하도록 설정한 경우 약 148KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="9b1f9-239">다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약만 사용 하도록 설정한 경우 약 12KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="9b1f9-240">hello blob에 대 한 용량 표에서 두 개의 행 (사용자는 로그에서 제외 된) 제공 매일 추가:이이 테이블의 모든 날 hello 크기가 증가 하 여 tooapproximately를 300 바이트 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b1f9-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b1f9-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b1f9-241">Next steps</span></span>
[<span data-ttu-id="9b1f9-242">저장소 로깅 사용 및 로그 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="9b1f9-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
