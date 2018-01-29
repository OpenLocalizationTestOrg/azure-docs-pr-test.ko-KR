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
ms.date: 01/23/2018
ms.author: sethm
ms.openlocfilehash: fc6db8aba887b186961da9b12e7c5f32afa4355b
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="available-relay-apis"></a>사용 가능한 Relay API

## <a name="runtime-apis"></a>런타임 API

다음 표에는 현재 사용 가능한 모든 Relay 런타임 클라이언트가 나와 있습니다.

[추가 정보](#additional-information) 섹션에는 각 런타임 라이브러리의 상태에 대한 자세한 정보가 포함되어 있습니다.

| 언어/플랫폼 | 사용 가능한 기능 | 클라이언트 패키지 | 리포지토리 |
| --- | --- | --- | --- |
| .NET Standard | 하이브리드 연결 | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | WCF 릴레이 | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | 해당 없음 |
| 노드 | 하이브리드 연결 | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>추가 정보

#### <a name="net"></a>.NET

.NET 에코 시스템에는 여러 개의 런타임이 있으므로 Event Hubs용 .NET 라이브러리도 여러 개 있습니다. .NET Framework 라이브러리는 .NET Framework 환경에서만 실행될 수 있지만 .NET Standard 라이브러리는 .NET Core 또는 .NET Framework를 사용하여 실행할 수 있습니다. .NET Framework에 대한 자세한 내용은 [프레임워크 버전](/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.

## <a name="next-steps"></a>다음 단계

Azure Relay에 대한 자세한 내용은 다음 링크를 방문하세요.
* [Azure 릴레이란?](relay-what-is-it.md)
* [릴레이 FAQ](relay-faq.md)