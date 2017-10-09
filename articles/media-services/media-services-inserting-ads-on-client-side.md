---
title: "hello 클라이언트 쪽에서 aaaInserting 광고 | Microsoft Docs"
description: "이 항목에 tooinsert 광고 클라이언트 쪽 hello 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Hello 클라이언트 쪽에서 광고 삽입
이 항목에서는 방법은 tooinsert 다양 한 유형의 광고 hello 클라이언트 쪽에서 합니다.

라이브 스트리밍 비디오에서 캡션 및 광고 지원에 대한 정보는 [지원되는 캡션 및 Ad 삽입 표준](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads)을 참조하세요.

> [!NOTE]
> Azure 미디어 플레이어는 현재 광고를 지원하지 않습니다.
> 
> 

## <a id="insert_ads_into_media"></a>미디어에 광고 삽입
Windows 미디어 플랫폼 hello 통해 광고 삽입에 대 한 azure 미디어 서비스에서는: 플레이어 프레임 워크입니다. 광고를 지원하는 플레이어 프레임워크는 Windows 8, Silverlight, Windows Phone 8 및 iOS 장치에 사용할 수 있습니다. 각 플레이어 프레임 워크에는 방법을 보여 주는 샘플 코드가 포함 되어 tooimplement 플레이어 응용 프로그램입니다. 종류를 미디어: 목록에 삽입할 수 있는 광고는 세 가지가 있습니다.

* **선형** – 전체 프레임 광고 hello 기본 비디오 일시 중지 하는 합니다.
* **비선형** – hello 기본 비디오가 재생 되로 표시 되는 오버레이 광고, 일반적으로 로고나 기타 정적 이미지 내에 배치 hello 플레이어입니다.
* **도우미** – 광고 hello 플레이어 외부에 표시 되는입니다.

Hello 기본 비디오 타임 라인의 한 지점에서 광고를 배치할 수 있습니다. Ad 및 tooplay hello 하는 경우 hello 플레이어 알려야 광고 tooplay 합니다. 이 작업은 표준 XML 기반 파일 집합을 사용하여 수행됩니다. VAST(Video Ad Service Template), VMAP(Digital Video Multiple Ad Playlist), MAST(Media Abstract Sequencing Template) 및 VPAID(Digital Video Player Ad Interface Definition). VAST 파일 어떤 광고 toodisplay를 지정합니다. 시점을 지정 하는 VMAP 파일 tooplay 다양 한 광고 하 고 VAST XML을 포함 합니다. MAST 파일은 또한 VAST XML을 포함할 수 있는 다른 방법은 toosequence 광고입니다. VPAID 파일 hello 비디오 플레이어와 hello 광고 또는 광고 서버 간의 인터페이스를 정의합니다.

각 플레이어 프레임워크는 서로 다르게 작동하고 각각 별도 토픽에서 설명합니다. 이 항목 hello 사용 되는 기본 메커니즘 tooinsert 광고를 설명 합니다. 비디오 플레이어 응용 프로그램 광고 서버에서 광고를 요청합니다. hello 광고 서버는 여러 가지 방법으로 응답할 수 있습니다.

* VAST 파일 반환
* VMAP 파일 반환(포함된 VAST와 함께)
* MAST 파일 반환(포함된 VAST와 함께)
* VAST 파일 반환(VPAID 광고와 함께)

### <a name="using-a-video-ad-service-template-vast-file"></a>VAST(Video Ad Service Template) 파일 사용
VAST 파일 광고 또는 광고 toodisplay 무엇을 지정합니다. hello 다음 XML은 선형 광고용 VAST 파일의 예:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

