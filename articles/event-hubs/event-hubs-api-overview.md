---
title: "Azure Event Hubs API 개요 | Microsoft Docs"
description: "사용할 수 있는 Azure Event Hubs API의 개요"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="a7c48-103">사용할 수 있는 Event Hubs API</span><span class="sxs-lookup"><span data-stu-id="a7c48-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="a7c48-104">런타임 API</span><span class="sxs-lookup"><span data-stu-id="a7c48-104">Runtime APIs</span></span>

<span data-ttu-id="a7c48-105">다음은 현재 사용 가능한 모든 Azure Event Hubs 런타임 클라이언트에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="a7c48-106">이러한 라이브러리 중 일부에는 제한된 관리 기능이 포함되어 있지만 관리 작업에만 사용되는 [특정 라이브러리](#management-apis)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="a7c48-107">이러한 라이브러리의 핵심적인 부분은 이벤트 허브에서 메시지를 주고 받는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="a7c48-108">각 런타임 라이브러리의 현재 상태에 대한 자세한 내용은 [추가 정보](#additional-information)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c48-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="a7c48-109">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="a7c48-109">Language/Platform</span></span> | <span data-ttu-id="a7c48-110">클라이언트 패키지</span><span class="sxs-lookup"><span data-stu-id="a7c48-110">Client package</span></span> | <span data-ttu-id="a7c48-111">EventProcessorHost 패키지</span><span class="sxs-lookup"><span data-stu-id="a7c48-111">EventProcessorHost package</span></span> | <span data-ttu-id="a7c48-112">리포지토리</span><span class="sxs-lookup"><span data-stu-id="a7c48-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7c48-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="a7c48-113">.NET Standard</span></span> | [<span data-ttu-id="a7c48-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="a7c48-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="a7c48-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="a7c48-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="a7c48-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="a7c48-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="a7c48-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a7c48-117">.NET Framework</span></span> | [<span data-ttu-id="a7c48-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="a7c48-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="a7c48-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="a7c48-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="a7c48-120">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a7c48-120">N/A</span></span> |
| <span data-ttu-id="a7c48-121">Java</span><span class="sxs-lookup"><span data-stu-id="a7c48-121">Java</span></span> | [<span data-ttu-id="a7c48-122">Maven</span><span class="sxs-lookup"><span data-stu-id="a7c48-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="a7c48-123">Maven</span><span class="sxs-lookup"><span data-stu-id="a7c48-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="a7c48-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="a7c48-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="a7c48-125">노드</span><span class="sxs-lookup"><span data-stu-id="a7c48-125">Node</span></span> | [<span data-ttu-id="a7c48-126">NPM</span><span class="sxs-lookup"><span data-stu-id="a7c48-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="a7c48-127">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a7c48-127">N/A</span></span> | [<span data-ttu-id="a7c48-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="a7c48-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="a7c48-129">C</span><span class="sxs-lookup"><span data-stu-id="a7c48-129">C</span></span> | <span data-ttu-id="a7c48-130">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a7c48-130">N/A</span></span> | <span data-ttu-id="a7c48-131">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a7c48-131">N/A</span></span> | [<span data-ttu-id="a7c48-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="a7c48-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="a7c48-133">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a7c48-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="a7c48-134">.NET</span><span class="sxs-lookup"><span data-stu-id="a7c48-134">.NET</span></span>
<span data-ttu-id="a7c48-135">.NET 에코 시스템에는 여러 개의 런타임이 있으므로 Event Hubs용 .NET 라이브러리도 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="a7c48-136">.NET Framework 라이브러리는 .NET Framework 환경에서만 실행될 수 있지만 .NET Standard 라이브러리는 .NET Core 또는 .NET Framework를 사용하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="a7c48-137">.NET Framework에 대한 자세한 내용은 [프레임워크 버전](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c48-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="a7c48-138">노드</span><span class="sxs-lookup"><span data-stu-id="a7c48-138">Node</span></span>

<span data-ttu-id="a7c48-139">Node.js 라이브러리는 현재 미리 보기로 제공되며 Microsoft 직원 및 외부 참가자가 추가적인 프로젝트로 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="a7c48-140">소스 코드를 포함하는 모든 참가 프로그램은 언제든지 환영이며 검토해드립니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="a7c48-141">관리 API</span><span class="sxs-lookup"><span data-stu-id="a7c48-141">Management APIs</span></span>

<span data-ttu-id="a7c48-142">다음은 현재 사용 가능한 관리용 라이브러리의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="a7c48-143">이러한 라이브러리 중 런타임 작업을 포함하는 것은 없으며 Event Hubs 엔터티를 관리하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7c48-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="a7c48-144">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="a7c48-144">Language/Platform</span></span> | <span data-ttu-id="a7c48-145">관리 패키지</span><span class="sxs-lookup"><span data-stu-id="a7c48-145">Management package</span></span> | <span data-ttu-id="a7c48-146">리포지토리</span><span class="sxs-lookup"><span data-stu-id="a7c48-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7c48-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="a7c48-147">.NET Standard</span></span> | [<span data-ttu-id="a7c48-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="a7c48-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="a7c48-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="a7c48-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="a7c48-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a7c48-150">Next steps</span></span>
<span data-ttu-id="a7c48-151">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7c48-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a7c48-152">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="a7c48-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a7c48-153">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="a7c48-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a7c48-154">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="a7c48-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)