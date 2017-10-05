---
title: "Azure CDN을 사용하여 HTTPS를 통한 사용자 지정 도메인으로 Blob 액세스"
description: "Azure CDN을 Blob Storage와 통합하여 HTTPS를 통한 사용자 지정 도메인으로 Blob에 액세스하는 하는 방법에 알아봅니다."
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: 1439198250346ae9484eae448489e8a5de4734b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cdn-to-access-blobs-with-custom-domains-over-https"></a><span data-ttu-id="3c8ad-103">Azure CDN을 사용하여 HTTPS를 통한 사용자 지정 도메인으로 Blob 액세스</span><span class="sxs-lookup"><span data-stu-id="3c8ad-103">Using the Azure CDN to access blobs with custom domains over HTTPS</span></span>

<span data-ttu-id="3c8ad-104">이제 Azure CDN(콘텐츠 배달 네트워크)은 사용자 지정 도메인 이름에 대한 HTTPS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-104">Azure Content Delivery Network (CDN) now supports HTTPS for custom domain names.</span></span>
<span data-ttu-id="3c8ad-105">이 기능을 활용하여 HTTPS를 통한 사용자 지정 도메인을 사용하여 저장소 Blob에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-105">You can leverage this feature to access storage blobs using your custom domain over HTTPS.</span></span> <span data-ttu-id="3c8ad-106">이렇게 하려면 먼저 Blob 끝점에서 Azure CDN을 사용하도록 설정하고 CDN을 사용자 지정 도메인 이름으로 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-106">To do so, you’ll first need to enable Azure CDN on your blob endpoint and map the CDN to a custom domain name.</span></span> <span data-ttu-id="3c8ad-107">이러한 단계를 수행하면 사용자 지정 도메인에 대해 HTTPS를 사용하도록 설정하는 것은 한 번 클릭, 완전한 인증서 관리를 통해 간소화되며 이 모든 것을 일반 CDN 가격 책정에 비용을 추가할 필요 없이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-107">Once you take these steps, enabling HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost to normal CDN pricing.</span></span>

<span data-ttu-id="3c8ad-108">이는 전송 중일 때 개인 정보 및 민감한 웹 응용 프로그램 데이터의 데이터 무결성을 보호하므로 중요한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-108">This ability is important because it enables you to protect the privacy and data integrity of your sensitive web application data while in transit.</span></span> <span data-ttu-id="3c8ad-109">SSL 프로토콜을 사용하여 HTTPS를 통해 트래픽을 제공하면 인터넷 간에 전송되는 데이터를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-109">Using the SSL protocol to serve traffic via HTTPS ensures that data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="3c8ad-110">HTTPS는 신뢰할 수 있는 인증을 제공하며 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-110">HTTPS provides trust and authentication, and protects your web applications from attacks.</span></span>

