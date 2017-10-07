---
title: "Azure 미디어 서비스를 사용 하 여 라이브 스트리밍의 aaaOverview | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스를 사용하는 라이브 스트리밍 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Azure 미디어 서비스를 사용하는 라이브 스트리밍 개요
## <a name="overview"></a>개요
실시간 배달할 때 Azure 미디어 서비스와 함께 이벤트 스트리밍 hello 다음과 같은 구성 요소가 일반적으로 다음과 같습니다.

* 카메라 사용된 toobroadcast 이벤트는입니다.
* hello 카메라 toostreams tooa 보낸 신호 변환 하는 라이브 비디오 인코더 라이브 스트리밍 서비스입니다.

    필요에 따라 여러 라이브 시간에 동기화된 인코더. 중요 한 라이브 요청 매우 높은 가용성 및 환경의 품질 것이 좋다는 시간 동기화 tooachieve 데이터 손실 없이 원활한 장애 tooemploy 활성-활성 중복 인코더 이벤트입니다.
* 다음 toodo hello 수 있도록 하는 라이브 스트리밍 서비스로:

  * 다양한 라이브 스트리밍 프로토콜(예: RTMP 또는 부드러운 스트리밍)을 사용하여 라이브 콘텐츠 수집
  * (선택 사항) 스트림을 적응 비트 전송률 스트림으로 인코딩
  * 라이브 스트림 미리 보기
  * 순서 toobe의 레코드와 저장소 hello 수집 된 콘텐츠 이상 (주문형 비디오) 스트리밍
  * 일반 스트리밍 프로토콜 (예: MPEG DASH, 부드러운 스트리밍, HLS)를 통해 hello 콘텐츠 제공 직접 tooyour 고객 또는 향후 배포를 위해 tooa 네트워크 CDN (콘텐츠 배달).

**Microsoft Azure 미디어 서비스** 기능 tooingest hello, 인코딩, 미리 보기, 저장 및 라이브 스트리밍 콘텐츠를 배달 AMS ()를 제공 합니다.

프로그램 콘텐츠 toocustomers 목표 배달할 때 toodeliver 다양 한 네트워크 조건에서 고품질의 비디오 toovarious 장치입니다. tooachieve이를 사용 하 여 라이브 인코더 tooencode 스트림 tooa 비디오 스트림을 다중 비트 전송률 (적응 비트 전송률).  미디어 서비스를 사용 하는 서로 다른 장치에서 스트리밍 care of tootake [동적 패키징](media-services-dynamic-packaging-overview.md) toodynamically 스트림 toodifferent 프로토콜을 다시 패키지입니다. 미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술 뒤의 배달을 지원: HLS HTTP 라이브 스트리밍 (), 부드러운 스트리밍, MPEG DASH 합니다.

Azure 미디어 서비스에서 **채널**, **프로그램**, 및 **Streamingendpoint** 모든 hello 라이브 수집, 형식 지정, DVR를 포함 한 기능을 스트리밍 핸들 보안, 확장성 및 중복 됩니다.

**채널** 은 라이브 스트리밍 콘텐츠를 처리하기 위한 파이프라인을 나타냅니다. 채널을 라이브 받을 수 있는 방법으로 다음 hello의 스트림 입력:

