---
title: "Azure 파일 저장소.NET에 대 한 aaaDevelop | Microsoft Docs"
description: "어떻게 toodevelop.NET 응용 프로그램 및 서비스 Azure 파일 저장소 toostore를 사용 하는 파일 데이터에 알아봅니다."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="3af49-103">.NET을 사용하여 Azure File Storage 개발</span><span class="sxs-lookup"><span data-stu-id="3af49-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="3af49-104">이 문서에서는 어떻게 toomanage.NET 코드와 함께 Azure 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="3af49-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="3af49-105">Azure 파일 저장소에 대해 자세히 toolearn를 참조 하십시오. hello [소개 tooAzure 파일 저장소](storage-files-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="3af49-106">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="3af49-106">About this tutorial</span></span>
<span data-ttu-id="3af49-107">이 자습서에서는.NET toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="3af49-108">이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을.NET 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:</span><span class="sxs-lookup"><span data-stu-id="3af49-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="3af49-109">파일의 hello 내용 가져오기</span><span class="sxs-lookup"><span data-stu-id="3af49-109">Get hello contents of a file</span></span>
* <span data-ttu-id="3af49-110">Hello 파일 공유에 대 한 hello 할당량 (최대 크기)을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="3af49-111">Hello 공유에 정의 된 공유 액세스 정책을 사용 하는 파일에 대 한 공유 액세스 서명 (SAS 키)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="3af49-112">Hello에 파일 tooanother 파일을 복사 합니다. 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="3af49-113">Hello에 파일 tooa blob 복사 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="3af49-114">문제 해결을 위해 Azure 저장소 메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="3af49-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="3af49-115">SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 파일 I/O에 대 한 hello 표준 System.IO 클래스를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="3af49-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="3af49-116">이 문서에서는 방법을 사용 하는 응용 프로그램 toowrite hello hello를 사용 하 여 Azure 저장소.NET SDK에 설명 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소.</span><span class="sxs-lookup"><span data-stu-id="3af49-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="3af49-117">Hello 어셈블리를 가져오고 hello 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3af49-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="3af49-118">Visual Studio에서 새로운 Windows 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="3af49-119">그러나 단계를 수행 하는 hello 어떻게 toocreate 2017 년 hello 단계 Visual Studio에서 콘솔 응용 프로그램은 다른 버전의 Visual Studio와 비슷한 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="3af49-120">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="3af49-121">**설치됨** > **템플릿** > **Visual C#** > **Windows 기본 바탕 화면**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="3af49-122">**콘솔 앱(.NET Framework)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="3af49-123">Hello에 응용 프로그램에 대 한 이름을 입력 **이름:** 필드</span><span class="sxs-lookup"><span data-stu-id="3af49-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="3af49-124">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-124">Select **OK**</span></span>

<span data-ttu-id="3af49-125">이 자습서의 모든 코드 예제를 추가할 수 있습니다 toohello `Main()` 콘솔 응용 프로그램의 메서드에 `Program.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="3af49-126">Azure 클라우드 서비스 또는 웹 앱을 포함 하 여.NET 응용 프로그램 및 데스크톱 및 모바일 응용 프로그램의 종류에 hello Azure 저장소 클라이언트 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="3af49-127">이 가이드에서는 편의상 콘솔 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="3af49-128">NuGet tooinstall hello 필요한 패키지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3af49-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="3af49-129">Tooreference에에서 필요한 프로젝트 toocomplete이 자습서이에서는 두 개의 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="3af49-130">[.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/):이 패키지 toodata 리소스 저장소 계정에 프로그래밍 방식의 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="3af49-131">[.NET용 Microsoft Azure 구성 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): 이 패키지는 응용 프로그램을 실행하는 위치에 관계없이 구성 파일에서 연결 문자열을 구문 분석하기 위한 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="3af49-132">Tooobtain NuGet 패키지를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="3af49-133">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="3af49-133">Follow these steps:</span></span>

1. <span data-ttu-id="3af49-134">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3af49-135">"WindowsAzure.Storage" 온라인 검색 하 고 클릭 **설치** tooinstall hello 저장소 클라이언트 라이브러리 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="3af49-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="3af49-136">"WindowsAzure.ConfigurationManager" 온라인 검색 하 고 클릭 **설치** tooinstall hello Azure 구성 관리자.</span><span class="sxs-lookup"><span data-stu-id="3af49-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="3af49-137">저장소 계정 자격 증명 toohello app.config 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="3af49-138">다음에는 프로젝트의 app.config 파일에 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="3af49-139">다음 예에서는, 대체 유사한 toohello 나타나도록 hello app.config 파일을 편집 `myaccount` 을 저장소 계정 이름으로, 및 `mykey` 저장소 계정 키를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> hello Azure 저장소 에뮬레이터의 hello 최신 버전에서 Azure 파일 저장소를 지원 하지 않습니다. <span data-ttu-id="3af49-141">연결 문자열에 Azure 파일 저장소 hello 클라우드 toowork에서 Azure 저장소 계정을 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="3af49-142">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="3af49-142">Add using directives</span></span>
<span data-ttu-id="3af49-143">열기 hello `Program.cs` 솔루션 탐색기에서 파일을 hello 다음 추가 hello 파일의 지시문 toohello top을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="3af49-144">Access hello 파일 공유를 프로그래밍 방식으로</span><span class="sxs-lookup"><span data-stu-id="3af49-144">Access hello file share programmatically</span></span>
<span data-ttu-id="3af49-145">다음으로, 다음 코드 toohello hello 추가 `Main()` 메서드 (위에 표시 된 hello 코드) 이후 tooretrieve hello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="3af49-146">이 코드는 앞에서 만든 참조 toohello 파일 가져오고 내용을 toohello 콘솔 창 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="3af49-147">Hello 콘솔 응용 프로그램 toosee hello 출력을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="3af49-148">파일 공유에 대 한 hello 최대 크기 설정</span><span class="sxs-lookup"><span data-stu-id="3af49-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="3af49-149">버전 부터는 hello Azure 저장소 클라이언트 라이브러리의 5.x 또는 설정할 수 있습니다 집합 hello 할당량 (최대 크기) 파일 공유에 대 한 (기가바이트)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="3af49-150">데이터의 양을 현재 hello 공유에 저장 된 toosee를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="3af49-151">공유에 대 한 hello 할당량을 설정 하 여 hello hello 공유에 저장 된 hello 파일의 전체 크기를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="3af49-152">Hello hello 공유에 있는 파일의 전체 크기를 초과 하는 경우 hello 공유에 hello 할당량을 설정한 후 클라이언트는 수 없습니다 tooincrease hello 크기의 기존 파일 또는 이러한 파일은 비어 경우가 아니면 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="3af49-153">다음 예제에서는 hello 방법을 toocheck hello 공유에 대 한 현재 사용량 및 tooset hello 공유에 대 한 할당량을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="3af49-154">파일 또는 파일 공유에 대한 공유 액세스 서명 생성</span><span class="sxs-lookup"><span data-stu-id="3af49-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="3af49-155">버전 부터는 5.x hello Azure 저장소 클라이언트 라이브러리, 파일 공유 또는 개별 파일에 대 한 공유 액세스 서명 (SAS)를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="3af49-156">서명 파일 공유 toomanage 공유 액세스에 공유 액세스 정책을도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="3af49-157">공유 액세스 정책 만들기 좋습니다 해야 손상 되 면 hello SAS를 해지 하는 수단을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="3af49-158">다음 예제는 hello 공유에 공유 액세스 정책을 만들고 정책 tooprovide hello 제약 조건을 SAS에 대 한 hello에서 파일 공유를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="3af49-159">공유 액세스 서명을 만들고 사용하는 방법에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 및 [Azure Blob을 사용하여 SAS 만들기 및 사용](storage-dotnet-shared-access-signature-part-2.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3af49-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="3af49-160">파일 복사</span><span class="sxs-lookup"><span data-stu-id="3af49-160">Copy files</span></span>
<span data-ttu-id="3af49-161">버전 부터는 5.x hello Azure 저장소 클라이언트 라이브러리, 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="3af49-162">Hello 다음 섹션에 대해서도 설명 방법을 tooperform 이러한 복사 작업 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="3af49-163">또한 AzCopy toocopy 하나의 파일 tooanother 또는 blob tooa 파일 되거나 그 반대 방향 toocopy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="3af49-164">참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-164">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3af49-165">복사 하는 hello 내에서 동일한 경우에 된 공유 액세스 서명 (SAS) tooauthenticate hello 원본 개체를 사용 해야 blob tooa 파일 또는 파일 tooa blob를 복사 하는 경우 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="3af49-166">**파일 tooanother 파일 복사** hello 다음 예제에서는 파일을 복사 파일 tooanother hello에 동일한 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="3af49-167">이 복사 작업 간에 복사 하므로 파일에 hello 동일한 저장소 계정, 공유 키 인증 tooperform hello 복사본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="3af49-168">**파일 tooa blob 복사** hello 다음 예제에서는 파일을 만들고 hello 내 tooa blob 복사 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="3af49-169">hello 예제는 hello 서비스 tooauthenticate 액세스 toohello 소스 파일을 사용 하 여 hello 복사 작업 중 hello 소스 파일에 대 한 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="3af49-170">Hello에 blob tooa 파일을 복사할 수는 있지만 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="3af49-171">Hello 소스 개체가 blob 인 경우 다음 hello 복사 작업 동안 SAS tooauthenticate 액세스 toothat blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="3af49-172">메트릭을 사용하여 Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3af49-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="3af49-173">이제 Azure Storage 분석은 Azure File Storage에 대한 메트릭을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="3af49-174">메트릭 데이터를 사용하여 요청을 추적하고 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="3af49-175">Hello에서 Azure 파일 저장소에 대 한 메트릭을 사용 하도록 설정할 수 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="3af49-176">또한 메트릭 호출 hello hello REST API를 통해 파일 서비스 속성 설정 작업 또는 hello 저장소 클라이언트 라이브러리에에서 해당 하는 유사한 점은 중 하나에서 프로그래밍 방식으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="3af49-177">다음 코드 예제는 hello toouse Azure 파일 저장소에 대 한.NET tooenable 메트릭 용 저장소 클라이언트 라이브러리를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="3af49-178">첫째, hello 다음 추가 `using` 지시문 tooyour `Program.cs` 위에 추가 toothose 또한 파일:</span><span class="sxs-lookup"><span data-stu-id="3af49-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="3af49-179">Azure Blob, Azure 테이블 및 Azure 큐는 동안 공유 hello를 사용 하는 참고 `ServiceProperties` hello에 대 한 형식 `Microsoft.WindowsAzure.Storage.Shared.Protocol` 네임 스페이스, Azure 파일 저장소 사용 하 여 고유한 형식이 hello `FileServiceProperties` hello에 대 한 형식 `Microsoft.WindowsAzure.Storage.File.Protocol` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="3af49-180">그러나 두 네임 스페이스 참조 해야 사용자 코드에서 코드 toocompile 다음 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="3af49-181">또한 참조할 수 있습니다 너무[Azure 파일 저장소 문제 해결 문서](storage-troubleshoot-file-connection-problems.md) 종단 간 문제 해결 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3af49-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3af49-182">Next steps</span></span>
<span data-ttu-id="3af49-183">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3af49-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="3af49-184">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="3af49-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="3af49-185">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="3af49-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="3af49-186">어떻게 toouse Linux로 Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="3af49-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="3af49-187">파일 저장소용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="3af49-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="3af49-188">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="3af49-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="3af49-189">어떻게 toouse AzCopy Microsoft Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="3af49-189">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="3af49-190">Hello Azure CLI를 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="3af49-190">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="3af49-191">Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3af49-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="3af49-192">참조</span><span class="sxs-lookup"><span data-stu-id="3af49-192">Reference</span></span>
* [<span data-ttu-id="3af49-193">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="3af49-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="3af49-194">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="3af49-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="3af49-195">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="3af49-195">Blog posts</span></span>
* [<span data-ttu-id="3af49-196">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="3af49-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="3af49-197">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="3af49-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="3af49-198">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="3af49-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="3af49-199">영구 연결 tooMicrosoft Azure 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="3af49-199">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
