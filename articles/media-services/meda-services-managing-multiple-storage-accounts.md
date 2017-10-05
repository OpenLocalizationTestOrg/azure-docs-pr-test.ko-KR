---
title: "여러 저장소 계정에서 Media Services 자산 관리 | Microsoft 문서"
description: "이 문서에서는 여러 저장소 계정에서 미디어 서비스 자산을 관리하는 방법에 대한 지침을 제공합니다."
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
ms.openlocfilehash: 0b407c3b092fd2c706775154cee3164a9869315a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="52fec-103">여러 저장소 계정에서 미디어 서비스 자산 관리</span><span class="sxs-lookup"><span data-stu-id="52fec-103">Managing Media Services Assets across Multiple Storage Accounts</span></span>
<span data-ttu-id="52fec-104">Microsoft Azure 미디어 서비스 2.2부터는 여러 저장소 계정을 단일 미디어 서비스 계정에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-104">Starting with Microsoft Azure Media Services 2.2, you can attach multiple storage accounts to a single Media Services account.</span></span> <span data-ttu-id="52fec-105">여러 저장소 계정을 미디어 서비스 계정에 연결하는 기능은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-105">Ability to attach multiple storage accounts to a Media Services account provides the following benefits:</span></span>

* <span data-ttu-id="52fec-106">자산을 여러 저장소 계정에서 부하 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-106">Load balancing your assets across multiple storage accounts.</span></span>
* <span data-ttu-id="52fec-107">대량의 콘텐츠 처리를 위한 미디어 서비스 크기 조정(현재 단일 저장소 계정의 최대 제한은 500TB).</span><span class="sxs-lookup"><span data-stu-id="52fec-107">Scaling Media Services for large amounts of content processing (as currently a single storage account has a max limit of 500 TB).</span></span> 

<span data-ttu-id="52fec-108">이 항목에서는 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](/powershell/module/azurerm.media)을 사용하여 여러 저장소 계정을 Media Services 계정에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-108">This topic demonstrates how to attach multiple storage accounts to a Media Services account using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media).</span></span> <span data-ttu-id="52fec-109">또한 미디어 서비스 SDK를 사용하여 자산을 만들 때 다른 저장소 계정을 지정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-109">It also shows how to specify different storage accounts when creating assets using the Media Services SDK.</span></span> 

## <a name="considerations"></a><span data-ttu-id="52fec-110">고려 사항</span><span class="sxs-lookup"><span data-stu-id="52fec-110">Considerations</span></span>
<span data-ttu-id="52fec-111">여러 저장소 계정을 미디어 서비스 계정에 연결할 때는 다음과 같은 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-111">When attaching multiple storage accounts to your Media Services account, the following considerations apply:</span></span>

* <span data-ttu-id="52fec-112">미디어 서비스 계정에 연결된 모든 저장소 계정이 미디어 서비스 계정과 동일한 데이터 센터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-112">All storage accounts attached to a Media Services account must be in the same data center as the Media Services account.</span></span>
* <span data-ttu-id="52fec-113">현재는 저장소 계정이 지정된 미디어 서비스 계정에 연결되고 나면 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-113">Currently, once a storage account is attached to the specified Media Services account, it cannot be detached.</span></span>
* <span data-ttu-id="52fec-114">기본 저장소 계정은 미디어 서비스 계정을 만드는 중에 지정된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-114">Primary storage account is the one indicated during Media Services account creation time.</span></span> <span data-ttu-id="52fec-115">현재는 기본 저장소 계정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-115">Currently, you cannot change the default storage account.</span></span> 
* <span data-ttu-id="52fec-116">현재 쿨 저장소 계정을 AMS 계정에 추가하려면 저장소 계정이 Blob 유형이고 주가 아닌 상태로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-116">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

<span data-ttu-id="52fec-117">기타 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="52fec-117">Other considerations:</span></span>

<span data-ttu-id="52fec-118">Media Services는 스트리밍 콘텐츠(예: http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.)를 위해 URL을 작성할 때 **IAssetFile.Name** 속성 값을 사용합니다. 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-118">Media Services uses the value of the **IAssetFile.Name** property when building URLs for the streaming content (for example, http://{WAMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="52fec-119">Name 속성 값에는 !*'();:@&=+$,/?%#[]"와 같은 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-119">The value of the Name property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="52fec-120">또한 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-120">Also, there can only be one ‘.’</span></span> <span data-ttu-id="52fec-121">또한 파일 이름 확장명에는 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-121">for the file name extension.</span></span>

