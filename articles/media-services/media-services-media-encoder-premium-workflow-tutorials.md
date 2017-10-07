---
title: "aaaAvanced 미디어 인코더 프리미엄 워크플로 자습서"
description: "이 문서 tooperform 고급 미디어 인코더 프리미엄 워크플로 작업 하는 방법을 보여 주는 연습이 포함 되어와 방법을 toocreate의 복잡 한 워크플로 워크플로 디자이너를 사용 합니다."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>고급 미디어 인코더 Premium 워크플로 자습서
## <a name="overview"></a>개요
이 문서에 보여 주는 연습이 포함 되어 방법을 사용 하는 toocustomize 워크플로 **워크플로 디자이너**합니다. Hello 실제 워크플로 파일을 찾을 수 [여기](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)합니다.  

## <a name="toc"></a>목차
hello 다음 항목에 설명 합니다.

* [단일 비트 전송률 MP4로 MXF 인코딩](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [새 워크플로 시작](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [미디어 파일 입력 hello를 사용 하 여](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [미디어 스트림 검사](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [MP4 파일 생성을 위해 비디오 인코더 추가](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Hello 오디오 스트림 인코딩](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Hello MP4 파일 쓰기](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Hello 출력 파일에서 미디어 서비스 자산 만들기](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [테스트 hello 로컬로 워크플로 완료 했습니다.](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [다중 비트 전송률 MP4로 MXF 인코딩 - 동적 패키징 사용](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [하나 이상의 추가 MP4 출력 추가](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [구성 hello 파일 출력 이름](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [별도 오디오 트랙 추가](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Hello를 추가 합니다. ISM SMIL 파일](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [워크플로 개요 tooenhance](#workflow-overview-to-enhance)
  * [파일 명명 규칙](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [게시에 hello 워크플로 루트 구성 요소 속성](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [게시된 속성 값을 사용하는 출력 파일 이름 생성](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [축소판 그림 toomultibitrate MP4 출력 추가](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [워크플로 개요 tooadd 미리 보기](#workflow-overview-to-add-thumbnails-to)
  * [JPG 인코딩 추가](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [색 공간 변환 처리](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [쓰기 hello 미리 보기](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [워크플로에서 오류 감지](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [완료된 워크플로](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [다중 비트 전송률 MP4 출력의 시간 기반 트리밍](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [워크플로 개요 toostart 트리밍을 추가 합니다.](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [스트림 트리머 hello를 사용 하 여](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [완료된 워크플로](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [스크립트 구성 요소를 hello 소개](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [워크플로 내의 스크립팅: Hello World](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [다중 비트 전송률 MP4 출력의 프레임 기반 트리밍](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [조정을 추가 개요 toostart 세부 계획](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Hello 클립 목록 XML을 사용 하 여](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [스크립트 구성 요소에서 hello 클립 목록을 수정](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [ClippingEnabled 편의 속성 추가](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>단일 비트 전송률 MP4로 MXF 인코딩
이 연습에서는 .MXF 입력 파일에서 AAC-HE 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일을 만듭니다.

### <a id="MXF_to_MP4_start_new"></a>새 워크플로 시작
워크플로 디자이너를 열고 "파일"-"새 작업 영역"-"청사진 트랜스코딩"을 선택합니다.

hello 새 워크플로 요소 3 개 표시 됩니다.

* 기본 원본 파일
* 클립 목록 XML
* 출력 파일/자산  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*새 인코딩 워크플로*

### <a id="MXF_to_MP4_with_file_input"></a>미디어 파일 입력 hello를 사용 하 여
순서 tooaccept에 쿼리하여 입력된 미디어 파일 하나으로 시작 미디어 파일 입력 구성 요소를 추가 합니다. 구성 요소 toohello 워크플로 tooadd hello 리포지토리 검색 상자에 검색할 끌어서 hello 디자이너 창에 놓을 hello 원하는 항목 합니다. 미디어 파일 입력 hello에 대 한이 작업을 수행 하 고 hello 미디어 파일 입력에서 hello 기본 소스 파일 구성 요소 toohello 파일 이름 입력된 핀을 연결 합니다.

![연결된 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*연결된 미디어 파일 입력*

다른 많은 실행 하기 전에 먼저 사용 해야 tooindicate toohello 워크플로 디자이너 어떤 샘플 파일 toouse toodesign 같은 우리의 워크플로와 합니다. 따라서 toodo hello 디자이너 창 배경을 클릭 하 고 hello 오른쪽 속성 창에서 hello 소스 파일을 기본 속성을 찾습니다. Hello 폴더 아이콘을 사용 하 여 원하는 선택 hello 파일 tootest hello 워크플로 클릭 합니다. 이 도구를 실행 하는 즉시 hello 미디어 파일 입력 구성 요소 되며 hello 파일을 검사 검사이 해당 출력 핀 tooreflect hello 파일을 채웁니다.

![채워진 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*채워진 미디어 파일 입력*

Toowork와 같은 입력 사항으로 지정 하는 동안 알 수 없습니다 아직 hello 인코딩된 출력 위치 이동 해야 합니다. 이제 기본 소스 파일 구성 된 유사한 toohow hello hello 바로 아래의 출력 폴더 변수 속성을 구성 합니다.

![구성된 입력 및 출력 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*구성된 입력 및 출력 속성*

### <a id="MXF_to_MP4_streams"></a>미디어 스트림 검사
종종 hello 스트림 그렇게 모양을 tooknow hello 워크플로 통해 흐르는 원하는입니다. tooinspect hello 워크플로에서 언제 든 지 스트림 출력 또는 입력된 핀 hello 구성 요소 중 하나를 클릭 하기만 됩니다. 이 경우의 미디어 파일 입력에서 hello 압축 되지 않은 비디오 출력 핀에 클릭 해 보십시오. 대화 상자가 열리고 tooinspect hello에 대 한 아웃 바운드 비디오 수 있도록 합니다.

![검사 hello 압축 되지 않은 비디오 출력 핀](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*검사 hello 압축 되지 않은 비디오 출력 핀*

이 경우에 예를 들어 거의 2분인 비디오의 4:2:2 샘플링에서 초 당 24프레임으로 1920x1080 입력을 사용하여 처리합니다.

### <a id="MXF_to_MP4_file_generation"></a>MP4 파일 생성을 위해 비디오 인코더 추가
이제 압축되지 않은 비디오 및 여러 압축되지 않은 오디오 출력 핀을 미디어 파일 입력에 사용할 수 있다는 점을 기억합니다. 순서 tooencode에서 인바운드 비디오 hello, 생성 하기 위한 인코딩 구성 요소-이 경우에 필요 합니다. MP4 파일입니다.

tooencode 비디오 스트림 tooH.264 hello, hello toohello 디자이너 화면 AVC 비디오 인코더 구성 요소를 추가 합니다. 이 구성 요소는 압축되지 않은 비디오 스트림을 입력으로 사용하고 AVC 압축된 비디오 스트림을 해당 출력 핀에 제공합니다.

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*연결되지 않은 AVC 인코더*

해당 속성 방법을 hello 인코딩 정확 하 게 발생 하는 결정 됩니다. 일부의 hello에 살펴봅시다 더 중요 한 설정:

* 출력 너비와 높이 출력: 이러한 hello 인코딩된 비디오의 hello 해상도 결정 합니다. 이 경우에 640x360로 결정하겠습니다.
* 프레임 속도: hello 소스 프레임 속도 채택 하는 집합 toopassthrough just 됩니다, 경우에 가능한 toooverride 하지만 있습니다. 이러한 프레임 속도 변환은 동작 보정할 수 없습니다.
* 프로필 및 수준: 이러한 hello AVC 프로필과 수준을 결정 합니다. tooconveniently 자세한 내용을 보려면 hello 다양 한 수준 및 프로필에 대 한 hello AVC 비디오 인코더 구성 요소에 대해 hello 물음표 아이콘을 클릭 한 hello 도움말 페이지에는 각 hello 수준에 대 한 자세한 정보 표시 됩니다. 이 샘플에서는 3.2 (hello 기본값) 수준에서 기본 프로필을 가진 해 보겠습니다.
* 전송률 제어 모드 및 비트 전송률(kbps): 이 시나리오에서는 1200kbps에서 상수 비트 전송률(CBR) 출력을 선택합니다.
* : 비디오이 형식은 hello hello H.264 스트림으로 작성 되려면 VUI (비디오 유용성 정보)에 대 한 (디코더 tooenhance hello 표시할 하지만 반드시 toocorrectly에서 사용할 수 있는 정보 디코드):
* NTSC(30fps를 사용하는 미국 또는 일본에 일반적임)
* PAL(25fps를 사용하는 유럽에 일반적임)
* GOP 크기 모드: 여기서는 닫힌 GOP로 키 간격이 2초인 고정된 GOP 크기를 구성합니다. 이렇게 하면 동적 패키징 Azure 미디어 서비스를 제공 하는 hello와의 호환성.

toofeed 우리의 AVC 인코더 hello 미디어 파일 입력 구성 요소 toohello 압축 되지 않은 비디오 입력된 핀 hello AVC 인코더에서에서 hello 압축 되지 않은 비디오 출력 핀을 연결 합니다.

![연결된 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*연결된 AVC 기본 인코더*

### <a id="MXF_to_MP4_audio"></a>Hello 오디오 스트림 인코딩
이 시점에서 인코딩된 비디오에서는 하지만 hello 원래 압축 되지 않은 오디오 스트림 여전히 toobe 압축 합니다. 이 대 한 AAC 인코더 (돌비) 구성 요소를 hello 하 여 인코딩을 AAC를 검토 합니다. Toohello 워크플로 추가 합니다.

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*연결되지 않은 AAC 인코더*

이제는 비 호환성: 오디오 스트림을 사용할 수 있는 압축 되지 않은 미디어 파일 입력 가능성이 hello 서로 다른 두 갖습니다 보다 더 많은 동안만 단일 압축 되지 않은 오디오 입력된 핀 hello AAC 인코더에서에서에: 왼쪽 오디오 채널 및 hello에 대 한 hello에 대 한 권한입니다. (서라운드 사운드를 처리하는 경우 6채널입니다.) 되므로 수 toodirectly hello 오디오 hello AAC 오디오 인코더에에 hello 미디어 파일 입력 원본에서 연결 합니다. hello AAC 구성 요소가 예상 이른바 "인터리브" 오디오 스트림을: 둘 다를 포함 하는 단일 스트림을 hello 서로 포함 되어 hello의 왼쪽 및 오른쪽 채널과 합니다. 소스 미디어 파일에서 알고 있으므로 오디오 트랙 hello 소스 어떤 위치에서 생성할 수 hello 사용 하 여 이러한 인터리브 오디오 스트림을 올바르게 할당 왼쪽 및 오른쪽에 대 한 스피커 위치 합니다.

먼저 하나 toogenerated hello 필요한 소스 오디오 채널에서 인터리빙된 된 스트림을 것이 좋습니다. hello 오디오 스트림 인터리브 구성 요소에이 처리 합니다. Toohello 워크플로 추가 하 고에 미디어 파일 입력 hello에서 hello 오디오 출력을 연결 합니다.

![연결된 오디오 스트림 인터리버](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*연결된 오디오 스트림 인터리버*

이제 인터리빙된 된 오디오 스트림을 했으므로 여전히 지정 하는 대신 tooassign hello 왼쪽 또는 오른쪽 스피커를 배치 하는 위치입니다. 이 toospecify 순서, hello 스피커 위치 Assigner 활용할 수 있습니다.

![스피커 위치 할당자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*스피커 위치 할당자 추가*

채널 "2.0 (L, R)"를 호출 하는 미리 설정 된 hello 및 인코더 사전 설정의 필터는 "Custom"를 통해 사용 하기 위해 스피커 위치 Assigner hello 스테레오 입력된 스트림을 사용 하 여 구성 합니다. (이 할당 hello 왼쪽된 스피커 위치 toochannel 1 및 2 hello 오른쪽 스피커 위치 toochannel 합니다.)

Hello AAC 인코더의 hello 스피커 위치 Assigner toohello 입력의 hello 출력에 연결 합니다. 그런 다음 hello AAC 인코더 toowork는 "2.0 (L, R)"를 입력으로 스테레오 오디오와 toodeal를 알 수 있도록 채널 미리 설정 합니다.

### <a id="MXF_to_MP4_audio_and_fideo"></a>MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱
AVC 인코딩된 비디오 스트림 및 AAC 인코딩된 오디오 스트림을 지정하여 둘 모두를 .MP4 컨테이너에 캡처할 수 있습니다. 단일는 다양 한 스트림 혼합의 hello 프로세스 "멀티플렉싱" (또는 "muxing") 라고 합니다. 이 경우 hello 오디오 및 일관 된 단일에서 비디오 스트림 hello 인터리빙 하는 것입니다. MP4 패키지입니다. hello 구성 요소에 대해이 조정 하는 합니다. MP4 컨테이너 ISO mpeg-4 멀티플렉서 hello를 라고 합니다. 하나의 toohello 디자이너 화면을 추가 하 고 hello AVC 비디오 인코더와 hello AAC 인코더 tooits 입력을 연결 합니다.

![연결된 MPEG4 멀티플렉서](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*연결된 MPEG4 멀티플렉서*

### <a id="MXF_to_MP4_writing_mp4"></a>Hello MP4 파일 쓰기
출력 파일을 작성할 때는 hello 출력 파일 구성 요소가 사용 됩니다. 출력 toodisk 작성 되려면 있도록 hello ISO mpeg-4 멀티플렉서의 toohello 출력을 연결할 수 있습니다. toodo이 hello 컨테이너 (mpeg-4) 출력 핀 toohello 쓰기 입력된 핀의 hello 파일 출력을 연결 합니다.

![연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*연결된 파일 출력*

사용 되는 hello filename hello 파일 속성 결정 됩니다. 가장 가능성이 높은 하나 tooset 합니다 해당 속성에는 하드 코드 된 tooa 값이 지정 될 수 있지만, 식을 통해 대신 합니다.

toohave hello 워크플로 hello 출력을 자동으로 결정 파일 이름 속성 식에서 hello 단추 다음 toohello 파일 이름을 클릭 합니다 (다음 toohello 폴더 아이콘). Hello에서 드롭다운 메뉴를 선택한 다음 "식"을 선택 합니다. 이 hello 식 편집기를 표시 합니다. 먼저 hello 내용을 hello 편집기의 선택을 취소 합니다.

![빈 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*빈 식 편집기*

hello 식 편집기를 사용 하면 tooenter 혼합 된 하나 이상의 변수, 리터럴 값입니다. 변수는 달러 기호로 시작합니다. Hello $ 키를 누르면 처럼 사용 가능한 변수를 선택할 드롭다운 상자 hello 편집기에 표시 됩니다. 여기서는 hello 출력 디렉터리 변수와 hello 기본 입력된 파일 이름 변수 사용:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![채워진 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*채워진 식 편집기*

> [!NOTE]
> Hello 식 편집기에서 값을 제공 해야, toosee 순서로 Azure에서 인코딩 작업의 출력 파일을 참조 하세요.
>
>

Hello 식 ok를 클릭 하 여 확인 하면 hello 속성 창은 미리 봅니다 toowhat 값 hello 파일 속성 확인을 시점에서.

![파일 식이 출력 dir 확인](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*파일 식이 출력 dir 확인*

### <a id="MXF_to_MP4_asset_from_output"></a>Hello 출력 파일에서 미디어 서비스 자산 만들기
Tooindicate 여전히 필요 MP4 출력 파일을 쓴 하는 동안이 워크플로 실행 한 결과로 생성 됩니다는 미디어 서비스 자산 출력 toohello이이 파일에 속해 있는지 합니다. toothis 끝나도 hello 출력 파일/자산 노드 hello 워크플로 캔버스에 사용 됩니다. 이 노드의에 들어오는 모든 파일 부분에서는 hello 결과 Azure 미디어 서비스 자산 생성 됩니다.

Hello 출력 파일 구성 요소 toohello 출력 파일/자산 구성 요소 toofinish hello 워크플로 연결 합니다.

![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*완료된 워크플로*

### <a id="MXF_to_MP4_test"></a>테스트 hello 로컬로 워크플로 완료 했습니다.
tootest hello 워크플로 로컬로 hello 위쪽에 hello 도구 모음에서 hello 재생 단추를 누릅니다. Hello 워크플로 실행을 완료 하는 경우 구성 하는 hello 출력 폴더에 생성 된 hello 출력을 검사 합니다. Hello 완료 hello MXF 입력된 소스 파일에서 인코딩된 MP4 출력 파일을 볼 수 있습니다.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>MP4로 MXF 인코딩 - 다중 비트 전송률 동적 패키징 사용
이 연습에서는 단일 .MXF 입력 파일에서 AAC 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일의 집합을 만듭니다.

때 Azure 미디어 서비스는 서로 다른 비트 전송률 및 해결 toobe 생성 해야 합니다 각 여러 GOP 정렬 MP4 파일에서 제공 하는 동적 패키징 기능 hello와 함께에서 사용 하기 위해 다중 비트 전송률 자산 출력 방법이 필요 합니다. toodo 따라서 hello [단일 비트 전송률 MP4에 인코딩 MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) 연습 좋은 출발점을 제공 합니다.

![워크플로 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*워크플로 시작*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>하나 이상의 추가 MP4 출력 추가
결과 Azure 미디어 서비스 자산의 모든 MP4 파일은 서로 다른 비트 전송률 및 해상도를 지원합니다. 하나 이상의 MP4 출력 파일 toohello 워크플로 추가 해 보겠습니다.

있는지 toomake 동일한 설정을 hello 우리의 비디오 인코더 사용 하 여 만든 모든, 가장 편리 하 게 tooduplicate 이미 기존 AVC 비디오 인코더 hello 및 해상도 비트 전송률의 다른 조합 구성 (추가해보겠습니다 960 x 540 중 하나에서 초당 25 프레임 2,5 Mbps)입니다. tooduplicate hello 기존 인코더 복사본에 붙여 hello 디자이너 화면입니다.

새 AVC 구성 요소에 미디어 파일 입력 hello hello 압축 되지 않은 비디오 출력 핀을 연결 합니다.

![연결된 두 번째 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*연결된 두 번째 AVC 인코더*

이제이 새 AVC 인코더 toooutput 960 x 540 2,5로 대 한 hello 구성을 활용 합니다. (여기에 해당 속성 "출력 너비", "출력 높이" 및 "비트 전송률(kbps)"을 사용합니다.)

지정 된 Azure 미디어 서비스 동적 패키징과 함께 toouse hello 결과 자산 원하는, 스트리밍 끝점 hello 필요한 toobe 정확 하 게 정렬 된 tooeach 다른 방식으로 HLS/조각난 MP4/DASH 조각의 이러한 MP4 파일에서 생성할 수 서로 다른 비트 전송률 간에 전환 하는 클라이언트는 단일 부드러운 연속 비디오 및 오디오 환경이 발생 합니다. toomake 발생 tooensure 두 AVC 인코더의 hello 속성, hello GOP ("그룹의 사진") 크기를 MP4 파일을 모두 설정 되어이 필요 하 여 변환을 수행할 수 있는 too2 초:

* hello GOP 크기 모드 tooFixed GOP 크기를 설정 하 고
* hello 키 프레임 간격 tootwo (초)입니다.
* hello GOP IDR 제어 tooClosed GOP tooensure 모든 GOP 대기 중입니다. 종속성 없이 자체에 설정

toomake 우리의 워크플로 편리한 toounderstand 너무 hello 첫 번째 AVC 인코더 이름 바꾸기 "AVC 비디오 인코더 640 x 360 1200 kbps" 두 번째 AVC 인코더 hello 및 "AVC 비디오 인코더 960 x 540 2500 kbps"입니다.

이제 두 번째 ISO MPEG-4 멀티플렉서 및 두 번째 파일 출력을 추가합니다. Hello 멀티플렉서 toohello 새 AVC 인코더를 연결 하 고 해당 결과 hello 파일 출력으로 전송 해야 합니다. 그런 다음 새 hello AAC 오디오 인코더 출력 toohello도 연결 멀티플렉서의 입력 합니다. hello 파일 출력 차례로 수 연결된 toohello 출력 파일/자산 노드 tooadd 것 toohello 미디어 서비스 자산으로 만들어집니다.

![두 번째 Muxer 및 연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*두 번째 Muxer 및 연결된 파일 출력*

Azure 미디어 서비스 동적 패키징 사용 호환성을 위해 hello 멀티플렉서의 청크 모드 tooGOP count 또는 기간을 구성 하 고 청크 too1 당 hello Gop를 설정 합니다. (Hello 기본 이어야 합니다.)

![Muxer 청크 모드](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Muxer 청크 모드*

참고: 수도 있습니다 toorepeat이이 프로세스 다른 비트 전송률 및 해상도 toohave 사용할 조합을 toohello 자산 출력을 추가 합니다.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>구성 hello 파일 출력 이름
둘 이상의 단일 파일에 추가 된 toohello 출력 자산을 개가 있습니다. 파일 이름의 각 hello에 대 한 출력 파일은 서로 다릅니다 및 미정도 적용 파일 명명 규칙 되므로 것을 알 수 hello 파일 이름에서으로 처리 하는 필요성 toomake 있는지 hello를 제공 합니다.

Hello 디자이너에서 식을 통해 파일 출력 이름 지정을 제어할 수 있습니다. Hello 출력 파일 구성 요소 중 하나에 대 한 hello 속성 창을 열고 hello 파일 속성에 대 한 hello 식 편집기를 엽니다. 다음 식은 hello를 통해 구성 된이 첫 번째 출력 파일 (hello 자습서에서 이동 하는 것에 대 한 참조 [MXF tooa 단일 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

즉, 우리의 파일 이름을 두 변수에 의해 결정 됩니다: hello 및를 출력 디렉터리 toowrite에 hello 소스 파일의 기본 이름입니다. hello 전자 hello 워크플로 루트를 속성으로 노출 됩니다 및 후자 hello hello 들어오는 파일에 의해 결정 됩니다. 로컬 테스트;에 대해 사용 하는 것이 hello 출력 디렉터리는 note 이 속성은 Azure 미디어 서비스에서 hello 클라우드 기반 미디어 프로세서에서 hello 워크플로가 실행 될 때 hello 워크플로 엔진에 의해 재정의 됩니다.
toogive 두 출력 파일 이름 지정 일관 된 출력을 변경 hello 명명 식을 첫 번째 파일:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

및를 두 번째로 hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Toomake MP4 출력 파일을 모두 올바르게 생성 되도록 실행 하는 중간 테스트를 실행 합니다.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>별도 오디오 트랙 추가
.Ism 파일 toogo MP4 출력 파일 생성 하는 경우 나중에 볼 수 있겠지만, 것도 필요 오디오 전용 MP4 파일을 hello 오디오 트랙으로 우리의 적응 스트리밍에 대 한 합니다. (ISO-mpeg-4 멀티플렉서) 추가 muxer toohello 워크플로 추가 toocreate이 파일을 연결 하 고 hello AAC 인코더 출력 핀 있는 해당 입력된 핀 트랙 1에 대 한 합니다.

![추가된 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*추가된 오디오 Muxer*

세 번째 파일 출력 구성 요소 toooutput hello 아웃 바운드 스트림은 hello muxer에서 만들고 hello 파일 명명 식으로 구성 합니다.

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![파일 출력을 생성하는 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*파일 출력을 생성하는 오디오 Muxer*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Hello를 추가 합니다. ISM SMIL 파일
Hello 동적 패키징 toowork 함께 두 MP4 파일 (및 오디오 전용 MP4 hello) 당사의 미디어 서비스 자산에도 필요 매니페스트 파일 ("SMIL" 파일이 라고도: 멀티미디어 Integration 언어 동기화). 이 파일 MP4 파일을 동적 패키징 및 hello 오디오 스트리밍에 대 한 이러한 tooconsider 중에 사용할 수 있는 tooAzure 미디어 서비스를 나타냅니다. 단일 오디오 스트림이 있는 MP4의 집합에 대한 일반적인 매니페스트 파일은 다음과 같습니다.

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

hello 개별 MP4 비디오 파일의 참조 tooeach switch 문 내에서 포함 된 hello.ism 파일 및 오디오 파일 toothose도 하나 이상의 tooan hello 오디오 포함 하는 MP4를 참조 하는 또한 합니다.

MP4의의 집합에 대 한 hello 매니페스트 파일을 생성 "AMS 매니페스트 Writer" hello 라는 구성 요소를 통해 수행할 수 있습니다. toouse, hello 화면으로 끌어 및 hello 세 개의 출력 파일 구성 요소 toohello 입력 AMS 매니페스트 기록기에서에서 hello "쓰기 완료" 출력 핀을 연결 합니다. Hello AMS 매니페스트 기록기 toohello 출력 파일/자산의 tooconnect hello 출력 있는지 확인 합니다.

이 다른 파일 출력 구성 요소와 마찬가지로 hello.ism 파일 출력 이름을 하는 식으로 구성 합니다.

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

완료 된 워크플로 hello 아래와 같습니다.

![완성 된 MXF toomultibitrate MP4 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*완성 된 MXF toomultibitrate MP4 워크플로*

## <a id="MXF_to__multibitrate_MP4"></a>다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진
Hello에 [이전 워크플로 연습](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) 어떻게 단일 MXF 입력된 자산으로 변환할 수 출력 자산을 다중 비트 전송률 MP4 파일, 오디오 전용 MP4 파일 매니페스트 파일을 Azure 미디어와 함께에서 사용 하 여 버퍼 오버런 서비스 동적 패키징입니다.

이 연습에서는 어떻게 hello 측면의 일부 향상 및 수 더 편리 표시 됩니다.

### <a id="MXF_to_multibitrate_MP4_overview"></a>워크플로 개요 tooenhance
![다중 비트 전송률 MP4 워크플로 tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*다중 비트 전송률 MP4 워크플로 tooenhance*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>파일 명명 규칙
Hello 이전 워크플로에서 출력 파일 이름을 생성 hello 기준으로 단순 식을 지정 합니다. 하지만 일부 중복 있는: hello hello 개별 출력 파일 구성 요소를 모두 지정 된 이러한 식입니다.

예를 들어 hello 첫 번째 비디오 파일에 대 한 파일 출력 구성 요소는이 식을 사용 하 여 구성 됩니다.

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

동안 hello 두 번째 출력에 비디오와 같은 식을 해야 합니다.

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

대신 이러한 중복을 제거하고 더 구성 가능하게 된다면 간결하며 오류가 발생할 가능성이 적고 더 편리해질 것입니다. 다행히을 활용해 서: hello 기능 toocreate 우리의 워크플로 루트에서 사용자 지정 속성을 조합 하 여 hello 디자이너의 식 기능 편의 추가 계층을 제공 합니다.

Hello 비트 전송률 MP4 파일을 개별 hello에서에서 드라이브 파일 이름 구성 하겠습니다 우리 가정해 보겠습니다. 이러한 비트 전송률 tooconfigure 하나의 중앙에서 항상 건강 합니다 (에 배치할 hello 그래프의 루트 우리의)에서 위치 액세스 tooconfigure 및 드라이브 파일 이름 생성 알게 됩니다. toodo이 hello AVC 인코더의 경우와 마찬가지로 모두 hello 루트에서 액세스할 수 있도록 두 AVC 인코더 toohello 루트 우리의 워크플로의 hello 비트 전송률 속성을 게시 하 여 시작 합니다. (두 개의 서로 다른 위치에 표시되는 경우에도 기본 값은 하나입니다.)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>게시에 hello 워크플로 루트 구성 요소 속성
첫 번째 AVC 인코더 hello를 열고 toohello 비트 전송률 (kbps) 속성이 이동 hello 드롭다운에서 게시를 선택 합니다.

![게시 hello 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*게시 hello 비트 전송률 속성*

Hello 구성 "1 비트 전송률 비디오"의 읽을 수 있는 표시 이름 및 "video1bitrate"의 게시 이름 대화 toopublish toohello 루트 우리의 워크플로 그래프의 게시 합니다. "비트 전송률 스트리밍"이라는 사용자 지정 그룹 이름을 구성하고 게시를 누릅니다.

![게시 hello 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*비트 전송률 속성에 게시 대화 상자*

반복 hello hello의 hello 비트 전송률 속성에 대해 동일 AVC 인코더의 두 번째 하 고 이름을 "video2bitrate" "2 비트 전송률 비디오"의 표시 이름으로, "비트 전송률 스트리밍" 사용자 지정 같은 그룹 hello에 있습니다.

에서는 이제 hello 워크플로 루트 속성을 검사, 사용자 지정 그룹을 표시 되는 두 개의 게시 속성 hello로를 살펴보겠습니다. 해당 AVC 인코더 비트 전송률의 hello 값을 반영 하는 둘 다 합니다.

![워크플로 루트에 게시된 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Tooaccess 코드 또는 식에서 이러한 속성을 원하는 때마다 다음과 같이 하겠습니다.

* hello 루트 바로 아래 구성 요소에서 인라인 코드 로부터: node.getPropertyAsString('.. / video1bitrate', null)
* 식 내에서: ${ROOT_video1bitrate}

우리의 오디오 트랙 비트 전송률에도 게시 하 여 hello "비트 전송률 스트리밍" 그룹을 완료 하겠습니다. Hello AAC 인코더의 hello 속성 내에서 hello 비트 전송률 설정에 대 한 검색 하 고 hello 드롭다운 다음 tooit에서 게시를 선택 합니다. 이름이 "audio1bitrate"를 사용 하 여 hello 그래프의 toohello 루트를 게시 하 고 표시 이름 "오디오 1 비트 전송률" "비트 전송률 스트리밍" 사용자 지정 그룹 내에서 키를 누릅니다.

![오디오 비트 전송률에 게시 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*오디오 비트 전송률에 게시 대화 상자*

![루트의 결과 비디오 및 오디오 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*루트의 결과 비디오 및 오디오 속성*

이러한 세 가지 중 하나를 변경 값도 다시 구성 되며 변경 내용이 hello hello 해당 구성 요소와 연결 된 값 (및에서 게시 된 경우).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>게시된 속성 값을 사용하는 출력 파일 이름 생성
하드 코딩 하는 대신이 생성 된 파일 이름을 변경할 수 있습니다 이제 각 hello 출력 파일 구성 요소 toorely hello 그래프 루트에 게시 된 뿐 우리 hello 비트 전송률 속성에서이 파일 이름 식입니다. 첫 번째 파일 출력을 hello 파일 속성을 찾을 hello 식을 다음과 같이 편집 합니다.

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

이 식에 다른 매개 변수 hello 액세스 하 고 hello 식 창에서 작업 하는 동안 hello 키보드 hello 달러 기호를 클릭 하 여 입력 한 수입니다. Hello 사용 가능한 매개 변수 중 하나는 우리의 video1bitrate 속성 이전에 게시입니다.

![식 내에서 매개 변수 액세스](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*식 내에서 매개 변수 액세스*

수행의 두 번째 비디오에 대 한 hello 파일 출력에 대 한 동일한 hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

및 hello 오디오 전용 파일 출력:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

이제 hello 비디오 또는 오디오 파일 중 하나에 대 한 hello 비트 전송률을 변경 하면 hello 각 인코더 다시 구성 됩니다 및 hello 비트 전송률 기반 파일 이름 규칙은 모두 자동으로 적용 됩니다.

## <a id="thumbnails_to__multibitrate_MP4"></a>축소판 그림 toomultibitrate MP4 출력 추가
생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것을 미리 보기 toohello 출력을 추가 하는 합니다.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>워크플로 개요 tooadd 미리 보기
![다중 비트 전송률 MP4 워크플로 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*다중 비트 전송률 MP4 워크플로 toostart*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>JPG 인코딩 추가
이 축소판 이미지 생성의 hello 핵심 hello JPG Encoder 구성 요소 수 toooutput JPG 파일 됩니다.

![JPG 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*JPG 인코더*

그러나 직접 우리의 압축 되지 않은 비디오 스트림 hello JPG 인코더에 미디어 파일 입력 hello에서 연결할 수 없습니다. 대신, toobe 전달 개별 프레임 필요 합니다. 이 hello 비디오 프레임 게이트 구성 요소를 통해 수행할 수 있습니다.

![연결 프레임 게이트 toohello JPG 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*연결 프레임 게이트 toohello JPG 인코더*

게이트 프레임 hello 사용 하면 비디오 프레임 toopass 모든 너무 많은 시간 (초) 또는 프레임 되 면 합니다. hello 간격 및 hello 이런 있는 오프셋 시간은 hello 속성에서 구성 가능 합니다.

![비디오 프레임 게이트 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*비디오 프레임 게이트 속성*

Hello 모드 tooTime (초)을 설정 하 여 미리 보기 1 분 마다 만들기 하 고 간격 too60 hello 살펴보겠습니다.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>색 공간 변환 처리
논리 것 모두 hello 프레임 게이트와 hello 미디어 파일 입력의 압축 되지 않은 비디오 핀 이제 연결 될 수 있습니다, 그리고 우리 대기줄 경고에서는 작업을 수행 합니다.

![입력 색 공간 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*입력 색 공간 오류*

즉, 어떤 컬러 정보가 표시 됩니다는 원래 원시 압축 되지 않은 비디오 스트림의 우리의 MXF에서 들어오는 hello 방법은 JPG 인코더에 필요 하지만 어떤 hello에서 달라 집니다. tooflow 예상은 특히는 소위 "색 공간"의 "RGB" 또는 "회색" 더 합니다. 즉, 해당 hello 비디오 프레임 게이트의 인바운드 비디오 스트림 toohave는 색 공간에 대 한이 먼저 적용 변환 해야 합니다.

Hello 워크플로 hello 색 공간 변환기-Intel 끌고 tooour 프레임 게이트를 연결 합니다.

![색 공간 변환 연결](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*색 공간 변환 연결*

Hello 속성 창에서 hello BGR 24 항목 hello 사전 설정 목록에서 선택 합니다.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>쓰기 hello 미리 보기
우리의 MP4 비디오에서 다른, hello 파일 하나 이상 JPG 인코더 구성 요소 출력 됩니다. 이 순서 toodeal에서 장면 검색 JPG 파일 기록기 구성 요소를 사용할 수 있습니다: 들어오는 hello JPG 미리 보기를 수행 하 고 여러 되 고 그 뒤에 각 파일 이름으로 작성 합니다. (일반적으로 hello hello 스트림 hello 축소판 그림의에서 시간 (초) / 단위 수를 나타내는 hello 숫자에서 출발 했습니다.)

![장면 검색 JPG 파일 기록기 용 hello 소개](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*장면 검색 JPG 파일 기록기 용 hello 소개*

Hello 식을 사용 하 여 hello 출력 폴더 경로 속성 구성: ${ROOT_outputWriteDirectory}

및 파일 이름 접두사 속성을 hello:

    ${ROOT_sourceFileBaseName}_thumb_

hello 접두사 hello 축소판 파일은 이름이 지정 되 고 방식을 결정 합니다. Hello 스트림 내의 위치를 숫자 나타내는 hello 엄지 것은 붙어야 합니다.

![장면 검색 JPG 파일 기록기 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*장면 검색 JPG 파일 기록기 속성*

Hello 장면 검색 JPG 파일 기록기 용 toohello 출력 파일/자산 노드를 연결 합니다.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>워크플로에서 오류 감지
Hello 색 공간 변환기 toohello 원시 압축 되지 않은 비디오 출력의 hello 입력을 연결 합니다. 이제 실행 hello 워크플로에 대 한 로컬 테스트를 수행 합니다. 될 가능성이 높은 hello 워크플로 갑자기 실행을 중지 하 고 오류가 발생 하는 hello 구성 요소에 대해 빨간색 윤곽선으로 나타냅니다.

![색 공간 변환기 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*색 공간 변환기 오류*

Hello 인코딩 시도가 실패 하는 hello 이유는 무엇 hello의 오른쪽 위 모서리 hello 색 공간 변환기 구성 요소 toosee에서에서 약간 빨간색 hello "E" 아이콘을 클릭 합니다.

![색 공간 변환기 오류 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*색 공간 변환기 오류 대화 상자*

Hello 들어오는 색 공간 hello 색 공간 변환기에 대 한 표준에 대 한 YUV tooRGB 우리의 요청한 변환 toobe rec601 있는지, 볼 수 있듯이을 설정 합니다. 스트림은 rec601을 나타내지 않습니다. (Rec 601은 디지털 비디오 형태로 인터레이스된 아날로그 비디오 신호를 인코딩하기 위한 표준입니다. 720 광도 샘플 및 줄 당 360 색차 샘플을 포함하는 활성 영역을 지정합니다. 인코딩 시스템 hello 색 YCbCr 4 라고: 2:2.)

toofix이 म rec601 콘텐츠로 처리할 우리의 스트림의 hello 메타 데이터에 표시 합니다. toodo 되므로 원시 원본과 hello 색 공간 변환 구성 요소 간의 입력 비디오 데이터 형식 업데이트 프로그램 구성 요소를 사용 합니다. 이 데이터 형식 업데이트 프로그램 형식 속성을 특정 비디오 데이터를 수동으로 업데이트 hello 허용합니다. Tooindicate는 색 공간 표준 "Rec 601"의 구성 합니다. 이렇게 하면 hello 비디오 데이터 형식 업데이트 프로그램 tootag hello 스트림 hello "Rec 601" 색 공간을 가진 경우 아직 정의 색 공간이 없습니다. (하지 파일로 재정의 됩니다 기존 메타 데이터, hello 재정의 확인란을 선택 하지 않으면.)

![데이터 형식 업데이트 프로그램 hello에 색 공간 표준 업데이트](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*데이터 형식 업데이트 프로그램 hello에 색 공간 표준 업데이트*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>완료된 워크플로
이제 우리 워크플로 완료 되 면 통과 하는 다른 테스트 실행 toosee 않습니다.

![미리 보기로 다중 mp4 출력에 대해 완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*미리 보기로 다중 mp4 출력에 대해 완료된 워크플로*

## <a id="time_based_trim"></a>다중 비트 전송률 MP4 출력의 시간 기반 트리밍
생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것 트리밍 hello 소스 비디오 타임 스탬프를 기반으로 합니다.

### <a id="time_based_trim_start"></a>워크플로 개요 toostart 트리밍을 추가 합니다.
![워크플로 tooadd 조정을 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*워크플로 tooadd 조정을 시작*

### <a id="time_based_trim_use_stream_trimmer"></a>스트림 트리머 hello를 사용 하 여
hello 스트림 트리머 구성 요소는 타이밍 정보 (초, 분,...)를 기준으로 tootrim hello 시작과 끝의 입력된 스트림 있습니다. hello 트리머 프레임 기반 트리밍을 지원 하지 않습니다.

![스트림 트리머](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*스트림 트리머*

Hello AVC 인코더 및 스피커 위치 assigner toohello 미디어 파일 입력을 직접 연결 하는 대신 이러한 hello 스트림 트리머 사이 포함 합니다. (Hello 비디오 신호 및 hello에 대 한 인터리빙 된 오디오 신호입니다.)

![사이 간 스트림 트리머 배치](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*사이 간 스트림 트리머 배치*

비디오 및 오디오 15 초에서 60 초 hello 비디오에서 사이만 처리 합니다 있도록 보겠습니다 hello 트리머를 구성 합니다.

Hello 비디오 스트림 트리머의 toohello 속성 이동한 다음 (15) 시작 시간 및 종료 시간 (60 초) 속성을 모두 구성 합니다. toomake 두 당사의 오디오 및 비디오 트리머가 항상 구성 된 toohello 동일 앞뒤에 값이 있는지, 해당 toohello 워크플로 루트를 hello 발표 합니다.

![스트림 트리머에서 시작 시간 속성 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*스트림 트리머에서 시작 시간 속성 게시*

![시작 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*시작 시간에 속성 대화 상자 게시*

![종료 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*종료 시간에 속성 대화 상자 게시*

म hello 우리의 워크플로 루트 이제 검사를 하는 경우 두 속성 모두 깔끔하게 표시 되 고 구성 가능한 여기에서.

![루트에 사용 가능한 게시된 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*루트에 사용 가능한 게시된 속성*

이제 hello 트리밍 속성 hello 오디오 트리머에서 열고 toohello 참조 하는 식으로 모두 시작 및 종료 시간을 구성 워크플로의 hello 루트에 대 한 속성을 게시 합니다.

Hello에 대 한 오디오 트리밍 시작 시간:

    ${ROOT_TrimmingStartTime}

그리고 종료 시간을 다음과 같습니다.

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>완료된 워크플로
![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*완료된 워크플로*

## <a id="scripting"></a>스크립트 구성 요소를 hello 소개
스크립트 구성 요소 워크플로 hello 실행 단계 중 임의의 스크립트를 실행할 수 있습니다. 실행 될 수 있는 다른 스크립트는 4 개가 각각 특정 한 특성 및 hello 워크플로 수명 주기에서 자신의 위치:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

스크립트 구성 요소 각 위의 hello에 대 한 자세히가 이동 hello hello 문서화 합니다. [섹션 다음 hello](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** hello 워크플로 시작할 때 스크립트 구성 요소는 사용 되는 tooconstruct hello 신속 하 게 cliplist xml입니다. 이 스크립트의 수명에 한 번만 수행 됨 hello 구성 요소 설치 하는 동안 호출 됩니다.

### <a id="scripting_hello_world"></a>워크플로 내의 스크립팅: Hello World
Hello 디자이너 화면에 스크립트 구성 요소를 끌어 하 고 (예: "SetClipListXML").

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*스크립팅된 구성 요소 추가*

hello 속성을 검사할 때 스크립트 구성 요소, 다른 스크립트 유형은 나타납니다 hello, 각 구성 가능한 tooa 다른 스크립트 hello 합니다.

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*스크립팅된 구성 요소 속성*

지우기 processInputScript hello 고 realizeScript hello에 대 한 hello 편집기를 엽니다. 이제를 설정 하는 하 고 toostart 스크립트를 준비 합니다.

스크립트 Groovy, Java와의 호환성을 유지 하는 hello Java 플랫폼에 대 한 동적으로 컴파일된 스크립트 언어로 작성 됩니다. 사실 대부분의 Java 코드는 유효한 Groovy 코드입니다.

우리의 realizeScript의 hello 컨텍스트에서 간단한 hello world 하시면 스크립트를 작성해 보겠습니다. Hello 편집기에서 hello 다음을 입력 합니다.

    node.log("hello world");

이제 로컬 테스트 실행을 실행합니다. 이 실행 한 후 검사할 (hello 시스템 탭을 통해 구성 요소 스크립팅 hello) hello 로그 속성입니다.

![Hello World 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Hello World 로그 출력*

hello 로그 메서드를 호출 하는 hello 노드 개체 tooour 현재 "노드" 또는 hello 구성 요소 내에서 스크립팅 하는 것을 나타냅니다. 따라서을 hello 기능 toooutput 로깅 데이터를 hello 시스템을 통해 사용할 수 있는 모든 구성 요소입니다. 이 경우에서는 문자열 리터럴 "hello world" hello를 출력합니다. 중요 한 toounderstand 여기에이 증명할 수 toobe hello 스크립트를 실제로에 대 한 정보를 제공 하는 매우 유용한 디버깅 도구입니다.

스크립팅 우리의 환경 내에서 해야 액세스 tooproperties 다른 구성 요소에 있습니다. 다음을 실행해보세요.

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

이 로그 창 다음 hello를 표시 됩니다.

![노드 경로에 액세스하기 위한 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*노드 경로에 액세스하기 위한 로그 출력*

## <a id="frame_based_trim"></a>다중 비트 전송률 MP4 출력의 프레임 기반 트리밍
생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것 잘라내기의 프레임 수에 비해 hello 원본 비디오에 있습니다.

### <a id="frame_based_trim_start"></a>조정을 추가 개요 toostart 세부 계획
![워크플로 toostart 트리밍을 추가 합니다.](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*워크플로 toostart 트리밍을 추가 합니다.*

### <a id="frame_based_trim_clip_list"></a>Hello 클립 목록 XML을 사용 하 여
모든 이전 워크플로 자습서 hello 미디어 파일 입력 구성 요소는 비디오 입력된 원본으로 사용 했습니다. 이 특정 시나리오에 대 한 하지만 사용할 예정 hello 클립 목록 원본 구성 요소 대신 합니다. 참고 hello 되지 않아야이 방식으로 작업;의 기본 설정 hello 클립 목록 소스는 실제 이유 toodo 하므로 경우에 사용 (hello 하는 중 있는 경우 아래에는 hello 클립 목록 지우기 기능을 사용).

당사의 미디어 파일 입력 toohello 클립 목록 소스에서에서 tooswitch hello 디자인 화면으로 끌어오는 hello 클립 목록 원본 구성 요소를 hello 워크플로 디자이너의 hello 클립 목록 XML pin toohello 클립 목록 XML 노드를 연결 합니다. 이 hello 클립 목록 소스 tooour 입력된 비디오에 따라 출력 핀으로 채워야 합니다. 이제 hello hello 클립 목록 소스 toohello에서 hello 압축 되지 않은 비디오 및 오디오를 압축 되지 않은 pin을 연결할 각 AVC 인코더 및 오디오 스트림 인터리브 됩니다. 이제 hello 미디어 파일 입력을 제거 합니다.

![미디어 파일 입력 hello 클립 목록 소스 hello로 대체](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*미디어 파일 입력 hello 클립 목록 소스 hello로 대체*

hello 클립 목록 원본 구성 요소는 입력으로 사용해 "클립 목록 XML"입니다. 와 소스 파일 tootest hello를 로컬에 선택이 클립 목록 xml은을 자동으로 채워집니다.

![자동으로 채워진 클립 목록 XML 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*자동으로 채워진 클립 목록 XML 속성*

좀 더 가깝기 때문 toohello xml을 찾고,이 같은 모양을:

![클립 목록 대화 상자 편집](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*클립 목록 대화 상자 편집*

그러나이 반영 하지 않습니다 hello 클립 목록 xml의 hello 기능. 한 가지 옵션은 tooadd hello 비디오 및 오디오 소스, 다음과 같이 모두에서 "트리밍" 요소.

![트림 요소 toohello 클립 목록 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*트림 요소 toohello 클립 목록 추가*

Hello 비디오 위에 다음과 같이 hello 클립 목록 xml을 수정 하 고 로컬 테스트를 실행 하는 경우 나타납니다 잘못 된 hello 비디오에서 10에서 20 초 사이의 잘립니다.

반대 toowhat이 동일한 cliplist xml hello Azure 미디어 서비스에서 실행 되는 워크플로에서 적용 될 때 효과가 같음 없는 경우 로컬 실행을 할 때 발생 합니다. Azure 프리미엄 인코더가 시작 되 면 hello cliplist xml 입력된 파일 hello 인코딩 hello에 따라 다시 될 때마다 생성 될 때 작업이 제공 되었습니다. 즉, hello xml에 대해 수행 하는 변경 내용을 아쉽게도 재정의 됩니다.

toocounter hello cliplist xml 인코딩 작업 시작 될 때 초기화 되 고 다시 생성할 수 것 hello 신속 하 게 취급 워크플로의 hello 시작 후 바로 합니다. "스크립팅된 구성 요소"라는 것을 통해 이러한 사용자 지정 작업을 수행할 수 있습니다. 자세한 내용은 참조 [소개 hello 구성 요소 스크립팅](media-services-media-encoder-premium-workflow-tutorials.md#scripting)합니다.

스크립트 구성 요소 hello 디자이너 화면으로 끌어서 너무 이름 바꾸기 "SetClipListXML"입니다.

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*스크립팅된 구성 요소 추가*

hello 속성을 검사할 때 스크립트 구성 요소, 다른 스크립트 유형은 나타납니다 hello, 각 구성 가능한 tooa 다른 스크립트 hello 합니다.

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*스크립팅된 구성 요소 속성*

### <a id="frame_based_trim_modify_clip_list"></a>스크립트 구성 요소에서 hello 클립 목록을 수정
Hello cliplist 생성 된 xml을 워크플로 시작 하는 동안 다시 작성할 수 있습니다, 전에 toohave 액세스 toohello cliplist xml 속성 및 내용 필요 합니다. 다음과 같은 작업을 수행할 수 있습니다.

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![기록된 들어오는 클립 목록](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*기록된 들어오는 클립 목록*

먼저 다음 방식으로 toodetermine 해야 tootrim 지점인까지 원하는 하는 시점을 hello 비디오. toomake hello 워크플로의이 편리한 toohello 간단한 기술 사용자 게시 hello 그래프의 두 가지 속성 toohello 루트입니다. toodo이 hello 디자이너 화면을 마우스 오른쪽 단추로 클릭 하 고 "속성 추가"를 선택 합니다.

* 첫 번째 속성: 형식의 "ClippingTimeStart": "시간 코드"
* 두 번째 속성: 형식의 "ClippingTimeEnd": "시간 코드"

![클리핑 시작 시간에 속성 대화 상자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*클리핑 시작 시간에 속성 대화 상자 추가*

![워크플로 루트에 게시된 클리핑 시간 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*워크플로 루트에 게시된 클리핑 시간 속성*

두 속성 tooa 적합 한 값을 구성 합니다.

![시작 및 끝 속성 클리핑 hello 구성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*시작 및 끝 속성 클리핑 hello 구성*

이제 스크립트 내에서 다음과 같은 두 속성에 액세스할 수 있습니다.

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![클리핑의 시작 및 종료를 보여주는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*클리핑의 시작 및 종료를 보여주는 로그 창*

보겠습니다 간단한 정규식을 사용 하 여 더 편리 toouse 양식으로 hello 시간 코드 문자열을 구문 분석:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![구문 분석된 시간 코드의 출력이 있는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*구문 분석된 시간 코드의 출력이 있는 로그 창*

이 정보를 이제 hello cliplist xml tooreflect hello 시작을 수정할 수 있습니다 및 hello에 대 한 종료 시간 프레임을 정확 하 게 클리핑 hello 동영상의 원하는 합니다.

![스크립트 코드 tooadd 트림 요소](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*스크립트 코드 tooadd 트림 요소*

이 작업은 일반 문자열 조작 작업을 통해 수행되었습니다. hello 결과 수정 된 클립 목록 xml은 다시 기록 toohello clipListXML 속성 hello 워크플로 루트에 hello "setProperty" 메서드를 통해. hello 로그 창 다른 테스트 실행 한 후에 다음 hello 보여주실:

![Hello 결과 클립 목록 로깅](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Hello 결과 클립 목록 로깅*

Hello 비디오 및 오디오 스트림이 자르는 방법을 테스트 실행 toosee를 수행 합니다. 그러나 Hello 트리밍 지점에 대 한 값이 서로 다른 여러 개 테스트 실행, 작업을 하는 것은 고려 되지 않습니다 수 알 수 있습니다! 이 대 한 hello 이유는 해당 hello 디자이너 hello Azure 런타임 달리, 모든 실행 hello cliplist xml를 재정의 하지 않습니다. 즉,만 hello hello를 설정 하면 처음으로 시작 및 종료 지점에서 않도록 hello xml tootransform, 시간, 우리의 가드 절 hello 모든 다른 (하는 경우 (clipListXML.indexOf ("<trim>")-1 = =)) hello 워크플로 트림 다른 추가 되지 것입니다 요소 한 개가 있는 경우 이미 존재 합니다.

toomake 우리의 워크플로 편리한 tootest 로컬로 최상의 우리 트림 요소가 이미 있는 경우를 검사 하는 일부 집 유지 코드를 추가 합니다. 이 경우 hello 새 값을 사용 하 여 hello xml을 수정 하 여 계속 하기 전에 제거할 수 있습니다. 실제 xml 개체를 통해이 모델을 구문 분석 하는 것 보다 안전한 toodo는 것 대신 일반 문자열 조작을 사용 합니다.

하지만 이러한 코드 추가할 수 있습니다, 전에 tooadd 스크립트의 다양 한 hello에 대 한 import 문 먼저 시작 해야:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

그러면 코드를 정리 하는 데 필요한 hello를 추가할 수 있습니다.

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

이 코드는 hello 트림 요소 toohello cliplist xml을 추가 하는 hello 지점 바로 위에 놓입니다.

이 시점에서 실행 하 고 hello 변경 내용을 계속 적용 하는 동안 원하는 만큼 시간 처럼 워크플로 수정 수 있습니다.    

### <a id="frame_based_trim_clippingenabled_prop"></a>ClippingEnabled 편의 속성 추가
항상 원하지 트리밍 toohappen, 대로 보겠습니다 마무리 하기만 하면 워크플로 편리 하 게 나타내는 부울 플래그를 추가 하 여 tooenable 트리밍 / 클리핑 원하는 여부.

와 마찬가지로 이전에 "부울" 형식의 "ClippingEnabled" 라는 워크플로 중 새 속성 toohello 루트를 게시 합니다.

![클리핑 설정에 게시된 속성 ](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*클리핑 설정에 게시된 속성*

간단한 가드 절 아래의 hello와 트리밍 해야 하는 경우를 확인 하 고 클립 목록 수정 toobe 따라서 있어야 하는 경우를 결정 수 했습니다.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>코드 완료
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>참고 항목
[Azure 미디어 서비스의 프리미엄 인코딩 소개](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[어떻게 tooUse Azure 미디어 서비스에서 프리미엄 인코딩](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Azure Media Service로 주문형 콘텐츠 인코딩](media-services-encode-asset.md#media-encoder-premium-workflow)

[미디어 인코더 Premium 워크플로 형식 및 코덱](media-services-premium-workflow-encoder-formats.md)

[샘플 워크플로 파일](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Azure 미디어 서비스 탐색기 도구](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
