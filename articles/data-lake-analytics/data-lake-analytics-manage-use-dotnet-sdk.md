---
title: "Azure.NET SDK를 사용 하 여 Azure Data Lake 분석 aaaManage | Microsoft Docs"
description: "어떻게 toomanage Data Lake 분석 작업을 데이터 원본, 사용자에 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Azure .NET SDK를 사용하여 Azure Data Lake Analytics 관리
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

어떻게 toomanage Azure Data Lake 분석 계정, 데이터 원본, 사용자 및 사용 하 여 작업 hello Azure.NET SDK에 알아봅니다. 

## <a name="prerequisites"></a>필수 조건

* **Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012와 Visual C++ 설치**.
* **.NET 버전 2.5 이상용 Microsoft Azure SDK**.  Hello를 사용 하 여 설치할 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.
* **필요한 NuGet 패키지**

### <a name="install-nuget-packages"></a>NuGet 패키지 설치

|패키지|버전|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0-preview|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0-preview|

다음 명령은 hello로 hello NuGet 명령줄을 통해 이러한 패키지를 설치할 수 있습니다.

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>일반적인 변수

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>인증

Data Lake 분석 tooAzure 로그온에 대 한 여러 옵션이 있습니다. hello 다음 코드 조각은의 예가 나와 팝업이 있는 대화형 사용자 인증으로 인증 합니다.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

소스 코드에 대 한 hello **GetCreds_User_Popup** 인증에 대 한 다른 옵션에 대해서는 설명에 대 한 코드를 hello 및 [데이터 레이크 분석.NET 인증 옵션](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-hello-client-management-objects"></a>Hello 클라이언트 관리 개체 만들기

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>계정 관리

### <a name="create-an-azure-resource-group"></a>Azure 리소스 그룹 만들기

만들어 아직 없는 경우에 Data Lake 분석 구성 요소를 Azure 리소스 그룹 toocreate 있어야 합니다. 인증 자격 증명, 구독 ID 및 위치가 필요합니다. 코드에서 보여 주는 방법을 다음 hello toocreate 리소스 그룹:

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
자세한 내용은 [Azure 리소스 그룹 및 Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics)를 참조하세요.

### <a name="create-a-data-lake-store-account"></a>Data Lake 저장소 계정 만들기

항상 ADLA 계정에는 ADLS 계정이 필요합니다. 하나의 toouse 없는 코드 다음 hello로 하나 만들 수 있습니다.

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Data Lake 분석 계정 만들기

코드 다음 hello ADLS 계정을 만듭니다.

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Data Lake Store 계정 나열

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>데이터 레이크 분석 계정을 나열합니다.

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>계정이 있는지 확인

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>계정에 대한 정보 가져오기

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>계정 삭제

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a>Hello 기본 데이터 레이크 저장소 계정 가져오기

모든 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 필요합니다. 분석 계정에 대 한이 코드 toodetermine hello 기본 저장소 계정을 사용 합니다.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>데이터 원본 관리

Data Lake 분석에는 현재 데이터 원본 hello를 지원 합니다.

* [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage 계정](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a>Tooan Azure 저장소 계정 연결

링크 tooAzure 저장소 계정을 만들 수 있습니다.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Azure Storage 데이터 원본 나열

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Data Lake Store 데이터 원본 나열

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>폴더 및 파일 업로드 및 다운로드
Hello 데이터 레이크 저장소 파일 시스템 클라이언트 관리 개체 tooupload를 사용할 수 있으며 개별 파일 또는 폴더 다운로드 Azure tooyour 로컬 컴퓨터에서 다음 메서드는 hello를 사용 하 여:

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

이러한 방법에 대 한 hello 첫 번째 매개 변수는 hello 이름 hello 원본 경로 hello 대상 경로 대 한 매개 변수가 올 hello 데이터 레이크 저장소 계정입니다.

다음 예제는 hello toodownload 폴더에 데이터 레이크 저장소 hello 하는 방법을 보여 줍니다.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Data Lake Store 계정에 파일 만들기

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Azure Storage 계정 경로 확인
hello 다음 코드는 Azure 저장소 계정 (storageAccntName) Data Lake 분석 계정 (analyticsAccountName)에 있는 경우 그리고 확인 컨테이너 (containerName) hello Azure 저장소 계정에 존재 합니다.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>카탈로그 및 작업 관리
hello DataLakeAnalyticsCatalogManagementClient 개체는 각 Azure Data Lake 분석 계정에 대해 제공 하는 hello SQL 데이터베이스를 관리 하기 위한 메서드를 제공 합니다. hello DataLakeAnalyticsJobManagementClient toosubmit 메서드를 제공 하 고 U-SQL 스크립트를 사용 하 여 hello 데이터베이스에서 실행 되는 작업을 관리 합니다.

### <a name="list-databases-and-schemas"></a>데이터베이스 및 스키마 나열
Hello 몇 가지 나열할 수 hello 가장 일반적인 데이터베이스와 해당 스키마는 있습니다. hello 다음 코드를 데이터베이스 컬렉션을 가져오고 각 데이터베이스에 대 한 hello 스키마를 열거 합니다.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>테이블 열 나열
hello 다음 코드에서는 어떻게 tooaccess hello 지정된 된 테이블에 데이터 레이크 분석 카탈로그 관리 클라이언트 toolist hello 열이 있는 데이터베이스

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>실패한 작업 나열
hello 다음 코드를 나열 실패 한 작업에 대 한 정보입니다.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>파이프라인 나열
hello 다음 코드를 나열 작업 제출 된 toohello 계정의 각 파이프라인에 대 한 정보입니다.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>되풀이 나열
hello 다음 코드를 나열 작업 제출 된 toohello 계정의 각 되풀이 하는 방법에 대 한 정보입니다.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>일반적인 그래프 시나리오

### <a name="look-up-user-in-hello-aad-directory"></a>Hello AAD 디렉터리에 사용자를 조회

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a>Hello AAD 디렉터리에 사용자의 ObjectId hello 가져오기

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>계산 정책 관리
hello DataLakeAnalyticsAccountManagementClient 개체 hello를 관리 하기 위한 메서드가 계산 Data Lake 분석 계정에 대 한 정책을 제공 합니다.

### <a name="list-compute-policies"></a>계산 정책 나열
hello 코드 다음에 Data Lake 분석 계정에 대 한 계산 정책의 목록을 검색 합니다.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>새 계산 정책 만들기
설정 hello 최대 AUs 사용 가능한 toohello 지정한 사용자 too50 및 hello 최소 작업 우선 순위 too250에 코드 다음 hello Data Lake 분석 계정에 대 한 새 계산 정책을 만듭니다.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>다음 단계
* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Azure 포털을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)
* [Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
