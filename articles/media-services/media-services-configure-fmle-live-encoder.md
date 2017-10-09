---
title: "aaaConfigure hello FMLE 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello 플래시 미디어 라이브 인코더 (FMLE) 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Hello FMLE 인코더 toosend 단일 비트 전송률 라이브 스트림을 사용 하 여
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

이 항목에서는 방법을 tooconfigure hello [Media 라이브 인코더 플래시](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) 인코더 toosend 단일 비트 전송률 스트림 라이브 인코딩을 tooAMS 채널입니다. 자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.

이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다. 이 도구는 Windows PC에서만 실행됩니다. Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.

이 자습서에서는 AAC 사용에 대해 설명합니다. 그러나 FMLE는 AAC를 기본적으로 지원하지 않습니다. 해야 toopurchase AAC 인코딩에 대 한 플러그 인에서와 같이 MainConcept: [AAC 플러그 인](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

## <a name="prerequisites"></a>필수 조건
* [Azure Media Services 계정 만들기](media-services-portal-create-account.md)
* 실행 중인 스트리밍 끝점이 있는지 확인합니다. 자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)
* 최신 버전의 hello hello 설치 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구입니다.
* Hello 도구를 시작 하 고 tooyour AMS 계정을 연결 합니다.

## <a name="tips"></a>팁
* 가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.
* 바람직한 방법은 대역폭 요구 사항을 결정할 때는 toodouble hello 비트 전송률 스트리밍입니다. 필수 요구 사항이 없을 때 네트워크 정체가 발생 hello 영향을 완화 데 도움이 됩니다.
* 소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.

## <a name="create-a-channel"></a>채널 만들기
1. Hello AMSE 도구에서 toohello 이동 **Live** 탭을 hello 채널 영역 내에서 마우스 오른쪽 단추로 클릭 합니다. 메뉴에서 **Create channel...** hello 메뉴에서 합니다.

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. 채널 이름을 지정 hello 설명 필드는 선택 사항입니다. 채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다. 다른 모든 설정은 그대로 유지할 수 있습니다.

    있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.

3. **채널 만들기**를 클릭합니다.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> hello 채널 toostart 20 분까지 걸릴 수 있습니다.
>
>

Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp)합니다.

> [!IMPORTANT]
> 채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다. 자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.
>
>

## <a id=configure_fmle_rtmp></a>Hello FMLE 인코더 구성
이 자습서 hello에 다음 출력 설정이 사용 됩니다. 이 섹션의 hello 나머지 구성 단계를 자세히 설명합니다.

**비디오**:

* 코덱: H.264
* 프로필: 높음(수준 4.0)
* 비트 전송률: 5,000kbps
* 키 프레임: 2초(60초)
* 프레임 속도: 30

**오디오**:

* 코덱: AAC(LC)
* 비트 전송률: 192kbps
* 샘플 속도: 44.1khz

### <a name="configuration-steps"></a>구성 단계
1. Toohello 플래시 미디어 라이브 인코더의 (FMLE)에 사용 되는 hello 컴퓨터에 대 한 인터페이스를 이동 합니다.

    hello 인터페이스는 설정의 기본 페이지 하나 있습니다. 권장 하는 hello 다음의 참고 설정 tooget FMLE를 사용 하 여 시작 합니다.

   * 형식: H.264 프레임 속도: 30.00
   * 입력 크기: 1280 x 720
   * 비트 전송률: 5,000kbps(네트워크 제한 사항에 따라 조정 가능)  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     사용 하 여 소스 인터레이스된 경우 확인 표시가 hello "" 디인터레이스 옵션 하세요.
2. 선택 hello 렌치 아이콘 다음 tooFormat, 이러한 추가 설정을 구성 해야 합니다.

   * 프로필: 기본
   * 수준: 4.0
   * 키 프레임 빈도: 2초

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. 중요 한 오디오 설정에 따라 hello를 설정 합니다.

   * 형식: AAC
   * 샘플 속도: 44,100hz
   * 비트 전송률: 192kbps

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. 순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello FMLE의 **RTMP 끝점**합니다.

    뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다. hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.

    Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Hello에이 정보를 붙여넣습니다 **FMS URL** 필드 hello 출력 섹션과 스트림 이름 할당 합니다.

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    추가 중복성을 위해 hello 보조 입력 URL로 다음이 단계를 반복 합니다.
6. **연결**을 선택합니다.

> [!IMPORTANT]
> 클릭 하기 전에 **연결**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.
> 또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.
>
>

## <a name="test-playback"></a>테스트 재생

Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다. Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.

오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다. Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.  

## <a name="create-a-program"></a>프로그램 만들기
1. 채널 재생이 확인되면 프로그램을 만듭니다. Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. Hello 프로그램 이름을 지정 하 고 필요한 경우 조정 hello **보관 창 길이** (기본값 too4 시간 어떤). 저장소 위치를 지정 하거나 hello 기본값으로 그대로 둡니다 수도 있습니다.  
3. Hello 확인 **시작 hello 프로그램 이제** 상자입니다.
4. **프로그램 만들기**를 클릭합니다.  

    >[!NOTE]
    >프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.
        
5. Hello 프로그램이 실행 되 면 hello 프로그램 마우스 오른쪽 단추로 클릭 하 고 너무 탐색 하 여 재생을 확인**재생 hello 프로그램이** 다음를 선택 하 고 **Azure Media player**합니다.  
6. 확인 하 고 나면 hello 프로그램을 다시 클릭 마우스 오른쪽 단추로 선택한 **hello 출력 URL tooClipboard 복사** (hello에서이 정보를 검색 하거나 **프로그램 정보 및 설정을** hello 메뉴에서 옵션).

분산된 tooan 대상 그룹에 대 한 라이브 보기 또는 hello 스트림 준비 toobe는 플레이어에 포함 되었습니다.  

## <a name="troubleshooting"></a>문제 해결
Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
