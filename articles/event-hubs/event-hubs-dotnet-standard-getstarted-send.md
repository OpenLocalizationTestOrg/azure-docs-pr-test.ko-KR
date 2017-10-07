---
title: "이벤트 허브 표준.NET을 사용 하 여 aaaSend 이벤트 tooAzure | Microsoft Docs"
description: "표준.NET의 이벤트를 tooEvent 허브 전송 시작"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>표준.NET에서 tooAzure 이벤트 허브 메시지를 보내기 시작.

> [!NOTE]
> 이 샘플은 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)에서 사용할 수 있습니다.

이 자습서에서는 toowrite 세트를 전송 하는.NET Core 콘솔 응용 프로그램 tooan 이벤트 허브를 메시지 하는 방법을 보여 줍니다. Hello를 실행할 수 있습니다 [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) 솔루션으로-, 대체 hello `EhConnectionString` 및 `EhEntityPath` 이벤트 허브 값이 포함 된 문자열입니다. 참고할 수 또는 hello에서에서 단계를이 자습서 toocreate 직접 합니다.

## <a name="prerequisites"></a>필수 조건

* [Microsoft Visual Studio 2015 또는 2017](http://www.visualstudio.com). hello의에서 예제가 자습서에서는 Visual Studio 2017 하지만 Visual Studio 2015 에서도 지원 됩니다.
* [.NET Core Visual Studio 2015 또는 2017 도구](http://www.microsoft.com/net/core).
* Azure 구독.
* 이벤트 허브 네임스페이스

toosend 메시지 tooan 이벤트 허브 toowrite Visual Studio는 C# 콘솔 응용 프로그램을 사용 합니다.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs 네임스페이스 및 이벤트 허브 만들기

hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate hello 이벤트 허브 유형에 대 한 네임 스페이스 및 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다. toocreate 네임 스페이스 및 이벤트 허브 절차에 따라 hello에 [이 여기서](event-hubs-create.md), 다음 단계를 수행 하는 hello 진행 합니다.

## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

Visual Studio를 시작합니다. Hello에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다. .NET Core 콘솔 응용 프로그램을 만듭니다.

![새 프로젝트][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Hello 이벤트 허브 NuGet 패키지 추가

Hello 추가 [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) 다음이 단계를 수행 하 여.NET 표준 라이브러리 NuGet 패키지 tooyour 프로젝트: 

1. Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.
2. Hello 클릭 **찾아보기** 누른 "Microsoft.Azure.EventHubs" 및 선택 hello에 대 한 검색 **Microsoft.Azure.EventHubs** 패키지 합니다. 클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>일부 코드 toosend 메시지 toohello 이벤트 허브를 작성 합니다.

1. Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. 상수 toohello 추가 `Program` hello 이벤트 허브 연결 문자열 및 엔터티 경로 (개별 이벤트 허브 이름)에 대 한 클래스입니다. Hello 적절 한 값을 hello 이벤트 허브를 만들 때 대괄호의 hello 자리 표시자를 바꿉니다.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. 라는 새 메서드 추가 `MainAsync` toohello `Program` 클래스 다음과 같습니다.

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. 라는 새 메서드 추가 `SendMessagesToEventHub` toohello `Program` 클래스 다음과 같습니다.

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. 다음 코드 toohello hello 추가 `Main` hello에 대 한 메서드 `Program` 클래스입니다.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Program.cs는 다음과 같아야 합니다.

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.

축하합니다. 이제 메시지 tooan 이벤트 허브를 보냈을.

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [Event Hubs에서 이벤트 수신](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
