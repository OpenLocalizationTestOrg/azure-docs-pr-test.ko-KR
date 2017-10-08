---
title: "aaaDelivering 콘텐츠 toocustomers | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스를 사용하여 콘텐츠를 배달하는데 필요한 항목을 간략히 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>콘텐츠 toocustomers를 제공 합니다.
스트리밍 또는 주문형 비디오 콘텐츠 toocustomers를 제공 하 고, 다양 한 네트워크 조건에서 toodeliver 고품질 비디오 toovarious 장치가 목표가입니다.

tooachieve이이 목표를 수행할 수 있습니다.

* 스트림 tooa 비디오 스트림을 다중 비트 전송률 (적응 비트 전송률)으로 인코딩하십시오. 이렇게 하면 품질 및 네트워크 상태가 관리됩니다.
* Microsoft Azure 미디어 서비스를 사용 하 여 [동적 패키징](media-services-dynamic-packaging-overview.md) toodynamically 다시 패키지할 스트림을 서로 다른 프로토콜입니다. 이렇게 하면 여러 장치의 스트리밍이 관리됩니다. 미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술 뒤의 배달을 지원: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

이 문서에서는 중요한 콘텐츠 배달 개념에 대해 간략하게 설명합니다.

알려진 문제, toocheck 참조 [알려진 문제](media-services-deliver-content-overview.md#known-issues)합니다.

## <a name="dynamic-packaging"></a>동적 패키징
Hello 동적 패키징을 사용 해당 미디어 서비스 제공, (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 지 원하는 형식 스트리밍을에서 적응 비트 전송률 MP4 또는 부드러운 스트리밍으로 인코딩 콘텐츠를 배달할 수 있습니다에 toore 패키지 필요 없이 이러한 스트리밍 형식입니다. 동적 패키징을 사용하여 콘텐츠를 전달하는 것이 좋습니다.

tootake 이점은 동적 패키징을 tooencode 중 2 층 (원본) 파일에 필요한 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합이 있습니다.

동적 패키징을 사용을 저장 하 고 hello 단일 저장소 형식의 파일에 대 한 비용을 지불 합니다. 미디어 서비스 빌드하고 사용자 요청에 따라 hello 적절 한 응답을 제공 합니다.

동적 패키징은 표준 및 프리미엄 스트리밍 끝점에 사용할 수 있습니다. 

자세한 내용은 [동적 패키징](media-services-dynamic-packaging-overview.md)을 참조하세요.

## <a name="filters-and-dynamic-manifests"></a>필터 및 동적 매니페스트
미디어 서비스를 사용하여 자산에 대한 필터를 정의할 수 있습니다. 이러한 필터는 확인할 수 있어 고객 비디오의 특정 섹션을 재생 하는 등 작업을 수행 하거나 고객 장치 (hello 자산에 연결 된 모든 hello 변환 하는 대신 처리할 수 있는 오디오 및 비디오 변환의 하위 집합을 지정 하는 서버 쪽 규칙 ). 이 필터링을 통해 얻습니다 *동적 매니페스트* 고객 요청 toostream 하나를 기반으로 하는 비디오 또는 이상의 필터를 지정 하는 경우 만들어집니다.

자세한 내용은 [필터 및 동적 매니페스트](media-services-dynamic-manifest-overview.md)를 참조하세요.

## <a name="locators"></a>로케이터
tooprovide 사용자 콘텐츠를 다운로드 하거나 toostream 사용된 될 수 있는 url 먼저 toopublish 자산 로케이터를 만들어 합니다. 로케이터는 자산에 포함 된 파일 항목이 지점 tooaccess hello를 제공 합니다. Media Services는 두 가지 유형의 로케이터를 지원합니다.

* OnDemandOrigin 로케이터. 이러한 열 사용된 toostream 미디어 (예를 들어, MPEG DASH, HLS 또는 부드러운 스트리밍)는 데이터 나 점진적으로 파일을 다운로드 합니다.
* SAS(공유 액세스 서명) URL 로케이터. 이들은 사용된 toodownload 미디어 파일 tooyour 로컬 컴퓨터입니다.

*액세스 정책* 가 사용 되는 toodefine hello 권한 (예: 읽기, 쓰기 및 목록)을 클라이언트의 특정 자산에 대 한 권한과 액세스 기간입니다. 참고 hello 나열 권한 (AccessPermissions.List)을 OrDemandOrigin 로케이터를 만들에서 사용할 해야 합니다.

로케이터에는 만료 날짜가 있습니다. Azure 포털 hello 만료 날짜를 설정 100 년 hello에 이후 로케이터에 대 한 합니다.

> [!NOTE]
> 2015 년 3 월 이전에 Azure 포털 toocreate 로케이터는 hello를 사용 하는 경우 이러한 로케이터는 2 년이 지나면 tooexpire를 설정 되었습니다.
> 
> 

만료 날짜를 사용 하 여 로케이터는 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) Api입니다. SAS 로케이터의 hello 만료 날짜를 업데이트 하면 hello URL 변경 되는지 note 합니다.

로케이터는 없는 toomanage 사용자별 액세스 제어를 설계 합니다. 디지털 Rights Management (DRM) 솔루션을 사용 하 여 서로 다른 액세스 권한을 tooindividual 가진 사용자가 제공할 수 있습니다. 자세한 내용은 [미디어 보안 설정](http://msdn.microsoft.com/library/azure/dn282272.aspx)을 참조하세요.

Locator를 만들 때 Azure 저장소의 저장소 및 전파 프로세스 toorequired 인해 30 초 간 지연이 있을 수 있습니다.

## <a name="adaptive-streaming"></a>적응 스트리밍
적응 비트 전송률 기술을 toodetermine 네트워크 상태 비디오 플레이어 응용 프로그램을 허용 하 고 여러 비트 전송률에서 선택 합니다. 네트워크 통신 저하 hello 클라이언트 재생 더 낮은 비디오 품질 계속 될 수 있도록 더 낮은 비트 전송률을 선택할 수 있습니다. 네트워크 상태가 개선 hello 클라이언트 tooa 비디오 품질이 향상된 된 더 높은 비트 전송률로 전환할 수 있습니다. Azure 미디어 서비스는 hello 다음 적응 비트 전송률 기술을 지원: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.

스트리밍 Url이 포함 된 사용자가 tooprovide를 먼저 만들어야 OnDemandOrigin 로케이터 합니다. Hello hello 콘텐츠를 포함 하는 기본 경로 toohello 자산 hello 로케이터에서는 만들기 toostream을 원하는 합니다. 그러나 toobe 수 toostream이 콘텐츠 toomodify 나중에이 경로 필요 합니다. 스트리밍 매니페스트 파일 전체 URL toohello, hello 로케이터 경로 연결 해야 tooconstruct 값과 hello 매니페스트 (filename.ism) 파일 이름입니다. 다음 추가 **/manifest** 와 적절 한 형식 (필요한 경우) toohello 로케이터 경로입니다.

> [!NOTE]
> SSL 연결을 통해 콘텐츠를 스트리밍할 수도 있습니다. toodo이를 HTTPS로 스트리밍 Url 시작 되었는지 확인 합니다. 현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.  
> 


스트리밍 끝점 콘텐츠를 배달 하는 hello 2014 년 9 월 10 일 이후에 만들어진 경우에 SSL을 통해 스트리밍할 수 있습니다. Hello URL에 "streaming.mediaservices.windows.net" 스트리밍 Url hello 스트리밍 끝점이 2014 년 9 월 10 일 이후에 작성을 기반으로 하는 경우 "Origin.mediaservices.windows.net" (이전 형식 hello)를 포함 하는 스트리밍 Url에서 SSL을 지원 하지 않습니다. URL이 이전 형식인 hello toobe 수 toostream SSL을 통해 원하는 경우 새 스트리밍 끝점을 만듭니다. 새 SSL을 통해 끝점 toostream 콘텐츠 스트리밍 hello에 따라 Url을 사용 합니다.

## <a name="streaming-url-formats"></a>스트리밍 URL 형식
### <a name="mpeg-dash-format"></a>MPEG-DASH 형식
{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Apple HLS(HTTP 라이브 스트리밍) V4 형식
{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Apple HLS(HTTP 라이브 스트리밍) V3 형식
{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>오디오 전용 필터로 Apple HTTP 라이브 스트리밍(HLS) 포맷
기본적으로 오디오 전용 트랙 HLS 매니페스트 hello에 포함 됩니다. 셀룰러 네트워크에 대한 Apple 스토어 인증이 필요합니다. 이 경우에 클라이언트가 대역폭이 충분 하지 않습니다 2g 연결을 통해 연결 된 경우 재생 tooaudio 전용 전환 합니다. 버퍼링 기능이 없으면 스트리밍 tookeep 콘텐츠 않아도 되지만 화면이 표시 되지 않습니다. 일부 시나리오에서 오디오 전용 화면보다는 어느 정도 버퍼링이 발생하는 것이 나을 수도 있습니다. Tooremove hello 오디오 전용 추적 하려는 경우 추가 **오디오 전용 = false** toohello URL입니다.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

자세한 내용은 [동적 매니페스트 컴퍼지션 지원 및 HLS 출력 추가 기능](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)을 참조하세요.

### <a name="smooth-streaming-format"></a>부드러운 스트리밍 형식
{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

예제:

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>부드러운 스트리밍 2.0 매니페스트(레거시 매니페스트)
기본적으로 부드러운 스트리밍 매니페스트 형식 hello 반복 태그 (r 태그)를 포함합니다. 그러나 일부 플레이어는 hello r 태그를 지원 하지 않습니다. 이러한 플레이어에는 클라이언트 hello r 태그를 사용 하지 않는 형식을 사용할 수 있습니다.:

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>점진적 다운로드
점진적 다운로드를 hello 전체 파일이 다운로드 되기 전에 미디어 재생을 시작할 수 있습니다. .ism*(ismv, isma, ismt, ismc) 파일을 점진적으로 다운로드할 수 없습니다.

tooprogressively 콘텐츠를 다운로드할 hello OnDemandOrigin 로케이터 종류에 사용 합니다. hello 다음 예제는 hello 유형의 OnDemandOrigin 로케이터를 기반으로 하는 hello URL.

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

모든 저장소 암호화 된 자산 toostream 점진적 다운로드에 대 한 hello origin 서비스에서 원하는 암호를 해독 해야 합니다.

## <a name="download"></a>다운로드
toodownload 콘텐츠 tooa 클라이언트 장치에서 SAS 로케이터를 작성 해야 합니다. hello SAS 로케이터에서는 파일에 위치한 toohello Azure 저장소 컨테이너에 액세스 합니다. hello 호스트와 SAS 서명 사이 tooembed hello 파일 이름이 있는 toobuild hello 다운로드 URL입니다.

hello 다음 예제는 hello SAS 로케이터를 기반으로 하는 hello URL.

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

hello 고려 사항에 따라 적용 됩니다.

* 모든 저장소 암호화 된 자산 toostream 점진적 다운로드에 대 한 hello origin 서비스에서 원하는 암호를 해독 해야 합니다.
* 12시간 안에 완료되지 않은 다운로드는 실패합니다.

## <a name="streaming-endpoints"></a>스트리밍 끝점

스트리밍 끝점 tooa 클라이언트 플레이어 응용 프로그램이 나 tooa CDN 콘텐츠 배달 네트워크 ()에 대 한 추가 배포 직접 콘텐츠를 배달할 수 있는 스트리밍 서비스를 나타냅니다. 스트리밍 끝점 서비스 hello 아웃 바운드 스트림은 라이브 스트림 또는 미디어 서비스 계정의 주문형 비디오 자산을 수 있습니다. 스트리밍 끝점 유형으로는 **표준** 및 **프리미엄** 두 가지가 있습니다. 자세한 내용은 [스트리밍 끝점 개요](media-services-streaming-endpoints-overview.md)를 참조하세요.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

## <a name="known-issues"></a>알려진 문제
### <a name="changes-toosmooth-streaming-manifest-version"></a>변경 내용 tooSmooth 스트리밍 매니페스트 버전
매니페스트 자산 미디어 인코더 표준, 미디어 인코더 프리미엄 워크플로 또는 hello 동적 패키징-부드러운 스트리밍 hello를 사용 하 여 스트리밍 되었습니다 이전 Azure 미디어 인코더에서 생성 하는 경우-2016 년 7 월 서비스 릴리스의 hello 반환 되기 전에 준수 tooversion 2.0입니다. 버전 2.0에서는 hello 조각 기간 hello 소위 반복 ('r') 태그를 사용 하지 마십시오. 예:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

2016 년 7 월 서비스 릴리스의 hello, 생성 된 hello 부드러운 스트리밍 매니페스트의 반복 태그를 사용 하 여 조각 기간와 tooversion 2.2를 준수 합니다. 예:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Hello 레거시 부드러운 스트리밍 클라이언트 중 일부가 hello 반복 태그를 지원 하지 않을 수 있습니다 및 tooload hello 매니페스트 실패 합니다. toomitigate이 문제를 hello 레거시 매니페스트 형식 매개 변수를 사용할 수 **(형식 = fmp4 v20)** 또는 프로그램 클라이언트 toohello 최신를 지 원하는 버전을 반복 하는 태그를 업데이트 합니다. 자세한 내용은 [부드러운 스트리밍 2.0](media-services-deliver-content-overview.md#fmp4_v20)을 참조하세요.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>관련된 항목
[저장소 키를 롤링 후 미디어 서비스 로케이터를 업데이트합니다.](media-services-roll-storage-access-keys.md)

