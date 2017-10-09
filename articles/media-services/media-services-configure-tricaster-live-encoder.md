---
title: "aaaConfigure hello NewTek TriCaster 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello Tricaster 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Hello NewTek TriCaster 인코더 toosend 단일 비트 전송률 라이브 스트림 사용 하 여
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

이 항목에서는 방법을 tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널입니다. 자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.

이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다. 이 도구는 Windows PC에서만 실행됩니다. Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.

> [!NOTE]
> 에 대 한 기여도 보내기 위한 Tricaster를 사용 하 여 라이브 인코딩을 tooAMS 채널 피드 때에 있을 수 비디오/오디오 결함 라이브 이벤트 Tricaster 신속 하 게 피드, 사이 자르는 또는 슬레이트에서 전환 등의 특정 기능을 사용 하는 경우 . hello AMS 팀은 협력 그때까지 이러한 문제를 수정한 것이 좋지 toouse 이러한 기능입니다.
>
>

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

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. 채널 이름을 지정 hello 설명 필드는 선택 사항입니다. 채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다. 다른 모든 설정은 그대로 유지할 수 있습니다.

    있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.

3. **채널 만들기**를 클릭합니다.

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> hello 채널 toostart 20 분까지 걸릴 수 있습니다.
>
>

Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp)합니다.

> [!IMPORTANT]
> 채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다. 자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.
>
>

## <a id=configure_tricaster_rtmp></a>Hello NewTek TriCaster 인코더 구성
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
1. 사용 중인 비디오 입력 원본에 따라 새 **NewTek TriCaster** 프로젝트를 만듭니다.
2. 한 번 해당 프로젝트 내의 hello 찾을 **스트림** 단추를 클릭 한 hello 기어 아이콘 다음 tooit tooaccess hello 스트림 구성 메뉴를 클릭 합니다.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Hello 메뉴를 연 후 클릭 **새로** hello 연결 제목에서 합니다. Hello 연결 유형에 대 한 메시지가 나타나면 선택 **Adobe Flash**합니다.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. **확인**을 클릭합니다.
5. FMLE 프로필 hello 드롭다운 아래 화살표를 클릭 하 여 가져올 수 이제 **스트리밍 프로필** 너무 이동**찾아보기**합니다.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Toowhere 탐색 구성 hello FMLE 프로필을 저장 했습니다.
7. 선택한 다음 **확인**을 누릅니다.

    Hello 프로필 업로드 되 면 toohello 다음 단계를 진행 합니다.
8. 순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello Tricaster **RTMP 끝점**합니다.

    뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다. hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.

    Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Hello에이 정보를 붙여넣습니다 **위치** 아래 **플래시 서버** hello Tricaster 프로젝트 내에서. Hello에 스트림 이름을 할당할 수도 **스트림 ID** 필드입니다.

    스트림 정보 toohello FMLE 프로필에 추가한은 가져올 수를 클릭 하 여 toothis 섹션 **설정 가져오기**저장 toohello FMLE 프로필 탐색을 클릭 하 **확인**합니다. hello 관련 서버 플래시 필드 FMLE hello 정보로 채워야 합니다.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. 완료 되 면 클릭 **확인** hello hello 화면 맨 아래에 있습니다. Tricaster hello에 대 한 비디오 및 오디오 입력 준비 되 면 hello를 클릭 하 여 tooAMS 스트리밍을 시작 **스트림** 단추입니다.

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> 클릭 하기 전에 **스트림**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.
> 또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.
>
>

## <a name="test-playback"></a>테스트 재생
Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다. Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.

오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다. Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.  

## <a name="create-a-program"></a>프로그램 만들기
1. 채널 재생이 확인되면 프로그램을 만듭니다. Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
