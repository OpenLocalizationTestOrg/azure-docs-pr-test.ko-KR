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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="55e30-103">로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스</span><span class="sxs-lookup"><span data-stu-id="55e30-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="55e30-104">Windows</span><span class="sxs-lookup"><span data-stu-id="55e30-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="55e30-105">Linux</span><span class="sxs-lookup"><span data-stu-id="55e30-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="55e30-106">모니터링, 검색, 진단 및 문제 해결 중단을 최소화 toohello 사용자 환경을 서비스 toocontinue 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="55e30-107">모니터링 및 진단은 실제 배포된 프로덕션 환경에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="55e30-108">서비스를 개발 하는 동안 비슷한 모델을 채택 hello 진단 파이프라인 tooa 프로덕션 환경 이동 하는 경우 작동 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="55e30-109">서비스 패브릭을 사용 하면 단일 컴퓨터의 로컬 개발 한 설정 및 실제 생산 클러스터 설치 모두에서 원활 하 게 사용할 수 있는 서비스 개발자가 tooimplement 진단 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="55e30-110">Service Fabric Java 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="55e30-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="55e30-111">Java 응용 프로그램에 대해 [다중 로깅 프레임워크](http://en.wikipedia.org/wiki/Java_logging_framework) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="55e30-112">이후 `java.util.logging` hello 기본 옵션은 JRE hello로도 사용 됩니다 hello에 대 한 [코드 github에서 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="55e30-113">hello 다음 논의 설명 어떻게 tooconfigure hello `java.util.logging` 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="55e30-114">Java.util.logging 응용 프로그램을 리디렉션할 수 있습니다를 사용 하 여 toomemory, 출력 스트림, 콘솔 파일 또는 소켓을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="55e30-115">각이 옵션에 대 한 기본 처리기 hello 프레임 워크에 이미 입력 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="55e30-116">만들 수는 `app.properties` 모든 응용 프로그램 tooredirect 프로그램에 대 한 파일 tooconfigure hello 파일 처리기 tooa 로컬 파일을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="55e30-117">다음 코드 조각 hello 구성을 예는 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="55e30-118">hello 폴더 뾰족한 tooby hello `app.properties` 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="55e30-119">Hello 후 `app.properties` 파일이 만들어지면 tooalso 필요한 항목 지점 스크립트를 수정 `entrypoint.sh` hello에 `<applicationfolder>/<servicePkg>/Code/` 폴더 tooset hello 속성 `java.util.logging.config.file` 너무`app.propertes` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="55e30-120">다음 코드 조각 hello 같이 hello 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="55e30-121">이 구성의 결과로 로그가 순환 방식으로 `/tmp/servicefabric/logs/`에 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="55e30-122">hello 로그 파일이 경우 이름은 mysfapp%u.%g.log 여기서:</span><span class="sxs-lookup"><span data-stu-id="55e30-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="55e30-123">**%u** 는 고유 번호 tooresolve 동시 Java 프로세스 간의 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="55e30-124">**%g** hello 로그 회전 사이의 숫자 toodistinguish 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="55e30-125">처리기를 명시적으로 구성 하는 경우에 기본적으로 hello 콘솔 처리기 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="55e30-126">Syslog /var/log/syslog 아래에 hello 로그를 볼 수 있습니다 하나.</span><span class="sxs-lookup"><span data-stu-id="55e30-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="55e30-127">자세한 내용은 참조 hello [코드 github에서 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="55e30-128">Service Fabric C# 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="55e30-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="55e30-129">다수의 프레임워크는 Linux의 CoreCLR 응용 프로그램 추적에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="55e30-130">자세한 내용은 [GitHub: 로깅](http:/github.com/aspnet/logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55e30-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="55e30-131">EventSource는 개발자가 익숙한 tooC #'이 문서에서는 linux CoreCLR 샘플에서 추적을 위한 EventSource를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="55e30-132">hello 첫 번째 단계에는 tooinclude System.Diagnostics.Tracing 때문에 로그 toomemory, 출력 스트림, 또는 콘솔 파일을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="55e30-133">EventSource를 사용 하 여 로깅에 대 한 다음 프로젝트 tooyour project.json hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="55e30-134">사용자 지정 EventListener toolisten hello 서비스 이벤트에 사용할 수 있으며 그런 다음 적절 하 게 리디렉션됩니다 tootrace 파일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="55e30-135">hello 만드는 코드는 EventSource 및 사용자 지정 EventListener를 사용 하 여 로깅 구현 하는 샘플:</span><span class="sxs-lookup"><span data-stu-id="55e30-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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


<span data-ttu-id="55e30-136">hello 앞의 조각 파일을 출력 hello 로그 tooa에 `/tmp/MyServiceLog.txt`합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="55e30-137">이 파일 이름은 toobe 적절 하 게 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="55e30-138">Tooredirect hello 로그 tooconsole를 원하는 경우에 다음 사용자 지정 된 EventListener 클래스에 코드 조각 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="55e30-139">예제를 hello [C# 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource 및 사용자 지정 EventListener toolog 이벤트 tooa 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="55e30-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55e30-140">Next steps</span></span>
<span data-ttu-id="55e30-141">추가 된 동일한 추적 코드 hello Azure 클러스터에서 응용 프로그램의 hello 진단 tooyour 응용 프로그램 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="55e30-142">체크 아웃 hello hello 도구에 대 한 다른 옵션에 설명 하 고 설명 하는 다음이 문서를 어떻게 tooset를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55e30-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="55e30-143">Azure 진단으로 toocollect 기록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="55e30-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
