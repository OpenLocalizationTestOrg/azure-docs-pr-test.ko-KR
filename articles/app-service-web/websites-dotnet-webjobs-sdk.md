---
title: "aaaWhat는 hello Azure WebJobs SDK"
description: "소개 toohello Azure WebJobs SDK입니다. 어떤 hello SDK는, 수행 하는 데 유용 하는 일반적인 시나리오 및 코드 샘플에 설명 합니다."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Hello Azure WebJobs SDK는 무엇입니까
## <a id="overview"></a>개요
이 문서에서는 WebJobs SDK hello 기능 설명를 검토 하는 몇 가지 일반적인 시나리오에 유용 하 고 사용법 코드에 대 한 개요를 제공 합니다.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs](websites-webjobs-resources.md) 는 프로그램 또는 스크립트의 hello toorun 수 있는 Azure 앱 서비스의 기능 웹 응용 프로그램, API 응용 프로그램 또는 모바일 앱으로 동일한 컨텍스트. hello의 목적은 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 코드가 예: 이미지 처리, 처리 큐, RSS 집계, 파일 유지 관리 같은 웹 작업이 수행할 수 있는 일반적인 작업에 대해 작성 되 고 전자 메일 보내기. hello WebJobs SDK는 Azure 저장소 및 서비스 버스 작업을 위한, 작업을 예약 하 고 오류를 처리 및 기타 여러 가지 일반적인 시나리오에 대 한 기본 제공 기능이 있습니다. 기능은 또한 toobe 확장 가능 합니다. hello [WebJobs SDK는 오픈 소스](https://github.com/Azure/azure-webjobs-sdk/), 있으면는 [확장에 대 한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)합니다.

WebJobs SDK hello를 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

* **NuGet 패키지**. NuGet 패키지 tooa Visual Studio 콘솔 응용 프로그램 프로젝트를 추가 하면 WebJobs SDK 특성으로 메서드를 데코레이팅하 코드에 사용 되는 프레임 워크를 제공 합니다.
* **대시보드**. Hello WebJobs SDK의 일부 Azure 앱 서비스에 포함 되 고 hello NuGet 패키지를 사용 하는 프로그램에 대 한 다양 한 모니터링 및 진단 정보를 제공 합니다. Toowrite 코드 toouse 이러한 모니터링 및 진단 기능 않아도 됩니다.

## <a id="scenarios"></a>시나리오
Azure WebJobs SDK hello로 더 쉽게 처리할 수는 몇 가지 일반적인 시나리오는 다음과 같습니다.

* 이미지 처리 또는 기타 CPU 집중 작업. 웹 사이트의 일반적인 기능에는 hello 기능 tooupload 이미지 또는 비디오입니다. 종종을 업로드 하지 않으려는 toomake hello 사용자 대기를 수행 하는 동안 후 toomanipulate hello 콘텐츠가 필요 합니다.
* 큐 처리. 백 엔드 서비스와 웹 프런트 엔드 toocommunicate에는 일반적인 방법은 toouse 큐 사용 하는 것입니다. Hello 웹 사이트 tooget 작업을 수행 하면 메시지 큐에 밀어넣습니다. 백 엔드 서비스는 hello 큐에서 메시지를 끌어오는 및 작업 hello지 않습니다. 이미지 처리를 위해 큐를 사용할 수 있습니다: 예를 들어 hello 사용자 많은 파일을 업로드 한 후 hello 파일에에서 이름을 추가할 hello 백 엔드 처리에 의해 선택 큐 메시지 toobe 합니다. 또는 큐 tooimprove 사이트 응답성을 사용할 수 있습니다. 예를 들어 직접 tooa SQL 데이터베이스를 작성 하는 대신 tooa 큐 쓰기, 완료 하 고 hello 백 엔드 서비스 핸들 대기 시간이 긴 관계형 데이터베이스 작동 hello 사용자에 게 알림입니다. 이미지 프로세스를 사용 하 여 처리 하는 큐의 예를 들어 참조 hello [WebJobs SDK 시작 자습서](websites-dotnet-webjobs-sdk-get-started.md)합니다.
* RSS 집계. RSS 피드 목록이 유지 하는 사이트를 사용 하는 경우에 모든 백그라운드 프로세스에서 hello 피드에서 hello 문서에 가져올 수 있습니다.
* 로그 파일 집계 또는 정리와 같은 파일 유지 관리.  로그 파일이 별개의 또는 여러 개의 사이트에서 작성 되 고 있을 수 있습니다에 toocombine 변경 되는 시간 범위를 정렬 toorun 분석 작업에 있습니다. 또는 오래 된 로그 파일을 작업 toorun 매주 tooclean tooschedule 할 수 있습니다.
* Azure 테이블로 수신. 수 저장 된 파일 및 blob 있고 tooparse 하 고 hello 데이터 테이블에 저장 합니다. 수신 함수 hello 여러 행 (경우에 따라 수백만)를 쓸 수 있습니다 및 hello WebJobs SDK 가능한 tooimplement를 사용 하면이 기능 쉽게 합니다. hello SDK는 또한 hello hello 테이블에 쓰여진 행 수와 같이 진행률 표시기에 대 한 실시간 모니터링을 제공 합니다.
* 백그라운드 스레드에서 toorun와 같은 되도록 다른 장기 실행 작업 [전자 메일을 보내는](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure)합니다. 
* Toorun 매일 밤 백업 작업을 수행 하는 등의 일정에 따라 원하는 작업입니다.

여러 이러한 시나리오에서 여러 Vm 동시에 여러 개의 WebJobs 실행에서 웹 앱 toorun tooscale를 수도 있습니다. 이 인해 hello에 동일 데이터를 처리 하는 일부 시나리오에서 여러 번 하지만이 문제가 되지 않습니다는 hello 기본 제공 큐, blob 및 hello WebJobs SDK의 서비스 버스 트리거를 사용 하는 경우. hello SDK 통해 각 메시지 또는 blob에 대 한 함수를 한 번만 처리할 수 됩니다.

hello WebJobs SDK을 사용 하면 쉽게 toohandle 일반적인 오류 처리 시나리오입니다. 설정할 수 있습니다 경고를 toosend 알림을 함수 오류가 발생 했으며 함수는 지정한 제한 시간 내에 완료 하지 않는 자동으로 취소 되도록 시간 제한을 설정할 수 있습니다.

## <a id="code"></a> 코드 샘플
Azure 저장소에서 작동 하는 일반적인 작업을 처리 하기 위한 hello 코드는 간단 합니다. 콘솔 응용 프로그램에서 `Main` 만들면 메서드는 `JobHost` hello를 조정 하는 개체 작성 toomethods를 호출 합니다. hello WebJobs SDK 프레임 워크를 알고 hello WebJobs SDK를 기반으로 메서드와 어떤 매개 변수 값 toouse toocall 때 특성에 사용 합니다. hello SDK 제공 *트리거* 호출 hello 함수 toobe 시키는 조건을 지정 하는 및 *바인더* 지정 하는 방법을 tooget 정보 내부 / 외부로 메서드 매개 변수입니다.

예를 들어 hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) 특성을 사용 하면 큐에서 메시지를 수신 하 고 hello 메시지는 자동으로 역직렬화 된 hello 메시지 형식은 바이트 배열 또는 사용자 지정 형식에 대 한 JSON 경우 때 호출 함수 toobe 합니다. hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) 는 Azure 저장소 계정에 새 blob을 만들 때마다 특성 프로세스를 트리거합니다.

