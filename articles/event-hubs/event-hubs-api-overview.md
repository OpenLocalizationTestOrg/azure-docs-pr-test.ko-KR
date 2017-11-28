---
title: "aaaAzure 이벤트 허브 API 개요 | Microsoft Docs"
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
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="372fc-103">사용할 수 있는 Event Hubs API</span><span class="sxs-lookup"><span data-stu-id="372fc-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="372fc-104">런타임 API</span><span class="sxs-lookup"><span data-stu-id="372fc-104">Runtime APIs</span></span>

<span data-ttu-id="372fc-105">hello 다음은 현재 사용할 수 있는 모든 Azure 이벤트 허브 런타임 클라이언트에 대 한 설명을입니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="372fc-106">또한 이러한 라이브러리 중 일부 제한적인된 관리 기능을 포함, 있지만 있습니다 [특정 라이브러리](#management-apis) toomanagement 작업 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="372fc-107">이러한 라이브러리의 코어 포커스 hello toosend 이며 이벤트 허브에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="372fc-108">참조 [추가 정보](#additional-information) hello 각 런타임 라이브러리의 현재 상태에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="372fc-109">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="372fc-109">Language/Platform</span></span> | <span data-ttu-id="372fc-110">클라이언트 패키지</span><span class="sxs-lookup"><span data-stu-id="372fc-110">Client package</span></span> | <span data-ttu-id="372fc-111">EventProcessorHost 패키지</span><span class="sxs-lookup"><span data-stu-id="372fc-111">EventProcessorHost package</span></span> | <span data-ttu-id="372fc-112">리포지토리</span><span class="sxs-lookup"><span data-stu-id="372fc-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="372fc-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="372fc-113">.NET Standard</span></span> | [<span data-ttu-id="372fc-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="372fc-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="372fc-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="372fc-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="372fc-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="372fc-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="372fc-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="372fc-117">.NET Framework</span></span> | [<span data-ttu-id="372fc-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="372fc-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="372fc-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="372fc-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="372fc-120">해당 없음</span><span class="sxs-lookup"><span data-stu-id="372fc-120">N/A</span></span> |
| <span data-ttu-id="372fc-121">Java</span><span class="sxs-lookup"><span data-stu-id="372fc-121">Java</span></span> | [<span data-ttu-id="372fc-122">Maven</span><span class="sxs-lookup"><span data-stu-id="372fc-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="372fc-123">Maven</span><span class="sxs-lookup"><span data-stu-id="372fc-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="372fc-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="372fc-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="372fc-125">노드</span><span class="sxs-lookup"><span data-stu-id="372fc-125">Node</span></span> | [<span data-ttu-id="372fc-126">NPM</span><span class="sxs-lookup"><span data-stu-id="372fc-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="372fc-127">해당 없음</span><span class="sxs-lookup"><span data-stu-id="372fc-127">N/A</span></span> | [<span data-ttu-id="372fc-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="372fc-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="372fc-129">C</span><span class="sxs-lookup"><span data-stu-id="372fc-129">C</span></span> | <span data-ttu-id="372fc-130">해당 없음</span><span class="sxs-lookup"><span data-stu-id="372fc-130">N/A</span></span> | <span data-ttu-id="372fc-131">해당 없음</span><span class="sxs-lookup"><span data-stu-id="372fc-131">N/A</span></span> | [<span data-ttu-id="372fc-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="372fc-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="372fc-133">추가 정보</span><span class="sxs-lookup"><span data-stu-id="372fc-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="372fc-134">.NET</span><span class="sxs-lookup"><span data-stu-id="372fc-134">.NET</span></span>
<span data-ttu-id="372fc-135">hello.NET 생태계 여러 런타임, 이벤트 허브에 대 한 여러.NET 라이브러리 되므로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="372fc-136">hello.NET 표준 라이브러리는 hello.NET Framework 라이브러리는.NET Framework 환경 에서만 실행할 수 있습니다 하는 동안.NET Core 또는.NET Framework hello를 사용 하 여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="372fc-137">.NET Framework에 대한 자세한 내용은 [프레임워크 버전](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="372fc-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="372fc-138">노드</span><span class="sxs-lookup"><span data-stu-id="372fc-138">Node</span></span>

<span data-ttu-id="372fc-139">hello Node.js 라이브러리는 현재 미리 보기로 및 Microsoft 직원과 외부 참가자가 쪽 프로젝트로 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="372fc-140">소스 코드를 포함하는 모든 참가 프로그램은 언제든지 환영이며 검토해드립니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="372fc-141">관리 API</span><span class="sxs-lookup"><span data-stu-id="372fc-141">Management APIs</span></span>

<span data-ttu-id="372fc-142">hello 다음은 모든 사용 가능한 현재 관리 특정 라이브러리의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="372fc-143">이러한 라이브러리 중 런타임 작업을 포함 하 고 hello 목적으로 이벤트 허브 엔터티 관리에 대 한 있으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="372fc-144">언어/플랫폼</span><span class="sxs-lookup"><span data-stu-id="372fc-144">Language/Platform</span></span> | <span data-ttu-id="372fc-145">관리 패키지</span><span class="sxs-lookup"><span data-stu-id="372fc-145">Management package</span></span> | <span data-ttu-id="372fc-146">리포지토리</span><span class="sxs-lookup"><span data-stu-id="372fc-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="372fc-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="372fc-147">.NET Standard</span></span> | [<span data-ttu-id="372fc-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="372fc-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="372fc-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="372fc-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="372fc-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="372fc-150">Next steps</span></span>
<span data-ttu-id="372fc-151">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="372fc-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="372fc-152">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="372fc-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="372fc-153">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="372fc-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="372fc-154">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="372fc-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)