선형 광고 hello hello에서 설명한 <**선형**> 요소입니다. Hello 광고의 hello 기간 지정, 추적 이벤트, 클릭 추적, 및 다양 한 통해 클릭 **MediaFile** 요소입니다. Hello 내 추적 이벤트에 지정 된 <**TrackingEvents**> 요소 ad 서버 tootrack hello 광고를 보는 동안 발생 하는 다양 한 이벤트를 허용 합니다. 이 경우 hello 시작, 중간점, 완료 및 확장 이벤트가 추적 됩니다. hello 광고가 표시 되 면 hello 시작 이벤트가 발생 합니다. hello 중간점 이벤트가 발생 이상 hello 광고의 타임 라인의 50%를 보았습니다. hello 완료 이벤트 hello ad toohello 끝 실행이 될 때 발생 합니다. hello 사용자 hello 비디오 플레이어 toofull 화면을 확장 하면 hello 확장 이벤트가 발생 합니다. 클릭 방문으로 지정 됩니다는 <**클릭 광고**> 내에서 요소는 <**VideoClicks**> 요소 hello 사용자 hello 광고를 클릭할 때 URI tooa 리소스 toodisplay를 지정 합니다. 에 지정 된 클릭은 <**클릭**> hello 내 에서도 요소 <**VideoClicks**> 요소 hello 사용자가 클릭할 때 플레이어 toorequest hello에 대 한 추적 리소스를 지정 합니다. hello ad.hello에 <**MediaFile**> 요소는 광고의 특정 인코딩에 대 한 정보를 지정 합니다. 여러 개 있으면 <**MediaFile**> 요소를 hello 비디오 플레이어 수 hello 최적의 인코딩을 선택할 hello 플랫폼에 대 한 합니다. 

선형 광고는 지정된 순서대로 표시될 수 있습니다. toodo이를 더 추가 <Ad> 요소 toohello VAST 파일을 hello 시퀀스 특성을 사용 하 여 hello 순서를 지정 합니다. 다음 예제는 hello이를 보여줍니다.

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

비선형 광고도 <Creative> 요소에서 지정합니다. 다음 예제와 hello는 <Creative> 는 비선형 광고를 설명 하는 요소입니다.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


hello <**NonLinearAds**> 요소에 하나 이상 포함 될 수 있습니다 <**비선형**> 요소는 비선형 광고를 설명할 수 있으며 각 합니다. hello <**비선형**> 요소는 비선형 광고 hello에 대 한 hello 리소스를 지정 합니다. hello 리소스 수는 <**StaticResouce**>, <**IFrameResource**>, 또는 <**HTMLResouce**> 합니다. <**StaticResource**> HTML이 아닌 리소스를 설명 하 고 hello 리소스가 표시 되는 방법을 지정 하는 creativeType 특성을 정의 합니다.

이미지/gif, jpeg 이미지 /, 이미지/png – html에서 hello 리소스가 표시 되는 <**img**> 태그입니다.

응용 프로그램/x-javascript – hello 리소스 HTML에 표시 됩니다 <**스크립트**> 태그입니다.

응용 프로그램/x-shockwave-깜박임 – hello 리소스 Flash player에 표시 됩니다.

**IFrameResource**는 IFrame에 표시할 수 있는 HTML 리소스를 설명합니다. **HTMLResource**는 웹 페이지에 삽입할 수 있는 HTML 코드 조각을 설명합니다. **TrackingEvents** hello 이벤트가 발생할 때 URI toorequest hello 및 추적 이벤트를 지정 합니다. 이 샘플 hello에서는 acceptInvitation 및 축소 이벤트가 추적 됩니다. Hello에 대 한 자세한 내용은 **NonLinearAds** 요소와 그 자식 IAB.NET/VAST를 참조 하십시오. 해당 hello 참고 **TrackingEvents** hello 내에 **NonLinearAds** hello 아닌 요소 **비선형** 요소입니다.

동반 광고는 <CompanionAds> 요소 내에서 정의됩니다. hello <CompanionAds> 하나 이상의 요소가 포함 될 수 있습니다 <Companion> 요소입니다. 각 <Companion> 요소는 동반 광고를 설명 하 고 포함 될 수 있습니다는 <StaticResource>, <IFrameResource>, 또는 <HTMLResource> 는에 지정 된 hello는 비선형 광고의 방식으로 동일 합니다. VAST 파일에는 여러 동반 광고 포함 될 수 있습니다 및 hello 플레이어 응용 프로그램에 가장 적합 한 ad toodisplay hello 선택할 수 있습니다. VAST에 대한 자세한 내용은 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)(영문)을 참조하세요.

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>디지털 VMAP(Video Multiple Ad Playlist) 파일 사용
VMAP 파일 toospecify 중간 광고 발생 하는 경우, 기간 각 구분선은, 나누기를 내에서 광고를 표시할 수 있습니다 하 고 있습니다 수 유형의 광고 도중 표시할 합니다. 단일 광고 재생을 정의 하는 예제 VMAP 파일에서 다음 hello:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

