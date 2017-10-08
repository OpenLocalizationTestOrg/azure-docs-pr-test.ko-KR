---
title: "온-프레미스 인코더 다중 비트 전송률 스트림을-Azure 만들는 계속 해 서 aaaStream | Microsoft Docs"
description: "이 항목에서는 다중 비트 전송률을 수신 하는 채널을 tooset 라이브 스트림을 온-프레미스 인코더에서 하는 방법을 설명 합니다. hello 스트림을 배달할 수 있습니다 hello 적응 스트리밍 프로토콜을 다음 중 하나를 사용 하 여 하나 이상의 스트리밍 끝점을 통해 tooclient 재생 응용 프로그램: HLS, 부드러운 스트리밍, DASH 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: d9f0912d-39ec-4c9c-817b-e5d9fcf1f7ea
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 04/12/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 00709cecfc3b5b5dcfaa8f1e4b25bcf9d470d50b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-with-on-premises-encoders-that-create-multi-bitrate-streams"></a>다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍
## <a name="overview"></a>개요
Azure Media Services에서 *채널*은 라이브 스트리밍 콘텐츠를 처리하기 위한 파이프라인을 나타냅니다. 채널은 다음 두 가지 방법 중 하나로 라이브 입력 스트림을 받습니다.

* 부드러운 스트리밍 (조각난된 MP4) 스트림 toohello 채널 tooperform 사용 하도록 설정된 하지 않은 라이브 미디어 서비스로 인코딩 또는 온-프레미스 라이브 인코더가 다중 비트 전송률 RTMP 보냅니다. hello 수집 된 채널을 통해 스트림 통과 추가 처리 없이 합니다. 이 방법을 *통과*라고 합니다. Hello 다음 출력으로 다중 비트 전송률 부드러운 스트리밍 있는 라이브 인코더를 사용할 수 있습니다: 미디어 Excel, Ateme, 통신 한다고 가정, Envivio, Cisco, 및 Elemental 합니다. 라이브 인코더 뒤 hello가 출력으로 RTMP: Adobe Flash 미디어 라이브 인코더, Telestream Wirecast, Haivision, Teradek, 및 TriCaster 합니다. 라이브 인코더 라이브 인코딩을 사용 하지 않는 단일 비트 전송률 스트림을 tooa 채널 보낼 수도 있지만 권장 하지 않습니다. 미디어 서비스는 요청 하는 hello 스트림 toocustomers를 제공 합니다.

  > [!NOTE]
  > 통과 메서드를 사용 하는 hello 가장 경제적인 방법 toodo 라이브 스트리밍입니다.


* 온-프레미스 라이브 인코더 tooperform hello 다음 형식 중 하나에 미디어 서비스로 인코딩 라이브을 사용 하도록 설정 하는 단일 비트 전송률 스트림을 toohello 채널이 보냅니다: RTP (MPEG-TS), RTMP 또는 부드러운 스트리밍 (조각난된 MP4). hello 채널 hello 들어오는 단일 비트 전송률 스트림 tooa 다중 비트 전송률 (적응) 비디오 스트림으로 라이브 인코딩을 수행 합니다. 미디어 서비스는 요청 하는 hello 스트림 toocustomers를 제공 합니다.

부터는 hello 미디어 서비스 2.10 릴리스부터 채널을 만들 때 채널 tooreceive hello 입력된 스트림의 원하는 방법을 지정할 수 있습니다. 사용할지 hello 채널 tooperform 라이브 스트림 인코딩을 지정할 수 있습니다. 다음 두 가지 옵션을 사용할 수 있습니다.

* **통과**: toouse 있는 (통과 스트림) 다중 비트 전송률 스트림을 출력으로 온-프레미스 라이브 인코더를 반환 하려는 경우이 값을 지정 합니다. 이 경우 hello 들어오는 스트림은 인코딩되지 않고 출력 toohello 통해 전달 됩니다. 이 hello 2.10 릴리스 전에 채널의 hello 동작 합니다. 이 항목에서는 이 형식의 채널을 사용하는 방법에 대한 세부 정보를 제공합니다.
* **인코딩 라이브**: toouse 미디어 서비스 tooencode tooa 단일 비트 전송률 라이브 스트림을 다중 비트 전송률 스트림을 계획 하는 경우이 값을 선택 합니다. 라이브 인코딩 채널을 **실행** 상태로 놔두면 청구 요금이 발생한다는 점에 유의하세요. 라이브 스트리밍 이벤트 후 실행 중인 채널을 즉시 중지 하는 것이 좋습니다 완료 tooavoid extra 시간별 요금 됩니다. 미디어 서비스는 요청 하는 hello 스트림 toocustomers를 제공 합니다.

