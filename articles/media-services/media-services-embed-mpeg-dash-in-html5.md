---
title: "MPEG-DASH 적응 스트리밍 비디오 dash.js를 사용 하 여 HTML5 응용 프로그램에서 aaaEmbedding | Microsoft Docs"
description: "이 항목에서 설명 방법을 tooembed는 MPEG-DASH 적응 스트리밍 비디오 dash.js를 사용 하 여 HTML5 응용 프로그램에 있습니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함
## <a name="overview"></a>개요
MPEG DASH는 toodeliver 고품질의 적응 비디오 스트리밍 출력을 원하는 사용자에 게 많은 혜택을 제공 하는 비디오 콘텐츠의 적응 스트리밍을 hello에 대 한 ISO 표준. MPEG DASH를 hello 비디오 스트림을 자동으로 삭제 합니다 tooa 낮은 정의 hello 네트워크 정체 되는 경우. 이렇게 하면 hello 플레이어 hello 다음 몇 초 tooplay (즉, 버퍼링)를 다운로드 하는 동안 "일시 중지 된" 비디오 보기 hello 뷰어 hello 가능성이 줄어듭니다. 네트워크 정체 줄일 수 hello 비디오 플레이어는 tooa 더 높은 품질 스트림을 다시 반환 합니다. 또한이 기능은 tooadapt hello 대역폭 필요한 비디오에 대 한 빠른 시작 시간에 발생 합니다. 처음 몇 초 hello 있다는 것을 의미 다운로드 하려면 빠른 낮은 품질 세그먼트에서 재생할 수 한 다음 단계를 tooa 더 높은 품질을 충분 한 콘텐츠 버퍼링 된 후입니다.

Dash.js는 JavaScript로 작성된 오픈 소스 MPEG-DASH 비디오 플레이어입니다. 목표는 tooprovide 비디오를 재생 해야 하는 응용 프로그램에서 자유롭게 다시 사용할 수 있는 강력 하 고 플랫폼 간 플레이어입니다. Hello W3C 미디어 원본 확장 MSE (), 즉 오늘 Chrome, Microsoft Edge 및 IE11 (다른 브라우저의 의도 toosupport MSE를 표시 했습니다)를 지 원하는 모든 브라우저에서 재생을 MPEG DASH를 제공 합니다. Dash.js를 사용 하는 방법에 대 한 자세한 내용은 js hello GitHub dash.js 리포지토리를 참조 합니다.

## <a name="creating-a-browser-based-streaming-video-player"></a>브라우저 기반 스트리밍 비디오 플레이어 만들기
이러한는 재생, 일시 중지, rewind 등 toocreate 예상 hello로 비디오 플레이어를 표시 하는 간단한 웹 페이지를 제어, 해야 합니다.

1. HTML 페이지 만들기
2. Hello 비디오 태그를 추가 합니다.
3. Hello dash.js 플레이어를 추가 합니다.
4. Hello 플레이어를 초기화 합니다.
5. 일부 CSS 스타일 추가
6. Hello 결과 MSE를 구현 하는 브라우저에서 보기

JavaScript 코드의 줄 약간에서 hello 플레이어 초기화를 완료할 수 있습니다. Dash.js를 사용 하 여 정말 그렇습니다 브라우저 기반 응용 프로그램에서 간단한 tooembed MPEG-DASH 비디오 해당 합니다.

## <a name="creating-hello-html-page"></a>Hello HTML 페이지 만들기
hello 첫 번째 단계는 hello를 포함 하는 표준 HTML toocreate 페이지 **비디오** 이 basicPlayer.html 다음 예제는 hello로이 파일 저장 형식 요소를 보여 줍니다.

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>추가 hello DASH.js 플레이어
tooadd hello dash.js 참조 구현 toohello 응용 프로그램을 dash.js 프로젝트의 hello 1.0 릴리스에서 toograb hello dash.all.js 파일이 필요 합니다. 이것은 응용 프로그램의 hello JavaScript 폴더에 저장 됩니다. 이 파일은 단일 파일에 모든 hello 필요한 dash.js 코드를 가져오는 편의 파일. 참조 hello dash.js 리포지토리 주위를 설정한 경우 hello 개별 파일을 찾을 코드와 더 많은 테스트 하는 모든 원하면 toodo dash.js를 사용 하 여 사용은 다음 hello dash.all.js 파일은 필요한 합니다.

tooadd hello dash.js 플레이어 tooyour 응용 프로그램, basicPlayer.html의 스크립트 태그 toohello 헤드 섹션을 추가 합니다.

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


다음으로 hello 페이지가 로드 될 때 함수 tooinitialize hello 플레이어를 만듭니다. Hello 스크립트 dash.all.js를 로드 하는 hello 줄 뒤에 다음을 추가 합니다.

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

이 함수는 먼저 DashContext를 만듭니다. 특정 런타임 환경에 대 한 사용 되는 tooconfigure hello 응용 프로그램입니다. 기술적 관점에서 hello 응용 프로그램을 만들 때 hello 종속성 주입 프레임 워크는 클래스를 사용 해야 하는 hello를 정의 합니다. 대부분의 경우, Dash.di.DashContext를 사용합니다.

다음으로 hello MediaPlayer hello dash.js 프레임 워크의 기본 클래스를 인스턴스화하십시오. 이 클래스는 hello 코어와 같은 필요한 메서드 재생 및 일시 중지, hello 비디오 요소와 hello 관계를 관리 하 고 hello 비디오 toobe 재생을 설명 하는 hello 미디어 프레젠테이션에 설명 (MPD) 파일의 hello 해석도 관리를 포함 합니다.

hello MediaPlayer 클래스의 startup () 함수 hello tooensure 라고 하는 hello 플레이어는 준비 tooplay 비디오. 다른 작업 중이 함수는 모든 hello 필요한 클래스 (hello 컨텍스트에 의해 정의 됨)으로 로드 되었는지 확인 합니다. Hello 플레이어 준비 되 면 hello 비디오 요소 tooit hello attachView() 함수를 사용 하 여 연결할 수 있습니다. Hello MediaPlayer tooinject hello 비디오 스트림 hello 요소에 사용할 수 있게 하 고 필요에 따라 재생을 제어할 수도 있습니다.

Hello MPD 파일 toohello MediaPlayer의 hello URL을 전달 하는 것으로 예상 비디오 hello에 대 한 알 수 있도록 방금 만든 tooplay.hello setupVideo() 함수 hello 페이지가 완전히 로드 한 후 실행 되는 toobe 필요 합니다. Hello 본문 요소의 hello onload 이벤트를 사용 하 여이 작업을 수행 합니다. <body> 요소를 다음으로 변경합니다.

    <body onload="setupVideo()">

마지막으로, CSS를 사용 하 여 hello 비디오 요소 hello 크기를 설정 하십시오. 적응 스트리밍 환경에서 특히 중요 때문에 이것이 재생 toochanging 네트워크 상태에 맞게 변경 hello 재생 중인 비디오의 hello 크기 변경 될 수 있습니다. 이 간단한 데모에서는 단순히 hello 비디오 요소 toobe hello 사용할 수 있는 브라우저 창의 80%를 추가 하 여 강제로 hello 페이지의 CSS toohello 헤드 섹션 뒤 hello:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>비디오 재생
비디오 tooplay hello basicPlayback.html 파일에서 브라우저 가리킨 표시 hello 비디오 플레이어에서 재생을 클릭 합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[비디오 플레이어 응용 프로그램 개발](media-services-develop-video-players.md)

[GitHub dash.js 리포지토리](https://github.com/Dash-Industry-Forum/dash.js) 