VMAP 파일은 각각 광고를 정의하는 하나 이상의 <AdBreak> 요소를 포함하는 <VMAP> 요소로 시작합니다. 각 광고는 광고 유형, 광고 ID 및 시간 오프셋을 지정합니다. hello breakType 특성 지정 hello 재생 중 재생할 수 있는 광고의 hello 유형을: 선형, 비선형 또는 표시 합니다. 표시 광고를 tooVAST 동반 광고를 매핑합니다. 둘 이상의 광고 유형은 공백 없이 쉼표로 구분된 목록으로 지정할 수 있습니다. hello breakID는 hello ad에 대 한 선택적 식별자입니다. hello timeoffset은 광고 hello ad를 표시 하는 경우 지정 합니다. Hello 같은 방법으로 다음 중 하나에 지정할 수 있습니다.

1. Time – hh:mm:ss 또는 hh:mm:ss.mmm 형식으로 지정합니다. 여기서 .mmm은 밀리초입니다. 이 특성의 hello 값 hello 중간 광고의 시작 하는 hello 비디오 타임 라인 toohello hello부터에서 hello 시간을 지정합니다.
2. 백분율 – n hello 광고를 재생 하기 전에 hello 비디오 타임 라인 tooplay의 hello 백분율을은 n % 형식
3. 시작/끝 – hello 비디오 표시 된 후 전이나 광고를 표시 해야 함을 지정 합니다.
4. 위치 – 때 hello 중간 광고의 hello 타이밍을 알 수 없는 라이브 스트리밍과 같이 중간 광고의 hello 순서를 지정 합니다. 각 중간 광고의 hello 순서는 여기서 n은 정수 1 이상 hello #n 형식으로 지정 됩니다. 1은 hello 광고를 재생 해야 hello 첫 번째 기회에 2는 hello 두 번째 기회에 등 hello 광고를 재생 해야 합니다.

Hello 내에서 <**AdBreak**> 요소 하나가 될 수 있습니다 <**AdSource**> 요소입니다. hello <**AdSource**> 요소 hello 다음 특성을 포함 합니다.

1. Id – hello ad 원본에 대 한 식별자를 지정 합니다.
2. hello 광고 재생 중에 여러 광고를 표시할 수 있는지 여부를 지정 하는 부울 값 allowmultipleads – 중간
3. followRedirects – 비디오 플레이어 hello를 따라야 하는 경우를 지정 하는 선택적 부울 값 광고 응답 내에서 리디렉션을 수행

hello <**AdSource**> 요소에 인라인 광고 응답 또는 참조 tooan 광고 응답 hello 플레이어를 제공 합니다. Hello 요소 다음 중 하나를 포함할 수 있습니다.

* <VASTAdData>VAST 광고 응답이 hello VMAP 파일 내에 포함 되어 나타냅니다.
* <AdTagURI>는 다른 시스템에서 나오는 광고 응답을 참조하는 URI입니다.
* <CustomAdData>는 비 VAST 응답을 나타내는 임의 문자열입니다.

이 예제에서 인라인 광고 응답은 VAST 광고 응답을 포함하는 <VASTAdData> 요소로 지정합니다. Hello에 대 한 자세한 내용은 다른 요소 참조 [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap)합니다.

hello <**AdBreak**> 요소가 하나 포함할 수도 있습니다 <**TrackingEvents**> 요소입니다. hello <**TrackingEvents**> 요소를 있습니다 tootrack hello 시작 또는 끝 광고 또는 hello 광고 재생 하는 동안 오류가 발생 했는지 여부입니다. hello <**TrackingEvents**> 요소가 하나 이상 포함 <**추적**> 요소를 각각 추적 이벤트 및 추적 URI 지정 합니다. hello 가능한 추적 이벤트는 같습니다.

1. breakStart – 광고의 시작 부분 hello를 추적 합니다.
2. breakEnd – 광고의 트랙 hello 완료
3. 오류 – hello 광고 재생 중에 발생 한 오류를 추적 합니다.

