---
title: "Azure 미디어 서비스.NET SDK를 사용 하 여 aaaCreating 필터"
description: "이 항목에서는 클라이언트 toostream 스트림의 특정 섹션 사용할 수 있도록 toocreate 필터링 하는 방법을 설명 합니다. 미디어 서비스 스트리밍이 선택적 tooachieve를 동적 매니페스트를 만듭니다."
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
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Azure 미디어 서비스 .NET SDK로 필터 생성
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST (영문)](media-services-rest-dynamic-manifest.md)
> 
> 

2.11 버전부터 미디어 서비스를 사용 하면 자산에 대 한 toodefine 필터. 이러한 필터는 고객에 게 toochoose toodo 등으로 나눌 수 있는 서버 쪽 규칙: 재생 (재생 하지 않고 hello 전체 비디오), 비디오의 섹션만 고객의 장치 (처리할 수 있도록 하는 오디오 및 비디오 변환의 하위 집합을 지정 하거나 모든 hello 변환 하는 대신 연결 된 hello 자산에). 이 자산의 필터링을 통해 얻습니다 **동적 매니페스트**비디오 고객의 요청 toostream 시 생성 되는 지정 된 필터를 기반 합니다.

자세한 내용을 보려면 관련된 toofilters 및 동적 매니페스트 참조 [동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)합니다.

이 항목에서는 toouse 미디어 서비스.NET SDK toocreate이, 업데이트 하 고 필터를 삭제 하는 방법을 보여 줍니다. 

필터를 업데이트 하는 경우 스트리밍 끝점 toorefresh hello 규칙에 대 일 분까지 걸릴 수 있으므로 note 합니다. Hello 콘텐츠가이 필터를 사용 하 여 제공 된 (그리고 캐시 프록시 및 CDN에 캐시 된) 하는 경우 플레이어에서 오류가 발생할 수 있습니다이 필터를 업데이트 합니다. 되기 tooclear hello 캐시 hello 필터를 업데이트 한 후 것이 좋습니다. 이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다. 

## <a name="types-used-toocreate-filters"></a>Toocreate 필터를 사용 하는 형식
hello 다음 유형은 사용할 필터를 만들 때. 

* **IStreamingFilter**.  이 형식은 다음 REST API hello 기반 [필터](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. 이 형식은 다음 REST API hello 기반 [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. 이 형식은 다음 REST API hello 기반 [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** 및 **IFilterTrackPropertyCondition**. 이러한 형식은 다음 REST Api hello 기반 [FilterTrackSelect 및 FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>전역 필터 생성/업데이트/읽기/삭제
hello 다음 코드에서는 toouse.NET toocreate를 업데이트, 읽기 및 자산 필터 삭제 방법

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


## <a name="createupdatereaddelete-asset-filters"></a>자산 필터 생성/업데이트/읽기/삭제
hello 다음 코드에서는 toouse.NET toocreate를 업데이트, 읽기 및 자산 필터 삭제 방법

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




## <a name="build-streaming-urls-that-use-filters"></a>필터를 사용하는 스트리밍 URL 작성
Toopublish 및 배달 자산을 확인 하려면 어떻게 해야에 대 한 내용은 [콘텐츠 배달 tooCustomers 개요](media-services-deliver-content-overview.md)합니다.

hello 다음 예제에서는 tooadd tooyour 스트리밍 Url을 필터링 하는 방법

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HLS(HTTP 라이브 스트리밍) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HLS(HTTP 라이브 스트리밍) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**부드러운 스트리밍**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)

