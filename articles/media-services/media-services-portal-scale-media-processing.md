---
title: "Azure Portal을 사용하여 미디어 처리 크기 조정 | Microsoft Docs"
description: "이 자습서에서는 Azure Portal을 사용하여 미디어 처리의 크기를 조정하는 단계를 안내합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="6ada5-103">예약 단위 유형 변경</span><span class="sxs-lookup"><span data-stu-id="6ada5-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ada5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6ada5-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="6ada5-105">포털</span><span class="sxs-lookup"><span data-stu-id="6ada5-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="6ada5-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="6ada5-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="6ada5-107">Java</span><span class="sxs-lookup"><span data-stu-id="6ada5-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="6ada5-108">PHP</span><span class="sxs-lookup"><span data-stu-id="6ada5-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="6ada5-109">개요</span><span class="sxs-lookup"><span data-stu-id="6ada5-109">Overview</span></span>

<span data-ttu-id="6ada5-110">미디어 서비스 계정은 미디어 처리 작업을 처리하는 속도를 결정하는 예약 단위 형식과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="6ada5-111">**S1**, **S2**, **S3** 예약 단위 유형 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="6ada5-112">예를 들어 **S2** 예약 단위 유형을 사용하는 경우 **S1** 유형에 비해 동일한 인코딩 작업이 더 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="6ada5-113">예약 단위 유형을 지정하는 것 외에도 계정에 **RU(예약 단위)**를 프로비전하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="6ada5-114">프로비전되는 RU의 수에 따라 특정 계정에서 동시에 처리할 수 있는 미디어 작업의 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="6ada5-115">RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="6ada5-116">그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ada5-117">미디어 처리 크기 조정에 대해 자세히 알아보려면 이 [개요](media-services-scale-media-processing-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ada5-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="6ada5-118">미디어 처리 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6ada5-118">Scale media processing</span></span>
<span data-ttu-id="6ada5-119">예약 단위 유형 및 예약 단위 수를 변경하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="6ada5-120">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="6ada5-121">**설정** 창에서 **미디어 예약 단위**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="6ada5-122">선택한 예약 단위 유형의 예약 단위 수를 변경하려면 **미디어 예약 단위** 슬라이더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="6ada5-123">**예약 단위 형식**을 변경하려면 S1, S2 또는 S3을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![프로세서 페이지](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="6ada5-125">저장 단추를 눌러 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="6ada5-126">저장을 누르면 새 예약 단위가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ada5-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ada5-127">Next steps</span></span>
<span data-ttu-id="6ada5-128">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6ada5-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6ada5-129">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="6ada5-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

