---
title: "시나리오에 대한 Azure 콘텐츠 배달 최적화"
description: "특정 시나리오에 대한 콘텐츠 배달을 최적화하는 방법"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 98941c49b057380b3ef9164515bcc2a63ccb56ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a><span data-ttu-id="62363-103">시나리오에 대한 Azure 콘텐츠 배달 최적화</span><span class="sxs-lookup"><span data-stu-id="62363-103">Optimize Azure content delivery for your scenario</span></span>

<span data-ttu-id="62363-104">전 세계의 수많은 대상 고객에게 콘텐츠를 배달하는 경우 콘텐츠의 최적화된 배달을 보장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-104">When you deliver content to a large global audience, it's critical to ensure the optimized delivery of your content.</span></span> <span data-ttu-id="62363-105">Azure Content Delivery Network는 보유한 콘텐츠의 형식에 따라 배달 환경을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-105">The Azure Content Delivery Network can optimize the delivery experience based on the type of content you have.</span></span> <span data-ttu-id="62363-106">콘텐츠는 다운로드를 위한 웹 사이트, 라이브 스트림, 비디오 또는 대용량 파일일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-106">Content can be a website, a live stream, a video, or a large file for download.</span></span> <span data-ttu-id="62363-107">CDN(Content Delivery Network) 끝점을 만들 때 **Optimized for**(최적화 대상) 메뉴 옵션에서 시나리오를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-107">When you create a content delivery network (CDN) endpoint, you specify a scenario in the **Optimized for** option.</span></span> <span data-ttu-id="62363-108">선택 항목에 따라 CDN 끝점에서 배달되는 콘텐츠에 적용될 최적화가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-108">Your choice determines which optimization is applied to the content delivered from the CDN endpoint.</span></span>

<span data-ttu-id="62363-109">최적화 선택 항목은 모범 사례 동작을 사용하여 콘텐츠 배달 성능을 향상시키고 원본 서버 오프로드를 개선하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-109">Optimization choices are designed to use best-practice behaviors to improve content delivery performance and better origin offload.</span></span> <span data-ttu-id="62363-110">시나리오를 선택하면 부분 캐싱, 개체 청크, 원본 오류 다시 시도 정책 등에 대한 구성을 수정하여 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="62363-110">Your scenario choices affect performance by modifying configurations for partial caching, object chunking, and the origin failure retry policy.</span></span> 

<span data-ttu-id="62363-111">이 문서에서는 다양한 최적화 기능과 사용 시기에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-111">This article provides an overview of various optimization features and when you should use them.</span></span> <span data-ttu-id="62363-112">기능 및 제한 사항에 대한 자세한 내용은 각각의 개별 최적화 형식에 대한 해당 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62363-112">For more information on features and limitations, see the respective articles on each individual optimization type.</span></span>

> [!NOTE]
> <span data-ttu-id="62363-113">**Optimized for**(최적화 대상) 메뉴 옵션은 선택한 공급자에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-113">Your **Optimized for** options can vary based on the provider you select.</span></span> <span data-ttu-id="62363-114">CDN 공급자는 시나리오에 따라 다양한 방법으로 향상된 기능을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-114">CDN providers apply enhancement in different ways, depending on the scenario.</span></span> 

## <a name="provider-options"></a><span data-ttu-id="62363-115">공급자 옵션</span><span class="sxs-lookup"><span data-stu-id="62363-115">Provider options</span></span>

<span data-ttu-id="62363-116">Akamai의 Azure Content Delivery Network는 다음을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-116">The Azure Content Delivery Network from Akamai supports:</span></span>

* <span data-ttu-id="62363-117">일반 웹 배달</span><span class="sxs-lookup"><span data-stu-id="62363-117">General web delivery</span></span> 

* <span data-ttu-id="62363-118">일반 미디어 스트리밍</span><span class="sxs-lookup"><span data-stu-id="62363-118">General media streaming</span></span>

* <span data-ttu-id="62363-119">주문형 비디오 미디어 스트리밍</span><span class="sxs-lookup"><span data-stu-id="62363-119">Video-on-demand media streaming</span></span>

* <span data-ttu-id="62363-120">대용량 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="62363-120">Large file download</span></span>

* <span data-ttu-id="62363-121">동적 사이트 가속</span><span class="sxs-lookup"><span data-stu-id="62363-121">Dynamic site acceleration</span></span> 

