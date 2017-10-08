---
title: "Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 aaaLive 스트리밍 | Microsoft Docs"
description: "이 항목에서는 단일 비트 전송률을 수신 하는 채널을 tooset 라이브 스트림을 온-프레미스 인코더에서 하 한 다음 미디어 서비스 라이브 인코딩 tooadaptive 비트 전송률 스트림을 수행 하는 방법을 설명 합니다. hello 스트림을 배달할 수 있습니다 하나 이상의 스트리밍 끝점을 통해 tooclient 재생 응용 프로그램 hello 적응 스트리밍 프로토콜을 다음 중 하나를 사용 하 여: HLS, 부드러운 스트림 MPEG DASH 합니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 30ce6556-b0ff-46d8-a15d-5f10e4c360e2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: a8bbdd1570cc9a11bfc2de7bb4ceb9006cc25534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams"></a>라이브 Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 스트리밍
## <a name="overview"></a>개요
AMS(Azure 미디어 서비스)에서 **채널** 은 라이브 스트리밍 콘텐츠를 처리하기 위한 파이프라인을 나타냅니다. **채널** 은 다음 두 가지 방법 중 하나로 라이브 입력 스트림을 받습니다.

* 온-프레미스 라이브 인코더 toohello 채널을 사용 하도록 설정된 tooperform 라이브 hello 다음 형식 중 하나에 미디어 서비스로 인코딩 단일 비트 전송률 스트림을 보냅니다: RTP (MPEG-TS), RTMP 또는 부드러운 스트리밍 (조각난 MP4). hello 채널 다음 라이브 인코딩합니다 hello 들어오는 단일 비트 전송률 스트림 tooa 다중 비트 전송률 (적응) 비디오 스트림으로 합니다. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.
* 온-프레미스 라이브 인코더가 다중 비트 전송률 보냅니다 **RTMP** 또는 **부드러운 스트리밍** 하지 않은 (조각난 MP4) toohello 채널 tooperform 라이브 AMS 인코딩을 사용 하도록 설정 합니다. 수집 된 hello 스트림을 통과 **채널**추가 처리 없이 s입니다. 이 방법을 **통과**라고 합니다. Hello 다음 다중 비트 전송률 부드러운 스트리밍 출력 하는 라이브 인코더를 사용할 수 있습니다: MediaExcel, Ateme, 통신 한다고 가정, Envivio, Cisco 및 Elemental 합니다. hello 라이브 인코더 출력: Adobe Flash 미디어 라이브 인코더 (FMLE), Telestream Wirecast, Haivision, Teradek 및 Tricaster 인코더입니다.  라이브 인코더에서 라이브 인코딩의 해제 되어 있지만 권장 되지 않습니다는 단일 비트 전송률 스트림을 tooa 채널을 보낼 수도 있습니다. 요청 미디어 서비스는 hello 스트림 toocustomers를 제공 합니다.
  
  > [!NOTE]
  > 통과 메서드를 사용 하는 hello 가장 경제적인 방법 toodo 라이브 스트리밍입니다.
  > 
  > 

부터는 hello 미디어 서비스 2.10 릴리스부터 채널을 만들 때 어떤 방식으로 채널 tooreceive hello 입력된 스트림 및 채널 tooperform hello에 대 한 원하는 여부에 대해 원하는 श 스트림 인코딩을 지정할 수 있습니다. 다음 두 가지 옵션을 사용할 수 있습니다.

