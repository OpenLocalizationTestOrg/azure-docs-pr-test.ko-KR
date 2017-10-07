---
title: "hello Azure 포털을 사용 하 여 끝점을 스트리밍 aaaScale | Microsoft Docs"
description: "이 자습서에서는 Azure 포털 hello로 스트리밍 끝점 확장 hello 절차를 안내 합니다."
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
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="6bcdf-103">Azure 포털 hello로 스트리밍 끝점의 크기를 조정합니다</span><span class="sxs-lookup"><span data-stu-id="6bcdf-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="6bcdf-104">개요</span><span class="sxs-lookup"><span data-stu-id="6bcdf-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="6bcdf-105">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6bcdf-106">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="6bcdf-107">**프리미엄** 스트리밍 끝점은 고급 워크로드에 적합하며, 확장성 있는 전용 대역폭 용량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="6bcdf-108">**프리미엄** 스트리밍 끝점이 있는 고객은 기본적으로 하나의 SU(스트리밍 단위)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="6bcdf-109">SUs를 추가 하 여 hello 스트리밍 끝점을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="6bcdf-110">각 SU 대역폭도 추가로 용량 toohello 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="6bcdf-111">스트리밍 끝점 유형 및 CDN 구성에 대 한 자세한 내용은 참조 hello [스트리밍 끝점 개요](media-services-portal-manage-streaming-endpoints.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="6bcdf-112">이 항목에서는 방법을 tooscale 스트리밍 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="6bcdf-113">가격 정보에 대한 자세한 내용은 [미디어 서비스 가격 정보](http://go.microsoft.com/fwlink/?LinkId=275107)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="6bcdf-114">스트리밍 끝점 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6bcdf-114">Scale streaming endpoints</span></span>

<span data-ttu-id="6bcdf-115">스트리밍 단위 toochange hello 수 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="6bcdf-116">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="6bcdf-117">Hello에 **설정** 창에서 **스트리밍 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="6bcdf-118">원하는 tooscale hello 스트리밍 끝점에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="6bcdf-119">**프리미엄** 스트리밍 끝점의 크기만 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="6bcdf-120">스트리밍 단위 hello 슬라이더 toospecify hello 수를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![스트리밍 끝점](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="6bcdf-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bcdf-122">Next steps</span></span>
<span data-ttu-id="6bcdf-123">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6bcdf-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6bcdf-124">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="6bcdf-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

