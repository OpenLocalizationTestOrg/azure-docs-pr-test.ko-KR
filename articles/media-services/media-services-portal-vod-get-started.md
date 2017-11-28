---
title: "VoD hello Azure 포털을 사용 하 여 제공 aaaGet 시작 | Microsoft Docs"
description: "이 자습서는 hello Azure 포털을 사용 하 여 Azure 미디어 서비스 (AMS) 응용 프로그램과 함께 기본 VoD ()를 주문형 비디오 콘텐츠 배달 서비스 구현의 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="65365-103">Hello Azure 포털을 사용 하 여 필요에 따라 콘텐츠를 제공 하기 시작</span><span class="sxs-lookup"><span data-stu-id="65365-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="65365-104">이 자습서는 hello Azure 포털을 사용 하 여 Azure 미디어 서비스 (AMS) 응용 프로그램과 함께 기본 VoD ()를 주문형 비디오 콘텐츠 배달 서비스 구현의 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65365-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65365-105">Prerequisites</span></span>
<span data-ttu-id="65365-106">hello 다음은 필요한 toocomplete hello 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="65365-107">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="65365-107">An Azure account.</span></span> <span data-ttu-id="65365-108">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65365-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="65365-109">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="65365-109">A Media Services account.</span></span> <span data-ttu-id="65365-110">미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="65365-111">이 자습서에는 작업을 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65365-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="65365-112">스트리밍 끝점을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="65365-113">비디오 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-113">Upload a video file.</span></span>
3. <span data-ttu-id="65365-114">Hello 소스 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="65365-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="65365-115">Hello 및 get 스트리밍 자산과 점진적 다운로드 Url을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="65365-116">콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="65365-117">스트리밍 끝점 시작</span><span class="sxs-lookup"><span data-stu-id="65365-117">Start streaming endpoints</span></span> 

<span data-ttu-id="65365-118">Azure 미디어 서비스를 통해 적응 비트 전송률 스트리밍 비디오를 제공 하는 hello 가장 일반적인 시나리오 중 하나 작업할 때는입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="65365-119">미디어 서비스는 적응 비트 전송률 사전 패키지 toostore 필요 없이 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 적시에서 지 원하는 형식 스트리밍을에 인코딩된 MP4 콘텐츠 toodeliver 수 있는 동적 패키징 제공 각각의 형식 스트리밍을 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="65365-120">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="65365-121">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="65365-122">toostart hello 스트리밍 끝점을 다음 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="65365-123">Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="65365-124">Hello 설정 창에서 스트리밍 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="65365-125">Hello 기본 스트리밍 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="65365-126">hello 스트리밍 끝점 세부 정보 기본 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="65365-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="65365-127">Hello 시작 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="65365-128">변경 내용을 저장 단추 toosave hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="65365-129">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="65365-129">Upload files</span></span>
<span data-ttu-id="65365-130">toostream tooupload hello 원본 비디오 해야 Azure 미디어 서비스를 사용 하 여 비디오를 다중 비트 전송률 인코딩 고 hello 결과 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="65365-131">hello 첫 번째 단계는이 섹션에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="65365-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="65365-132">Hello에 **설정** 창 클릭 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![파일 업로드](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="65365-134">Hello 클릭 **업로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="65365-135">hello **비디오 자산을 업로드** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="65365-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="65365-136">파일 크기에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="65365-137">컴퓨터에 필요한 toohello 비디오 찾아보기 선택한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="65365-138">hello 업로드 시작 하 고 hello 파일 이름에서 hello 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="65365-139">Hello에 나열 된 hello 새 자산 참조 hello 업로드가 완료 되 면 **자산** 창.</span><span class="sxs-lookup"><span data-stu-id="65365-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="65365-140">자산 인코딩</span><span class="sxs-lookup"><span data-stu-id="65365-140">Encode assets</span></span>

