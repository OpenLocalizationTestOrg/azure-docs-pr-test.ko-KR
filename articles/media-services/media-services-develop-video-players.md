---
title: "aaaDevelop 비디오 플레이어 응용 프로그램"
description: "hello 항목 링크 tooPlayer 프레임 워크를 제공 하 고 플러그 인을 사용할 수 있는 toodevelop 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램입니다."
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
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a><span data-ttu-id="aa90e-103">비디오 플레이어 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="aa90e-103">Develop video player applications</span></span>
## <a name="overview"></a><span data-ttu-id="aa90e-104">개요</span><span class="sxs-lookup"><span data-stu-id="aa90e-104">Overview</span></span>
<span data-ttu-id="aa90e-105">Azure 미디어 서비스는 hello 도구 toocreate rich 필요 등 대부분의 플랫폼에 대 한 동적 클라이언트 플레이어 응용 프로그램: iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-105">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="aa90e-106">또한이 항목 링크 tooSDKs 및 사용할 수 있는 toodevelop Azure 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램 플레이어 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-106">This topic also provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Azure Media Services.</span></span>

>[!NOTE]
><span data-ttu-id="aa90e-107">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="aa90e-108">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
 
## <a name="azure-media-player"></a><span data-ttu-id="aa90e-109">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="aa90e-109">Azure Media Player</span></span>
<span data-ttu-id="aa90e-110">[Azure Media Player](http://aka.ms/ampinfo) 웹 비디오 플레이어 기반 tooplay 백 미디어 콘텐츠 Microsoft Azure 미디어 서비스에서 다양 한 브라우저와 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-110">[Azure Media Player](http://aka.ms/ampinfo) is a web video player built tooplay back media content from Microsoft Azure Media Services on a wide variety of browsers and devices.</span></span> <span data-ttu-id="aa90e-111">Azure 미디어 플레이어에서 HTML5, 미디어 원본 확장 (MSE) 및 암호화 된 미디어 확장 (EME) tooprovide 다양된 한 적응 스트리밍 환경 등의 업계 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-111">Azure Media Player utilizes industry standards, such as HTML5, Media Source Extensions (MSE), and Encrypted Media Extensions (EME) tooprovide an enriched adaptive streaming experience.</span></span> <span data-ttu-id="aa90e-112">이러한 표준을 장치 또는 브라우저에서 사용할 수 없는 경우, Azure 미디어 플레이어는 Flash 및 Silverlight를 대체 기술로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-112">When these standards are not available on a device or in a browser, Azure Media Player uses Flash and Silverlight as fallback technology.</span></span> <span data-ttu-id="aa90e-113">개발자는 hello 재생 기술을 사용에 관계 없이 통합된 JavaScript 인터페이스 tooaccess Api 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-113">Regardless of hello playback technology used, developers will have a unified JavaScript interface tooaccess APIs.</span></span> <span data-ttu-id="aa90e-114">따라서 콘텐츠는 광범위 한 장치 및 추가 작업 없이 브라우저에서 재생 하는 Azure 미디어 서비스 toobe 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-114">This allows for content served by Azure Media Services toobe played across a wide-range of devices and browsers without any extra effort.</span></span>

<span data-ttu-id="aa90e-115">Microsoft Azure 미디어 서비스 콘텐츠 toobe DASH, 부드러운 스트리밍 처리에 대 한 있으며 tooplay 형식 스트리밍을 HLS 콘텐츠를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-115">Microsoft Azure Media Services allows for content toobe served up with DASH, Smooth Streaming, and HLS streaming formats tooplay back content.</span></span> <span data-ttu-id="aa90e-116">Azure 미디어 플레이어는 고려 이러한 다양 한 형식 및 자동으로 재생 hello hello 플랫폼/브라우저의 기능에 따라 최상의 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-116">Azure Media Player takes into account these various formats and automatically plays hello best link based on hello platform/browser capabilities.</span></span> <span data-ttu-id="aa90e-117">Microsoft Azure 미디어 서비스에서 PlayReady 암호화 또는 AES 128 비트 봉투 암호화로 자산의 동적 암호화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-117">Microsoft Azure Media Services also allows for dynamic encryption of assets with PlayReady encryption or AES-128 bit envelope encryption.</span></span> <span data-ttu-id="aa90e-118">적절하게 구성된 경우 Azure 미디어 플레이어를 사용하여 PlayReady의 및 AES 128 비트 암호화된 콘텐츠를 암호 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-118">Azure Media Player allows for decryption of PlayReady and AES-128 bit encrypted content when appropriately configured.</span></span> 

<span data-ttu-id="aa90e-119">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa90e-119">For more information:</span></span>

* [<span data-ttu-id="aa90e-120">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="aa90e-120">Azure Media Player</span></span>](http://aka.ms/ampinfo)
* [<span data-ttu-id="aa90e-121">Azure 미디어 플레이어 서비스 설명서</span><span class="sxs-lookup"><span data-stu-id="aa90e-121">Azure Media Player Documentation</span></span>](http://aka.ms/ampdocs) 
* [<span data-ttu-id="aa90e-122">Azure 미디어 플레이어 시작 블로그</span><span class="sxs-lookup"><span data-stu-id="aa90e-122">Azure Media Player Getting Started Blog</span></span>](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [<span data-ttu-id="aa90e-123">Azure 미디어 플레이어에서 최신 hello로 toodate toostay 등록</span><span class="sxs-lookup"><span data-stu-id="aa90e-123">Sign up toostay up toodate with hello latest from Azure Media Player</span></span>](http://aka.ms/ampsignup)
* [<span data-ttu-id="aa90e-124">새로운 기능 요청, 아이디어, 사용자 의견 추가</span><span class="sxs-lookup"><span data-stu-id="aa90e-124">Add new feature requests, ideas, feedback</span></span>](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a><span data-ttu-id="aa90e-125">플레이어 응용 프로그램을 만들기 위한 다른 도구</span><span class="sxs-lookup"><span data-stu-id="aa90e-125">Other Tools for Creating Player Applications</span></span>
<span data-ttu-id="aa90e-126">또한 다음 Sdk hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-126">You can also use any of hello following SDKs:</span></span>

* [<span data-ttu-id="aa90e-127">부드러운 스트리밍 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="aa90e-127">Smooth Streaming Client SDK</span></span>](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [<span data-ttu-id="aa90e-128">부드러운 스트리밍 Windows 스토어 앱</span><span class="sxs-lookup"><span data-stu-id="aa90e-128">Smooth Streaming Windows Store App</span></span>](media-services-build-smooth-streaming-apps.md)
* [<span data-ttu-id="aa90e-129">Microsoft Media Platform: 플레이어 프레임워크</span><span class="sxs-lookup"><span data-stu-id="aa90e-129">Microsoft Media Platform: Player Framework</span></span>](http://playerframework.codeplex.com/) 
* [<span data-ttu-id="aa90e-130">HTML5 플레이어 프레임워크 설명서</span><span class="sxs-lookup"><span data-stu-id="aa90e-130">HTML5 Player Framework Documentation</span></span>](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [<span data-ttu-id="aa90e-131">OSMF용 Microsoft 부드러운 스트리밍 플러그인</span><span class="sxs-lookup"><span data-stu-id="aa90e-131">Microsoft Smooth Streaming Plugin for OSMF</span></span>](https://www.microsoft.com/download/details.aspx?id=36057) 
* [<span data-ttu-id="aa90e-132">Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스</span><span class="sxs-lookup"><span data-stu-id="aa90e-132">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>](http://aka.ms/sspk) 
* [<span data-ttu-id="aa90e-133">XBOX 비디오 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="aa90e-133">XBOX Video Application Development</span></span>](http://xbox.create.msdn.com/) 

## <a name="advertising"></a><span data-ttu-id="aa90e-134">광고</span><span class="sxs-lookup"><span data-stu-id="aa90e-134">Advertising</span></span>
<span data-ttu-id="aa90e-135">Windows 미디어 플랫폼 hello 통해 광고 삽입에 대 한 azure 미디어 서비스에서는: 플레이어 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-135">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="aa90e-136">광고를 지원하는 플레이어 프레임워크는 Windows 8, Silverlight, Windows Phone 8 및 iOS 장치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-136">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="aa90e-137">각 플레이어 프레임 워크에는 방법을 보여 주는 샘플 코드가 포함 되어 tooimplement 플레이어 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-137">Each player framework contains sample code that shows you how tooimplement a player application.</span></span> <span data-ttu-id="aa90e-138">미디어에 삽입할 수 있는 서로 다른 세 종류의 광고가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-138">There are three different kinds of ads you can insert into your media:</span></span>

<span data-ttu-id="aa90e-139">선형-기본 비디오 hello 일시 중지 하는 전체 프레임 광고</span><span class="sxs-lookup"><span data-stu-id="aa90e-139">Linear – full frame ads that pause hello main video</span></span>

<span data-ttu-id="aa90e-140">비선형-hello 기본 비디오가 재생 되로 표시 되는 오버레이 광고, 일반적으로 로고나 기타 정적 이미지 hello 플레이어 내에 배치</span><span class="sxs-lookup"><span data-stu-id="aa90e-140">Nonlinear – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player</span></span>

<span data-ttu-id="aa90e-141">동반-플레이어 hello 외부에서 표시 되는 광고</span><span class="sxs-lookup"><span data-stu-id="aa90e-141">Companion – ads that are displayed outside of hello player</span></span>

<span data-ttu-id="aa90e-142">Hello 기본 비디오 타임 라인의 한 지점에서 광고를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-142">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="aa90e-143">Ad 및 tooplay hello 하는 경우 hello 플레이어 알려야 광고 tooplay 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-143">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="aa90e-144">이 작업은 표준 XML 기반 파일 집합을 사용하여 수행됩니다. VAST(Video Ad Service Template), VMAP(Digital Video Multiple Ad Playlist), MAST(Media Abstract Sequencing Template) 및 VPAID(Digital Video Player Ad Interface Definition).</span><span class="sxs-lookup"><span data-stu-id="aa90e-144">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="aa90e-145">VAST 파일 어떤 광고 toodisplay를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-145">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="aa90e-146">시점을 지정 하는 VMAP 파일 tooplay 다양 한 광고 하 고 VAST XML을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-146">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="aa90e-147">MAST 파일은 또한 VAST XML을 포함할 수 있는 다른 방법은 toosequence 광고입니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-147">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="aa90e-148">VPAID 파일 hello 비디오 플레이어와 hello 광고 또는 광고 서버 간의 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="aa90e-148">VPAID files define an interface between hello video player and hello ad or ad server.</span></span> <span data-ttu-id="aa90e-149">자세한 내용은 [광고 삽입](https://msdn.microsoft.com/library/dn387398.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa90e-149">For more information, see [Inserting Ads](https://msdn.microsoft.com/library/dn387398.aspx).</span></span>

<span data-ttu-id="aa90e-150">라이브 스트리밍 비디오의 선택 캡션 및 광고 지원에 대한 정보는 [지원되는 선택 캡션 및 광고 삽입 표준](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa90e-150">For information about closed captioning and ads support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="aa90e-151">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="aa90e-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aa90e-152">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="aa90e-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="aa90e-153">참고 항목</span><span class="sxs-lookup"><span data-stu-id="aa90e-153">See Also</span></span>
[<span data-ttu-id="aa90e-154">DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함</span><span class="sxs-lookup"><span data-stu-id="aa90e-154">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

[<span data-ttu-id="aa90e-155">GitHub dash.js 리포지토리</span><span class="sxs-lookup"><span data-stu-id="aa90e-155">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js)

