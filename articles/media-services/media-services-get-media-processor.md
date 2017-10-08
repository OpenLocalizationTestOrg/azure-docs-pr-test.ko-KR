---
title: "사용 하 여 미디어 프로세서 aaaHow tooCreate는 Azure Media Services SDK for.NET hello | Microsoft Docs"
description: "미디어 프로세서 구성 요소 tooencode toocreate를 형식으로 변환, 암호화 또는 Azure 미디어 서비스에 대 한 미디어 콘텐츠를 암호 해독 방법에 대해 알아봅니다. 코드 예제는 C#으로 작성 및 hello Media Services SDK for.NET 사용 합니다."
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
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>방법: 미디어 프로세서 인스턴스 가져오기
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST (영문)](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>개요
미디어 서비스에서 미디어 프로세서는 미디어 콘텐츠 인코딩, 형식 변환, 암호화 또는 암호 해독과 같은 특정 처리 작업을 다루는 구성 요소입니다. 일반적으로 미디어 프로세서 작업 tooencode를 만들 때, encrypt, 만들거나 미디어 콘텐츠 hello 형식으로 변환 합니다.

## <a name="azure-media-processors"></a>Azure 미디어 프로세서 

hello 항목에서는 미디어 프로세서의 목록을 제공 합니다.

* [인코딩 미디어 프로세서](scenarios-and-availability.md#encoding-media-processors)
* [분석 미디어 프로세서](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>미디어 프로세서 가져오기

메서드를 보여 줍니다 방법을 따르는 hello tooget 미디어 프로세서 인스턴스. hello 코드 예제에서는 라는 모듈 수준 변수를 사용 하 여 hello 가정 **컨텍스트** tooreference hello 서버 컨텍스트 hello 섹션에 설명 된 대로 [하는 방법: tooMedia 프로그래밍 방식으로 서비스 연결](media-services-use-aad-auth-to-access-ams-api.md)합니다.

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>다음 단계
배웠으므로 tooget 미디어 프로세서 인스턴스를 이동 하는 방법을 toohello [어떻게 tooEncode 자산](media-services-dotnet-encode-with-media-encoder-standard.md) 항목 어떻게 toouse hello 미디어 인코더 표준 tooencode 자산을 볼 수 있습니다.

