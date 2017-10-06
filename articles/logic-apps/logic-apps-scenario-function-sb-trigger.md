---
title: "aaaScenario-Azure 함수 및 Azure 서비스 버스를 사용 하 여 논리 앱 트리거 | Microsoft Docs"
description: "Azure 함수 및 Azure 서비스 버스를 사용 하 여 함수 tootrigger 논리 앱 만들기"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>시나리오: Azure Functions 및 Azure Service Bus를 사용하여 논리 앱 트리거

장기 실행 수신기 또는 작업 toodeploy 필요할 때 논리 앱에 대 한 Azure 기능 toocreate 트리거를 사용할 수 있습니다. 예를 들어, 큐에서 수신 대기하고 있다가 푸시 트리거로 즉시 논리 앱을 실행하는 함수를 만들 수 있습니다.

## <a name="build-hello-logic-app"></a>Hello 논리 앱 빌드
이 예제에서는 함수 toobe 트리거되는 각 논리 앱에 대해 실행 해야 합니다. 먼저, HTTP 요청 트리거가 있는 논리 앱을 만듭니다. hello 함수 큐 메시지를 받을 때마다 해당 끝점을 호출 합니다.  

1. 논리 앱을 만듭니다.
2. 선택 hello **수동-HTTP 요청을 받으면** 트리거.
   와 같은 도구를 사용 하 여 hello 큐 메시지와 함께 JSON 스키마 toouse를 지정할 수는 필요에 따라 [jsonschema.net](http://jsonschema.net)합니다. Hello 트리거에서 hello 스키마를 붙여 넣습니다. 스키마는 hello 모양의 hello 데이터 및 흐름 속성 hello 워크플로 통해 보다 쉽게 이해 하는 hello 디자이너 데 도움이 됩니다.
2. 큐 메시지를 받은 후 toooccur 되도록 추가 단계를 추가 합니다. 예를 들어, Office 365로 이메일을 전송합니다.  
3. Hello 트리거 toothis 논리 앱 hello 논리 앱 toogenerate hello 콜백 URL을 저장 합니다. hello URL hello 트리거 카드에 표시 됩니다.

![hello 트리거 카드에 hello 콜백 URL 표시][1]

## <a name="build-hello-function"></a>Hello 함수를 작성 합니다.
다음으로 역할을 hello 트리거 toohello 큐에서 수신 하는 함수를 만들어야 합니다.

1. Hello에 [Azure 함수 포털](https://functions.azure.com/signin)을 선택 **새 함수**를 클릭 한 hello **ServiceBusQueueTrigger-C#** 서식 파일입니다.
   
    ![Azure Functions 포털][2]
2. Hello 연결 toohello 서비스 버스 큐를 사용 하 여 Azure 서비스 버스 SDK hello 구성 `OnMessageReceive()` 수신기입니다.
3. 기본 함수 toocall hello 논리가 응용 프로그램 끝점 (앞에서 만든)을 트리거로 hello 큐 메시지를 사용 하 여 작성 합니다. 함수의 전체 예제는 다음과 같습니다. 사용 하 여 hello 예제는 `application/json` 메시지 콘텐츠 형식에 필요한 만큼이 유형을 변경할 수 있습니다.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest와 같은 도구를 통해 큐 메시지 추가 [서비스 버스 탐색기](https://github.com/paolosalvatori/ServiceBusExplorer)합니다. Hello 함수 hello 메시지를 받은 후에 즉시 실행 하는 hello 논리 앱을 참조 하십시오.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