<span data-ttu-id="62363-122">Verizon의 Azure Content Delivery Network는 일반 웹 배달만 지원하며,</span><span class="sxs-lookup"><span data-stu-id="62363-122">The Azure Content Delivery Network from Verizon supports general web delivery only.</span></span> <span data-ttu-id="62363-123">주문형 비디오 및 대용량 파일 다운로드에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-123">It can be used for video on demand and large file download.</span></span> <span data-ttu-id="62363-124">최적화 형식을 선택할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-124">You don't have to select an optimization type.</span></span>

<span data-ttu-id="62363-125">다양한 공급자 간의 성능 차이를 테스트하여 배달에 가장 적합한 공급자를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-125">We highly recommend that you test performance variations between different providers to select the optimal provider for your delivery.</span></span>

## <a name="select-and-configure-optimization-types"></a><span data-ttu-id="62363-126">최적화 형식 선택 및 구성</span><span class="sxs-lookup"><span data-stu-id="62363-126">Select and configure optimization types</span></span>

<span data-ttu-id="62363-127">새 끝점을 만들려면 끝점에서 제공할 시나리오 및 콘텐츠 형식과 가장 잘 맞는 최적화 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-127">To create a new endpoint, select an optimization type that best matches the scenario and type of content that you want the endpoint to deliver.</span></span> <span data-ttu-id="62363-128">**일반 웹 배달**이 기본 선택 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="62363-128">**General web delivery** is the default selection.</span></span> <span data-ttu-id="62363-129">언제든지 기존 Akamai 끝점에 대한 최적화 옵션을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-129">You can update the optimization option for any existing Akamai endpoint at any time.</span></span> <span data-ttu-id="62363-130">이러한 변경으로 인해 CDN에서 배달이 중단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-130">This change doesn't interrupt delivery from the CDN.</span></span> 

1. <span data-ttu-id="62363-131">표준 Akamai 프로필 내에서 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-131">Select an endpoint within a Standard Akamai profile.</span></span>

    ![<span data-ttu-id="62363-132">끝점 선택</span><span class="sxs-lookup"><span data-stu-id="62363-132">Endpoint selection</span></span> ](./media/cdn-optimization-overview/01_Akamai.png)