다음 예제는 hello 추적 이벤트를 지정 하는 VMAP 파일을 보여 줍니다.

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Hello에 대 한 자세한 내용은 <**TrackingEvents**> 요소와 그 자식 http://iab.org/VMAP.pdf 참조

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>MAST(Media Abstract Sequencing Template) 파일 사용
MAST 파일 광고 표시 시기를 정의 하는 toospecify 트리거를 허용 합니다. hello 다음은 이전에 나오는 광고, 중간에 나오는 광고 및 후에 나오는 광고에 대 한 트리거를 포함 하는 예제 MAST 파일입니다.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



MAST 파일은 하나의 **triggers** 요소를 포함하는 **MAST** 요소로 시작합니다. hello <triggers> 요소 하나 이상 포함 **트리거** 는 광고를 재생 해야 하는 시기를 정의 하는 요소입니다. 

hello **트리거** 요소를 포함 한 **startConditions** 광고 tooplay 해야 시작 하는 시기를 지정 하는 요소입니다. hello **startConditions** 요소 하나 이상 포함 <condition> 요소입니다. 때 각 <condition> 트리거를 시작 하거나 인지 여부에 따라 해지 tootrue 평가 hello <condition> 내에 포함 된 한 **startConditions** 또는 **endConditions** 요소 각각. 때 여러 <condition> 요소가 있는는 암시적 OR로 처리 되며, tootrue 평가 되는 조건은 hello 트리거 tooinitiate 발생 합니다. <condition> 요소는 중첩될 수 있습니다. 때 자식 <condition> 요소는 미리 설정, 암시적 AND로 처리 되며, 모든 조건이 tootrue 트리거 tooinitiate hello에 대 한 계산 되어야 합니다. hello <condition> hello hello 상태 판단 기준을 정의 하는 특성을 다음 요소를 포함 합니다. 

1. **형식** – 조건, 이벤트 또는 속성의 hello 유형을 지정
2. **이름** – hello hello 속성 또는 이벤트 toobe 평가 하는 동안 사용 되는 이름
3. **값** – hello 속성을 평가 하는 값
4. **연산자** – 평가 하는 동안 작업 toouse hello: EQ (같음), NEQ (같지 않음), GTR (보다), GEQ (크거나 같음), LT (보다 작음), MOD (모듈로) (작거나 같음), LEQ

**endConditions**도 <condition> 요소를 포함합니다. Tootrue hello 트리거는 reset.hello 조건이 평가 되 면 <trigger> 포함 한 <sources> 하나 이상 포함 된 요소 <source> 요소입니다. hello <source> 요소 hello URI toohello 광고 응답 및 광고 응답의 hello 형식을 정의 합니다. 이 예제에서 URI가 주어진 tooa VAST 응답 합니다. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>VPAID(Video Player-Ad Interface Definition) 사용
VPAID는 실행 가능한 광고 단위가 toocommunicate 비디오 플레이어와 사용을 위한는 API입니다. 이를 통해 높은 수준의 대화형 광고 환경이 가능합니다. hello 사용자 hello ad와 상호 작용할 수 및 hello ad hello 뷰어 수행한 tooactions 응답할 수 있습니다. 예를 들어 광고 자세한 정보나 길이가 긴 버전 hello ad의 hello 사용자 tooview 수 있는 단추가 표시 될 수 있습니다. hello 비디오 플레이어는 VPAID API hello를 지원 해야 하 고 hello 실행 가능한 광고는 hello API를 구현 해야 합니다. 플레이어가 광고 서버 hello 서버에서 광고를 요청 하는 경우는 VPAID 광고가 포함 된 VAST 응답을 사용 하 여 응답할 수 있습니다.

실행 가능한 광고는 Adobe Flash™ 또는 JavaScript와 같이 웹 브라우저에서 실행할 수 있는 런타임 환경에서 실행되어야 하는 코드로 생성됩니다. 광고 서버는 VPAID 광고가 포함 된 VAST 응답 반환 되 면 hello에서 hello apiFramework 특성의 값을 hello <MediaFile> 요소가 "VPAID" 여야 합니다. 이 특성에 포함 된 hello ad 광고가 VPAID 실행 가능을 지정 합니다. hello 유형 특성을 설정 해야 toohello MIME 형식의 hello "응용 프로그램/x-shockwave-깜박임" 또는 "응용 프로그램/x-javascript"와 같은 실행 합니다. hello 아래 XML 조각 표시 hello <MediaFile> VPAID 실행 가능 광고가 포함 된 VAST 응답의 요소입니다. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


