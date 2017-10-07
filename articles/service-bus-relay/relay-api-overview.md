---
title: "aaaAzure 릴레이 API 개요 | Microsoft Docs"
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
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="9eb34-103">사용 가능한 Relay API</span><span class="sxs-lookup"><span data-stu-id="9eb34-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="9eb34-104">런타임 API</span><span class="sxs-lookup"><span data-stu-id="9eb34-104">Runtime APIs</span></span>

<span data-ttu-id="9eb34-105">hello 다음 표에 모든 릴레이 런타임 클라이언트 현재 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb34-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="9eb34-106">hello [추가 정보](#additional-information) 섹션의 각 런타임 라이브러리 hello 상태에 대 한 자세한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9eb34-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="9eb34-107">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="9eb34-107">Language/Platform</span></span> | <span data-ttu-id="9eb34-108">사용 가능한 기능</span><span class="sxs-lookup"><span data-stu-id="9eb34-108">Available feature</span></span> | <span data-ttu-id="9eb34-109">클라이언트 패키지</span><span class="sxs-lookup"><span data-stu-id="9eb34-109">Client package</span></span> | <span data-ttu-id="9eb34-110">리포지토리</span><span class="sxs-lookup"><span data-stu-id="9eb34-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9eb34-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="9eb34-111">.NET Standard</span></span> | <span data-ttu-id="9eb34-112">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="9eb34-112">Hybrid Connections</span></span> | [<span data-ttu-id="9eb34-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="9eb34-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="9eb34-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="9eb34-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="9eb34-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="9eb34-115">.NET Framework</span></span> | <span data-ttu-id="9eb34-116">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="9eb34-116">WCF Relay</span></span> | [<span data-ttu-id="9eb34-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="9eb34-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="9eb34-118">해당 없음</span><span class="sxs-lookup"><span data-stu-id="9eb34-118">N/A</span></span> |
| <span data-ttu-id="9eb34-119">노드</span><span class="sxs-lookup"><span data-stu-id="9eb34-119">Node</span></span> | <span data-ttu-id="9eb34-120">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="9eb34-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="9eb34-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="9eb34-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="9eb34-122">추가 정보</span><span class="sxs-lookup"><span data-stu-id="9eb34-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="9eb34-123">.NET</span><span class="sxs-lookup"><span data-stu-id="9eb34-123">.NET</span></span>
<span data-ttu-id="9eb34-124">hello.NET 생태계 여러 런타임, 이벤트 허브에 대 한 여러.NET 라이브러리 되므로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eb34-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="9eb34-125">hello.NET 표준 라이브러리는 hello.NET Framework 라이브러리는.NET Framework 환경 에서만 실행할 수 있습니다 하는 동안.NET Core 또는.NET Framework hello를 사용 하 여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eb34-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="9eb34-126">.NET Framework에 대한 자세한 내용은 [프레임워크 버전](/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eb34-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eb34-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9eb34-127">Next steps</span></span>
<span data-ttu-id="9eb34-128">다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="9eb34-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="9eb34-129">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="9eb34-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="9eb34-130">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="9eb34-130">Relay FAQ</span></span>](relay-faq.md)