---
title: "Azure Portal을 사용한 VoD 제공 시작 | Microsoft Docs"
description: "이 자습서에서는 Azure Portal을 사용한 AMS(Azure Media Services) 응용 프로그램으로 기본 VoD(주문형 비디오) 콘텐츠 배달 서비스를 구현하는 단계를 안내합니다."
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
ms.openlocfilehash: a8eeeeff412837acba14b441a3c590edf7e3597a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-the-azure-portal"></a><span data-ttu-id="6bdd5-103">Azure Portal을 사용한 주문형 콘텐츠 제공 시작</span><span class="sxs-lookup"><span data-stu-id="6bdd5-103">Get started with delivering content on demand using the Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="6bdd5-104">이 자습서에서는 Azure Portal을 사용한 AMS(Azure Media Services) 응용 프로그램으로 기본 VoD(주문형 비디오) 콘텐츠 배달 서비스를 구현하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bdd5-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6bdd5-105">Prerequisites</span></span>
<span data-ttu-id="6bdd5-106">자습서를 완료하는 데 필요한 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="6bdd5-107">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-107">An Azure account.</span></span> <span data-ttu-id="6bdd5-108">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="6bdd5-109">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-109">A Media Services account.</span></span> <span data-ttu-id="6bdd5-110">Media Services 계정을 만들려면 [Media Services 계정을 만드는 방법](media-services-portal-create-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="6bdd5-111">이 자습서에는 다음 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-111">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="6bdd5-112">스트리밍 끝점을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="6bdd5-113">비디오 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-113">Upload a video file.</span></span>
3. <span data-ttu-id="6bdd5-114">원본 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-114">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="6bdd5-115">자산을 게시하고, 스트리밍 기능을 사용하고, URL을 점진적으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-115">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="6bdd5-116">콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="6bdd5-117">스트리밍 끝점 시작</span><span class="sxs-lookup"><span data-stu-id="6bdd5-117">Start streaming endpoints</span></span> 

<span data-ttu-id="6bdd5-118">Azure Media Services 작업 시 가장 일반적인 시나리오 중 하나는 적응 비트 전송률 스트리밍을 통해 비디오를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-118">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="6bdd5-119">Media Services는 적응 비트 전송률 MP4 인코딩 콘텐츠를 Media Services에서 적시에 지원되는 각 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍)의 사전 패키징된 버전을 저장하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-119">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="6bdd5-120">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-120">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="6bdd5-121">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-121">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="6bdd5-122">스트리밍 끝점을 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-122">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="6bdd5-123">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-123">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6bdd5-124">설정 창에서 스트리밍 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-124">In the Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="6bdd5-125">기본 스트리밍 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-125">Click the default streaming endpoint.</span></span> 

    <span data-ttu-id="6bdd5-126">기본 스트리밍 끝점 세부 정보 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-126">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="6bdd5-127">시작 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-127">Click the Start icon.</span></span>
5. <span data-ttu-id="6bdd5-128">저장 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-128">Click the Save button to save your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="6bdd5-129">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="6bdd5-129">Upload files</span></span>
<span data-ttu-id="6bdd5-130">Azure Media Services를 사용하여 비디오를 스트림하려면 원본 비디오를 업로드하고 다중 비트 전송률로 인코딩하고 결과를 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-130">To stream videos using Azure Media Services, you need to upload the source videos, encode them into multiple bitrates, and publish the result.</span></span> <span data-ttu-id="6bdd5-131">첫 번째 단계는 이 섹션에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-131">The first step is covered in this section.</span></span> 

1. <span data-ttu-id="6bdd5-132">**설정** 창에서 **자산**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-132">In the **Setting** window, click **Assets**.</span></span>
   
    ![파일 업로드](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="6bdd5-134">**업로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-134">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="6bdd5-135">**비디오 자산 업로드** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-135">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6bdd5-136">파일 크기에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="6bdd5-137">컴퓨터에 원하는 비디오를 찾아 선택하고 확인을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-137">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="6bdd5-138">업로드가 시작되고 파일 이름 아래에 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-138">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="6bdd5-139">업로드가 완료되면 **자산** 창에 새 자산이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-139">Once the upload completes, you see the new asset listed in the **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="6bdd5-140">자산 인코딩</span><span class="sxs-lookup"><span data-stu-id="6bdd5-140">Encode assets</span></span>

<span data-ttu-id="6bdd5-141">Azure Media Services 작업 시 가장 일반적인 시나리오 중 하나는 클라이언트에 적응 비트 전송률 스트리밍을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-141">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="6bdd5-142">Media Services에서 지원하는 적응 비트 전송률 스트리밍은 HLS(HTTP 라이브 스트리밍), 부드러운 스트리밍, MPEG-DASH입니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-142">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="6bdd5-143">적응 비트 전송률 스트리밍을 위한 비디오를 준비하려면 소스 비디오를 다중 비트 전송률 파일로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-143">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="6bdd5-144">비디오를 인코딩하는 데는 **미디어 인코더 표준** 인코더를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-144">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="6bdd5-145">Media Services는 다중 비트 전송률 MP4를 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍)으로 다시 패키지하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-145">Media Services also provides dynamic packaging, which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to repackage into these streaming formats.</span></span> <span data-ttu-id="6bdd5-146">동적 패키징에서는 단일 저장소 형식으로 파일을 저장하고 비용을 지불하기만 하면 됩니다. 그러면 Media Services가 클라이언트의 요청에 따라 적절한 응답을 빌드 및 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-146">With dynamic packaging, you only need to store and pay for the files in single storage format and Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="6bdd5-147">동적 패키징을 활용하려면 원본 파일을 다중 비트 전송률 MP4 파일 집합으로 인코딩해야 합니다(인코딩 단계는 이 섹션의 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="6bdd5-147">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

### <a name="to-use-the-portal-to-encode"></a><span data-ttu-id="6bdd5-148">인코딩하는 데 포털을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="6bdd5-148">To use the portal to encode</span></span>
<span data-ttu-id="6bdd5-149">이 섹션에서는 미디어 인코더 표준을 사용하여 콘텐츠를 인코딩할 수 있는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-149">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="6bdd5-150">**설정** 창에서 **자산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-150">In the **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="6bdd5-151">**자산** 창에서 인코딩할 자산을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-151">In the **Assets** window, select the asset that you would like to encode.</span></span>
3. <span data-ttu-id="6bdd5-152">**인코딩** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-152">Press the **Encode** button.</span></span>
4. <span data-ttu-id="6bdd5-153">**자산 인코딩** 창에서 "Media Encoder Standard" 프로세서 및 사전 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-153">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="6bdd5-154">기본 설정에 대한 자세한 내용은 [비트 전송률 래더 자동 생성](media-services-autogen-bitrate-ladder-with-mes.md) 및 [MES에 대한 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="6bdd5-155">사용하는 인코딩 기본 설정을 제어하려는 경우 입력 비디오에 가장 적합한 기본 설정을 선택하는 것이 중요하다는 사실을 유념하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-155">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="6bdd5-156">예를 들어 입력 비디오가 1920x1080픽셀 해상도를 포함하는 것을 알고 있는 경우 "H264 다중 비트 전송률 1080p" 사전 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="6bdd5-157">낮은 해상도(640x360) 비디오가 있는 경우 기본 “H264 다중 비트 전송률 1080p” 기본 설정을 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="6bdd5-158">관리를 간소화하기 위해 출력 자산의 이름과 작업 이름을 편집하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-158">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![자산 인코딩](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="6bdd5-160">**만들기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="6bdd5-161">인코딩 작업의 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="6bdd5-161">Monitor encoding job progress</span></span>
<span data-ttu-id="6bdd5-162">인코딩 작업의 진행 상태를 모니터링하려면 페이지 맨 위에 있는 **설정**을 클릭한 후 **작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-162">To monitor the progress of the encoding job, click **Settings** (at the top of the page) and then select **Jobs**.</span></span>

![교육](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="6bdd5-164">콘텐츠 게시</span><span class="sxs-lookup"><span data-stu-id="6bdd5-164">Publish content</span></span>
<span data-ttu-id="6bdd5-165">콘텐츠를 스트리밍 또는 다운로드하는 데 사용할 수 있는 URL을 사용자에게 제공하려면 먼저 로케이터를 만들어 자산을 "게시"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-165">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="6bdd5-166">로케이터는 자산에 포함된 파일에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-166">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="6bdd5-167">Media Services는 두 가지 유형의 로케이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="6bdd5-168">스트리밍(OnDemandOrigin) 로케이터로, 적응 스트리밍(예: MPEG DASH, HLS 또는 부드러운 스트리밍을 스트림)에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="6bdd5-169">스트리밍 로케이터를 만들려면 자산에 .ism 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-169">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="6bdd5-170">점진적(SAS) 로케이터로, 점진적 다운로드를 통해 비디오를 배달하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="6bdd5-171">스트리밍 URL에는 다음 형식이 있으며 부드러운 스트리밍 자산을 재생하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-171">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="6bdd5-172">HLS 스트리밍 URL을 작성하려면 URL에 (format=m3u8-aapl)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-172">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="6bdd5-173">MPEG DASH 스트리밍 URL을 작성하려면 URL에 (format=mpd-time-csf)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-173">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="6bdd5-174">SAS URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-174">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="6bdd5-175">2015년 3월 이전에 로케이터를 만드는 데 포털을 사용한 경우에는 만료 날짜가 2년인 로케이터가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-175">If you used the portal to create locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="6bdd5-176">로케이터의 만료 날짜를 업데이트하려면 [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-176">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="6bdd5-177">SAS 로케이터의 만료 날짜를 업데이트할 때 해당 URL도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-177">When you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="6bdd5-178">자산을 게시하기 위해 포털을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="6bdd5-178">To use the portal to publish an asset</span></span>
<span data-ttu-id="6bdd5-179">자산을 게시하기 위해 포털을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-179">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="6bdd5-180">계정 배포 진행 상태를 보려면 **설정** > **자산**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="6bdd5-181">게시하려는 자산을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-181">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="6bdd5-182">**게시** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-182">Click the **Publish** button.</span></span>
4. <span data-ttu-id="6bdd5-183">로케이터 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-183">Select the locator type.</span></span>
5. <span data-ttu-id="6bdd5-184">**추가**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-184">Press **Add**.</span></span>
   
    ![게시](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="6bdd5-186">URL이 **게시된 URL**목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-186">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="6bdd5-187">포털에서 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="6bdd5-187">Play content from the portal</span></span>
<span data-ttu-id="6bdd5-188">Azure Portal에서는 비디오를 테스트하는 데 사용할 수 있는 콘텐츠 플레이어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-188">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="6bdd5-189">원하는 비디오를 클릭하고 **재생** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-189">Click the desired video and then click the **Play** button.</span></span>

![게시](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="6bdd5-191">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-191">Some considerations apply:</span></span>

* <span data-ttu-id="6bdd5-192">스트리밍을 시작하려면 **기본** 스트리밍 끝점 실행을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-192">To begin streaming, start running the **default** streaming endpoint.</span></span>
* <span data-ttu-id="6bdd5-193">비디오가 게시된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-193">Make sure the video has been published.</span></span>
* <span data-ttu-id="6bdd5-194">이 **미디어 플레이어**가 기본 스트리밍 끝점에서 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-194">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="6bdd5-195">기본이 아닌 스트리밍 끝점에서 재생하려면 URL 복사를 클릭하고 다른 플레이어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-195">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="6bdd5-196">예를 들어 [Azure Media Services 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bdd5-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bdd5-197">Next steps</span></span>
<span data-ttu-id="6bdd5-198">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6bdd5-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6bdd5-199">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="6bdd5-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

