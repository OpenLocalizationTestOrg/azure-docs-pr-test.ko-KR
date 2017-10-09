---
title: "blob 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (클라우드 서비스) | Microsoft Docs"
description: "연결 된 서비스를 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Visual Studio에서 클라우드 서비스 프로젝트에서 Azure Blob 저장소를 사용 하 여 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(클라우드 서비스 프로젝트)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
이 문서에서 설명 하는 hello Visual Studio를 사용 하 여 Azure 저장소 계정을 참조 하거나 만든 후 tooget Azure Blob 저장소 시작 방법을 **연결 된 서비스 추가** 대화 상자에 Visual Studio 클라우드 서비스 프로젝트입니다. 방식을 보여줍니다 tooaccess blob 컨테이너 및 업로드, 나열 및 blob를 다운로드할 tooperform 일반적인 작업의 같은 방식을 만듭니다. hello 샘플은 C로 작성 된\# hello를 사용 하 여 [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx)합니다.

Azure Blob 저장소는 많은 양의 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 구조화 되지 않은 데이터를 저장 하기 위한 서비스입니다. 단일 Blob은 임의의 크기일 수 있습니다. Blob은 이미지, 오디오 및 비디오 파일, 원시 데이터, 문서 파일 등일 수 있습니다.

파일이 폴더에 저장되듯이 저장소 Blob은 컨테이너에 저장됩니다. 저장소를 만든 후에 hello 저장소에서 하나 이상의 컨테이너를 만듭니다. 예를 들어 "스크랩" 라는 저장소에서 "이미지" toostore 그림을 호출 하는 hello 저장소의 컨테이너를 만들 수 있습니다 및 다른 호출한 "오디오" toostore 오디오 파일입니다. Hello 컨테이너를 만든 후 파일 toothem 개별 blob를 업로드할 수 있습니다.

* 프로그래밍 방식으로 조작하는 blob에 대한 자세한 내용은 [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md)을 참조하세요.
* Azure 저장소에 대한 일반 정보는 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)를 참조하세요.
* Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/)를 참조하세요.
* ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net)을 참조하세요.

## <a name="access-blob-containers-in-code"></a>코드에서 Blob 컨테이너에 액세스하기
클라우드 서비스 프로젝트에서 blob를 액세스 하는 tooprogrammatically, 이미 존재 하지 않는 경우 다음 항목을 tooadd hello가 필요 합니다.

1. Azure 저장소 tooprogrammatically 액세스 원하는 모든 C# 파일의 코드 네임 스페이스 선언을 toohello 위쪽 다음 hello를 추가 합니다.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다. 사용 하 여 hello tooget 코드를 다음 저장소 연결 문자열 및 hello Azure 서비스 구성에서 저장소 계정 정보 hello 합니다.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. 가져오기는 **CloudBlobClient** tooreference 저장소 계정에 기존 컨테이너 개체입니다.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. 가져오기는 **CloudBlobContainer** tooreference 특정 blob 컨테이너 개체입니다.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> 모든 hello hello 다음 섹션에에서 표시 된 hello 코드 앞에 이전 절차에 표시 된 hello 코드를 사용 합니다.
> 
> 

## <a name="create-a-container-in-code"></a>코드에서 컨테이너 만들기
> [!NOTE]
> ASP.NET에서 tooAzure 저장소 호출을 수행 하는 일부 Api는 비동기 작업입니다. 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요. 다음 예에서는 hello에 hello 코드는 비동기 프로그래밍 메서드를 사용 하는 가정 합니다.
> 
> 

저장소 계정에서 컨테이너 toocreate toodo 가장 필요한 것은 호출 추가 너무**CreateIfNotExistsAsync** 코드 다음 hello와 같이:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


hello 컨테이너 사용 가능한 tooeveryone 내의 toomake hello 파일을 설정할 수 있습니다 hello 컨테이너 toobe 공용 코드 다음 hello를 사용 하 여.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Hello 인터넷에서 누구나 공용 컨테이너의 blob를 볼 수 있지만 수정 하거나 hello 적절 한 액세스 키가 있는 경우에 삭제할 수 있습니다.

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 Blob 업로드
Azure 저장소는 블록 Blob 및 페이지 Blob을 지원합니다. Hello 대부분의 경우에서 블록 blob는 형식 toouse 권장 hello를 사용 합니다.

