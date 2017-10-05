---
title: "DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함 | Microsoft 문서"
description: "이 토픽에서는 DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오를 포함시키는 방법을 보여 줍니다."
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="b1d4e-103">DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함</span><span class="sxs-lookup"><span data-stu-id="b1d4e-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="b1d4e-104">개요</span><span class="sxs-lookup"><span data-stu-id="b1d4e-104">Overview</span></span>
<span data-ttu-id="b1d4e-105">MPEG-DASH는 고품질 적응 비디오 스트리밍 출력을 전달하려는 사용자에게 많은 혜택을 제공하는 비디오 콘텐츠의 적응 스트리밍을 위한 ISO 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="b1d4e-106">MPEG-DASH를 사용하면 네트워크 정체 상태일 때 비디오 스트림이 자동으로 낮은 화질로 떨어집니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="b1d4e-107">따라서 플레이어가 재생할 다음 몇 초를 다운로드(버퍼링)하는 동안 뷰어에 "일시 중지된" 비디오가 표시될 가능성을 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="b1d4e-108">네트워크 정체가 줄어들면 비디오 플레이어가 높은 품질의 스트림에 다시 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="b1d4e-109">또한 이렇게 필요한 대역폭으로 조정하는 기능 덕분에 비디오의 시작 시간이 더욱 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="b1d4e-110">즉, 처음 몇 초는 낮은 품질로 세그먼트를 빠르게 다운로드하여 재생한 다음 충분한 콘텐츠가 버퍼링되고 나면 높은 품질로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="b1d4e-111">Dash.js는 JavaScript로 작성된 오픈 소스 MPEG-DASH 비디오 플레이어입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="b1d4e-112">목표는 비디오 재생이 필요한 응용 프로그램에서 자유롭게 다시 사용할 수 있는 강력한 플랫폼 간 플레이어를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="b1d4e-113">W3C MSE(미디어 원본 확장)를 지원하는 모든 브라우저에서 MPEG-DASH 재생을 제공합니다. 현재는 Chrome, Microsoft Edge 및 IE11에서 지원되며 다른 브라우저는 MSE를 지원하지 않는 것으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="b1d4e-114">DASH.js에 대한 자세한 내용은 GitHub dash.js 리포지토리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="b1d4e-115">브라우저 기반 스트리밍 비디오 플레이어 만들기</span><span class="sxs-lookup"><span data-stu-id="b1d4e-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="b1d4e-116">재생, 일시 중지, 되감기 등의 원하는 컨트롤이 포함된 비디오 플레이어를 표시하는 간단한 웹 페이지를 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="b1d4e-117">HTML 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b1d4e-117">Create an HTML page</span></span>
2. <span data-ttu-id="b1d4e-118">비디오 태그 추가</span><span class="sxs-lookup"><span data-stu-id="b1d4e-118">Add the video tag</span></span>
3. <span data-ttu-id="b1d4e-119">dash.js 플레이어 추가</span><span class="sxs-lookup"><span data-stu-id="b1d4e-119">Add the dash.js player</span></span>
4. <span data-ttu-id="b1d4e-120">플레이어 초기화</span><span class="sxs-lookup"><span data-stu-id="b1d4e-120">Initialize the player</span></span>
5. <span data-ttu-id="b1d4e-121">일부 CSS 스타일 추가</span><span class="sxs-lookup"><span data-stu-id="b1d4e-121">Add some CSS style</span></span>
6. <span data-ttu-id="b1d4e-122">MSE를 구현하는 브라우저에서 결과 보기</span><span class="sxs-lookup"><span data-stu-id="b1d4e-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="b1d4e-123">몇 줄의 JavaScript 코드로 플레이어 초기화를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="b1d4e-124">dash.js를 사용하면 매우 간단하게 브라우저 기반 응용 프로그램에 MPEG-DASH 비디오를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="b1d4e-125">HTML 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b1d4e-125">Creating the HTML Page</span></span>
<span data-ttu-id="b1d4e-126">첫 번째 단계는 다음 예제에 나온 것처럼 **video** 요소가 포함된 표준 HTML 페이지를 만들고 이 파일을 basicPlayer.html로 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="b1d4e-127">DASH.js 플레이어 추가</span><span class="sxs-lookup"><span data-stu-id="b1d4e-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="b1d4e-128">응용 프로그램에 dash.js 참조 구현을 추가하려면 dash.js 프로젝트 1.0 릴리스에서 dash.all.js 파일을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="b1d4e-129">이 파일은 응용 프로그램의 JavaScript 폴더에 저장되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="b1d4e-130">이 파일은 단일 파일에 모든 필요한 dash.js 코드를 간편하게 취합해 놓은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="b1d4e-131">dash.js 리포지토리를 살펴보면 개별 파일, 테스트 코드 등을 찾을 수 있지만 dash.js만 사용하려는 경우는 dash.all.js 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="b1d4e-132">응용 프로그램에 dash.js 플레이어를 추가하려면 basicPlayer.html의 헤드 섹션에 다음 스크립트 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="b1d4e-133">다음으로, 페이지가 로드될 때 플레이어를 초기화하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="b1d4e-134">dash.all.js를 로드하는 행 뒤에 다음 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="b1d4e-135">이 함수는 먼저 DashContext를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-135">This function first creates a DashContext.</span></span> <span data-ttu-id="b1d4e-136">이 항목은 특정 런타임 환경에 맞게 응용 프로그램을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="b1d4e-137">기술적인 관점에서 보면, 응용 프로그램을 생성할 때 종속성 주입 프레임 워크를 사용해야 하는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="b1d4e-138">대부분의 경우, Dash.di.DashContext를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="b1d4e-139">다음으로, dash.js 프레임워크의 기본 클래스인 MediaPlayer를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="b1d4e-140">이 클래스는 재생 및 일시 중지 등의 필요한 핵심 메서드를 포함하며, 비디오 요소와의 관계를 관리하고 재생할 비디오를 설명하는 MPD(미디어 프레젠테이션 설명) 파일의 해석을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="b1d4e-141">플레이어가 비디오를 재생할 준비가 되도록 MediaPlayer 클래스의 startup() 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="b1d4e-142">무엇보다도 이 함수는 컨텍스트에 정의된 대로 필요한 모든 클래스가 로드되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="b1d4e-143">플레이어가 준비되면 attachView() 함수를 사용하여 비디오 요소를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="b1d4e-144">그러면 MediaPlayer가 비디오 스트림을 요소에 주입하고 필요에 따라 재생을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="b1d4e-145">재생하려는 비디오에 대해 알 수 있도록 MediaPlayer에 MPD 파일의 URL을 전달합니다. 방금 만든 setupVideo() 함수는 페이지가 완전히 로드된 후 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="b1d4e-146">body 요소의 onload 이벤트를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="b1d4e-147"><body> 요소를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="b1d4e-148">마지막으로, CSS를 사용하여 video 요소의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="b1d4e-149">적응 스트리밍 환경에서는 네트워크 상태 변화에 따라 재생이 조정되면 재생 중인 비디오의 크기가 변경될 수 있으므로 이 작업이 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="b1d4e-150">이 간단한 데모에서는 페이지의 헤드 섹션에 다음 CSS를 추가하여 사용 가능한 브라우저 창의 80%가 되도록 비디오 요소를 강제 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="b1d4e-151">비디오 재생</span><span class="sxs-lookup"><span data-stu-id="b1d4e-151">Playing a Video</span></span>
<span data-ttu-id="b1d4e-152">비디오를 재생하려면 브라우저가 basicPlayback.html 파일을 가리키도록 지정하고 표시된 비디오 플레이어에서 재생을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1d4e-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b1d4e-153">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b1d4e-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b1d4e-154">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b1d4e-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="b1d4e-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b1d4e-155">See Also</span></span>
[<span data-ttu-id="b1d4e-156">비디오 플레이어 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="b1d4e-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="b1d4e-157">GitHub dash.js 리포지토리</span><span class="sxs-lookup"><span data-stu-id="b1d4e-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

