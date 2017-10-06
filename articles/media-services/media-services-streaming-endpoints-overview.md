---
title: "aaaAzure 미디어 서비스 스트리밍 끝점 개요 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services 스트리밍 끝점의 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>스트리밍 끝점 개요 

##<a name="overview"></a>개요

Microsoft Azure 미디어 서비스 AMS ()는 **스트리밍 끝점** 직접 tooa 클라이언트 플레이어 응용 프로그램 또는 향후 배포를 위해 네트워크 CDN (콘텐츠 배달) tooa 콘텐츠를 배달할 수 있는 스트리밍 서비스를 나타냅니다. 미디어 서비스는 매끄러운 Azure CDN 통합도 제공합니다. StreamingEndpoint 서비스 hello 아웃 바운드 스트림은 라이브 스트림, 수요 또는 미디어 서비스 계정에 자산 점진적 다운로드 관련 한 비디오 수 있습니다. 각 Azure Media Services 계정에는 기본 StreamingEndpoint 포함됩니다. Hello 계정에서 추가 Streamingendpoint은 만들 수 있습니다. StreamingEndpoints 1.0 및 2.0이라는 두 가지 버전이 있습니다. 2017년 1월 10일부터 새로 만든 AMS 계정은 **기본** StreamingEndpoint 버전 2.0을 포함합니다. 스트리밍 끝점 toothis 계정을 추가 하는 추가 됩니다 버전 2.0. 이 변경은 기존 계정 hello; 영향을 미치지 않습니다. 기존 Streamingendpoint 버전 1.0 및 2.0 업그레이드 tooversion 될 수 있습니다. 이러한 변경으로 인해 동작, 청구 및 기능은 변경 될 (자세한 내용은 참조 hello **스트리밍 유형 및 버전** 아래 섹션에서 설명).

Azure 미디어 서비스 (2017 년 1 월에에서 릴리스됨) hello 2.15 버전 이상 hello toohello 스트리밍 끝점 엔터티 속성을 다음을 추가 하는 또한: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**합니다. 이러한 속성의 자세한 개요는 [여기](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)를 참조하세요. 

Azure 미디어 서비스 계정을 만들 때 표준 스트리밍 끝점은에서 만들어진 hello 기본 **Stopped** 상태입니다. Hello 기본 스트리밍 끝점을 삭제할 수 없습니다. Hello hello 대상 지역에서 Azure CDN 가용성에 따라 새로 만든 기본 기본적으로 스트리밍 끝점도 포함 되어 "StandardVerizon" CDN 공급자 통합 합니다. 

>[!NOTE]
>Azure CDN 통합 hello 스트리밍 끝점을 시작 하기 전에 비활성화할 수 있습니다.

이 항목에서는 스트리밍 끝점에서 제공 하는 hello 주요 기능에 대 한 개요를 제공 합니다.

## <a name="streaming-types-and-versions"></a>스트리밍 형식 및 버전

### <a name="standardpremium-types-version-20"></a>표준/프리미엄 유형(버전 2.0)

두 개의 스트리밍 형식이 있는 경우 릴리스부터 hello 2017 년 1 월 미디어 서비스의: **표준** 및 **프리미엄**합니다. 이러한 유형은 hello 스트리밍 끝점 버전 "2.0"의 일부입니다.

형식|설명
---|---
**Standard**|Hello 대부분의 hello 시나리오에 대 한 hello 기본 옵션입니다.<br/>이 옵션을 고정/제한 SLA를 얻게, 시작한 후 처음 15 일 hello 스트리밍 끝점은 무료입니다.<br/>둘 이상의 스트리밍 끝점을 만들면만 hello 하나는 hello에 대 한 무료 처음 15 일을 시작 하는 즉시 청구 됩니다. 다른 hello 합니다. <br/>Note 무료 평가판 toonewly 미디어 서비스 계정 및 기본 스트리밍 끝점 생성을 적용 됩니다. 기존 스트리밍 끝점 및 또한 생성된 된 스트리밍 끝점 무료 평가판을 포함 하지 않는 기간도는 업그레이드 tooversion 2.0 또는 버전 2.0으로 생성 됩니다.
**Premium**|이 옵션은 큰 규모나 세밀한 컨트롤을 필요로 하는 전문 시나리오에 적합합니다.<br/>구입한 프리미엄 SU(스트리밍 단위) 용량을 기반으로 하는 변수 SLA은 격리된 환경에서 스트리밍 끝점 라이브 전용이며 리소스를 두고 경쟁하지 않습니다.

자세한 내용은 참조 hello **형식 스트리밍을 비교** 다음 단원을 합니다.

### <a name="classic-type-version-10"></a>클래식 유형(버전 1.0)

가 이전 toohello 10 2017 년 1 월 릴리스 AMS 계정을 만든 사용자의 경우는 **클래식** 스트리밍 끝점의 형식입니다. 이 형식은 hello 스트리밍 끝점 버전 "1.0"의 일부에 설명 합니다.

