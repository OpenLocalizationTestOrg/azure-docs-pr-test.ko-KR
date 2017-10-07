---
title: ".NET을 사용 하 여 aaaPublish Azure 미디어 서비스 콘텐츠 | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate는 로케이터를 사용 하는 toobuild 스트리밍 URL입니다. 코드 예제는 C#으로 작성 및 hello Media Services SDK for.NET 사용 합니다."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a>.NET을 사용하여 Azure Media Services 콘텐츠 게시
> [!div class="op_single_selector"]
> * [REST (영문)](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [포털](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>개요
적응 비트 전송률 MP4 집합은 주문형 스트리밍 로케이터를 만들고 스트리밍 URL을 작성하여 스트리밍할 수 있습니다. hello [자산 인코딩](media-services-encode-asset.md) 항목을 적응 비트 전송률 MP4 tooencode 설정 하는 방법을 보여 줍니다. 

> [!NOTE]
> 콘텐츠가 암호화되어 있는 경우 [이 항목](media-services-dotnet-configure-asset-delivery-policy.md) 에서 설명하는 대로 자산 배달 정책을 구성한 후에 로케이터를 만듭니다. 
> 
> 

또한 스트리밍 로케이터 toobuild Url 점진적으로 다운로드할 수 있는 지점 tooMP4 파일을 하는 요청 시 사용할 수 있습니다.  

이 항목에서는 방법을 toocreate 자산 및 빌드 부드러운 스트리밍, MPEG DASH 및 HLS 스트리밍 Url locator toopublish 스트리밍는 OnDemand 합니다. 핫 toobuild 점진적 다운로드 Url도 표시 됩니다. 

## <a name="create-an-ondemand-streaming-locator"></a>주문형 스트리밍 로케이터 만들기
toocreate OnDemand 로케이터 스트리밍 hello 및 Url을 가져올 toodo hello 작업을 수행 해야 합니다.

1. Hello 콘텐츠 암호화 되어 있으면 액세스 정책을 정의 합니다.
2. 주문형 스트리밍 로케이터를 만듭니다.
3. Toostream 하려는 경우 스트리밍 매니페스트 파일 (.ism) hello 자산에 hello를 가져옵니다. 
   
   Tooprogressively 다운로드 하려는 경우에 hello 자산에서 MP4 파일의 hello 이름을 가져옵니다.  
4. Url toohello 매니페스트 파일 또는 MP4 파일을 빌드하십시오. 


>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. 동일 사용 하 여 hello 정책 ID를 항상 사용 하는 경우 동일한 hello 일 / 액세스 권한. 예를 들어는 로케이터에 대 한 정책을 위한 tooremain 위치에 오랫동안 (비-업로드 정책). 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

### <a name="use-media-services-net-sdk"></a>Media Services .NET SDK 사용
스트리밍 URL 작성 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

hello를 출력합니다.

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> SSL 연결을 통해 콘텐츠를 스트리밍할 수도 있습니다. toodo 응용 프로그램 수준 보안을 HTTPS로 스트리밍 Url 시작 되었는지 확인 합니다. 현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.
> 
> 

점진적 다운로드 URL 작성 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

hello를 출력합니다.

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Media Services .NET SDK Extensions 사용
hello 다음 코드에서는 호출 로케이터를 만들고 적응 스트리밍에 대 한 hello 부드러운 스트리밍, HLS 및 MPEG-DASH Url을 생성 하는.NET SDK extensions 메서드.

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>다음 단계
* [자산 다운로드](media-services-deliver-asset-download.md)
* [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)

