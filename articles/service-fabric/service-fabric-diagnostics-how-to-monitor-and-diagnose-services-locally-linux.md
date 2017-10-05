---
title: "Linux에서 Azure 마이크로 서비스 디버그 | Microsoft Docs"
description: "로컬 개발 컴퓨터에서 Microsoft Azure 서비스 패브릭을 사용하여 작성된 서비스를 모니터링하고 진단하는 방법에 대해 알아보세요."
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
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="1e7f3-103">로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스</span><span class="sxs-lookup"><span data-stu-id="1e7f3-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e7f3-104">Windows</span><span class="sxs-lookup"><span data-stu-id="1e7f3-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="1e7f3-105">Linux</span><span class="sxs-lookup"><span data-stu-id="1e7f3-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="1e7f3-106">모니터링, 감지, 진단 및 문제 해결을 통해 사용자 환경에 미치는 영향을 최소화하면서 서비스를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="1e7f3-107">모니터링 및 진단은 실제 배포된 프로덕션 환경에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="1e7f3-108">서비스를 개발하는 동안 유사한 모델을 채택하면 프로덕션 환경으로 이동 시 진단 파이프라인이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="1e7f3-109">서비스 패브릭을 사용하면 서비스 개발자가 단일 컴퓨터 로컬 개발 설정과 실제 사용 프로덕션 클러스터 설정 양쪽에서 매끄럽게 작동하는 진단 기능을 간편하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="1e7f3-110">Service Fabric Java 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="1e7f3-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="1e7f3-111">Java 응용 프로그램에 대해 [다중 로깅 프레임워크](http://en.wikipedia.org/wiki/Java_logging_framework) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="1e7f3-112">`java.util.logging` 이 JRE의 기본 옵션이므로 [GitHub의 코드 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="1e7f3-113">다음 논의에서는 `java.util.logging` 프레임워크를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="1e7f3-114">java.util.logging을 사용하면 응용 프로그램 로그를 메모리, 출력 스트림, 콘솔 파일 또는 소켓으로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="1e7f3-115">이들 옵션 각각에 대해 프레임워크에 이미 제공되어 있는 기본 핸들러가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="1e7f3-116">`app.properties` 파일을 만들어서 응용 프로그램에 대한 파일 핸들러가 모든 로그를 로컬 파일로 리디렉션하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="1e7f3-117">다음 코드 조각은 예제 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="1e7f3-118">`app.properties` 파일이 가리키는 폴더가 반드시 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="1e7f3-119">`app.properties` 파일이 생성된 후에는 `<applicationfolder>/<servicePkg>/Code/` 폴더의 진입점 스크립트 `entrypoint.sh`가 속성 `java.util.logging.config.file`을 `app.propertes` 파일로 설정하도록 수정도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="1e7f3-120">항목은 다음 코드 조각과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="1e7f3-121">이 구성의 결과로 로그가 순환 방식으로 `/tmp/servicefabric/logs/`에 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="1e7f3-122">이 경우의 로그 파일 이름은 mysfapp%u.%g.log입니다. 여기서,</span><span class="sxs-lookup"><span data-stu-id="1e7f3-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="1e7f3-123">**%u**는 동시 Java 프로세스 간에 충돌을 확인하기 위한 고유 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="1e7f3-124">**%g**는 회전 로그를 구분하기 위한 세대 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="1e7f3-125">기본적으로 핸들러가 명시적으로 구성되지 않으면 콘솔 핸들러가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="1e7f3-126">/var/log/syslog 아래 syslog에서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="1e7f3-127">자세한 내용은 [GitHub의 코드 예제](http://github.com/Azure-Samples/service-fabric-java-getting-started)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="1e7f3-128">Service Fabric C# 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="1e7f3-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="1e7f3-129">다수의 프레임워크는 Linux의 CoreCLR 응용 프로그램 추적에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="1e7f3-130">자세한 내용은 [GitHub: 로깅](http:/github.com/aspnet/logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="1e7f3-131">EventSource는 C# 개발자에게 친숙하기 때문에 이 문서에서는 Linux의 CoreCLR 샘플에서 추적용으로 EventSource를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="1e7f3-132">첫 번째 단계는 메모리, 출력 스트림 또는 콘솔 파일 로그를 쓸 수 있도록 System.Diagnostics.Tracing를 포함하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="1e7f3-133">EventSource를 사용하여 기록하려면 project.json에 다음 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="1e7f3-134">서비스 이벤트를 수신 대기하기 위해 사용자 지정 EventListener를 사용한 다음 적절하게 리디렉션하여 파일을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="1e7f3-135">다음 코드 조각은 EventSource 및 사용자 지정 EventListener를 사용하여 로깅의 샘플 구현을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need to add method for sample event.

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


<span data-ttu-id="1e7f3-136">앞의 코드 조각은 로그를 `/tmp/MyServiceLog.txt`의 파일에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="1e7f3-137">이 파일 이름을 적절하게 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="1e7f3-138">콘솔로 기록을 리디렉션하려는 경우 사용자 지정된 EventListener 클래스에 다음 코드 조각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="1e7f3-139">[C# 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)의 샘플은 EventSource 및 사용자 지정 EventListener를 사용하여 이벤트를 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1e7f3-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e7f3-140">Next steps</span></span>
<span data-ttu-id="1e7f3-141">응용 프로그램에 추가된 동일한 추적 코드 역시 Azure 클러스터에서 응용 프로그램의 진단과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="1e7f3-142">도구에 대한 다양한 옵션과 도구를 설정하는 방법에 대해 설명하는 이러한 문서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e7f3-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="1e7f3-143">Azure 진단을 사용하여 로그를 수집하는 방법</span><span class="sxs-lookup"><span data-stu-id="1e7f3-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