> [!NOTE]
> <span data-ttu-id="3c8ad-111">사용자 지정 도메인 이름에 대한 SSL 지원뿐 아니라 Azure CDN은 전 세계 고대역폭 콘텐츠를 제공하는 응용 프로그램의 규모를 확장하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-111">In addition to providing SSL support for custom domain names, the Azure CDN can help you scale your application to deliver high-bandwidth content around the world.</span></span>
> <span data-ttu-id="3c8ad-112">자세한 내용은 [Azure CDN 개요](../cdn/cdn-overview.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-112">To learn more, check out [Overview of the Azure CDN](../cdn/cdn-overview.md).</span></span>
>
>

## <a name="quick-start"></a><span data-ttu-id="3c8ad-113">빠른 시작</span><span class="sxs-lookup"><span data-stu-id="3c8ad-113">Quick start</span></span>

<span data-ttu-id="3c8ad-114">다음은 사용자 지정 Blob Storage 끝점에 대한 HTTPS를 사용하도록 설정하는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-114">These are the steps required to enable HTTPS for your custom blob storage endpoint:</span></span>

1.  <span data-ttu-id="3c8ad-115">[Azure Storage 계정과 Azure CDN을 통합합니다](../cdn/cdn-create-a-storage-account-with-cdn.md).</span><span class="sxs-lookup"><span data-stu-id="3c8ad-115">[Integrate an Azure storage account with Azure CDN](../cdn/cdn-create-a-storage-account-with-cdn.md).</span></span>
    <span data-ttu-id="3c8ad-116">이 문서에서는 아직 수행하지 않은 경우 Azure Portal에서 저장소 계정을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-116">This article walks you through creating a storage account in the Azure Portal if you have not done so already.</span></span>
2.  <span data-ttu-id="3c8ad-117">[Azure CDN 콘텐츠를 사용자 지정 도메인에 매핑합니다](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3c8ad-117">[Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>
3.  <span data-ttu-id="3c8ad-118">[Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정합니다](../cdn/cdn-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="3c8ad-118">[Enable HTTPS on an Azure CDN custom domain](../cdn/cdn-custom-ssl.md).</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="3c8ad-119">공유 액세스 서명</span><span class="sxs-lookup"><span data-stu-id="3c8ad-119">Shared Access Signatures</span></span>

<span data-ttu-id="3c8ad-120">익명 읽기 액세스를 허용하지 않도록 Blob Storage 끝점을 구성한 경우 [SAS(공유 액세스 서명)](storage-dotnet-shared-access-signature-part-1.md) 토큰을 사용자 지정 도메인에 사용자가 만든 각 요청에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-120">If your blob storage endpoint is configured to disallow anonymous read access, you will need to provide a [Shared Access Signature (SAS)](storage-dotnet-shared-access-signature-part-1.md) token in each request you make to your custom domain.</span></span> <span data-ttu-id="3c8ad-121">기본적으로 Blob Storage 끝점은 익명 읽기 액세스를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-121">By default, blob storage endpoints disallow anonymous read access.</span></span> <span data-ttu-id="3c8ad-122">공유 액세스 서명에 관한 자세한 내용은 [컨테이너 및 Blob에 대한 익명 읽기 권한 관리](storage-manage-access-to-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-122">See [Managing anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information on shared access signatures.</span></span>

<span data-ttu-id="3c8ad-123">Azure CDN은 SAS 토큰에 추가된 제한 사항을 준수하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-123">Azure CDN does not respect any restrictions added to the SAS token.</span></span> <span data-ttu-id="3c8ad-124">예를 들어 모든 SAS 토큰은 만료 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-124">For example, all SAS tokens have an expiration time.</span></span> <span data-ttu-id="3c8ad-125">즉, 콘텐츠가 CDN 에지 노드에서 제거될 때까지는 만료된 SAS로 콘텐츠에 여전히 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-125">This means that content can still be accessed with an expired SAS until that content is purged from the CDN edge nodes.</span></span> <span data-ttu-id="3c8ad-126">캐시 응답 헤더를 설정하여 데이터를 CDN에 얼마나 오래 캐시할 것인지 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-126">You can control how long data is cached on the CDN by setting the cache response header.</span></span> <span data-ttu-id="3c8ad-127">지침에 관해서는 [Azure CDN에서 Azure Storage Blob 만료 관리](../cdn/cdn-manage-expiration-of-blob-content.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-127">See [Managing expiration of Azure Storage blobs in Azure CDN](../cdn/cdn-manage-expiration-of-blob-content.md) for instructions.</span></span>

<span data-ttu-id="3c8ad-128">동일한 Blob 끝점에 대한 여러 개의 SAS URL을 만드는 경우 Azure CDN에 대해 쿼리 문자열 캐싱을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-128">If you create multiple SAS URLs for the same blob endpoint, we recommend turning on query string caching for your Azure CDN.</span></span> <span data-ttu-id="3c8ad-129">이는 각 URL이 고유한 엔터티로 처리되었는지 확인하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-129">This is to ensure that each URL is treated as a unique entity.</span></span> <span data-ttu-id="3c8ad-130">자세한 내용은 [쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어](../cdn/cdn-query-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-130">See [Controlling Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md) for more information.</span></span>

## <a name="http-to-https-redirection"></a><span data-ttu-id="3c8ad-131">HTTP에서 HTTPS로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3c8ad-131">HTTP to HTTPS redirection</span></span>

<span data-ttu-id="3c8ad-132">HTTP 트래픽을 HTTPS로 리디렉션하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-132">You can elect to redirect HTTP traffic to HTTPS.</span></span> <span data-ttu-id="3c8ad-133">그러려면 Verizon에서 제공하는 Azure CDN 프리미엄을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-133">This requires use of the Azure CDN premium offering from Verizon.</span></span> <span data-ttu-id="3c8ad-134">다음 규칙을 사용하여 [Azure CDN 규칙 엔진을 사용하여 HTTP 동작을 재정의](../cdn/cdn-rules-engine.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-134">You need to [Override HTTP behavior using the Azure CDN rules engine](../cdn/cdn-rules-engine.md) with the following rule:</span></span>

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

<span data-ttu-id="3c8ad-135">“Cdn-endpoint-name”은 CDN 끝점에 대해 구성한 이름을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-135">“Cdn-endpoint-name” refers to the name that you configured for your CDN endpoint.</span></span> <span data-ttu-id="3c8ad-136">드롭다운에서 이 값을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-136">You can select this value from the dropdown.</span></span> <span data-ttu-id="3c8ad-137">“Origin-path”는 정적 콘텐츠가 있는 원본 저장소 계정 내 경로를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-137">“Origin-path” refers to the path within your origin storage account where your static content resides.</span></span>
<span data-ttu-id="3c8ad-138">단일 컨테이너의 모든 정적 콘텐츠를 호스팅하는 경우 “origin-path”를 해당 컨테이너의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-138">If you are hosting all static content in a single container, replace “origin-path” with the name of that container.</span></span>

<span data-ttu-id="3c8ad-139">규칙에 자세히 알아보려면 [Azure CDN 규칙 엔진 기능](../cdn/cdn-rules-engine-reference-features.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-139">For a deeper dive into rules, please see the [Azure CDN rules engine features](../cdn/cdn-rules-engine-reference-features.md).</span></span>

## <a name="pricing-and-billing"></a><span data-ttu-id="3c8ad-140">가격 책정 및 대금 청구</span><span class="sxs-lookup"><span data-stu-id="3c8ad-140">Pricing and billing</span></span>

<span data-ttu-id="3c8ad-141">Azure CDN을 통해 Blob에 액세스할 때 에지 노드와 원본(Blob Storage) 사이의 트래픽에 대해 [Blob Storage 가격](https://azure.microsoft.com/pricing/details/storage/blobs/)을, 에지 노드에서 액세스하는 데이터에 대해 [CDN 가격](https://azure.microsoft.com/pricing/details/cdn/)을 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-141">When you access blobs through an Azure CDN, you pay [Blob storage prices](https://azure.microsoft.com/pricing/details/storage/blobs/) for traffic between the edge nodes and the origin (Blob storage), and [CDN prices](https://azure.microsoft.com/pricing/details/cdn/) for data accessed from the edge nodes.</span></span>

<span data-ttu-id="3c8ad-142">예를 들어, Azure CDN을 사용하여 액세스되는 저장소 계정이 미국 서부에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-142">For example, say you have a storage account in West US that is being accessed using an Azure CDN.</span></span> <span data-ttu-id="3c8ad-143">영국에서 CDN을 통해 해당 저장소 계정에 있는 Blob 중 하나에 액세스하려고 시도하는 경우 Azure는 먼저 해당 Blob에 대한 영국 가장 가까이에 있는 에지 노드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-143">If someone in the UK tries to access one of the blobs in that storage account via the CDN, Azure first checks the edge node closest to the UK for that blob.</span></span> <span data-ttu-id="3c8ad-144">발견한 경우 Blob의 해당 복사본에 액세스하고, CDN에서 액세스하였으므로 CDN 가격 책정을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-144">If found, it accesses that copy of the blob and will use CDN pricing, because it is being accessed on the CDN.</span></span> <span data-ttu-id="3c8ad-145">찾을 수 없는 경우, Azure는 Blob을 에지 노드에 복사합니다. 이는 Blob Storage 가격 책정에 지정된 대로 송신 및 트랜잭션 비용이 발생됩니다. 그런 다음, CDN 결제로 이어지는 에지 노드의 파일에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-145">If not found, Azure will copy the blob to the edge node, which will result in egress and transaction charges as specified in the Blob storage pricing, and then access the file on the edge node, which will result in CDN billing.</span></span>

<span data-ttu-id="3c8ad-146">[CDN 가격 책정 페이지](https://azure.microsoft.com/pricing/details/cdn/)에서 살펴볼 때 사용자 지정 도메인 이름을 위한 HTTPS 지원은 Verizon 제품(표준 및 프리미엄)의 Azure CDN에만 사용할 수 있다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8ad-146">When looking at the [CDN pricing page](https://azure.microsoft.com/pricing/details/cdn/), note that HTTPS support for custom domain names is only available for Azure CDN from Verizon products (Standard and Premium).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c8ad-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c8ad-147">Next steps</span></span>

[<span data-ttu-id="3c8ad-148">Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="3c8ad-148">Configure a custom domain name for your Blob storage endpoint</span></span>](storage-custom-domain-name.md)
