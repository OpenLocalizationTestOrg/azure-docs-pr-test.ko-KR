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
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="2000e-103">Azure .NET SDK를 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="2000e-104">어떻게 toomanage Azure Data Lake 분석 계정, 데이터 원본, 사용자 및 사용 하 여 작업 hello Azure.NET SDK에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2000e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2000e-105">Prerequisites</span></span>

* <span data-ttu-id="2000e-106">**Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012와 Visual C++ 설치**.</span><span class="sxs-lookup"><span data-stu-id="2000e-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="2000e-107">**.NET 버전 2.5 이상용 Microsoft Azure SDK**.</span><span class="sxs-lookup"><span data-stu-id="2000e-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="2000e-108">Hello를 사용 하 여 설치할 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="2000e-109">**필요한 NuGet 패키지**</span><span class="sxs-lookup"><span data-stu-id="2000e-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="2000e-110">NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="2000e-110">Install NuGet packages</span></span>

|<span data-ttu-id="2000e-111">패키지</span><span class="sxs-lookup"><span data-stu-id="2000e-111">Package</span></span>|<span data-ttu-id="2000e-112">버전</span><span class="sxs-lookup"><span data-stu-id="2000e-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="2000e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="2000e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="2000e-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="2000e-114">2.3.1</span></span>|
|[<span data-ttu-id="2000e-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="2000e-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="2000e-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="2000e-116">3.0.0</span></span>|
|[<span data-ttu-id="2000e-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="2000e-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="2000e-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="2000e-118">2.2.0</span></span>|
|[<span data-ttu-id="2000e-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="2000e-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="2000e-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="2000e-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="2000e-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="2000e-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="2000e-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="2000e-122">3.4.0-preview</span></span>|

<span data-ttu-id="2000e-123">다음 명령은 hello로 hello NuGet 명령줄을 통해 이러한 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="2000e-124">일반적인 변수</span><span class="sxs-lookup"><span data-stu-id="2000e-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="2000e-125">인증</span><span class="sxs-lookup"><span data-stu-id="2000e-125">Authentication</span></span>

<span data-ttu-id="2000e-126">Data Lake 분석 tooAzure 로그온에 대 한 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="2000e-127">hello 다음 코드 조각은의 예가 나와 팝업이 있는 대화형 사용자 인증으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="2000e-128">소스 코드에 대 한 hello **GetCreds_User_Popup** 인증에 대 한 다른 옵션에 대해서는 설명에 대 한 코드를 hello 및 [데이터 레이크 분석.NET 인증 옵션](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="2000e-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="2000e-129">Hello 클라이언트 관리 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="2000e-130">계정 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="2000e-131">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="2000e-132">만들어 아직 없는 경우에 Data Lake 분석 구성 요소를 Azure 리소스 그룹 toocreate 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="2000e-133">인증 자격 증명, 구독 ID 및 위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="2000e-134">코드에서 보여 주는 방법을 다음 hello toocreate 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="2000e-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="2000e-135">자세한 내용은 [Azure 리소스 그룹 및 Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2000e-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="2000e-136">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="2000e-137">항상 ADLA 계정에는 ADLS 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="2000e-138">하나의 toouse 없는 코드 다음 hello로 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2000e-139">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="2000e-140">코드 다음 hello ADLS 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="2000e-141">Data Lake Store 계정 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="2000e-142">데이터 레이크 분석 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="2000e-143">계정이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="2000e-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="2000e-144">계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2000e-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="2000e-145">계정 삭제</span><span class="sxs-lookup"><span data-stu-id="2000e-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="2000e-146">Hello 기본 데이터 레이크 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="2000e-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="2000e-147">모든 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="2000e-148">분석 계정에 대 한이 코드 toodetermine hello 기본 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="2000e-149">데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-149">Manage data sources</span></span>

<span data-ttu-id="2000e-150">Data Lake 분석에는 현재 데이터 원본 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="2000e-151">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="2000e-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="2000e-152">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="2000e-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="2000e-153">Tooan Azure 저장소 계정 연결</span><span class="sxs-lookup"><span data-stu-id="2000e-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="2000e-154">링크 tooAzure 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="2000e-155">Azure Storage 데이터 원본 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="2000e-156">Data Lake Store 데이터 원본 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="2000e-157">폴더 및 파일 업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="2000e-157">Upload and download folders and files</span></span>
<span data-ttu-id="2000e-158">Hello 데이터 레이크 저장소 파일 시스템 클라이언트 관리 개체 tooupload를 사용할 수 있으며 개별 파일 또는 폴더 다운로드 Azure tooyour 로컬 컴퓨터에서 다음 메서드는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="2000e-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="2000e-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="2000e-159">UploadFolder</span></span>
- <span data-ttu-id="2000e-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="2000e-160">UploadFile</span></span>
- <span data-ttu-id="2000e-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="2000e-161">DownloadFolder</span></span>
- <span data-ttu-id="2000e-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="2000e-162">DownloadFile</span></span>

<span data-ttu-id="2000e-163">이러한 방법에 대 한 hello 첫 번째 매개 변수는 hello 이름 hello 원본 경로 hello 대상 경로 대 한 매개 변수가 올 hello 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="2000e-164">다음 예제는 hello toodownload 폴더에 데이터 레이크 저장소 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="2000e-165">Data Lake Store 계정에 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="2000e-166">Azure Storage 계정 경로 확인</span><span class="sxs-lookup"><span data-stu-id="2000e-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="2000e-167">hello 다음 코드는 Azure 저장소 계정 (storageAccntName) Data Lake 분석 계정 (analyticsAccountName)에 있는 경우 그리고 확인 컨테이너 (containerName) hello Azure 저장소 계정에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="2000e-168">카탈로그 및 작업 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-168">Manage catalog and jobs</span></span>
<span data-ttu-id="2000e-169">hello DataLakeAnalyticsCatalogManagementClient 개체는 각 Azure Data Lake 분석 계정에 대해 제공 하는 hello SQL 데이터베이스를 관리 하기 위한 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="2000e-170">hello DataLakeAnalyticsJobManagementClient toosubmit 메서드를 제공 하 고 U-SQL 스크립트를 사용 하 여 hello 데이터베이스에서 실행 되는 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="2000e-171">데이터베이스 및 스키마 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-171">List databases and schemas</span></span>
<span data-ttu-id="2000e-172">Hello 몇 가지 나열할 수 hello 가장 일반적인 데이터베이스와 해당 스키마는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="2000e-173">hello 다음 코드를 데이터베이스 컬렉션을 가져오고 각 데이터베이스에 대 한 hello 스키마를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="2000e-174">테이블 열 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-174">List table columns</span></span>
<span data-ttu-id="2000e-175">hello 다음 코드에서는 어떻게 tooaccess hello 지정된 된 테이블에 데이터 레이크 분석 카탈로그 관리 클라이언트 toolist hello 열이 있는 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="2000e-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="2000e-176">실패한 작업 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-176">List failed jobs</span></span>
<span data-ttu-id="2000e-177">hello 다음 코드를 나열 실패 한 작업에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="2000e-178">파이프라인 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-178">List pipelines</span></span>
<span data-ttu-id="2000e-179">hello 다음 코드를 나열 작업 제출 된 toohello 계정의 각 파이프라인에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="2000e-180">되풀이 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-180">List recurrences</span></span>
<span data-ttu-id="2000e-181">hello 다음 코드를 나열 작업 제출 된 toohello 계정의 각 되풀이 하는 방법에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="2000e-182">일반적인 그래프 시나리오</span><span class="sxs-lookup"><span data-stu-id="2000e-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="2000e-183">Hello AAD 디렉터리에 사용자를 조회</span><span class="sxs-lookup"><span data-stu-id="2000e-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="2000e-184">Hello AAD 디렉터리에 사용자의 ObjectId hello 가져오기</span><span class="sxs-lookup"><span data-stu-id="2000e-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="2000e-185">계산 정책 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-185">Manage compute policies</span></span>
<span data-ttu-id="2000e-186">hello DataLakeAnalyticsAccountManagementClient 개체 hello를 관리 하기 위한 메서드가 계산 Data Lake 분석 계정에 대 한 정책을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="2000e-187">계산 정책 나열</span><span class="sxs-lookup"><span data-stu-id="2000e-187">List compute policies</span></span>
<span data-ttu-id="2000e-188">hello 코드 다음에 Data Lake 분석 계정에 대 한 계산 정책의 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="2000e-189">새 계산 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="2000e-189">Create a new compute policy</span></span>
<span data-ttu-id="2000e-190">설정 hello 최대 AUs 사용 가능한 toohello 지정한 사용자 too50 및 hello 최소 작업 우선 순위 too250에 코드 다음 hello Data Lake 분석 계정에 대 한 새 계산 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2000e-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="2000e-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2000e-191">Next steps</span></span>
* [<span data-ttu-id="2000e-192">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="2000e-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2000e-193">Azure 포털을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="2000e-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="2000e-194">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2000e-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