> [!NOTE]
> 이 항목에서는 활성화 되지 않은 채널의 특성을 설명 tooperform 라이브 인코딩을 합니다. 채널은 사용에 대 한 내용은 tooperform 라이브 인코딩을 사용 하도록 설정에 대 한 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.
>
>

다음 다이어그램 hello는 온-프레미스 라이브 인코더 toohave 다중 비트 전송률 RTMP 또는 조각난된 MP4 (부드러운 스트리밍) 스트림을 출력으로 사용 하 여 라이브 스트리밍 워크플로 나타냅니다.

![라이브 워크플로][live-overview]

## <a id="scenario"></a>일반적인 라이브 스트리밍 시나리오
hello 다음 단계에서는 일반적인 라이브 스트리밍 응용 프로그램 작성과 관련 된 작업.

1. 비디오 카메라 tooa 컴퓨터에 연결 합니다. 다중 비트 전송률 RTMP 또는 조각화된 MP4(부드러운 스트리밍) 스트림을 출력하는 온-프레미스 라이브 인코더를 실행 및 구성합니다. 자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.

    채널을 만든 후에도 이 단계를 수행할 수 있습니다.
2. 채널을 만들고 시작합니다.

3. 검색 hello 채널 URL을 수집 합니다.

    hello 라이브 인코더 사용 하 여 hello 수집 URL toosend hello 스트림 toohello 채널입니다.
4. Hello 채널 미리 보기 URL을 검색 합니다.

    이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.
5. 프로그램을 만듭니다.

    Hello Azure 포털을 사용 하면 프로그램을 만들면 자산도 만들어집니다.

    Hello.NET SDK 또는 REST를 사용 하면 자산 toocreate 필요 하 고 프로그램을 만들 때 toouse이이 자산을 지정 합니다.
6. Hello 프로그램와 관련 된 hello 자산을 게시 합니다.   

    >[!NOTE]
    >Azure 미디어 서비스 계정을 만든 경우는 **기본** hello에 tooyour 계정 추가 되어 스트리밍 끝점 **Stopped** 상태입니다. 스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 대 한 toobe **실행** 상태입니다.

7. 준비 toostart 스트리밍 및 보관 하는 hello 프로그램을 시작 합니다.

8. 필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다. hello 광고 hello 출력 스트림에 삽입 됩니다.

9. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다.

10. Hello 프로그램을 삭제 합니다 (및 필요에 따라 hello 자산을 삭제) 합니다.     

## <a id="channel"></a>채널 및 관련 구성 요소에 대한 설명
### <a id="channel_input"></a>채널 입력(수집) 구성
#### <a id="ingest_protocols"></a>수집 스트리밍 프로토콜
Media Services는 다중 비트 전송률 조각화된 MP4 및 다중 비트 전송률 RTMP를 스트리밍 프로토콜로 사용하여 라이브 피드를 수집하도록 지원합니다. Hello RTMP 수집 스트리밍 프로토콜을 선택 합니다.를 두 개의 수집 (입력된) 끝점 hello 채널에 대해 생성 됩니다.

* **기본 URL**: hello 지정 정규화 된 URL의 hello 채널의 기본 RTMP 수집 끝점입니다.
* **보조 URL** (선택 사항): hello 지정 정규화 된 URL의 hello 채널의 보조 RTMP 수집 끝점입니다.

특히 다음 시나리오는 hello에 대 한 프로그램 수집 스트림 (뿐만 아니라 인코더 장애 조치 및 내결함성)의 tooimprove hello 영속성 및 내결함성 하려는 경우 hello 보조 URL을 사용 합니다.

