---
title: "Azure Relay API 개요 | Microsoft Docs"
description: "사용 가능한 Azure Relay API 개요"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="80f3e-103">사용 가능한 Relay API</span><span class="sxs-lookup"><span data-stu-id="80f3e-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="80f3e-104">런타임 API</span><span class="sxs-lookup"><span data-stu-id="80f3e-104">Runtime APIs</span></span>

<span data-ttu-id="80f3e-105">다음 표에는 현재 사용 가능한 모든 Relay 런타임 클라이언트가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3e-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="80f3e-106">[추가 정보](#additional-information) 섹션에는 각 런타임 라이브러리의 상태에 대한 자세한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3e-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="80f3e-107">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="80f3e-107">Language/Platform</span></span> | <span data-ttu-id="80f3e-108">사용 가능한 기능</span><span class="sxs-lookup"><span data-stu-id="80f3e-108">Available feature</span></span> | <span data-ttu-id="80f3e-109">클라이언트 패키지</span><span class="sxs-lookup"><span data-stu-id="80f3e-109">Client package</span></span> | <span data-ttu-id="80f3e-110">리포지토리</span><span class="sxs-lookup"><span data-stu-id="80f3e-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="80f3e-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="80f3e-111">.NET Standard</span></span> | <span data-ttu-id="80f3e-112">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="80f3e-112">Hybrid Connections</span></span> | [<span data-ttu-id="80f3e-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="80f3e-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="80f3e-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="80f3e-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="80f3e-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="80f3e-115">.NET Framework</span></span> | <span data-ttu-id="80f3e-116">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="80f3e-116">WCF Relay</span></span> | [<span data-ttu-id="80f3e-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="80f3e-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="80f3e-118">해당 없음</span><span class="sxs-lookup"><span data-stu-id="80f3e-118">N/A</span></span> |
| <span data-ttu-id="80f3e-119">노드</span><span class="sxs-lookup"><span data-stu-id="80f3e-119">Node</span></span> | <span data-ttu-id="80f3e-120">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="80f3e-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="80f3e-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="80f3e-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="80f3e-122">추가 정보</span><span class="sxs-lookup"><span data-stu-id="80f3e-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="80f3e-123">.NET</span><span class="sxs-lookup"><span data-stu-id="80f3e-123">.NET</span></span>
<span data-ttu-id="80f3e-124">.NET 에코 시스템에는 여러 개의 런타임이 있으므로 Event Hubs용 .NET 라이브러리도 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3e-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="80f3e-125">.NET Framework 라이브러리는 .NET Framework 환경에서만 실행될 수 있지만 .NET Standard 라이브러리는 .NET Core 또는 .NET Framework를 사용하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f3e-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="80f3e-126">.NET Framework에 대한 자세한 내용은 [프레임워크 버전](/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="80f3e-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80f3e-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80f3e-127">Next steps</span></span>
<span data-ttu-id="80f3e-128">Azure Relay에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="80f3e-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="80f3e-129">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="80f3e-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="80f3e-130">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="80f3e-130">Relay FAQ</span></span>](relay-faq.md)