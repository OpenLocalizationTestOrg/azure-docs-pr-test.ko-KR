---
title: "Azure Portal을 통해 Media Encoder Standard을 사용하여 자산 인코딩 | Microsoft 문서"
description: "이 자습서에서는 Azure Portal을 통해 미디어 인코더 표준을 사용하여 자산을 인코딩하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="3c6cc-103">Azure Portal을 통해 미디어 인코더 표준을 사용하여 자산 인코딩</span><span class="sxs-lookup"><span data-stu-id="3c6cc-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3c6cc-104">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3c6cc-105">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="3c6cc-106">Azure Media Services 작업 시 가장 일반적인 시나리오 중 하나는 클라이언트에 적응 비트 전송률 스트리밍을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="3c6cc-107">Media Services에서 지원하는 적응 비트 전송률 스트리밍은 HLS(HTTP 라이브 스트리밍), 부드러운 스트리밍, MPEG-DASH입니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="3c6cc-108">적응 비트 전송률 스트리밍을 위한 비디오를 준비하려면 소스 비디오를 다중 비트 전송률 파일로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="3c6cc-109">비디오를 인코딩하는 데는 **미디어 인코더 표준** 인코더를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="3c6cc-110">Media Services는 다중 비트 전송률 MP4를 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍)으로 다시 패키지하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="3c6cc-111">동적 패키징에서는 단일 저장소 형식으로 파일을 저장하고 비용을 지불하기만 하면 됩니다. 그러면 Media Services가 클라이언트의 요청에 따라 적절한 응답을 빌드 및 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3c6cc-112">동적 패키징을 활용하려면 원본 파일을 다중 비트 전송률 MP4 파일 집합으로 인코딩해야 합니다(인코딩 단계는 이 섹션의 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="3c6cc-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="3c6cc-113">미디어 처리의 크기를 조정하려면 [이 항목](media-services-portal-scale-media-processing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="3c6cc-114">Azure Portal을 통해 인코딩</span><span class="sxs-lookup"><span data-stu-id="3c6cc-114">Encode with the Azure portal</span></span>
<span data-ttu-id="3c6cc-115">이 섹션에서는 미디어 인코더 표준을 사용하여 콘텐츠를 인코딩할 수 있는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="3c6cc-116">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3c6cc-117">**설정** 창에서 **자산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="3c6cc-118">**자산** 창에서 인코딩할 자산을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="3c6cc-119">**인코딩** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="3c6cc-120">**자산 인코딩** 창에서 "Media Encoder Standard" 프로세서 및 사전 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="3c6cc-121">기본 설정에 대한 자세한 내용은 [비트 전송률 래더 자동 생성](media-services-autogen-bitrate-ladder-with-mes.md) 및 [MES에 대한 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="3c6cc-122">사용하는 인코딩 기본 설정을 제어하려는 경우 입력 비디오에 가장 적합한 기본 설정을 선택하는 것이 중요하다는 사실을 유념하세요.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="3c6cc-123">예를 들어 입력 비디오가 1920x1080픽셀 해상도를 포함하는 것을 알고 있는 경우 "H264 다중 비트 전송률 1080p" 사전 설정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="3c6cc-124">낮은 해상도(640x360) 비디오가 있는 경우 기본 “H264 다중 비트 전송률 1080p” 기본 설정을 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="3c6cc-125">관리를 간소화하기 위해 출력 자산의 이름과 작업 이름을 편집하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![자산 인코딩](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="3c6cc-127">**만들기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="3c6cc-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c6cc-128">Next step</span></span>
<span data-ttu-id="3c6cc-129">[이 문서](media-services-portal-check-job-progress.md) 의 설명에 따라 Azure Portal을 통해 인코딩 작업 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c6cc-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="3c6cc-130">Media Services 학습 경로</span><span class="sxs-lookup"><span data-stu-id="3c6cc-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c6cc-131">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="3c6cc-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