- 단일 인코더가 더블 푸시하여 tooboth 기본 및 보조 Url:

    이 시나리오의 주요 목적은 hello 더 많은 복원 력 toonetwork 불안정 하 고 jitter tooprovide 됩니다. 일부 RTMP 인코더는 네트워크 연결 끊기를 잘 처리하지 않습니다. 네트워크 연결이 문제가 발생 하면 인코더는 인코딩 중지 하 고 재연결 발생 하지 hello 버퍼링 데이터 전송 될 수 있습니다. 이로 인해 불연속 및 데이터 손실 문제가 발생합니다. 네트워크 연결을 끊습니다 hello Azure 측에서 잘못 된 네트워크 또는 유지 관리로 인해 발생할 수 있습니다. 주/보조 Url hello 네트워크 문제를 줄이는 하 고 제어 되는 업그레이드 프로세스를 제공 합니다. 미디어 서비스는 hello 주를 관리 하 고 보조 복제본 연결 끊김 및 지연 된 제공 예약 된 네트워크 연결이 문제가 발생 될 때마다 두 hello 간의 연결을 끊습니다. 인코더 다음 데이터를 보내는 시간 tookeep 있고 다시 연결 합니다. hello hello 순서 연결을 끊습니다 임의 수 있지만 항상 있을 지연 주/보조 또는 보조/기본 Url 사이입니다. 이 시나리오에서는 hello 인코더는 여전히 hello 단일 실패 지점이입니다.

- Tooa 푸시하여 각 인코더로 여러 인코더 전용 지점:

    이 시나리오에서는 두 인코더 및 수집 중복성을 모두 제공합니다. 이 시나리오에서는 encoder1 toohello 기본 URL 푸시하고 encoder2 toohello 보조 URL을 푸시합니다. 인코더에 실패 하면 hello 다른 인코더 수 유지할 데이터 보내기. 미디어 서비스는 hello 아래에 기본 및 보조 Url을 끊지 않습니다 때문에 데이터 중복을 유지 될 수 있습니다 동시 합니다. 이 시나리오에서는 인코더 시간이 동기화 되어와 정확 하 게 제공 가정 hello 같은 데이터입니다.  

- 여러 인코더를 두 번 푸시 tooboth 기본 및 보조 Url:

    이 시나리오에서는 두 인코더 데이터 tooboth 기본 및 보조 Url을 푸시합니다. 이 hello 최선의 안정성 및 내결함성 뿐 아니라 데이터 중복성을 제공합니다. 이 시나리오에서는 하나의 인코더가 작동을 중지하는 경우에도 인코더 오류 및 연결 해제를 모두 허용할 수 있습니다. 인코더 시간이 동기화 되어 있으며 정확 하 게 제공 가정 hello 같은 데이터입니다.  

RTMP 라이브 인코더에 대한 자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.

#### <a name="ingest-urls-endpoints"></a>수집 URL(끝점)
Channel에서 제공 하는 입력된 끝점 (수집 URL) hello 인코더 푸시할 수 있도록 hello 라이브 인코더에서 지정 하는 tooyour 채널을 스트리밍합니다.   

Hello를 얻을 수 hello 채널을 만들 때 수집 Url입니다. Tooget 있습니다에 대 한 이러한 Url hello 채널이 없는 toobe hello **실행** 상태입니다. 을 사용 하는 데이터 toohello 채널 푸시하여 준비 toostart hello 채널 hello에 있어야 **실행** 상태입니다. Hello 채널 데이터 수집을 시작 후 hello 미리 보기 URL 통해 스트림을 미리 볼 수 있습니다.

SSL 연결을 통한 조각화된 MP4(부드러운 스트리밍) 라이브 스트림을 수집하는 옵션이 있습니다. SSL 통해 tooingest 수집 URL tooHTTPS 있는지 tooupdate hello를 확인 합니다. 현재 SSL을 통해 RTMP를 수집할 수 없습니다.

#### <a id="keyframe_interval"></a>키 프레임 간격
온-프레미스 라이브 인코더 toogenerate 다중 비트 전송률 스트림을 사용 하는 경우 해당 외부 인코더에서 사용 되는 hello 키 프레임 간격 (GOP) 사진의 hello 그룹의 hello 기간을 지정 합니다. Hello 채널 이렇게 들어오는 스트림을 받은 후에 배달할 수 라이브 스트림을 hello 다음 형식 중 하나에 tooclient 재생 응용 프로그램: 부드러운 스트리밍, HTTP (대시) 및 HTTP 라이브 스트리밍 (HLS)를 통해 동적 적응 스트리밍. 라이브 스트리밍을 수행할 경우 HLS는 항상 동적으로 패키지됩니다. 기본적으로 미디어 서비스는 hello HLS 세그먼트 패키징 비율 (세그먼트 당 조각)이 hello 라이브 인코더에서 받은 hello 키프레임 간격에 따라 자동으로 계산 합니다.