## <a name="to-attach-storage-accounts"></a><span data-ttu-id="52fec-122">저장소 계정을 연결하려면</span><span class="sxs-lookup"><span data-stu-id="52fec-122">To attach storage accounts</span></span>  

<span data-ttu-id="52fec-123">저장소 계정을 AMS 계정에 연결하려면 다음 예제와 같이 [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) 및 [Powershell](/powershell/module/azurerm.media)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-123">To attach storage accounts to your AMS account, use [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](/powershell/module/azurerm.media), as shown in the following example.</span></span>

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

### <a name="support-for-cool-storage"></a><span data-ttu-id="52fec-124">쿨 저장소 지원</span><span class="sxs-lookup"><span data-stu-id="52fec-124">Support for Cool Storage</span></span>

<span data-ttu-id="52fec-125">현재 쿨 저장소 계정을 AMS 계정에 추가하려면 저장소 계정이 Blob 유형이고 주가 아닌 상태로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-125">Currently, if you want to add a Cool Storage account to the AMS account, the storage account must be a Blob type and set to non-primary.</span></span>

## <a name="to-manage-media-services-assets-across-multiple-storage-accounts"></a><span data-ttu-id="52fec-126">여러 저장소 계정에서 미디어 서비스 자산을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="52fec-126">To manage Media Services assets across multiple Storage Accounts</span></span>
<span data-ttu-id="52fec-127">다음 코드에서는 최신 미디어 서비스 SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-127">The following code uses the latest Media Services SDK to perform the following tasks:</span></span>

1. <span data-ttu-id="52fec-128">지정된 미디어 서비스 계정에 연결된 모든 저장소 계정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-128">Display all the storage accounts associated with the specified Media Services account.</span></span>
2. <span data-ttu-id="52fec-129">기본 저장소 계정의 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-129">Retrieve the name of the default storage account.</span></span>
3. <span data-ttu-id="52fec-130">기본 저장소 계정에서 새 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-130">Create a new asset in the default storage account.</span></span>
4. <span data-ttu-id="52fec-131">지정된 저장소 계정에서 인코딩 작업의 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52fec-131">Create an output asset of the encoding job in the specified storage account.</span></span>
   
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
        // Location of the media file that you want to encode. 
        private static readonly string _singleInputFilePath =
            Path.GetFullPath(@"../..\supportFiles\multifile\interview2.wmv");

        // Read values from the App.config file.
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

            // Display the storage accounts associated with 
            // the specified Media Services account:
            foreach (var sa in _context.StorageAccounts)
                Console.WriteLine(sa.Name);

            // Retrieve the name of the default storage account.
            var defaultStorageName = _context.StorageAccounts.Where(s => s.IsDefault == true).FirstOrDefault();
            Console.WriteLine("Name: {0}", defaultStorageName.Name);
            Console.WriteLine("IsDefault: {0}", defaultStorageName.IsDefault);

            // Retrieve the name of a storage account that is not the default one.
            var notDefaultStroageName = _context.StorageAccounts.Where(s => s.IsDefault == false).FirstOrDefault();
            Console.WriteLine("Name: {0}", notDefaultStroageName.Name);
            Console.WriteLine("IsDefault: {0}", notDefaultStroageName.IsDefault);

            // Create the original asset in the default storage account.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.None,
                defaultStorageName.Name, _singleInputFilePath);
            Console.WriteLine("Created the asset in the {0} storage account", asset.StorageAccountName);

            // Create an output asset of the encoding job in the other storage account.
            IAsset outputAsset = CreateEncodingJob(asset, notDefaultStroageName.Name, _singleInputFilePath);
            if (outputAsset != null)
                Console.WriteLine("Created the output asset in the {0} storage account", outputAsset.StorageAccountName);

        }

        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string storageName, string singleFilePath)
        {
            var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();

            // If you are creating an asset in the default storage account, you can omit the StorageName parameter.
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
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My encoding task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.ProtectedConfiguration);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset", storageName,
                AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new
                    EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish. 
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
            progressJobTask.Wait();

            // Get an updated job reference.
            job = GetJob(job.Id);

            // If job state is Error the event handling 
            // method for job progress should log errors.  Here we check 
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
                Console.WriteLine("\nExiting method due to job error.");
                return null;
            }

            // Get a reference to the output asset from the job.
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
            // Use a Linq select query to get an updated 
            // reference by Id. 
            var jobInstance =
                from j in _context.Jobs
                where j.Id == jobId
                select j;
            // Return the job reference as an Ijob. 
            IJob job = jobInstance.FirstOrDefault();

            return job;
        }
    }
}
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="52fec-132">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="52fec-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="52fec-133">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="52fec-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