경우에 **버전 "1.0"** 스트리밍 끝점에 > = 1 프리미엄 스트리밍 단위 (SU) 프리미엄 스트리밍 끝점 이며 모든 AMS 기능을 제공 합니다 (hello와 마찬가지로 **표준/프리미엄** 형식) 없이 추가 구성 단계입니다.

>[!NOTE]
>**클래식** 스트리밍 끝점(버전 "1.0" 및 0SU)은 제한된 기능을 제공하고 SLA를 포함하지 않습니다. 좋습니다 toomigrate 너무**표준** 동적 패키징 또는 암호화 및 hello와 함께 제공 되는 다른 기능 등의 더 나은 환경 및 toouse 기능 tooget 입력 **표준** 유형입니다. toomigrate toohello **표준** 입력, toohello 이동 [Azure 포털](https://portal.azure.com/) 선택 **옵트인 tooStandard**합니다. 마이그레이션에 대 한 자세한 내용은 참조 hello [마이그레이션](#migration-between-types) 섹션.
>
>이 작업을 롤백할 수 없고 가격 책정에 미치는 영향이 있음에 주의합니다.
>
 
## <a name="comparing-streaming-types"></a>스트리밍 유형 비교

### <a name="versions"></a>버전

|유형|StreamingEndpointVersion|ScaleUnits|CDN|결제|SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|클래식|1.0|0|해당 없음|무료|해당 없음|
|표준 스트리밍 끝점|2.0|0|예|유료|예|
|프리미엄 스트리밍 단위|1.0|>0|예|유료|예|
|프리미엄 스트리밍 단위|2.0|>0|예|유료|예|

### <a name="features"></a>기능

기능|표준|Premium
---|---|---
처음 15일 무료| 예 |아니요
처리량 |too600 Mbps Azure CDN을 사용 하지 않는 경우. CDN을 사용하여 크기를 조정합니다.|SU(스트리밍 단위)당 200Mbps CDN을 사용하여 크기를 조정합니다.
SLA | 99.9|99.9(SU당 200Mbps)입니다.
CDN|Azure CDN, 타사 CDN 또는 CDN 없음.|Azure CDN, 타사 CDN 또는 CDN 없음.
청구를 계산합니다.| 매일|매일
동적 암호화|예|예
동적 패키징|예|예
확장|자동은 toohello 대상 처리량을 확장할 수 있습니다.|추가 스트리밍 단위
IP 필터링/G20/사용자 지정 호스트|예|예
점진적 다운로드|예|예
권장 사용량 |Hello 포함 된 대부분의 스트리밍 시나리오에 권장 됩니다.|전문 사용량입니다.<br/>필요한 경우 표준 이상이 필요할 수 있습니다. 50,000명의 뷰어보다 많은 동시 대상 그룹이 예상되는 경우 문의하세요(microsoft.com에서 amsstreaming).


## <a name="migration-between-types"></a>유형 간의 마이그레이션

원본 | 너무| 동작
---|---|---
클래식|Standard|Tooopt에 필요
클래식|Premium| 크기 조정(추가 스트리밍 단위)
표준/프리미엄|클래식|사용할 수 없음(스트리밍 끝점 버전이 1.0인 경우 Toochange tooclassic scaleunits 설정을 사용할 수는 너무 "0")
표준(CDN 포함/없이)|프리미엄 hello와 같은 구성|Hello에 허용 **시작** 상태입니다. (Azure Portal을 통해)
프리미엄(CDN 포함/없이)|Hello로 표준 구성이 동일한 여러|Hello에 허용 **시작** (Azure 포털)를 통해 상태
표준(CDN 포함/없이)|다른 구성을 포함한 프리미엄|Hello에 허용 **중지** (Azure 포털)를 통해 상태입니다. Hello 실행 중 상태에에서 사용할 수 없습니다.
프리미엄(CDN 포함/없이)|다른 구성을 포함한 표준|Hello에 허용 **중지** (Azure 포털)를 통해 상태입니다. Hello 실행 중 상태에에서 사용할 수 없습니다.
CDN 포함 SU >= 1인 버전 1.0|CDN 없는 표준/프리미엄|Hello에 허용 **중지** 상태입니다. Hello에 사용할 수 없습니다 **시작** 상태입니다.
CDN 포함 SU >= 1인 버전 1.0|CDN 포함된/없는 표준|Hello에 허용 **중지** 상태입니다. Hello에 사용할 수 없습니다 **시작** 상태입니다. CDN 버전 1.0을 삭제하고 새로 만들어서 시작합니다.
CDN 포함 SU >= 1인 버전 1.0|CDN 포함된/없는 프리미엄|Hello에 허용 **중지** 상태입니다. Hello에 사용할 수 없습니다 **시작** 상태입니다. 클래식 CDN을 삭제하고 새로 만들어서 시작합니다.

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