* 온-프레미스 라이브 인코더가 다중 비트 전송률 보냅니다 **RTMP** 또는 **부드러운 스트리밍** (조각난 MP4)에 대해 구성 된 toohello 채널 **통과** 배달 합니다. hello **통과** 배달이 hello 수집 된 스트림을 통과할 때 **채널**추가 처리 없이 s입니다. Hello 다음 다중 비트 전송률 부드러운 스트리밍 출력 하는 라이브 인코더를 사용할 수 있습니다: MediaExcel, Ateme, 통신 한다고 가정, Envivio, Cisco 및 Elemental 합니다. hello 라이브 인코더 출력: Adobe Flash 미디어 라이브 인코더 (FMLE), Telestream Wirecast, Haivision, Teradek tricaster 트랜스코더 등이 있습니다.  라이브 인코더에서 라이브 인코딩의 해제 되어 있지만 권장 되지 않습니다는 단일 비트 전송률 스트림을 tooa 채널을 보낼 수도 있습니다. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.

  > [!NOTE]
  > 통과 메서드를 사용 하 여 방법은 hello 가장 경제적 toodo 라이브 스트리밍는 오랜 기간 동안 여러 이벤트를 수행 하는 경우 온-프레미스 인코더에 투자 이미 있습니다. [가격 책정](https://azure.microsoft.com/pricing/details/media-services/) 세부 정보를 참조하세요.
  > 
  > 
* 온-프레미스 라이브 인코더 toohello 채널을 사용 하도록 설정된 tooperform 라이브 hello 다음 형식 중 하나에 미디어 서비스로 인코딩 단일 비트 전송률 스트림을 보냅니다: RTMP 또는 부드러운 스트리밍 (조각난된 MP4). 전용된 연결이 toohello Azure 데이터 센터에 있는 경우 RTP (MPEG-TS)도 지원 됩니다. RTMP와 라이브 인코더 뒤 hello 출력 채널의이 유형의 toowork 알려진: Telestream Wirecast, FMLE 합니다. hello 채널 다음 라이브 인코딩합니다 hello 들어오는 단일 비트 전송률 스트림 tooa 다중 비트 전송률 (적응) 비디오 스트림으로 합니다. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.

부터는 hello 미디어 서비스 2.10 릴리스부터 채널을 만들 때 어떤 방식으로 채널 tooreceive hello 입력된 스트림 및 채널 tooperform hello에 대 한 원하는 여부에 대해 원하는 श 스트림 인코딩을 지정할 수 있습니다. 다음 두 가지 옵션을 사용할 수 있습니다.

* **None** (통과) – toouse (통과 스트림) 다중 비트 전송률 스트림을 출력 하는 온-프레미스 라이브 인코더를 계획 하는 경우이 값을 지정 합니다. 이 경우 hello 들어오는 스트림은 인코딩되지 않고 출력 toohello 통과 합니다. 이것이 채널 이전 too2.10 릴리스의 hello 동작입니다.  
* **표준** –이 값을 선택, toouse 미디어 서비스 tooencode 하려는 경우 단일 비트 전송률 라이브 스트림을 toomulti 비트 전송률 스트림을 합니다. 이 방법은 자주 수행하지 않는 이벤트를 신속하게 강화하는 데 더욱 경제적입니다. 업그레이드할 청구 영향을 줄 정도로 라이브 인코딩의 라이브 인코딩 채널 hello "실행 중" 상태로 남게 됩니다 인해 발생 하는 요금 청구 점을 기억해 야 합니다.  라이브 스트리밍 이벤트 후 실행 중인 채널을 즉시 중지 하는 것이 좋습니다 완료 tooavoid extra 시간별 요금 됩니다.

## <a name="comparison-of-channel-types"></a>채널 형식 비교
다음 표에서 toocomparing hello 두 채널 형식을 미디어 서비스에서 지원 되는 지침 제공

| 기능 | 통과 채널 | 표준 채널 |
| --- | --- | --- |
| 단일 비트 전송률 입력 hello 클라우드에서 여러 비트 전송률으로 인코딩되어 |아니요 |예 |
| 최대 해상도, 계층 수 |1080p, 8계층, 60+fps |720p, 6계층, 30fps |
| 입력 프로토콜 |RTMP, 부드러운 스트리밍 |RTMP, 부드러운 스트리밍, RTP |
| 가격 |Hello 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/media-services/) "라이브 비디오" 탭을 클릭 |Hello 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/media-services/) |
| 최대 실행 시간 |연중 무휴 |8시간 |
| 슬레이트 삽입 지원 |아니요 |예 |
| 광고 신호 지원 |아니요 |예 |
| 통과 CEA 608/708 캡션 |예 |예 |
| 기여에 대 한 간략 한 대기에서 기능 toorecover 피드 |예 |아니요(채널은 입력 데이터가 6초 이상 없으면 슬레이팅을 시작함) |
| 균일하지 않은 입력 GOP에 대한 지원 |예 |아니요 - 입력은 고정된 2초 GOP여야 함 |
| 변수 프레임 속도 입력에 대한 지원 |예 |아니요 - 입력은 고정된 프레임 속도여야 함.<br/>예를 들어 움직임이 많은 장면 중에는 사소한 차이가 허용됩니다. 하지만 인코더 too10 프레임/sec를 삭제할 수 없습니다. |
| 입력 피드가 손실될 경우 채널 자동 차단 |아니요 |12시간 동안 프로그램 실행이 없는 경우 |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>온-프레미스 인코더(통과)에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업
hello 다음 다이어그램에서는 hello와 관련 된 hello AMS 플랫폼의 주요 부분 hello **통과** 워크플로 합니다.

