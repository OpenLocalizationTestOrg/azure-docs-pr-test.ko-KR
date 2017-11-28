---
title: "aaaDownload 미디어 서비스 자산 tooyour 컴퓨터-Azure | Microsoft Docs"
description: "Toodownload 자산 tooyour 컴퓨터에 알아봅니다. 코드 예제는 C#으로 작성 및 hello Media Services SDK for.NET 사용 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="38209-104">방법: 다운로드를 통해 자산 제공</span><span class="sxs-lookup"><span data-stu-id="38209-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="38209-105">이 항목에서는 tooMedia 서비스 업로드 미디어 자산 제공에 대 한 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="38209-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="38209-106">다양한 응용 프로그램 시나리오에서 미디어 서비스 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38209-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="38209-107">로케이터를 사용하여 미디어 자산을 다운로드하거나 미디어 자산에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38209-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="38209-108">미디어 콘텐츠 tooanother 응용 프로그램이 나 tooanother 콘텐츠 공급자를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38209-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="38209-109">향상된 성능과 확장성을 위해 콘텐츠 배달 네트워크(CDN)를 사용하여 콘텐츠를 배달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38209-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="38209-110">이 예에서는 방법을 미디어 서비스 tooyour 로컬 컴퓨터에서 미디어 자산에 toodownload 합니다.</span><span class="sxs-lookup"><span data-stu-id="38209-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="38209-111">hello 코드 쿼리 hello 작업 ID 및 액세스 하 여 hello 미디어 서비스 계정과 연결 된 작업의 **OutputMediaAssets** 컬렉션 (즉, 작업 실행 으로부터 만들어지는 hello 집합 하나 이상의 출력 미디어 자산을).</span><span class="sxs-lookup"><span data-stu-id="38209-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="38209-112">이 예제는 어떻게 toodownload 출력 미디어 자산, 작업에서 적용할 수 hello 동일한 접근 방식을 toodownload 밖의 자산을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="38209-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="38209-113">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="38209-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="38209-114">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="38209-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="38209-115">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38209-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="38209-116">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="38209-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="38209-117">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="38209-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="38209-118">참고 항목</span><span class="sxs-lookup"><span data-stu-id="38209-118">See Also</span></span>
[<span data-ttu-id="38209-119">스트리밍 콘텐츠 제공</span><span class="sxs-lookup"><span data-stu-id="38209-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

