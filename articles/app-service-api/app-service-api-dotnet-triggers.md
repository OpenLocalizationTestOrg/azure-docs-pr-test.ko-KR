---
title: "서비스 API 앱 트리거 aaaApp | Microsoft Docs"
description: "Azure 앱 서비스에서 API 앱에서 tooimplement 트리거합니다 하는 방법"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a>Azure 앱 서비스 API 앱 트리거
> [!NOTE]
> 이 버전의 hello 문서 tooAPI 앱 2014-12-01-미리 보기 스키마 버전을 적용합니다.
>
>

## <a name="overview"></a>개요
이 문서에서는 tooimplement API 앱 트리거하며 논리 앱에서 사용을 설명 합니다.

이 항목의 hello 코드 조각 복사 hello에서 [있는 FileWatcher API 앱 코드 샘플](http://go.microsoft.com/fwlink/?LinkId=534802)합니다.

Toodownload hello hello 코드 문서 toobuild이에 대 한 nuget 패키지 하 고 실행 해야 하는 참고: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/)합니다.

## <a name="what-are-api-app-triggers"></a>API 앱 트리거 정의
API 앱 toofire 이벤트에 대 한 일반적인 시나리오는 하는 hello API 앱의 클라이언트에서 응답 toohello 이벤트 hello 적절 한 조치를 수행할 수 있도록 합니다. 이 시나리오를 지 원하는 REST API 기반 메커니즘 hello API 앱 트리거에서 호출 됩니다.

예를 들어 가정해 클라이언트 코드는 hello를 사용 하 여 [Twitter 커넥터 API 앱](../connectors/connectors-create-api-twitter.md) 코드 필요한 특정 단어를 포함 하는 새 트 윗에 기반한 동작 tooperform 및 합니다. 이 경우 이와 같이 폴링 또는 푸시 트리거 toofacilitate를 설정할 수 있습니다.

## <a name="poll-trigger-versus-push-trigger"></a>폴링 트리거와 밀어넣기 트리거
현재 다음 두 가지 유형의 트리거가 지원됩니다.

* 설문 조사 트리거-클라이언트를 폴링하여 이벤트 발생 했음을 것에 대 한 알림 hello API 앱
* 이벤트가 발생할 때 hello API 앱 로부터 알림을 푸시 트리거-클라이언트

### <a name="poll-trigger"></a>폴링 트리거
설문 조사 트리거는 일반 REST API로 구현 되었으며 해당 클라이언트 (예: 논리 앱) toopoll에서는 주문 tooget 알림에 있습니다. Hello 클라이언트 상태를 유지 될 수 있습니다, 하는 동안에 자체 hello 폴링 트리거는 상태 비저장입니다.

다음 요청 및 응답 패킷 hello에 대 한 정보는 hello hello 폴링 트리거 계약의 몇 가지 주요 측면을 설명 합니다.

* 요청
  * HTTP 메서드: GET
  * 매개 변수
    * triggerState-사용 하면 클라이언트가이 선택적 매개 변수는 hello 폴링 트리거 하므로 상태일 수 제대로 toospecify tooreturn 알림 또는 하지 기반된 hello 상태가 지정 되었는지 여부를 결정 합니다.
    * API 관련 매개 변수
* 응답
  * 상태 코드 **200** -요청이 유효 하 고는 hello 트리거에서 알림이 표시 됩니다. hello 알림의 hello 콘텐츠 hello 응답 본문 됩니다. Hello에 대 한 응답 "Retry-after" 헤더는 후속 요청 호출 하 여 추가 알림 데이터를 검색할 수 있어야 나타냅니다.
  * 상태 코드 **202** -요청 유효 하지만 hello 트리거에서 새 알림이 있습니다.
  * 상태 코드 **4xx** - 요청이 유효하지 않습니다. hello 클라이언트 hello 요청을 다시 시도 합니다.
  * 상태 코드 **5xx** - 요청 시 내부 서버 오류 및/또는 일시적인 문제가 발생했습니다. hello 클라이언트 hello 요청을 다시 시도 합니다.

다음 코드 조각 hello는 tooimplement 설문 조사를 트리거할 방법의 예시입니다.

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

