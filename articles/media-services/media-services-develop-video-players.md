---
title: "비디오 플레이어 응용 프로그램 개발"
description: "이 토픽에서는 Media Services의 스트리밍 미디어를 사용할 수 있는 고유한 클라이언트 응용 프로그램을 개발하는 데 사용할 수 있는 플레이어 프레임워크 및 플러그 인에 대한 링크를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 0e88baed8188890e80d4c2e7ee9d510fdabf6e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-video-player-applications"></a><span data-ttu-id="034ab-103">비디오 플레이어 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="034ab-103">Develop video player applications</span></span>
## <a name="overview"></a><span data-ttu-id="034ab-104">개요</span><span class="sxs-lookup"><span data-stu-id="034ab-104">Overview</span></span>
<span data-ttu-id="034ab-105">Azure 미디어 서비스는 iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 박스를 포함한 대부분의 플랫폼에서 풍부한 동적 클라이언트 플레이어 응용 프로그램을 만드는 데 필요한 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-105">Azure Media Services provides the tools you need to create rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="034ab-106">또한 이 토픽에서는 Azure Media Services의 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램을 개발하는 데 사용할 수 있는 SDK 및 플레이어 프레임워크 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-106">This topic also provides links to SDKs and Player Frameworks that you can use to develop your own client applications that can consume streaming media from Azure Media Services.</span></span>

>[!NOTE]
><span data-ttu-id="034ab-107">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="034ab-108">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
 
