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
# <a name="available-event-hubs-apis"></a>사용할 수 있는 Event Hubs API

## <a name="runtime-apis"></a>런타임 API

hello 다음은 현재 사용할 수 있는 모든 Azure 이벤트 허브 런타임 클라이언트에 대 한 설명을입니다. 또한 이러한 라이브러리 중 일부 제한적인된 관리 기능을 포함, 있지만 있습니다 [특정 라이브러리](#management-apis) toomanagement 작업 전용입니다. 이러한 라이브러리의 코어 포커스 hello toosend 이며 이벤트 허브에서 메시지를 수신 합니다.

참조 [추가 정보](#additional-information) hello 각 런타임 라이브러리의 현재 상태에 대 한 자세한 내용은 합니다.

| 언어/플랫폼 | 클라이언트 패키지 | EventProcessorHost 패키지 | 리포지토리 |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | 해당 없음 |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| 노드 | [NPM](https://www.npmjs.com/package/azure-event-hubs) | 해당 없음 | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | 해당 없음 | 해당 없음 | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>추가 정보

#### <a name="net"></a>.NET
hello.NET 생태계 여러 런타임, 이벤트 허브에 대 한 여러.NET 라이브러리 되므로 됩니다. hello.NET 표준 라이브러리는 hello.NET Framework 라이브러리는.NET Framework 환경 에서만 실행할 수 있습니다 하는 동안.NET Core 또는.NET Framework hello를 사용 하 여 실행할 수 있습니다. .NET Framework에 대한 자세한 내용은 [프레임워크 버전](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.

#### <a name="node"></a>노드

hello Node.js 라이브러리는 현재 미리 보기로 및 Microsoft 직원과 외부 참가자가 쪽 프로젝트로 유지 관리 합니다. 소스 코드를 포함하는 모든 참가 프로그램은 언제든지 환영이며 검토해드립니다.

## <a name="management-apis"></a>관리 API

hello 다음은 모든 사용 가능한 현재 관리 특정 라이브러리의 목록입니다. 이러한 라이브러리 중 런타임 작업을 포함 하 고 hello 목적으로 이벤트 허브 엔터티 관리에 대 한 있으며 합니다.

| 언어/플랫폼 | 관리 패키지 | 리포지토리 |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)