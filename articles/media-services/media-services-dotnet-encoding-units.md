---
title: "Azure-는 인코딩 단위를 추가 하 여 처리 aaaScale 미디어 |  Microsoft Docs"
description: "자세한 내용은 방법.net toohow tooadd 인코딩 단위"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="b05db-103">어떻게 tooscale.NET SDK와 인코딩</span><span class="sxs-lookup"><span data-stu-id="b05db-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b05db-104">포털</span><span class="sxs-lookup"><span data-stu-id="b05db-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="b05db-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b05db-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="b05db-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b05db-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="b05db-107">Java</span><span class="sxs-lookup"><span data-stu-id="b05db-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="b05db-108">PHP</span><span class="sxs-lookup"><span data-stu-id="b05db-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="b05db-109">개요</span><span class="sxs-lookup"><span data-stu-id="b05db-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b05db-110">있는지 tooreview hello 확인 [개요](media-services-scale-media-processing-overview.md) 항목 tooget 항목을 처리 하는 미디어 확장에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="b05db-111">toochange hello 예약 단위 형식 및 hello 수가 인코딩 예약된 단위.NET SDK를 사용 하 여 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="b05db-112">지원 티켓 열기</span><span class="sxs-lookup"><span data-stu-id="b05db-112">Opening a Support Ticket</span></span>
<span data-ttu-id="b05db-113">기본적으로 모든 미디어 서비스 계정은 tooup too25 확장할 수 인코딩 및 5 주문형 스트리밍 예약 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="b05db-114">지원 티켓을 열어 더 높은 한도를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="b05db-115">지원 티켓 열기</span><span class="sxs-lookup"><span data-stu-id="b05db-115">Open a support ticket</span></span>
<span data-ttu-id="b05db-116">지원 티켓 tooopen 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="b05db-117">[지원 받기](https://manage.windowsazure.com/?getsupport=true)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="b05db-118">로그인 하지 않은 경우 자격 증명 프롬프트 tooenter 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="b05db-119">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-119">Select your subscription.</span></span>
3. <span data-ttu-id="b05db-120">지원 유형으로 "기술적"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="b05db-121">"티켓 만들기"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="b05db-122">"Azure 미디어 서비스" hello 제품 목록에서 hello 다음 페이지에 표시를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="b05db-123">사용자의 문제에 적절한 "문제 유형"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="b05db-124">계속을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-124">Click Continue.</span></span>
8. <span data-ttu-id="b05db-125">다음 페이지의 지시에 따라 문제에 대한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="b05db-126">클릭은 tooopen hello 티켓을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b05db-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b05db-127">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b05db-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b05db-128">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b05db-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

