---
title: "오픈 소스 미디어 프레임워크용 부드러운 스트리밍 플러그 인"
description: "Adobe 오픈 소스 미디어 프레임워크용 Azure 미디어 서비스 부드러운 스트리밍 플러그 인을 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="abd3d-103">Adobe 오픈 소스 미디어 프레임워크용 Microsoft 부드러운 스트리밍 플러그 인을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="abd3d-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="abd3d-104">개요</span><span class="sxs-lookup"><span data-stu-id="abd3d-104">Overview</span></span>
<span data-ttu-id="abd3d-105">오픈 소스 미디어 프레임워크용 Microsoft 부드러운 스트리밍 플러그 인 2.0(SS for OSMF)은 OSMF의 기본 기능을 확장하며 기존 및 새로운 OSMF 플레이어에 Microsoft 부드러운 스트리밍 콘텐츠 재생을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="abd3d-106">이 플러그 인은 또한 SMP(Strobe Media Playback)에 부드러운 스트리밍 재생 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="abd3d-107">SS for OSMF에는 두 가지 버전의 플러그 인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="abd3d-108">OSMF용 정적 부드러운 스트리밍 플러그 인(.swc)</span><span class="sxs-lookup"><span data-stu-id="abd3d-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="abd3d-109">OSMF용 동적 부드러운 스트리밍 플러그 인(.swf)</span><span class="sxs-lookup"><span data-stu-id="abd3d-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="abd3d-110">이 문서는 OSMF 및 OSMF 플러그 인에 대한 실용적인 일반 지식을 가진 독자를 대상으로 합니다. OSMF에 대한 자세한 내용은 [OSMF 공식 사이트](http://osmf.org/)(영문)에 있는 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="abd3d-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="abd3d-111">OSMF용 부드러운 스트리밍 플러그 인 2.0</span><span class="sxs-lookup"><span data-stu-id="abd3d-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="abd3d-112">이 플러그 인은 다음 기능을 통해 주문형 부드러운 스트리밍 콘텐츠의 로딩과 재생을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="abd3d-113">주문형 부드러운 스트리밍 재생(재생, 일시 중지, 검색, 중지)</span><span class="sxs-lookup"><span data-stu-id="abd3d-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="abd3d-114">Live Smooth Streaming 재생(재생)</span><span class="sxs-lookup"><span data-stu-id="abd3d-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="abd3d-115">Live DVR 기능(일시 중지, 검색, DVR 재생, 라이브 전환)</span><span class="sxs-lookup"><span data-stu-id="abd3d-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="abd3d-116">비디오 코덱 지원 - H.264</span><span class="sxs-lookup"><span data-stu-id="abd3d-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="abd3d-117">오디오 코덱 지원 - AAC</span><span class="sxs-lookup"><span data-stu-id="abd3d-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="abd3d-118">OSMF 기본 제공 API로 여러 오디오 언어 전환</span><span class="sxs-lookup"><span data-stu-id="abd3d-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="abd3d-119">OSMF 기본 제공 API로 최대 재생 품질 선택</span><span class="sxs-lookup"><span data-stu-id="abd3d-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="abd3d-120">OSMF 캡션 플러그 인으로 사이드카 선택 캡션</span><span class="sxs-lookup"><span data-stu-id="abd3d-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="abd3d-121">Adobe&reg; Flash&reg; Player 11.4 이상.</span><span class="sxs-lookup"><span data-stu-id="abd3d-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="abd3d-122">이 버전은 OSMF 2.0만 지원함</span><span class="sxs-lookup"><span data-stu-id="abd3d-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="abd3d-123">지원되는 기능 및 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="abd3d-123">Supported features and known issues</span></span>
<span data-ttu-id="abd3d-124">지원되는 기능, 지원되지 않는 기능 및 알려진 문제의 전체 목록은 [이 문서](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abd3d-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="abd3d-125">플러그 인 로드</span><span class="sxs-lookup"><span data-stu-id="abd3d-125">Loading the Plugin</span></span>
<span data-ttu-id="abd3d-126">OSMF 플러그 인은 정적으로(컴파일 시간에) 또는 동적으로(런타임에) 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="abd3d-127">OSMF용 부드러운 스트리밍 플러그 인 다운로드에는 동적 버전과 정적 버전이 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="abd3d-128">정적 로드: 정적으로 로드하려면 정적 라이브러리(SWC) 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="abd3d-129">정적 플러그 인이 프로젝트에 참조로 추가되고 컴파일 시간에 최종 출력 파일 내에 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="abd3d-130">동적 로드: 동적으로 로드하려면 미리 컴파일된(SWF) 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="abd3d-131">동적 플러그 인이 런타임에 로드되며 프로젝트 출력에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="abd3d-132">(컴파일된 출력) 동적 플러그 인은 HTTP 및 FILE 프로토콜을 사용하여 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="abd3d-133">정적 및 동적 로드에 대한 자세한 내용은 공식 [OSMF 플러그 인 페이지](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf)(영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="abd3d-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="abd3d-134">SS for OSMF 정적 로드</span><span class="sxs-lookup"><span data-stu-id="abd3d-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="abd3d-135">아래 코드 조각은 OSMF용 SS 플러그 인을 정적으로 로드하고 OSMF MediaFactory 클래스를 사용하여 기본 비디오를 재생하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="abd3d-136">SS for OSMF 코드를 포함하기 전에 먼저 프로젝트 참조에 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" 정적 플러그 인이 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="abd3d-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="abd3d-137">SS for OSMF 동적 로드</span><span class="sxs-lookup"><span data-stu-id="abd3d-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="abd3d-138">아래 코드 조각은 OSMF용 SS 플러그 인을 동적으로 로드하고 OSMF MediaFactory 클래스를 사용하여 기본 비디오를 재생하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="abd3d-139">SS for OSMF 코드를 포함하기 전에 먼저 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" 동적 플러그 인을 프로젝트 폴더에 복사(FILE 프로토콜을 사용하여 로드하려는 경우)하거나 HTTP 로드용 웹 서버 아래에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="abd3d-140">프로젝트 참조에 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc"를 포함할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="abd3d-141">package {</span><span class="sxs-lookup"><span data-stu-id="abd3d-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="abd3d-142">}</span><span class="sxs-lookup"><span data-stu-id="abd3d-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="abd3d-143">Strobe Media Playback 및 SS ODMF 동적 플러그 인</span><span class="sxs-lookup"><span data-stu-id="abd3d-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="abd3d-144">OSMF용 부드러운 스트리밍 동적 플러그 인은 [SMP(Strobe Media Playback)](http://osmf.org/strobe_mediaplayback.html)(영문)와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="abd3d-145">SS for OSMF 플러그 인을 사용하여 SMP에 부드러운 스트리밍 콘텐츠 재생을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="abd3d-146">이렇게 하려면 다음 단계에 따라 "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf"를 HTTP 로드용 웹 서버 아래에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="abd3d-147">[Strobe Media Playback 설정 페이지](http://osmf.org/dev/2.0gm/setup.html)(영문)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="abd3d-148">src를 부드러운 스트리밍 원본(예: http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="abd3d-149">원하는 대로 구성을 변경하고 Preview and Update를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="abd3d-150">**참고** 콘텐츠 웹 서버에는 유효한 crossdomain.xml이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="abd3d-151">즐겨 사용하는 텍스트 편집기에서 코드를 복사하여 다음 예와 같이 간단한 HTML 페이지에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="abd3d-152">부드러운 스트리밍 OSMF 플러그 인을 embed 태그에 추가하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="abd3d-153">HTML 페이지를 저장하고 웹 서버에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="abd3d-154">즐겨 사용하는 Flash&reg; Player 지원 인터넷 브라우저(Internet Explorer, Chrome, Firefox 등)를 사용하여 게시된 웹 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="abd3d-155">Adobe&reg; Flash&reg; Player에서 부드러운 스트리밍 콘텐츠를 즐깁니다.</span><span class="sxs-lookup"><span data-stu-id="abd3d-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="abd3d-156">일반적인 OSMF 개발에 대한 자세한 내용은 공식 [OSMF 개발 페이지](http://osmf.org/resources.html)(영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="abd3d-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="abd3d-157">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="abd3d-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="abd3d-158">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="abd3d-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="abd3d-159">참고 항목</span><span class="sxs-lookup"><span data-stu-id="abd3d-159">See Also</span></span>
[<span data-ttu-id="abd3d-160">OSMF용 Microsoft 적응 스트리밍 플러그 인 업데이트</span><span class="sxs-lookup"><span data-stu-id="abd3d-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

