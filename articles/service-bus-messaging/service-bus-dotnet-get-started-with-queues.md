---
title: "Azure 서비스 버스 큐 aaaGet 시작 | Microsoft Docs"
description: "Service Bus 메시징 큐를 사용하는 C# 콘솔 응용 프로그램을 작성합니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Service Bus 큐 시작
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>수행될 작업
이 자습서에서는 hello 다음 단계를 설명 합니다.

1. Hello Azure 포털을 사용 하 여 서비스 버스 네임 스페이스를 만듭니다.
2. Hello Azure 포털을 사용 하 여 서비스 버스 큐를 만듭니다.
3. 콘솔 응용 프로그램 toosend 메시지를 기록 합니다.
4. 콘솔 응용 프로그램 tooreceive hello hello 이전 단계에서 전송 된 메시지를 작성 합니다.

## <a name="prerequisites"></a>필수 조건
1. [Visual Studio 2015 이상](http://www.visualstudio.com). 이 자습서의 hello 예제에서는 Visual Studio 2017를 사용 합니다.
2. Azure 구독.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure 포털을 사용 하 여 네임 스페이스 만들기
서비스 버스 메시징 네임 스페이스를 이미 만든 경우 점프 toohello [hello Azure 포털을 사용 하 여 큐를 만들](#2-create-a-queue-using-the-azure-portal) 섹션.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Hello Azure 포털을 사용 하 여 큐 만들기
이미 서비스 버스 큐를 만든 경우 점프 toohello [송신 메시지 toohello 큐](#3-send-messages-to-the-queue) 섹션.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. 송신 메시지 toohello 큐
Visual Studio를 사용 하 여 C# 콘솔 응용 프로그램을 작성 했습니다 toosend 메시지 toohello 큐

### <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

Visual Studio를 시작하고 **콘솔 앱(.NET Framework)** 프로젝트를 만듭니다.

### <a name="add-hello-service-bus-nuget-package"></a>Hello Service Bus NuGet 패키지를 추가 합니다.
1. Hello 새로 만든 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.
2. Hello 클릭 **찾아보기** 탭에서 검색할 **Microsoft Azure 서비스 버스**를 선택한 후 hello **WindowsAzure.ServiceBus** 항목입니다. 클릭 **설치** toocomplete hello 설치의 경우 다음이 대화 상자를 닫습니다.
   
    ![NuGet 패키지 선택][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>일부 코드 toosend 메시지 toohello 큐 쓰기
1. Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. 다음 코드 toohello hello 추가 `Main` 메서드. 집합 hello `connectionString` 변수 toohello 연결 문자열 hello 네임 스페이스를 만들 때 가져온 마우스 설정 `queueName` hello 큐를 만들 때 사용한 toohello 큐 이름입니다.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs 파일은 다음과 같아야 합니다.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Hello 프로그램을 실행 하 고 Azure 포털 hello 확인: hello 네임 스페이스에 큐의 hello 이름을 클릭 **개요** 블레이드입니다. hello 큐 **Essentials** 블레이드가 표시 됩니다. 해당 hello 확인 **근무 중인 메시지 수** 값은 이제 1 여야 합니다. Hello 메시지를 검색 하지 않고 hello 보낸 사람 응용 프로그램을 실행할 때마다가이 값 1 씩 증가 합니다. 또한 참고 hello hello queue의 현재 크기 증가 각 시간 hello 응용 프로그램을 메시지 toohello 큐를 추가 합니다.
   
      ![메시지 크기][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Hello 큐에서 메시지를 수신 합니다.

1. 방금 전송 받은 tooreceive hello 메시지 새 콘솔 응용 프로그램을 만들고 유사한 toohello 이전 보낸 사람 응용 프로그램 참조 toohello Service Bus NuGet 패키지를 추가 합니다.
2. Hello 다음 추가 `using` hello Program.cs 파일의 문 toohello 맨 위로 이동 합니다.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. 다음 코드 toohello hello 추가 `Main` 메서드. 집합 hello `connectionString` hello 네임 스페이스를 만들 때를 설정 하는 변수 toohello 연결 문자열 `queueName` hello 큐를 만들 때 사용한 toohello 큐 이름입니다.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs 파일은 다음과 같아야 합니다.
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Hello 프로그램을 실행 하 고 hello 포털을 다시 확인 합니다. 해당 hello 확인 **근무 중인 메시지 수** 및 **현재** 값은 이제 0입니다.
   
    ![큐 길이][queue-message-receive]

축하합니다. 이제 큐를 만들고 메시지를 보내고 메시지를 받았습니다.

## <a name="next-steps"></a>다음 단계

체크 아웃 우리의 [샘플 GitHub 리포지토리](https://github.com/Azure/azure-service-bus/tree/master/samples) hello 보다 고급 서비스 버스 메시징 기능 중 일부를 보여 주는 합니다.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
