---
title: "aaaConfigure hello Telestream Wirecast 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello Wirecast 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Hello Wirecast 인코더 toosend 단일 비트 전송률 라이브 스트림을 사용 하 여
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

이 항목에서는 방법을 tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널입니다.  자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.

이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다. 이 도구는 Windows PC에서만 실행됩니다. Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.

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

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. 채널 이름을 지정 hello 설명 필드는 선택 사항입니다. 채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다. 다른 모든 설정은 그대로 유지할 수 있습니다.

    있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.

3. **채널 만들기**를 클릭합니다.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> hello 채널 toostart 20 분까지 걸릴 수 있습니다.
>
>

Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp)합니다.

> [!IMPORTANT]
> 채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다. 자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.
>
>

## <a id=configure_wirecast_rtmp></a>Hello Telestream Wirecast 인코더 구성
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
1. RTMP 스트리밍에 대 한 설정 및을 사용 하는 hello 컴퓨터 있는 것에 hello Telestream Wirecast 응용 프로그램을 엽니다.
2. Hello 출력 toohello 이동 하 여 구성 **출력** 탭을 선택 하 고 **출력 설정...** .

    있는지 hello 확인 **출력 대상** 너무 설정**RTMP 서버**합니다.
3. **확인**을 클릭합니다.
4. Hello 설정 페이지에서 설정 hello **대상** 필드 toobe **Azure 미디어 서비스**합니다.

    hello 인코딩 프로필은 너무 미리 선택**Azure H.264 720 p 16:9 (1280x720)**합니다. toocustomize 이러한 설정은 선택 hello 기어 아이콘 toohello hello 오른쪽의 드롭다운을 선택한 후 **새 사전 설정**합니다.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. 인코더 기본 설정을 구성합니다.

    이름 hello 미리 설정 하 고 hello 다음 권장 되는 설정에 대 한 확인 합니다.

    **비디오**

   * 인코더: MainConcept H.264
   * 초당 프레임 수: 30
   * 평균 비트 전송률: 5000kbps(네트워크 제한 사항에 따라 조정 가능)
   * 프로필: 기본
   * 키 프레임 간격: 60프레임

    **오디오**

   * 대상 비트 전송률: 192kbps
   * 샘플 속도: 44.100kHz

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. **저장**을 누릅니다.

    hello Encoding 필드가 선택할 수 있는 새로 만든 hello 프로필이 되었습니다.

    새 프로필 hello 선택 되어 있는지 확인 합니다.
7. 순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello Wirecast **RTMP 끝점**합니다.

    뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다. hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.

    Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. Wirecast hello에 **출력 설정** 창 hello에이 정보를 붙여넣습니다 **주소** 필드 hello 출력 섹션과 스트림 이름 할당 합니다.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. **확인**을 선택합니다.
2. 주 hello에 **Wirecast** 화면에서 비디오 및 오디오 준비에 대 한 입력된 소스를 확인 한 다음 **스트림** hello 왼쪽 위 모서리에서 합니다.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> 클릭 하기 전에 **스트림**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.
> 또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.
>
>

## <a name="test-playback"></a>테스트 재생

Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다. Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.

오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다. Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.  

## <a name="create-a-program"></a>프로그램 만들기
1. 채널 재생이 확인되면 프로그램을 만듭니다. Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
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
