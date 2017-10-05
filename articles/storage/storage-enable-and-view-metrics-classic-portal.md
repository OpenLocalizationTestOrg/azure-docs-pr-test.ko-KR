---
title: "Azure Portal에서 저장소 메트릭 사용 | Microsoft Docs"
description: "Blob, 큐, 테이블 및 파일 서비스의 저장소 메트릭을 활성화하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="cb05c-103">저장소 메트릭 설정 및 메트릭 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="cb05c-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="cb05c-104">개요</span><span class="sxs-lookup"><span data-stu-id="cb05c-104">Overview</span></span>
<span data-ttu-id="cb05c-105">새 저장소 계정을 만들 때 기본적으로 저장소 메트릭을 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="cb05c-106">[Azure 클래식 포털](https://manage.windowsazure.com)이나 Windows PowerShell을 사용하여 또는 저장소 API를 통해 프로그래밍 방식으로 모니터링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="cb05c-107">저장소 메트릭을 사용하도록 설정할 때는데이터 보존 기간을 선택해야 합니다. 이 기간에 따라 저장소 서비스에서 메트릭을 보관하는 기간이 결정되며, 해당 메트릭을 저장하는 데 필요한 저장소에 대해 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="cb05c-108">일반적으로는 시간 메트릭보다 분 메트릭에 더 짧은 보존 기간을 사용해야 합니다. 분 메트릭의 경우 추가 공간이 상당히 많이 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="cb05c-109">데이터를 분석하고 오프라인 분석용 또는 보고용으로 보관할 메트릭을 다운로드할 시간이 충분하도록 보존 기간을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="cb05c-110">저장소 계정에서 메트릭 데이터를 다운로드할 때도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="cb05c-111">Azure 클래식 포털을 사용하여 저장소 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="cb05c-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="cb05c-112">[Azure 클래식 포털](https://manage.windowsazure.com)에서 저장소 계정의 구성 페이지를 사용하여 저장소 메트릭을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="cb05c-113">모니터링의 경우 Blob, 테이블 및 큐에 대해 일 단위 보존 기간과 수준을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="cb05c-114">각 경우 수준은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="cb05c-115">해제 - 메트릭이 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="cb05c-116">최소 - 저장소 메트릭이 수신/송신, 가용성, 대기 시간, 성공률 등 Blob, 테이블 및 큐 서비스에 대해 집계되는 기본적인 메트릭 집합을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="cb05c-117">자세한 정보 표시 - 저장소 메트릭이 서비스 수준 메트릭과 함께 각 저장소 API 작업에 대한 동일 메트릭을 포함하는 전체 메트릭 집합을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="cb05c-118">세부 정보 표시 메트릭을 사용하면 응용 프로그램 작업 중 발생하는 문제를 더 면밀하게 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="cb05c-119">Azure 클래식 포털에서는 현재 저장소 계정에서 분 메트릭을 구성할 수 없습니다. 따라서 PowerShell을 사용하거나 프로그래밍 방식으로 분 메트릭을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="cb05c-120">PowerShell을 사용하여 저장소 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="cb05c-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="cb05c-121">로컬 컴퓨터에서 PowerShell을 사용하여 저장소 계정의 저장소 메트릭을 구성할 수 있습니다. Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty를 사용하여 현재 설정을 검색하고, Set-AzureStorageServiceMetricsProperty cmdlet을 사용하여 현재 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="cb05c-122">저장소 메트릭을 제어하는 cmdlet은 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="cb05c-123">MetricsType - 사용 가능한 값은 Hour 및 Minute입니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="cb05c-124">ServiceType: 사용 가능한 값은 Blob, Queue, Table입니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="cb05c-125">MetricsLevel 사용 가능한 값은 None(Azure 클래식 포털에서 해제를 선택하는 경우와 같음), Service(Azure 클래식 포털에서 최소를 선택하는 경우와 같음), ServiceAndApi(Azure 클래식 포털에서 자세한 정보 표시를 선택하는 경우와 같음)입니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="cb05c-126">예를 들어 다음 명령은 보존 기간을 5일로 설정하여 기본 저장소 계정의 Blob 서비스에 대해 분 메트릭을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="cb05c-127">다음 명령은 기본 저장소 계정의 Blob 서비스에 대해 현재 시간 메트릭 수준 및 보존 기간(일)을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="cb05c-128">Azure 구독에서 작동하도록 Azure PowerShell cmdlet을 구성하고 사용할 기본 저장소 계정을 선택하는 방법에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb05c-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="cb05c-129">프로그래밍 방식으로 저장소 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="cb05c-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="cb05c-130">다음 C# 코드 조각은 .NET용 저장소 클라이언트 라이브러리를 사용하여 Blob 서비스에 대한 로깅 및 메트릭을 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="cb05c-131">저장소 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="cb05c-131">Viewing Storage metrics</span></span>
<span data-ttu-id="cb05c-132">저장소 계정을 모니터링하도록 저장소 메트릭을 구성하면 저장소 계정의 알려진 테이블 집합에 메트릭이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="cb05c-133">차트에서 시간 메트릭이 사용 가능해지면 Azure 클래식 포털에서 저장소 계정의 모니터 페이지를 통해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="cb05c-134">Azure 클래식 포털의 이 페이지에서 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="cb05c-135">차트에 그릴 메트릭을 선택합니다. 사용 가능한 메트릭 선택 항목은 구성 페이지에서 서비스에 대해 선택한 모니터링 방식(자세한 정보 표시 또는 최소)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="cb05c-136">차트에 표시되는 메트릭의 시간 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="cb05c-137">메트릭을 그리는 데 사용할 배율(절대 또는 상대)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="cb05c-138">특정 메트릭이 특정 값에 도달할 때 알림을 보내도록 전자 메일 알림을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="cb05c-139">장기 저장용 메트릭을 다운로드하거나 메트릭을 로컬에서 분석하려는 경우에는 테이블을 읽는 코드를 작성하거나 도구를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="cb05c-140">분석용으로는 분 메트릭을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="cb05c-141">저장소 계정의 모든 테이블을 나열해도 테이블은 표시되지 않지만 테이블 이름을 통해 직접 액세스할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="cb05c-142">대부분의 타사 저장소 찾아보기 도구는 이러한 테이블을 인식하며 테이블을 직접 보는 기능을 제공합니다. 사용 가능한 도구의 목록은 [Microsoft Azure Storage 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb05c-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="cb05c-143">시간 메트릭</span><span class="sxs-lookup"><span data-stu-id="cb05c-143">Hourly metrics</span></span>
* <span data-ttu-id="cb05c-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="cb05c-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="cb05c-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="cb05c-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="cb05c-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="cb05c-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="cb05c-147">분 메트릭</span><span class="sxs-lookup"><span data-stu-id="cb05c-147">Minute metrics</span></span>
* <span data-ttu-id="cb05c-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="cb05c-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="cb05c-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="cb05c-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="cb05c-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="cb05c-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="cb05c-151">용량</span><span class="sxs-lookup"><span data-stu-id="cb05c-151">Capacity</span></span>
* <span data-ttu-id="cb05c-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="cb05c-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="cb05c-153">[저장소 분석 메트릭 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)에서 이러한 테이블의 스키마에 대한 전체 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="cb05c-154">아래의 샘플 행에는 사용 가능한 열 중 일부만 나와 있습니다. 그러나 저장소 메트릭에서 이러한 메트릭을 저장하는 방식과 관련한 몇 가지 중요한 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="cb05c-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="cb05c-155">PartitionKey</span></span> | <span data-ttu-id="cb05c-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="cb05c-156">RowKey</span></span> | <span data-ttu-id="cb05c-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="cb05c-157">Timestamp</span></span> | <span data-ttu-id="cb05c-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="cb05c-158">TotalRequests</span></span> | <span data-ttu-id="cb05c-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="cb05c-159">TotalBillableRequests</span></span> | <span data-ttu-id="cb05c-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="cb05c-160">TotalIngress</span></span> | <span data-ttu-id="cb05c-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="cb05c-161">TotalEgress</span></span> | <span data-ttu-id="cb05c-162">Availability</span><span class="sxs-lookup"><span data-stu-id="cb05c-162">Availability</span></span> | <span data-ttu-id="cb05c-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="cb05c-163">AverageE2ELatency</span></span> | <span data-ttu-id="cb05c-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="cb05c-164">AverageServerLatency</span></span> | <span data-ttu-id="cb05c-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="cb05c-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="cb05c-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="cb05c-166">20140522T1100</span></span> |<span data-ttu-id="cb05c-167">user;All</span><span class="sxs-lookup"><span data-stu-id="cb05c-167">user;All</span></span> |<span data-ttu-id="cb05c-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="cb05c-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="cb05c-169">7</span><span class="sxs-lookup"><span data-stu-id="cb05c-169">7</span></span> |<span data-ttu-id="cb05c-170">7</span><span class="sxs-lookup"><span data-stu-id="cb05c-170">7</span></span> |<span data-ttu-id="cb05c-171">4003</span><span class="sxs-lookup"><span data-stu-id="cb05c-171">4003</span></span> |<span data-ttu-id="cb05c-172">46801</span><span class="sxs-lookup"><span data-stu-id="cb05c-172">46801</span></span> |<span data-ttu-id="cb05c-173">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-173">100</span></span> |<span data-ttu-id="cb05c-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="cb05c-174">104.4286</span></span> |<span data-ttu-id="cb05c-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="cb05c-175">6.857143</span></span> |<span data-ttu-id="cb05c-176">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-176">100</span></span> |
| <span data-ttu-id="cb05c-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="cb05c-177">20140522T1100</span></span> |<span data-ttu-id="cb05c-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="cb05c-178">user;QueryEntities</span></span> |<span data-ttu-id="cb05c-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="cb05c-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="cb05c-180">5</span><span class="sxs-lookup"><span data-stu-id="cb05c-180">5</span></span> |<span data-ttu-id="cb05c-181">5</span><span class="sxs-lookup"><span data-stu-id="cb05c-181">5</span></span> |<span data-ttu-id="cb05c-182">2694</span><span class="sxs-lookup"><span data-stu-id="cb05c-182">2694</span></span> |<span data-ttu-id="cb05c-183">45951</span><span class="sxs-lookup"><span data-stu-id="cb05c-183">45951</span></span> |<span data-ttu-id="cb05c-184">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-184">100</span></span> |<span data-ttu-id="cb05c-185">143.8</span><span class="sxs-lookup"><span data-stu-id="cb05c-185">143.8</span></span> |<span data-ttu-id="cb05c-186">7.8</span><span class="sxs-lookup"><span data-stu-id="cb05c-186">7.8</span></span> |<span data-ttu-id="cb05c-187">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-187">100</span></span> |
| <span data-ttu-id="cb05c-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="cb05c-188">20140522T1100</span></span> |<span data-ttu-id="cb05c-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="cb05c-189">user;QueryEntity</span></span> |<span data-ttu-id="cb05c-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="cb05c-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="cb05c-191">1</span><span class="sxs-lookup"><span data-stu-id="cb05c-191">1</span></span> |<span data-ttu-id="cb05c-192">1</span><span class="sxs-lookup"><span data-stu-id="cb05c-192">1</span></span> |<span data-ttu-id="cb05c-193">538</span><span class="sxs-lookup"><span data-stu-id="cb05c-193">538</span></span> |<span data-ttu-id="cb05c-194">633</span><span class="sxs-lookup"><span data-stu-id="cb05c-194">633</span></span> |<span data-ttu-id="cb05c-195">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-195">100</span></span> |<span data-ttu-id="cb05c-196">3</span><span class="sxs-lookup"><span data-stu-id="cb05c-196">3</span></span> |<span data-ttu-id="cb05c-197">3</span><span class="sxs-lookup"><span data-stu-id="cb05c-197">3</span></span> |<span data-ttu-id="cb05c-198">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-198">100</span></span> |
| <span data-ttu-id="cb05c-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="cb05c-199">20140522T1100</span></span> |<span data-ttu-id="cb05c-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="cb05c-200">user;UpdateEntity</span></span> |<span data-ttu-id="cb05c-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="cb05c-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="cb05c-202">1</span><span class="sxs-lookup"><span data-stu-id="cb05c-202">1</span></span> |<span data-ttu-id="cb05c-203">1</span><span class="sxs-lookup"><span data-stu-id="cb05c-203">1</span></span> |<span data-ttu-id="cb05c-204">771</span><span class="sxs-lookup"><span data-stu-id="cb05c-204">771</span></span> |<span data-ttu-id="cb05c-205">217</span><span class="sxs-lookup"><span data-stu-id="cb05c-205">217</span></span> |<span data-ttu-id="cb05c-206">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-206">100</span></span> |<span data-ttu-id="cb05c-207">9</span><span class="sxs-lookup"><span data-stu-id="cb05c-207">9</span></span> |<span data-ttu-id="cb05c-208">6</span><span class="sxs-lookup"><span data-stu-id="cb05c-208">6</span></span> |<span data-ttu-id="cb05c-209">100</span><span class="sxs-lookup"><span data-stu-id="cb05c-209">100</span></span> |

<span data-ttu-id="cb05c-210">이 예제 분 메트릭 데이터에서 파티션 키는 분 확인 시의 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="cb05c-211">행 키는 행에 저장되는 정보의 유형을 식별합니다. 이 정보는 액세스 형식과 요청 형식의 두 가지 정보로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="cb05c-212">액세스 형식은 user 또는 system입니다. 여기서 user는 저장소 서비스에 대한 모든 사용자 요청을 지칭하며 system은 저장소 분석에서 수행한 요청을 지칭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="cb05c-213">요청 형식은 all(이 경우 요약 줄)이거나 QueryEntity 또는 UpdateEntity 등의 특정 API를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="cb05c-214">위의 샘플 데이터는 오전 11시부터 1분 동안의 모든 레코드를 표시하므로 QueryEntities 요청의 수 + QueryEntity 요청의 수 + UpdateEntity 요청의 수 = 7입니다. 이 합계가 user:All 행에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="cb05c-215">마찬가지로 ((143.8 * 5) + 3 + 9)/7을 계산하여 user:All 행에 평균 종단 간 대기 시간인 104.4286을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="cb05c-216">저장소 메트릭에서 저장소 서비스 동작의 중요한 변경 내용을 자동으로 알릴 수 있도록 Azure 클래식 포털의 모니터 페이지에서 경고를 설정하는 것이 좋습니다. 저장소 탐색기 도구를 사용하여 이 메트릭 데이터를 구분된 형식으로 다운로드하는 경우에는 Microsoft Excel을 사용하여 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="cb05c-217">사용 가능한 저장소 탐색기 도구의 목록은 [Microsoft Azure Storage 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb05c-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="cb05c-218">프로그래밍 방식으로 메트릭 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="cb05c-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="cb05c-219">다음 목록에서는 특정 시간(분) 범위에 대한 분 메트릭에 액세스하여 결과를 콘솔 창에 표시하는 샘플 C# 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="cb05c-220">이 코드는 저장소의 메트릭 테이블 액세스를 간소화하는 CloudAnalyticsClient 클래스가 포함된 Azure 저장소 라이브러리 버전 4를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="cb05c-221">저장소 메트릭 사용 시 발생하는 요금</span><span class="sxs-lookup"><span data-stu-id="cb05c-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="cb05c-222">메트릭용 테이블 엔터티 작성을 위한 쓰기 요청에는 모든 Azure 저장소 작업에 적용되는 표준 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="cb05c-223">클라이언트의 메트릭 데이터 읽기 및 삭제 요청 역시 표준 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="cb05c-224">데이터 보존 정책을 구성한 경우에는 Azure 저장소에서 이전 메트릭 데이터를 삭제할 때 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="cb05c-225">그러나 분석 데이터를 삭제하는 경우 계정에 대해 삭제 작업 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="cb05c-226">메트릭 테이블에서 사용하는 용량에 대해서도 요금이 청구됩니다. 아래 지침을 참조하여 메트릭 데이터를 저장하는 데 사용될 용량을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="cb05c-227">서비스가 1시간마다 모든 서비스의 모든 API를 사용하는 경우, 서비스 및 API 수준 요약을 모두 사용하도록 설정했다면 메트릭 트랜잭션 테이블에 시간당 약 148KB의 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="cb05c-228">서비스가 1시간마다 모든 서비스의 모든 API를 사용하는 경우, 서비스 수준 요약만 사용하도록 설정했다면 메트릭 트랜잭션 테이블에 시간당 약 12KB의 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="cb05c-229">사용자가 로그를 옵트인(opt in)한 경우 Blob용 용량 테이블에는 매일 2개 행이 추가됩니다. 따라서 이 테이블의 크기가 매일 약 300바이트씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb05c-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb05c-230">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="cb05c-230">Next steps:</span></span>
[<span data-ttu-id="cb05c-231">저장소 분석 로깅 사용 및 로그 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="cb05c-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
