---
title: "Azure Portal에서 저장소 메트릭 사용 | Microsoft Docs"
description: "Blob, 큐, 테이블 및 파일 서비스의 저장소 메트릭을 활성화하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1525a2258dd6ab8e72e8607826523eca8121483c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="0e17e-103">Azure 저장소 메트릭 사용 및 메트릭 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="0e17e-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="0e17e-104">개요</span><span class="sxs-lookup"><span data-stu-id="0e17e-104">Overview</span></span>
<span data-ttu-id="0e17e-105">새 저장소 계정을 만들 때 기본적으로 저장소 메트릭을 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="0e17e-106">[Azure Portal](https://portal.azure.com)이나 Windows PowerShell을 통해 또는 저장소 클라이언트 라이브러리 중 하나를 통해 프로그래밍 방식으로 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="0e17e-107">메트릭 데이터 보존 기간을 구성해야 합니다. 이 기간에 따라 저장소 서비스에서 메트릭을 보관하는 기간이 결정되며, 해당 메트릭을 저장하는 데 필요한 저장소에 대해 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="0e17e-108">일반적으로는 시간 메트릭보다 분 메트릭에 더 짧은 보존 기간을 사용해야 합니다. 분 메트릭의 경우 추가 공간이 상당히 많이 필요하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="0e17e-109">데이터를 분석하고 오프라인 분석용 또는 보고용으로 보관할 메트릭을 다운로드할 시간이 충분하도록 보존 기간을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="0e17e-110">저장소 계정에서 메트릭 데이터를 다운로드할 때도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="0e17e-111">Azure Portal을 사용하여 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e17e-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="0e17e-112">[Azure Portal](https://portal.azure.com)에서 메트릭을 사용하도록 설정하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="0e17e-113">저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="0e17e-114">**메뉴** 블레이드에서 **진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="0e17e-115">**상태**가 **켜기**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="0e17e-116">모니터링하려는 서비스에 대한 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="0e17e-117">보존 정책을 지정하여 메트릭 및 로그 데이터를 보존하는 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="0e17e-118">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-118">Select **Save**.</span></span>

<span data-ttu-id="0e17e-119">[Azure Portal](https://portal.azure.com)에서는 현재 저장소 계정에서 분 메트릭을 구성할 수 없습니다. 따라서 PowerShell을 사용하거나 프로그래밍 방식으로 분 메트릭을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="0e17e-120">PowerShell을 사용하여 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e17e-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="0e17e-121">로컬 컴퓨터에서 PowerShell을 사용하여 저장소 계정의 저장소 메트릭을 구성할 수 있습니다. Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty를 사용하여 현재 설정을 검색하고, Set-AzureStorageServiceMetricsProperty cmdlet을 사용하여 현재 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="0e17e-122">저장소 메트릭을 제어하는 cmdlet은 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="0e17e-123">MetricsType: 사용 가능한 값은 Hour 및 Minute입니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="0e17e-124">ServiceType: 사용 가능한 값은 Blob, Queue, Table입니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="0e17e-125">MetricsLevel: 사용 가능한 값은 None, Service 및 ServiceAndApi입니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="0e17e-126">예를 들어 다음 명령은 보존 기간을 5일로 설정하여 기본 저장소 계정의 Blob 서비스에 대해 분 메트릭을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="0e17e-127">다음 명령은 기본 저장소 계정의 Blob 서비스에 대해 현재 시간 메트릭 수준 및 보존 기간(일)을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="0e17e-128">Azure 구독에서 작동하도록 Azure PowerShell cmdlet을 구성하고 사용할 기본 저장소 계정을 선택하는 방법에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e17e-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="0e17e-129">프로그래밍 방식으로 저장소 메트릭을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="0e17e-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="0e17e-130">다음 C# 코드 조각은 .NET용 저장소 클라이언트 라이브러리를 사용하여 Blob 서비스에 대한 로깅 및 메트릭을 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="0e17e-131">저장소 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="0e17e-131">Viewing Storage metrics</span></span>
<span data-ttu-id="0e17e-132">저장소 계정을 모니터링하도록 저장소 분석 메트릭을 구성하면 저장소 분석에서 저장소 계정의 알려진 테이블 집합에 메트릭을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="0e17e-133">[Azure Portal](https://portal.azure.com)에서 시간별 메트릭을 보도록 차트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="0e17e-134">[Azure Portal](https://portal.azure.com)의 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="0e17e-135">메트릭을 보려는 서비스에 대한 **메뉴** 블레이드에서 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="0e17e-136">구성하려는 차트에 대해 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="0e17e-137">**차트 편집** 블레이드에서 **시간 범위**, **차트 종류** 및 차트에 표시할 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="0e17e-138">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-138">Select **OK**</span></span>

<span data-ttu-id="0e17e-139">장기 저장용 메트릭을 다운로드하거나 메트릭을 로컬에서 분석하려는 경우에는 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="0e17e-140">이러한 테이블을 인식하고 있고 그것들을 보고 다운로드할 수 있도록 하는 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="0e17e-141">사용자 지정 응용 프로그램 또는 스크립트를 작성하여 테이블을 읽고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="0e17e-142">대부분의 타사 저장소 찾아보기 도구는 이러한 테이블을 인식하며 테이블을 직접 보는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="0e17e-143">사용 가능한 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e17e-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="0e17e-144">[Microsoft Azure Storage Explorer](http://storageexplorer.com/) 버전 0.8.0부터 분석 및 메트릭 테이블을 보고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="0e17e-145">프로그래밍 방식으로 분석 테이블에 액세스하기 위해서는 저장소 계정의 모든 테이블을 나열하면 분석 테이블은 표시되지 않음에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="0e17e-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="0e17e-146">테이블 이름을 쿼리하려면 이름을 통해 직접 액세스하거나 .NET 클라이언트 라이브러리에서 [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="0e17e-147">시간 메트릭</span><span class="sxs-lookup"><span data-stu-id="0e17e-147">Hourly metrics</span></span>
* <span data-ttu-id="0e17e-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="0e17e-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="0e17e-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="0e17e-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="0e17e-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="0e17e-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="0e17e-151">분 메트릭</span><span class="sxs-lookup"><span data-stu-id="0e17e-151">Minute metrics</span></span>
* <span data-ttu-id="0e17e-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="0e17e-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="0e17e-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="0e17e-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="0e17e-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="0e17e-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="0e17e-155">용량</span><span class="sxs-lookup"><span data-stu-id="0e17e-155">Capacity</span></span>
* <span data-ttu-id="0e17e-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="0e17e-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="0e17e-157">[저장소 분석 메트릭 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)에서 이러한 테이블의 스키마에 대한 전체 세부 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="0e17e-158">아래의 샘플 행에는 사용 가능한 열 중 일부만 나와 있습니다. 그러나 저장소 메트릭에서 이러한 메트릭을 저장하는 방식과 관련한 몇 가지 중요한 기능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="0e17e-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="0e17e-159">PartitionKey</span></span> | <span data-ttu-id="0e17e-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="0e17e-160">RowKey</span></span> | <span data-ttu-id="0e17e-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="0e17e-161">Timestamp</span></span> | <span data-ttu-id="0e17e-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="0e17e-162">TotalRequests</span></span> | <span data-ttu-id="0e17e-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="0e17e-163">TotalBillableRequests</span></span> | <span data-ttu-id="0e17e-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="0e17e-164">TotalIngress</span></span> | <span data-ttu-id="0e17e-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="0e17e-165">TotalEgress</span></span> | <span data-ttu-id="0e17e-166">Availability</span><span class="sxs-lookup"><span data-stu-id="0e17e-166">Availability</span></span> | <span data-ttu-id="0e17e-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="0e17e-167">AverageE2ELatency</span></span> | <span data-ttu-id="0e17e-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="0e17e-168">AverageServerLatency</span></span> | <span data-ttu-id="0e17e-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="0e17e-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0e17e-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="0e17e-170">20140522T1100</span></span> |<span data-ttu-id="0e17e-171">user;All</span><span class="sxs-lookup"><span data-stu-id="0e17e-171">user;All</span></span> |<span data-ttu-id="0e17e-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="0e17e-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="0e17e-173">7</span><span class="sxs-lookup"><span data-stu-id="0e17e-173">7</span></span> |<span data-ttu-id="0e17e-174">7</span><span class="sxs-lookup"><span data-stu-id="0e17e-174">7</span></span> |<span data-ttu-id="0e17e-175">4003</span><span class="sxs-lookup"><span data-stu-id="0e17e-175">4003</span></span> |<span data-ttu-id="0e17e-176">46801</span><span class="sxs-lookup"><span data-stu-id="0e17e-176">46801</span></span> |<span data-ttu-id="0e17e-177">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-177">100</span></span> |<span data-ttu-id="0e17e-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="0e17e-178">104.4286</span></span> |<span data-ttu-id="0e17e-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="0e17e-179">6.857143</span></span> |<span data-ttu-id="0e17e-180">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-180">100</span></span> |
| <span data-ttu-id="0e17e-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="0e17e-181">20140522T1100</span></span> |<span data-ttu-id="0e17e-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="0e17e-182">user;QueryEntities</span></span> |<span data-ttu-id="0e17e-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="0e17e-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="0e17e-184">5</span><span class="sxs-lookup"><span data-stu-id="0e17e-184">5</span></span> |<span data-ttu-id="0e17e-185">5</span><span class="sxs-lookup"><span data-stu-id="0e17e-185">5</span></span> |<span data-ttu-id="0e17e-186">2694</span><span class="sxs-lookup"><span data-stu-id="0e17e-186">2694</span></span> |<span data-ttu-id="0e17e-187">45951</span><span class="sxs-lookup"><span data-stu-id="0e17e-187">45951</span></span> |<span data-ttu-id="0e17e-188">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-188">100</span></span> |<span data-ttu-id="0e17e-189">143.8</span><span class="sxs-lookup"><span data-stu-id="0e17e-189">143.8</span></span> |<span data-ttu-id="0e17e-190">7.8</span><span class="sxs-lookup"><span data-stu-id="0e17e-190">7.8</span></span> |<span data-ttu-id="0e17e-191">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-191">100</span></span> |
| <span data-ttu-id="0e17e-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="0e17e-192">20140522T1100</span></span> |<span data-ttu-id="0e17e-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="0e17e-193">user;QueryEntity</span></span> |<span data-ttu-id="0e17e-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="0e17e-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="0e17e-195">1</span><span class="sxs-lookup"><span data-stu-id="0e17e-195">1</span></span> |<span data-ttu-id="0e17e-196">1</span><span class="sxs-lookup"><span data-stu-id="0e17e-196">1</span></span> |<span data-ttu-id="0e17e-197">538</span><span class="sxs-lookup"><span data-stu-id="0e17e-197">538</span></span> |<span data-ttu-id="0e17e-198">633</span><span class="sxs-lookup"><span data-stu-id="0e17e-198">633</span></span> |<span data-ttu-id="0e17e-199">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-199">100</span></span> |<span data-ttu-id="0e17e-200">3</span><span class="sxs-lookup"><span data-stu-id="0e17e-200">3</span></span> |<span data-ttu-id="0e17e-201">3</span><span class="sxs-lookup"><span data-stu-id="0e17e-201">3</span></span> |<span data-ttu-id="0e17e-202">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-202">100</span></span> |
| <span data-ttu-id="0e17e-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="0e17e-203">20140522T1100</span></span> |<span data-ttu-id="0e17e-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="0e17e-204">user;UpdateEntity</span></span> |<span data-ttu-id="0e17e-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="0e17e-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="0e17e-206">1</span><span class="sxs-lookup"><span data-stu-id="0e17e-206">1</span></span> |<span data-ttu-id="0e17e-207">1</span><span class="sxs-lookup"><span data-stu-id="0e17e-207">1</span></span> |<span data-ttu-id="0e17e-208">771</span><span class="sxs-lookup"><span data-stu-id="0e17e-208">771</span></span> |<span data-ttu-id="0e17e-209">217</span><span class="sxs-lookup"><span data-stu-id="0e17e-209">217</span></span> |<span data-ttu-id="0e17e-210">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-210">100</span></span> |<span data-ttu-id="0e17e-211">9</span><span class="sxs-lookup"><span data-stu-id="0e17e-211">9</span></span> |<span data-ttu-id="0e17e-212">6</span><span class="sxs-lookup"><span data-stu-id="0e17e-212">6</span></span> |<span data-ttu-id="0e17e-213">100</span><span class="sxs-lookup"><span data-stu-id="0e17e-213">100</span></span> |

<span data-ttu-id="0e17e-214">이 예제 분 메트릭 데이터에서 파티션 키는 분 확인 시의 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="0e17e-215">행 키는 행에 저장되는 정보의 유형을 식별합니다. 이 정보는 액세스 형식과 요청 형식의 두 가지 정보로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="0e17e-216">액세스 형식은 user 또는 system입니다. 여기서 user는 저장소 서비스에 대한 모든 사용자 요청을 지칭하며 system은 저장소 분석에서 수행한 요청을 지칭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="0e17e-217">요청 형식은 all(이 경우 요약 줄)이거나 QueryEntity 또는 UpdateEntity 등의 특정 API를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="0e17e-218">위의 샘플 데이터는 오전 11시부터 1분 동안의 모든 레코드를 표시하므로 QueryEntities 요청의 수 + QueryEntity 요청의 수 + UpdateEntity 요청의 수 = 7입니다. 이 합계가 user:All 행에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="0e17e-219">마찬가지로 ((143.8 * 5) + 3 + 9)/7을 계산하여 user:All 행에 평균 종단 간 대기 시간인 104.4286을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="0e17e-220">메트릭 알림</span><span class="sxs-lookup"><span data-stu-id="0e17e-220">Metrics alerts</span></span>
<span data-ttu-id="0e17e-221">저장소 메트릭이 저장소 서비스 동작의 중요한 변경 내용을 자동으로 알릴 수 있도록 [Azure Portal](https://portal.azure.com)에서 경고를 설정하는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="0e17e-222">저장소 탐색기 도구를 사용하여 이 메트릭 데이터를 구분된 형식에서 다운로드하려면 Microsoft Excel을 사용하여 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="0e17e-223">사용 가능한 저장소 탐색기 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e17e-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="0e17e-224">저장소 계정 메뉴 블레이드에서 **모니터링** 아래에서 액세스할 수 있는 **경고 규칙** 블레이드에서 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e17e-225">저장소 이벤트와 해당 시간 또는 분 메트릭 데이터가 기록되는 시간 사이에 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="0e17e-226">분 메트릭의 경우 데이터의 몇 분을 한 번에 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="0e17e-227">이로 인해 현재 분의 트랜잭션에 집계되는 이전 분의 트랜잭션이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="0e17e-228">이 경우 알림 서비스에는 구성된 알림 간격에 대한 사용 가능한 모든 메트릭 데이터가 없을 수 있어서 예기치 않게 알림이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="0e17e-229">프로그래밍 방식으로 메트릭 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="0e17e-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="0e17e-230">다음 목록에서는 특정 시간(분) 범위에 대한 분 메트릭에 액세스하여 결과를 콘솔 창에 표시하는 샘플 C# 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="0e17e-231">이 코드는 저장소의 메트릭 테이블 액세스를 간소화하는 CloudAnalyticsClient 클래스가 포함된 Azure 저장소 라이브러리 버전 4를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="0e17e-232">저장소 메트릭 사용 시 발생하는 요금</span><span class="sxs-lookup"><span data-stu-id="0e17e-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="0e17e-233">메트릭용 테이블 엔터티 작성을 위한 쓰기 요청에는 모든 Azure 저장소 작업에 적용되는 표준 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="0e17e-234">클라이언트의 메트릭 데이터 읽기 및 삭제 요청 역시 표준 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="0e17e-235">데이터 보존 정책을 구성한 경우에는 Azure 저장소에서 이전 메트릭 데이터를 삭제할 때 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="0e17e-236">그러나 분석 데이터를 삭제하는 경우 계정에 대해 삭제 작업 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="0e17e-237">메트릭 테이블에서 사용하는 용량에 대해서도 요금이 청구됩니다. 아래 지침을 참조하여 메트릭 데이터를 저장하는 데 사용될 용량을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="0e17e-238">서비스가 1시간마다 모든 서비스의 모든 API를 사용하는 경우, 서비스 및 API 수준 요약을 모두 사용하도록 설정했다면 메트릭 트랜잭션 테이블에 시간당 약 148KB의 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="0e17e-239">서비스가 1시간마다 모든 서비스의 모든 API를 사용하는 경우, 서비스 수준 요약만 사용하도록 설정했다면 메트릭 트랜잭션 테이블에 시간당 약 12KB의 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="0e17e-240">사용자가 로그를 옵트인(opt in)한 경우 Blob용 용량 테이블에는 매일 2개 행이 추가됩니다. 따라서 이 테이블의 크기가 매일 약 300바이트씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e17e-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e17e-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e17e-241">Next steps</span></span>
[<span data-ttu-id="0e17e-242">저장소 로깅 사용 및 로그 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="0e17e-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
