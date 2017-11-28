---
title: "클라이언트 쪽에 광고 삽입 | Microsoft 문서"
description: "이 토픽에서는 클라이언트 쪽에 광고를 삽입하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="1728c-103">클라이언트 쪽에 광고 삽입</span><span class="sxs-lookup"><span data-stu-id="1728c-103">Inserting ads on the client side</span></span>
<span data-ttu-id="1728c-104">이 토픽에서는 클라이언트 쪽에 다양한 유형의 광고를 삽입하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="1728c-105">라이브 스트리밍 비디오에서 캡션 및 광고 지원에 대한 정보는 [지원되는 캡션 및 Ad 삽입 표준](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="1728c-106">Azure 미디어 플레이어는 현재 광고를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="1728c-107"><a id="insert_ads_into_media"></a>미디어에 광고 삽입</span><span class="sxs-lookup"><span data-stu-id="1728c-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="1728c-108">Azure 미디어 서비스는 Windows 미디어 플랫폼: 플레이어 프레임워크를 통해 광고 삽입에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="1728c-109">광고를 지원하는 플레이어 프레임워크는 Windows 8, Silverlight, Windows Phone 8 및 iOS 장치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="1728c-110">각 플레이어 프레임워크는 플레이어 응용 프로그램을 구현하는 방법을 보여주는 샘플 코드를 포함합니다. 미디어 목록에 삽입할 수 있는 서로 다른 세 종류의 광고가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="1728c-111">**선형** -기본 비디오를 일시 중지하는 전체 프레임 광고</span><span class="sxs-lookup"><span data-stu-id="1728c-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="1728c-112">**비선형** -기본 비디오를 재생할 때 표시되는 오버레이 광고로, 일반적으로 플레이어 내에 배치된 로고나 기타 정적 이미지</span><span class="sxs-lookup"><span data-stu-id="1728c-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="1728c-113">**동반** -플레이어 외부에 표시되는 광고</span><span class="sxs-lookup"><span data-stu-id="1728c-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="1728c-114">광고는 기본 비디오 타임 라인에 언제든지 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="1728c-115">플레이어에 광고를 재생하는 시기 및 재생하는 광고를 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="1728c-116">이 작업은 표준 XML 기반 파일 집합을 사용하여 수행됩니다. VAST(Video Ad Service Template), VMAP(Digital Video Multiple Ad Playlist), MAST(Media Abstract Sequencing Template) 및 VPAID(Digital Video Player Ad Interface Definition).</span><span class="sxs-lookup"><span data-stu-id="1728c-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="1728c-117">VAST 파일은 표시할 광고를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="1728c-118">VMAP 파일은 다양한 광고를 재생하고 VAST XML을 포함하는 시기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="1728c-119">또한 MAST 파일은 VAST XML도 포함할 수 있는 광고를 시퀀스하는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="1728c-120">VPAID 파일은 비디오 플레이어와 광고 또는 광고 서버 간의 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="1728c-121">각 플레이어 프레임워크는 서로 다르게 작동하고 각각 별도 토픽에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="1728c-122">이 토픽에서는 광고를 삽입하는 데 사용되는 기본 메커니즘을 설명합니다. 비디오 플레이어 응용 프로그램은 광고 서버에서 광고를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="1728c-123">광고 서버는 다양한 방법으로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="1728c-124">VAST 파일 반환</span><span class="sxs-lookup"><span data-stu-id="1728c-124">Return a VAST file</span></span>
* <span data-ttu-id="1728c-125">VMAP 파일 반환(포함된 VAST와 함께)</span><span class="sxs-lookup"><span data-stu-id="1728c-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="1728c-126">MAST 파일 반환(포함된 VAST와 함께)</span><span class="sxs-lookup"><span data-stu-id="1728c-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="1728c-127">VAST 파일 반환(VPAID 광고와 함께)</span><span class="sxs-lookup"><span data-stu-id="1728c-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="1728c-128">VAST(Video Ad Service Template) 파일 사용</span><span class="sxs-lookup"><span data-stu-id="1728c-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="1728c-129">VAST 파일은 표시할 광고를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="1728c-130">다음 XML은 선형 광고에 대한 VAST 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="1728c-131">선형 광고는 <**Linear**> 요소로 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="1728c-132">광고 기간, 추적 이벤트, 클릭 방문, 클릭 추적 및 다양한 **MediaFile** 요소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="1728c-133">추적 이벤트는 <**TrackingEvents**> 요소 내에서 지정되고, 이를 통해 광고 서버에서 광고를 보는 동안 발생하는 다양한 이벤트를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="1728c-134">이 경우 start, midpoint, complete 및 expand 이벤트가 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="1728c-135">start 이벤트는 광고가 표시될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="1728c-136">midpoint 이벤트는 광고 타임라인의 50% 이상이 표시되었을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="1728c-137">complete 이벤트는 광고가 끝까지 실행되었을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="1728c-138">expand 이벤트는 사용자가 비디오 플레이어를 전체 화면으로 확장할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="1728c-139">광고 방문은 <**VideoClicks**> 요소 내의 <**ClickThrough**> 요소로 지정되고, 사용자가 광고를 클릭할 때 표시할 리소스에 대한 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="1728c-140">클릭 추적은 <**VideoClicks**> 요소 내의 <**ClickTracking**> 요소로 지정되고, 사용자가 광고를 클릭할 때 플레이어에서 요청하는 추적 리소스를 지정합니다. <**MediaFile**> 요소는 광고의 특정 인코딩에 대한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="1728c-141"><**MediaFile**> 요소가 둘 이상 있으면 비디오 플레이어에서 플랫폼에 가장 적합한 인코딩을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="1728c-142">선형 광고는 지정된 순서대로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="1728c-143">이렇게 하려면 VAST 파일에 다른 <Ad> 요소를 추가하고 시퀀스 특성을 사용하여 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="1728c-144">다음 예제에서는 이에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="1728c-145">비선형 광고도 <Creative> 요소에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="1728c-146">다음 예제에서는 비선형 광고를 설명하는 <Creative> 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="1728c-147"><**NonLinearAds**> 요소에는 각각 비선형 광고를 설명할 수 있는 <**NonLinear**> 요소가 둘 이상 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="1728c-148"><**NonLinear**> 요소는 비선형 광고의 리소스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="1728c-149">리소스는 <**StaticResouce**>, <**IFrameResource**> 또는 <**HTMLResouce**>일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="1728c-150"> <**StaticResource**>는 비 HTML 리소스를 설명하고, 다음과 같이 리소스가 표시되는 방식을 지정하는 creativeType 특성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="1728c-151">Image/gif, image/jpeg, image/png – 리소스가 HTML <**img**> 태그에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="1728c-152">Application/x-javascript – 리소스가 HTML <**script**> 태그에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="1728c-153">Application/x-shockwave-flash – 리소스가 Flash Player에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="1728c-154">**IFrameResource**는 IFrame에 표시할 수 있는 HTML 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="1728c-155">**HTMLResource**는 웹 페이지에 삽입할 수 있는 HTML 코드 조각을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="1728c-156">**TrackingEvents**는 추적 이벤트와 이벤트가 발생할 때 요청할 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="1728c-157">이 샘플에서 acceptInvitation 및 collapse 이벤트가 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="1728c-158">**NonLinearAds** 요소 및 해당 자식에 대한 자세한 내용은 IAB.NET/VAST를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="1728c-159">**TrackingEvents** 요소는 **NonLinear** 요소가 아닌 **NonLinearAds** 요소 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="1728c-160">동반 광고는 <CompanionAds> 요소 내에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="1728c-161"><CompanionAds> 요소에는 하나 이상의 <Companion> 요소가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="1728c-162">각 <Companion> 요소는 동반을 설명하며, 비선형 광고에서와 같은 방법으로 지정되는 <StaticResource>, <IFrameResource> 또는 <HTMLResource>를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="1728c-163">VAST 파일은 여러 동반 광고를 포함할 수 있고 플레이어 응용 프로그램은 표시할 가장 적합한 광고를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="1728c-164">VAST에 대한 자세한 내용은 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="1728c-165">디지털 VMAP(Video Multiple Ad Playlist) 파일 사용</span><span class="sxs-lookup"><span data-stu-id="1728c-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="1728c-166">VMAP 파일을 사용하여 광고가 발생하는 시기, 각 광고가 지속되는 기간, 광고 시간 내에 표시될 수 있는 광고 수, 광고 시간 중에 표시될 수 있는 광고 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="1728c-167">단일 광고를 정의하는 예제 VMAP 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="1728c-168">VMAP 파일은 각각 광고를 정의하는 하나 이상의 <AdBreak> 요소를 포함하는 <VMAP> 요소로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="1728c-169">각 광고는 광고 유형, 광고 ID 및 시간 오프셋을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="1728c-170">breakType 특성은 광고 중에 표시할 수 있는 광고 유형을 선형, 비선형 또는 표시 중에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="1728c-171">표시 광고는 VAST 동반 광고에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="1728c-172">둘 이상의 광고 유형은 공백 없이 쉼표로 구분된 목록으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="1728c-173">breakID는 광고의 선택적 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="1728c-174">timeOffset은 광고가 표시되어야 하는 시기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="1728c-175">다음 방법의 하나로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="1728c-176">Time – hh:mm:ss 또는 hh:mm:ss.mmm 형식으로 지정합니다. 여기서 .mmm은 밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="1728c-177">이 특성 값은 비디오 타임라인 시작부터 광고 시작까지 지나는 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="1728c-178">Percentage – n% 형식으로 지정합니다. 여기서 n은 광고를 재생하기 전에 재생할 비디오 타임라인의 백분율입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="1728c-179">Start/End – 비디오가 표시되기 전이나 후에 광고가 표시되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="1728c-180">Position – 라이브 스트리밍과 같이 광고 타이밍을 알 수 없을 때 광고 순서를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="1728c-181">각 광고 순서는 #n 형식으로 지정합니다. 여기서 n은 정수 1 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="1728c-182">1은 광고가 첫 번째 기회에 재생되어야 함을 나타내고, 2는 광고가 두 번째 기회에 재생되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="1728c-183"><**AdBreak**> 요소 내에는 <**AdSource**> 요소 하나가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="1728c-184"><**AdSource**> 요소는 다음 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="1728c-185">Id – 광고 소스의 식별자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="1728c-186">allowMultipleAds – 광고 중에 여러 광고를 표시할 수 있는지를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="1728c-187">followRedirects – 비디오 플레이어가 광고 응답 내에서 리디렉션을 제공해야 하는지 지정하는 선택적 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="1728c-188"><**AdSource**> 요소는 플레이어에 인라인 광고 응답이나 광고 응답에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="1728c-189">다음 요소의 하나를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="1728c-190"><VASTAdData>는 VAST 광고 응답이 VMAP 파일 내에 포함됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="1728c-191"><AdTagURI>는 다른 시스템에서 나오는 광고 응답을 참조하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="1728c-192"><CustomAdData>는 비 VAST 응답을 나타내는 임의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="1728c-193">이 예제에서 인라인 광고 응답은 VAST 광고 응답을 포함하는 <VASTAdData> 요소로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="1728c-194">기타 요소에 대한 자세한 내용은 [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="1728c-195"><**AdBreak**> 요소는 하나의 <**TrackingEvents**> 요소도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="1728c-196"><**TrackingEvents**> 요소를 사용하여 광고의 시작 또는 종료를 추적하거나 광고 중에 오류가 발생했는지를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="1728c-197"><**TrackingEvents**> 요소는 각각 추적 이벤트와 추적 URI를 지정하는 <**Tracking**> 요소를 하나 이상 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="1728c-198">가능한 추적 이벤트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="1728c-199">breakStart – 광고의 시작을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="1728c-200">breakStart – 광고의 완료를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="1728c-201">error – 광고 중에 발생한 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="1728c-202">다음 예제에서는 추적 이벤트를 지정하는 VMAP 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="1728c-203"><**TrackingEvents**> 요소 및 해당 자식에 대한 자세한 내용은 http://iab.org/VMAP.pdf를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="1728c-204">MAST(Media Abstract Sequencing Template) 파일 사용</span><span class="sxs-lookup"><span data-stu-id="1728c-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="1728c-205">MAST 파일을 사용하여 광고가 표시되는 시기를 정의하는 트리거를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="1728c-206">재생 전 광고, 재생 중 광고 및 재생 후 광고에 대한 트리거를 포함하는 예제 MAST 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="1728c-207">MAST 파일은 하나의 **triggers** 요소를 포함하는 **MAST** 요소로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="1728c-208"><triggers> 요소는 광고가 재생되는 시기를 정의하는 **trigger** 요소를 하나 이상 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="1728c-209">**trigger** 요소는 광고 재생이 시작되는 시기를 지정하는 **startConditions** 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="1728c-210">**startConditions** 요소는 <condition> 요소를 하나 이상 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="1728c-211">각 <condition>이 true로 평가되면 <condition>이 각각 **startConditions** 또는 **endConditions** 요소 안에 포함되는지에 따라 트리거가 시작되거나 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="1728c-212">여러 <condition> 요소가 있으면 암시적 OR로 처리되고, 모든 조건이 true로 평가되어 트리거가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="1728c-213"><condition> 요소는 중첩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-213"><condition> elements can be nested.</span></span> <span data-ttu-id="1728c-214">자식 <condition> 요소가 기본 설정되면 암시적 AND로 처리되고, 트리거가 시작되려면 모든 조건이 true로 평가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="1728c-215"><condition> 요소는 조건을 정의하는 다음 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="1728c-216">**type** – 조건, 이벤트 또는 속성 유형 지정</span><span class="sxs-lookup"><span data-stu-id="1728c-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="1728c-217">**name** – 평가 중에 사용할 속성 또는 이벤트의 이름</span><span class="sxs-lookup"><span data-stu-id="1728c-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="1728c-218">**value** – 속성을 평가할 기준 값</span><span class="sxs-lookup"><span data-stu-id="1728c-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="1728c-219">**operator** – 평가 중에 사용할 연산: EQ(같음), NEQ(같지 않음), GTR(보다 큼), GEQ(크거나 같음), LT(보다 작음), LEQ(작거나 같음), MOD(나머지)</span><span class="sxs-lookup"><span data-stu-id="1728c-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="1728c-220">**endConditions**도 <condition> 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="1728c-221">조건이 true로 평가되면 트리거가 재설정됩니다. <trigger> 요소는 하나 이상의 <source> 요소가 들어 있는 <sources> 요소도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="1728c-222"><source> 요소는 광고 응답에 대한 URI와 광고 응답 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="1728c-223">이 예제에서는 VAST 응답에 대한 URI가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="1728c-224">VPAID(Video Player-Ad Interface Definition) 사용</span><span class="sxs-lookup"><span data-stu-id="1728c-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="1728c-225">VPAID는 실행 가능한 광고 단위가 비디오 플레이어와 통신하는 데 사용되는 API입니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="1728c-226">이를 통해 높은 수준의 대화형 광고 환경이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="1728c-227">사용자는 광고를 조작할 수 있고 광고는 뷰어가 수행한 작업에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="1728c-228">예를 들어 사용자가 자세한 정보나 더 긴 광고를 볼 수 있도록 하는 단추가 광고에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="1728c-229">비디오 플레이어에서 VPAID API를 지원해야 하고 실행 가능한 광고에서 API를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="1728c-230">플레이어가 광고 서버의 광고를 요청하면 서버에서는 VPAID 광고가 포함된 VAST 응답으로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="1728c-231">실행 가능한 광고는 Adobe Flash™ 또는 JavaScript와 같이 웹 브라우저에서 실행할 수 있는 런타임 환경에서 실행되어야 하는 코드로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="1728c-232">광고 서버에서 VPAID 광고가 포함된 VAST 응답을 반환할 때 <MediaFile> 요소의 apiFramework 특성 값은 “VPAID”여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="1728c-233">이 특성은 포함된 광고가 VPAID 실행 가능한 광고임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="1728c-234">type 특성은 “application/x-shockwave-flash” 또는 “application/x-javascript”와 같은 실행 파일의 MIME 형식으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="1728c-235">다음 XML 조각에서는 VPAID 실행 가능한 광고가 포함된 VAST 응답의 <MediaFile> 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="1728c-236">실행 가능한 광고는 VAST 응답의 <Linear> 또는 <NonLinear> 요소 내에서 <AdParameters> 요소를 사용하여 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="1728c-237"><AdParameters> 요소에 대한 자세한 내용은 [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="1728c-238">VPAID API에 대한 자세한 내용은 [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1728c-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="1728c-239">광고 지원이 포함된 Windows 또는 Windows Phone 8 플레이어 구현</span><span class="sxs-lookup"><span data-stu-id="1728c-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="1728c-240">Microsoft Media Platform: Windows 8 및 Windows Phone 8용 플레이어 프레임워크에는 프레임워크를 사용하여 비디오 플레이어 응용 프로그램을 구현하는 방법을 보여 주는 샘플 응용 프로그램 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="1728c-241">[Windows 8 및 Windows Phone 8용 플레이어 프레임워크](https://playerframework.codeplex.com)에서 플레이어 프레임워크와 샘플을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="1728c-242">Microsoft.PlayerFramework.Xaml.Samples 솔루션을 열면 프로젝트 내에 많은 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="1728c-243">Advertising 폴더에는 광고 지원이 있는 비디오 플레이어를 만드는 방법과 관련된 샘플 코드가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="1728c-244">Advertising 폴더 내에는 각각 광고를 다르게 삽입하는 방법을 보여 주는 다양한 XAML/cs 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="1728c-245">다음 목록은 각각에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-245">The following list describes each:</span></span>

* <span data-ttu-id="1728c-246">AdPodPage.xaml - 광고 포드를 표시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="1728c-247">AdSchedulingPage.xaml - 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="1728c-248">FreeWheelPage.xaml - FreeWheel 플러그 인을 사용하여 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="1728c-249">MastPage.xaml - MAST 파일을 사용하여 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="1728c-250">ProgrammaticAdPage.xaml - 프로그래밍 방식으로 광고를 비디오에 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="1728c-251">ScheduleClipPage.xaml - VAST 파일 없이 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="1728c-252">VastLinearCompanionPage.xaml - 선형 및 동반 광고를 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="1728c-253">VastNonLinearPage.xaml - 비선형 광고를 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="1728c-254">VmapPage.xaml - VMAP 파일을 사용하여 광고를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="1728c-255">이들 샘플에서는 각각 플레이어 프레임워크에서 정의된 MediaPlayer 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="1728c-256">대부분 샘플에서는 다양한 광고 응답 형식에 대한 지원을 추가하는 플러그 인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="1728c-257">ProgrammaticAdPage 샘플에서는 MediaPlayer 인스턴스를 프로그래밍 방식으로 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="1728c-258">AdPodPage 샘플</span><span class="sxs-lookup"><span data-stu-id="1728c-258">AdPodPage Sample</span></span>
<span data-ttu-id="1728c-259">이 샘플에서는 AdSchedulerPlugin을 사용하여 광고를 표시할 시기를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="1728c-260">이 예제에서 재생 중 광고는 5초 후 재생되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="1728c-261">광고 포드(순서대로 표시할 광고 그룹)는 광고 서버에서 반환되는 VAST 파일로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="1728c-262">VAST 파일에 대한 URI는 <RemoteAdSource> 요소에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="1728c-263">AdSchedulerPlugin에 대한 자세한 내용은 [Windows 8 및 Windows Phone 8의 플레이어 프레임워크에서 광고](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="1728c-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="1728c-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="1728c-264">AdSchedulingPage</span></span>
<span data-ttu-id="1728c-265">이 샘플에서도 AdSchedulerPlugin을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="1728c-266">세 가지 광고인 재생 전 광고, 재생 중 광고 및 재생 후 광고를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="1728c-267">각 광고의 VAST 파일에 대한 URI는 <RemoteAdSource> 요소에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="1728c-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="1728c-268">FreeWheelPage</span></span>
<span data-ttu-id="1728c-269">이 샘플에서는 광고 예약 정보와 광고 콘텐츠를 지정하는 SmartXML 파일을 가리키는 URI를 지정하는 Source 특성을 지정하는 FreeWheelPlugin을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="1728c-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="1728c-270">MastPage</span></span>
<span data-ttu-id="1728c-271">이 샘플에서는 MAST 파일을 사용할 수 있게 하는 MastSchedulerPlugin을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="1728c-272">Source 특성은 MAST 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="1728c-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="1728c-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="1728c-274">이 샘플에서는 MediaPlayer를 프로그래밍 방식으로 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="1728c-275">ProgrammaticAdPage.xaml 파일은 MediaPlayer를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="1728c-276">ProgrammaticAdPage.xaml.cs 파일은 AdHandlerPlugin을 만들고, TimelineMarker를 추가하여 광고가 표시되어야 하는 시기를 지정하고, VAST 파일에 대한 URI를 지정하여 RemoteAdSource를 로드하는 MarkerReached 이벤트에 대한 처리기를 추가하고, 광고를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="1728c-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="1728c-277">ScheduleClipPage</span></span>
<span data-ttu-id="1728c-278">이 샘플에서는 AdSchedulerPlugin을 사용하여 광고가 포함된 .wmv 파일을 지정하는 방법으로 재생 중 광고를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="1728c-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="1728c-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="1728c-280">이 샘플에서는 AdSchedulerPlugin을 사용하여 재생 중 선형 광고를 동반 광고와 함께 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="1728c-281"><RemoteAdSource> 요소는 VAST 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="1728c-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="1728c-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="1728c-283">이 샘플에서는 AdSchedulerPlugin을 사용하여 선형 및 비선형 광고를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="1728c-284">VAST 파일 위치는 <RemoteAdSource> 요소로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="1728c-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="1728c-285">VMAPPage</span></span>
<span data-ttu-id="1728c-286">이 샘플에서는 VmapSchedulerPlugin을 사용하여 VMAP 파일을 통해 광고를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="1728c-287">VMAP 파일에 대한 URI는 <VmapSchedulerPlugin> 요소의 Source 특성으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="1728c-288">광고 지원이 포함된 iOS 비디오 플레이어 구현</span><span class="sxs-lookup"><span data-stu-id="1728c-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="1728c-289">Microsoft Media Platform: iOS용 플레이어 프레임워크에는 프레임워크를 사용하여 비디오 플레이어 응용 프로그램을 구현하는 방법을 보여 주는 샘플 응용 프로그램 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="1728c-290">[Azure 미디어 플레이어 프레임워크](https://github.com/Azure/azure-media-player-framework)에서 플레이어 프레임워크와 샘플을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="1728c-291">github 페이지에는 플레이어 프레임워크에 대한 추가 정보와 플레이어 샘플에 대한 소개가 포함된 Wiki 링크, [Azure 미디어 플레이어 Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="1728c-292">VMAP를 사용하여 광고 예약</span><span class="sxs-lookup"><span data-stu-id="1728c-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="1728c-293">다음 예제에서는 VMAP 파일을 사용하여 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="1728c-294">VAST를 사용하여 광고 예약</span><span class="sxs-lookup"><span data-stu-id="1728c-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="1728c-295">다음 샘플에서는 런타임에 바인딩 VAST 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="1728c-296">다음 샘플에서는 컴파일 시 바인딩 VAST 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="1728c-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="1728c-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="1728c-298">다음 샘플에서는 RCE(가편집)를 사용하여 광고를 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="1728c-299">다음 예제에서는 광고 포드를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="1728c-300">다음 예제에서는 비고정 재생 중 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="1728c-301">비고정 광고는 뷰어가 수행하는 검색과 관계없이 한 번만 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="1728c-302">다음 예제에서는 고정 재생 중 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="1728c-303">고정 광고는 비디오 타임라인의 지정된 지점에 도달할 때마다 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="1728c-304">다음 샘플에서는 재생 후 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="1728c-305">다음 샘플에서는 재생 전 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="1728c-306">다음 샘플에서는 재생 중 오버레이 광고를 예약하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1728c-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="1728c-307">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="1728c-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1728c-308">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="1728c-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1728c-309">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1728c-309">See Also</span></span>
[<span data-ttu-id="1728c-310">비디오 플레이어 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="1728c-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