이 폴링 트리거가 tootest을 다음이 단계를 수행 합니다.

1. 배포의 인증 설정 사용 하 여 API 앱 hello **익명 공용**합니다.
2. Hello 호출 **터치** 작업 tootouch 파일입니다. 다음 이미지는 hello 우체부 통해 샘플 요청을 보여 줍니다.
   ![Postman을 통해 Touch 작업 호출](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
3. Hello로 hello 폴링 트리거 호출 **triggerState** tooa 타임 스탬프 이전 tooStep #2 매개 변수를 설정 합니다. hello 다음 이미지에서는 우체부 통해 hello 샘플 요청
   ![Postman을 통해 폴링 트리거 호출](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)

### <a name="push-trigger"></a>밀어넣기 트리거
밀어넣기 트리거 푸시 알림을 tooclients toobe 특정 이벤트를 발생 하는 경우 알림을 등록 하는 일반 REST API로 구현 됩니다.

다음 요청 및 응답 패킷 hello에 대 한 정보는 hello hello 푸시 트리거 계약의 몇 가지 주요 측면을 설명 합니다.

* 요청
  * HTTP 메서드: PUT
  * 매개 변수
    * triggerId: 필요-불투명 문자열 (예: GUID) 나타내는 hello 밀어넣기 트리거의 등록을 합니다.
    * callbackUrl: 필요-hello 콜백 tooinvoke hello 이벤트가 발생할 때의 URL입니다. hello 호출에 대 한 단순 HTTP POST 호출입니다.
    * API 관련 매개 변수
* 응답
  * 상태 코드 **200** -요청 tooregister 클라이언트가 성공 합니다.
  * 상태 코드 **4xx** - 요청이 유효하지 않습니다. hello 클라이언트 hello 요청을 다시 시도 합니다.
  * 상태 코드 **5xx** - 요청 시 내부 서버 오류 및/또는 일시적인 문제가 발생했습니다. hello 클라이언트 hello 요청을 다시 시도 합니다.
* 콜백
  * HTTP 메서드: POST
  * 요청 본문: 알림 내용

다음 코드 조각 hello은 tooimplement 푸시를 트리거할 방법의 예:

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

이 폴링 트리거가 tootest을 다음이 단계를 수행 합니다.

1. 배포의 인증 설정 사용 하 여 API 앱 hello **익명 공용**합니다.
2. 너무 찾아보기[http://requestb.in/](http://requestb.in/) toocreate 콜백 URL로 사용할 RequestBin 합니다.
3. 으로 GUID 가진 hello 푸시 트리거 호출 **triggerId** RequestBin URL로 hello 및 **callbackUrl**합니다.
   ![Postman을 통해 밀어넣기 트리거 호출](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)
4. Hello 호출 **터치** 작업 tootouch 파일입니다. 다음 이미지는 hello 우체부 통해 샘플 요청을 보여 줍니다.
   ![Postman을 통해 Touch 작업 호출](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)
5. 푸시 트리거 콜백 hello hello RequestBin tooconfirm 속성 출력와 함께 호출 되는지 확인 합니다.
   ![Postman을 통해 폴링 트리거 호출](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)

### <a name="describe-triggers-in-api-definition"></a>API 정의에서 트리거 설명
을 hello 트리거 구현 및 API 앱 tooAzure 배포 후 이동 toohello **API 정의** 트리거 hello에 의해 발생 하는 UI에서 자동으로 인식 됩니다 블레이드 hello Azure preview 포털에 나타납니다. hello hello API 앱의 Swagger 2.0 API 정의 합니다.

![API 정의 블레이드](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

Hello를 누르면 **Swagger 다운로드** 단추와 열기 hello JSON 파일을 다음 결과 유사한 toohello 표시 됩니다.

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

확장 속성을 hello **x-ms-schedular-트리거** 는 트리거를 API 정의에 설명 하는 방법 및 hello의 tooone를 요청 하는 경우 hello 게이트웨이 통해 hello API 정의 요청 하는 경우 hello API 응용 프로그램 게이트웨이에 의해 자동으로 추가 다음 조건 번호입니다. 이 속성을 수동으로 추가할 수도 있습니다.

* 폴링 트리거
  * Hello HTTP 메서드가 **가져오기**합니다.
  * 경우 hello **operationId** hello 문자열을 포함 하는 속성 **트리거**합니다.
  * 경우 hello **매개 변수** 속성으로 매개 변수를 포함 한 **이름** 속성이 너무 설정**triggerState**합니다.
* 밀어넣기 트리거
  * Hello HTTP 메서드가 **배치**합니다.
  * 경우 hello **operationId** hello 문자열을 포함 하는 속성 **트리거**합니다.
  * 경우 hello **매개 변수** 속성으로 매개 변수를 포함 한 **이름** 속성이 너무 설정**triggerId**합니다.

## <a name="use-api-app-triggers-in-logic-apps"></a>논리 앱에서 API 앱 트리거 사용
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a>목록 및 API 앱 트리거 hello 논리 앱 디자이너에서 구성
Hello에 논리 앱을 만드는 경우와 동일한 리소스 그룹 hello API 앱, 수 tooadd 됩니다 것 toohello 디자이너 캔버스를 클릭 하 여 하기만 합니다. 다음 이미지는 hello 이러한 경우를 설명 합니다.

![논리 앱 디자이너의 트리거](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![논리 앱 디자이너에서 폴링 트리거 구성](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![논리 앱 디자이너에서 밀어넣기 트리거 구성](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a>논리 앱에 맞게 API 앱 트리거 최적화
트리거 tooan API 앱에 추가한 후 몇 가지 방법으로 hello API 앱을 사용 하 여 논리 앱의 경우 tooimprove hello 경험을 수행할 수 있습니다.

예를 들어 hello **triggerState** 폴링 트리거에 대 한 매개 변수는 toohello 다음 식은 hello 논리 앱에 설정 해야 합니다. 이 식은 hello hello 논리 앱에서 hello 트리거의 마지막 호출을 평가 하 고 해당 값을 반환 해야 합니다.  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

참고:에 대 한 설명은 위의 hello 식에 사용 되는 hello 함수 참조 toohello 설명서에 [논리 앱 워크플로 정의 언어](https://msdn.microsoft.com/library/azure/dn948512.aspx)합니다.

논리 앱 사용자 hello에 대 한 위의 tooprovide hello 식 해야 **triggerState** hello 트리거를 사용 하는 동안 매개 변수입니다. Hello 확장 속성을 통해 hello 논리가 응용 프로그램 디자이너에서이 값이 사전 설정 가능한 toohave는 **ms 스케줄러 권장 x**합니다.  hello **x ms 표시** 확장 속성의 tooa 값 *내부* hello 매개 변수 자체를 hello 디자이너에 표시 되지 않습니다.  다음 코드 조각 hello 것을 보여줍니다.

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

밀어넣기 트리거에 대 한 hello **triggerId** 매개 변수 hello 논리 앱을 고유 하 게 식별 해야 합니다. 권장된 모범 사례는이 속성 toohello 이름을 사용 하 여 hello 워크플로의 다음 식은 hello tooset:

    @workflow().name

Hello를 사용 하 여 **ms 스케줄러 권장 x** 및 **x ms 표시** toohello 논리 앱 디자이너 tooautomatically이 설정의 확장 속성의 API 정의 hello API 앱에 전달할 수 있습니다 hello 사용자에 대 한 식입니다.

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a>API 정의에서 확장 속성 추가
Hello 확장 속성과 같은 추가 메타 데이터 정보- **ms 스케줄러 권장 x** 및 **x ms 표시** -두 가지 방법 중 하나로 hello API 정의에 추가할 수 있습니다: 정적 또는 동적입니다.

정적 메타 데이터에 대 한 직접 편집할 수 있습니다 hello */metadata/apiDefinition.swagger.json* 프로젝트에서 파일을 수동으로 hello 속성을 추가 합니다.

동적 메타 데이터를 사용 하 여 API 앱에 대 한 hello SwaggerConfig.cs 파일 tooadd 이러한 확장을 추가할 수 있는 작업 필터를 편집할 수 있습니다.

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


hello 다음은이 클래스 구현된 toofacilitate hello 동적 메타 데이터 시나리오를 수 있는 방법의 예입니다.

    // Add extension properties on hello triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