tooupload 파일 tooa 블록 blob 컨테이너 참조를 가져오고 tooget 블록 blob 참조를 사용 합니다. Hello를 호출 하 여 모든 스트림 데이터 tooit의 blob 참조를 만든 후 업로드할 수 있습니다 **UploadFromStream** 메서드. 이 작업은 이전에 없던 되거나 파일이 있으면 덮어씁니다 hello blob을 만듭니다. hello 방법을 예제와 다음 tooupload blob 컨테이너에 이미 해당 hello 컨테이너를 만든 가정 합니다.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>컨테이너에서 hello blob 나열
먼저 toolist hello에서에서 컨테이너의 blob를 컨테이너 참조를 가져옵니다. Hello 컨테이너를 사용 하 여 있습니다 **ListBlobs** tooretrieve hello blob 메서드 및/또는 디렉터리에 있습니다. tooaccess 다양 한 속성 및 메서드는 반환 된 작업에 대 한 hello **IListBlobItem**, tooa 캐스팅 해야 **CloudBlockBlob**, **CloudPageBlob**, 또는  **CloudBlobDirectory** 개체입니다. Hello 종류를 알 수 없는 경우 사용할 수 있습니다 형식 검사 toodetermine 어떤 toocast 되 게 합니다. hello 다음 코드에서는 방법을 tooretrieve 및 출력 hello hello의 각 항목의 URI **사진** 컨테이너:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

Hello 앞의 코드 예제와 같이 hello blob 서비스에도 컨테이너 내에서 디렉터리의 hello 개념이 있습니다. 따라서 폴더와 유사한 구조로 Blob을 구성할 수 있습니다. 예를 들어 라는 컨테이너에 블록 blob의 집합을 추적 하는 hello **사진**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

호출 하는 경우 **ListBlobs** hello 컨테이너 (예: hello 이전 샘플)를 반환 하는 hello 컬렉션 포함 **CloudBlobDirectory** 및 **CloudBlockBlob** 개체 hello 디렉터리 및 hello 최상위 수준에 포함 된 blob을 나타내는입니다. Hello 출력 결과 다음과 같습니다.

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


필요에 따라 hello를 설정할 수 있습니다 **UseFlatBlobListing** hello의 매개 변수 **ListBlobs** 메서드를 **true**합니다. 이 경우 디렉터리에 관계없이 모든 Blob이 **CloudBlockBlob**으로 반환됩니다. Hello 호출을 너무 같습니다**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

및 다음은 hello 결과:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

자세한 내용은 [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx)를 참조하세요.

## <a name="download-blobs"></a>Blob 다운로드
toodownload blob을 먼저 blob 참조를 검색 하 고 hello 호출 **DownloadToStream** 메서드. hello 다음 예제에서는 hello **DownloadToStream** 메서드 tootransfer hello blob 내용 tooa stream 개체 다음 tooa 로컬 파일 유지할 수 있습니다.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Hello를 사용할 수도 있습니다 **DownloadToStream** 텍스트 문자열로 blob 내용의 toodownload hello 메서드.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Blob 삭제
toodelete blob blob 참조를 먼저 가져온 고 호출 하 여 **삭제** 메서드.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>여러 페이지에서 비동기식으로 Blob 나열
많은 수의 blob 나열 하거나 하나의 나열 작업에서 반환 하는 결과 toocontrol hello 수, 결과의 페이지 blob을 나열할 수 있습니다. 이 예제에서는 표시 방법을 tooreturn 결과 페이지에서 비동기적으로 하 여 실행 tooreturn 다양 한 결과 기다리는 동안 차단 되지 않습니다.

이 예에서는 플랫 blob을 나열 하지만 hello 설정 하 여 계층적 목록을 수행할 수도 있습니다 **useFlatBlobListing** hello의 매개 변수 **ListBlobsSegmentedAsync** 메서드 너무 **false**합니다.

앞 hello로 해야 hello 예제 메서드는 비동기 메서드를 호출 하기 때문에 **비동기** 키워드 및이 반환 해야 합니다는 **작업** 개체입니다. hello await 키워드 hello에 대 한 지정 **ListBlobsSegmentedAsync** 메서드 hello 목록 작업이 완료 될 때까지 hello 샘플 메서드의 실행을 일시 중단 합니다.

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a>다음 단계
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