## <a name="azure-media-player"></a><span data-ttu-id="034ab-109">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="034ab-109">Azure Media Player</span></span>
<span data-ttu-id="034ab-110">[Azure 미디어 플레이어](http://aka.ms/ampinfo) 는 다양한 브라우저 및 장치의 Microsoft Azure 미디어 서비스에서 미디어 콘텐츠를 재생하기 위해 작성된 웹 비디오 플레이어입니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-110">[Azure Media Player](http://aka.ms/ampinfo) is a web video player built to play back media content from Microsoft Azure Media Services on a wide variety of browsers and devices.</span></span> <span data-ttu-id="034ab-111">Azure 미디어 플레이어는 풍부해진 적응 스트리밍 환경을 제공할 수 있는 HTML5, 미디어 원본 확장(MSE) 및 암호화된 미디어 확장(EME) 등의 업계 표준을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-111">Azure Media Player utilizes industry standards, such as HTML5, Media Source Extensions (MSE), and Encrypted Media Extensions (EME) to provide an enriched adaptive streaming experience.</span></span> <span data-ttu-id="034ab-112">이러한 표준을 장치 또는 브라우저에서 사용할 수 없는 경우, Azure 미디어 플레이어는 Flash 및 Silverlight를 대체 기술로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-112">When these standards are not available on a device or in a browser, Azure Media Player uses Flash and Silverlight as fallback technology.</span></span> <span data-ttu-id="034ab-113">사용된 재생 기술에 관계 없이 개발자는 API에 액세스하기 위한 통합된 JavaScript 인터페이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-113">Regardless of the playback technology used, developers will have a unified JavaScript interface to access APIs.</span></span> <span data-ttu-id="034ab-114">이렇게 하면 Azure 미디어 서비스에서 제공하는 콘텐츠를 추가 작업 없이 광범위한 장치 및 브라우저에서 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-114">This allows for content served by Azure Media Services to be played across a wide-range of devices and browsers without any extra effort.</span></span>

<span data-ttu-id="034ab-115">Microsoft Azure 미디어 서비스에서 컨텐츠를 DASH, 부드러운 스트리밍 및 HLS 스트리밍 형식으로 제공하여 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-115">Microsoft Azure Media Services allows for content to be served up with DASH, Smooth Streaming, and HLS streaming formats to play back content.</span></span> <span data-ttu-id="034ab-116">Azure 미디어 플레이어는 이러한 다양한 형식을 고려하여 플랫폼/브라우저 기능에 따라 최상의 링크를 자동으로 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-116">Azure Media Player takes into account these various formats and automatically plays the best link based on the platform/browser capabilities.</span></span> <span data-ttu-id="034ab-117">Microsoft Azure 미디어 서비스에서 PlayReady 암호화 또는 AES 128 비트 봉투 암호화로 자산의 동적 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-117">Microsoft Azure Media Services also allows for dynamic encryption of assets with PlayReady encryption or AES-128 bit envelope encryption.</span></span> <span data-ttu-id="034ab-118">적절하게 구성된 경우 Azure 미디어 플레이어를 사용하여 PlayReady의 및 AES 128 비트 암호화된 콘텐츠를 암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-118">Azure Media Player allows for decryption of PlayReady and AES-128 bit encrypted content when appropriately configured.</span></span> 

<span data-ttu-id="034ab-119">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="034ab-119">For more information:</span></span>

* [<span data-ttu-id="034ab-120">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="034ab-120">Azure Media Player</span></span>](http://aka.ms/ampinfo)
* [<span data-ttu-id="034ab-121">Azure 미디어 플레이어 서비스 설명서</span><span class="sxs-lookup"><span data-stu-id="034ab-121">Azure Media Player Documentation</span></span>](http://aka.ms/ampdocs) 
* [<span data-ttu-id="034ab-122">Azure 미디어 플레이어 시작 블로그</span><span class="sxs-lookup"><span data-stu-id="034ab-122">Azure Media Player Getting Started Blog</span></span>](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [<span data-ttu-id="034ab-123">최신 Azure 미디어 플레이어 관련 최신 정보를 얻으려면 등록</span><span class="sxs-lookup"><span data-stu-id="034ab-123">Sign up to stay up to date with the latest from Azure Media Player</span></span>](http://aka.ms/ampsignup)
* [<span data-ttu-id="034ab-124">새로운 기능 요청, 아이디어, 사용자 의견 추가</span><span class="sxs-lookup"><span data-stu-id="034ab-124">Add new feature requests, ideas, feedback</span></span>](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a><span data-ttu-id="034ab-125">플레이어 응용 프로그램을 만들기 위한 다른 도구</span><span class="sxs-lookup"><span data-stu-id="034ab-125">Other Tools for Creating Player Applications</span></span>
<span data-ttu-id="034ab-126">또한 다음 SDK 중 하나를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-126">You can also use any of the following SDKs:</span></span>

* [<span data-ttu-id="034ab-127">부드러운 스트리밍 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="034ab-127">Smooth Streaming Client SDK</span></span>](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [<span data-ttu-id="034ab-128">부드러운 스트리밍 Windows 스토어 앱</span><span class="sxs-lookup"><span data-stu-id="034ab-128">Smooth Streaming Windows Store App</span></span>](media-services-build-smooth-streaming-apps.md)
* [<span data-ttu-id="034ab-129">Microsoft Media Platform: 플레이어 프레임워크</span><span class="sxs-lookup"><span data-stu-id="034ab-129">Microsoft Media Platform: Player Framework</span></span>](http://playerframework.codeplex.com/) 
* [<span data-ttu-id="034ab-130">HTML5 플레이어 프레임워크 설명서</span><span class="sxs-lookup"><span data-stu-id="034ab-130">HTML5 Player Framework Documentation</span></span>](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [<span data-ttu-id="034ab-131">OSMF용 Microsoft 부드러운 스트리밍 플러그인</span><span class="sxs-lookup"><span data-stu-id="034ab-131">Microsoft Smooth Streaming Plugin for OSMF</span></span>](https://www.microsoft.com/download/details.aspx?id=36057) 
* [<span data-ttu-id="034ab-132">Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스</span><span class="sxs-lookup"><span data-stu-id="034ab-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>](http://aka.ms/sspk) 
* [<span data-ttu-id="034ab-133">XBOX 비디오 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="034ab-133">XBOX Video Application Development</span></span>](http://xbox.create.msdn.com/) 

## <a name="advertising"></a><span data-ttu-id="034ab-134">광고</span><span class="sxs-lookup"><span data-stu-id="034ab-134">Advertising</span></span>
<span data-ttu-id="034ab-135">Azure 미디어 서비스는 Windows 미디어 플랫폼: 플레이어 프레임워크를 통해 광고 삽입에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-135">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="034ab-136">광고를 지원하는 플레이어 프레임워크는 Windows 8, Silverlight, Windows Phone 8 및 iOS 장치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-136">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="034ab-137">각 플레이어 프레임워크는 플레이어 응용 프로그램을 구현하는 방법을 보여주는 샘플 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-137">Each player framework contains sample code that shows you how to implement a player application.</span></span> <span data-ttu-id="034ab-138">미디어에 삽입할 수 있는 서로 다른 세 종류의 광고가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-138">There are three different kinds of ads you can insert into your media:</span></span>

<span data-ttu-id="034ab-139">선형-기본 비디오를 일시 중지하는 전체 프레임 광고</span><span class="sxs-lookup"><span data-stu-id="034ab-139">Linear – full frame ads that pause the main video</span></span>

<span data-ttu-id="034ab-140">비선형-기본 비디오를 재생할 때 표시되는 오버레이 광고로, 일반적으로 플레이어 내에 배치된 로고나 기타 정적 이미지</span><span class="sxs-lookup"><span data-stu-id="034ab-140">Nonlinear – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player</span></span>

<span data-ttu-id="034ab-141">동반-플레이어 외부에 표시되는 광고</span><span class="sxs-lookup"><span data-stu-id="034ab-141">Companion – ads that are displayed outside of the player</span></span>

<span data-ttu-id="034ab-142">광고는 기본 비디오 타임 라인에 언제든지 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-142">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="034ab-143">플레이어에 광고를 재생하는 시기 및 재생하는 광고를 알려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-143">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="034ab-144">이 작업은 표준 XML 기반 파일 집합을 사용하여 수행됩니다. VAST(Video Ad Service Template), VMAP(Digital Video Multiple Ad Playlist), MAST(Media Abstract Sequencing Template) 및 VPAID(Digital Video Player Ad Interface Definition).</span><span class="sxs-lookup"><span data-stu-id="034ab-144">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="034ab-145">VAST 파일은 표시할 광고를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-145">VAST files specify what ads to display.</span></span> <span data-ttu-id="034ab-146">VMAP 파일은 다양한 광고를 재생하고 VAST XML을 포함하는 시기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-146">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="034ab-147">또한 MAST 파일은 VAST XML도 포함할 수 있는 광고를 시퀀스하는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-147">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="034ab-148">VPAID 파일은 비디오 플레이어와 광고 또는 광고 서버 간의 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="034ab-148">VPAID files define an interface between the video player and the ad or ad server.</span></span> <span data-ttu-id="034ab-149">자세한 내용은 [광고 삽입](https://msdn.microsoft.com/library/dn387398.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="034ab-149">For more information, see [Inserting Ads](https://msdn.microsoft.com/library/dn387398.aspx).</span></span>

<span data-ttu-id="034ab-150">라이브 스트리밍 비디오의 선택 캡션 및 광고 지원에 대한 정보는 [지원되는 선택 캡션 및 광고 삽입 표준](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="034ab-150">For information about closed captioning and ads support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="034ab-151">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="034ab-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="034ab-152">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="034ab-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="034ab-153">참고 항목</span><span class="sxs-lookup"><span data-stu-id="034ab-153">See Also</span></span>
[<span data-ttu-id="034ab-154">DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함</span><span class="sxs-lookup"><span data-stu-id="034ab-154">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

[<span data-ttu-id="034ab-155">GitHub dash.js 리포지토리</span><span class="sxs-lookup"><span data-stu-id="034ab-155">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js)