실행 가능한 광고는 hello를 사용 하 여 초기화 될 수 있습니다 <AdParameters> hello 내의 요소 <Linear> 또는 <NonLinear> VAST 응답의 요소입니다. Hello에 대 한 자세한 내용은 <AdParameters> 요소 참조 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)합니다. Hello VPAID API에 대 한 자세한 내용은 참조 [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf)합니다.

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>광고 지원이 포함된 Windows 또는 Windows Phone 8 플레이어 구현
Microsoft Media Platform hello: Windows 8 용 플레이어 프레임 워크 및 Windows Phone 8 tooimplement 사용 하 여 비디오 플레이어 응용 프로그램 프레임 워크를 hello 하는 방법을 보여 주는 샘플 응용 프로그램의 컬렉션을 포함 합니다. Hello 플레이어 프레임 워크 및 hello 샘플에서 다운로드할 수 있습니다 [Windows 8 용 플레이어 프레임 워크 및 Windows Phone 8](https://playerframework.codeplex.com)합니다.

Hello Microsoft.PlayerFramework.Xaml.Samples 솔루션을 열 수의 hello 프로젝트 내에서 폴더를 표시 됩니다. Advertising 폴더에 hello hello 예제 코드 관련 toocreating 광고를 지 원하는 비디오 플레이어를 포함합니다. XAML/cs 파일 수는 보기의 각 방법을 내부 hello 광고 폴더는 다른 방식으로 tooinsert 광고 합니다. hello 다음 목록에서는 각 설명 합니다.

* AdPodPage.xaml은 toodisplay 광고 포드 방법을 보여 줍니다.
* AdSchedulingPage.xaml 표시 방법을 tooschedule 광고 합니다.
* FreeWheelPage.xaml은 toouse FreeWheel 플러그 인 tooschedule 광고 hello 하는 방법을 보여 줍니다.
* MastPage.xaml 표시 방법을 tooschedule 광고 MAST 파일입니다.
* ProgrammaticAdPage.xaml은 tooprogrammatically 비디오에 광고를 예약 하는 방법을 보여 줍니다.
* ScheduleClipPage.xaml 표시 방법을 tooschedule 광고는 VAST 파일 없이도 합니다.
* VastLinearCompanionPage.xaml 표시 방법을 tooinsert 선형 광고 및 동반 광고 합니다.
* VastNonLinearPage.xaml 표시 방법을 tooinsert는 비선형 광고 합니다.
* VmapPage.xaml 표시 방법을 toospecify 광고 VMAP 파일입니다.

이러한 각 샘플 hello 플레이어 프레임 워크에 의해 정의 된 hello MediaPlayer 클래스를 사용 합니다. 대부분 샘플에서는 다양한 광고 응답 형식에 대한 지원을 추가하는 플러그 인을 사용합니다. hello ProgrammaticAdPage 샘플 MediaPlayer 인스턴스와 프로그래밍 방식으로 상호 작용합니다.

### <a name="adpodpage-sample"></a>AdPodPage 샘플
이 샘플에서는 hello AdSchedulerPlugin toodefine 때 toodisplay 광고 합니다. 이 예에서는 중간에 나오는 광고가 5 초 후에 재생 하는 예약 된 toobe입니다. hello 광고 포드 (순서 대로 광고 toodisplay 그룹)는 광고 서버에서 반환 되는 VAST 파일에서 지정 됩니다. hello URI toohello VAST 파일 hello에 지정 된 <RemoteAdSource> 요소입니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

AdSchedulerPlugin hello에 대 한 자세한 내용은 참조 하세요. [hello Windows 8 및 Windows Phone 8 플레이어 프레임 워크에서에서 광고](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
또한이 샘플 AdSchedulerPlugin hello를 사용합니다. 세 가지 광고인 재생 전 광고, 재생 중 광고 및 재생 후 광고를 예약합니다. 에 지정 된 각 광고에 대 한 URI toohello VAST hello는 <RemoteAdSource> 요소입니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
이 샘플에서는 FreeWheelPlugin 광고 콘텐츠 및 광고 예약 정보를 지정 하는 지점 tooa SmartXML 파일 URI를 지정 하는 원본 특성을 지정 하는 hello를 사용 합니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
이 샘플에서는 MAST 파일 toouse 수 있는 MastSchedulerPlugin hello 합니다. hello 소스 특성 hello MAST 파일의 hello 위치를 지정합니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
이 샘플은 프로그래밍 방식으로 hello MediaPlayer 상호 작용합니다. hello ProgrammaticAdPage.xaml 파일 MediaPlayer hello를 인스턴스화합니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

hello ProgrammaticAdPage.xaml.cs 파일은 AdHandlerPlugin 만듭니다, 그리고 광고를 표시 하 고 URI tooa VAST 파일을 지정 하는 RemoteAdSource 로드 하 고을 수행 하는 hello MarkerReached 이벤트에 대 한 처리기를 추가 하는 다음 TimelineMarker toospecify 추가 hello ad 합니다.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
이 샘플에서는 hello 광고를 포함 하는.wmv 파일을 지정 하 여 hello AdSchedulerPlugin tooschedule 중간에 나오는 광고를 사용 합니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
이 샘플에서는 어떻게 toouse hello AdSchedulerPlugin tooschedule 중간에 나오는 선형 광고를 동반 광고를 보여 줍니다. hello <RemoteAdSource> 요소 hello VAST 파일의 hello 위치를 지정 합니다.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
이 샘플에서는 선형 및 비선형 광고 AdSchedulerPlugin tooschedule hello를 사용 합니다. VAST 파일 위치 hello hello로 지정 된 <RemoteAdSource> 요소입니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
이 예제 VMAP 파일을 사용 하 여 hello VmapSchedulerPlugin tooschedule 광고를 사용 합니다. hello URI toohello VMAP 파일의 hello hello 소스 특성에 지정 된 <VmapSchedulerPlugin> 요소입니다.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>광고 지원이 포함된 iOS 비디오 플레이어 구현
Microsoft Media Platform hello: iOS 용 플레이어 프레임 워크 tooimplement 사용 하 여 비디오 플레이어 응용 프로그램 프레임 워크를 hello 하는 방법을 보여 주는 샘플 응용 프로그램의 컬렉션을 포함 합니다. Hello 플레이어 프레임 워크 및 hello 샘플에서 다운로드할 수 있습니다 [Azure 미디어 플레이어 프레임 워크](https://github.com/Azure/azure-media-player-framework)합니다. hello github 페이지에 링크 tooa hello 플레이어 프레임 워크 및 소개 toohello 플레이어 샘플에 대 한 추가 정보를 포함 하는 Wiki: [Azure 미디어 플레이어 Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework)합니다.

### <a name="scheduling-ads-with-vmap"></a>VMAP를 사용하여 광고 예약
hello 방법을 예제와 다음 tooschedule 광고 VMAP 파일을 사용 합니다.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>VAST를 사용하여 광고 예약
hello 다음 샘플에서는 어떻게 tooschedule 런타임에 바인딩 VAST 광고 합니다.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   hello 다음 샘플에서는 어떻게 tooschedule 바인딩 VAST 광고를 초기 합니다.
경우에 초기 바인딩 VAST 광고 //Download hello VAST 파일 예: 4 일정 (! [ framework.adResolver downloadManifest: 매니페스트 및 withURL: [NSURL URLWithString: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[자체 logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

hello 다음 샘플에서는 어떻게 tooinsert 대략적인 잘라내기 편집 (소스)를 사용 하 여 광고

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

hello 다음 예제에서는 어떻게 tooschedule 광고 포드

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

hello 방법을 예제와 다음 tooschedule 스티커 중간에 나오는 광고 합니다. 뷰어 모든 검색 hello에 관계 없이 수행 되 면에 스티커는 광고 재생 됩니다.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

hello 방법을 예제와 다음 tooschedule 스티커 중간에 나오는 광고 합니다. 팀 멤버는 광고 hello 지정 hello 비디오 타임 라인 상의 지점에 도달할 때마다 표시 됩니다.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


hello 다음 샘플에서는 어떻게 tooschedule 이후에 나오는 광고 합니다.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

hello 다음 샘플에서는 어떻게 tooschedule 나오는 광고 합니다.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

다음 예제는 hello tooschedule 중간에 나오는 광고 오버레이 사용 방법을 보여 줍니다.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[비디오 플레이어 응용 프로그램 개발](media-services-develop-video-players.md)

