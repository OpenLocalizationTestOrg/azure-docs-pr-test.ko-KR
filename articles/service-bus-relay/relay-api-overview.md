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
# <a name="available-relay-apis"></a>사용 가능한 Relay API

## <a name="runtime-apis"></a>런타임 API

hello 다음 표에 모든 릴레이 런타임 클라이언트 현재 사용할 수 있습니다.

hello [추가 정보](#additional-information) 섹션의 각 런타임 라이브러리 hello 상태에 대 한 자세한 정보를 포함 합니다.

| 언어/플랫폼 | 사용 가능한 기능 | 클라이언트 패키지 | 리포지토리 |
| --- | --- | --- | --- |
| .NET Standard | 하이브리드 연결 | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | WCF 릴레이 | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | 해당 없음 |
| 노드 | 하이브리드 연결 | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>추가 정보

#### <a name="net"></a>.NET
hello.NET 생태계 여러 런타임, 이벤트 허브에 대 한 여러.NET 라이브러리 되므로 됩니다. hello.NET 표준 라이브러리는 hello.NET Framework 라이브러리는.NET Framework 환경 에서만 실행할 수 있습니다 하는 동안.NET Core 또는.NET Framework hello를 사용 하 여 실행할 수 있습니다. .NET Framework에 대한 자세한 내용은 [프레임워크 버전](/dotnet/articles/standard/frameworks#framework-versions)을 참조하세요.

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:
* [Azure 릴레이란?](relay-what-is-it.md)
* [릴레이 FAQ](relay-faq.md)