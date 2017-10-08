---
title: "aaaDelivering 콘텐츠 toocustomers | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스를 사용하여 콘텐츠를 배달하는데 필요한 항목을 간략히 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a><span data-ttu-id="18483-103">콘텐츠 toocustomers를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-103">Deliver content toocustomers</span></span>
<span data-ttu-id="18483-104">스트리밍 또는 주문형 비디오 콘텐츠 toocustomers를 제공 하 고, 다양 한 네트워크 조건에서 toodeliver 고품질 비디오 toovarious 장치가 목표가입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-104">When you're delivering your streaming or video-on-demand content toocustomers, your goal is toodeliver high-quality video toovarious devices under different network conditions.</span></span>

<span data-ttu-id="18483-105">tooachieve이이 목표를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-105">tooachieve this goal, you can:</span></span>

* <span data-ttu-id="18483-106">스트림 tooa 비디오 스트림을 다중 비트 전송률 (적응 비트 전송률)으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="18483-106">Encode your stream tooa multi-bitrate (adaptive bitrate) video stream.</span></span> <span data-ttu-id="18483-107">이렇게 하면 품질 및 네트워크 상태가 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="18483-107">This will take care of quality and network conditions.</span></span>
* <span data-ttu-id="18483-108">Microsoft Azure 미디어 서비스를 사용 하 여 [동적 패키징](media-services-dynamic-packaging-overview.md) toodynamically 다시 패키지할 스트림을 서로 다른 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-108">Use Microsoft Azure Media Services [dynamic packaging](media-services-dynamic-packaging-overview.md) toodynamically re-package your stream into different protocols.</span></span> <span data-ttu-id="18483-109">이렇게 하면 여러 장치의 스트리밍이 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="18483-109">This will take care of streaming on different devices.</span></span> <span data-ttu-id="18483-110">미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술 뒤의 배달을 지원: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-110">Media Services supports delivery of hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

>[!NOTE]
><span data-ttu-id="18483-111">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-111">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="18483-112">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-112">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="18483-113">이 문서에서는 중요한 콘텐츠 배달 개념에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-113">This article gives an overview of important content delivery concepts.</span></span>

