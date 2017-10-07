---
title: "여러 저장소 계정에서 미디어 서비스 자산 aaaManaging | Microsoft Docs"
description: "이 문서는 toomanage 미디어 자산 여러 저장소 계정에서 서비스 하는 방법에 대 한 지침을 제공 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4e4a9ec3-8ddb-4938-aec1-d7172d3db858
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 812f290d91f8d739be1c88db2b612767fda96220
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a>여러 저장소 계정에서 미디어 서비스 자산 관리
Microsoft Azure 미디어 서비스 2.2 부터는 여러 저장소 계정을 tooa 단일 미디어 서비스 계정에 연결할 수 있습니다. 여러 저장소 계정을 미디어 서비스 계정 tooa 다음 hello를 제공 하는 기능 tooattach 이점:

* 자산을 여러 저장소 계정에서 부하 분산합니다.
* 대량의 콘텐츠 처리를 위한 미디어 서비스 크기 조정(현재 단일 저장소 계정의 최대 제한은 500TB). 

이 항목에서 설명 하는 방법을 tooattach 여러 저장소 계정을 사용 하 여 미디어 서비스 계정을 tooa [Azure 리소스 관리자 Api](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](/powershell/module/azurerm.media)합니다. 또한 hello 미디어 서비스 SDK를 사용 하 여 자산을 만들 때 toospecify 다른 저장소 계정을 하는 방법을 보여 줍니다. 

## <a name="considerations"></a>고려 사항
여러 저장소 계정을 미디어 서비스 계정 tooyour를 연결할 때는 hello 다음 고려 사항이 적용 됩니다.

* 모든 저장소 계정은 연결 된 tooa 미디어 서비스 계정에 있어야 합니다. hello hello 미디어 서비스 계정과 동일한 데이터 센터입니다.
* 현재 저장소 계정을 연결 되 면 toohello 미디어 서비스 계정 지정, 분리할 수 없습니다.
* 기본 저장소 계정을 미디어 서비스 계정 만든 시간 동안 표시 된 한 hello입니다. 현재 hello 기본 저장소 계정을 변경할 수 없습니다. 
* 현재 tooadd 쿨 저장소 계정 toohello AMS 계정 하려는 경우 hello 저장소 계정은 Blob 유형 이어야 합니다 toonon 기본 설정.

기타 고려 사항:

미디어 서비스는 hello hello 값 **IAssetFile.Name** 스트리밍 콘텐츠 (예를 들어 http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/ hello에 대 한 Url을 작성할 때 속성 streamingParameters입니다.) 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다. hello hello Name 속성의 값이 하 여야 hello 다음 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다. 또한 ‘.’ 하나만 사용할 수 있습니다. hello 파일 이름 확장명입니다.

## <a name="tooattach-storage-accounts"></a>tooattach 저장소 계정  

tooattach 저장소 계정 tooyour AMS 계정을 사용 하 여 [Azure 리소스 관리자 Api](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](/powershell/module/azurerm.media)hello 다음 예제에에서 나온 것 처럼 합니다.

    $regionName = "West US"
    $subscriptionId = " xxxxxxxx-xxxx-xxxx-xxxx- xxxxxxxxxxxx "
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccount1Name = "skystorage1"
    $storageAccount2Name = "skystorage2"
    $storageAccount1Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount1Name"
    $storageAccount2Id = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccount2Name"
    $storageAccount1 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount1Id -IsPrimary
    $storageAccount2 = New-AzureRmMediaServiceStorageConfig -StorageAccountId $storageAccount2Id
    $storageAccounts = @($storageAccount1, $storageAccount2)
    
    Set-AzureRmMediaService -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccounts $storageAccounts

### <a name="support-for-cool-storage"></a>쿨 저장소 지원

현재 tooadd 쿨 저장소 계정 toohello AMS 계정 하려는 경우 hello 저장소 계정은 Blob 유형 이어야 합니다 toonon 기본 설정.

## <a name="toomanage-media-services-assets-across-multiple-storage-accounts"></a>여러 저장소 계정에서 미디어 서비스 자산 toomanage
코드 다음 hello hello 최신 Media Services SDK tooperform hello 다음 작업을 사용 합니다.

1. 미디어 서비스 계정을 지정 하는 hello와 관련 된 모든 hello 저장소 계정을 표시 합니다.
2. Hello hello 기본 저장소 계정의 이름으로 검색 합니다.
3. Hello 기본 저장소 계정에 새 자산을 만듭니다.
4. Hello 인코딩 출력 자산 만들기 작업 hello에 저장소 계정을 지정 합니다.
   
```
using Microsoft.WindowsAzure.MediaServices.Client;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace MultipleStorageAccounts
{
    class Program
    {
        // Location of hello media file that you want tooencode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Display hello storage accounts associated with 
            // hello specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve hello name of hello default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve hello name of a storage account that is not hello default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create hello original asset in hello default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created hello asset in hello {0} storage account", asset.StorageAccountName);

            // Create an output asset of hello encoding job in hello other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created hello output asset in hello {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in hello default storage account, you can omit hello StorageName parameter.
            var asset = _context.Assets.Create(assetName, storageName, assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);

            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return asset;
        }

        static IAsset CreateEncodingJob(IAsset asset, string storageName, string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My encoding job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error hello event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due toojob error.");
                return null;
            }

            // Get a reference toohello output asset from hello job.
            IAsset outputAsset = job.OutputMediaAssets[0];

            return outputAsset;
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        private static void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
                case JobState.Finished:
                    Console.WriteLine();
                    Console.WriteLine("********************");
                    Console.WriteLine("Job is finished.");
                    Console.WriteLine("Please wait while local tasks or downloads complete...");
                    Console.WriteLine("********************");
                    Console.WriteLine();
                    Console.WriteLine();
                    break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    Console.WriteLine("Please wait...\n");
                    break;
                case JobState.Canceled:
                case JobState.Error:
                    // Cast sender as a job.
                    IJob job = (IJob)sender;
                    // Display or log error details as needed.
                    Console.WriteLine("An error occurred in {0}", job.Id);
                    break;
                default:
                    break;
            }
        }

        static IJob GetJob(string jobId)
        {
            // Use a Linq select query tooget an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return hello job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