![라이브 워크플로](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

자세한 내용은 [온-프레미스 인코더의 다중 비트 전송률 라이브 스트림을 수신하는 채널 사용](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>채널을 사용 활성화 tooperform 라이브 Azure 미디어 서비스로 인코딩
hello 다음 그림에 hello를 주요 부분 hello AMS 플랫폼의 라이브 스트리밍 워크플로에 포함 되는 여기서 채널은 라이브 미디어 서비스로 인코딩 tooperform 사용 하도록 설정 합니다.

![라이브 워크플로](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.

## <a name="description-of-a-channel-and-its-related-components"></a>채널 및 관련 구성 요소에 대한 설명
### <a name="channel"></a>채널
미디어 서비스에서, [채널](https://docs.microsoft.com/rest/api/media/operations/channel)은 라이브 스트리밍 콘텐츠 처리를 담당합니다. Channel에서 제공 하는 입력된 끝점 (수집 URL) tooa 라이브 코드 변환기를 제공 합니다. hello 채널 hello 라이브 코드 변환기 로부터 라이브 입력된 스트림을 수신 하 고 하나 이상의 Streamingendpoint를 통해 스트리밍에 사용할 수 있게 합니다. 미리 보기 끝점 (미리 보기 URL) toopreview를 사용 하 고 추가 처리 및 배달 하기 전에 스트림을 유효성을 검사 하는 또한 채널을 제공 합니다.

Hello를 얻을 수 hello 채널을 만들 때 URL과 hello 미리 보기 URL을 수집 합니다. tooget 이러한 Url hello 채널이 없는 toobe hello 시작 상태입니다. 준비 toostart hello 채널에 라이브 코드 변환기에서 데이터 푸시의 경우에 hello 채널이 시작 되어야 합니다. 면 hello 라이브 코드 변환기 데이터 수집을 시작 하면 스트림을 미리볼 수 있습니다.

각 미디어 서비스 계정에는 여러 채널, 여러 프로그램 및 여러 StreamingEndpoints가 포함될 수 있습니다. Hello 대역폭 및 보안 요구에 따라 StreamingEndpoint 서비스 전용된 tooone 개 이상의 채널을 수 있습니다. 모든 StreamingEndpoint는 모든 채널에서 가져올 수 있습니다.

### <a name="program"></a>프로그램
A [프로그램](https://docs.microsoft.com/rest/api/media/operations/program) toocontrol hello 게시 및 라이브 스트림의 세그먼트의 저장소를 사용 하면 됩니다. 채널은 프로그램을 관리합니다. hello 채널과 프로그램 관계는 매우 유사한 tootraditional 미디어 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.
시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **ArchiveWindowLength** 속성입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다.

또한 ArchiveWindowLength hello 최대 양을 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 지정 합니다. 프로그램 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 프로그램은 자산에 연결됩니다. toopublish hello 프로그램 hello에 대 한 로케이터를 만들어야 합니다 자산에 연결 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL 사용 됩니다.

최대 동시에 실행 중인 프로그램 hello 여러 보관 본을 만들 수 있도록 toothree 채널을 지원 합니다. 동일한 들어오는 스트림을 합니다. 이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다. 예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 마지막 10 분입니다. tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다. 한 프로그램 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.

## <a name="billing-implications"></a>요금 청구
채널 시작 너무 "Running" hello API 통해 상태로 전환 되는 즉시 청구 됩니다.  

hello 다음 표에 나와 채널 상태의 hello API에서에서 toobilling 상태 및 Azure 포털 있습니다. Hello 상태는 hello API 및 포털 사용자 환경 간에 약간 다른 note 즉시 hello "실행 중" 상태에 hello API 통해 채널은 hello "준비" 또는 "스트리밍" 상태 hello Azure 포털에서에서 결제를 활성화할 수 있습니다.

hello API 통해 또는 hello Azure 포털에서에서 tooStop hello 채널을 해야 toostop hello 채널에서 추가로 대금을 청구 합니다.
Hello 채널 완료 되 면 채널 중지 책임이 있습니다. 오류 toostop hello 채널 계속된 청구 됩니다.

> [!NOTE]
> 기본 채널에서 작업할 때는 AMS 자동 차단 12 시간 후 hello 입력된 피드 손실 되 고 실행 중인 프로그램이 아직 "실행 중" 상태에에서 있는 모든 채널입니다. 그러나 채널 "실행 중" 상태에 있어 hello 시간 hello에 대 한 청구 계속 됩니다.
>
>

### <a id="states"></a>채널 상태 및 모드 청구 toohello 매핑되는 방식
hello 채널의 현재 상태입니다. 가능한 값은 다음과 같습니다.

* **중지됨**. 표시 되지 않으면 hello hello 채널의 초기 상태로 만든 후 (자동 시작 hello 포털에서 선택 했습니다.) 이 상태에서는 요금이 청구되지 않습니다. 이 상태의 hello 채널 속성을 업데이트할 수 있지만 스트리밍은 허용 되지 않습니다.
* **시작 중**. hello 채널을 시작 하는 중입니다. 이 상태에서는 요금이 청구되지 않습니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다. 오류가 발생 하는 경우 채널 hello toohello 중지 됨 상태를 반환 합니다.
* **실행 중**. hello 채널은 라이브 스트림을 처리할 수 있습니다. 이제 사용 요금이 청구됩니다. Hello 채널 tooprevent 추가로 청구를 중지 해야 합니다.
* **중지 중**. hello 채널을 중지 하는 중입니다. 이 일시적인 상태에서는 요금이 청구되지 않습니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.
* **삭제 중**. hello 채널을 삭제 하는 중입니다. 이 일시적인 상태에서는 요금이 청구되지 않습니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.

hello 다음 표에서 채널 맵 toohello 결제 모드를 설명 하는 방법을 나타냅니다.

| 채널 상태 | 포털 UI 표시기 | 요금이 청구됩니까? |
| --- | --- | --- |
| 시작 중 |시작 중 |없음(일시적인 상태) |
| 실행 중 |준비(실행 중인 프로그램이 없음)<br/>또는<br/>스트리밍(실행 중인 프로그램이 하나 이상임) |예 |
| 중지 중 |중지 중 |없음(일시적인 상태) |
| 중지됨 |중지됨 |아니요 |

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>관련된 항목
[Azure 미디어 서비스 조각화된 MP4 라이브 수집 사양](media-services-fmp4-live-ingest-overview.md)

[Live Enabled tooPerform 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)

[온-프레미스 인코더에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업](media-services-live-streaming-with-onprem-encoders.md)

[할당량 및 제한 사항](media-services-quotas-and-limitations.md)  

[미디어 서비스 개념](media-services-concepts.md)
