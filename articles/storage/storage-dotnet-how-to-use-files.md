---
title: ".NET을 사용하여 Azure File Storage 개발 | Microsoft Docs"
description: "Azure File Storage를 사용하여 파일 데이터를 저장하는 .NET 응용 프로그램 및 서비스를 개발하는 방법을 알아봅니다."
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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="9ca6f-103">.NET을 사용하여 Azure File Storage 개발</span><span class="sxs-lookup"><span data-stu-id="9ca6f-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="9ca6f-104">이 문서에서는 .NET 코드를 사용하여 Azure File Storage를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="9ca6f-105">Azure File Storage에 대한 자세한 내용은 [Azure File Storage 소개](storage-files-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="9ca6f-106">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="9ca6f-106">About this tutorial</span></span>
<span data-ttu-id="9ca6f-107">이 자습서에서는 .NET을 사용하여 Azure File Storage를 사용하여 파일 데이터를 저장하는 응용 프로그램이나 서비스를 개발하는 데 필요한 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="9ca6f-108">즉 간단한 콘솔 응용 프로그램을 만들고, .NET 및 Azure File Storage를 통해 기본 동작을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="9ca6f-109">파일 내용 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ca6f-109">Get the contents of a file</span></span>
* <span data-ttu-id="9ca6f-110">파일 공유에 대한 할당량(최대 크기) 설정</span><span class="sxs-lookup"><span data-stu-id="9ca6f-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="9ca6f-111">공유에 정의된 공유 액세스 정책을 사용하는 파일에 대해 공유 액세스 서명(SAS 키) 만들기</span><span class="sxs-lookup"><span data-stu-id="9ca6f-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="9ca6f-112">동일한 저장소 계정의 다른 파일로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="9ca6f-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="9ca6f-113">동일한 저장소 계정의 blob으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="9ca6f-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="9ca6f-114">문제 해결을 위해 Azure 저장소 메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="9ca6f-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="9ca6f-115">Azure File Storage는 SMB를 통해 액세스할 수 있기 때문에 파일 I/O에 대한 표준 System.IO 클래스를 사용하여 Azure 파일 공유에 액세스하는 간단한 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="9ca6f-116">이 문서에서는 [Azure File Storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api)를 사용하여 Azure File Storage와 통신하는 Azure Storage .NET SDK를 사용하는 응용 프로그램을 작성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="9ca6f-117">콘솔 응용 프로그램 만들기 및 어셈블리 가져오기</span><span class="sxs-lookup"><span data-stu-id="9ca6f-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="9ca6f-118">Visual Studio에서 새로운 Windows 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="9ca6f-119">다음 단계에서는 Visual Studio 2017에서 콘솔 응용 프로그램을 만드는 방법을 보여 줍니다. 이 단계는 다른 버전의 Visual Studio에서도 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="9ca6f-120">**파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="9ca6f-121">**설치됨** > **템플릿** > **Visual C#** > **Windows 기본 바탕 화면**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="9ca6f-122">**콘솔 앱(.NET Framework)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="9ca6f-123">**이름:** 필드에서 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="9ca6f-124">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-124">Select **OK**</span></span>

<span data-ttu-id="9ca6f-125">이 자습서의 모든 코드 예제는 콘솔 응용 프로그램에 있는 `Program.cs` 파일의 `Main()` 메서드에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="9ca6f-126">Azure 클라우드 서비스, 웹앱, 데스크톱 및 모바일 응용 프로그램을 포함하여 .NET 응용 프로그램의 모든 형식에서 Azure Storage 클라이언트 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="9ca6f-127">이 가이드에서는 편의상 콘솔 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="9ca6f-128">NuGet을 사용하여 필요한 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="9ca6f-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="9ca6f-129">이 자습서를 완료하기 위해 프로젝트에서 참조해야 하는 두 개의 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="9ca6f-130">[.NET용 Microsoft Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/): 이 패키지는 저장소 계정에서 데이터 리소스에 프로그래밍 방식의 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="9ca6f-131">[.NET용 Microsoft Azure 구성 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): 이 패키지는 응용 프로그램을 실행하는 위치에 관계없이 구성 파일에서 연결 문자열을 구문 분석하기 위한 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="9ca6f-132">NuGet을 사용하여 패키지를 모두 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="9ca6f-133">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-133">Follow these steps:</span></span>

