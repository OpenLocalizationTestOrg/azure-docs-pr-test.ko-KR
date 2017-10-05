---
title: "Azure Media Services 개요 | Microsoft Docs"
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
ms.openlocfilehash: 2a175aed40b9775d9a4de6877eb3467b43819568
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="04116-103">Azure Media Services 개요</span><span class="sxs-lookup"><span data-stu-id="04116-103">Azure Media Services overview</span></span> 

<span data-ttu-id="04116-104">Microsoft Azure Media Services는 개발자가 확장 가능한 미디어 관리 및 배달 응용 프로그램을 빌드할 수 있는 확장 가능한 클라우드 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="04116-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="04116-105">Media Services는 다양한 클라이언트(예: TV, PC 및 모바일 장치)로의 주문형 및 라이브 스트리밍 배달을 위해 비디오 또는 오디오 콘텐츠를 안전하게 업로드, 저장, 인코딩 및 패키지할 수 있는 REST API를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-105">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="04116-106">전체 Media Services를 사용하여 종단 간 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="04116-107">또한 워크플로의 일부에 타사 구성 요소를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-107">You can also choose to use third-party components for some parts of your workflow.</span></span> <span data-ttu-id="04116-108">예를 들어 타사 인코더를 사용하여 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="04116-109">그런 다음 Media Services를 사용하여 업로드, 보호, 패키징 및 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="04116-110">콘텐츠를 라이브로 스트리밍하고 주문형 콘텐츠를 배달하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-110">You can choose to stream your content live or deliver content on-demand.</span></span> <span data-ttu-id="04116-111">이 항목은 관련 항목으로도 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="04116-111">The topic also links to other relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="04116-112">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="04116-112">Media Services learning paths</span></span>
<span data-ttu-id="04116-113">여기서 AMS 학습 경로를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="04116-114">AMS 라이브 스트리밍 워크플로</span><span class="sxs-lookup"><span data-stu-id="04116-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="04116-115">AMS 주문형 스트리밍 워크플로</span><span class="sxs-lookup"><span data-stu-id="04116-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="04116-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04116-116">Prerequisites</span></span>

<span data-ttu-id="04116-117">Azure Media Services 사용을 시작하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-117">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="04116-118">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="04116-118">An Azure account.</span></span> <span data-ttu-id="04116-119">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="04116-120">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="04116-121">Azure Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="04116-121">An Azure Media Services account.</span></span> <span data-ttu-id="04116-122">자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="04116-123">(선택 사항) 개발 환경 설정.</span><span class="sxs-lookup"><span data-stu-id="04116-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="04116-124">개발 환경에 .NET 또는 REST API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="04116-125">자세한 내용은 [환경 설정](media-services-dotnet-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="04116-126">[프로그래밍 방식으로 AMS API에 연결](media-services-use-aad-auth-to-access-ams-api.md)하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="04116-126">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="04116-127">시작된 상태에 있는 표준 또는 프리미엄 스트리밍 끝점.</span><span class="sxs-lookup"><span data-stu-id="04116-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="04116-128">자세한 내용은 [스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="04116-129">SDK 및 도구</span><span class="sxs-lookup"><span data-stu-id="04116-129">SDKs and tools</span></span>

<span data-ttu-id="04116-130">Media Services 솔루션을 빌드하려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04116-130">To build Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="04116-131">Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="04116-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="04116-132">사용 가능한 클라이언트 SDK 중 하나:</span><span class="sxs-lookup"><span data-stu-id="04116-132">One of the available client SDKs:</span></span>
    * <span data-ttu-id="04116-133">[.NET용 Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="04116-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="04116-134">[Java용 Azure SDK](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="04116-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="04116-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="04116-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="04116-136">[Node.js용 Azure Media Services](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Node.js SDK의 Microsoft가 아닌 타사 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="04116-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="04116-137">커뮤니티에서 유지 관리하고 현재 AMS API를 100% 포함하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="04116-137">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span></span>
* <span data-ttu-id="04116-138">기존 도구:</span><span class="sxs-lookup"><span data-stu-id="04116-138">Existing tools:</span></span>
    * [<span data-ttu-id="04116-139">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="04116-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="04116-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE(Azure Media Services 탐색기)는 Windows용 Winforms/C# 응용 프로그램임)</span><span class="sxs-lookup"><span data-stu-id="04116-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="04116-141">개념 및 개요</span><span class="sxs-lookup"><span data-stu-id="04116-141">Concepts and overview</span></span>
<span data-ttu-id="04116-142">Azure Media Services 개념은 [개념](media-services-concepts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="04116-143">Azure Media Services의 모든 주요 구성 요소를 소개하는 사용 방법 시리즈는 [Azure Media Services 단계별 자습서](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-143">For a how-to series that introduces you to all the main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="04116-144">이 시리즈에는 개념에 대한 훌륭한 개요가 포함되어 있으며 AMSE 도구를 사용하여 AMS 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04116-144">This series has a great overview of concepts and it uses the AMSE tool to demonstrate AMS tasks.</span></span> <span data-ttu-id="04116-145">AMSE 도구는 Windows 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="04116-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="04116-146">이 도구는 [.NET용 AMS SDK](https://github.com/Azure/azure-sdk-for-media-services), [Java용 Azure SDK](https://github.com/Azure/azure-sdk-for-java) 또는 [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)를 사용하여 프로그래밍 방식으로 수행할 수 있는 대부분의 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-146">This tool supports most of the tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="04116-147">지원되는 시나리오 및 데이터 센터에서 Media Services의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="04116-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="04116-148">자세한 내용은 [AMS 시나리오 및 데이터 센터에서 기능 및 서비스의 사용 가용성](scenarios-and-availability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="04116-149">SLA(서비스 수준 계약)</span><span class="sxs-lookup"><span data-stu-id="04116-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="04116-150">Media Services Encoding을 위해 REST API 트랜잭션의 99.9% 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="04116-151">표준 또는 프리미엄 스트리밍 끝점을 구매하는 경우 스트리밍을 위해 기존 미디어 콘텐츠에 대해 99.9% 가용성을 보장하는 요청을 서비스합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="04116-152">라이브 채널을 위해 실행 중인 채널이 최소 99.9%의 시간 동안 외부 연결을 사용할 수 있도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="04116-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span></span>
* <span data-ttu-id="04116-153">Content Protection을 위해 최소 99.9%의 시간 동안 주요 요청을 처리할 것을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span></span>
* <span data-ttu-id="04116-154">인덱서를 위해 99.9%의 시간 동안 Encoding 예약 단위로 처리되는 인덱서 작업 요청을 서비스합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span></span>

<span data-ttu-id="04116-155">자세한 내용은 [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="04116-156">데이터 센터에서 가용성에 대한 정보는 [사용 가능성](scenarios-and-availability.md#availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04116-156">For information about availability in datacenters, see the [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="04116-157">지원</span><span class="sxs-lookup"><span data-stu-id="04116-157">Support</span></span>

<span data-ttu-id="04116-158">[Azure 지원](https://azure.microsoft.com/support/options/) 에서는 Media Services를 포함하여 Azure에 대한 지원 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04116-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="04116-159">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="04116-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
