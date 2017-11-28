---
title: "aaaSmooth hello Open 소스 미디어 프레임 워크에 대 한 스트리밍 플러그 인"
description: "Toouse hello Adobe 열기 소스 미디어 프레임 워크에 대 한 Azure 미디어 서비스 부드러운 스트리밍 플러그 인을 hello 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="52d5d-103">TooUse는 hello Adobe 열기 소스 미디어 프레임 워크에 대 한 Microsoft 부드러운 스트리밍 플러그 인을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="52d5d-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="52d5d-104">개요</span><span class="sxs-lookup"><span data-stu-id="52d5d-104">Overview</span></span>
<span data-ttu-id="52d5d-105">열기 소스 미디어 Framework 2.0 (OSMF 용 SS) OSMF의 hello 기본 기능을 확장 하 고 Microsoft 부드러운 스트리밍 콘텐츠 재생 toonew 기존 OSMF 추가 대 한 Microsoft 부드러운 스트리밍 플러그 인을 hello 플레이어입니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="52d5d-106">또한 hello 플러그 인 부드러운 스트리밍 재생 기능 tooStrobe 미디어 재생 (SMP)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="52d5d-107">SS for OSMF에는 두 가지 버전의 플러그 인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="52d5d-108">OSMF용 정적 부드러운 스트리밍 플러그 인(.swc)</span><span class="sxs-lookup"><span data-stu-id="52d5d-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="52d5d-109">OSMF용 동적 부드러운 스트리밍 플러그 인(.swf)</span><span class="sxs-lookup"><span data-stu-id="52d5d-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="52d5d-110">이 문서에서는 hello 판독기에는 OSMF 및 OSMF 대 한 일반 작업 지식이 가정 플러그 인 합니다. OSMF에 대 한 자세한 내용은 설명서를 참조 하십시오 hello hello에 [공식 OSMF 사이트](http://osmf.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="52d5d-111">OSMF용 부드러운 스트리밍 플러그 인 2.0</span><span class="sxs-lookup"><span data-stu-id="52d5d-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="52d5d-112">hello 플러그 인 같은 기능 hello로 로드 하 고 주문형 부드러운 스트리밍 콘텐츠의 재생을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="52d5d-113">주문형 부드러운 스트리밍 재생(재생, 일시 중지, 검색, 중지)</span><span class="sxs-lookup"><span data-stu-id="52d5d-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="52d5d-114">Live Smooth Streaming 재생(재생)</span><span class="sxs-lookup"><span data-stu-id="52d5d-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="52d5d-115">Live DVR 기능(일시 중지, 검색, DVR 재생, 라이브 전환)</span><span class="sxs-lookup"><span data-stu-id="52d5d-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="52d5d-116">비디오 코덱 지원 - H.264</span><span class="sxs-lookup"><span data-stu-id="52d5d-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="52d5d-117">오디오 코덱 지원 - AAC</span><span class="sxs-lookup"><span data-stu-id="52d5d-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="52d5d-118">OSMF 기본 제공 API로 여러 오디오 언어 전환</span><span class="sxs-lookup"><span data-stu-id="52d5d-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="52d5d-119">OSMF 기본 제공 API로 최대 재생 품질 선택</span><span class="sxs-lookup"><span data-stu-id="52d5d-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="52d5d-120">OSMF 캡션 플러그 인으로 사이드카 선택 캡션</span><span class="sxs-lookup"><span data-stu-id="52d5d-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="52d5d-121">Adobe&reg; Flash&reg; Player 11.4 이상.</span><span class="sxs-lookup"><span data-stu-id="52d5d-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="52d5d-122">이 버전은 OSMF 2.0만 지원함</span><span class="sxs-lookup"><span data-stu-id="52d5d-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="52d5d-123">지원되는 기능 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="52d5d-123">Supported features and known issues</span></span>
<span data-ttu-id="52d5d-124">전체 목록을 지원 되는 기능, 지원 되지 않는 기능 및 알려진된 문제에 대 한 참조 너무[이 문서](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="52d5d-125">로드 hello 플러그 인</span><span class="sxs-lookup"><span data-stu-id="52d5d-125">Loading hello Plugin</span></span>
<span data-ttu-id="52d5d-126">OSMF 플러그 인은 정적으로(컴파일 시간에) 또는 동적으로(런타임에) 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="52d5d-127">OSMF 다운로드에 대 한 부드러운 스트리밍 플러그인 hello 동적 및 정적 버전이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="52d5d-128">정적 로드: tooload 정적으로 정적 라이브러리 (SWC) 파일은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="52d5d-129">정적 플러그 인 참조로 추가 된 hello 컴파일 타임에 파일 toohello 프로젝트와 hello 최종 출력 내부 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="52d5d-130">동적 로드: tooload 동적으로 미리 컴파일된 (SWF) 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="52d5d-131">동적 플러그 인 hello 런타임에서 로드 되 고 hello 프로젝트 출력에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="52d5d-132">(컴파일된 출력) 동적 플러그 인은 HTTP 및 FILE 프로토콜을 사용하여 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="52d5d-133">정적 및 동적 로드에 대 한 자세한 내용은 참조 hello 공식 [OSMF 플러그 인 페이지](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="52d5d-134">SS for OSMF 정적 로드</span><span class="sxs-lookup"><span data-stu-id="52d5d-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="52d5d-135">아래 코드 조각 hello tooload이 OSMF 용 SS 플러그 인을 정적으로 hello 하 한 OSMF MediaFactory 클래스를 사용 하 여 기본 비디오를 재생 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="52d5d-136">OSMF 코드에 대 한 hello SS를 포함 하기 전에 hello 프로젝트 참조 "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" hello 정적 플러그 인이 포함 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="52d5d-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="52d5d-137">SS for OSMF 동적 로드</span><span class="sxs-lookup"><span data-stu-id="52d5d-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="52d5d-138">아래 코드 조각 hello tooload OSMF 용 SS 플러그 인을 동적으로 hello 하 고 hello OSMF MediaFactory 클래스를 사용 하는 기본 비디오를 재생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="52d5d-139">OSMF 코드에 대 한 hello SS를 포함 하기 전에 파일 프로토콜을 사용 하 여 tooload 이나 HTTP 부하에 대 한 웹 서버에서 복사 hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" 동적 플러그 인 toohello 프로젝트 폴더를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="52d5d-140">없는 필요 tooinclude "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" hello 프로젝트 참조에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="52d5d-141">package {</span><span class="sxs-lookup"><span data-stu-id="52d5d-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="52d5d-142">}</span><span class="sxs-lookup"><span data-stu-id="52d5d-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="52d5d-143">SS ODMF 동적 플러그 인 hello로 strobe Media Playback</span><span class="sxs-lookup"><span data-stu-id="52d5d-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="52d5d-144">hello 부드러운 스트리밍 OSMF 동적 플러그 인에 대해 호환 되 [Strobe 미디어 재생 (SMP)](http://osmf.org/strobe_mediaplayback.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="52d5d-145">OSMF 플러그 인 tooadd 부드러운 스트리밍 콘텐츠 재생 tooSMP에 대 한 hello SS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="52d5d-146">toodo "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" 웹 서버에서 다음 hello를 사용 하 여 HTTP 부하에 대 한 단계는이 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="52d5d-147">Hello 찾아보기 [Strobe Media Playback 설정 페이지](http://osmf.org/dev/2.0gm/setup.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="52d5d-148">Hello src tooa 부드러운 스트리밍 원본 (예: http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 설정</span><span class="sxs-lookup"><span data-stu-id="52d5d-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="52d5d-149">Hello 필요한 구성 변경 내용을 확인 하 고 미리 보기 및 업데이트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="52d5d-150">**참고** 콘텐츠 웹 서버에는 유효한 crossdomain.xml이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="52d5d-151">복사한 hello 코드 tooa 간단한 HTML 페이지와 같은 원하는 텍스트 편집기를 사용 하 여 다음 예제는 hello에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="52d5d-152">부드러운 스트리밍 OSMF 플러그 인 toohello 추가 코드를 포함 하 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="52d5d-153">HTML 페이지를 저장 하 고 tooa 웹 서버를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="52d5d-154">찾아보기 toohello 즐겨 찾는 Flash 사용자를 사용 하 여 웹 페이지를 게시&reg; 플레이어 인터넷 브라우저 (Internet Explorer, Chrome, Firefox, 등)를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="52d5d-155">Adobe&reg; Flash&reg; Player에서 부드러운 스트리밍 콘텐츠를 즐깁니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="52d5d-156">일반 OSMF 개발에 대 한 자세한 내용은 hello 공식을 참조 하십시오 [OSMF 개발 페이지](http://osmf.org/resources.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="52d5d-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="52d5d-157">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="52d5d-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="52d5d-158">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="52d5d-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="52d5d-159">참고 항목</span><span class="sxs-lookup"><span data-stu-id="52d5d-159">See Also</span></span>
[<span data-ttu-id="52d5d-160">OSMF용 Microsoft 적응 스트리밍 플러그 인 업데이트</span><span class="sxs-lookup"><span data-stu-id="52d5d-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

