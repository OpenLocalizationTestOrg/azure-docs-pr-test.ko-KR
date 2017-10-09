---
title: "aaaAzure DocumentDB.NET 변경 피드 프로세서 SDK 및 리소스 | Microsoft Docs"
description: "변경 피드 프로세서 API와 SDK 릴리스 날짜, 사용 중지 날짜 및 hello DocumentDB.NET 변경 피드 프로세서 SDK의 각 버전 간의 변경 내용을 포함 하 여 hello에 대 한 모든에 대해 알아봅니다."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="b3678-103">DocumentDB .NET 변경 피드 프로세서 SDK: 다운로드 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b3678-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3678-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b3678-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="b3678-105">.NET 변경 피드</span><span class="sxs-lookup"><span data-stu-id="b3678-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="b3678-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b3678-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="b3678-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b3678-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="b3678-108">Java</span><span class="sxs-lookup"><span data-stu-id="b3678-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="b3678-109">Python</span><span class="sxs-lookup"><span data-stu-id="b3678-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="b3678-110">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b3678-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="b3678-111">REST 리소스 공급자</span><span class="sxs-lookup"><span data-stu-id="b3678-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="b3678-112">SQL</span><span class="sxs-lookup"><span data-stu-id="b3678-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="b3678-113">**SDK 다운로드**</span><span class="sxs-lookup"><span data-stu-id="b3678-113">**SDK download**</span></span></td><td>[<span data-ttu-id="b3678-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="b3678-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="b3678-115">**API 설명서**</span><span class="sxs-lookup"><span data-stu-id="b3678-115">**API documentation**</span></span></td><td>[<span data-ttu-id="b3678-116">피드 프로세서 라이브러리 API 참조 문서 변경</span><span class="sxs-lookup"><span data-stu-id="b3678-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="b3678-117">**시작**</span><span class="sxs-lookup"><span data-stu-id="b3678-117">**Get started**</span></span></td><td>[<span data-ttu-id="b3678-118">DocumentDB 변경 피드 프로세서.NET SDK hello로 시작.</span><span class="sxs-lookup"><span data-stu-id="b3678-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="b3678-119">**현재 지원되는 프레임워크**</span><span class="sxs-lookup"><span data-stu-id="b3678-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="b3678-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b3678-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="b3678-121">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b3678-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="b3678-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3678-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="b3678-123">메서드 tooobtain 변경 피드 hello에서 처리 하는 남은 작업 toobe의 추정치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3678-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="b3678-124">[DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 버전 1.13.2 이상과 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b3678-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="b3678-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="b3678-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="b3678-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="b3678-126">GA SDK</span></span>
* <span data-ttu-id="b3678-127">[DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 버전 1.14.1 이하와 호환 가능</span><span class="sxs-lookup"><span data-stu-id="b3678-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="b3678-128">릴리스 및 사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="b3678-128">Release & Retirement dates</span></span>
<span data-ttu-id="b3678-129">Microsoft는 알림을 적어도 제공 **12 개월** 순서 toosmooth hello 전환 tooa 지원/최신 버전의 SDK를 사용 중지 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3678-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="b3678-130">새로운 기능 및 기능 및 최적화는 toohello 현재만 추가 SDK, 따라서 것이 좋습니다 하면 항상 업그레이드 toohello 최신 SDK 버전 가능한 한 빨리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3678-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="b3678-131">모든 요청 tooCosmos 사용 중지 된 SDK를 사용 하 여 DB hello 서비스에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3678-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="b3678-132">버전</span><span class="sxs-lookup"><span data-stu-id="b3678-132">Version</span></span> | <span data-ttu-id="b3678-133">릴리스 날짜</span><span class="sxs-lookup"><span data-stu-id="b3678-133">Release Date</span></span> | <span data-ttu-id="b3678-134">사용 중지 날짜</span><span class="sxs-lookup"><span data-stu-id="b3678-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b3678-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3678-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="b3678-136">2017년 8월 13일</span><span class="sxs-lookup"><span data-stu-id="b3678-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="b3678-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b3678-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="b3678-138">2017년 7월 7일</span><span class="sxs-lookup"><span data-stu-id="b3678-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="b3678-139">FAQ</span><span class="sxs-lookup"><span data-stu-id="b3678-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="b3678-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b3678-140">See also</span></span>
<span data-ttu-id="b3678-141">Cosmos DB에 대해 자세히 toolearn 참조 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 서비스 페이지.</span><span class="sxs-lookup"><span data-stu-id="b3678-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

