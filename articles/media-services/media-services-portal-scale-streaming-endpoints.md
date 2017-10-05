---
title: "Azure Portal을 통해 스트리밍 끝점 크기 조정 | Microsoft 문서"
description: "이 자습서에서는 Azure 포털을 사용하여 스트리밍 끝점의 크기를 조정하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="6a310-103">Azure 포털을 통해 스트리밍 끝점 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6a310-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="6a310-104">개요</span><span class="sxs-lookup"><span data-stu-id="6a310-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="6a310-105">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6a310-106">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a310-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="6a310-107">**프리미엄** 스트리밍 끝점은 고급 워크로드에 적합하며, 확장성 있는 전용 대역폭 용량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="6a310-108">**프리미엄** 스트리밍 끝점이 있는 고객은 기본적으로 하나의 SU(스트리밍 단위)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="6a310-109">SU를 추가하여 스트리밍 끝점의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="6a310-110">각 SU는 응용 프로그램에 추가 대역폭 수용작업량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="6a310-111">스트리밍 끝점 유형 및 CDN 구성에 대한 자세한 내용은 [스트리밍 끝점 개요](media-services-portal-manage-streaming-endpoints.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a310-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="6a310-112">이 항목에서는 스트리밍 끝점의 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="6a310-113">가격 정보에 대한 자세한 내용은 [미디어 서비스 가격 정보](http://go.microsoft.com/fwlink/?LinkId=275107)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a310-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="6a310-114">스트리밍 끝점 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6a310-114">Scale streaming endpoints</span></span>

<span data-ttu-id="6a310-115">스트리밍 단위 수를 변경하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="6a310-116">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="6a310-117">**설정** 창에서 **스트리밍 끝점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="6a310-118">크기를 조정할 스트리밍 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="6a310-119">**프리미엄** 스트리밍 끝점의 크기만 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="6a310-120">슬라이더를 이동하여 스트리밍 단위 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-120">Move the slider to specify the number of streaming units.</span></span>

    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="6a310-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a310-122">Next steps</span></span>
<span data-ttu-id="6a310-123">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6a310-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a310-124">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="6a310-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

