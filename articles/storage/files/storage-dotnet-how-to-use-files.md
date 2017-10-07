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
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>.NET을 사용하여 Azure File Storage 개발 
> [!NOTE]
> 이 문서에서는 어떻게 toomanage.NET 코드와 함께 Azure 파일 저장소. Azure 파일 저장소에 대해 자세히 toolearn를 참조 하십시오. hello [소개 tooAzure 파일 저장소](storage-files-introduction.md)합니다.
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는.NET toodevelop 응용 프로그램이 나 Azure 파일 저장소 toostore 파일 데이터를 사용 하는 서비스를 사용 하 여의 hello 기본 사항을 보여 줍니다. 이 자습서에서는 간단한 콘솔 응용 프로그램 만들어져 표시 방법을.NET 및 Azure 파일 저장소를 사용 하 여 기본 동작 tooperform:

* 파일의 hello 내용 가져오기
* Hello 파일 공유에 대 한 hello 할당량 (최대 크기)을 설정 합니다.
* Hello 공유에 정의 된 공유 액세스 정책을 사용 하는 파일에 대 한 공유 액세스 서명 (SAS 키)를 만듭니다.
* Hello에 파일 tooanother 파일을 복사 합니다. 동일한 저장소 계정입니다.
* Hello에 파일 tooa blob 복사 동일한 저장소 계정입니다.
* 문제 해결을 위해 Azure 저장소 메트릭 사용