아래에는 큐를 폴링하고 수신된 각 큐 메시지에 대해 Blob를 만드는 간단한 프로그램이 나와 있습니다.

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

hello `JobHost` 개체는 일련의 배경 함수에 대 한 컨테이너입니다. hello `JobHost` 개체 모니터 hello 함수를 트리거하는 이벤트를 감시 하 고 트리거 이벤트가 발생할 때 hello 함수를 실행 합니다. 호출 하는 `JobHost` 메서드 tooindicate hello 컨테이너 프로세스 toorun에 연결할지 hello 현재 스레드 또는 백그라운드 스레드가 있습니다. Hello 예에서 hello `RunAndBlock` 메서드 hello 프로세스 지속적으로 hello 현재 스레드의 실행 합니다.

때문에 hello `ProcessQueueMessage` 이 예에서 메서드에 `QueueTrigger` 특성 hello 트리거 해당 함수는 hello 새 큐 메시지의 आ स ा. hello `JobHost` hello 지정 된 큐 (이 샘플에서 "webjobsqueue")에 새 큐 메시지 개체를 감시 하 고 발견 되 면 호출 하 고 `ProcessQueueMessage`합니다. 

hello `QueueTrigger` 특성 바인딩합니다 hello `inputText` hello 큐 메시지의 매개 변수 toohello 값입니다. Hello 및 `Blob` 바인딩 특성을 `TextWriter` 개체 tooa blob 이름은 "containername" 라는 컨테이너에 "blobname"를 지정 합니다.  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

hello 함수 hello 큐 메시지 toohello blob의 toowrite hello 이러한 매개 변수 값에 다음 사용 하 여:

        writer.WriteLine(inputText);

