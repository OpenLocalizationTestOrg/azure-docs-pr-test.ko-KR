---
title: "논리 앱에서 aaaLearn toouse hello Azure 서비스 버스 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. 서비스 버스 toosend tooAzure를 연결 하 고 메시지를 받습니다. 송신 tooqueue 같은 동작을 수행할 tootopic 송신 및 큐에서 받을 구독에서 수신 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Hello Azure 서비스 버스 커넥터와 함께 시작.
서비스 버스 toosend tooAzure를 연결 하 고 메시지를 받습니다. 송신 tooqueue 같은 동작을 수행할 tootopic 송신 및 큐에서 받을 구독에서 수신 수 있습니다.

toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다. [지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.

## <a name="connect-tooservice-bus"></a>버스 tooService 연결
논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 연결 toohello 서비스 toocreate를 해야 합니다. [연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>서비스 버스 트리거 사용
트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다. [트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>서비스 버스 동작 사용
동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/servicebus/)합니다. 

## <a name="next-steps"></a>다음 단계
[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)