> [!Note]  
> SMB를 통한 Azure 파일 저장소에 액세스할 수 있습니다, 되므로 파일 I/O에 대 한 hello 표준 System.IO 클래스를 사용 하 여 hello Azure 파일 공유에 액세스 가능한 toowrite 간단한 응용 프로그램. 이 문서에서는 방법을 사용 하는 응용 프로그램 toowrite hello hello를 사용 하 여 Azure 저장소.NET SDK에 설명 [Azure 파일 저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 파일 저장소. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Hello 어셈블리를 가져오고 hello 콘솔 응용 프로그램 만들기
Visual Studio에서 새로운 Windows 콘솔 응용 프로그램을 만듭니다. 그러나 단계를 수행 하는 hello 어떻게 toocreate 2017 년 hello 단계 Visual Studio에서 콘솔 응용 프로그램은 다른 버전의 Visual Studio와 비슷한 보여 줍니다.

1. **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
2. **설치됨** > **템플릿** > **Visual C#** > **Windows 기본 바탕 화면**을 선택합니다.
3. **콘솔 앱(.NET Framework)**를 선택합니다.
4. Hello에 응용 프로그램에 대 한 이름을 입력 **이름:** 필드
5. **확인**을 선택합니다.

이 자습서의 모든 코드 예제를 추가할 수 있습니다 toohello `Main()` 콘솔 응용 프로그램의 메서드에 `Program.cs` 파일입니다.

Azure 클라우드 서비스 또는 웹 앱을 포함 하 여.NET 응용 프로그램 및 데스크톱 및 모바일 응용 프로그램의 종류에 hello Azure 저장소 클라이언트 라이브러리를 사용할 수 있습니다. 이 가이드에서는 편의상 콘솔 응용 프로그램을 사용합니다.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>NuGet tooinstall hello 필요한 패키지를 사용 하 여
Tooreference에에서 필요한 프로젝트 toocomplete이 자습서이에서는 두 개의 패키지가 있습니다.

* [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/):이 패키지 toodata 리소스 저장소 계정에 프로그래밍 방식의 액세스를 제공 합니다.
* [.NET용 Microsoft Azure 구성 관리자 라이브러리](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): 이 패키지는 응용 프로그램을 실행하는 위치에 관계없이 구성 파일에서 연결 문자열을 구문 분석하기 위한 클래스를 제공합니다.

Tooobtain NuGet 패키지를 모두 사용할 수 있습니다. 다음 단계를 수행하세요.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
2. "WindowsAzure.Storage" 온라인 검색 하 고 클릭 **설치** tooinstall hello 저장소 클라이언트 라이브러리 및 해당 종속성.
3. "WindowsAzure.ConfigurationManager" 온라인 검색 하 고 클릭 **설치** tooinstall hello Azure 구성 관리자.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>저장소 계정 자격 증명 toohello app.config 파일을 저장 합니다.
다음에는 프로젝트의 app.config 파일에 자격 증명을 저장합니다. 다음 예에서는, 대체 유사한 toohello 나타나도록 hello app.config 파일을 편집 `myaccount` 을 저장소 계정 이름으로, 및 `mykey` 저장소 계정 키를 가진 합니다.

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
> hello Azure 저장소 에뮬레이터의 hello 최신 버전에서 Azure 파일 저장소를 지원 하지 않습니다. 연결 문자열에 Azure 파일 저장소 hello 클라우드 toowork에서 Azure 저장소 계정을 대상으로 해야 합니다.

## <a name="add-using-directives"></a>지시문을 사용하여 추가
열기 hello `Program.cs` 솔루션 탐색기에서 파일을 hello 다음 추가 hello 파일의 지시문 toohello top을 사용 하 여 합니다.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Access hello 파일 공유를 프로그래밍 방식으로
다음으로, 다음 코드 toohello hello 추가 `Main()` 메서드 (위에 표시 된 hello 코드) 이후 tooretrieve hello 연결 문자열입니다. 이 코드는 앞에서 만든 참조 toohello 파일 가져오고 내용을 toohello 콘솔 창 출력 합니다.

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

Hello 콘솔 응용 프로그램 toosee hello 출력을 실행 합니다.

## <a name="set-hello-maximum-size-for-a-file-share"></a>파일 공유에 대 한 hello 최대 크기 설정
버전 부터는 hello Azure 저장소 클라이언트 라이브러리의 5.x 또는 설정할 수 있습니다 집합 hello 할당량 (최대 크기) 파일 공유에 대 한 (기가바이트)에서입니다. 데이터의 양을 현재 hello 공유에 저장 된 toosee를 확인할 수 있습니다.

공유에 대 한 hello 할당량을 설정 하 여 hello hello 공유에 저장 된 hello 파일의 전체 크기를 제한할 수 있습니다. Hello hello 공유에 있는 파일의 전체 크기를 초과 하는 경우 hello 공유에 hello 할당량을 설정한 후 클라이언트는 수 없습니다 tooincrease hello 크기의 기존 파일 또는 이러한 파일은 비어 경우가 아니면 새 파일을 만듭니다.

다음 예제에서는 hello 방법을 toocheck hello 공유에 대 한 현재 사용량 및 tooset hello 공유에 대 한 할당량을 hello 하는 방법을 보여 줍니다.

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>파일 또는 파일 공유에 대한 공유 액세스 서명 생성
버전 부터는 5.x hello Azure 저장소 클라이언트 라이브러리, 파일 공유 또는 개별 파일에 대 한 공유 액세스 서명 (SAS)를 생성할 수 있습니다. 서명 파일 공유 toomanage 공유 액세스에 공유 액세스 정책을도 만들 수 있습니다. 공유 액세스 정책 만들기 좋습니다 해야 손상 되 면 hello SAS를 해지 하는 수단을 제공 합니다.

다음 예제는 hello 공유에 공유 액세스 정책을 만들고 정책 tooprovide hello 제약 조건을 SAS에 대 한 hello에서 파일 공유를 사용 하 여 합니다.

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

공유 액세스 서명을 만들고 사용하는 방법에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) 및 [Azure Blob을 사용하여 SAS 만들기 및 사용](../blobs/storage-dotnet-shared-access-signature-part-2.md)을 참조하세요.

## <a name="copy-files"></a>파일 복사
버전 부터는 5.x hello Azure 저장소 클라이언트 라이브러리, 파일 tooanother 파일, 파일 tooa blob 또는 blob tooa 파일을 복사할 수 있습니다. Hello 다음 섹션에 대해서도 설명 방법을 tooperform 이러한 복사 작업 프로그래밍 방식으로 합니다.