1. <span data-ttu-id="9ca6f-134">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="9ca6f-135">온라인에서 "WindowsAzure.Storage"를 검색하고 **설치** 를 클릭하여 저장소 클라이언트 라이브러리와 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="9ca6f-136">온라인에서 "WindowsAzure.ConfigurationManager"를 검색하고 **설치**를 클릭하여 Azure 구성 관리자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="9ca6f-137">저장소 계정 자격 증명을 app.config 파일에 저장</span><span class="sxs-lookup"><span data-stu-id="9ca6f-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="9ca6f-138">다음에는 프로젝트의 app.config 파일에 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="9ca6f-139">다음과 비슷하게 app.config 파일을 편집합니다. 여기서는 `myaccount`을(를) 저장소 계정 이름으로 바꾸고 `mykey`을(를) 저장소 계정 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> 최신 버전의 Azure 저장소 에뮬레이터는 Azure File Storage를 지원하지 않습니다. <span data-ttu-id="9ca6f-141">Azure File Storage를 사용하려면 연결 문자열이 클라우드의 Azure Storage 계정을 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="9ca6f-142">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="9ca6f-142">Add using directives</span></span>
<span data-ttu-id="9ca6f-143">솔루션 탐색기에서 `Program.cs` 파일을 열고 지시문을 사용하여 파일 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="9ca6f-144">프로그래밍 방식으로 파일 공유 액세스</span><span class="sxs-lookup"><span data-stu-id="9ca6f-144">Access the file share programmatically</span></span>
<span data-ttu-id="9ca6f-145">다음에는 위에 표시된 코드 뒤에 나오는 `Main()` 메서드에 다음 코드를 추가하여 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="9ca6f-146">이 코드는 이전에 만든 파일에 대한 참조를 가져오고 해당 내용을 콘솔 창에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="9ca6f-147">콘솔 응용 프로그램을 실행하여 출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="9ca6f-148">파일 공유에 대한 최대 크기 설정</span><span class="sxs-lookup"><span data-stu-id="9ca6f-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="9ca6f-149">Azure 저장소 클라이언트 라이브러리 버전 5.x부터 파일 공유에 대한 할당량(또는 최대 크기)을 기가바이트 단위로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="9ca6f-150">또한 공유에 현재 저장된 데이터의 양도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="9ca6f-151">공유에 대한 할당량을 설정하여 공유에 저장되는 파일의 전체 크기를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="9ca6f-152">공유에 있는 파일의 총 크기가 공유에 대해 설정된 할당량을 초과하면 클라이언트는 해당 파일이 비어 있지 않는 한, 기존 파일의 크기를 늘리거나 새 파일을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="9ca6f-153">아래 예제에서는 공유에 대한 현재 사용량을 확인하고 공유에 대해 할당량을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="9ca6f-154">파일 또는 파일 공유에 대한 공유 액세스 서명 생성</span><span class="sxs-lookup"><span data-stu-id="9ca6f-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="9ca6f-155">Azure 저장소 클라이언트 라이브러리 버전 5.x부터 파일 공유 또는 개별 파일에 대해 SAS(공유 액세스 서명)를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="9ca6f-156">또한 파일 공유에 대해 공유 액세스 정책을 만들어 공유 액세스 서명을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="9ca6f-157">공유 액세스 정책을 만들면 노출된 SAS를 해지할 수 있으므로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="9ca6f-158">다음 예제에서는 공유에 대해 공유 액세스 정책을 만들고 해당 정책을 사용하여 공유의 파일에 대해 SAS에 대한 제약 조건을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="9ca6f-159">공유 액세스 서명을 만들고 사용하는 방법에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 및 [Azure Blob을 사용하여 SAS 만들기 및 사용](storage-dotnet-shared-access-signature-part-2.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="9ca6f-160">파일 복사</span><span class="sxs-lookup"><span data-stu-id="9ca6f-160">Copy files</span></span>
<span data-ttu-id="9ca6f-161">Azure 저장소 클라이언트 라이브러리 버전 5.x부터 파일을 다른 파일로, 파일을 blob으로 또는 blob을 파일로 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="9ca6f-162">다음 섹션에는 이러한 복사 작업을 프로그래밍 방식으로 수행하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="9ca6f-163">AzCopy를 사용하여 파일을 다른 파일로 복사하거나 blob을 파일로 복사할 수도 있고 그 반대로 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="9ca6f-164">[AzCopy 명령줄 유틸리티로 데이터 전송](storage-use-azcopy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-164">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9ca6f-165">blob을 파일에 복사하거나 파일을 blob에 복사하는 경우 두 항목이 동일한 저장소 계정 내에 있더라도 SAS(공유 액세스 서명)를 사용하여 원본 개체를 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="9ca6f-166">**다른 파일에 파일 복사** 다음 예제에서는 동일한 공유의 다른 파일에 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="9ca6f-167">이 복사 작업은 동일한 저장소 계정의 파일 간에 복사를 수행하므로 공유 키 인증을 사용하여 복사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="9ca6f-168">**Blob에 파일 복사** 다음 예제에서는 파일을 만들고 동일한 저장소 계정 내의 Blob에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="9ca6f-169">이 예제에서 서비스는 복사 작업 동안 원본 파일에 대한 액세스를 인증하는 데 사용하는 소스 파일용 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="9ca6f-170">동일한 방식으로 blob을 파일에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="9ca6f-171">원본 개체가 blob인 경우 복사 작업 동안 해당 blob에 대한 액세스를 인증하는 SAS를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="9ca6f-172">메트릭을 사용하여 Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9ca6f-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="9ca6f-173">이제 Azure Storage 분석은 Azure File Storage에 대한 메트릭을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="9ca6f-174">메트릭 데이터를 사용하여 요청을 추적하고 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="9ca6f-175">[Azure Portal](https://portal.azure.com)에서 Azure File Storage에 대한 메트릭을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="9ca6f-176">또한 REST API 또는 저장소 클라이언트 라이브러리의 유사한 기능 중 하나를 통해 파일 서비스 설정 속성을 호출하여 프로그래밍 방식으로 메트릭을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="9ca6f-177">다음 코드 예제에서는 .NET용 저장소 클라이언트 라이브러리를 사용하여 Azure File Storage에 대한 메트릭을 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="9ca6f-178">먼저 위에서 추가한 항목 외에도 다음 `using` 지시문을 `Program.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="9ca6f-179">Azure Blob, Azure 테이블 및 Azure 큐는 `Microsoft.WindowsAzure.Storage.Shared.Protocol`네임스페이스에서 `ServiceProperties` 공유 형식을 사용하지만, Azure File Storage는 `Microsoft.WindowsAzure.Storage.File.Protocol` 네임스페이스에서 `FileServiceProperties` 고유 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="9ca6f-180">그러나 두 네임스페이스는 컴파일할 다음 코드의 경우 코드에서 참조되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

<span data-ttu-id="9ca6f-181">또한 종단 간 문제 해결 지침에 대해서는 [Azure File Storage 문제 해결 문서](storage-troubleshoot-file-connection-problems.md)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ca6f-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ca6f-182">Next steps</span></span>
<span data-ttu-id="9ca6f-183">Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9ca6f-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="9ca6f-184">개념 문서 및 비디오</span><span class="sxs-lookup"><span data-stu-id="9ca6f-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="9ca6f-185">Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)</span><span class="sxs-lookup"><span data-stu-id="9ca6f-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="9ca6f-186">Linux에서 Azure File Storage 사용 방법</span><span class="sxs-lookup"><span data-stu-id="9ca6f-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="9ca6f-187">파일 저장소용 도구 지원</span><span class="sxs-lookup"><span data-stu-id="9ca6f-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="9ca6f-188">Azure 저장소와 함께 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="9ca6f-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="9ca6f-189">Microsoft Azure 저장소와 함께 AzCopy를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9ca6f-189">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="9ca6f-190">Azure 저장소에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="9ca6f-190">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="9ca6f-191">Azure File Storage 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9ca6f-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="9ca6f-192">참조</span><span class="sxs-lookup"><span data-stu-id="9ca6f-192">Reference</span></span>
* [<span data-ttu-id="9ca6f-193">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="9ca6f-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="9ca6f-194">파일 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="9ca6f-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="9ca6f-195">블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="9ca6f-195">Blog posts</span></span>
* [<span data-ttu-id="9ca6f-196">Azure 파일 저장소 일반적으로 사용 가능(영문)</span><span class="sxs-lookup"><span data-stu-id="9ca6f-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="9ca6f-197">Azure File Storage 내부 구조(영문)</span><span class="sxs-lookup"><span data-stu-id="9ca6f-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="9ca6f-198">Microsoft Azure 파일 서비스 소개</span><span class="sxs-lookup"><span data-stu-id="9ca6f-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="9ca6f-199">Microsoft Azure File Storage에 대한 연결 유지(영문)</span><span class="sxs-lookup"><span data-stu-id="9ca6f-199">Persisting connections to Microsoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)