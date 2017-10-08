---
title: "미디어 인코더 표준 Azure 포털 hello로 사용 하 여 자산 aaaEncode | Microsoft Docs"
description: "이 자습서는 Azure 포털 hello로 미디어 인코더 표준를 사용 하 여 자산 인코딩 hello 단계를 안내 합니다."
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
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="a8dc8-103">미디어 인코더 표준 Azure 포털 hello로 사용 하 여 자산을 인코딩하</span><span class="sxs-lookup"><span data-stu-id="a8dc8-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="a8dc8-104">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a8dc8-105">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="a8dc8-106">적응 비트 전송률 스트리밍 tooyour 클라이언트 제공 하는 hello 가장 일반적인 시나리오 중 하나는 Azure 미디어 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="a8dc8-107">미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술에 따라 지원: HLS HTTP 라이브 스트리밍 (), 부드러운 스트리밍, MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="a8dc8-108">tooprepare 비디오 적응 비트 전송률 스트리밍에 대 한 필요한 tooencode 원본 비디오를 다중 비트 전송률 파일로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="a8dc8-109">Hello를 사용 해야 **미디어 인코더 표준** 인코더 tooencode 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="a8dc8-110">또한 미디어 서비스 제공 toodeliver 수 있는 동적 패키징 hello 스트리밍 형식 뒤에 여 다중 비트 전송률 mp4: MPEG DASH, HLS, 부드러운 스트리밍 형식 스트리밍을로 toore 패키지 필요 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="a8dc8-111">동적 패키징을 사용 하면 toostore 및 단일 저장소 형식 및 미디어 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="a8dc8-112">tootake 이점은 동적 패키징을 tooencode 소스 파일에 필요한 (hello 인코딩 단계는이 섹션의 나중에 설명 된) 다중 비트 전송률 MP4 파일 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="a8dc8-113">처리 tooscale 미디어 참조 [이](media-services-portal-scale-media-processing.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="a8dc8-114">Azure 포털 hello로 인코딩</span><span class="sxs-lookup"><span data-stu-id="a8dc8-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="a8dc8-115">이 섹션에서는 프록시 hello tooencode 미디어 인코더 표준 사용 하 여 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="a8dc8-116">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a8dc8-117">Hello에 **설정** 창에서 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="a8dc8-118">Hello에 **자산** 창, 싶다는 의사를 tooencode 선택 hello 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="a8dc8-119">키를 눌러 hello **인코딩** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="a8dc8-120">Hello에 **자산을 인코딩하** 창, "미디어 인코더 표준" 선택 hello 프로세서 및 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="a8dc8-121">기본 설정에 대한 자세한 내용은 [비트 전송률 래더 자동 생성](media-services-autogen-bitrate-ladder-with-mes.md) 및 [MES에 대한 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="a8dc8-122">Toocontrol 어떤 인코딩 사전 설정을 사용 하려는 경우이 점을 명심: tooselect hello 입력된 비디오에 가장 적합 하는 미리 설정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="a8dc8-123">예를 들어 입력된 비디오 1920 x 1080 픽셀이 고 해상도 알고 있는 경우 다음 사용할 수 있습니다 hello "H264 다중 비트 전송률 1080p" 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="a8dc8-124">낮은 해상도(640x360) 비디오가 있는 경우 기본 “H264 다중 비트 전송률 1080p” 기본 설정을 사용하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="a8dc8-125">관리를 간소화 하기 hello 출력 자산 편집 hello 이름 및 hello 작업의 hello 이름은 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![자산 인코딩](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="a8dc8-127">**만들기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="a8dc8-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8dc8-128">Next step</span></span>
<span data-ttu-id="a8dc8-129">에 설명 된 대로 hello Azure 포털을 사용 하 여 인코딩 작업 진행률을 모니터링할 수 있습니다 [이](media-services-portal-check-job-progress.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a8dc8-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="a8dc8-130">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a8dc8-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8dc8-131">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a8dc8-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

