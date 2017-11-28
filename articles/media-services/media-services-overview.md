---
title: "aaaAzure 미디어 서비스 개요 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="4fcd8-103">Azure Media Services 개요</span><span class="sxs-lookup"><span data-stu-id="4fcd8-103">Azure Media Services overview</span></span> 

<span data-ttu-id="4fcd8-104">Microsoft Azure 미디어 서비스는 개발자 toobuild 확장 가능한 미디어 관리 및 제공 응용 프로그램 수 있도록 하는 확장 가능한 클라우드 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="4fcd8-105">Toosecurely 업로드를 허용 하는 REST Api를 기반으로 하는 미디어 서비스, 저장, 인코딩 및 주문형 및 라이브 스트리밍 배달 toovarious 클라이언트 모두 (예를 들어, TV, PC 및 모바일 장치)에 대 한 비디오 또는 오디오 콘텐츠를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="4fcd8-106">전체 Media Services를 사용하여 종단 간 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="4fcd8-107">작업을 워크플로의 일부분에 대해 타사 구성 요소 toouse로 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="4fcd8-108">예를 들어 타사 인코더를 사용하여 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="4fcd8-109">그런 다음 Media Services를 사용하여 업로드, 보호, 패키징 및 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="4fcd8-110">주문형으로 콘텐츠를 배달 하거나 toostream 라이브 콘텐츠를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="4fcd8-111">또한 hello 항목 tooother 관련 항목을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4fcd8-112">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="4fcd8-112">Media Services learning paths</span></span>
<span data-ttu-id="4fcd8-113">여기서 AMS 학습 경로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="4fcd8-114">AMS 라이브 스트리밍 워크플로</span><span class="sxs-lookup"><span data-stu-id="4fcd8-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="4fcd8-115">AMS 주문형 스트리밍 워크플로</span><span class="sxs-lookup"><span data-stu-id="4fcd8-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="4fcd8-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4fcd8-116">Prerequisites</span></span>

<span data-ttu-id="4fcd8-117">Azure 미디어 서비스를 사용 하 여 toostart hello 다음 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="4fcd8-118">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-118">An Azure account.</span></span> <span data-ttu-id="4fcd8-119">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4fcd8-120">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="4fcd8-121">Azure Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-121">An Azure Media Services account.</span></span> <span data-ttu-id="4fcd8-122">자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="4fcd8-123">(선택 사항) 개발 환경 설정.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="4fcd8-124">개발 환경에 .NET 또는 REST API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="4fcd8-125">자세한 내용은 [환경 설정](media-services-dotnet-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="4fcd8-126">또한, 너무 방법을 학습[tooAMS API를 프로그래밍 방식으로 연결](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="4fcd8-127">시작된 상태에 있는 표준 또는 프리미엄 스트리밍 끝점.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="4fcd8-128">자세한 내용은 [스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="4fcd8-129">SDK 및 도구</span><span class="sxs-lookup"><span data-stu-id="4fcd8-129">SDKs and tools</span></span>

<span data-ttu-id="4fcd8-130">toobuild 미디어 서비스 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="4fcd8-131">Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="4fcd8-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="4fcd8-132">Hello 사용 가능한 클라이언트 Sdk 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="4fcd8-133">[.NET용 Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="4fcd8-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="4fcd8-134">[Java용 Azure SDK](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="4fcd8-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="4fcd8-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="4fcd8-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="4fcd8-136">[Node.js용 Azure Media Services](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Node.js SDK의 Microsoft가 아닌 타사 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="4fcd8-137">커뮤니티에서 유지 관리 되 고 현재 없는 hello AMS Api의 100% 검사).</span><span class="sxs-lookup"><span data-stu-id="4fcd8-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="4fcd8-138">기존 도구:</span><span class="sxs-lookup"><span data-stu-id="4fcd8-138">Existing tools:</span></span>
    * [<span data-ttu-id="4fcd8-139">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4fcd8-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="4fcd8-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE(Azure Media Services 탐색기)는 Windows용 Winforms/C# 응용 프로그램임)</span><span class="sxs-lookup"><span data-stu-id="4fcd8-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="4fcd8-141">개념 및 개요</span><span class="sxs-lookup"><span data-stu-id="4fcd8-141">Concepts and overview</span></span>
<span data-ttu-id="4fcd8-142">Azure Media Services 개념은 [개념](media-services-concepts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="4fcd8-143">방법-tooseries tooall hello의 주요 구성 요소 Azure 미디어 서비스를 소개 하는, 참조 [Azure 미디어 서비스 단계별 자습서](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="4fcd8-144">이 시리즈 개념에 대 한 훌륭한 개괄적 개이고 hello AMSE 도구 toodemonstrate AMS 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="4fcd8-145">AMSE 도구는 Windows 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="4fcd8-146">이 도구는 대부분의 hello 작업을 프로그래밍 방식으로 작업을 수행할 수 지원 [AMS SDK for.NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), 또는 [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="4fcd8-147">지원되는 시나리오 및 데이터 센터에서 Media Services의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="4fcd8-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="4fcd8-148">자세한 내용은 [AMS 시나리오 및 데이터 센터에서 기능 및 서비스의 사용 가용성](scenarios-and-availability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="4fcd8-149">SLA(서비스 수준 계약)</span><span class="sxs-lookup"><span data-stu-id="4fcd8-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="4fcd8-150">Media Services Encoding을 위해 REST API 트랜잭션의 99.9% 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="4fcd8-151">표준 또는 프리미엄 스트리밍 끝점을 구매하는 경우 스트리밍을 위해 기존 미디어 콘텐츠에 대해 99.9% 가용성을 보장하는 요청을 서비스합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="4fcd8-152">라이브 채널에 대 한 채널을 실행 해야는 외부 연결 hello 시간의 99.9% 이상의 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="4fcd8-153">콘텐츠 보호는 우리는 성공적으로 요청을 처리 해야 키 이상 hello 시간의 99.9% 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="4fcd8-154">에 대 한 인덱서에서는 요청을 처리 인덱서 작업 인코딩 예약을 사용 하 여 처리 hello 시간 단위 99.9%입니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="4fcd8-155">자세한 내용은 [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="4fcd8-156">데이터 센터의 가용성에 대 한 정보를 참조 hello [Avaiability](scenarios-and-availability.md#availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="4fcd8-157">지원</span><span class="sxs-lookup"><span data-stu-id="4fcd8-157">Support</span></span>

<span data-ttu-id="4fcd8-158">[Azure 지원](https://azure.microsoft.com/support/options/) 에서는 Media Services를 포함하여 Azure에 대한 지원 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fcd8-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="4fcd8-159">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="4fcd8-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