2. <span data-ttu-id="62363-133">**설정** 아래에서 **최적화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-133">Under **SETTINGS**, select **Optimization**.</span></span> <span data-ttu-id="62363-134">그런 다음 **Optimized for**(최적화 대상) 드롭다운 목록에서 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-134">Then select a type from the **Optimized for** drop-down list.</span></span>

    ![최적화 및 형식 선택](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a><span data-ttu-id="62363-136">특정 시나리오에 대한 최적화</span><span class="sxs-lookup"><span data-stu-id="62363-136">Optimization for specific scenarios</span></span>

<span data-ttu-id="62363-137">다음 시나리오 중 하나에 대해 CDN 끝점을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-137">You can optimize the CDN endpoint for one of the following scenarios.</span></span> 

### <a name="general-web-delivery"></a><span data-ttu-id="62363-138">일반 웹 배달</span><span class="sxs-lookup"><span data-stu-id="62363-138">General web delivery</span></span>

<span data-ttu-id="62363-139">일반 웹 배달은 가장 일반적인 최적화 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="62363-139">General web delivery is the most common optimization option.</span></span> <span data-ttu-id="62363-140">웹 페이지 및 웹 응용 프로그램과 같은 일반 웹 콘텐츠 최적화를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-140">It's designed for general web content optimization, such as webpages and web applications.</span></span> <span data-ttu-id="62363-141">이 최적화는 파일 및 비디오 다운로드에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-141">This optimization also can be used for file and video downloads.</span></span>

<span data-ttu-id="62363-142">일반적인 웹 사이트에는 정적 및 동적 콘텐츠가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-142">A typical website contains static and dynamic content.</span></span> <span data-ttu-id="62363-143">정적 콘텐츠는 캐시되고 다른 사용자에게 배달될 수 있는 이미지, JavaScript 라이브러리 및 스타일시트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-143">Static content includes images, JavaScript libraries, and style sheets that can be cached and delivered to different users.</span></span> <span data-ttu-id="62363-144">동적 콘텐츠는 사용자 프로필에 맞게 조정된 뉴스 항목과 같이 개별 사용자에 맞게 개인 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-144">Dynamic content is personalized for an individual user, such as news items that are tailored to a user profile.</span></span> <span data-ttu-id="62363-145">동적 콘텐츠는 쇼핑 카트 콘텐츠와 같이 각 사용자에게 고유하기 때문에 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-145">Dynamic content isn't cached because it's unique to each user, such as shopping cart contents.</span></span> <span data-ttu-id="62363-146">일반 웹 배달은 전체 웹 사이트를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-146">General web delivery can optimize your entire website.</span></span> 

> [!NOTE]
> <span data-ttu-id="62363-147">Akamai의 Azure Content Delivery Network를 사용하는 경우 평균 파일 크기가 10MB보다 작으면 이 최적화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-147">If you use the Azure Content Delivery Network from Akamai, you might want to use this optimization if your average file size is smaller than 10 MB.</span></span> <span data-ttu-id="62363-148">평균 파일 크기가 10MB보다 큰 경우 **Optimized for**(최적화 대상) 드롭다운 목록에서 **대용량 파일 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-148">If your average file size is larger than 10 MB, select **Large file download** from the **Optimized for** drop-down list.</span></span>

### <a name="general-media-streaming"></a><span data-ttu-id="62363-149">일반 미디어 스트리밍</span><span class="sxs-lookup"><span data-stu-id="62363-149">General media streaming</span></span>

<span data-ttu-id="62363-150">라이브 스트리밍과 주문형 비디오 스트리밍에 끝점을 사용해야 하는 경우 일반 미디어 스트리밍 최적화가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-150">If you need to use the endpoint for live streaming and video-on-demand streaming, we recommend general media streaming optimization.</span></span>

<span data-ttu-id="62363-151">클라이언트에 늦게 도착하는 패킷으로 인해 비디오 콘텐츠의 잦은 버퍼링과 같이 시청 환경이 저하될 수 있으므로 미디어 스트리밍은 시간에 민감합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-151">Media streaming is time sensitive, because packets that arrive late on the client can cause a degraded viewing experience, such as frequent buffering of video content.</span></span> <span data-ttu-id="62363-152">미디어 스트리밍 최적화는 미디어 콘텐츠 배달의 대기 시간을 줄이고 최종 사용자에게 부드러운 스트리밍 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-152">Media streaming optimization reduces the latency of media content delivery and provides a smooth streaming experience for users.</span></span> 

<span data-ttu-id="62363-153">이 시나리오는 Azure Media Service 고객에게 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="62363-153">This scenario is common for Azure media service customers.</span></span> <span data-ttu-id="62363-154">Azure Media Services를 사용하면 하나의 스트리밍 끝점을 라이브 스트리밍과 주문형 스트리밍 둘 다에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-154">When you use Azure media services, you get one streaming endpoint that can be used for both live and on-demand streaming.</span></span> <span data-ttu-id="62363-155">이 시나리오에서는 고객이 라이브 스트리밍에서 주문형 스트리밍으로 변경할 때 다른 끝점으로 전환할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-155">With this scenario, customers don't need to switch to another endpoint when they change from live to on-demand streaming.</span></span> <span data-ttu-id="62363-156">일반 미디어 스트리밍 최적화는 이 유형의 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-156">General media streaming optimization supports this type of scenario.</span></span>

<span data-ttu-id="62363-157">Verizon의 Azure Content Delivery Network는 일반 웹 배달 최적화 형식을 사용하여 스트리밍 미디어 콘텐츠를 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-157">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="62363-158">미디어 스트리밍 최적화에 대한 자세한 내용은 [미디어 스트리밍 최적화](cdn-media-streaming-optimization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62363-158">To learn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

### <a name="video-on-demand-media-streaming"></a><span data-ttu-id="62363-159">주문형 비디오 미디어 스트리밍</span><span class="sxs-lookup"><span data-stu-id="62363-159">Video-on-demand media streaming</span></span>

<span data-ttu-id="62363-160">주문형 비디오 미디어 스트리밍 최적화는 주문형 비디오 스트리밍 콘텐츠를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="62363-160">Video-on-demand media streaming optimization improves video-on-demand streaming content.</span></span> <span data-ttu-id="62363-161">주문형 비디오 스트리밍에 끝점을 사용하는 경우 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-161">If you use an endpoint for video-on-demand streaming, you might want to use this option.</span></span>

<span data-ttu-id="62363-162">Verizon의 Azure Content Delivery Network는 일반 웹 배달 최적화 형식을 사용하여 스트리밍 미디어 콘텐츠를 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-162">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="62363-163">미디어 스트리밍 최적화에 대한 자세한 내용은 [미디어 스트리밍 최적화](cdn-media-streaming-optimization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62363-163">To learn more about media streaming optimization, see [Media streaming optimization](cdn-media-streaming-optimization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="62363-164">끝점에서 주로 주문형 비디오 콘텐츠를 제공하는 경우 이 최적화 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-164">If the endpoint primarily serves video-on-demand content, use this optimization type.</span></span> <span data-ttu-id="62363-165">이 최적화와 일반 미디어 스트리밍 최적화 사이의 주요 차이점은 연결 다시 시도 시간 제한에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-165">The major difference between this optimization and the general media streaming optimization is the connection retry time-out.</span></span> <span data-ttu-id="62363-166">라이브 스트리밍 시나리오를 사용하는 경우 시간 제한이 더 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-166">The time-out is much shorter to work with live streaming scenarios.</span></span>

### <a name="large-file-download"></a><span data-ttu-id="62363-167">대용량 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="62363-167">Large file download</span></span>

<span data-ttu-id="62363-168">Akamai의 Azure Content Delivery Network를 사용하는 경우 대용량 파일 다운로드를 사용하여 1.8GB보다 큰 파일을 배달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62363-168">If you use the Azure Content Delivery Network from Akamai, you must use large file download to deliver files larger than 1.8 GB.</span></span> <span data-ttu-id="62363-169">Verizon의 Azure Content Delivery Network에서는 일반 웹 배달 최적화의 파일 다운로드 크기에 대한 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-169">The Azure Content Delivery Network from Verizon doesn't have a limitation on file download size in its general web delivery optimization.</span></span>

<span data-ttu-id="62363-170">Akamai의 Azure Content Delivery Network를 사용하는 경우 대용량 파일 다운로드가 10MB보다 큰 콘텐츠에 대해 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-170">If you use the Azure Content Delivery Network from Akamai, large file downloads are optimized for content larger than 10 MB.</span></span> <span data-ttu-id="62363-171">평균 파일 크기가 10MB보다 작은 경우 일반 웹 배달을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-171">If your average file size is smaller than 10 MB, you might want to use general web delivery.</span></span> <span data-ttu-id="62363-172">평균 파일 크기가 일관되게 10MB보다 큰 경우 대용량 파일에 대해 별도의 끝점을 만드는 것이 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-172">If your average files sizes are consistently larger than 10 MB, it might be more efficient to create a separate endpoint for large files.</span></span> <span data-ttu-id="62363-173">예를 들어 펌웨어 또는 소프트웨어 업데이트는 일반적으로 대용량 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="62363-173">For example, firmware or software updates typically are large files.</span></span>

<span data-ttu-id="62363-174">Verizon의 Azure Content Delivery Network는 일반 웹 배달 최적화 형식을 사용하여 스트리밍 미디어 콘텐츠를 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-174">The Azure Content Delivery Network from Verizon uses the general web delivery optimization type to deliver streaming media content.</span></span>

<span data-ttu-id="62363-175">대용량 파일 최적화에 대한 자세한 내용은 [대용량 파일 최적화](cdn-large-file-optimization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62363-175">To learn more about large file optimization, see [Large file optimization](cdn-large-file-optimization.md).</span></span>

### <a name="dynamic-site-acceleration"></a><span data-ttu-id="62363-176">동적 사이트 가속</span><span class="sxs-lookup"><span data-stu-id="62363-176">Dynamic site acceleration</span></span>

 <span data-ttu-id="62363-177">동적 사이트 가속은 Akamai 및 Verizon Content Delivery Network 프로필에서 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-177">Dynamic site acceleration is available from both Akamai and Verizon Content Delivery Network profiles.</span></span> <span data-ttu-id="62363-178">이 최적화는 추가 사용 요금에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-178">This optimization involves an additional fee to use.</span></span> <span data-ttu-id="62363-179">자세한 내용은 가격 책정 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62363-179">For more information, see the pricing page.</span></span>

<span data-ttu-id="62363-180">동적 사이트 가속에는 동적 콘텐츠의 대기 시간과 성능에 도움이 되는 다양한 기술이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-180">Dynamic site acceleration includes various techniques that benefit the latency and performance of dynamic content.</span></span> <span data-ttu-id="62363-181">경로 및 네트워크 최적화, TCP 최적화 등이 이러한 기술에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="62363-181">Techniques include route and network optimization, TCP optimization, and more.</span></span> 

<span data-ttu-id="62363-182">이 최적화를 사용하여 캐시할 수 없는 수많은 응답을 포함하는 웹앱을 가속화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-182">You can use this optimization to accelerate a web app that includes numerous responses that aren't cacheable.</span></span> <span data-ttu-id="62363-183">예를 들어 검색 결과, 체크 아웃 트랜잭션 또는 실시간 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-183">Examples are search results, checkout transactions, or real-time data.</span></span> <span data-ttu-id="62363-184">정적 데이터에 대해 핵심 CDN 캐싱 기능을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62363-184">You can continue to use core CDN caching capabilities for static data.</span></span> 



