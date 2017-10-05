---
title: "Azure CDN에서 HTTP/2 지원 | Microsoft Docs"
description: "HTTP/2 및 CDN 지원에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="a8e5b-103">Azure CDN에서 HTTP/2 지원</span><span class="sxs-lookup"><span data-stu-id="a8e5b-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="a8e5b-104">HTTP/2는 HTTP/1.1\ 주 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="a8e5b-105">웹 성능, 감소 응답 시간 및 향상 된 사용자 경험을 친숙 한 HTTP 메서드, 상태 코드 및 의미 체계를 유지 하면서 더 빠르게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="a8e5b-106">HTTP/2는 HTTP 및 HTTPS와 함께 작동하도록 설계되었지만 많은 클라이언트 웹 브라우저는 TLS를 통한 HTTP/2만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="a8e5b-107">HTTP/2 이점</span><span class="sxs-lookup"><span data-stu-id="a8e5b-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="a8e5b-108">HTTP/2의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="a8e5b-109">**멀티플렉싱 및 동시성**</span><span class="sxs-lookup"><span data-stu-id="a8e5b-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="a8e5b-110">HTTP 1.1을 사용하여 여러 개의 리소스 요청을 여러 번 수행하려면 여러 개의 TCP 연결이 필요하며 각 연결에는 이와 관련된 성능 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="a8e5b-111">HTTP/2를 통해 단일 TCP 연결에서 여러 리소스가 요청되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="a8e5b-112">**헤더 압축**</span><span class="sxs-lookup"><span data-stu-id="a8e5b-112">**Header compression**</span></span>

    <span data-ttu-id="a8e5b-113">제공된 리소스에 대한 HTTP 헤더를 압축하여 통신 시간을 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="a8e5b-114">**스트림 종속성**</span><span class="sxs-lookup"><span data-stu-id="a8e5b-114">**Stream dependencies**</span></span>

    <span data-ttu-id="a8e5b-115">스트림 종속성을 통해 클라이언트가 우선 순위가 높은 리소스를 서버에 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="a8e5b-116">HTTP/2 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="a8e5b-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="a8e5b-117">모든 주요 브라우저는 최신 버전에서 HTTP/2 지원을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="a8e5b-118">지원되지 않는 브라우저는 HTTP/1.1로 자동으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="a8e5b-119">브라우저</span><span class="sxs-lookup"><span data-stu-id="a8e5b-119">Browser</span></span>|<span data-ttu-id="a8e5b-120">최소 버전</span><span class="sxs-lookup"><span data-stu-id="a8e5b-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="a8e5b-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="a8e5b-121">Microsoft Edge</span></span>| <span data-ttu-id="a8e5b-122">12</span><span class="sxs-lookup"><span data-stu-id="a8e5b-122">12</span></span>|
|<span data-ttu-id="a8e5b-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="a8e5b-123">Google Chrome</span></span>| <span data-ttu-id="a8e5b-124">43</span><span class="sxs-lookup"><span data-stu-id="a8e5b-124">43</span></span>|
|<span data-ttu-id="a8e5b-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="a8e5b-125">Mozilla Firefox</span></span>| <span data-ttu-id="a8e5b-126">38</span><span class="sxs-lookup"><span data-stu-id="a8e5b-126">38</span></span>|
|<span data-ttu-id="a8e5b-127">Opera</span><span class="sxs-lookup"><span data-stu-id="a8e5b-127">Opera</span></span>| <span data-ttu-id="a8e5b-128">32</span><span class="sxs-lookup"><span data-stu-id="a8e5b-128">32</span></span>|
|<span data-ttu-id="a8e5b-129">Safari</span><span class="sxs-lookup"><span data-stu-id="a8e5b-129">Safari</span></span>| <span data-ttu-id="a8e5b-130">9</span><span class="sxs-lookup"><span data-stu-id="a8e5b-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="a8e5b-131">Azure CDN에서 HTTP/2 지원 활성화</span><span class="sxs-lookup"><span data-stu-id="a8e5b-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="a8e5b-132">현재 **Akamai의 Azure CDN** 및 **Verizon의 Azure CDN** 프로필에 대해 HTTP/2 지원이 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="a8e5b-133">고객의 별도의 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="a8e5b-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8e5b-134">Next Steps</span></span>

<span data-ttu-id="a8e5b-135">실제 HTTP/2의 이점을 보려면 [Akamai의 데모](https://http2.akamai.com/demo)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="a8e5b-136">HTTP/2에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="a8e5b-137">HTTP/2 사양 홈 페이지</span><span class="sxs-lookup"><span data-stu-id="a8e5b-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="a8e5b-138">공식 HTTP/2 FAQ</span><span class="sxs-lookup"><span data-stu-id="a8e5b-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="a8e5b-139">Akamai HTTP/2 정보</span><span class="sxs-lookup"><span data-stu-id="a8e5b-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="a8e5b-140">Azure CDN의 제공되는 기능에 대한 자세한 내용은 [Azure CDN 개요](https://azure.microsoft.com/documentation/articles/cdn-overview/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8e5b-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>