다음 표에서 hello hello 세그먼트 기간 계산 하는 방법을 보여 줍니다.

| 키프레임 간격 | HLS 세그먼트 패키징 비율(FragmentsPerSegment) | 예제 |
| --- | --- | --- |
| 보다 작거나 같은 too3 초 |3:1 |Keyframeinterval (GOP)이 2 초 hello 기본 HLS 세그먼트 패키징 비율이 3 too1 됩니다. 그러면 6초 HLS 세그먼트를 만듭니다. |
| 3 too5 초 |2:1 |Keyframeinterval (GOP)이 4 초 hello 기본 HLS 세그먼트 패키징 비율이 2 too1 됩니다. 그러면 8초 HLS 세그먼트를 만듭니다. |
| 5초보다 큼 |1:1 |Keyframeinterval (GOP)이 6 초 hello 기본 HLS 세그먼트 패키징 비율이 1 too1 됩니다. 그러면 6초 HLS 세그먼트를 만듭니다. |

구성 hello 채널의 출력 하 고 설정 ChannelOutputHls 대 FragmentsPerSegment hello 세그먼트 당 조각 비율을 변경할 수 있습니다.

또한 ChanneInput에 hello KeyFrameInterval 속성을 설정 하 여 hello 키 프레임 간격 값을 변경할 수 있습니다. KeyFrameInterval를 명시적으로 설정 하면 hello HLS 세그먼트 패키징 비율이 FragmentsPerSegment 앞에서 설명한 hello 규칙을 통해 계산 됩니다.  

KeyFrameInterval 및 FragmentsPerSegment 모두 명시적으로 설정 하면 미디어 서비스 설정한 hello 값을 사용 합니다.

#### <a name="allowed-ip-addresses"></a>허용된 IP 주소
허용 되는 비디오 toothis 채널 toopublish hello IP 주소를 정의할 수 있습니다. Hello 다음 중 하나로 허용 된 IP 주소를 지정할 수 있습니다.

* 단일 IP 주소(예: 10.0.0.1)
* IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: 10.0.0.1/22)
* IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: 10.0.0.1(255.255.252.0))

지정된 IP 주소가 없고 정의된 규칙이 없는 경우, IP 주소가 허용되지 않습니다. tooallow 모든 IP 주소 규칙을 만들고 0.0.0.0/0을 설정 합니다.

### <a name="channel-preview"></a>채널 미리 보기
#### <a name="preview-urls"></a>미리 보기 URL
미리 보기 끝점 (미리 보기 URL) toopreview를 사용 하 고 추가 처리 및 배달 하기 전에 스트림을 유효성을 검사 하는 채널을 제공 합니다.

Hello 채널을 만들 때 hello 미리 보기 URL을 가져올 수 있습니다. URL에 대해 있습니다 tooget hello hello 채널이 없는 toobe hello **실행** 상태입니다. 후 hello 채널 데이터 수집을 시작 하면 스트림을 미리볼 수 있습니다.

현재 미리 보기 스트림 hello 배달 될 수만 조각난된 MP4 (부드러운 스트리밍) 형식으로 hello에 관계 없이 지정 된 입력된 유형입니다. Hello를 사용할 수 있습니다 [부드러운 스트리밍 상태 모니터](http://smf.cloudapp.net/healthmonitor) 플레이어 tootest hello 부드러운 스트림 합니다. 스트림을 hello Azure 포털 tooview에서에서 호스트에 있는 플레이어를 사용할 수 있습니다.

#### <a name="allowed-ip-addresses"></a>허용된 IP 주소
Tooconnect toohello 미리 보기 끝점 수 hello IP 주소를 정의할 수 있습니다. 지정된 IP 주소가 없는 경우 모든 IP 주소가 허용됩니다. Hello 다음 중 하나로 허용 된 IP 주소를 지정할 수 있습니다.

* 단일 IP 주소(예: 10.0.0.1)
* IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: 10.0.0.1/22)
* IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: 10.0.0.1(255.255.252.0))

