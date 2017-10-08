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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>TooUse는 hello Adobe 열기 소스 미디어 프레임 워크에 대 한 Microsoft 부드러운 스트리밍 플러그 인을 hello 하는 방법
## <a name="overview"></a>개요
열기 소스 미디어 Framework 2.0 (OSMF 용 SS) OSMF의 hello 기본 기능을 확장 하 고 Microsoft 부드러운 스트리밍 콘텐츠 재생 toonew 기존 OSMF 추가 대 한 Microsoft 부드러운 스트리밍 플러그 인을 hello 플레이어입니다. 또한 hello 플러그 인 부드러운 스트리밍 재생 기능 tooStrobe 미디어 재생 (SMP)를 추가합니다.

SS for OSMF에는 두 가지 버전의 플러그 인이 포함됩니다.

* OSMF용 정적 부드러운 스트리밍 플러그 인(.swc)
* OSMF용 동적 부드러운 스트리밍 플러그 인(.swf)

이 문서에서는 hello 판독기에는 OSMF 및 OSMF 대 한 일반 작업 지식이 가정 플러그 인 합니다. OSMF에 대 한 자세한 내용은 설명서를 참조 하십시오 hello hello에 [공식 OSMF 사이트](http://osmf.org/)합니다.

### <a name="smooth-streaming-plugin-for-osmf-20"></a>OSMF용 부드러운 스트리밍 플러그 인 2.0
hello 플러그 인 같은 기능 hello로 로드 하 고 주문형 부드러운 스트리밍 콘텐츠의 재생을 지원 합니다.

* 주문형 부드러운 스트리밍 재생(재생, 일시 중지, 검색, 중지)
* Live Smooth Streaming 재생(재생)
* Live DVR 기능(일시 중지, 검색, DVR 재생, 라이브 전환)
* 비디오 코덱 지원 - H.264
* 오디오 코덱 지원 - AAC
* OSMF 기본 제공 API로 여러 오디오 언어 전환
* OSMF 기본 제공 API로 최대 재생 품질 선택
* OSMF 캡션 플러그 인으로 사이드카 선택 캡션
* Adobe&reg; Flash&reg; Player 11.4 이상.
* 이 버전은 OSMF 2.0만 지원함

## <a name="supported-features-and-known-issues"></a>지원되는 기능 및 알려진 문제
전체 목록을 지원 되는 기능, 지원 되지 않는 기능 및 알려진된 문제에 대 한 참조 너무[이 문서](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf)합니다.

## <a name="loading-hello-plugin"></a>로드 hello 플러그 인
OSMF 플러그 인은 정적으로(컴파일 시간에) 또는 동적으로(런타임에) 로드할 수 있습니다. OSMF 다운로드에 대 한 부드러운 스트리밍 플러그인 hello 동적 및 정적 버전이 포함 됩니다.

* 정적 로드: tooload 정적으로 정적 라이브러리 (SWC) 파일은 필요 합니다. 정적 플러그 인 참조로 추가 된 hello 컴파일 타임에 파일 toohello 프로젝트와 hello 최종 출력 내부 병합 합니다.
* 동적 로드: tooload 동적으로 미리 컴파일된 (SWF) 파일이 필요 합니다. 동적 플러그 인 hello 런타임에서 로드 되 고 hello 프로젝트 출력에 포함 되지 않습니다. (컴파일된 출력) 동적 플러그 인은 HTTP 및 FILE 프로토콜을 사용하여 로드할 수 있습니다.

정적 및 동적 로드에 대 한 자세한 내용은 참조 hello 공식 [OSMF 플러그 인 페이지](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf)합니다.

### <a name="ss-for-osmf-static-loading"></a>SS for OSMF 정적 로드
아래 코드 조각 hello tooload이 OSMF 용 SS 플러그 인을 정적으로 hello 하 한 OSMF MediaFactory 클래스를 사용 하 여 기본 비디오를 재생 하는 방법을 보여줍니다. OSMF 코드에 대 한 hello SS를 포함 하기 전에 hello 프로젝트 참조 "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" hello 정적 플러그 인이 포함 되어 있는지 확인 하십시오.

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


### <a name="ss-for-osmf-dynamic-loading"></a>SS for OSMF 동적 로드
아래 코드 조각 hello tooload OSMF 용 SS 플러그 인을 동적으로 hello 하 고 hello OSMF MediaFactory 클래스를 사용 하는 기본 비디오를 재생 하는 방법을 보여 줍니다. OSMF 코드에 대 한 hello SS를 포함 하기 전에 파일 프로토콜을 사용 하 여 tooload 이나 HTTP 부하에 대 한 웹 서버에서 복사 hello "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf" 동적 플러그 인 toohello 프로젝트 폴더를 복사 합니다. 없는 필요 tooinclude "MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc" hello 프로젝트 참조에 있습니다.

package {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>SS ODMF 동적 플러그 인 hello로 strobe Media Playback
hello 부드러운 스트리밍 OSMF 동적 플러그 인에 대해 호환 되 [Strobe 미디어 재생 (SMP)](http://osmf.org/strobe_mediaplayback.html)합니다. OSMF 플러그 인 tooadd 부드러운 스트리밍 콘텐츠 재생 tooSMP에 대 한 hello SS를 사용할 수 있습니다. toodo "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" 웹 서버에서 다음 hello를 사용 하 여 HTTP 부하에 대 한 단계는이 복사 합니다.

1. Hello 찾아보기 [Strobe Media Playback 설정 페이지](http://osmf.org/dev/2.0gm/setup.html)합니다. 
2. Hello src tooa 부드러운 스트리밍 원본 (예: http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 설정 
3. Hello 필요한 구성 변경 내용을 확인 하 고 미리 보기 및 업데이트를 클릭 합니다.
   
   **참고** 콘텐츠 웹 서버에는 유효한 crossdomain.xml이 필요합니다. 
4. 복사한 hello 코드 tooa 간단한 HTML 페이지와 같은 원하는 텍스트 편집기를 사용 하 여 다음 예제는 hello에 붙여넣습니다.

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



1. 부드러운 스트리밍 OSMF 플러그 인 toohello 추가 코드를 포함 하 고 저장 합니다.
   
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
2. HTML 페이지를 저장 하 고 tooa 웹 서버를 게시 합니다. 찾아보기 toohello 즐겨 찾는 Flash 사용자를 사용 하 여 웹 페이지를 게시&reg; 플레이어 인터넷 브라우저 (Internet Explorer, Chrome, Firefox, 등)를 사용 하도록 설정 합니다.
3. Adobe&reg; Flash&reg; Player에서 부드러운 스트리밍 콘텐츠를 즐깁니다.

일반 OSMF 개발에 대 한 자세한 내용은 hello 공식을 참조 하십시오 [OSMF 개발 페이지](http://osmf.org/resources.html)합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[OSMF용 Microsoft 적응 스트리밍 플러그 인 업데이트](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

