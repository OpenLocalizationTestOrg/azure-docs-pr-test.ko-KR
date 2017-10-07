---
title: "aaaScaling 미디어 처리 개요 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services를 사용하여 미디어 처리의 크기를 조정하는 방법을 대략적으로 설명합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>미디어 처리 크기 조정 개요
이 페이지에서는 방법과 그 이유에 대 한 개요를 제공 tooscale 미디어 처리 합니다. 

## <a name="overview"></a>개요
미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약 된 단위 유형과 연관 되어 있습니다. Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다. Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다. 자세한 내용은 참조 hello [예약 단위 형식](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/)합니다.

또한 toospecifying hello 예약 단위 형식, 예약 단위 tooprovision 계정을 지정할 수 있습니다. 제공된 된 예약된 단위 수가 hello hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다. 예를 들어 5 개의 미디어 작업이 동시에 실행 될 다음 사용자 계정에 5 명의 예약된 단위 같이 많은 경우 작업 toobe 처리 합니다. hello 남은 작업이 hello 큐에서 대기 하 고 실행 중인 작업이 완료 되는 경우 순차적으로 처리 하도록 선택 됩니다. 계정에 프로비전된 예약 단위가 없는 경우에는 작업이 순차적으로 선택됩니다. 이 경우 hello 한 작업 완료 사이의 시간 기다렸다가 hello 다음 시작에 따라 달라 집니다 리소스의 hello 가용성 hello 시스템.

## <a name="choosing-between-different-reserved-unit-types"></a>여러 예약 단위 유형 중에서 선택
다음 표는 hello를 사용 하면 다양 한 인코딩 속도 선택할 때 결정을 내릴 수 있습니다. 또한 몇 가지 벤치 마크 사례를 제공 하 고 SAS Url을 수행할 수 toodownload 비디오를 사용할 수 있는 사용자가 직접 제공 합니다.

| 시나리오 | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| 대상 사용 사례 |단일 비트 전송률 인코딩 <br/>SD 이하 해상도의 파일, 시간이 중요하지 않은 인코딩, 저가형 비디오. |단일 비트 전송률 및 다중 비트 전송률 인코딩.<br/>SD 및 HD 인코딩에서 모두 일반적으로 사용됨 |단일 비트 전송률 및 다중 비트 전송률 인코딩.<br/>Full HD 및 4K 해상도 비디오. 시간이 중요하며 소요 시간이 짧은 인코딩 |
| 벤치마크 |[입력 파일: 길이 5분/640x360p/초당 29.97프레임](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Tooa 단일 비트 전송률 MP4 파일 인코딩 hello 같은 해상도 약 11 분입니다. |[입력 파일: 길이 5분/1280x720p/초당 29.97프레임](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>"H264 단일 비트 전송률 720p" 사전 설정을 사용하여 인코딩할 때 약 5분이 걸립니다.<br/><br/>"H264 다중 비트 전송률 720p" 사전 설정을 사용하여 인코딩할 때 약 11분 30초가 걸립니다. |[입력 파일: 길이 5분/1920x1080p/초당 29.97프레임](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>"H264 단일 비트 전송률 1080p" 사전 설정을 사용하여 인코딩할 때 약 2.7분이 걸립니다.<br/><br/>"H264 단일 비트 전송률 1080p" 사전 설정을 사용하여 인코딩할 때 약 5.7분이 걸립니다. |

## <a name="considerations"></a>고려 사항
> [!IMPORTANT]
> 이 섹션에서 설명하는 고려 사항을 검토하세요.  
> 
> 

* 예약된 단위는 Azure 미디어 인덱서를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다.  그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.
* 인코딩 작업에서 한 다음 공유 hello를 사용 하는 경우 풀, 즉, 없이 예약 단위를 동일한 성능 S1 RUs와 마찬가지로 hello 합니다. 그러나 작업 큐에 대기 중인된 상태에서 소비할 수 상한을 toohello 시간이 없습니다 및 지정된 된 시간에 최대 하나의 작업 실행 됩니다.
* 데이터 센터를 수행 하는 hello hello를 제공 하지 않는 **S2** 예약 단위 형식: 브라질 남쪽 및 인도 서 부 합니다.
* hello 다음과 같은 데이터 센터 제공 하지 않으므로 hello **S3** 예약 단위 형식: 인도 서 부 합니다.

## <a name="billing"></a>결제

미디어 예약 단위의 실제 사용 시간(분)을 기준으로 요금이 청구됩니다. 에 대 한 자세한 설명은 hello의 hello FAQ 섹션을 참조 [미디어 서비스 가격](https://azure.microsoft.com/pricing/details/media-services/) 페이지.   

## <a name="quotas-and-limitations"></a>할당량 및 제한 사항
할당량 및 제한 사항에 대 한 내용은 tooopen 지원 티켓을 확인 하는 방법 및 [할당량 및 제한](media-services-quotas-and-limitations.md)합니다.

## <a name="next-step"></a>다음 단계
Hello 이러한 기술 중 하나, 작업을 처리 하는 미디어 확장을 수행 합니다. 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [포털](media-services-portal-scale-media-processing.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

