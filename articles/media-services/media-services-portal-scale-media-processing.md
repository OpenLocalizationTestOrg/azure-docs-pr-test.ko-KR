---
title: "사용 하 여 처리 aaaScale 미디어 hello Azure 포털 | Microsoft Docs"
description: "이 자습서에서는 hello Azure 포털을 사용 하 여 처리 하는 크기 조정 미디어의 hello 단계를 안내 합니다."
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="bcf68-103">Hello 예약 단위 형식 변경</span><span class="sxs-lookup"><span data-stu-id="bcf68-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcf68-104">.NET</span><span class="sxs-lookup"><span data-stu-id="bcf68-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="bcf68-105">포털</span><span class="sxs-lookup"><span data-stu-id="bcf68-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="bcf68-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="bcf68-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="bcf68-107">Java</span><span class="sxs-lookup"><span data-stu-id="bcf68-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="bcf68-108">PHP</span><span class="sxs-lookup"><span data-stu-id="bcf68-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="bcf68-109">개요</span><span class="sxs-lookup"><span data-stu-id="bcf68-109">Overview</span></span>

<span data-ttu-id="bcf68-110">미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약 된 단위 유형과 연관 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="bcf68-111">Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="bcf68-112">Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="bcf68-113">또한 toospecifying hello 예약 단위 형식, tooprovision를 사용 하 여 계정을 지정할 수 있습니다 **예약 단위** (RUs).</span><span class="sxs-lookup"><span data-stu-id="bcf68-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="bcf68-114">프로 비전 된 RUs hello 수 hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="bcf68-115">RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="bcf68-116">그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf68-117">있는지 tooreview hello 확인 [개요](media-services-scale-media-processing-overview.md) 항목 tooget 항목을 처리 하는 미디어 확장에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="bcf68-118">미디어 처리 크기 조정</span><span class="sxs-lookup"><span data-stu-id="bcf68-118">Scale media processing</span></span>
<span data-ttu-id="bcf68-119">toochange hello 예약 단위 형식 및 hello 예약된 단위 수를 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="bcf68-120">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="bcf68-121">Hello에 **설정** 창에서 **미디어 예약 단위**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="bcf68-122">예약된 단위 형식 너무 많이 선택 hello에 대 한 예약 단위 toochange hello 수, hello를 사용 하 여 **미디어 처리 단위** 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="bcf68-123">toochange hello **예약 단위 형식**, S1, S2 또는 S3 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![프로세서 페이지](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="bcf68-125">단추 toosave 변경 내용을 저장 하는 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="bcf68-126">저장 단추를 누를 때 hello 새 예약된 단위 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcf68-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcf68-127">Next steps</span></span>
<span data-ttu-id="bcf68-128">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf68-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bcf68-129">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="bcf68-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

