---
title: "hello 미디어 서비스 플랫폼에서 분석 aaaMedia | Microsoft Docs"
description: "엔터프라이즈 규모, 규정 준수, 보안 및 전 세계 범위의 음성 및 컴퓨터 비전 서비스 컬렉션인 미디어 분석의 공개 미리 보기"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>미디어 분석 hello 미디어 서비스 플랫폼에서
## <a name="overview"></a>개요
많은 조직에서 사용 하는 비디오 선호 중간 tootrain hello 직원, 자신의 고객 및 비즈니스 기능 문서 의견을 교환 합니다. 클라우드 컴퓨팅 방식으로 toostore 제공 스트림, 및 이러한 큰 미디어 파일에 액세스 합니다. 하지만는 회사의 라이브러리의 비디오 콘텐츠까지 확장 되면서 hello 콘텐츠에서 통찰력을 추출 하는 효과적인 방법을 합니다. 

tooaddress이 증가 요구 Azure 미디어 서비스는 Azure 미디어 분석을 제공합니다. 미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 및 비전 구성 요소 컬렉션입니다. 미디어 분석 hello 핵심 미디어 서비스 플랫폼 구성 요소를 사용 하 여 작성, 하루만에 대규모로 처리 하는 미디어를 처리할 수 있습니다.

개발자는 미디어 분석을 통해 응용 프로그램에 고급 비디오 기능을 신속하게 가져올 수 있습니다. Hello 대형, 규정 준수, 보안, 대규모 조직에 필요한 글로벌 서비스와 엔터프라이즈 환경에 제공 합니다.

hello 다음 보여 주는 다이어그램 미디어 분석 및 hello 미디어 서비스 플랫폼의 다른 주요 부분입니다. 

