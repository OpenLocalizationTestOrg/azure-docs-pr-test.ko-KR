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
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Azure 저장소 메트릭 사용 및 메트릭 데이터 보기
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>개요
새 저장소 계정을 만들 때 기본적으로 저장소 메트릭을 사용하도록 설정되어 있습니다. Hello를 통해 모니터링을 구성할 수 [Azure 포털](https://portal.azure.com) 또는 Windows PowerShell 또는 hello 저장소 클라이언트 라이브러리 중 하나를 통해 프로그래밍 방식으로 합니다.

Hello 메트릭 데이터에 대 한 보존 기간을 구성할 수 있습니다:이 기간 결정 기간 hello 저장소에 대 한 서비스가 hello 메트릭 및 필요한 toostore 공간 있습니다 hello에 대 한 요금을 보관 하 합니다. 일반적으로 분 메트릭에 필요한 hello 중요 한 추가 공간 때문에 시간 메트릭 보다 분 메트릭에 대 한 짧은 보존 기간을 사용 해야 하면 합니다. 충분 한 시간 tooanalyze hello 데이터가 있어야 하 고 오프 라인 분석 이나 보고를 위해 tookeep 모든 메트릭을 다운로드 한 보존 기간을 선택 해야 합니다. 저장소 계정에서 메트릭 데이터를 다운로드할 때도 요금이 청구됩니다.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>어떻게 사용 하 여 tooenable 메트릭을 hello Azure 포털
Hello에 이러한 단계 tooenable 메트릭에 따라 [Azure 포털](https://portal.azure.com):

1. 저장소 계정 tooyour 이동 합니다.
1. 선택 **진단** hello에 **메뉴** 블레이드
1. 되도록 **상태** 너무 설정**에**합니다.
1. Hello 서비스에 대 한 메트릭을 선택 hello toomonitor 판독기.
1. 보존 정책 tooindicate 지정 시간 tooretain 메트릭 및 로그 데이터입니다.
1. **저장**을 선택합니다.

해당 hello 참고 [Azure 포털](https://portal.azure.com) 현재 사용 수는 없습니다; 저장소 계정의 tooconfigure 분 메트릭 PowerShell을 사용 하 여 분 메트릭을 사용 하도록 설정 해야 하거나 프로그래밍 방식으로 합니다.

## <a name="how-tooenable-metrics-using-powershell"></a>어떻게 PowerShell을 사용 하 여 tooenable 메트릭
Hello Azure PowerShell cmdlet Get-azurestorageservicemetricsproperty tooretrieve hello 현재 설정을 사용 하 여 저장소 계정의 저장소 메트릭을 하 여 로컬 컴퓨터 tooconfigure에서 PowerShell을 사용 하는 hello cmdlet Set-azurestorageservicemetricsproperty toochange hello 현재 설정입니다.

저장소 메트릭을 제어 하는 hello cmdlet 매개 변수 뒤 hello를 사용 합니다.

* MetricsType: 사용 가능한 값은 Hour 및 Minute입니다.
* ServiceType: 사용 가능한 값은 Blob, Queue, Table입니다.
* MetricsLevel: 사용 가능한 값은 None, Service 및 ServiceAndApi입니다.

예를 들어 hello 다음 명령을 전환 하는 분 hello hello 보존 기간으로 기본 저장소 계정의 Blob 서비스에 대 한 메트릭을 설정 toofive (일):

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

hello 다음 명령은 검색 hello 현재 시간 메트릭 수준 및 보존 기간 기본 저장소 계정의 blob 서비스 hello에 대 한:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

어떻게 tooconfigure Azure 구독과 Azure PowerShell cmdlet toowork hello 방법을 tooselect hello 기본 저장소 계정 및 toouse 하는 방법에 대 한 정보를 참조 하세요.: [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="how-tooenable-storage-metrics-programmatically"></a>어떻게 tooenable 저장소 메트릭 프로그래밍 방식으로
다음 C# 조각은 hello 방법을 tooenable 메트릭 및 사용 하 여 hello Blob 서비스에 대 한 로깅을 hello 저장소 클라이언트 라이브러리 for.net 보여 줍니다.

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

## <a name="viewing-storage-metrics"></a>저장소 메트릭 보기
저장소 계정의 저장소 분석 메트릭 toomonitor을 구성한 후 Storage Analytics는 저장소 계정의 잘 알려진 테이블 집합에 hello 메트릭의 기록 합니다. Hello에서 tooview 시간 메트릭 차트를 구성할 수 있습니다 [Azure 포털](https://portal.azure.com):

1. Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.
1. 선택 **메트릭** hello에 **메뉴** 블레이드 hello에 대 한 서비스 메트릭 인 tooview 원하는 합니다.
1. 선택 **편집** 원하는 tooconfigure hello 차트에 있습니다.
1. Hello에 **차트 편집** 블레이드, 선택 hello **시간 범위**, **차트 종류**, 및 hello 차트에 표시 하려는 hello 메트릭.
1. **확인**을 선택합니다.

Toodownload hello 메트릭을 하려는 경우 장기 저장 또는 tooanalyze에 로컬로 해야 합니다.

* 이러한 테이블을 인식 하는 도구를 사용 하 여는 tooview 및 있습니다 사이트 설정을 다운로드 합니다.
* Hello 테이블에 저장 하 고 사용자 지정 응용 프로그램 또는 스크립트 tooread 작성 합니다.

많은 타사 저장소 검색 도구는 이러한 테이블 중 파악 하 고 tooview를 사용 하면 직접 해당 합니다.
사용 가능한 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요.

> [!NOTE]
> Hello 버전 0.8.0부터 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/), 보고 및 분석 메트릭 테이블 hello를 다운로드할 수 있습니다.
> 
> 

순서 tooaccess hello 분석 테이블 프로그래밍 방식으로 수행 메모 hello 분석 테이블 저장소 계정의 모든 hello 테이블을 나열 하는 경우 표시 되지 않습니다. 이름으로 직접 액세스 하거나 hello를 사용 하 여 [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello.NET 클라이언트 라이브러리 tooquery hello 테이블 이름에 있습니다.

### <a name="hourly-metrics"></a>시간 메트릭
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>분 메트릭
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>용량
* $MetricsCapacityBlob

해당이 테이블에 대 한 hello 스키마의 전체 세부 정보를 찾을 수 있습니다 [저장소 분석 통계 테이블 스키마](https://msdn.microsoft.com/library/azure/hh343264.aspx)합니다. hello 아래 샘플 행만 사용할 수 있는, hello 열의 하위 집합을 표시 하지만 저장소 메트릭이 이러한 메트릭을 저장 하는 hello 방법의 몇 가지 중요 한 기능을 보여 줍니다.

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Availability | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

이 분 메트릭 데이터를 사용 하 여 hello 파티션 키는 분 해상도에서 hello 시간을 사용 합니다. hello 행 키 hello 유형의 hello 행에 저장 된 정보를 식별 하 고 두 가지 정보, hello 액세스 유형 및 hello 요청 종류의 조각으로 구성 됩니다.

* hello 액세스 형식은 사용자 또는 시스템, 여기서 사용자 tooall 사용자 요청 toohello 저장소 서비스를 참조 하 고 시스템 참조 toorequests Storage Analytics에서 수행 합니다.
* hello 요청 형식은 모두 있는 경우에에서는 요약 행 않거나 hello QueryEntity 또는 UpdateEntity 같은 특정 API를 식별 합니다.

위의 모든 hello hello 예제 데이터 수를 기록 합니다 (오전 11시 시작) 하는 1 분 동안의 너무 hello QueryEntities 요청 플러스 hello QueryEntity 요청 수를 더한 hello UpdateEntity 요청 수를 합 tooseven는 hello 총에 표시 되는 hello user: All 행입니다. 마찬가지로, hello 평균 종단 간 대기 시간 104.4286 hello 사용자: 모든 행을 계산 하 여 얻을 수 있습니다 ((143.8 * 5) + 3 + 9) / 7입니다.

## <a name="metrics-alerts"></a>메트릭 알림
Hello에서 경고를 설정 해야 [Azure 포털](https://portal.azure.com) 하도록 저장소 메트릭을 자동으로 알릴 수 저장소 서비스의 hello 동작의 주요 변경 내용. 를 사용 하면 저장소 탐색기 도구 toodownload이 메트릭 데이터를 분리 된 형식에서에 Microsoft Excel tooanalyze hello 데이터를 사용할 수 있습니다. 사용 가능한 저장소 탐색기 도구의 목록은 [Azure Storage Client Tools](storage-explorers.md)를 참조하세요. Hello에 경고를 구성할 수 있습니다 **규칙 경고** 액세스할 수 있는 블레이드 **모니터링** hello 저장소 계정 메뉴 블레이드에서 합니다.

> [!IMPORTANT]
> 저장소 이벤트와 시간 또는 분 메트릭 데이터에 해당 하는 hello 기록 되는 시간 사이의 지연 될 수 있습니다. 분 메트릭의 hello 경우에서 데이터의 몇 분 정도 한 번에 기록할 수 있습니다. 현재 분 hello에 대 한 hello 트랜잭션을으로 집계 되 고 이전 분의 tootransactions를 발생할 수 있습니다. 이 경우 hello 경고 서비스는 hello에 대 한 모든 사용 가능한 메트릭 데이터 있을 수 없습니다 예기치 않게 발생 tooalerts를 야기할 수 있는 경고 간격을 구성 합니다.
>

## <a name="accessing-metrics-data-programmatically"></a>프로그래밍 방식으로 메트릭 데이터 액세스
hello는 다음과 같습니다 hello 분 범위의 분 메트릭에 액세스 하 고 hello 결과 콘솔 창에에서 표시 하는 샘플 C# 코드입니다. Azure 저장소 라이브러리 버전 4 hello 저장소에 hello 메트릭 테이블에 액세스를 간소화 하 CloudAnalyticsClient 클래스를 포함 하는 hello를 사용 합니다.

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>저장소 메트릭 사용 시 발생하는 요금
쓰기 요청 toocreate 메트릭의 테이블 엔터티를 hello 표준 요금이 적용 가능한 tooall Azure 저장소 작업에는 요금이 청구 됩니다.

클라이언트 toometrics 데이터 읽기 및 삭제 요청도 표준 요율로 청구 있습니다. 데이터 보존 정책을 구성한 경우에는 Azure 저장소에서 이전 메트릭 데이터를 삭제할 때 요금이 부과되지 않습니다. 그러나 분석 데이터를 삭제 하면 계정 hello 삭제 작업에 대 한 청구 됩니다.

hello 메트릭 테이블에서 사용 하는 hello 용량을 기준으로 청구할 수도: hello 다음 tooestimate hello 양을 메트릭 데이터를 저장 하는 데 사용 되는 용량을 사용할 수 있습니다.

* 다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약과 API 수준 요약 모두 사용 하도록 설정한 경우 약 148KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.
* 다음 매시간 서비스가 모든 서비스에 모든 API를 사용, 서비스 수준 요약만 사용 하도록 설정한 경우 약 12KB의 데이터가 매시간 hello 메트릭 트랜잭션 테이블을 저장 됩니다.
* hello blob에 대 한 용량 표에서 두 개의 행 (사용자는 로그에서 제외 된) 제공 매일 추가:이이 테이블의 모든 날 hello 크기가 증가 하 여 tooapproximately를 300 바이트 의미 합니다.

## <a name="next-steps"></a>다음 단계
[저장소 로깅 사용 및 로그 데이터 액세스](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
