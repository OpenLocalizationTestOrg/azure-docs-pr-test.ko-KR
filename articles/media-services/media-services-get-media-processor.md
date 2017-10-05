---
title: "Azure Media Services SDK for .NET을 사용하여 미디어 프로세서를 만드는 방법 | Microsoft 문서"
description: "Azure 미디어 서비스용 미디어 콘텐츠를 인코딩하거나 형식을 변환하거나 암호화하거나 암호 해독하기 위한 미디어 프로세서 구성 요소를 만드는 방법에 대해 알아봅니다. 코드 샘플은 C#으로 작성되었으며 Media Services SDK for .NET을 사용합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="22b65-104">방법: 미디어 프로세서 인스턴스 가져오기</span><span class="sxs-lookup"><span data-stu-id="22b65-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22b65-105">.NET</span><span class="sxs-lookup"><span data-stu-id="22b65-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="22b65-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="22b65-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="22b65-107">개요</span><span class="sxs-lookup"><span data-stu-id="22b65-107">Overview</span></span>
<span data-ttu-id="22b65-108">미디어 서비스에서 미디어 프로세서는 미디어 콘텐츠 인코딩, 형식 변환, 암호화 또는 암호 해독과 같은 특정 처리 작업을 다루는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="22b65-109">일반적으로 미디어 콘텐츠 인코드, 암호화 또는 형식 변환 작업을 만들 때 미디어 프로세서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="22b65-110">Azure 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="22b65-110">Azure media processors</span></span> 

<span data-ttu-id="22b65-111">미디어 프로세스 목록은 다음 항목에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="22b65-112">인코딩 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="22b65-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="22b65-113">분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="22b65-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="22b65-114">미디어 프로세서 가져오기</span><span class="sxs-lookup"><span data-stu-id="22b65-114">Get Media Processor</span></span>

<span data-ttu-id="22b65-115">다음 메서드는 미디어 프로세서 인스턴스를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="22b65-116">이 코드 예제에서는 **_context**라는 모듈 수준 변수를 사용하여 [방법: 프로그래밍 방식으로 Media Services에 연결](media-services-use-aad-auth-to-access-ams-api.md) 섹션에 설명된 대로 서버 컨텍스트를 참조한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="22b65-117">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="22b65-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22b65-118">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="22b65-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="22b65-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22b65-119">Next Steps</span></span>
<span data-ttu-id="22b65-120">미디어 프로세서 인스턴스를 가져오는 방법을 알아보았으므로 이제 Media Encoder Standard를 사용하여 자산을 인코딩하는 방법을 보여 주는 [자산을 인코딩하는 방법](media-services-dotnet-encode-with-media-encoder-standard.md) 토픽으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22b65-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