![VoD 워크플로](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다. MP4 파일을 생성 하는 미디어 프로세서를 점진적으로 hello 파일을 다운로드할 수 있습니다. JSON 파일을 생성 하는 미디어 프로세서 하는 경우에 Azure Blob 저장소에서 hello 파일을 다운로드할 수 있습니다. 

## <a name="media-analytics-services"></a>미디어 분석 서비스

### <a name="indexer"></a>인덱서
Azure Media Indexer를 사용하면 콘텐츠를 검색할 수 있도록 설정하고 선택 캡션 트랙을 생성할 수 있습니다. 비교 toohello 이전 버전에서는 Azure 미디어 인덱서 2 미리 보기에서 인덱싱 빠르고 보다 광범위 한 언어를 지원 합니다. 지원되는 언어는 영어, 스페인어, 프랑스어, 독일어, 이탈리아어, 중국어, 포르투갈어, 아랍어 등입니다. 자세한 내용 및 예제는 [Azure Media Indexer 2를 사용하여 비디오 처리](media-services-process-content-with-indexer2.md)를 참조하세요.
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse 안정화 비디오 및 long 형식의 콘텐츠에서 경과 기능 toocreate 신속 하 고 사용 될 수 있습니다 비디오에 결합합니다. 경과 비디오를 만드는 것 외에도 Hyperlapse toocreate 안정적인 비디오 휴대 전화 및 캠코더를 통해 캡처된 떨림 비디오를 사용할 수 있습니다. 자세한 내용 및 예제는 [Hyperlapse 미디어 파일 및 Azure Media Hyperlapse](media-services-hyperlapse-content.md)를 참조하세요.
### <a name="motion-detector"></a>동작 감지기
고정 배경이 있는 비디오 동작 탐지기 toodetect 동작을 사용할 수 있습니다. 따라서 거짓 긍정에 대 한 가능한 toocheck 동작 이벤트에서 감시 카메라 검색에 있습니다. 자세한 내용 및 예제는 [Azure Media 분석에 대한 동작 감지](media-services-motion-detection.md)를 참조하세요.
### <a name="face-detector"></a>얼굴 감지기
얼굴 감지기를 사용하여 사람들의 얼굴과 행복, 슬픔, 놀라움 등의 감정을 감지할 수 있습니다. 여기에는 이벤트 참여자의 반응을 집계하고 분석하는 등 나중에 설명된 몇 가지 유용한 산업 응용 분야가 있습니다. 자세한 내용 및 예제는 [Azure Media 분석에 대한 얼굴 및 감정 감지](media-services-face-and-emotion-detection.md)를 참조하세요.
### <a name="video-summarization"></a>비디오 요약
비디오 요약을 사용 하면 hello 원본 비디오에서 흥미로운 조각을 자동으로 선택 하 여 긴 비디오의 요약을 만들 수 있습니다. 이 기능은 tooprovide 비디오에서 어떤 tooexpect의 간략 한 개요를 하려는 경우에 유용 합니다. 자세한 내용 및 예제에 대 한 참조 [사용 하 여 Azure 미디어 비디오 축소판 toocreate 비디오 요약](media-services-video-summarization.md)합니다.
### <a name="optical-character-recognition"></a>광학 문자 인식
Azure Media OCR(광학 문자 인식)을 사용하여 비디오 파일의 텍스트 콘텐츠를 편집 및 검색 가능한 디지털 텍스트로 변환할 수 있습니다. 그런 다음 미디어의 hello 비디오 신호에서 의미 있는 메타 데이터 추출 hello를 자동화할 수 있습니다.
### <a name="scalable-face-redaction"></a>확장 가능한 얼굴 편집
Azure 미디어 Redactor hello 클라우드에서 확장 가능한 글꼴 교정 제공 하는 미디어 분석 미디어 프로세서입니다. Face 교정을 사용 하 여 선택한 개인의 비디오 tooblur 면 프로그램을 수정할 수 있습니다. 뉴스 미디어 또는 공공 안전 관련 된 경우 toouse hello 얼굴 교정 서비스를 할 수 있습니다. 몇 분 정도 장면 여러 글꼴로 포함 하 고 표시 되려면 시간 tooredact 수동으로 마이그레이션하지만이 서비스와 얼굴 교정 몇 가지 간단한 단계만 거치면 합니다. 자세한 내용은 참조 hello [Azure 미디어 분석을 면 교정](media-services-face-redaction.md) 문서.

## <a name="common-scenarios"></a>일반적인 시나리오
미디어 분석은 조직 및 기업이 비디오에서 새로운 통찰력을 얻고 대용량의 비디오 콘텐츠를 효율적으로 관리하는 데 도움이 됩니다. 다음은 몇 가지 시나리오입니다.

* **콜 센터** 소셜 미디어, hello 도입 된 경우에 고객의 전화 교환 국 높은 비율의 고객 서비스 트랜잭션이 여전히 용이 하 게 합니다. 이 오디오 데이터 인코딩된 tooachieve 고객 만족도 분석 하는 많은 양의 될 수 있는 고객 정보입니다. 미디어 인덱서를 사용하여 조직은 텍스트를 추출하고 검색 인덱스와 대시보드를 빌드할 수 있습니다. 그런 다음 일반적인 불만, 불만의 원인 및 기타 관련 데이터 인텔리전스를 추출할 수 있습니다.
* **사용자 생성 콘텐츠 조정** 뉴스 미디어 콘센트 toopolice 부서의 많은 조직은 비디오 및 이미지와 같은 미디어 사용자 생성을 허용 하는 공용 웹 포털 있습니다. hello 볼륨이 콘텐츠 toounexpected 이벤트 인해 스파이크 수 있습니다. 이러한 시나리오에서는 것이 어려운 tooconduct 적합성에 대 한 콘텐츠 효과적인 수동 검토 합니다. 해당 되는 콘텐츠에 hello 콘텐츠 중재 서비스 toofocus 고객 사용 수 있습니다.
* **감시** Hello로 사용 하 여 IP 카메라의 증가 거리 내 감시 비디오의 증가 하 고 인벤토리를 제공 됩니다. 거리 내 감시 비디오를 수동으로 검토 하는 시간이 많이 사용 하 고 발생할 가능성이 toohuman 오류입니다. 미디어 분석 동작 감지, 얼굴 감지, 검토, 관리 및 파생 항목을 쉽게 만들 Hyperlapse toomake hello 과정 등과 같은 서비스를 제공 합니다.

## <a name="media-analytics-media-processors"></a>미디어 분석 미디어 프로세서
이 섹션 목록 hello 미디어 분석 미디어 프로세서 및 표시 방법을 toouse.NET 또는 REST tooget 미디어 프로세서 (MP) 개체입니다.

### <a name="mp-names"></a>MP 이름
* Azure 미디어 인덱서 2 미리 보기
* Azure 미디어 인덱서
* Azure 미디어 Hyperlapse
* Azure 미디어 얼굴 탐지기
* Azure 미디어 동작 탐지기
* Azure 미디어 비디오 미리 보기
* Azure 미디어 OCR

### <a name="net"></a>.NET
hello의 함수 하나 하나를 수행 하는 hello MP 이름을 지정 하 고 MP 개체를 반환을 지정 합니다.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST (영문)
요청:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

응답:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>데모
[Azure Media 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)를 참조하세요.

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>관련된 문서
[Media Services 분석 알림](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)을 참조하세요.

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
