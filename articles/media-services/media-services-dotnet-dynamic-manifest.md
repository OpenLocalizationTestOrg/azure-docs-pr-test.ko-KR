---
title: "Azure 미디어 서비스 .NET SDK로 필터 생성"
description: "이 항목에서는 클라이언트가 스트림의 특정 섹션을 스트리밍하는 데 사용할 수 있는 필터를 생성하는 방법을 설명합니다. 이 선택적 스트리밍은 미디어 서비스가 동적 매니페스트를 생성하여 이루어집니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="01d51-104">Azure 미디어 서비스 .NET SDK로 필터 생성</span><span class="sxs-lookup"><span data-stu-id="01d51-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01d51-105">.NET</span><span class="sxs-lookup"><span data-stu-id="01d51-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="01d51-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="01d51-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="01d51-107">미디어 서비스 2.11 버전부터 자산에 대한 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="01d51-108">이 필터는 고객이 전체 비디오를 재생하는 대신 비디오의 한 섹션만 재생하거나 자산과 연결된 모든 변환 대신 고객의 장치가 처리할 수 있는 오디오 및 비디오 변환의 하위 집합만 지정하는 등을 선택할 수 있도록 하는 서버 측 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="01d51-109">지정한 필터에 따라 비디오를 스트림하는 고객의 요청에 따라 생성된 **동적 매니페스트**를 통해 자산의 필터링이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="01d51-110">필터 및 동적 매니페스트에 대한 더 자세한 내용은 [동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="01d51-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="01d51-111">이 항목에서는 미디어 서비스 .NET SDK를 사용하여 필더를 생성하고, 업데이트하며, 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="01d51-112">필터를 업데이트하는 경우, 규칙을 새로 고치는 스트리밍 끝점에 최대 2분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="01d51-113">콘텐츠가 이 필터로 처리된 경우(및 프록시와 CDN 캐시에서 캐시된 경우) 이 필터를 업데이트하면 플레이어 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="01d51-114">필터 업데이트 후에는 캐시를 지우는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="01d51-115">이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="01d51-116">필터 생성에 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="01d51-116">Types used to create filters</span></span>
<span data-ttu-id="01d51-117">필터를 생성할 때는 다음 형식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="01d51-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="01d51-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="01d51-119">이 형식은 다음 REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="01d51-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="01d51-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="01d51-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="01d51-121">이 형식은 다음 REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="01d51-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="01d51-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="01d51-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="01d51-123">이 형식은 다음 REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="01d51-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="01d51-124">**FilterTrackSelectStatement** 및 **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="01d51-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="01d51-125">이 형식은 다음 REST API [FilterTrackSelect 및 FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="01d51-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="01d51-126">전역 필터 생성/업데이트/읽기/삭제</span><span class="sxs-lookup"><span data-stu-id="01d51-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="01d51-127">다음 코드에서는 .NET을 사용하여 자산 필더를 생성, 업데이트, 읽기 및 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="01d51-128">자산 필터 생성/업데이트/읽기/삭제</span><span class="sxs-lookup"><span data-stu-id="01d51-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="01d51-129">다음 코드에서는 .NET을 사용하여 자산 필더를 생성, 업데이트, 읽기 및 삭제하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="01d51-130">필터를 사용하는 스트리밍 URL 작성</span><span class="sxs-lookup"><span data-stu-id="01d51-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="01d51-131">자산을 게시하고 제공하는 방법에 대한 자세한 내용은 [고객에 콘텐츠 배달 개요](media-services-deliver-content-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="01d51-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="01d51-132">다음 예제에서는 스트리밍 URL에 필터를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="01d51-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="01d51-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="01d51-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="01d51-134">**Apple HLS(HTTP 라이브 스트리밍) V4**</span><span class="sxs-lookup"><span data-stu-id="01d51-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="01d51-135">**Apple HLS(HTTP 라이브 스트리밍) V3**</span><span class="sxs-lookup"><span data-stu-id="01d51-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="01d51-136">**부드러운 스트리밍**</span><span class="sxs-lookup"><span data-stu-id="01d51-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="01d51-137">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="01d51-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01d51-138">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="01d51-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="01d51-139">참고 항목</span><span class="sxs-lookup"><span data-stu-id="01d51-139">See Also</span></span>
[<span data-ttu-id="01d51-140">동적 매니페스트 개요</span><span class="sxs-lookup"><span data-stu-id="01d51-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