* **None** – 다중 비트 전송률 스트림을 (통과 스트림)을 출력 하는 온-프레미스 라이브 인코더 toouse 하려는 경우이 값을 지정 합니다. 이 경우 hello 들어오는 스트림은 인코딩되지 않고 출력 toohello 통과 합니다. 이것이 채널 이전 too2.10 릴리스의 hello 동작입니다.  이 형식의 채널 작업에 대한 자세한 내용은 [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.
* **표준** –이 값을 선택, toouse 미디어 서비스 tooencode 하려는 경우 단일 비트 전송률 라이브 스트림을 toomulti 비트 전송률 스트림을 합니다. 업그레이드할 청구 영향을 줄 정도로 라이브 인코딩의 라이브 인코딩 채널 hello "실행 중" 상태로 남게 됩니다 인해 발생 하는 요금 청구 점을 기억해 야 합니다.  라이브 스트리밍 이벤트 후 실행 중인 채널을 즉시 중지 하는 것이 좋습니다 완료 tooavoid extra 시간별 요금 됩니다.

> [!NOTE]
> 이 항목에서는 사용할 수 있는 채널의 특성을 설명 tooperform 라이브 인코딩을 (**표준** 인코딩 유형). Tooperform 라이브 인코딩을 사용 하는 작업 하지 않은 채널에 대 한 정보, 참조 [다중 비트 전송률 스트림을 만들 수 있는 온-프레미스 인코더를 통해 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)합니다.
> 
> 있는지 tooreview hello 확인 [고려 사항](media-services-manage-live-encoder-enabled-channels.md#Considerations) 섹션.
> 
> 

## <a name="billing-implications"></a>요금 청구
라이브 인코딩 채널 시작 너무 "Running" hello API 통해 상태로 전환 되는 즉시 청구 됩니다.   또한 hello Azure 포털 또는 hello Azure 미디어 서비스 탐색기 도구 (http://aka.ms/amse) hello 상태를 볼 수 있습니다.

hello 다음 표에 나와 채널 상태의 hello API에서에서 toobilling 상태 및 Azure 포털 있습니다. Hello 상태는 hello API 및 포털 사용자 환경 간에 약간 다른 note 즉시 hello "실행 중" 상태에 hello API 통해 채널은 hello "준비" 또는 "스트리밍" 상태 hello Azure 포털에서에서 결제를 활성화할 수 있습니다.
hello API 통해 또는 hello Azure 포털에서에서 tooStop hello 채널을 해야 toostop hello 채널에서 추가로 대금을 청구 합니다.
Hello 라이브 인코딩 채널 완료 되 면 채널 중지 책임이 있습니다.  오류 toostop 인코딩 채널 계속된 청구 됩니다.

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

### <a name="automatic-shut-off-for-unused-channels"></a>사용하지 않는 채널에 대한 자동 종료
2016년 1월 25일부터 시작하는 미디어 서비스는 장기간 사용하지 않은 상태로 실행된 후 자동으로 채널을 중지하는(라이브 인코딩 사용) 업데이트를 출시했습니다. 이 없는 활성 프로그램 있고 오랜 시간에 대 한 피드는 입력된 기여 받았는지 여부 tooChannels 적용 됩니다.

hello 임계값을 사용 하지 않는 동안에는 12 시간 명목상으로 있지만 주체 toochange 있습니다.

## <a name="live-encoding-workflow"></a>라이브 인코딩 워크플로
hello 다음 다이어그램은 나타냅니다 채널이 hello 다음 프로토콜 중 하나에 단일 비트 전송률 스트림을 받는 라이브 스트리밍 워크플로에: RTMP, 부드러운 스트리밍 또는 RTP (MPEG-TS); 그런 다음 hello 스트림 tooa 다중 비트 전송률 스트림으로를 인코딩합니다. 

![라이브 워크플로][live-overview]

## <a id="scenario"></a>일반적인 라이브 스트리밍 시나리오
hello 다음은 일반적인 라이브 스트리밍 응용 프로그램 만들기와 관련 된 일반적인 단계입니다.

> [!NOTE]
> 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오. 업그레이드할 청구 영향을 줄 정도로 라이브 인코딩의 라이브 인코딩 채널 hello "실행 중" 상태로 남게 됩니다 인해 발생 하는 시간별 요금 청구 점을 기억해 야 합니다.  라이브 스트리밍 이벤트 후 실행 중인 채널을 즉시 중지 하는 것이 좋습니다 완료 tooavoid extra 시간별 요금 됩니다. 
> 
> 

1. 비디오 카메라 tooa 컴퓨터에 연결 합니다. 시작 하 고 출력 하는 온-프레미스 라이브 인코더 구성는 **단일** hello 다음 프로토콜 중 하나에 비트 전송률 스트림을: RTMP, 부드러운 스트리밍 또는 RTP (MPEG-TS). 
   
    이 단계는 채널을 만든 후에도 수행할 수 있습니다.
2. 채널을 만들고 시작합니다. 
3. 검색 hello 채널 수집 URL입니다. 
   
    hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.
4. Hello 채널 미리 보기 URL을 검색 합니다. 
   
    이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.
5. 프로그램을 만듭니다. 
   
    Azure 포털을 hello를 사용 하 여 때 프로그램을 만들어 자산을 만듭니다. 
   
    .NET SDK 또는 REST를 사용 하는 경우 자산 toocreate 필요 하 고 프로그램을 만들 때 toouse이이 자산을 지정 합니다. 
6. Hello 프로그램과 연결 된 hello 자산을 게시 합니다.   
   
    >[!NOTE]
    >AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 대 한 toobe **실행** 상태입니다. 
    
7. 스트리밍 및 보관 준비 toostart 있을 때는 hello 프로그램을 시작 합니다.
8. 필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다. hello 광고 hello 출력 스트림에 삽입 됩니다.
9. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다.
10. Hello 프로그램을 삭제 합니다 (한 필요에 따라 hello 자산을 삭제) 합니다.   

> [!NOTE]
> 매우 중요 tooforget tooStop 라이브 인코딩을 채널 되지 않습니다. 업그레이드할 라이브 인코딩에 영향 청구 시간별은 라이브 인코딩 채널 hello "실행 중" 상태로 남게 됩니다 인해 발생 하는 요금 청구 점을 기억해 야 합니다.  라이브 스트리밍 이벤트 후 실행 중인 채널을 즉시 중지 하는 것이 좋습니다 완료 tooavoid extra 시간별 요금 됩니다. 
> 
> 

## <a id="channel"></a>채널 입력(수집) 구성
### <a id="Ingest_Protocols"></a>수집 스트리밍 프로토콜
경우 hello **인코더 유형을** 너무 설정**표준**, 올바른 옵션은:

* **RTP** (MPEG-TS): RTP를 통한 MPEG-2 전송 스트림  
* 단일 비트 전송률 **RTMP**
* 단일 비트 전송률 **조각화된 MP4** (부드러운 스트리밍)

#### <a name="rtp-mpeg-ts---mpeg-2-transport-stream-over-rtp"></a>RTP(MPEG-TS) - RTP를 통한 MPEG-2 전송 스트림
일반적인 사용 사례: 

전문 방송국 일반적으로 작업할 실세계 기술, Ericsson, Ateme, Imagine 또는 Envivio toosend 같은 공급 업체에서 고급 온-프레미스 라이브 인코더를 스트림으로. IT 부서 및 개인 네트워크와 함께 사용되는 경우가 많습니다.

고려 사항:

* 입력 단일 프로그램 전송 스트림 (SPTS) hello 사용이 좋습니다. 
* RTP를 통한 mpeg-2 TS를 사용 하 여 too8 오디오 스트림을를 입력할 수 있습니다. 
* 비디오 스트림 hello 15mbps 아래는 평균 비트 전송률이 있어야 합니다.
* hello 집계 평균 비트 전송률 hello 오디오 스트림의 1mbps 미만 이어야 합니다.
* 다음 지원 되는 코덱을 hello 됩니다.
  
  * MPEG-2 / H.262 비디오 
    
    * 기본 프로필(4:2:0)
    * 상위 프로필(4:2:0, 4:2:2)
    * 422 프로필(4:2:0, 4:2:2)
  * MPEG-4 AVC / H.264 비디오  
    
    * 기준, 기본, 상위 프로필(8비트 4:2:0)
    * 상위 10 프로필(10비트 4:2:0)
    * 상위 422 프로필(10비트 4:2:2)
  * MPEG-2 AAC-LC 오디오 
    
    * 모노, 스테레오, 서라운드(5.1, 7.1)
    * Mpeg-2 스타일 ADTS 패키징
  * Dolby Digital(AC-3) 오디오 
    
    * 모노, 스테레오, 서라운드(5.1, 7.1)
  * MPEG 오디오(Layer II 및 III) 
    
    * 모노, 스테레오
* 권장되는 브로드캐스트 인코더는 다음과 같습니다.
  
  * Imagine Communications Selenio ENC 1
  * Imagine Communications Selenio ENC 2
  * Elemental Live

#### <a id="single_bitrate_RTMP"></a>단일 비트 전송률 RTMP
고려 사항:

* hello 들어오는 스트림을 다중 비트 전송률 비디오를 포함할 수 없습니다.
* 비디오 스트림 hello 15mbps 아래는 평균 비트 전송률이 있어야 합니다.
* 오디오 스트림 hello 1mbps 아래는 평균 비트 전송률이 있어야 합니다.
* 다음 지원 되는 코덱을 hello 됩니다.
* MPEG-4 AVC / H.264 비디오
* 기준, 기본, 상위 프로필(8비트 4:2:0)
* 상위 10 프로필(10비트 4:2:0)
* 상위 422 프로필(10비트 4:2:2)
* MPEG-2 AAC-LC 오디오
* 모노, 스테레오, 서라운드(5.1, 7.1)
* 44.1kHz 샘플링 주기
* Mpeg-2 스타일 ADTS 패키징
* 권장되는 인코더는 다음과 같습니다.
* Telestream Wirecast
* Flash Media Live Encoder

#### <a name="single-bitrate-fragmented-mp4-smooth-streaming"></a>단일 비트 전송률 조각화된 MP4(부드러운 스트리밍)
일반적인 사용 사례:

실세계 기술, Ericsson, Ateme, Envivio toosend hello hello open 인터넷 tooa 근처의 Azure 데이터 센터를 통해 입력된 스트림 공급 업체에서 온-프레미스 라이브 인코더를 사용 합니다.

고려 사항:

[단일 비트 전송률 RTMP](media-services-manage-live-encoder-enabled-channels.md#single_bitrate_RTMP)와 동일합니다.

#### <a name="other-considerations"></a>기타 고려 사항
* 연결 된 해당 프로그램이 실행 되는 또는 hello 입력된 hello 채널 프로토콜을 변경할 수 없습니다. 다른 프로토콜을 요청하는 경우 각각의 입력 프로토콜에 대한 개별 채널을 만들어야 합니다.
* Hello 들어오는 비디오 스트림에 대 한 최대 해상도 1920 x 1080 및 최대 60 필드 수/초, 인터레이스된 경우 또는 30 프레임/second 점진적 하는 경우.

### <a name="ingest-urls-endpoints"></a>수집 URL(끝점)
Channel에서 제공 하는 입력된 끝점 (수집 URL) hello 인코더 푸시할 수 있도록 hello 라이브 인코더에서 지정 하는 tooyour 채널을 스트리밍합니다.

Hello를 얻을 수 있습니다는 채널을 만들면 Url을 수집 합니다. tooget 이러한 Url hello 채널이 없는 toobe hello **실행** 상태입니다. Hello에 있어야 준비 toostart hello 채널에 데이터 푸시의 경우 **실행** 상태입니다. Hello 채널 데이터 수집을 시작 되 면 hello 미리 보기 URL 통해 스트림을 미리 볼 수 있습니다.

SSL 연결을 통한 조각화된 MP4(부드러운 스트리밍) 라이브 스트림 수집 옵션이 있습니다. SSL 통해 tooingest 수집 URL tooHTTPS 있는지 tooupdate hello를 확인 합니다. 현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.  

### <a name="allowed-ip-addresses"></a>허용된 IP 주소
허용 되는 비디오 toothis 채널 toopublish hello IP 주소를 정의할 수 있습니다. 허용된 IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: ‘10.0.0.1/22’) 또는 IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.252.0)').

IP 주소가 지정되지 않고 정의된 규칙이 없는 경우 IP 주소가 허용되지 않습니다. tooallow 모든 IP 주소 규칙을 만들고 0.0.0.0/0을 설정 합니다.

## <a name="channel-preview"></a>채널 미리 보기
### <a name="preview-urls"></a>미리 보기 URL
미리 보기 끝점 (미리 보기 URL) toopreview를 사용 하 고 추가 처리 및 배달 하기 전에 스트림을 유효성을 검사 하는 채널을 제공 합니다.

Hello 채널을 만들 때 hello 미리 보기 URL을 가져올 수 있습니다. tooget hello URL hello 채널이 없는 toobe hello **실행** 상태입니다.

면 hello 채널 데이터 수집을 시작 하면 스트림을 미리볼 수 있습니다.

> [!NOTE]
> 현재 미리 보기 스트림 hello만 전달 될 수 있습니다 조각난 MP4 (부드러운 스트리밍) 형식 hello에 관계 없이 지정 된 입력된 유형입니다. Hello를 사용할 수 있습니다 [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) 플레이어 tootest hello 부드러운 스트림 합니다. 사용할 수도 있습니다 스트림을 hello Azure 포털 tooview에서에서 플레이어를 호스트 합니다.
> 
> 

### <a name="allowed-ip-addresses"></a>허용된 IP 주소
Tooconnect toohello 미리 보기 끝점 수 hello IP 주소를 정의할 수 있습니다. 지정된 IP 주소가 없는 경우 모든 IP 주소가 허용됩니다. 허용된 IP 주소는 단일 IP 주소(예: ‘10.0.0.1’), IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: ‘10.0.0.1/22’) 또는 IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: ‘10.0.0.1(255.255.252.0)’)로 지정될 수 있습니다.

