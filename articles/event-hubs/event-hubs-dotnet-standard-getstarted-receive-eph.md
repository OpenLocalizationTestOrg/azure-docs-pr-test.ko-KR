---
title: "표준.NET을 사용 하 여 Azure 이벤트 허브에서 aaaReceive 이벤트 | Microsoft Docs"
description: "표준.NET에서 EventProcessorHost hello로 메시지를 받기 시작."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>표준.NET의 이벤트 프로세서 호스트 hello로 메시지를 받기 시작.

> [!NOTE]
> 이 샘플은 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)에서 사용할 수 있습니다.

이 자습서에서는 어떻게 toowrite.NET Core 콘솔 사용 하 여 이벤트 허브에서 메시지를 수신 하는 응용 프로그램 **EventProcessorHost**합니다. Hello를 실행할 수 있습니다 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) 솔루션으로-, 대체 문자열 hello 이벤트 허브 및 저장소 계정 값을 사용 합니다. 참고할 수 또는 hello에서에서 단계를이 자습서 toocreate 직접 합니다.

## <a name="prerequisites"></a>필수 조건

* [Microsoft Visual Studio 2015 또는 2017](http://www.visualstudio.com). hello의에서 예제가 자습서에서는 Visual Studio 2017 하지만 Visual Studio 2015 에서도 지원 됩니다.
* [.NET Core Visual Studio 2015 또는 2017 도구](http://www.microsoft.com/net/core).
* Azure 구독.
* Azure Event Hubs 네임스페이스.
* Azure 저장소 계정.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs 네임스페이스 및 이벤트 허브 만들기  

hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate hello 이벤트 허브에 대 한 네임 스페이스를 입력 하 고 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다. toocreate 네임 스페이스 및 이벤트 허브 hello 절차에 따라 [이 여기서](event-hubs-create.md), 다음 단계를 수행 하는 hello 진행 합니다.  

## <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기  

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.  
2. Hello hello 포털의 왼쪽된 탐색 창에서 클릭 **새로**, 클릭 **저장소**, 클릭 하 고 **저장소 계정**합니다.  
3. 저장소 계정 블레이드에서 hello hello 필드에 내용을 입력 하 고 클릭 **만들기**합니다.

    ![저장소 계정 만들기][1]

4. Hello를 본 후 **배포 성공** 메시지에서 새 저장소 계정 hello의 hello 이름을 클릭 합니다. Hello에 **Essentials** 블레이드에서 클릭 **Blob**합니다. Hello 때 **Blob 서비스** 블레이드를 열고, 클릭 **+ 컨테이너** hello 위쪽에 있습니다. Hello 컨테이너 이름을 입력 한 다음 hello 닫습니다 **Blob 서비스** 블레이드입니다.  
5. 클릭 **선택키가** hello 왼쪽된 블레이드 및 복사 hello의 이름에 hello 저장소 컨테이너, hello 저장소 계정과의 hello 값 **key1**합니다. 이러한 값 tooNotepad 또는 일부 다른 임시 위치에 저장 합니다.  

## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

Visual Studio를 시작합니다. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다. .NET Core 콘솔 응용 프로그램을 만듭니다.

![새 프로젝트][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Hello 이벤트 허브 NuGet 패키지 추가

Hello 추가 [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 및 [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) 다음이 단계를 수행 하 여.NET 표준 라이브러리 NuGet 패키지 tooyour 프로젝트: 

1. Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.
2. Hello 클릭 **찾아보기** 누른 "Microsoft.Azure.EventHubs" 및 선택 hello에 대 한 검색 **Microsoft.Azure.EventHubs** 패키지 합니다. 클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.
3. 1과 2 단계를 반복 하 여 hello 설치 **Microsoft.Azure.EventHubs.Processor** 패키지 합니다.

## <a name="implement-hello-ieventprocessor-interface"></a>Hello IEventProcessor 인터페이스 구현

1. 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 프로젝트에서에서 클릭 **추가**, 클릭 하 고 **클래스**합니다. Hello 새 클래스 이름을 **SimpleEventProcessor**합니다.

2. Hello SimpleEventProcessor.cs 파일을 열고 hello 다음 추가 `using` hello 파일의 문 toohello 맨 위로 이동 합니다.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. 구현 hello `IEventProcessor` 인터페이스입니다. Hello의 전체 내용을 hello 대체 `SimpleEventProcessor` 코드 다음 hello 사용 하 여 클래스:

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Hello SimpleEventProcessor 클래스 tooreceive 메시지를 사용 하는 주 콘솔 메서드를 작성 합니다.

1. Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. 상수 toohello 추가 `Program` hello 이벤트 허브 연결 문자열, 이벤트 허브 이름, 저장소 계정 컨테이너 이름, 저장소 계정 이름과 저장소 계정 키에 대 한 클래스입니다. 코드 다음, 해당 값과 함께 hello 자리 표시자를 대체 하는 hello를 추가 합니다.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. 라는 새 메서드 추가 `MainAsync` toohello `Program` 클래스 다음과 같습니다.

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. 다음 줄의 코드 toohello hello 추가 `Main` 메서드:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Program.cs 파일은 다음과 같아야 합니다.

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.

축하합니다. 이벤트 프로세서 호스트 hello를 사용 하 여 이벤트 허브에서 메시지를 받은 있을 있습니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
