---
title: "Azure 미디어 서비스 aaaMicrosoft 시나리오 및 사용 가능한 데이터 센터 간에 기능 | Microsoft Docs"
description: "이 항목은 Microsoft Azure Media Services 시나리오 및 데이터 센터에서 기능 및 서비스의 사용 가용성 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a>시나리오 및 데이터 센터에서 Media Services 기능의 사용 가용성

Microsoft Azure 미디어 서비스 AMS ()를 사용 하면 toosecurely 업로드, 저장, 인코딩 및 주문형 및 라이브 스트리밍 배달 toovarious 클라이언트 모두 (예를 들어, TV, PC 및 모바일 장치)에 대 한 비디오 또는 오디오 콘텐츠를 패키지 합니다.

AMS는 hello 전 세계 여러 데이터 센터에서 작동합니다. 이러한 데이터 센터 위치 선택에 유연성을 제공, toogeographic 영역에 그룹화 되어 toobuild 응용 프로그램입니다. Hello를 검토할 수 있습니다 [지역 및 해당 위치의 목록](https://azure.microsoft.com/regions/)합니다. 

이 항목에서는 [라이브](#live_scenarios) 또는 [주문형](#vod_scenarios) 콘텐츠를 배달하는 일반적인 시나리오를 보여줍니다. 또한 hello 항목 데이터 센터 간 미디어 기능 및 서비스의 가용성에 대 한 세부 정보를 제공합니다.

## <a name="overview"></a>개요

### <a name="prerequisites"></a>필수 조건

Azure 미디어 서비스를 사용 하 여 toostart hello 다음 있어야 합니다.

* Azure 계정. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.
* Azure Media Services 계정. 자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.
* 스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 대 한 toobe **실행** 상태입니다.

    AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화를 hello 스트리밍 끝점의 콘텐츠 및 take 있다는 이점이 스트리밍 toostart hello에 대 한 toobe **실행** 상태입니다.

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a>일반적으로 사용 되는 개체 hello AMS OData 모델에 대해 개발할 때

hello 다음 이미지에서는 가장 일반적으로 사용 하는 hello 개체 중 일부를 hello 미디어 서비스 OData 모델에 대해 개발할 때

전체 크기로 hello 이미지 tooview를 클릭 합니다.  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

Hello 전체 모델을 볼 수 있습니다 [여기](https://media.windows.net/API/$metadata?api-version=2.15)합니다.  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a>저장소의 콘텐츠를 보호 하 고 hello에서 스트리밍 미디어 배달 (암호화 되지 않은)의 선택을 취소합니다

![VoD 워크플로](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. 자산에 고품질 미디어 파일을 업로드합니다.

    순서 tooprotect 하는 동안 콘텐츠를 업로드 및 저장소에 저장 된 상태의에서 tooapply 저장소 암호화 옵션 tooyour 자산 것이 좋습니다.
2. Tooa 적응 비트 전송률 MP4 파일 집합을으로 인코딩하십시오.

    Tooapply 저장소 암호화 옵션 toohello 미사용 콘텐츠 순서 tooprotect에 자산을 출력 하는 것이 좋습니다.
3. 자산 배달 정책(동적 패키징에서 사용)을 구성합니다.

    자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 **합니다** .
4. OnDemand 로케이터를 만들어 hello 자산을 게시 합니다.
5. 게시된 콘텐츠를 스트리밍합니다.

데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a>저장소에서 콘텐츠를 보호하고 암호화된 스트리밍 미디어를 동적으로 배달합니다.

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. 자산에 고품질 미디어 파일을 업로드합니다. 저장소 암호화 옵션 toohello 자산을 적용 합니다.
2. Tooa 적응 비트 전송률 MP4 파일 집합을으로 인코딩하십시오. 저장소 암호화 옵션 toohello 출력 자산을 적용 합니다.
3. 동적으로 재생 하는 동안 암호화 toobe 원하는 hello 자산에 대 한 암호화 콘텐츠 키를 만듭니다.
4. 콘텐츠 키 인증 정책을 구성합니다.
5. 자산 배달 정책(동적 패키징 및 동적 암호화에서 사용)을 구성합니다.
6. OnDemand 로케이터를 만들어 hello 자산을 게시 합니다.
7. 게시된 콘텐츠를 스트리밍합니다.

데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a>미디어 분석 tooderive 비디오에서 실행 가능한 통찰력을 사용 하 여

미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 / 비전 구성 요소 컬렉션입니다. 자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.

1. 자산에 고품질 미디어 파일을 업로드합니다.
2. Hello에 설명 된 hello 미디어 분석 서비스 중 하나가 지정 된 비디오 처리 [미디어 분석 개요](media-services-analytics-overview.md) 섹션.
3. 미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다. 미디어 프로세서 MP4 파일을 생성 하는 경우에 hello 파일을 점진적으로 다운로드할 수 있습니다. 미디어 프로세서는 JSON 파일을 생성 하는 경우에 hello Azure blob 저장소에서에서 hello 파일을 다운로드할 수 있습니다.

데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.

## <a name="deliver-progressive-download"></a>점진적 다운로드 제공

1. 자산에 고품질 미디어 파일을 업로드합니다.
2. Tooa 단일 MP4 파일로를 인코딩하십시오.
3. 요청 시 또는 SAS 로케이터를 만들어 hello 자산을 게시 합니다.

    SAS 로케이터를 사용 하 여 hello 콘텐츠 hello Azure blob 저장소에서에서 다운로드 됩니다. 이 경우 toohave 스트리밍 채널 시작 됨된 상태에 필요 하지 않습니다.
4. 콘텐츠를 점진적으로 다운로드합니다.

## <a id="live_scenarios"></a>라이브 스트리밍 이벤트 배달 

1. 다양한 라이브 스트리밍 프로토콜(예: RTMP 또는 부드러운 스트리밍)을 사용하여 라이브 콘텐츠를 수집합니다.
2. (선택 사항)스트림을 적응 비트 전송률 스트림으로 인코딩합니다.
3. 라이브 스트림을 미리 봅니다.
4. 일반 스트리밍 프로토콜 (예: MPEG DASH, 부드러운 스트리밍, HLS)를 통해 hello 콘텐츠 제공 직접 tooyour 고객 또는 향후 배포를 위해 tooa 네트워크 CDN (콘텐츠 배달).

    또는

    순서 toobe의 레코드와 저장소 hello 수집 된 콘텐츠 이상 (주문형 비디오) 스트리밍.

라이브 스트리밍을 수행할 때 라우팅합니다 hello 다음 중 하나를 선택할 수 있습니다.

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>온-프레미스 인코더(통과)에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업

hello 다음 다이어그램에서는 hello와 관련 된 hello AMS 플랫폼의 주요 부분 hello **통과** 워크플로 합니다.

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-current.png)

자세한 내용은 [온-프레미스 인코더의 다중 비트 전송률 라이브 스트림을 수신하는 채널 사용](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>채널을 사용 활성화 tooperform 라이브 Azure 미디어 서비스로 인코딩

hello 다음 그림에 hello를 주요 부분 hello AMS 플랫폼의 라이브 스트리밍 워크플로에 포함 되는 여기서 채널은 라이브 미디어 서비스로 인코딩 tooperform 사용 하도록 설정 합니다.

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-new.png)

자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.

데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.

## <a name="consuming-content"></a>콘텐츠 사용

Azure 미디어 서비스는 hello 도구 toocreate rich 필요 등 대부분의 플랫폼에 대 한 동적 클라이언트 플레이어 응용 프로그램: iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 상자입니다. hello 항목 링크 tooSDKs 및 플레이어 프레임 워크를 사용할 수 있는 toodevelop 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램을 제공 합니다. 자세한 내용은 [비디오 플레이어 응용 프로그램 개발](media-services-develop-video-players.md)을 참조하세요.

## <a name="enabling-azure-cdn"></a>Azure CDN 사용하기

Media Services는 Azure CDN과의 통합을 지원합니다. 방법에 대 한 Azure CDN tooenable 참조 [방법을 미디어 서비스 계정에서 tooManage 스트리밍 끝점](media-services-portal-manage-streaming-endpoints.md)합니다.

## <a id="scaling"></a>Media Services 계정 크기 조정하기

AMS 고객은 해당 AMS 계정에서 스트리밍 끝점, 미디어 처리 및 저장소의 크기를 조정할 수 있습니다.

* Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다. **표준** 스트리밍 끝점은 대부분의 스트리밍 워크로드에 적합합니다. Hello로 동일한 기능을 포함 한 **프리미엄** 끝점 및 배율 아웃 바운드 대역폭을 자동으로 스트리밍. 

    **프리미엄** 스트리밍 끝점은 고급 워크로드에 적합하며, 확장성 있는 전용 대역폭 용량을 제공합니다. **프리미엄** 스트리밍 끝점이 있는 고객은 기본적으로 하나의 SU(스트리밍 단위)를 가져옵니다. SUs를 추가 하 여 hello 스트리밍 끝점을 확장할 수 있습니다. 각 SU 대역폭도 추가로 용량 toohello 응용 프로그램을 제공 합니다. 확장에 대 한 자세한 내용은 **프리미엄** hello 참조 스트리밍 끝점을 [스트리밍 끝점 확장](media-services-portal-scale-streaming-endpoints.md) 항목입니다.

* 미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약 된 단위 유형과 연관 되어 있습니다. Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다. Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다.

    또한 toospecifying hello 예약 단위 형식, tooprovision를 사용 하 여 계정을 지정할 수 있습니다 **예약 단위** (RUs). 프로 비전 된 RUs hello 수 hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.

    >[!NOTE]
    >RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다. 그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.

    자세한 내용은 [미디어 처리 크기 조정](media-services-portal-scale-media-processing.md)을 참조하세요.
* 또한 저장소 계정 tooit를 추가 하 여 미디어 서비스 계정에 확장할 수 있습니다. 각 저장소 계정은 제한 된 too500 TB입니다. tooexpand hello 기본 제한 보다 크게 저장소를 선택할 수 있습니다 tooattach 여러 저장소 계정을 tooa 단일 미디어 서비스 계정입니다. 자세한 내용은 [저장소 계정 관리](meda-services-managing-multiple-storage-accounts.md)를 참조하세요.

##<a id="availability"></a>데이터 센터에서 Media Services 기능의 사용 가용성

이 섹션에서는 데이터 센터에서 Media Services 기능 의 사용 가용성에 대한 세부 정보를 제공합니다.

### <a name="ams-accounts"></a>AMS 계정

#### <a name="availability"></a>Availability

Hello 다음 지역에서에서 미디어 서비스 계정을 만들 수 있습니다: 북유럽, 서유럽, 미국 서 부, 미국 동부, 동남 아시아, 아시아 동부, 일본 서 부, 일본 동쪽, 브라질 남쪽, 인도 서 부, 인도 남부 및 중앙 인도 있습니다. 

### <a name="streaming-endpoints"></a>스트리밍 끝점 

Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다. 자세한 내용은 참조 hello [배율](#scaling) 섹션.

#### <a name="availability"></a>Availability

|이름|가동 상태|데이터 센터
|---|---|---|
|Standard|GA|모두|
|Premium|GA|모두|

### <a name="live-encoding"></a>라이브 인코딩

#### <a name="availability"></a>Availability

독일, 브라질 남부, 인도 서부, 인도 남부 및 인도 중부를 제외한 모든 데이터 센터에서 사용할 수 있습니다. 

### <a name="encoding-media-processors"></a>미디어 프로세서 인코딩

AMS에서는 두 가지 주문형 인코더인 **Media Encoder Standard** 및 **Media Encoder Premium 워크플로**를 제공합니다. 자세한 내용은 [Azure 주문형 미디어 인코더의 개요 및 비교](media-services-encode-asset.md)를 참조하세요. 

#### <a name="availability"></a>Availability

|미디어 프로세서 이름|가동 상태|데이터 센터
|---|---|---|
|미디어 인코더 표준|GA|모두|
|미디어 인코더 Premium 워크플로|GA|중국을 제외한 모든 지역|

### <a name="analytics-media-processors"></a>분석 미디어 프로세서

미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 및 비전 구성 요소 컬렉션입니다. 자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.

#### <a name="availability"></a>Availability

|미디어 프로세서 이름|가동 상태|데이터 센터
|---|---|---|
|Azure 미디어 얼굴 탐지기|미리 보기|모두|
|Azure 미디어 Hyperlapse|미리 보기|모두|
|Azure Media Indexer|GA|모두|
|Azure 미디어 동작 탐지기|미리 보기|모두|
|Azure 미디어 OCR|미리 보기|모두|
|Azure Media Redactor|미리 보기|모두|
|Azure Media Stabilizer|미리 보기|모두|
|Azure 미디어 비디오 미리 보기|미리 보기|모두|
|Azure Media Indexer 2|미리 보기|중국 및 연방 정부 지역을 제외한 모든 지역|

### <a name="protection"></a>보호

Microsoft Azure 미디어 서비스 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간을 수 있습니다. 자세한 내용은 [AMS 콘텐츠 보호](media-services-content-protection-overview.md)를 참조하세요.

#### <a name="availability"></a>Availability

|암호화|가동 상태|데이터 센터|
|---|---|---| 
|저장소|GA|모두|
|AES-128 키|GA|모두|
|Fairplay|GA|모두|
|PlayReady|GA|모두|
|Widevine|GA|독일, 연방 정부 및 중국을 제외한 모든 지역

### <a name="reserved-units-rus"></a>RU(예약 단위)

제공된 된 예약된 단위 수가 hello hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다. 

자세한 내용은 참조 hello [배율](#scaling) 섹션.

#### <a name="availability"></a>Availability

모든 데이터 센터에서 사용할 수 있습니다.

### <a name="reserved-unit-ru-type"></a>RU(예약 단위) 형식

미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약된 단위 형식과 연결 됩니다. Hello 다음 중에서 선택할 수 예약 단위 형식: S1, S2 또는 s 3입니다.

자세한 내용은 참조 hello [배율](#scaling) 섹션.

#### <a name="availability"></a>Availability

|RU 형식 이름|가동 상태|데이터 센터
|---|---|---|
|S1|GA|모두|
|S2|GA|브라질 남부 및 인도 서부를 제외한 모든 지역|
|S3|GA|인도 서부를 제외한 모든 지역|

## <a name="next-steps"></a>다음 단계

Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