hello WebJobs SDK의 hello 트리거와 바인더 기능 toowrite는 hello 코드를 간소화 합니다. hello 필요한 하위 수준 코드 tooprocess 큐, blob 또는 파일 또는 tooinitiate 예약 된 작업은 자동으로 수행 하 여 hello WebJobs SDK 프레임 워크입니다. 예를 들어 hello 프레임 워크는 아직 존재 하지 않는 큐를 만듭니다, 그리고 열립니다 hello 큐, 메시지를 큐에 읽기, 삭제 큐에 메시지 처리가 완료 된은 존재 하지 않는 blob 컨테이너를 만들고 아직 tooblobs, 및 기타 등등을 씁니다.

hello 다음 코드 예제에서는 다양 한 트리거에서 하나의 WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, 및 `ErrorTrigger`합니다. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a> 예약
hello `TimerTrigger` 특성은 일정에 따라 기능 tootrigger 함수 toorun hello 합니다. WebJobs SDK를 hello를 통해 전체 Azure 또는 일정 개별 함수 사용 하 여 웹 작업으로는 WebJob을 예약할 수 `TimerTrigger`합니다. 코드 샘플은 다음과 같습니다.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

더 많은 샘플 코드에 대 한 참조 [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) GitHub.com에 hello webjobs sdk 확장 azure 저장소에 있습니다.

## <a name="extensibility"></a>확장성
Toobuilt에 제한 되지 하는 기능-hello WebJobs SDK 있습니다 toowrite 사용자 지정 트리거 및 바인더입니다.  예를 들어, 캐시 이벤트 및 정기적인 일정에 대한 트리거를 작성할 수 있습니다. [오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions) 포함 한 [WebJobs SDK 확장성에 대 한 자세한 지침](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) 및 샘플 코드 toohelp 드리겠습니다 자신의 트리거 및 바인더 작성 합니다.

## <a id="workerrole"></a>Hello WebJobs 외부에서 WebJobs SDK를 사용 하 여
WebJobs SDK는 표준 콘솔 응용 프로그램 및 어느-실행할 있습니다 hello hello를 사용 하는 프로그램 toorun는 WebJob으로 되어 있지 않습니다. 프로덕션 이러한 환경 중 하나를 선호 하는 경우 클라우드 서비스 작업자 역할 또는 Windows 서비스에서 실행할 수 있습니다 및 개발 컴퓨터에서 로컬로 hello 프로그램을 테스트할 수 있습니다. 

그러나 hello 대시보드는 Azure 앱 서비스 웹 앱에 대 한 확장으로 사용할 수만 있습니다. WebJob 외부 toorun를 원하고 여전히 hello 대시보드를 사용 하는 경우에 웹을 구성할 수 있습니다 앱 toouse hello 동일한 저장소 계정 연결 문자열을 WebJobs SDK 대시보드 참조 하 고 해당 웹 응용 프로그램의 WebJobs 대시보드 그런 다음 함수에 대 한 데이터를 표시 됩니다 다른 위치를 실행 하는 프로그램에서 실행 합니다. URL https:// hello를 사용 하 여 toohello 대시보드를 얻을 수*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions 합니다. 자세한 내용은 참조 [hello WebJobs SDK로 로컬 개발에 대 한 대시보드를 가져오는](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), 하지만 hello 블로그 게시물 이전 연결 문자열 이름에 표시 합니다. 

## <a id="nostorage"></a>대시보드 기능
WebJobs SDK hello WebJobs SDK 트리거 또는 바인더를 사용 하지 않는 경우에 여러 가지 이점을 제공 합니다.

* 대시보드 hello에서 함수를 호출할 수 있습니다.
* 대시보드 hello에서 함수를 재생할 수 있습니다.
* 대시보드, 연결 된 toohello hello에 로그를 볼 수 특정 WebJob (Console.Out, Console.Error, 추적 등을 사용 하 여 작성 된 응용 프로그램 로그) 또는를 생성 toohello 특정 함수 호출 연결 (로그를 사용 하 여 기록는 `TextWriter` SDK toohello 함수를 매개 변수로 전달 하는 hello 개체). 

자세한 내용은 참조 [toomanually 함수를 호출 하는 방법을](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) 및 [toowrite 기록 하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>다음 단계
WebJobs SDK hello에 대 한 자세한 내용은 참조 [Azure WebJobs 리소스 권장](http://go.microsoft.com/fwlink/?linkid=390226)합니다.

Hello 최신 향상 기능 toohello WebJobs SDK에 대 한 정보를 참조 hello [릴리스 정보](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)합니다.

