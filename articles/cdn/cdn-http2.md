---
title: "Azure CDN에서 aaaHTTP/2 지원은 | Microsoft Docs"
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="d72db-103">Azure CDN에서 HTTP/2 지원</span><span class="sxs-lookup"><span data-stu-id="d72db-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d72db-104">HTTP/2는 주 버전 tooHTTP/1.1\입니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="d72db-105">웹 성능, 감소 응답 시간 및 향상 된 사용자 경험을 hello 친숙 한 HTTP 메서드, 상태 코드 및 의미 체계를 유지 하면서 더 빠르게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="d72db-106">HTTP/2는 HTTP와 HTTPS가 디자인 된 toowork, 다양 한 클라이언트 웹 브라우저 tls HTTP/2만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="d72db-107">HTTP/2 이점</span><span class="sxs-lookup"><span data-stu-id="d72db-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="d72db-108">HTTP/2의 hello 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="d72db-109">**멀티플렉싱 및 동시성**</span><span class="sxs-lookup"><span data-stu-id="d72db-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="d72db-110">HTTP 1.1을 사용하여 여러 개의 리소스 요청을 여러 번 수행하려면 여러 개의 TCP 연결이 필요하며 각 연결에는 이와 관련된 성능 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="d72db-111">HTTP/2 여러 리소스 toobe 단일 TCP 연결에서 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="d72db-112">**헤더 압축**</span><span class="sxs-lookup"><span data-stu-id="d72db-112">**Header compression**</span></span>

    <span data-ttu-id="d72db-113">제공 된 리소스에 대 한 hello HTTP 헤더를 압축 하 여 hello 통신 중에 시간이 크게 단축 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="d72db-114">**스트림 종속성**</span><span class="sxs-lookup"><span data-stu-id="d72db-114">**Stream dependencies**</span></span>

    <span data-ttu-id="d72db-115">스트림 종속성 tooindicate toohello 서버 리소스의 우선 순위를 포함 하는 hello 클라이언트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="d72db-116">HTTP/2 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="d72db-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="d72db-117">현재 버전의 HTTP/2 지원은 구현한 모든 주요 브라우저 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="d72db-118">지원 되지 않는 브라우저 tooHTTP/1.1 자동으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="d72db-119">브라우저</span><span class="sxs-lookup"><span data-stu-id="d72db-119">Browser</span></span>|<span data-ttu-id="d72db-120">최소 버전</span><span class="sxs-lookup"><span data-stu-id="d72db-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="d72db-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d72db-121">Microsoft Edge</span></span>| <span data-ttu-id="d72db-122">12</span><span class="sxs-lookup"><span data-stu-id="d72db-122">12</span></span>|
|<span data-ttu-id="d72db-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d72db-123">Google Chrome</span></span>| <span data-ttu-id="d72db-124">43</span><span class="sxs-lookup"><span data-stu-id="d72db-124">43</span></span>|
|<span data-ttu-id="d72db-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d72db-125">Mozilla Firefox</span></span>| <span data-ttu-id="d72db-126">38</span><span class="sxs-lookup"><span data-stu-id="d72db-126">38</span></span>|
|<span data-ttu-id="d72db-127">Opera</span><span class="sxs-lookup"><span data-stu-id="d72db-127">Opera</span></span>| <span data-ttu-id="d72db-128">32</span><span class="sxs-lookup"><span data-stu-id="d72db-128">32</span></span>|
|<span data-ttu-id="d72db-129">Safari</span><span class="sxs-lookup"><span data-stu-id="d72db-129">Safari</span></span>| <span data-ttu-id="d72db-130">9</span><span class="sxs-lookup"><span data-stu-id="d72db-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="d72db-131">Azure CDN에서 HTTP/2 지원 활성화</span><span class="sxs-lookup"><span data-stu-id="d72db-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d72db-132">현재 **Akamai의 Azure CDN** 및 **Verizon의 Azure CDN** 프로필에 대해 HTTP/2 지원이 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="d72db-133">고객의 별도의 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="d72db-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d72db-134">Next Steps</span></span>

<span data-ttu-id="d72db-135">작업에서 HTTP/2의 toosee hello 이점 참조 [Akamai에서이 데모](https://http2.akamai.com/demo)합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="d72db-136">HTTP/2, 리소스 다음 방문 hello에 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="d72db-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="d72db-137">HTTP/2 사양 홈 페이지</span><span class="sxs-lookup"><span data-stu-id="d72db-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="d72db-138">공식 HTTP/2 FAQ</span><span class="sxs-lookup"><span data-stu-id="d72db-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="d72db-139">Akamai HTTP/2 정보</span><span class="sxs-lookup"><span data-stu-id="d72db-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="d72db-140">Azure CDN 사용 가능한 기능에 대해 자세히 toolearn 참조 hello [Azure CDN 개요](https://azure.microsoft.com/documentation/articles/cdn-overview/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d72db-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