또한 AzCopy toocopy 하나의 파일 tooanother 또는 blob tooa 파일 되거나 그 반대 방향 toocopy를 사용할 수 있습니다. 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)합니다.

> [!NOTE]
> 복사 하는 hello 내에서 동일한 경우에 된 공유 액세스 서명 (SAS) tooauthenticate hello 원본 개체를 사용 해야 blob tooa 파일 또는 파일 tooa blob를 복사 하는 경우 저장소 계정입니다.
> 
> 

**파일 tooanother 파일 복사** hello 다음 예제에서는 파일을 복사 파일 tooanother hello에 동일한 공유 합니다. 이 복사 작업 간에 복사 하므로 파일에 hello 동일한 저장소 계정, 공유 키 인증 tooperform hello 복사본을 사용할 수 있습니다.

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

**파일 tooa blob 복사** hello 다음 예제에서는 파일을 만들고 hello 내 tooa blob 복사 동일한 저장소 계정입니다. hello 예제는 hello 서비스 tooauthenticate 액세스 toohello 소스 파일을 사용 하 여 hello 복사 작업 중 hello 소스 파일에 대 한 SAS를 만듭니다.

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

Hello에 blob tooa 파일을 복사할 수는 있지만 동일한 방식으로 합니다. Hello 소스 개체가 blob 인 경우 다음 hello 복사 작업 동안 SAS tooauthenticate 액세스 toothat blob을 만듭니다.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>메트릭을 사용하여 Azure File Storage 문제 해결
이제 Azure Storage 분석은 Azure File Storage에 대한 메트릭을 지원합니다. 메트릭 데이터를 사용하여 요청을 추적하고 문제를 진단할 수 있습니다.


Hello에서 Azure 파일 저장소에 대 한 메트릭을 사용 하도록 설정할 수 [Azure 포털](https://portal.azure.com)합니다. 또한 메트릭 호출 hello hello REST API를 통해 파일 서비스 속성 설정 작업 또는 hello 저장소 클라이언트 라이브러리에에서 해당 하는 유사한 점은 중 하나에서 프로그래밍 방식으로 설정할 수 있습니다.


다음 코드 예제는 hello toouse Azure 파일 저장소에 대 한.NET tooenable 메트릭 용 저장소 클라이언트 라이브러리를 hello 하는 방법을 보여 줍니다.

첫째, hello 다음 추가 `using` 지시문 tooyour `Program.cs` 위에 추가 toothose 또한 파일:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Azure Blob, Azure 테이블 및 Azure 큐는 동안 공유 hello를 사용 하는 참고 `ServiceProperties` hello에 대 한 형식 `Microsoft.WindowsAzure.Storage.Shared.Protocol` 네임 스페이스, Azure 파일 저장소 사용 하 여 고유한 형식이 hello `FileServiceProperties` hello에 대 한 형식 `Microsoft.WindowsAzure.Storage.File.Protocol` 네임 스페이스입니다. 그러나 두 네임 스페이스 참조 해야 사용자 코드에서 코드 toocompile 다음 hello에 대 한 합니다.

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

또한 참조할 수 있습니다 너무[Azure 파일 저장소 문제 해결 문서](storage-troubleshoot-windows-file-connection-problems.md) 종단 간 문제 해결 지침에 대 한 합니다.

## <a name="next-steps"></a>다음 단계
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

### <a name="conceptual-articles-and-videos"></a>개념 문서 및 비디오
* [Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [어떻게 toouse Linux로 Azure 파일 저장소](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>파일 저장소용 도구 지원
* [어떻게 toouse AzCopy Microsoft Azure 저장소](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 Azure 저장소](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Azure File Storage 문제 해결](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>참조
* [Storage Client Library for .NET 참조](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [파일 서비스 REST API 참조](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>블로그 게시물
* [Azure 파일 저장소 일반적으로 사용 가능(영문)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure File Storage 내부 구조(영문)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 파일 서비스 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [영구 연결 tooMicrosoft Azure 파일 저장소](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