## <a name="live-encoding-settings"></a>라이브 인코딩 설정
이 섹션에서는 hello 채널 내의 라이브 인코더가 hello에 대 한 hello 설정을 수 있는 방법을 설명 hello 때 조정 **인코딩 유형** 채널 설정 너무**표준**합니다.

> [!NOTE]
> Azure를 사용하여 여러 언어 트랙을 입력하고 라이브 인코딩을 수행할 때 RTP만은 다국어 입력에 지원됩니다. RTP를 통한 mpeg-2 TS를 사용 하 여 too8 오디오 스트림을를 정의할 수 있습니다. RTMP 또는 부드러운 스트리밍으로 여러 오디오 트랙을 수집하는 작업은 현재 지원되지 않습니다. 통한 라이브 인코딩을 수행할 때 [온-프레미스 라이브 인코딩합니다](media-services-live-streaming-with-onprem-encoders.md), 더 이상 처리 하지 않고 채널을 통해 전달 tooAMS 보내집니다 무엇이 든 때문에 이러한 제한이 않습니다.
> 
> 

### <a name="ad-marker-source"></a>광고 표식 원본
Hello 광고 표식 신호의 소스를 지정할 수 있습니다. 기본값은 **Api**, hello 채널 내의 해당 hello 라이브 인코더를 나타내는 수신 해야 하는 비동기 tooan **광고 표식 API**합니다.

