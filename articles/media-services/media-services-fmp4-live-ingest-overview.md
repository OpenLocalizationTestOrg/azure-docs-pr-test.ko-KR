---
title: "aaaAzure 미디어 서비스 라이브 조각난된 MP4 수집 사양 | Microsoft Docs"
description: "이 사양은 hello 프로토콜 및 조각난된 MP4 기반 라이브 스트리밍 수집 Azure 미디어 서비스에 대 한 형식을 설명합니다. Azure 미디어 서비스 toostream 라이브 이벤트를 사용할 수 있으며 hello 클라우드 플랫폼으로 Azure를 사용 하 여 실시간에서 콘텐츠 브로드캐스트 수 있습니다. 이 문서에서는 매우 중복되고 강력한 라이브 수집 메커니즘을 구축하는 모범 사례도 다룹니다."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 43fac263-a5ea-44af-8dd5-cc88e423b4de
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 0c191f8d6c5a595621feaba0e571fb984b666f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-fragmented-mp4-live-ingest-specification"></a>Azure Media Services 조각화된 MP4 라이브 수집 사양
이 사양은 hello 프로토콜 및 조각난된 MP4 기반 라이브 스트리밍 수집 Azure 미디어 서비스에 대 한 형식을 설명합니다. 미디어 서비스 라이브 스트리밍 서비스로 고객 toostream 라이브 이벤트를 사용 하 고 hello 클라우드 플랫폼으로 Azure를 사용 하 여 실시간에서 콘텐츠 브로드캐스트할 수를 제공 합니다. 이 문서에서는 매우 중복되고 강력한 라이브 수집 메커니즘을 구축하는 모범 사례도 다룹니다.

## <a name="1-conformance-notation"></a>1. 적합성 표기
"권장", "가능", 및이 문서의 "OPTIONAL"는 해야만에 설명 된 대로 해석 toobe는 hello 키워드 "해야," "하지 않아야," "REQUIRED,", "은 NOT", "해서는 안" 되어서는 안, "입니다.

## <a name="2-service-diagram"></a>2. 서비스 다이어그램
hello 다음 그림에 hello의 상위 수준 아키텍처 hello 라이브 스트리밍 미디어 서비스의 서비스:

1. 라이브 인코더 hello Azure Media Services SDK를 통해 생성 되 고 사용자를 프로 비전 하는 라이브 피드 toochannels를 푸시합니다.
2. 채널, 프로그램 및 스트리밍 끝점에서 미디어 서비스 핸들 모든 hello 라이브 스트리밍 기능을 수집, 형식 지정, DVR, 보안, 확장성 및 중복성 클라우드입니다.
3. 필요에 따라 고객 toodeploy hello 스트리밍 끝점 및 hello 클라이언트 끝점 사이의 프로그램 Azure 콘텐츠 배달 네트워크 계층을 선택할 수 있습니다.
4. 클라이언트 hello HTTP 적응 스트리밍 프로토콜을 사용 하 여 스트리밍 끝점에서에서 끝점 스트림. 예로 Microsoft 부드러운 스트리밍, HTTP를 통한 동적 적응 스트리밍(DASH 또는 MPEG-DASH) 및 Apple HLS(HTTP 라이브 스트리밍)가 있습니다.

![수집 흐름][image1]

