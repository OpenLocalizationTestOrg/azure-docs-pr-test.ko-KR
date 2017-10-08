---
title: ".NET을 사용 하 여 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "만들고 자산을 업로드 하 여 tooget 미디어를 미디어 서비스 콘텐츠 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a>.NET을 사용하여 Media Services 계정에 파일 업로드
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST (영문)](media-services-rest-upload-files.md)
> * [포털](media-services-portal-upload-files.md)
> 
> 

Media Services에서 자산에 디지털 파일을 업로드(수집)합니다. hello **자산** 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.

hello 자산에 hello 파일 이라고 **자산 파일**합니다. hello **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다. hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.

> [!NOTE]
> hello 고려 사항에 따라 적용 됩니다.
> 
> * 미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다. 값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다. 또한 하나만 있을 수 있습니다 하나 '.' hello 파일 이름 확장명에 대 한 합니다.
> * hello hello 이름 길이 260 자 보다 클 수 없습니다.
> * 미디어 서비스에서 처리에 지원 되는 제한 toohello 최대 파일 크기 있습니다. 참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.
> * 다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.
> 

자산을 만들 때 hello 다음 암호화 옵션을 지정할 수 있습니다. 

* **없음** - 암호화가 사용되지 않습니다. Hello 기본값입니다. 이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.
  Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다. 
* **CommonEncryption** - 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 이미 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.
* **EnvelopeEncrypted** – AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다. 참고 hello 파일을 인코딩된 있는지 및 Transform Manager를 통해 암호화 해야 합니다.
* **StorageEncrypted** -AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 암호화 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다. 자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다. 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.
  
    미디어 서비스는 DRM(Digital Rights Manager)처럼 네트워크상이 아니라 자산에 대해 디스크상의 저장소 암호화 기능을 제공합니다.
  
    자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다. 자세한 내용은 [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)을 참조하세요.

사용 하 여 자산 toobe 암호화에 대해 지정 하는 경우는 **CommonEncrypted** 옵션을 또는 **EnvelopeEncypted** 옵션을 tooassociate 자산 사용 해야 합니다는 **ContentKey**. 자세한 내용은 참조 [어떻게 toocreate ContentKey](media-services-dotnet-create-contentkey.md)합니다. 

사용 하 여 자산 toobe 암호화에 대해 지정 하는 경우는 **StorageEncrypted** 옵션,.NET 만들어집니다에 대 한 미디어 서비스 SDK를 hello는 **StorateEncrypted** **ContentKey** 에 대 한 사용자 자산입니다.

이 항목에서는 toouse 미디어 서비스 하는 방법을 보여 줍니다. 미디어 서비스 자산으로 미디어 서비스.NET SDK extensions tooupload 파일 뿐만 아니라.NET SDK.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>미디어 서비스 .NET SDK를 사용하여 단일 파일 업로드
아래 샘플 코드 hello.NET SDK tooupload 단일 파일을 사용합니다. hello AccessPolicy와 Locator는 생성 되 고 hello 업로드 함수에 의해 삭제 합니다. 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>미디어 서비스 .NET SDK를 사용하여 여러 파일 업로드
코드에서 보여 주는 방법을 다음 hello toocreate 자산 여러 파일을 업로드 하 고 있습니다.

hello 코드는 다음 hello:

* Hello 이전 단계에서 정의 된 hello CreateEmptyAsset 메서드를 사용 하 여 빈 자산을 만듭니다.
* 만듭니다는 **AccessPolicy** hello 권한 및 액세스 toohello 자산의 기간을 정의 하는 인스턴스.
* 만듭니다는 **로케이터** toohello 자산 액세스를 제공 하는 인스턴스.
* **BlobTransferClient** 인스턴스를 만듭니다. 이 형식은 hello Azure blob에 대해 작동 하는 클라이언트를 나타냅니다. 이 예에서는 hello 클라이언트 toomonitor hello 업로드 진행률을 사용 합니다. 
* Hello 지정 된 디렉터리에 파일을 통해 열거 하 고 만듭니다는 **AssetFile** 각 파일에 대 한 인스턴스.
* 업로드 hello를 사용 하 여 미디어 서비스에 파일을 hello **UploadAsync** 메서드. 

> [!NOTE]
> Hello 호출이 차단 되지 않고 및 병렬로 hello 파일을 업로드 하는 hello UploadAsync 메서드 tooensure를 사용 합니다.
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



많은 자산을 업로드 하는 경우에 hello 다음 사항을 고려 합니다.

