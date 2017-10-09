---
title: "blob 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (ASP.NET Core) | Microsoft Docs"
description: "연결 된 서비스 tooget 시작 Visual Studio를 사용 하 여 저장소 계정을 만든 후 Visual Studio ASP.NET Core 프로젝트에 Azure Blob 저장소를 사용 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Azure Blob Storage 및 Visual Studio 연결된 서비스 시작(ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
이 문서에서는 tooget 시작 hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 ASP.NET Core 프로젝트에 Azure 저장소 계정을 참조 하거나 만든 후 Visual Studio에서 Azure Blob 저장소를 사용 하는 방법을 설명 합니다.

Azure Blob 저장소는 많은 양의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다. 단일 Blob은 임의의 크기일 수 있습니다. Blob은 이미지, 오디오 및 비디오 파일, 원시 데이터, 문서 파일 등일 수 있습니다. 이 문서에서는 Visual Studio hello를 사용 하 여 Azure 저장소 계정을 만든 후 tooget blob 저장소 시작 방법 설명 **연결 된 서비스 추가** ASP.NET Core 프로젝트에 대화 상자.

파일이 폴더에 저장되듯이 저장소 Blob은 컨테이너에 저장됩니다. 저장소를 만든 후에 hello 저장소에서 하나 이상의 컨테이너를 만듭니다. 예를 들어 "스크랩" 라는 저장소에서 "이미지" toostore 그림을 호출 하는 hello 저장소의 컨테이너를 만들 수 있습니다 및 다른 호출한 "오디오" toostore 오디오 파일입니다. Hello 컨테이너를 만든 후 파일 toothem 개별 blob를 업로드할 수 있습니다. Blob을 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 을 참조하세요.

## <a name="access-blob-containers-in-code"></a>코드에서 Blob 컨테이너에 액세스하기
ASP.NET Core 프로젝트에 대 한 액세스 blob tooprogrammatically 해야 tooadd hello 다음 항목을 이미 존재 하지 않는 경우.

1. Hello 코드 네임 스페이스 선언을 toohello 위쪽 tooprogrammatically 액세스 메트릭을 제공 하기를 원하는 C# 파일에 다음을 추가 합니다.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다. 다음 코드 tooget hello를 사용 하 여 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **참고:** hello 다음 섹션에서에서 코드 hello 코드 앞에 위의 hello를 모두 사용 합니다.
3. 사용 하 여 한 **CloudBlobClient** tooget 개체는 **CloudBlobContainer** 저장소 계정에 참조 tooan 기존 컨테이너입니다.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>코드에서 컨테이너 만들기
Hello를 사용할 수도 있습니다 **CloudBlobClient** toocreate 저장소 계정의 컨테이너입니다. Toodo 있으면 tooadd 호출 너무**CreateIfNotExistsAsync** 코드 다음 hello와 같이:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**참고:** hello에서 ASP.NET Core tooAzure 저장소 호출을 수행 하는 Api는 비동기 작업입니다. 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요. 아래 hello 코드는 비동기 프로그래밍 메서드를 사용 하 되 고 가정 합니다.

hello 컨테이너 사용 가능한 tooeveryone 내의 toomake hello 파일을 설정할 수 있습니다 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
컨테이너에 있는 blob 파일 tooupload를 컨테이너 참조를 가져오고 tooget blob 참조를 사용 합니다. Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 사용 하는 다음 업로드할 수 있습니다 **UploadFromStreamAsync** 메서드. 이 작업은 아직 실행 하지 않은, 있거나 파일이 있으면 덮어씁니다 hello blob을 만듭니다. hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다. Hello 컨테이너를 호출할 수 있습니다 **ListBlobsSegmentedAsync** 메서드 tooretrieve hello blob 및/또는 디렉터리에 있습니다. tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **IListBlobItem**, tooa 캐스팅 해야 **CloudBlockBlob**, **CloudPageBlob**, 또는  **CloudBlobDirectory** 개체입니다. 경우 입력 hello blob를 알 수 없는 형식 검사 toodetermine 어떤 toocast를 사용할 수 있습니다, 되 게 합니다. 코드 다음 hello tooretrieve 및 출력 컨테이너의 각 항목의 URI hello 방법을 보여 줍니다.

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

Blob 컨테이너의 방법으로 toolist hello 내용의 다른 있습니다. 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) 을 참조하세요.

## <a name="download-a-blob"></a>Blob 다운로드
toodownload blob 가져오려면 먼저 참조 toohello blob를 hello 호출 **DownloadToStreamAsync** 메서드. hello 다음 예제에서는 hello **DownloadToStreamAsync** 메서드 tootransfer hello blob 내용 tooa 스트림 개체를 로컬 파일로 저장할 수 있습니다.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

다른 여러 가지 toosave blob 파일로 합니다. 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) 을 참조하세요.

## <a name="delete-a-blob"></a>Blob 삭제
toodelete blob 가져오려면 먼저 참조 toohello blob를 hello 호출 **DeleteAsync** 메서드를 합니다.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>다음 단계
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