<span data-ttu-id="65365-141">적응 비트 전송률 스트리밍 tooyour 클라이언트 제공 하는 hello 가장 일반적인 시나리오 중 하나는 Azure 미디어 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="65365-142">미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술에 따라 지원: HLS HTTP 라이브 스트리밍 (), 부드러운 스트리밍, MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="65365-143">tooprepare 비디오 적응 비트 전송률 스트리밍에 대 한 필요한 tooencode 원본 비디오를 다중 비트 전송률 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="65365-144">Hello를 사용 해야 **미디어 인코더 표준** 인코더 tooencode 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="65365-145">또한 미디어 서비스 제공 toodeliver 수 있는 동적 패키징 hello 스트리밍 형식 뒤에 여 다중 비트 전송률 mp4: MPEG DASH, HLS, 부드러운 스트리밍 형식 스트리밍을로 toorepackage 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="65365-146">동적 패키징을 사용 하면 toostore 및 단일 저장소 형식 및 미디어 서비스의 hello 파일에 대 한 급여 빌드되고 클라이언트의 요청에 따라 hello 적절 한 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="65365-147">tootake 이점은 동적 패키징을 tooencode 소스 파일에 필요한 (hello 인코딩 단계는이 섹션의 나중에 설명 된) 다중 비트 전송률 MP4 파일 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="65365-148">toouse hello 포털 tooencode</span><span class="sxs-lookup"><span data-stu-id="65365-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="65365-149">이 섹션에서는 프록시 hello tooencode 미디어 인코더 표준 사용 하 여 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="65365-150">Hello에 **설정** 창에서 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="65365-151">Hello에 **자산** 창, 싶다는 의사를 tooencode 선택 hello 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="65365-152">키를 눌러 hello **인코딩** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="65365-153">Hello에 **자산을 인코딩하** 창, "미디어 인코더 표준" 선택 hello 프로세서 및 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="65365-154">기본 설정에 대한 자세한 내용은 [비트 전송률 래더 자동 생성](media-services-autogen-bitrate-ladder-with-mes.md) 및 [MES에 대한 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65365-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="65365-155">Toocontrol 어떤 인코딩 사전 설정을 사용 하려는 경우이 점을 명심: tooselect hello 입력된 비디오에 가장 적합 하는 미리 설정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="65365-156">예를 들어 입력된 비디오 1920 x 1080 픽셀이 고 해상도 알고 있는 경우 다음 사용할 수 있습니다 hello "H264 다중 비트 전송률 1080p" 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="65365-157">낮은 해상도(640x360) 비디오가 있는 경우 기본 “H264 다중 비트 전송률 1080p” 기본 설정을 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="65365-158">관리를 간소화 하기 hello 출력 자산 편집 hello 이름 및 hello 작업의 hello 이름은 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![자산 인코딩](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="65365-160">**만들기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="65365-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="65365-161">인코딩 작업의 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="65365-161">Monitor encoding job progress</span></span>
<span data-ttu-id="65365-162">인코딩 작업을 하는 hello의 toomonitor hello 진행률 클릭 **설정** (hello 페이지의 위쪽 hello)를 클릭 한 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![작업](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="65365-164">콘텐츠 게시</span><span class="sxs-lookup"><span data-stu-id="65365-164">Publish content</span></span>
<span data-ttu-id="65365-165">tooprovide는 url을 사용 하는 toostream 하거나 콘텐츠를 다운로드할 수 있는 사용자를 처음 필요 너무 "게시할" 자산 로케이터를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="65365-166">로케이터는 hello 자산에 포함 된 액세스 toofiles를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="65365-167">Media Services는 두 가지 유형의 로케이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="65365-168">스트리밍 로케이터 (OnDemandOrigin), (예를 들어 toostream MPEG DASH, HLS 또는 부드러운 스트리밍) 적응 스트리밍에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="65365-169">스트리밍 로케이터 toocreate 자산인.ism 파일을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="65365-170">점진적(SAS) 로케이터로, 점진적 다운로드를 통해 비디오를 배달하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="65365-171">스트리밍 URL 형식에 따라 hello 개이고 tooplay 부드러운 스트리밍 자산을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="65365-172">HLS 스트리밍 URL을 한 toobuild 추가 (형식 = m3u8 aapl) toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="65365-173">스트리밍 URL, MPEG DASH는 toobuild 추가 (형식 = mpd-시간-csf) toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="65365-174">SAS URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="65365-175">2015 년 3 월 이전에 hello 포털 toocreate 로케이터를 사용 하는 경우 로케이터는 2 년 유효 기간으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="65365-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="65365-176">만료 날짜를 사용 하 여 로케이터는 tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) Api입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="65365-177">SAS 로케이터의 hello 만료 날짜를 업데이트 하면 hello URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="65365-178">toouse hello 포털 toopublish 자산</span><span class="sxs-lookup"><span data-stu-id="65365-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="65365-179">toouse hello 포털 toopublish 자산, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65365-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="65365-180">계정 배포 진행 상태를 보려면 **설정** > **자산**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65365-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="65365-181">원하는 toopublish hello 자산을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="65365-182">Hello 클릭 **게시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="65365-183">Hello 로케이터 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-183">Select hello locator type.</span></span>
5. <span data-ttu-id="65365-184">**추가**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="65365-184">Press **Add**.</span></span>
   
    ![게시](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="65365-186">hello URL이 toohello 목록이 추가 **게시 Url**합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="65365-187">Hello 포털에서 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="65365-187">Play content from hello portal</span></span>
<span data-ttu-id="65365-188">hello Azure 포털에서 제공 콘텐츠 플레이어를 사용할 수 있는 tootest 비디오.</span><span class="sxs-lookup"><span data-stu-id="65365-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="65365-189">원하는 hello 비디오를 클릭 하 고 hello 클릭 **재생** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-189">Click hello desired video and then click hello **Play** button.</span></span>

![게시](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="65365-191">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65365-191">Some considerations apply:</span></span>

* <span data-ttu-id="65365-192">toobegin 스트리밍을 시작 실행 중인 hello **기본** 스트리밍 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="65365-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="65365-193">게시 된 비디오 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="65365-194">이 **미디어 플레이어** hello 기본 스트리밍 끝점에서에서 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="65365-195">기본이 아닌에서 tooplay 스트리밍 끝점을 toocopy hello URL을 클릭 하 고 다른 플레이어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="65365-196">예를 들어 [Azure Media Services 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65365-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65365-197">Next steps</span></span>
<span data-ttu-id="65365-198">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="65365-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="65365-199">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="65365-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