* 스레드마다 새 **CloudMediaContext** 개체를 만듭니다. hello **CloudMediaContext** 클래스는 스레드로부터 안전 하지 않습니다.
* 5와 2 tooa 더 높은 값의 hello 기본값에서 NumberOfConcurrentTransfers를 늘립니다. 이 자산을 설정하면 **CloudMediaContext**의 모든 인스턴스에 영향을 미칩니다. 
* Hello 기본값 10에 ParallelTransferThreadCount를 보관 합니다.

## <a id="ingest_in_bulk"></a>미디어 서비스 .NET SDK를 사용하여 대량으로 자산 수집
큰 자산 파일을 업로드하면 자산을 만드는 동안 병목 상태가 될 수 있습니다. 대량 또는 "대량 수집"에 자산을 수집, hello 업로드 프로세스에서 자산 만들기를 분리 해야 합니다. 대량 수집 하는 방법 방식을 toouse hello 자산 및 관련된 파일을 설명 하는 매니페스트 (IngestManifest)를 만듭니다. 사용자 선택 tooupload hello 관련된 파일 toohello 매니페스트의 blob 컨테이너의 hello 업로드 메서드를 사용 합니다. Microsoft Azure 미디어 서비스는 hello 매니페스트와 연결 된 hello blob 컨테이너를 감시 합니다. 파일 업로드 toohello blob 컨테이너를 Microsoft Azure 미디어 서비스는 hello 매니페스트에 (IngestManifestAsset) hello 자산의 hello 구성에 따라 hello 자산 만들기를 완료 합니다.

새 IngestManifest toocreate hello IngestManifests 컬렉션 CloudMediaContext hello에 의해 노출 되는 hello Create 메서드를 호출 합니다. 이 방법을 제공 하는 hello 매니페스트 이름의 새 IngestManifest 만들어집니다.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Hello 대량 IngestManifest와 연결 될 hello 자산을 만듭니다. Hello 대량 수집할 자산에서 원하는 hello 암호화 옵션을 구성 합니다.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

IngestManifestAsset는 대량 수집을 위한 대량 IngestManifest와 자산을 연결합니다. 또한 각 자산을 구성할 Assetfile hello를 연결 합니다. IngestManifestAsset toocreate hello 서버 컨텍스트에서 hello Create 메서드를 사용 합니다.

hello 다음 예제에서는 이전에 만든 toohello 대량 hello 두 개의 자산에 연결 하는 추가 두 개의 새 Ingestmanifestasset 수집 매니페스트 각각의 IngestManifestAsset는 대량 수집 중에 각각의 자산에 업로드할 파일 집합도 연결합니다.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Hello 자산 파일 toohello blob 저장소 컨테이너에서 hello 제공 하는 URI를 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다 **IIngestManifest.BlobStorageUriForUpload** hello IngestManifest의 속성입니다. 주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6)입니다. 작성할 수도 있습니다 코드 tooupload hello 자산 파일 hello 다음 코드 예제와 같이 합니다.

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

이 항목에서 사용 하는 hello 샘플에 대 한 hello 자산 파일을 업로드 하기 위한 hello 코드는 다음 코드 예제는 hello에 표시 됩니다.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


연결 된 모든 자산에 대 한 hello 대량 수집의 hello 진행률을 확인할 수 있습니다는 **IngestManifest** hello의 hello 통계 속성을 폴링하여 **IngestManifest**합니다. 주문 tooupdate 진행률 정보를 사용 해야 하는 새 **CloudMediaContext** hello 통계 속성을 폴링할 때마다 합니다.

hello 다음 예제에서는 여는 IngestManifest 폴링 해당 **Id**합니다.

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a>.NET SDK Extensions를 사용하여 파일 업로드
아래 hello 예제는 단일 tooupload 파일.NET SDK Extensions를 사용 하 여 하는 방법을 보여 줍니다. 이 경우 hello **CreateFromFile** 메서드는 사용 되지 않지만 hello 비동기 버전도 있습니다 (**CreateFromFileAsync**). hello **CreateFromFile** 메서드를 사용 하면 hello 파일 이름, 암호화 옵션 및 순서 tooreport hello에서 콜백을 업로드 진행률 hello 파일을 지정할 수 있습니다.

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }

hello 다음 UploadFile 함수를 호출 하 고 저장소 암호화 hello 자산 만들기 옵션으로 지정 합니다.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>다음 단계

이제 업로드된 자산을 인코딩할 수 있습니다. 자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.

또한 Azure 함수 tootrigger hello 구성 컨테이너에 도착 하는 파일을 기반으로 하는 인코딩 작업을 사용할 수 있습니다. 자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.

## <a name="media-services-learning-paths"></a>Media Services 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>다음 단계
자산에 업로드 했으므로 tooMedia 서비스 이동 toohello [어떻게 tooGet 미디어 프로세서] [ How tooGet a Media Processor] 항목입니다.

[How tooGet a Media Processor]: media-services-get-media-processor.md

