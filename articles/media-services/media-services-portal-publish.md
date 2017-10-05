---
title: "  Azure Portal을 통해 콘텐츠 게시 | Microsoft 문서"
description: "이 자습서에서는 Azure 포털을 통해 콘텐츠를 게시하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="563df-103">Azure 포털을 통해 콘텐츠 게시</span><span class="sxs-lookup"><span data-stu-id="563df-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="563df-104">포털</span><span class="sxs-lookup"><span data-stu-id="563df-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="563df-105">.NET</span><span class="sxs-lookup"><span data-stu-id="563df-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="563df-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="563df-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="563df-107">개요</span><span class="sxs-lookup"><span data-stu-id="563df-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="563df-108">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="563df-109">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="563df-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="563df-110">콘텐츠를 스트리밍 또는 다운로드하는 데 사용할 수 있는 URL을 사용자에게 제공하려면 먼저 로케이터를 만들어 자산을 "게시"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="563df-111">로케이터는 자산에 포함된 파일에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="563df-112">Media Services는 두 가지 유형의 로케이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="563df-113">스트리밍(OnDemandOrigin) 로케이터로, 적응 스트리밍(예: MPEG DASH, HLS 또는 부드러운 스트리밍을 스트림)에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="563df-114">스트리밍 로케이터를 만들려면 자산에 .ism 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="563df-115">점진적(SAS) 로케이터로, 점진적 다운로드를 통해 비디오를 배달하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="563df-116">스트리밍 URL에는 다음 형식이 있으며 부드러운 스트리밍 자산을 재생하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="563df-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="563df-117">HLS 스트리밍 URL을 작성하려면 URL에 (format=m3u8-aapl)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="563df-118">MPEG DASH 스트리밍 URL을 작성하려면 URL에 (format=mpd-time-csf)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="563df-119">SAS URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="563df-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="563df-120">자세한 내용은 [콘텐츠 제공 개요](media-services-deliver-content-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="563df-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="563df-121">2015년 3월 이전에 로케이터를 만드는 데 포털을 사용한 경우에는 만료 날짜가 2년인 로케이터가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="563df-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="563df-122">로케이터의 만료 날짜를 업데이트하려면 [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) 또는 [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="563df-123">SAS 로케이터의 만료 날짜를 업데이트할 때 해당 URL도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="563df-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="563df-124">자산을 게시하기 위해 포털을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="563df-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="563df-125">자산을 게시하기 위해 포털을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="563df-126">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="563df-127">계정 배포 진행 상태를 보려면 **설정** > **자산**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="563df-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="563df-128">게시하려는 자산을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="563df-129">**게시** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="563df-130">로케이터 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-130">Select the locator type.</span></span>
6. <span data-ttu-id="563df-131">**추가**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="563df-131">Press **Add**.</span></span>
   
    ![게시](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="563df-133">URL이 **게시된 URL**목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="563df-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="563df-134">포털에서 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="563df-134">Play content from the portal</span></span>
<span data-ttu-id="563df-135">Azure Portal에서는 비디오를 테스트하는 데 사용할 수 있는 콘텐츠 플레이어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="563df-136">원하는 비디오를 클릭하고 **재생** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-136">Click the desired video and then click the **Play** button.</span></span>

![게시](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="563df-138">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="563df-138">Some considerations apply:</span></span>

* <span data-ttu-id="563df-139">비디오가 게시된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="563df-140">이 **미디어 플레이어**가 기본 스트리밍 끝점에서 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="563df-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="563df-141">기본이 아닌 스트리밍 끝점에서 재생하려면 URL 복사를 클릭하고 다른 플레이어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="563df-142">예를 들어 [Azure 미디어 서비스 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="563df-143">스트리밍을 하고 있는 스트리밍 끝점이 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="563df-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="563df-144">Next steps</span></span>
<span data-ttu-id="563df-145">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="563df-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="563df-146">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="563df-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