### <a name="channel-output"></a>채널 출력
채널 출력에 대 한 정보를 참조 hello [키 프레임 간격](#keyframe_interval) 섹션.

### <a name="channel-managed-programs"></a>채널 관리되는 프로그램
채널은 라이브 스트림의 toocontrol hello 게시 및 세그먼트의 저장을 사용할 수 있는 프로그램 연관 됩니다. 채널은 프로그램을 관리합니다. hello 채널과 프로그램 관계는 매우 유사한 tootraditional 미디어, 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.

시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다. 보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다. 프로그램 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 프로그램 hello 스트리밍 콘텐츠를 저장 하는 자산에 연결 됩니다. 자산 hello Azure 저장소 계정에 매핑된 tooa 블록 blob 컨테이너 이며 hello 파일 hello 자산에는 해당 컨테이너의 blob으로 저장 됩니다. toopublish hello 프로그램 고객 hello 스트림을 볼 수 있도록 연결 된 hello 자산에 대 한 OnDemand 로케이터를 만들어야 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL을 사용할 수 있습니다.

최대 동시에 실행 중인 프로그램 hello 여러 보관 본을 만들 수 있도록 toothree 채널을 지원 합니다. 동일한 들어오는 스트림을 합니다. 이벤트의 여러 부분을 필요에 따라 게시하고 보관할 수 있습니다. 예를 들어 비즈니스 요구 사항 인지 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 hello 지난 10 분 한다고 가정 합니다. tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다. 한 프로그램 tooarchive 6 시간의 hello 이벤트 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.

새 이벤트에 기존 프로그램을 다시 사용할 수 없습니다. 대신, 각 이벤트에 대해 새 프로그램을 만듭니다. 준비 toostart 스트리밍 및 보관 하는 hello 프로그램을 시작 합니다. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다.

보관 toodelete 콘텐츠 중지 되어 hello 프로그램을 삭제 하 고 hello 관련된 자산을 삭제 합니다. 프로그램을 사용하는 경우 자산을 삭제할 수 없습니다. hello 프로그램을 먼저 삭제 해야 합니다.

중지 하 고 hello 프로그램을 삭제 한 후에 사용자가 스트리밍할 수 보관 된 콘텐츠 주문형 비디오로 hello 자산을 삭제 합니다. Tooretain 보관 hello 콘텐츠가 필요 하지만 스트리밍에 사용할 수 없는 경우 hello 스트리밍 로케이터를 삭제 합니다.

## <a id="states"></a>채널 상태 및 청구
Hello 채널의 현재 상태에 대 한 가능한 값은 다음과 같습니다.

* **중지**: 만든 후 hello hello 채널의 초기 상태입니다. 이 상태의 hello 채널 속성을 업데이트할 수 있지만 스트리밍은 허용 되지 않습니다.
* **시작**: hello 채널을 시작 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다. Hello 채널이 toohello 반환 오류가 발생 하면 **Stopped** 상태입니다.
* **실행**: hello 채널이 라이브 스트림을 처리할 수 있습니다.
* **중지**: hello 채널을 중지 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.
* **삭제**: hello 채널을 삭제 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.

hello 다음 표에서 채널 맵 toohello 결제 모드를 설명 하는 방법을 나타냅니다.

| 채널 상태 | 포털 UI 표시기 | 청구 여부 |
| --- | --- | --- | --- |
| **시작 중** |**시작 중** |없음(일시적인 상태) |
| **실행 중** |**준비**(실행 중인 프로그램이 없음)<p><p>또는<p>**스트리밍**(실행 중인 프로그램이 하나 이상임) |예 |
| **중지 중** |**중지 중** |없음(일시적인 상태) |
| **중지** |**중지** |아니요 |

## <a id="cc_and_ads"></a>선택 자막 및 광고 삽입
다음 표에서 hello 닫힌 캡션 및 광고 삽입에 대 한 지원 되는 표준 방법을 보여 줍니다.

| Standard | 참고 사항 |
| --- | --- |
| CEA-708 및 EIA-608(708/608) |Cea-708 및 e i A-608은 닫힌 캡션 hello 미국 및 캐나다에 대 한 표준입니다.<p><p>현재 캡션은 지원 됩니다 hello 인코드된 입력된 스트림으로 전달 되는 경우에 합니다. Toouse tooMedia 서비스 전송 hello 인코드된 스트림에 608 또는 708 캡션을 삽입할 수 있는 라이브 미디어 인코더를 해야 합니다. 미디어 서비스는 삽입 된 캡션과 tooyour 뷰어 hello 콘텐츠를 제공합니다. |
| TTML inside ismt(부드러운 스트리밍 텍스트 트랙) |미디어 서비스 동적 패키징을 사용 hello 다음 형식 중 하나에서 클라이언트 toostream 콘텐츠: DASH, HLS 또는 부드러운 스트리밍. 수집 하는 경우 조각난 MP4 (부드러운 스트리밍).ismt (부드러운 스트리밍 텍스트 트랙) 내부에 캡션과, 함께 전달할 수 있습니다 hello 스트림 tooonly 부드러운 스트리밍 클라이언트입니다. |
| SCTE-35 |S c t E-35는 디지털 신호 시스템 toocue 광고 삽입을 사용 하는입니다. 다운스트림 수신기 hello 할당 시간에 대 한 hello 스트림으로 hello 신호 toosplice 광고를 사용 합니다. S c t E-35 hello 입력 스트림에서 스파스 트랙으로 전송 되어야 합니다.<p><p>광고 신호를 전달 하는 hello 지원만 입력된 스트림 형식 조각화 되어 현재 MP4 (부드러운 스트리밍). 출력 형식 에서만 지원 hello 부드러운 스트리밍 이기도합니다. |

## <a id="considerations"></a>고려 사항
온-프레미스 라이브 인코더 toosend 다중 비트 전송률 스트림 tooa 채널을 사용 하는 경우 hello 다음 제약 조건을 적용 합니다.

* 충분 한 사용 가능한 인터넷 연결 toosend 데이터 toohello 포인트 수집 있는지 확인 합니다.
* 보조 수집 URL을 사용하려면 추가 대역폭이 필요합니다.
* 최대 10 개의 비디오 품질 수준 (계층)과 5 오디오 트랙 최대 hello 들어오는 다중 비트 전송률 스트림이 있을 수 있습니다.
* hello 가장 높은 평균 비트 전송률의 비디오 품질 수준 hello에 대 한 10mbps 미만 이어야 합니다.
* hello 모든 hello 비디오 및 오디오 스트림의 평균 비트 전송률 hello에 대 한 집계가 미만 이어야 합니다 25 Mbps 합니다.
* 연결 된 해당 프로그램이 실행 되는 또는 hello 입력된 hello 채널 프로토콜을 변경할 수 없습니다. 다른 프로토콜을 요청하는 경우 각각의 입력 프로토콜에 대한 개별 채널을 만들어야 합니다.
* 채널에서 단일 비트 전송률을 수집할 수 있습니다. 하지만 hello 클라이언트 응용 프로그램은 단일 비트 전송률 스트림을 받습니다 hello 채널에서 hello 스트림, 처리 하지 않으므로. 이 옵션을 권장하지 않습니다.

채널 및 관련된 구성 요소와 기타 고려 사항 관련된 tooworking 다음과 같습니다.

* Hello 라이브 인코더를 다시 구성할 때마다 호출 hello **재설정** hello 채널에서 메서드. Hello 채널을 다시 설정 하기 전에 toostop hello 프로그램을 해야 합니다. Hello 채널을 다시 설정한 후 hello 프로그램을 다시 시작 합니다.
* Hello에 경우에 채널을 중지할 수 있습니다 **실행** 상태 및 모든 프로그램 hello 채널에서 중지 되었습니다.
* 기본적으로 5 개만 채널 tooyour 미디어 서비스 계정을 추가할 수 있습니다. 자세한 내용은 [할당량 및 제한 사항](media-services-quotas-and-limitations.md)을 참조하세요.
* 채널 hello에 있을 때만 청구 됩니다 **실행** 상태입니다. 자세한 내용은 참조 toohello [채널 상태 및 청구](media-services-live-streaming-with-onprem-encoders.md#states) 섹션.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="feedback"></a>사용자 의견
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>관련된 항목
[Azure Media Services 조각화된 MP4 라이브 수집 사양](media-services-fmp4-live-ingest-overview.md)

[Azure Media Services 개요 및 일반적인 시나리오](media-services-overview.md)

[Media Services 개념](media-services-concepts.md)

[live-overview]: ./media/media-services-manage-channels-overview/media-services-live-streaming-current.png