<span data-ttu-id="18483-114">알려진 문제, toocheck 참조 [알려진 문제](media-services-deliver-content-overview.md#known-issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-114">toocheck known issues, see [Known issues](media-services-deliver-content-overview.md#known-issues).</span></span>

## <a name="dynamic-packaging"></a><span data-ttu-id="18483-115">동적 패키징</span><span class="sxs-lookup"><span data-stu-id="18483-115">Dynamic packaging</span></span>
<span data-ttu-id="18483-116">Hello 동적 패키징을 사용 해당 미디어 서비스 제공, (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 지 원하는 형식 스트리밍을에서 적응 비트 전송률 MP4 또는 부드러운 스트리밍으로 인코딩 콘텐츠를 배달할 수 있습니다에 toore 패키지 필요 없이 이러한 스트리밍 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-116">With hello dynamic packaging that Media Services provides, you can deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG-DASH, HLS, Smooth Streaming,) without having toore-package into these streaming formats.</span></span> <span data-ttu-id="18483-117">동적 패키징을 사용하여 콘텐츠를 전달하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-117">We recommend delivering your content with dynamic packaging.</span></span>

<span data-ttu-id="18483-118">tootake 이점은 동적 패키징을 tooencode 중 2 층 (원본) 파일에 필요한 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-118">tootake advantage of dynamic packaging, you need tooencode your mezzanine (source) file into a set of adaptive-bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="18483-119">동적 패키징을 사용을 저장 하 고 hello 단일 저장소 형식의 파일에 대 한 비용을 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-119">With dynamic packaging, you store and pay for hello files in single storage format.</span></span> <span data-ttu-id="18483-120">미디어 서비스 빌드하고 사용자 요청에 따라 hello 적절 한 응답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-120">Media Services will build and serve hello appropriate response based on your requests.</span></span>

<span data-ttu-id="18483-121">동적 패키징은 표준 및 프리미엄 스트리밍 끝점에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-121">Dynamic packaging is available for standard and premium streaming endpoints.</span></span> 

<span data-ttu-id="18483-122">자세한 내용은 [동적 패키징](media-services-dynamic-packaging-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-122">For more information, see [Dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

## <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="18483-123">필터 및 동적 매니페스트</span><span class="sxs-lookup"><span data-stu-id="18483-123">Filters and dynamic manifests</span></span>
<span data-ttu-id="18483-124">미디어 서비스를 사용하여 자산에 대한 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-124">You can define filters for your assets with Media Services.</span></span> <span data-ttu-id="18483-125">이러한 필터는 확인할 수 있어 고객 비디오의 특정 섹션을 재생 하는 등 작업을 수행 하거나 고객 장치 (hello 자산에 연결 된 모든 hello 변환 하는 대신 처리할 수 있는 오디오 및 비디오 변환의 하위 집합을 지정 하는 서버 쪽 규칙 ).</span><span class="sxs-lookup"><span data-stu-id="18483-125">These filters are server-side rules that help your customers do things like play a specific section of a video or specify a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="18483-126">이 필터링을 통해 얻습니다 *동적 매니페스트* 고객 요청 toostream 하나를 기반으로 하는 비디오 또는 이상의 필터를 지정 하는 경우 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="18483-126">This filtering is achieved through *dynamic manifests* that are created when your customer requests toostream a video based on one or more specified filters.</span></span>

<span data-ttu-id="18483-127">자세한 내용은 [필터 및 동적 매니페스트](media-services-dynamic-manifest-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-127">For more information, see [Filters and dynamic manifests](media-services-dynamic-manifest-overview.md).</span></span>

## <a name="locators"></a><span data-ttu-id="18483-128">로케이터</span><span class="sxs-lookup"><span data-stu-id="18483-128">Locators</span></span>
<span data-ttu-id="18483-129">tooprovide 사용자 콘텐츠를 다운로드 하거나 toostream 사용된 될 수 있는 url 먼저 toopublish 자산 로케이터를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-129">tooprovide your user with a URL that can be used toostream or download your content, you first need toopublish your asset by creating a locator.</span></span> <span data-ttu-id="18483-130">로케이터는 자산에 포함 된 파일 항목이 지점 tooaccess hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-130">A locator provides an entry point tooaccess hello files contained in an asset.</span></span> <span data-ttu-id="18483-131">Media Services는 두 가지 유형의 로케이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-131">Media Services supports two types of locators:</span></span>

* <span data-ttu-id="18483-132">OnDemandOrigin 로케이터.</span><span class="sxs-lookup"><span data-stu-id="18483-132">OnDemandOrigin locators.</span></span> <span data-ttu-id="18483-133">이러한 열 사용된 toostream 미디어 (예를 들어, MPEG DASH, HLS 또는 부드러운 스트리밍)는 데이터 나 점진적으로 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-133">These are used toostream media (for example, MPEG-DASH, HLS, or Smooth Streaming) or progressively download files.</span></span>
* <span data-ttu-id="18483-134">SAS(공유 액세스 서명) URL 로케이터.</span><span class="sxs-lookup"><span data-stu-id="18483-134">Shared access signature (SAS) URL locators.</span></span> <span data-ttu-id="18483-135">이들은 사용된 toodownload 미디어 파일 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-135">These are used toodownload media files tooyour local computer.</span></span>

<span data-ttu-id="18483-136">*액세스 정책* 가 사용 되는 toodefine hello 권한 (예: 읽기, 쓰기 및 목록)을 클라이언트의 특정 자산에 대 한 권한과 액세스 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-136">An *access policy* is used toodefine hello permissions (such as read, write, and list) and duration for which a client has access for a particular asset.</span></span> <span data-ttu-id="18483-137">참고 hello 나열 권한 (AccessPermissions.List)을 OrDemandOrigin 로케이터를 만들에서 사용할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-137">Note that hello list permission (AccessPermissions.List) should not be used in creating an OrDemandOrigin locator.</span></span>

<span data-ttu-id="18483-138">로케이터에는 만료 날짜가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-138">Locators have expiration dates.</span></span> <span data-ttu-id="18483-139">Azure 포털 hello 만료 날짜를 설정 100 년 hello에 이후 로케이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-139">hello Azure portal sets an expiration date 100 years in hello future for locators.</span></span>

> [!NOTE]
> <span data-ttu-id="18483-140">2015 년 3 월 이전에 Azure 포털 toocreate 로케이터는 hello를 사용 하는 경우 이러한 로케이터는 2 년이 지나면 tooexpire를 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-140">If you used hello Azure portal toocreate locators before March 2015, those locators were set tooexpire after two years.</span></span>
> 
> 

<span data-ttu-id="18483-141">만료 날짜를 사용 하 여 로케이터는 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) Api입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-141">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="18483-142">SAS 로케이터의 hello 만료 날짜를 업데이트 하면 hello URL 변경 되는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-142">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

<span data-ttu-id="18483-143">로케이터는 없는 toomanage 사용자별 액세스 제어를 설계 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-143">Locators are not designed toomanage per-user access control.</span></span> <span data-ttu-id="18483-144">디지털 Rights Management (DRM) 솔루션을 사용 하 여 서로 다른 액세스 권한을 tooindividual 가진 사용자가 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-144">You can give different access rights tooindividual users by using Digital Rights Management (DRM) solutions.</span></span> <span data-ttu-id="18483-145">자세한 내용은 [미디어 보안 설정](http://msdn.microsoft.com/library/azure/dn282272.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-145">For more information, see [Securing Media](http://msdn.microsoft.com/library/azure/dn282272.aspx).</span></span>

<span data-ttu-id="18483-146">Locator를 만들 때 Azure 저장소의 저장소 및 전파 프로세스 toorequired 인해 30 초 간 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-146">When you create a locator, there may be a 30-second delay due toorequired storage and propagation processes in Azure Storage.</span></span>

## <a name="adaptive-streaming"></a><span data-ttu-id="18483-147">적응 스트리밍</span><span class="sxs-lookup"><span data-stu-id="18483-147">Adaptive streaming</span></span>
<span data-ttu-id="18483-148">적응 비트 전송률 기술을 toodetermine 네트워크 상태 비디오 플레이어 응용 프로그램을 허용 하 고 여러 비트 전송률에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-148">Adaptive bitrate technologies allow video player applications toodetermine network conditions and select from several bitrates.</span></span> <span data-ttu-id="18483-149">네트워크 통신 저하 hello 클라이언트 재생 더 낮은 비디오 품질 계속 될 수 있도록 더 낮은 비트 전송률을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-149">When network communication degrades, hello client can select a lower bitrate so playback can continue with lower video quality.</span></span> <span data-ttu-id="18483-150">네트워크 상태가 개선 hello 클라이언트 tooa 비디오 품질이 향상된 된 더 높은 비트 전송률로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-150">As network conditions improve, hello client can switch tooa higher bitrate with improved video quality.</span></span> <span data-ttu-id="18483-151">Azure 미디어 서비스는 hello 다음 적응 비트 전송률 기술을 지원: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-151">Azure Media Services supports hello following adaptive bitrate technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG-DASH.</span></span>

<span data-ttu-id="18483-152">스트리밍 Url이 포함 된 사용자가 tooprovide를 먼저 만들어야 OnDemandOrigin 로케이터 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-152">tooprovide users with streaming URLs, you first must create an OnDemandOrigin locator.</span></span> <span data-ttu-id="18483-153">Hello hello 콘텐츠를 포함 하는 기본 경로 toohello 자산 hello 로케이터에서는 만들기 toostream을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-153">Creating hello locator gives you hello base path toohello asset that contains hello content you want toostream.</span></span> <span data-ttu-id="18483-154">그러나 toobe 수 toostream이 콘텐츠 toomodify 나중에이 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-154">However, toobe able toostream this content, you need toomodify this path further.</span></span> <span data-ttu-id="18483-155">스트리밍 매니페스트 파일 전체 URL toohello, hello 로케이터 경로 연결 해야 tooconstruct 값과 hello 매니페스트 (filename.ism) 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-155">tooconstruct a full URL toohello streaming manifest file, you must concatenate hello locator’s path value and hello manifest (filename.ism) file name.</span></span> <span data-ttu-id="18483-156">다음 추가 **/manifest** 와 적절 한 형식 (필요한 경우) toohello 로케이터 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-156">Then append **/Manifest** and an appropriate format (if needed) toohello locator path.</span></span>

> [!NOTE]
> <span data-ttu-id="18483-157">SSL 연결을 통해 콘텐츠를 스트리밍할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-157">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="18483-158">toodo이를 HTTPS로 스트리밍 Url 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-158">toodo this, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="18483-159">현재 AMS는 사용자 지정 도메인을 사용하는 SSL을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-159">Note that, currently, AMS doesn’t support SSL with custom domains.</span></span>  
> 


<span data-ttu-id="18483-160">스트리밍 끝점 콘텐츠를 배달 하는 hello 2014 년 9 월 10 일 이후에 만들어진 경우에 SSL을 통해 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-160">You can only stream over SSL if hello streaming endpoint from which you deliver your content was created after September 10th, 2014.</span></span> <span data-ttu-id="18483-161">Hello URL에 "streaming.mediaservices.windows.net" 스트리밍 Url hello 스트리밍 끝점이 2014 년 9 월 10 일 이후에 작성을 기반으로 하는 경우</span><span class="sxs-lookup"><span data-stu-id="18483-161">If your streaming URLs are based on hello streaming endpoints created after September 10th, 2014, hello URL contains “streaming.mediaservices.windows.net.”</span></span> <span data-ttu-id="18483-162">"Origin.mediaservices.windows.net" (이전 형식 hello)를 포함 하는 스트리밍 Url에서 SSL을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-162">Streaming URLs that contain “origin.mediaservices.windows.net” (hello old format) do not support SSL.</span></span> <span data-ttu-id="18483-163">URL이 이전 형식인 hello toobe 수 toostream SSL을 통해 원하는 경우 새 스트리밍 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18483-163">If your URL is in hello old format and you want toobe able toostream over SSL, create a new streaming endpoint.</span></span> <span data-ttu-id="18483-164">새 SSL을 통해 끝점 toostream 콘텐츠 스트리밍 hello에 따라 Url을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-164">Use URLs based on hello new streaming endpoint toostream your content over SSL.</span></span>

## <a name="streaming-url-formats"></a><span data-ttu-id="18483-165">스트리밍 URL 형식</span><span class="sxs-lookup"><span data-stu-id="18483-165">Streaming URL formats</span></span>
### <a name="mpeg-dash-format"></a><span data-ttu-id="18483-166">MPEG-DASH 형식</span><span class="sxs-lookup"><span data-stu-id="18483-166">MPEG-DASH format</span></span>
<span data-ttu-id="18483-167">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="18483-167">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>

<span data-ttu-id="18483-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="18483-168">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)</span></span>

### <a name="apple-http-live-streaming-hls-v4-format"></a><span data-ttu-id="18483-169">Apple HLS(HTTP 라이브 스트리밍) V4 형식</span><span class="sxs-lookup"><span data-stu-id="18483-169">Apple HTTP Live Streaming (HLS) V4 format</span></span>
<span data-ttu-id="18483-170">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="18483-170">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="18483-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="18483-171">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)</span></span>

### <a name="apple-http-live-streaming-hls-v3-format"></a><span data-ttu-id="18483-172">Apple HLS(HTTP 라이브 스트리밍) V3 형식</span><span class="sxs-lookup"><span data-stu-id="18483-172">Apple HTTP Live Streaming (HLS) V3 format</span></span>
<span data-ttu-id="18483-173">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="18483-173">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)</span></span>

<span data-ttu-id="18483-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span><span class="sxs-lookup"><span data-stu-id="18483-174">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)</span></span>

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a><span data-ttu-id="18483-175">오디오 전용 필터로 Apple HTTP 라이브 스트리밍(HLS) 포맷</span><span class="sxs-lookup"><span data-stu-id="18483-175">Apple HTTP Live Streaming (HLS) format with audio-only filter</span></span>
<span data-ttu-id="18483-176">기본적으로 오디오 전용 트랙 HLS 매니페스트 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18483-176">By default, audio-only tracks are included in hello HLS manifest.</span></span> <span data-ttu-id="18483-177">셀룰러 네트워크에 대한 Apple 스토어 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-177">This is required for Apple Store certification for cellular networks.</span></span> <span data-ttu-id="18483-178">이 경우에 클라이언트가 대역폭이 충분 하지 않습니다 2g 연결을 통해 연결 된 경우 재생 tooaudio 전용 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-178">In this case, if a client doesn’t have sufficient bandwidth or is connected over a 2G connection, playback switches tooaudio-only.</span></span> <span data-ttu-id="18483-179">버퍼링 기능이 없으면 스트리밍 tookeep 콘텐츠 않아도 되지만 화면이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-179">This helps tookeep content streaming without buffering, but there is no video.</span></span> <span data-ttu-id="18483-180">일부 시나리오에서 오디오 전용 화면보다는 어느 정도 버퍼링이 발생하는 것이 나을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-180">In some scenarios, player buffering might be preferred over audio-only.</span></span> <span data-ttu-id="18483-181">Tooremove hello 오디오 전용 추적 하려는 경우 추가 **오디오 전용 = false** toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-181">If you want tooremove hello audio-only track, add **audio-only=false** toohello URL.</span></span>

<span data-ttu-id="18483-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span><span class="sxs-lookup"><span data-stu-id="18483-182">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)</span></span>

<span data-ttu-id="18483-183">자세한 내용은 [동적 매니페스트 컴퍼지션 지원 및 HLS 출력 추가 기능](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-183">For more information, see [Dynamic Manifest Composition support and HLS output additional features](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/).</span></span>

### <a name="smooth-streaming-format"></a><span data-ttu-id="18483-184">부드러운 스트리밍 형식</span><span class="sxs-lookup"><span data-stu-id="18483-184">Smooth Streaming format</span></span>
<span data-ttu-id="18483-185">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="18483-185">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="18483-186">예제:</span><span class="sxs-lookup"><span data-stu-id="18483-186">Example:</span></span>

<span data-ttu-id="18483-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="18483-187">http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest</span></span>

### <span data-ttu-id="18483-188"><a id="fmp4_v20"></a>부드러운 스트리밍 2.0 매니페스트(레거시 매니페스트)</span><span class="sxs-lookup"><span data-stu-id="18483-188"><a id="fmp4_v20"></a>Smooth Streaming 2.0 manifest (legacy manifest)</span></span>
<span data-ttu-id="18483-189">기본적으로 부드러운 스트리밍 매니페스트 형식 hello 반복 태그 (r 태그)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-189">By default, Smooth Streaming manifest format contains hello repeat tag (r-tag).</span></span> <span data-ttu-id="18483-190">그러나 일부 플레이어는 hello r 태그를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-190">However, some players do not support hello r-tag.</span></span> <span data-ttu-id="18483-191">이러한 플레이어에는 클라이언트 hello r 태그를 사용 하지 않는 형식을 사용할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="18483-191">Clients with these players can use a format that disables hello r-tag:</span></span>

<span data-ttu-id="18483-192">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)</span><span class="sxs-lookup"><span data-stu-id="18483-192">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=fmp4-v20)</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a><span data-ttu-id="18483-193">점진적 다운로드</span><span class="sxs-lookup"><span data-stu-id="18483-193">Progressive download</span></span>
<span data-ttu-id="18483-194">점진적 다운로드를 hello 전체 파일이 다운로드 되기 전에 미디어 재생을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-194">With progressive download, you can start playing media before hello entire file has been downloaded.</span></span> <span data-ttu-id="18483-195">.ism*(ismv, isma, ismt, ismc) 파일을 점진적으로 다운로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-195">You cannot progressively download .ism* (ismv, isma, ismt, or ismc) files.</span></span>

<span data-ttu-id="18483-196">tooprogressively 콘텐츠를 다운로드할 hello OnDemandOrigin 로케이터 종류에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-196">tooprogressively download content, use hello OnDemandOrigin type of locator.</span></span> <span data-ttu-id="18483-197">hello 다음 예제는 hello 유형의 OnDemandOrigin 로케이터를 기반으로 하는 hello URL.</span><span class="sxs-lookup"><span data-stu-id="18483-197">hello following example shows hello URL that is based on hello OnDemandOrigin type of locator:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

<span data-ttu-id="18483-198">모든 저장소 암호화 된 자산 toostream 점진적 다운로드에 대 한 hello origin 서비스에서 원하는 암호를 해독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-198">You must decrypt any storage-encrypted assets that you want toostream from hello origin service for progressive download.</span></span>

## <a name="download"></a><span data-ttu-id="18483-199">다운로드</span><span class="sxs-lookup"><span data-stu-id="18483-199">Download</span></span>
<span data-ttu-id="18483-200">toodownload 콘텐츠 tooa 클라이언트 장치에서 SAS 로케이터를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-200">toodownload your content tooa client device, you must create a SAS Locator.</span></span> <span data-ttu-id="18483-201">hello SAS 로케이터에서는 파일에 위치한 toohello Azure 저장소 컨테이너에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-201">hello SAS locator gives you access toohello Azure Storage container where your file is located.</span></span> <span data-ttu-id="18483-202">hello 호스트와 SAS 서명 사이 tooembed hello 파일 이름이 있는 toobuild hello 다운로드 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-202">toobuild hello download URL, you have tooembed hello file name between hello host and SAS signature.</span></span>

<span data-ttu-id="18483-203">hello 다음 예제는 hello SAS 로케이터를 기반으로 하는 hello URL.</span><span class="sxs-lookup"><span data-stu-id="18483-203">hello following example shows hello URL that is based on hello SAS locator:</span></span>

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

<span data-ttu-id="18483-204">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18483-204">hello following considerations apply:</span></span>

* <span data-ttu-id="18483-205">모든 저장소 암호화 된 자산 toostream 점진적 다운로드에 대 한 hello origin 서비스에서 원하는 암호를 해독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-205">You must decrypt any storage-encrypted assets that you want toostream from hello origin service for progressive download.</span></span>
* <span data-ttu-id="18483-206">12시간 안에 완료되지 않은 다운로드는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-206">A download that has not finished within 12 hours will fail.</span></span>

## <a name="streaming-endpoints"></a><span data-ttu-id="18483-207">스트리밍 끝점</span><span class="sxs-lookup"><span data-stu-id="18483-207">Streaming endpoints</span></span>

<span data-ttu-id="18483-208">스트리밍 끝점 tooa 클라이언트 플레이어 응용 프로그램이 나 tooa CDN 콘텐츠 배달 네트워크 ()에 대 한 추가 배포 직접 콘텐츠를 배달할 수 있는 스트리밍 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18483-208">A streaming endpoint represents a streaming service that can deliver content directly tooa client player application or tooa content delivery network (CDN) for further distribution.</span></span> <span data-ttu-id="18483-209">스트리밍 끝점 서비스 hello 아웃 바운드 스트림은 라이브 스트림 또는 미디어 서비스 계정의 주문형 비디오 자산을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-209">hello outbound stream from a streaming endpoint service can be a live stream or a video-on-demand asset in your Media Services account.</span></span> <span data-ttu-id="18483-210">스트리밍 끝점 유형으로는 **표준** 및 **프리미엄** 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18483-210">There are two types of streaming endpoints, **standard** and **premium**.</span></span> <span data-ttu-id="18483-211">자세한 내용은 [스트리밍 끝점 개요](media-services-streaming-endpoints-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-211">For more information, see [Streaming endpoints overview](media-services-streaming-endpoints-overview.md).</span></span>

>[!NOTE]
><span data-ttu-id="18483-212">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-212">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="18483-213">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-213">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="18483-214">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="18483-214">Known issues</span></span>
### <a name="changes-toosmooth-streaming-manifest-version"></a><span data-ttu-id="18483-215">변경 내용 tooSmooth 스트리밍 매니페스트 버전</span><span class="sxs-lookup"><span data-stu-id="18483-215">Changes tooSmooth Streaming manifest version</span></span>
<span data-ttu-id="18483-216">매니페스트 자산 미디어 인코더 표준, 미디어 인코더 프리미엄 워크플로 또는 hello 동적 패키징-부드러운 스트리밍 hello를 사용 하 여 스트리밍 되었습니다 이전 Azure 미디어 인코더에서 생성 하는 경우-2016 년 7 월 서비스 릴리스의 hello 반환 되기 전에 준수 tooversion 2.0입니다.</span><span class="sxs-lookup"><span data-stu-id="18483-216">Before hello July 2016 service release--when assets produced by Media Encoder Standard, Media Encoder Premium Workflow, or hello earlier Azure Media Encoder were streamed by using dynamic packaging--hello Smooth Streaming manifest returned would conform tooversion 2.0.</span></span> <span data-ttu-id="18483-217">버전 2.0에서는 hello 조각 기간 hello 소위 반복 ('r') 태그를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="18483-217">In version 2.0, hello fragment durations do not use hello so-called repeat (‘r’) tags.</span></span> <span data-ttu-id="18483-218">예:</span><span class="sxs-lookup"><span data-stu-id="18483-218">For example:</span></span>

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

<span data-ttu-id="18483-219">2016 년 7 월 서비스 릴리스의 hello, 생성 된 hello 부드러운 스트리밍 매니페스트의 반복 태그를 사용 하 여 조각 기간와 tooversion 2.2를 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-219">In hello July 2016 service release, hello generated Smooth Streaming manifest conforms tooversion 2.2, with fragment durations using repeat tags.</span></span> <span data-ttu-id="18483-220">예:</span><span class="sxs-lookup"><span data-stu-id="18483-220">For example:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

<span data-ttu-id="18483-221">Hello 레거시 부드러운 스트리밍 클라이언트 중 일부가 hello 반복 태그를 지원 하지 않을 수 있습니다 및 tooload hello 매니페스트 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-221">Some of hello legacy Smooth Streaming clients may not support hello repeat tags and will fail tooload hello manifest.</span></span> <span data-ttu-id="18483-222">toomitigate이 문제를 hello 레거시 매니페스트 형식 매개 변수를 사용할 수 **(형식 = fmp4 v20)** 또는 프로그램 클라이언트 toohello 최신를 지 원하는 버전을 반복 하는 태그를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-222">toomitigate this issue, you can use hello legacy manifest format parameter **(format=fmp4-v20)** or update your client toohello latest version, which supports repeat tags.</span></span> <span data-ttu-id="18483-223">자세한 내용은 [부드러운 스트리밍 2.0](media-services-deliver-content-overview.md#fmp4_v20)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18483-223">For more information, see [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="18483-224">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="18483-224">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="18483-225">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="18483-225">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a><span data-ttu-id="18483-226">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="18483-226">Related topics</span></span>
[<span data-ttu-id="18483-227">저장소 키를 롤링 후 미디어 서비스 로케이터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="18483-227">Update Media Services locators after rolling storage keys</span></span>](media-services-roll-storage-access-keys.md)