hello 다른 유효한 옵션은 **Scte35** (경우에 허용 hello 수집 스트리밍 프로토콜 (MPEG-TS) tooRTP 설정 됩니다. Scte35를 지정 하면 hello 라이브 인코더는 hello 입력 RTP (MPEG-TS) 스트림에서 신호 s c t E-35을 구문 분석 합니다.

### <a name="cea-708-closed-captions"></a>CEA 708 선택 캡션
Hello 라이브 인코더 tooignore CEA 708 캡션 데이터를 알려 주는 선택적 플래그 hello 들어오는 비디오에 포함 합니다. Hello 플래그를 설정 (기본값) toofalse hello 인코더에서는 검색 하 고 다시 hello 출력 비디오 스트림으로 CEA 708 데이터를 삽입 합니다.

### <a name="video-stream"></a>비디오 스트림
선택 사항입니다. Hello 입력된 비디오 스트림을 설명합니다. 이 필드를 지정 하지 않으면 hello 기본값이 사용 됩니다. 이 설정은 hello 입력 스트리밍 프로토콜이 tooRTP (MPEG-TS)를 설정 된 경우에 허용 됩니다.

#### <a name="index"></a>인덱스
Hello hello 채널 내의 라이브 인코더에 의해 처리 되어야 사용할 입력된 비디오 스트림을 지정 하는 0부터 시작 인덱스입니다. 이 설정은 수집 스트리밍 프로토콜이 RTP(MPEG-TS)인 경우에만 적용됩니다.

기본값은 0입니다. 단일 프로그램 전송 스트림 (SPTS)에서 toosend 것이 좋습니다. Hello 입력된 스트림에 여러 프로그램이 들어 있는 경우 hello 라이브 인코더 구문 분석 hello 입력의 프로그램 맵 테이블 (PMT) hello, 스트림 형식 이름이 mpeg-2 비디오 또는 h. 264, 있는 hello 입력을 식별 하 고 hello 해야 합니다..에에서 지정 된 hello 순서로 정렬 합니다. 그런 다음 인덱스를 0부터 시작 하는 hello를 사용 toopick 해당 정렬에서 n 번째 항목 hello 합니다.

### <a name="audio-stream"></a>오디오 스트림
선택 사항입니다. Hello 입력된 오디오 스트림을 설명합니다. 이 필드를 지정 하지 않으면 지정 된 hello 기본값이 적용 됩니다. 이 설정은 hello 입력 스트리밍 프로토콜이 tooRTP (MPEG-TS)를 설정 된 경우에 허용 됩니다.

#### <a name="index"></a>인덱스
단일 프로그램 전송 스트림 (SPTS)에서 toosend 것이 좋습니다. Hello 입력된 스트림에 여러 프로그램이 들어 있는 경우 hello hello 채널 내의 라이브 인코더가 hello 입력의 프로그램 맵 테이블 (PMT) hello를 구문 분석, 스트림 형식 이름이 mpeg-2 AAC ADTS 또는 ac-3 시스템 A 또는 ac-3 시스템 B 또는 mpeg-2 개인 있는 hello 입력을 식별 합니다. PES, mpeg-1 오디오 또는 mpeg-2 오디오 해야 합니다. hello에 지정 된 hello 순서로 정렬 합니다 그런 다음 인덱스를 0부터 시작 하는 hello를 사용 toopick 해당 정렬에서 n 번째 항목 hello 합니다.

#### <a name="language"></a>언어
hello ENG. 같은 tooISO 639-2를 준수 하는 hello 오디오 스트림의 언어 식별자 가 없으면 hello 기본값인 UND (정의 되지 않음).

있을를 too8 오디오 스트림 집합 hello toohello 채널 입력 RTP를 통한 mpeg-2 TS 인을 지정할 수 있습니다. 그러나 있을 수 있습니다 hello로 두 개의 항목이 없는 인덱스의 동일한 값입니다.

### <a id="preset"></a>시스템 기본 설정
Hello toobe hello이이 채널 내의 라이브 인코더에서 사용 하는 사전 설정을 지정 합니다. 현재 값이 허용 되는 hello **Default720p** (기본값).

사용자 지정 사전 설정이 필요한 경우 amslived@microsoft.com으로 문의해야 합니다.

**Default720p** 는 hello 비디오 다음 7 개 레이어로 hello 인코딩합니다.

#### <a name="output-video-stream"></a>출력 비디오 스트림
| 비트 전송률 | 너비 | 높이 | MaxFPS | 프로필 | 출력 스트림 이름 |
| --- | --- | --- | --- | --- | --- |
| 3500 |1280 |720 |30 |높음 |Video_1280x720_3500kbps |
| 2200 |960 |540 |30 |기본 |Video_960x540_2200kbps |
| 1350 |704 |396 |30 |기본 |Video_704x396_1350kbps |
| 850 |512 |288 |30 |기본 |Video_512x288_850kbps |
| 550 |384 |216 |30 |기본 |Video_384x216_550kbps |
| 350 |340 |192 |30 |기초 |Video_340x192_350kbps |
| 200 |340 |192 |30 |기초 |Video_340x192_200kbps |

#### <a name="output-audio-stream"></a>출력 오디오 스트림
오디오는 샘플링 속도 44.1 k h z의 64kbps로 인코딩된 toostereo AAC-LC 있습니다.

## <a name="signaling-advertisements"></a>광고 신호 보내기
채널이 라이브 인코딩을 사용하도록 설정된 경우 파이프라인에 비디오를 처리하는 구성 요소가 있으며 이 구성 요소를 조작할 수 있습니다. Hello 채널 tooinsert 슬레이트 및/또는 hello 나가는 적응 비트 전송률 스트림으로 광고에 알릴 수 있습니다. 슬레이트 이미지 (예: 광고 재생) 동안 hello 입력된 라이브 피드를 toocover을 사용할 경우에 따라 수 있는 남아 있습니다. 광고 신호, hello 나가는 스트림 tootell hello 비디오 플레이어 tootake 특별 한 동작으로 – hello 적절 한 시간에 tooswitch tooan 광고 등 포함 시간 동기화 신호 됩니다. 이 참조 [블로그](https://codesequoia.wordpress.com/2014/02/24/understanding-scte-35/) 이 용도로 사용 되는 s c t E-35 hello 신호 메커니즘에 대 한 개요입니다. 다음은 라이브 이벤트에서 구현할 수 있는 일반적인 시나리오입니다.

1. Hello 이벤트를 시작 하기 전에 사전 이벤트 이미지 될 뷰어 있어야 합니다.
2. Hello 이벤트가 종료 된 후 사후 이벤트 이미지 될 뷰어 있어야 합니다.
3. Hello 이벤트 (예를 들어 hello 경기장에서 전원 오류) 하는 동안 문제가 없으면 오류 이벤트 이미지를 가져올 뷰어 있어야 합니다.
4. 광고 재생 중 피드 광고 재생 이미지 toohide hello 라이브 이벤트를 보냅니다.

hello 다음은 hello 속성 광고 신호 때 설정할 수 있습니다. 

### <a name="duration"></a>기간
hello 기간 (초) hello 광고 재생 중입니다. 이 toobe 0이 아닌 양수 값 순서 toostart hello 광고 재생 합니다. 광고 재생 hello 기간과 진행 중인 경우 CueId hello로 집합 toozero 일치 하는 hello 진행 중인 광고 재생 시간의 취소 됩니다.

### <a name="cueid"></a>CueId
다운스트림 응용 프로그램 tootake 적절 한 작업에서 사용 하는 toobe hello 광고 재생에 대 한 고유 ID입니다. Toobe는 양의 정수 필요합니다. 이 값 tooany 임의의 양의 정수를 설정 하거나 업스트림 시스템 tootrack hello 큐 Id를 사용할 수 있습니다. Hello API 통해 전송 하기 전에 특정 toonormalize 모든 id toopositive 정수를 확인 합니다.

### <a name="show-slate"></a>슬레이트 표시
선택 사항입니다. 신호를 라이브 인코더 tooswitch toohello hello [기본 슬레이트](media-services-manage-live-encoder-enabled-channels.md#default_slate) 광고 재생 중 이미지 및 hello 들어오는 비디오 피드를 숨깁니다. 슬레이트 중에는 오디오도 음소거됩니다. 기본값은 **false**입니다. 

사용 되는 hello 이미지 hello hello hello 채널 생성 시 hello 기본 슬레이트 자산 Id 속성을 통해 지정 됩니다. hello slate 됩니다 toofit hello 표시 이미지 크기를 확대 합니다. 

## <a name="insert-slate--images"></a>슬레이트 이미지 삽입
hello 채널 내의 라이브 인코더가 hello 신호를 받은 tooswitch tooa 슬레이트 이미지 될 수 있습니다. 신호를 받은 tooend 진행 중인 슬레이트 수도 있습니다. 

hello 라이브 인코더 구성된 tooswitch tooa 슬레이트 이미지 될 및 hello 들어오는 비디오 신호 특정 상황에서-예를 들어 광고 재생 중 숨길 수 있습니다. 이러한 슬레이트를 구성하지 않는 경우 입력 비디오가 해당 중간 광고 중에 마스킹되지 않습니다.

### <a name="duration"></a>기간
hello 슬레이트의 기간 (초) hello입니다. 이 toobe 0이 아닌 양수 값 순서 toostart hello 슬레이트입니다. 진행 중인 슬레이트가 있는 경우 기간을 0으로 지정하면 진행 중인 슬레이트가 종료됩니다.

### <a name="insert-slate-on-ad-marker"></a>광고 표식에서 슬레이트 삽입
때 집합 tootrue,이 설정은 광고 재생 중 hello 라이브 인코더 tooinsert 슬레이트 이미지를 구성합니다. hello 기본값은 true입니다. 

### <a id="default_slate"></a>기본 슬레이트 자산 ID

선택 사항입니다. Hello의 hello hello 슬레이트 이미지를 포함 하는 미디어 서비스 자산의 자산 Id를 지정 합니다. 기본값은 null입니다. 


>[!NOTE] 
>Hello 채널을 만들기 전에 hello 슬레이트 이미지 제약 조건에 따라 hello로 업로드 되어야 합니다 (이 자산에 다른 모든 파일 이어야 함)를 전용된 자산으로. 이 이미지는 hello 라이브 인코더의 tooan 광고 재생 인해 슬레이트를 삽입 하는 경우 또는 명시적으로 신호 tooinsert 슬레이트만 사용 됩니다. hello 라이브 인코더도 동안 이동할 수 있습니다를 슬레이트 모드로 특정 오류 조건-예를 들어 hello 입력된 신호를 잃게 됩니다. 가 없는 옵션 toouse 현재 사용자 지정 이미지 hello 라이브 인코더에는 이러한 '입력된 신호 손실' 상태로 전환입니다. [여기](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/10190457-define-custom-slate-image-on-a-live-encoder-channel)서 이 기능에 대해 투표할 수 있습니다.


* 최대 1920x1080 해상도.
* 최대 3MB 크기.
* hello 파일 이름 확장명은 *.jpg 있어야 합니다.
* 해당 자산에만 AssetFile 및이 AssetFile hello 주 파일으로 표시 해야 하는 hello로 hello 이미지 자산으로 업로드 해야 합니다. hello 자산 저장소 암호화 될 수 없습니다.

경우 hello **기본 슬레이트 자산 Id** 를 지정 하지 않으면 및 **광고 표식에 슬레이트 삽입** 너무 설정**true**, 기본 Azure 미디어 서비스 이미지를 사용 하는 toohide hello 입력 됩니다 비디오 스트림 합니다. 슬레이트 중에는 오디오도 음소거됩니다. 

## <a name="channels-programs"></a>채널의 프로그램
채널은 toocontrol hello 게시 및 라이브 스트림의 세그먼트는 저장이를 사용 하는 프로그램을 연결 합니다. 채널은 프로그램을 관리합니다. hello 채널과 프로그램 관계는 매우 유사한 tootraditional 미디어 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.

시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다. 이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다. 보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다. 프로그램 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다. 또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.

각 프로그램 hello 스트리밍 콘텐츠를 저장 하는 자산에 연결 됩니다. 자산 hello Azure 저장소 계정에서 매핑된 tooa 블록 blob 컨테이너 이며 hello 파일 hello 자산에는 해당 컨테이너의 blob으로 저장 됩니다. 고객 hello에 대 한 OnDemand 로케이터를 만들어야 하는 hello 스트림을 볼 수 있도록 toopublish hello 프로그램 자산에 연결 합니다. 이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL 사용 됩니다.

최대 동시에 실행 중인 프로그램 hello 여러 보관 본을 만들 수 있도록 toothree 채널을 지원 합니다. 동일한 들어오는 스트림을 합니다. 이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다. 예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 마지막 10 분입니다. tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다. 한 프로그램 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다. hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.

새 이벤트에 기존 프로그램을 다시 사용할 수 없습니다. 대신 만들고 hello 라이브 스트리밍 응용 프로그램 프로그래밍 섹션에 설명 된 대로 각 이벤트에 대 한 새 프로그램을 시작 합니다.

스트리밍 및 보관 준비 toostart 있을 때는 hello 프로그램을 시작 합니다. Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다. 

보관 toodelete 콘텐츠 중지 되어 hello 프로그램을 삭제 하 고 hello 관련된 자산을 삭제 합니다. 프로그램;에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 프로그램을 먼저 삭제 해야 합니다. 

중지 하 고 hello 프로그램을 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.

수행 tooretain hello 보관 된 콘텐츠, 하지만 스트리밍에 사용할 수 없는, hello 스트리밍 로케이터를 삭제 합니다.

## <a name="getting-a-thumbnail-preview-of-a-live-feed"></a>라이브 피드의 축소판 그림 미리 보기 가져오기
라이브 인코딩을 사용 하는 hello 채널에 도달할 때 이제 hello 라이브 피드 미리 보기를 얻을 수 있습니다. 이 옵션을 사용 하면 라이브 피드 hello 채널에 도달 함 실제로 있는지 여부를 매우 유용한 도구 toocheck 수 있습니다. 

## <a id="states"></a>채널 상태 및 상태 매핑하 toohello 모드 청구 하는 방법
hello 채널의 현재 상태입니다. 가능한 값은 다음과 같습니다.

* **중지됨**. 만든 후 hello 채널의 hello 초기 상태입니다. 이 상태의 hello 채널 속성을 업데이트할 수 있지만 스트리밍은 허용 되지 않습니다.
* **시작 중**. hello 채널을 시작 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다. 오류가 발생 하는 경우 채널 hello toohello 중지 됨 상태를 반환 합니다.
* **실행 중**. hello 채널은 라이브 스트림을 처리할 수 있습니다.
* **중지 중**. hello 채널을 중지 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.
* **삭제 중**. hello 채널을 삭제 하는 중입니다. 이 상태에서는 업데이트 또는 스트리밍이 허용되지 않습니다.

hello 다음 표에서 채널 맵 toohello 결제 모드를 설명 하는 방법을 나타냅니다. 

| 채널 상태 | 포털 UI 표시기 | 청구 여부 |
| --- | --- | --- |
| 시작 중 |시작 중 |없음(일시적인 상태) |
| 실행 중 |준비(실행 중인 프로그램이 없음)<br/>또는<br/>스트리밍(실행 중인 프로그램이 하나 이상임) |예 |
| 중지 중 |중지 중 |없음(일시적인 상태) |
| 중지됨 |중지됨 |아니요 |

> [!NOTE]
> 현재 hello 채널 시작 평균 2 분 이며 하지만 too20 + 분을 때때로 걸릴 수 있습니다. 채널 재설정 too5 분 정도 걸릴 수 있습니다.
> 
> 

## <a id="Considerations"></a>고려 사항
* 채널 **표준** 입력된 소스/기여 피드 손실 발생 인코딩 유형, 해당 오류 슬레이트 및 대기를 hello 원본 비디오/오디오로 보완 합니다. hello 입력/기여 피드 다시 시작 될 때까지 hello 채널에서 슬레이트 tooemit을 계속 됩니다. 라이브 채널을 2시간 이상 이러한 상태로 두지 않는 것이 좋습니다. 그 외의 입력된 재연결 시 채널 hello hello 동작이 보장 되지는 않습니다, 응답 tooa 리셋 명령에서에서 해당 동작을 둘 다 합니다. Toostop hello 채널이 있을, 삭제 하 고 새로 만드십시오 됩니다.
* 연결 된 해당 프로그램이 실행 되는 또는 hello 입력된 hello 채널 프로토콜을 변경할 수 없습니다. 다른 프로토콜을 요청하는 경우 각각의 입력 프로토콜에 대한 개별 채널을 만들어야 합니다.
* Hello 라이브 인코더를 다시 구성할 때마다 호출 hello **재설정** hello 채널에서 메서드. Hello 채널을 다시 설정 하기 전에 toostop hello 프로그램을 해야 합니다. Hello 채널을 다시 설정한 후 hello 프로그램을 다시 시작 합니다.
* Hello 실행 상태에 hello 채널의 모든 프로그램을 중지 된 경우에 채널을 중지할 수 있습니다.
* 기본적으로 5 채널 tooyour 미디어 서비스 계정에만 추가할 수 있습니다. 이는 모든 새 계정에 대한 소프트 할당량입니다. 자세한 내용은 [할당량 및 제한 사항](media-services-quotas-and-limitations.md)을 참조하세요.
* 연결 된 해당 프로그램이 실행 되는 또는 hello 입력된 hello 채널 프로토콜을 변경할 수 없습니다. 다른 프로토콜을 요청하는 경우 각각의 입력 프로토콜에 대한 개별 채널을 만들어야 합니다.
* 채널 hello 중일 때만 청구 됩니다 **실행** 상태입니다. 자세한 내용은 참조 너무[이](media-services-manage-live-encoder-enabled-channels.md#states) 섹션.
* 현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다. 오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.
* Toohave hello toostream 콘텐츠 hello에 들어 있는 스트리밍 끝점이 있는지 확인 **실행** 상태입니다.
* Azure를 사용하여 여러 언어 트랙을 입력하고 라이브 인코딩을 수행할 때 RTP만은 다국어 입력에 지원됩니다. RTP를 통한 mpeg-2 TS를 사용 하 여 too8 오디오 스트림을를 정의할 수 있습니다. RTMP 또는 부드러운 스트리밍으로 여러 오디오 트랙을 수집하는 작업은 현재 지원되지 않습니다. 통한 라이브 인코딩을 수행할 때 [온-프레미스 라이브 인코딩합니다](media-services-live-streaming-with-onprem-encoders.md), 더 이상 처리 하지 않고 채널을 통해 전달 tooAMS 보내집니다 무엇이 든 때문에 이러한 제한이 않습니다.
* hello 인코딩 미리 설정 된 사용 하 여 hello 30fps의 "max 프레임 속도"의 개념입니다. 아니므로 hello 입력 60fps / 59.97i, hello 입력된 프레임 삭제/de-interlaced too30/29.97 fps 됩니다. Hello 입력 50 fps/50i 이면 hello 입력된 프레임 삭제/de-interlaced too25 fps은 없습니다. 25 fps hello 입력을 사용 하는 경우 출력 25 fps에 그대로 유지 됩니다.
* 완료 한 후에 tooSTOP 귀하가 채널을 잊지 마십시오. 그렇지 않으면 요금이 계속 청구됩니다.

## <a name="known-issues"></a>알려진 문제
* 채널 시작 시간이 향상 되어 tooan 평균 2 분 하지만 늘어난된 수요의 시간에 여전히 데 too20 + 분까지 걸릴 수 있습니다.
* RTP 지원은 전문 방송인을 위해 제공됩니다. RTP에 대 한 hello 메모를 검토 하십시오 [이](https://azure.microsoft.com/blog/2015/04/13/an-introduction-to-live-encoding-with-azure-media-services/) 블로그.
* 슬레이트 이미지를 설명 하는 toorestrictions 준수 해야 [여기](media-services-manage-live-encoder-enabled-channels.md#default_slate)합니다. 사용 하려는 경우 아웃 기본 슬레이트 보다 크면 1920 x 1080 hello 결국 요청 하는 오류를 표시 한 채널을 만듭니다.
* 다시 한 번... 완료 되 면 tooSTOP 귀하가 채널 반드시 스트리밍. 그렇지 않으면 요금이 계속 청구됩니다.

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>관련된 항목
[Azure 미디어 서비스를 사용하여 라이브 스트리밍 이벤트 제공](media-services-overview.md)

[단일 비트 전송률 tooadaptive 비트 전송률 스트림을 포털을 통한 라이브 인코딩을 수행 하는 채널 만들기](media-services-portal-creating-live-encoder-enabled-channel.md)

[단일 비트 전송률 tooadaptive 비트 전송률 스트림을.NET SDK와 라이브 인코딩을 수행 하는 채널 만들기](media-services-dotnet-creating-live-encoder-enabled-channel.md)

[REST API를 사용하여 채널 관리](https://docs.microsoft.com/rest/api/media/operations/channel)
 
[미디어 서비스 개념](media-services-concepts.md)

[Azure 미디어 서비스 조각화된 MP4 라이브 수집 사양](media-services-fmp4-live-ingest-overview.md)

[live-overview]: ./media/media-services-manage-live-encoder-enabled-channels/media-services-live-streaming-new.png

