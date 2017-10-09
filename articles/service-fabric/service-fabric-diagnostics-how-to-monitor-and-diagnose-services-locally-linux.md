---
title: "Linux에서 Azure microservices aaaDebug | Microsoft Docs"
description: "자세한 방법을 toomonitor 하 고 로컬 개발 컴퓨터에서 Microsoft Azure Service Fabric을 사용 하 여 작성 하 여 서비스를 진단 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

모니터링, 검색, 진단 및 문제 해결 중단을 최소화 toohello 사용자 환경을 서비스 toocontinue 허용 합니다. 모니터링 및 진단은 실제 배포된 프로덕션 환경에 중요합니다. 서비스를 개발 하는 동안 비슷한 모델을 채택 hello 진단 파이프라인 tooa 프로덕션 환경 이동 하는 경우 작동 되도록 합니다. 서비스 패브릭을 사용 하면 단일 컴퓨터의 로컬 개발 한 설정 및 실제 생산 클러스터 설치 모두에서 원활 하 게 사용할 수 있는 서비스 개발자가 tooimplement 진단 쉬워집니다.


## <a name="debugging-service-fabric-java-applications"></a>Service Fabric Java 응용 프로그램 디버깅

Java 응용 프로그램에 대해 [다중 로깅 프레임워크](http://en.wikipedia.org/wiki/Java_logging_framework) 를 사용할 수 있습니다. 이후 `java.util.logging` hello 기본 옵션은 JRE hello로도 사용 됩니다 hello에 대 한 [코드 github에서 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)합니다.  hello 다음 논의 설명 어떻게 tooconfigure hello `java.util.logging` 프레임 워크입니다.

Java.util.logging 응용 프로그램을 리디렉션할 수 있습니다를 사용 하 여 toomemory, 출력 스트림, 콘솔 파일 또는 소켓을 기록 합니다. 각이 옵션에 대 한 기본 처리기 hello 프레임 워크에 이미 입력 되어 있습니다. 만들 수는 `app.properties` 모든 응용 프로그램 tooredirect 프로그램에 대 한 파일 tooconfigure hello 파일 처리기 tooa 로컬 파일을 기록 합니다.

다음 코드 조각 hello 구성을 예는 포함 되어 있습니다.

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

hello 폴더 뾰족한 tooby hello `app.properties` 파일이 있어야 합니다. Hello 후 `app.properties` 파일이 만들어지면 tooalso 필요한 항목 지점 스크립트를 수정 `entrypoint.sh` hello에 `<applicationfolder>/<servicePkg>/Code/` 폴더 tooset hello 속성 `java.util.logging.config.file` 너무`app.propertes` 파일입니다. 다음 코드 조각 hello 같이 hello 항목이 표시 됩니다.

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


이 구성의 결과로 로그가 순환 방식으로 `/tmp/servicefabric/logs/`에 수집됩니다. hello 로그 파일이 경우 이름은 mysfapp%u.%g.log 여기서:
* **%u** 는 고유 번호 tooresolve 동시 Java 프로세스 간의 충돌 합니다.
* **%g** hello 로그 회전 사이의 숫자 toodistinguish 생성 됩니다.

처리기를 명시적으로 구성 하는 경우에 기본적으로 hello 콘솔 처리기 등록 됩니다. Syslog /var/log/syslog 아래에 hello 로그를 볼 수 있습니다 하나.

자세한 내용은 참조 hello [코드 github에서 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)합니다.  


## <a name="debugging-service-fabric-c-applications"></a>Service Fabric C# 응용 프로그램 디버깅


다수의 프레임워크는 Linux의 CoreCLR 응용 프로그램 추적에 사용할 수 있습니다. 자세한 내용은 [GitHub: 로깅](http:/github.com/aspnet/logging)을 참조하세요.  EventSource는 개발자가 익숙한 tooC #'이 문서에서는 linux CoreCLR 샘플에서 추적을 위한 EventSource를 사용 합니다.

hello 첫 번째 단계에는 tooinclude System.Diagnostics.Tracing 때문에 로그 toomemory, 출력 스트림, 또는 콘솔 파일을 작성할 수 있습니다.  EventSource를 사용 하 여 로깅에 대 한 다음 프로젝트 tooyour project.json hello를 추가 합니다.

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

사용자 지정 EventListener toolisten hello 서비스 이벤트에 사용할 수 있으며 그런 다음 적절 하 게 리디렉션됩니다 tootrace 파일 수 있습니다. hello 만드는 코드는 EventSource 및 사용자 지정 EventListener를 사용 하 여 로깅 구현 하는 샘플:


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


hello 앞의 조각 파일을 출력 hello 로그 tooa에 `/tmp/MyServiceLog.txt`합니다. 이 파일 이름은 toobe 적절 하 게 업데이트 해야 합니다. Tooredirect hello 로그 tooconsole를 원하는 경우에 다음 사용자 지정 된 EventListener 클래스에 코드 조각 hello를 사용 합니다.

```csharp
public static TextWriter Out = Console.Out;
```

예제를 hello [C# 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource 및 사용자 지정 EventListener toolog 이벤트 tooa 파일을 사용 합니다.



## <a name="next-steps"></a>다음 단계
추가 된 동일한 추적 코드 hello Azure 클러스터에서 응용 프로그램의 hello 진단 tooyour 응용 프로그램 에서도 작동 합니다. 체크 아웃 hello hello 도구에 대 한 다른 옵션에 설명 하 고 설명 하는 다음이 문서를 어떻게 tooset를 구성 합니다.
* [Azure 진단으로 toocollect 기록 하는 방법](service-fabric-diagnostics-how-to-setup-lad.md)