## <a name="3-bitstream-format--iso-14496-12-fragmented-mp4"></a>3. 비트스트림 형식 - ISO 14496-12 조각화된 MP4
hello 통신 형식 수집 라이브 스트리밍에 대 한 설명에서이 문서는 [14496-12]를 기반 합니다. 주문형 비디오 파일 및 라이브 스트리밍 수집 모두에 대한 조각화된 MP4 형식 및 확장에 대한 자세한 내용은 [[MS-SSTR]](http://msdn.microsoft.com/library/ff469518.aspx)을 참조하세요.

### <a name="live-ingest-format-definitions"></a>라이브 수집 형식 정의
hello 다음 목록은 toolive 적용 되는 정의가 Azure 미디어 서비스에 수집 하는 특수 형식.

1. hello **ftyp**, **서버 매니페스트 상자 라이브**, 및 **moov** 상자 (HTTP POST) 각 요청과 함께 보내야 합니다. Hello 스트림의 hello 시작 부분에서 이러한 상자 전송 되어야 하 고 수집 하는 언제 든 지 hello 인코더 tooresume 스트림에 다시 연결 해야 합니다. 자세한 내용은 [1]의 섹션 6을 참조하세요.
2. [1]의 섹션 3.3.2는 라이브 수집용 **StreamManifestBox**라는 옵션 상자를 설명합니다. Toohello hello Azure 부하 분산 장치 라우팅 논리를 인해이 상자를 사용 하는 사용 되지 않습니다. hello 상자 미디어 서비스에 수집 시 표시 되지 않아야 합니다. 이 상자가 표시되는 경우 Media Services는 자동으로 이를 무시합니다.
3. hello **TrackFragmentExtendedHeaderBox** 상자에 [1] 3.2.3.2에 정의 된 각 조각에 대 한 있어야 합니다.
4. 버전 2의 hello **TrackFragmentExtendedHeaderBox** 상자에는 여러 데이터 센터에서 동일한 Url이 있는 미디어 세그먼트를 사용 하는 toogenerate 되어야 합니다. hello 조각 인덱스 필드 인덱스 기반 스트리밍 형식 Apple HLS 등의 데이터 센터 간 장애 조치에는 REQUIRED 및 인덱스 기반 MPEG DASH는입니다. tooenable 데이터 센터 간 장애 조치 hello 조각 인덱스 여러 인코더에서 동기화 해야 하 고 인코더 다시 시작 또는 오류 간에 각 연속 미디어 조각에 대 한 1 씩 증가 합니다.
5. 섹션 3.3.6 [1] 정의 라는 상자 **MovieFragmentRandomAccessBox** (**mfra**) 라이브 수집 tooindicate 스트림의 끝 (EOS) toohello 채널의 hello 끝에 전송 될 수 있습니다. 기한 toohello EOS를 사용 하는 더 이상 hello 미디어 서비스의 논리를 수집 **mfra** 라이브 수집 보내지 않아야에 대 한 상자입니다. 전송한 경우 Media Services는 자동으로 이를 무시합니다. tooreset hello 상태의 hello 지점 수집, 사용 하는 것이 좋습니다 [채널 재설정](https://docs.microsoft.com/rest/api/media/operations/channel#reset_channels)합니다. 사용 하는 것이 좋습니다 [프로그램 중지](https://msdn.microsoft.com/library/azure/dn783463.aspx#stop_programs) tooend 프레젠테이션 및 스트림 합니다.
6. hello MP4 조각 시간을 일정 해야 hello 클라이언트 매니페스트 tooreduce hello 크기입니다. 상수 MP4 조각 기간에는 반복 태그의 hello 사용을 통해 클라이언트 다운로드 추론 향상 됩니다. hello 기간 정수가 아닌 프레임 속도 대 한 toocompensate를 변동 될 수 있습니다.
7. hello MP4 조각 기간 약 2-6 초 사이 여야 합니다.
8. MP4 조각 타임스탬프 및 인덱스(**TrackFragmentExtendedHeaderBox** `fragment_ absolute_ time` 및 `fragment_index`)는 오름차순으로 도착해야 합니다. 미디어 서비스 탄력적 tooduplicate 조각 이지만, toohello 미디어 타임 라인에 따라 기능 tooreorder 조각 제한적입니다.

## <a name="4-protocol-format--http"></a>4. 프로토콜 형식 – HTTP
ISO 조각난 MP4 기반 라이브 미디어 서비스는 표준 장기 실행 HTTP POST 요청 tootransmit 인코딩된 미디어 데이터 조각난된 MP4 형식 toohello 서비스에서 패키지에서 사용 하 여 수집 합니다. 각 HTTP POST 보냅니다 전체 조각난 MP4 bitstream ("stream") 헤더 상자와 hello 시작 부분에서 시작 (**ftyp**, **서버 매니페스트 상자 라이브**, 및 **moov** 상자) 조각 시퀀스를 계속 하 고 (**moof** 및 **인식 되지** 상자). Hello HTTP POST 요청에 대 한 URL 구문에 대 한 섹션을 참조 9.2 [1]입니다. Hello 게시 URL의 예는. 

    http://customer.channel.mediaservices.windows.net/ingest.isml/streams(720p)

### <a name="requirements"></a>요구 사항
Hello 자세한 요구 사항은 다음과 같습니다.

1. hello 인코더 시작할지은 빈 HTTP POST 요청을 전송 하 여 브로드캐스팅 hello "body" (콘텐츠 길이가 0)를 사용 하 여 hello 동일한 수집 URL입니다. 이 hello 라이브 수집 끝점 유효 하며 인증이 또는 필요한 기타 조건 있을 경우 신속 하 게 감지 하는 hello 인코더를 수 있습니다. 각 HTTP 프로토콜 hello 서버 없습니다 다시 보낼 HTTP 응답 hello hello POST 본문을 포함 하는 전체 요청을 받을 때까지 합니다. 이 단계에서는 hello 인코더 하지 않고 라이브 이벤트의 hello 장기 실행 특성을 지정 된 아닐 수 있습니다 수 toodetect 오류 모든 hello 데이터를 보내기 완료 될 때까지.
2. hello 인코더 (1)로 인해 오류 또는 인증 문제를 처리 해야 합니다. (1)이(가) 200 응답에 성공하면 계속합니다.
3. hello 인코더 hello 조각난 MP4 스트림을 사용 하 여 새 HTTP POST 요청을 시작 해야 합니다. hello 페이로드 hello 헤더 상자 뒤에 조각의로 시작 해야 합니다. 해당 hello 참고 **ftyp**, **서버 매니페스트 상자 라이브**, 및 **moov** hello 인코더 때문에 다시 연결 해야 하는 경우에이 순서에 따라이 상자 각 요청과 함께 전송 해야 hello 이전 요청에는 이전 toohello hello 스트림 끝에 종료 되었습니다. 
4. hello 인코더는 청크 분할된 전송 업로드에 대 한 인코딩을 사용 하 여, 불가능 한 toopredict hello 전체의 콘텐츠 길이 hello 있기 때문에 라이브 이벤트 해야 합니다.
5. Hello 마지막 조각의 보낸 후 hello 이벤트를 움직일 때 hello 인코더 hello 청크 분할 전송 인코딩 (대부분 HTTP 클라이언트 스택에 것을 자동으로 처리) 하는 메시지 시퀀스를 정상적으로 종료 해야 합니다. hello 인코더는 hello 서비스 tooreturn hello 최종 응답 코드에 대 한 대기 하 고 hello 연결을 종료 해야 합니다. 
6. hello를 사용 하는 hello 인코더 해서는 안 `Events()` 를 미디어 서비스 라이브 수집에 대 한 9.2에 [1]에 설명 된 대로 명사.
7. Hello HTTP POST 요청을 종료 하거나 시간 초과 hello 스트림의 TCP 오류 이전 toohello 끝과 hello 인코더 새 연결을 사용 하 여 새 POST 요청을 실행 하며 수행 하는 경우에 앞의 요구 사항을 hello 합니다. 또한 hello 인코더 hello hello 스트림의 각 추적에 대 한 이전 두 MP4 조각을 다시 전송 하 고 hello 미디어 타임 라인에서 불연속성을 도입 하지 않고 다시 시작 해야 합니다. 각 추적에 대 한 마지막 두 개의 MP4 조각을 hello를 다시 보내는 등 어떤 데이터도 손실 되는지 확인 합니다. 즉, 스트림을 오디오와 비디오 트랙을 포함 하는 경우 POST 요청을 현재 hello 오류가 발생 하면 hello 인코더 다시 연결 해야 하 고 resend hello 오디오 트랙에 대 한 이전에 성공적으로 전송 된, 마지막 두 개의 조각을 hello와 hello 마지막 두 개의 조각을 대 한 hello 비디오 트랙을 이전에 성공적으로 전송 된, 데이터 손실도 없고 tooensure입니다. hello 인코더 다시 연결 하는 경우 다시 보내기 미디어 조각의 "앞 으로" 버퍼를 유지 해야 합니다.

## <a name="5-timescale"></a>5. 시간 간격
[[MS SSTR] ](https://msdn.microsoft.com/library/ff469518.aspx) hello 사용법에 대 한 시간 간격을 **SmoothStreamingMedia** (단원 2.2.2.1) **StreamElement** (단원 2.2.2.3) **StreamFragmentElement**(2.2.2.6 섹션) 및 **LiveSMIL** (2.2.7.3.1 섹션). Hello 시간 간격 값 없으면 hello 사용 되는 기본값이 10000000 (10 MHz)입니다. 대부분의 인코더 구현에서는이 기본값을 사용할 hello 부드러운 스트리밍 형식 지정 다른 시간 간격 값의 사용을 차단 하지 않습니다, 하지만 값 (10 MHz) toogenerate 부드러운 스트리밍 데이터를 수집 합니다. 기한 toohello [Azure 미디어 동적 패키징](media-services-dynamic-packaging-overview.md) 기능, 권장 오디오 스트림에 대 한 비디오 스트림 및 44.1 k h z 또는 48.1 KHz 90 KHz 표시줄을 사용 합니다. 다양 한 스트림에 사용 되는 서로 다른 시간 간격 값, hello 스트림 수준 시간 간격을 전송 되어야 합니다. 자세한 내용은 [[MS-SSTR]](https://msdn.microsoft.com/library/ff469518.aspx)을 참조하세요.     

## <a name="6-definition-of-stream"></a>6. “스트림”의 정의
스트림이 hello 기본 단위 연산의 실시간 프레젠테이션을 작성에 대 한 라이브 수집 스트리밍 장애 조치 및 중복성 시나리오를 처리 합니다. 스트림은 단일 트랙 또는 여러 트랙을 포함할 수 있는 하나의 고유한 조각화된 MP4 비트스트림으로 정의됩니다. 전체 라이브 프레젠테이션의 hello 라이브 인코더의 hello 구성에 따라 하나 이상의 스트림을 포함 될 수 있습니다. 예제 따르는 hello 프레젠테이션을 전체 라이브 스트림을 toocompose를 사용 하 여 다양 한 옵션을 보여 줍니다.

**예제:** 

고객이 toocreate hello 오디오/비디오 비트 전송률 다음을 포함 하는 라이브 스트리밍 프레젠테이션은:

비디오 - 3000kbps, 1500kbps, 750kbps

오디오 - 128kbps

### <a name="option-1-all-tracks-in-one-stream"></a>옵션 1: 모든 트랙을 하나의 스트림에
이 옵션에서는 단일 인코더가 모든 오디오/비디오 트랙을 생성한 다음 하나의 조각화된 MP4 비트스트림으로 번들화합니다. hello 조각난 MP4 bitstream 단일 HTTP POST 연결을 통해 전송 됩니다. 이 예제에서는 이 라이브 프레젠테이션에 스트림이 하나만 존재합니다.

![스트림 - 한 트랙][image2]

### <a name="option-2-each-track-in-a-separate-stream"></a>옵션 2: 각각의 트랙을 별도의 스트림에
이 옵션에서는 hello 인코더 각 MP4 조각 bitstream에 한 트랙을 넣고 별도 HTTP 연결을 통해 모든 hello 스트림 게시 됩니다. 이는 하나 이상의 인코더로 수행할 수 있습니다. hello 라이브 수집 4 개의 스트림 구성 처럼이 라이브 프레젠테이션의 볼 수 있습니다.

![스트림 - 별도 트랙][image3]

### <a name="option-3-bundle-audio-track-with-hello-lowest-bitrate-video-track-into-one-stream"></a>옵션 3: 하나의 스트림으로 오디오 트랙 hello 가장 낮은 비트 전송률 비디오 트랙으로 번들
이 옵션을 hello 고객이 toobundle hello 오디오 MP4 조각 하나의 bitstream에서 가장 낮은 비트 전송률 비디오 트랙 hello와 추적 및 leave hello 별개의 스트림으로 다른 두 개의 비디오 트랙을 선택 합니다. 

![스트림 - 오디오 및 비디오 트랙][image4]

### <a name="summary"></a>요약
이는 이 예제에서 가능한 모든 수집 옵션의 완벽한 목록은 아닙니다. 사실상 어떤 트랙을 스트림에 그룹화하는 것은 라이브 수집에서 지원됩니다. 고객 및 인코더 공급 업체는 엔지니어링 복잡성, 인코더 용량 및 중복성과 장애 조치 고려 사항에 따라 고유한 구현을 선택할 수 있습니다. 그러나 대부분의 경우, 즉 전체 라이브 프레젠테이션의 hello에 대 한 오디오 트랙을 하나만 있습니다. 따라서의 중요 한 tooensure hello healthiness hello의 hello 오디오 트랙을 포함 하는 스트림을 수집 합니다. Hello 오디오 트랙 (옵션 2)에서 같이 자체 스트림에 배치 하거나 (옵션 3)에서 같이 hello 비트 전송률이 가장 낮은 비디오 트랙으로 번들이 고려 종종 발생 합니다. 또한, 더 나은 중복과 내결함성을 위해 보내는 hello 두 개의 스트림 (중복 오디오 트랙으로 옵션 2)에 동일한 오디오 트랙 또는 번들 hello 오디오 트랙 (옵션 3 시에 번들로 묶이는 오디오와 hello 비트 전송률이 가장 낮은 비디오 트랙의 두 개 이상 있는 최소 두 개의 비디오 스트림)이 가장 좋습니다에 대 한 라이브 미디어 서비스에 수집 합니다.

## <a name="7-service-failover"></a>7. 서비스 장애 조치(failover)
라이브 스트리밍을의 hello 특성을 지정한 좋은 장애 조치 지원을 hello hello 서비스 가용성 보장 중요 합니다. 미디어 서비스 다양 한 유형의 실패, 네트워크 오류, 서버 오류 및 저장소 문제를 포함 하 여 디자인 된 toohandle 됩니다. Hello 라이브 인코더에서에서 적절 한 장애 조치 논리와 함께 사용할 경우 고객 hello 클라우드에서 항상 신뢰할 수 있는 라이브 스트리밍 서비스로 달성할 수 있습니다.

이 섹션에서는 서비스 장애 조치(failover) 시나리오를 설명합니다. 네트워크 오류로 하기도 hello 오류 hello 서비스 내에서 어딘가에 발생이 경우 합니다. 다음은 서비스 장애를 처리 하기 위한 hello 인코더 구현에 대 한 몇 가지 권장 사항입니다.

1. Hello TCP 연결을 설정 하는 데 10 초 제한 시간을 사용 합니다. Hello 작업을 중단 하는 시도 tooestablish hello 연결 10 초 보다 더 오래 걸리면, 다시 시도 하십시오. 
2. Hello HTTP 요청 메시지 청크를 보내기 위한 짧은 제한 시간을 사용 합니다. N 초 hello 대상 MP4 조각 지속 시간을 사용 하는 경우 사용 하 여 N과 2 N 초 간의 전송 시간 초과 예를 들어 6 초 hello MP4 조각 기간을 사용 하는 경우 6 too12 초 제한 시간을 사용 합니다. 시간 초과가 발생 하는 경우 재설정 hello 연결, 새 연결 열기 및 resume 스트림 hello 새 연결에 대해 수집 합니다. 
3. Hello 마지막 두 개의 조각이 각 추적에 대 한 완전히 및 성공적으로 보낸 toohello 서비스를 포함 하는 롤링 버퍼를 유지 합니다.  스트림에 대 한 HTTP POST 요청 hello 종료 되거나 제한 시간이 초과 이전 toohello hello 스트림 끝을 하는 경우 새 연결을 열거나 및 다른 HTTP POST 요청을 시작, hello 스트림 헤더를 다시 보낼, 각 추적에 대 한 마지막 두 조각의 hello를 다시 보냅니다 및 다시 시작 없이 hello 스트림 hello 미디어 타임 라인에서 불연속성을 소개 합니다. 이렇게 하면 hello 데이터 손실 가능성이 줄어듭니다.
4. 해당 hello 인코더 hello 재시도 tooestablish 연결 수를 제한 하거나 스트리밍 TCP 오류가 발생 한 후 다시 시작 하지 않는 것이 좋습니다.
5. TCP 오류 후:
  
    a. 현재 연결 hello 해야 닫히고 새 HTTP POST 요청에 대 한 새 연결을 만들어야 합니다.

    b. 새 HTTP POST URL 해야 하는 hello hello 초기 게시 URL hello와 동일 합니다.
  
    c. hello 새 HTTP POST 헤더를 포함 해야 스트림 (**ftyp**, **서버 매니페스트 상자 라이브**, 및 **moov** 상자) 하는 동일한 toohello 스트림 헤더 hello에 POST를 초기 합니다.
  
    d. 각 추적에 대 한 전송 hello 마지막 두 개의 조각이 다시 보내야, 및 스트리밍 불연속성 hello 미디어 타임 라인에는 위험 없이 재개 해야 합니다. hello MP4 조각 타임 스탬프 HTTP POST 요청 간에 계속 해 서 증가 해야 합니다.
6. hello 인코더 hello MP4 조각 작업 기간에 비례하여 속도로 데이터는 전송 되지 않을 경우 hello HTTP POST 요청을 종료 해야 합니다.  데이터를 보내지 않습니다 하는 HTTP POST 요청은 서비스 업데이트의 hello 이벤트의 hello 인코더에서 신속 하 게 연결 끊기에서 미디어 서비스를 방지할 수 있습니다. 이러한 이유로 hello에 대 한 HTTP POST 스파스 (광고 신호)를 추적 해야 단기 hello 스파스 조각 전송 되는 즉시 종료 합니다.

## <a name="8-encoder-failover"></a>8. 인코더 장애 조치(failover)
인코더 장애 조치는 hello 두 번째 종류의 종단 간 라이브 스트리밍 배달에 대 한 toobe 해결 해야 하는 장애 조치 시나리오입니다. 이 시나리오에서는 hello 인코더 쪽 hello 오류 조건이 발생합니다. 

![인코더 장애 조치(failover)][image5]

hello 기대 다음 인코더 장애 조치 하는 경우 hello 라이브 수집 끝점에서 적용 됩니다.

1. 새 인코더 인스턴스 만들어야 toocontinue 스트리밍 그림과 같이 hello (3000 k에 파선이 있는 비디오에 대 한 스트림) 합니다.
2. hello 새 인코더 해야 사용 하 여 hello 동일한 URL을 HTTP POST 요청으로 hello 인스턴스 실패 했습니다.
3. hello 새 인코더의 POST 요청에 포함 되어야 hello 실패 한 인스턴스 hello으로 MP4 헤더 상자 조각화 동일 합니다.
4. hello 동일한 라이브 프레젠테이션의 toogenerate 동기화 정렬 된 조각 경계와 오디오/비디오 샘플에 대 한 hello 새 인코더 실행 중인 다른 모든 인코더와 제대로 동기화 해야 합니다.
5. hello 새 스트림이 hello 이전 스트림을 사용 하 여 의미는 동일 해야 합니다. 및 hello 헤더 및 조각 수준에서 사용이 가능 합니다.
6. 새 인코더 hello toominimize 데이터 손실을 시도해 보십시오. hello `fragment_absolute_time` 및 `fragment_index` hello 지점 hello 인코더 마지막 중지 위치에서 미디어 조각을 증가 해야 합니다. hello `fragment_absolute_time` 및 `fragment_index` 는 지속적으로 증가 해야 하지만 것이 허용 가능한 toointroduce 불연속성, 필요한 경우. 미디어 서비스는 hello 미디어 타임 라인에서 toointroduce 불연속 보다 조각을 다시 보내는 등의 hello 측에 더 나은 tooerr 되기 때문 수신 및 처리 하 고, 이미에 조각의 무시 합니다. 

## <a name="9-encoder-redundancy"></a>9. 인코더 중복성
중요 한 라이브 있는지 요구 더 높은 가용성 및 환경의 품질 것이 좋습니다 데이터 손실 없이 활성-활성 중복 인코더 tooachieve 원활한 장애 조치를 사용 하는 이벤트입니다.

![인코더 중복성][image6]

이 다이어그램에 볼 수 있듯이, 인코더의 두 그룹 푸시 각 스트림에의 두 복사본이 동시에 hello 라이브 서비스입니다. 이 설정은 Media Services가 중복된 조각을 스트림 ID와 조각 타임스탬프에 따라 필터링할 수 있기 때문에 지원됩니다. 결과 라이브 스트림을 hello 및 보관 파일이 hello 두 소스의 hello 최상의 가능한 집계 하는 모든 hello 스트림의 단일 복사본입니다. 예를 들어 가상 극단적인 경우에는 하나의 인코더 (없어도 toobe hello 동일한 하나)으로 특정 시점에 실행 각 스트림에 대해 hello hello 서비스에서 라이브 스트림을 결과 연속 데이터 손실 없이 합니다. 

이 시나리오에 대 한 hello 요구 사항 거의 동일 hello "인코더 장애 조치" 경우에서 hello 요구 사항으로 hello, 인코더의 두 번째 집합 hello hello에서 실행 되는 hello 예외와 동일한 기본 인코더 hello 된 표준 시간입니다.

## <a name="10-service-redundancy"></a>10. 서비스 중복성
경우에 따라 중복성이 뛰어나고 글로벌 배포에 대 한 지역 간 백업 toohandle 국가별 재해를 있어야 합니다. Hello "인코더 중복" 토폴로지를 확장 고객이 선택할 수 toohave 중복 서비스 배포 인코더의 두 번째 집합 hello와 연결 된 다른 지역에 있습니다. 또한 고객 작업 수 콘텐츠 배달 네트워크 공급자 toodeploy hello 두 서비스 배포 tooseamlessly 경로 클라이언트 트래픽 앞에 전역 트래픽 관리자를 사용 합니다. hello hello 인코더에 대 한 요건은 hello "인코더 중복" 대/소문자 hello와 동일 합니다. hello만 예외는 hello 두 번째 집합이 인코더 요구 toobe 다른 tooa 실시간 가리키고 수집 끝점입니다. hello 다음 그림에이 설치:

![서비스 중복성][image7]

## <a name="11-special-types-of-ingestion-formats"></a>11. 수집 형식의 특수한 유형
이 섹션에는 특정 시나리오에 맞춰 디자인된 toohandle 있는 라이브 수집 형식의 특별 한 형식을 설명 합니다.

### <a name="sparse-track"></a>스파스 트랙
리치 클라이언트 시각적 효과를 라이브 스트리밍 프레젠테이션의 서비스를 제공 하 종종 필요한 tootransmit 시간 동기화 이벤트 또는 hello 주 미디어 데이터와는 별도로에 신호를 보냅니다. 동적 라이브 광고 삽입이 하나의 예입니다. 이벤트 신호 보내기의 이 유형은 스파스 특성 때문에 일반적인 오디오/비디오 스트리밍과 다릅니다. 데이터 일반적으로 계속 해 서 발생 하지 않는 및 hello 간격은 하드 toopredict 수 신호 hello 즉, 스파스 트랙의 hello 개념은 설계 된 tooingest 브로드캐스트 밴드 신호 데이터.

hello 다음 단계는 스파스 트랙을 수집 하는 방법에 대 한 권장된 구현.

1. 오디오/비디오 트랙 없이 스파스 트랙만 포함하는 별도의 조각화된 MP4 비트스트림을 생성합니다.
2. Hello에 **서버 매니페스트 상자 라이브** hello를 사용 하 여에 정의 된 대로 섹션 6에 [1]의 *parentTrackName* hello 부모 트랙의 매개 변수 toospecify hello 이름입니다. 자세한 내용은 [1]의 섹션 4.2.1.2.1.2를 참조하세요.
3. Hello에 **서버 매니페스트 상자 라이브**, **manifestOutput** 너무 설정 되어 있어야**true**합니다.
4. 이벤트 신호를 보내는 hello의 hello 스파스 특성에 지정 된 경우 hello 다음을 좋습니다.
   
    a. Hello 라이브 이벤트의 hello 맨 hello 인코더 hello 클라이언트 매니페스트에 hello 서비스 tooregister hello 스파스 트랙 수 있는 toohello 서비스 hello 초기 헤더 상자를 보냅니다.
   
    b. 데이터가 전송 되지 않으므로 때 hello 인코더 hello HTTP POST 요청을 종료 해야 합니다. 데이터를 보내지 않는 장기 실행 HTTP POST 서비스 업데이트 또는 서버 재부팅 hello 이벤트의 hello 인코더에서 신속 하 게 연결 끊기에서 미디어 서비스를 방지할 수 있습니다. 이러한 경우 hello 미디어 서버 hello 소켓에서 수신 작업에서 일시적으로 차단 됩니다.
   
    c. 데이터를 신호 없는 경우 사용할 수 없는 hello 시간 동안 hello 인코더 hello HTTP POST 요청을 닫아야 합니다. Hello POST 요청이 활성 상태인 동안 hello 인코더 데이터를 보내야 합니다.

    d. 스파스 조각을 보낼 때 hello 인코더 사용 가능한 경우 명시적 콘텐츠 길이 헤더를 설정할 수 있습니다.

    e. 새 연결 된 스파스 조각을 보낼 때 hello 인코더 뒤에 새 조각을 hello hello 헤더 상자에서 보내기 시작 해야 합니다. 사이, 발생 하는 장애 조치의 경우 이것이 hello 새 스파스 연결 하기 전에 hello 스파스 트랙 찾을 수 없습니다. 설정 된 tooa 새 서버 되 고 있습니다.

    f. hello 스파스 트랙 조각 hello 해당 부모 트랙 조각 값을 같거나 더 큰 타임 스탬프 값이 사용 가능한 toohello 클라이언트 만들어질 때 사용할 수 있는 toohello 클라이언트 됩니다. 예를 들어 hello 스파스 조각에는 t의 타임 스탬프 = 1000, 하는 hello 클라이언트 "비디오" ("비디오" hello 부모 트랙 이름 라고 가정함) 조각 1000 타임 스탬프 또는 beyond, 다운로드할 수를 표시 한 후 hello 스파스 조각 t 것으로 예상 = 1000입니다. 실제 신호 hello는 지정 된 용도 대 한 hello 프레젠테이션 타임 라인에서 다른 위치에 대해 사용할 수 있습니다. 이 예제에서는 t의 스파스 조각 hello 가능한의 = 1000의 위치를 몇 초 후에 광고를 삽입 하는 데 사용 되는 XML 페이로드는 나중에 있습니다.

    g. 스파스 트랙 조각의 hello 페이로드 hello 시나리오에 따라 서로 다른 형식 (예: XML, 텍스트 또는 이진) 될 수 있습니다.

### <a name="redundant-audio-track"></a>중복 오디오 트랙
일반적인 HTTP 적응 스트리밍 시나리오 (예: 부드러운 스트리밍 또는 대시) 종종, 즉 hello 전체 프레젠테이션에서 오디오 트랙을 하나만 있습니다. 오류 조건에에서 클라이언트 toochoose hello에 대 한 여러 품질 수준이 있는 비디오 트랙 달리 hello 오디오 트랙 hello hello 오디오 트랙을 포함 하는 hello 스트림의 수집 중단 된 단일 실패 지점이 수 있습니다. 

이 문제를 미디어 서비스 지원 toosolve 라이브 중복 오디오 트랙의 수집 합니다. hello 개념은 해당 hello 동일한 오디오 트랙 다양 한 스트림에 여러 번 보낼 수 있습니다. Hello 서비스만 등록 hello 오디오 트랙 한 번 hello 클라이언트 매니페스트에 있지만 사용할 수 있습니다 중복 오디오 트랙으로 백업 hello 주 오디오 트랙에 문제가 오디오 조각을 검색에 대 한 합니다. 중복 오디오 트랙 tooingest hello 인코더를 해야합니다.

1. 여러 조각 MP4 bitstreams에에서 동일한 오디오 트랙 hello를 만듭니다. hello 중복 오디오 트랙 의미론적으로 동일 해야, hello로 동일 타임 스탬프를 조각화 하 고 hello 헤더 및 조각 수준에서 서로 바꿔 사용할 합니다.
2. 해당 hello "오디오" 항목을 확인 hello에 라이브 서버 매니페스트 ([1] 섹션 6)은 hello 동일 중복 오디오 트랙에 대 한 합니다.

구현은 다음 hello 중복 오디오 트랙에 대 한 것이 좋습니다.

1. 하나의 스트림에서 자체적으로 고유한 각 오디오 트랙을 전송합니다. 또한 이러한 오디오 트랙 스트림의 여기서 두 번째 스트림의 hello와 다른 hello에서 먼저 hello HTTP POST URL에서에서 hello 식별자로만 각각에 대해 중복 스트림을 보낼: {프로토콜}:// {서버 주소} / {지점 path}/Streams({identifier}) 게시 합니다.
2. 별도 스트림을 toosend hello 두 개의 가장 낮은 비디오 비트 전송률을 사용 합니다. 이 스트림 각각은 각 고유한 오디오 트랙 각각의 복사본도 포함해야 합니다. 예를 들어, 여러 언어가 지원되는 경우 이 스트림은 각 언어에 대한 오디오 트랙을 포함해야 합니다.
3. 별도 서버 (인코더) 인스턴스 tooencode를 사용 하 고에 언급 된 hello 중복 스트림 (1) 및 (2)를 보냅니다. 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[image1]: ./media/media-services-fmp4-live-ingest-overview/media-services-image1.png
[image2]: ./media/media-services-fmp4-live-ingest-overview/media-services-image2.png
[image3]: ./media/media-services-fmp4-live-ingest-overview/media-services-image3.png
[image4]: ./media/media-services-fmp4-live-ingest-overview/media-services-image4.png
[image5]: ./media/media-services-fmp4-live-ingest-overview/media-services-image5.png
[image6]: ./media/media-services-fmp4-live-ingest-overview/media-services-image6.png
[image7]: ./media/media-services-fmp4-live-ingest-overview/media-services-image7.png
