---
title: "Azure .NET SDK를 사용하여 Azure Data Lake Analytics 관리 | Microsoft Docs"
description: "데이터 레이크 분석 작업, 데이터 원본, 사용자를 관리하는 방법에 대해 알아봅니다. "
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
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="abd6a-103">Azure .NET SDK를 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="abd6a-104">Azure .NET SDK를 사용하여 Azure Data Lake Analytics 계정, 데이터 원본, 사용자 및 작업을 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="abd6a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="abd6a-105">Prerequisites</span></span>

* <span data-ttu-id="abd6a-106">**Visual Studio 2015, Visual Studio 2013 업데이트 4 또는 Visual Studio 2012와 Visual C++ 설치**.</span><span class="sxs-lookup"><span data-stu-id="abd6a-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="abd6a-107">**.NET 버전 2.5 이상용 Microsoft Azure SDK**.</span><span class="sxs-lookup"><span data-stu-id="abd6a-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="abd6a-108">[웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)를 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-108">Install it using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="abd6a-109">**필요한 NuGet 패키지**</span><span class="sxs-lookup"><span data-stu-id="abd6a-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="abd6a-110">NuGet 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="abd6a-110">Install NuGet packages</span></span>

|<span data-ttu-id="abd6a-111">패키지</span><span class="sxs-lookup"><span data-stu-id="abd6a-111">Package</span></span>|<span data-ttu-id="abd6a-112">버전</span><span class="sxs-lookup"><span data-stu-id="abd6a-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="abd6a-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="abd6a-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="abd6a-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="abd6a-114">2.3.1</span></span>|
|[<span data-ttu-id="abd6a-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="abd6a-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="abd6a-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="abd6a-116">3.0.0</span></span>|
|[<span data-ttu-id="abd6a-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="abd6a-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="abd6a-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="abd6a-118">2.2.0</span></span>|
|[<span data-ttu-id="abd6a-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="abd6a-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="abd6a-120">1.6.0-preview</span><span class="sxs-lookup"><span data-stu-id="abd6a-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="abd6a-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="abd6a-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="abd6a-122">3.4.0-preview</span><span class="sxs-lookup"><span data-stu-id="abd6a-122">3.4.0-preview</span></span>|

<span data-ttu-id="abd6a-123">NuGet 명령줄을 통해 다음 명령을 사용하여 이러한 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-123">You can install these packages via the NuGet command line with the following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="abd6a-124">일반적인 변수</span><span class="sxs-lookup"><span data-stu-id="abd6a-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="abd6a-125">인증</span><span class="sxs-lookup"><span data-stu-id="abd6a-125">Authentication</span></span>

<span data-ttu-id="abd6a-126">Azure Data Lake Analytics에 로그온하는 옵션은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-126">You have multiple options for logging on to Azure Data Lake Analytics.</span></span> <span data-ttu-id="abd6a-127">다음 코드 조각은 팝업을 사용한 대화형 사용자 인증의 인증 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-127">The following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="abd6a-128">**GetCreds_User_Popup**의 소스 코드와 인증에 대한 다른 옵션 코드는 [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)(Data Lake Analytics .NET 인증 옵션)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-128">The source code for **GetCreds_User_Popup** and the code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-the-client-management-objects"></a><span data-ttu-id="abd6a-129">클라이언트 관리 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-129">Create the client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="abd6a-130">계정 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="abd6a-131">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="abd6a-132">아직 만들지 않은 경우에는 반드시 Azure 리소스 그룹을 만들어 Data Lake Analytics 구성 요소를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-132">If you haven't already created one, you must have an Azure Resource Group to create your Data Lake Analytics components.</span></span> <span data-ttu-id="abd6a-133">인증 자격 증명, 구독 ID 및 위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="abd6a-134">다음 코드는 리소스 그룹을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-134">The following code shows how to create a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="abd6a-135">자세한 내용은 [Azure 리소스 그룹 및 Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abd6a-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="abd6a-136">Data Lake 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="abd6a-137">항상 ADLA 계정에는 ADLS 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="abd6a-138">아직 사용할 ADLS 계정이 없는 경우 다음 코드를 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-138">If you don't already have one to use, you can create one with the following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="abd6a-139">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="abd6a-140">다음 코드는 ADLS 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-140">The following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="abd6a-141">Data Lake Store 계정 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="abd6a-142">데이터 레이크 분석 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="abd6a-143">계정이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="abd6a-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="abd6a-144">계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="abd6a-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="abd6a-145">계정 삭제</span><span class="sxs-lookup"><span data-stu-id="abd6a-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a><span data-ttu-id="abd6a-146">기본 Data Lake Store 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="abd6a-146">Get the default Data Lake Store account</span></span>

<span data-ttu-id="abd6a-147">모든 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="abd6a-148">다음 코드를 사용하여 Analytics 계정의 기본 Store 계정을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-148">Use this code to determine the default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="abd6a-149">데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-149">Manage data sources</span></span>

<span data-ttu-id="abd6a-150">데이터 레이크 분석은 현재 다음 데이터 원본을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-150">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="abd6a-151">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="abd6a-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="abd6a-152">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="abd6a-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a><span data-ttu-id="abd6a-153">Azure Storage 계정에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="abd6a-153">Link to an Azure Storage account</span></span>

<span data-ttu-id="abd6a-154">Azure Storage 계정에 대한 링크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-154">You can create links to Azure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="abd6a-155">Azure Storage 데이터 원본 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="abd6a-156">Data Lake Store 데이터 원본 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="abd6a-157">폴더 및 파일 업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="abd6a-157">Upload and download folders and files</span></span>
<span data-ttu-id="abd6a-158">Data Lake Store 파일 시스템 클라이언트 관리 개체를 사용하여 다음 메서드를 통해 Azure에서 로컬 컴퓨터로 개별 파일 또는 폴더를 업로드하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-158">You can use the Data Lake Store file system client management object to upload and download individual files or folders from Azure to your local computer, using the following methods:</span></span>

- <span data-ttu-id="abd6a-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="abd6a-159">UploadFolder</span></span>
- <span data-ttu-id="abd6a-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="abd6a-160">UploadFile</span></span>
- <span data-ttu-id="abd6a-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="abd6a-161">DownloadFolder</span></span>
- <span data-ttu-id="abd6a-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="abd6a-162">DownloadFile</span></span>

<span data-ttu-id="abd6a-163">이러한 메서드의 첫 번째 매개 변수는 원본 경로 및 대상 경로 매개 변수가 뒤에 나오는 Data Lake Store 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-163">The first parameter for these methods is the name of the Data Lake Store Account, followed by parameters for the source path and the destination path.</span></span>

<span data-ttu-id="abd6a-164">다음 예제는 Data Lake Store에서 폴더를 다운로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-164">The following example shows how to download a folder in the Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="abd6a-165">Data Lake Store 계정에 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="abd6a-166">Azure Storage 계정 경로 확인</span><span class="sxs-lookup"><span data-stu-id="abd6a-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="abd6a-167">다음 코드에서는 Azure Storage 계정(storageAccntName)이 Data Lake Analytics 계정(analyticsAccountName)에 있는지 및 컨테이너(containerName)가 Azure Storage 계정에 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-167">The following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in the Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="abd6a-168">카탈로그 및 작업 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-168">Manage catalog and jobs</span></span>
<span data-ttu-id="abd6a-169">DataLakeAnalyticsCatalogManagementClient 개체는 각 Azure Data Lake Analytics 계정에 제공된 SQL 데이터베이스를 관리하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-169">The DataLakeAnalyticsCatalogManagementClient object provides methods for managing the SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="abd6a-170">DataLakeAnalyticsJobManagementClient는 U-SQL 스크립트를 사용하여 데이터베이스에서 실행되는 작업을 제출하고 관리하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-170">The DataLakeAnalyticsJobManagementClient provides methods to submit and manage jobs run on the database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="abd6a-171">데이터베이스 및 스키마 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-171">List databases and schemas</span></span>
<span data-ttu-id="abd6a-172">나열할 수 있는 항목들 중에서 가장 일반적인 항목이 데이터베이스와 해당 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-172">Among the several things you can list, the most common are databases and their schema.</span></span> <span data-ttu-id="abd6a-173">다음 코드에서는 데이터베이스 컬렉션을 가져온 다음 각 데이터베이스에 대한 스키마를 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-173">The following code obtains a collection of databases, and then enumerates the schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="abd6a-174">테이블 열 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-174">List table columns</span></span>
<span data-ttu-id="abd6a-175">다음 코드에서는 Data Lake Analytics 카탈로그 관리 클라이언트를 통해 데이터베이스에 액세스하여 지정한 테이블의 열을 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-175">The following code shows how to access the database with a Data Lake Analytics Catalog management client to list the columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="abd6a-176">실패한 작업 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-176">List failed jobs</span></span>
<span data-ttu-id="abd6a-177">다음 코드에서는 실패한 작업에 대한 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-177">The following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="abd6a-178">파이프라인 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-178">List pipelines</span></span>
<span data-ttu-id="abd6a-179">다음 코드는 계정에 제출된 작업의 각 파이프라인에 대한 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-179">The following code lists information about each pipeline of jobs submitted to the account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="abd6a-180">되풀이 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-180">List recurrences</span></span>
<span data-ttu-id="abd6a-181">다음 코드는 계정에 제출된 작업의 각 되풀이에 대한 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-181">The following code lists information about each recurrence of jobs submitted to the account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="abd6a-182">일반적인 그래프 시나리오</span><span class="sxs-lookup"><span data-stu-id="abd6a-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-the-aad-directory"></a><span data-ttu-id="abd6a-183">AAD 디렉터리에서 사용자 조회</span><span class="sxs-lookup"><span data-stu-id="abd6a-183">Look up user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a><span data-ttu-id="abd6a-184">AAD 디렉터리에서 사용자의 ObjectId 가져오기</span><span class="sxs-lookup"><span data-stu-id="abd6a-184">Get the ObjectId of a user in the AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="abd6a-185">계산 정책 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-185">Manage compute policies</span></span>
<span data-ttu-id="abd6a-186">DataLakeAnalyticsAccountManagementClient 개체는 Data Lake Analytics 계정에 대한 계산 정책을 관리하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-186">The DataLakeAnalyticsAccountManagementClient object provides methods for managing the compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="abd6a-187">계산 정책 나열</span><span class="sxs-lookup"><span data-stu-id="abd6a-187">List compute policies</span></span>
<span data-ttu-id="abd6a-188">다음 코드는 Data Lake Analytics 계정에 대한 계산 정책 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-188">The following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="abd6a-189">새 계산 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="abd6a-189">Create a new compute policy</span></span>
<span data-ttu-id="abd6a-190">다음 코드는 지정된 사용자가 사용할 수 있는 최대 AU를 50으로, 최소 작업 우선 순위를 250으로 설정하는, Data Lake Analytics 계정에 대한 새 계산 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abd6a-190">The following code creates a new compute policy for a Data Lake Analytics account, setting the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="abd6a-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="abd6a-191">Next steps</span></span>
* [<span data-ttu-id="abd6a-192">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="abd6a-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="abd6a-193">Azure 포털을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="abd6a-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="abd6a-194">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="abd6a-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
