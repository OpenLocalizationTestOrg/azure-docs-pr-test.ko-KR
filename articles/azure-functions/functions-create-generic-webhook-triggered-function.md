---
title: "제네릭 webhook에 의해 트리거되는 Azure에서 함수 aaaCreate | Microsoft Docs"
description: "Azure 함수 toocreate Azure에서 webhook 호출 하는 서버가 없는 함수를 사용 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a>제네릭 웹후크를 통해 트리거되는 함수 만들기

Azure 기능을 사용 하면 toofirst VM을 만들거나 웹 응용 프로그램을 게시 하지 않고도 서버가 없는 환경에서 코드를 실행 합니다. 예를 들어 Azure 모니터에 의해 발생 된 경고가 트리거됨 함수 toobe를 구성할 수 있습니다. 이 항목에서는 리소스 그룹은 때 tooexecute C# 코드 tooyour 구독을 추가 하는 방법을 보여 줍니다.   

![제네릭 webhook hello Azure 포털에서에서 함수를 트리거](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a>필수 조건 

toocomplete이이 자습서:

+ Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure Function 앱 만들기

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

다음으로 hello 새 함수 앱에서 함수를 만듭니다.

## <a name="create-function"></a>제네릭 웹후크를 통해 트리거되는 함수 만들기

1. 함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다. 이 함수는 함수 응용 프로그램의 첫 번째 hello는, 선택 **사용자 정의 함수**합니다. 이 함수 템플릿의 hello 전체 집합을 표시합니다.

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. 선택 hello **제네릭 WebHook-C#** 서식 파일입니다. C# 함수의 이름을 입력하고 **만들기**를 선택합니다.

     ![Hello Azure 포털에서에서 트리거된 제네릭 webhook 함수를 만듭니다](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. 클릭 하 여 새 함수에 **<> / Get 함수 URL**, 다음 복사 하 고 hello 값을 저장 합니다. 이 값 tooconfigure hello webhook를 사용 합니다. 

    ![Hello 함수 코드를 검토 합니다.](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
다음으로 Azure Monitor의 활동 로그 경고에서 웹후크 끝점을 만듭니다. 

## <a name="create-an-activity-log-alert"></a>활동 로그 경고 만들기

1. Hello Azure 포털에서 탐색 toohello **모니터** 서비스, **경고**를 클릭 하 고 **추가 활동 로그 경고**합니다.   

    ![모니터](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. Hello 테이블에 지정 된 hello 설정을 사용 합니다.

    ![활동 로그 경고 만들기](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | 설정      |  제안 값   | 설명                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **활동 로그 경고 이름** | resource-group-create-alert | Hello 활동 로그 경고의 이름입니다. |
    | **구독** | 사용자의 구독 | 이 자습서에 사용 하는 hello 구독입니다. | 
    |  **리소스 그룹** | myResourceGroup | hello 리소스 그룹에 배포 된 hello 경고 리소스입니다. 함수 앱 함에 따라 것 보다 쉽게 tooclean hello 자습서를 완료 한 후에 동일한 리소스 그룹을 hello를 사용 하 여 합니다. |
    | **이벤트 범주** | 관리 | 이 범주는 변경 내용을 tooAzure 리소스를 포함 합니다.  |
    | **리소스 종류** | 리소스 그룹 | 경고 tooresource 그룹 활동을 필터링합니다. |
    | **리소스 그룹**<br/>및 **리소스** | 모두 | 모든 리소스를 모니터링합니다. |
    | **작업 이름** | 리소스 그룹 만들기 | 경고 toocreate 작업을 필터링합니다. |
    | **Level** | 정보 제공 | 정보 수준 경고를 포함합니다. | 
    | **상태** | Succeeded | 성공적으로 완료 된 경고 tooactions를 필터링 합니다. |
    | **작업 그룹** | 새로 만들기 | 경고가 발생 하는 경우 수행 하는 hello 작업을 정의 하는 새 작업 그룹을 만듭니다. |
    | **작업 그룹 이름** | function-webhook | 이름 tooidentify hello 작업 그룹입니다.  | 
    | **짧은 이름** | funcwebhook | Hello 동작 그룹에 대 한 짧은 이름입니다. |  

3. **동작**, hello 설정을 사용 하 여 hello 테이블에 지정 된 작업을 추가 합니다. 

    ![작업 그룹 추가](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | 설정      |  제안 값   | 설명                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Name** | CallFunctionWebhook | Hello 동작에 대 한 이름입니다. |
    | **작업 유형** | 웹후크 | hello 응답 toohello 경고는 Webhook URL 호출 됩니다. |
    | **세부 정보** | 함수 URL | 앞에서 복사한 hello 함수 hello webhook URL에 붙여 넣습니다. |v

4. 클릭 **확인** toocreate hello 경고 및 작업 그룹입니다.  

구독에서 리소스 그룹을 만들 때 이제 hello webhook 라고 합니다. 다음으로, 함수 toohandle hello hello hello 요청 본문의 JSON 로그 데이터의에서 hello 코드를 업데이트 합니다.   

## <a name="update-hello-function-code"></a>Hello 함수 코드를 업데이트 합니다.

1. Hello 포털에서 뒤로 tooyour 함수 응용 프로그램을 찾아서 함수를 확장 합니다. 

2. 코드 다음 hello hello 포털에서 hello 함수가 hello C# 스크립트 코드를 바꿉니다.

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

이제 구독에 새 리소스 그룹을 만들어 hello 함수를 테스트할 수 있습니다.

## <a name="test-hello-function"></a>테스트 hello 함수

1. Hello Azure 포털의 왼쪽 hello hello 리소스 그룹 아이콘을 클릭 **+ 추가**, 입력 **리소스 그룹 이름은**를 선택 하 고 **만들기** toocreate 빈 리소스 그룹입니다.
    
    ![리소스 그룹을 만듭니다.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. Tooyour 함수 돌아가서 hello 확장 **로그** 창. Hello 리소스 그룹을 만든 후 hello 활동 로그 경고 트리거 hello webhook 및 hello 함수를 실행 합니다. Toohello 로그 기록 hello 새 리소스 그룹의 hello 이름을 표시 합니다.  

    ![테스트 응용 프로그램 설정을 추가합니다.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. (선택 사항) 뒤로 돌아가서 만든 hello 리소스 그룹을 삭제 합니다. 참고가이 활동 hello 함수를 트리거되지 않습니다. 즉, delete 작업 hello 경고에 의해 필터링 됩니다. 

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>다음 단계

제네릭 웹후크에서 요청을 수신할 때 실행되는 함수를 만들었습니다. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

웹후크 트리거에 대한 자세한 내용은 [Azure Functions HTTP 및 웹후크 바인딩](functions-bindings-http-webhook.md)을 참조하세요. C#의 기능을 개발에 대해 자세히 toolearn 참조 [Azure 함수 C# 스크립트 개발자 참조](functions-reference-csharp.md)합니다.

