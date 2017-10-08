---
title: ".NET Framework hello aaaSend tooAzure 이벤트 허브 사용 하 여 이벤트 | Microsoft Docs"
description: ".NET Framework hello를 사용 하 여 tooEvent 허브 이벤트를 전송 합니다. 시작."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>.NET Framework hello를 사용 하 여 tooAzure 이벤트 허브 이벤트를 전송 합니다.

## <a name="introduction"></a>소개

이벤트 허브는 연결된 장치 및 응용 프로그램에서 많은 양의 이벤트 데이터(원격 분석)를 처리하는 서비스입니다. 이벤트 허브로 데이터를 수집한 후 저장소 클러스터를 사용 하 여 hello 데이터를 저장할 수도 있고 실시간 분석 공급자를 사용 하 여 변환할 수 있습니다. 이 대규모 이벤트 수집 및 처리 기능은 hello 인터넷 IoT (사물)를 포함 하 여 최신 응용 프로그램 아키텍처의 핵심 구성 요소입니다.

이 자습서에서는 어떻게 toouse hello [Azure 포털](https://portal.azure.com) toocreate 이벤트 허브입니다. 또한 toosend 이벤트 tooan 이벤트 허브로 작성 된 C# 사용 하 여 콘솔 응용 프로그램을 사용 하 여.NET Framework hello 하는 방법을 보여 줍니다. .NET Framework hello를 사용 하 여 tooreceive 이벤트 참조 hello [hello.NET Framework를 사용 하 여 이벤트를 수신](event-hubs-dotnet-framework-getstarted-receive-eph.md) , 문서 또는 hello hello 내용의 왼쪽 테이블에서 적절 한 받는 언어를 선택 합니다.

toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:

* [Microsoft Visual Studio 2015 이상](http://visualstudio.com). 이 자습서에서는 hello 스크린 샷 Visual Studio 2017을 사용합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs 네임스페이스 및 이벤트 허브 만들기

hello 첫 번째 단계는 toouse hello [Azure 포털](https://portal.azure.com) toocreate의 네임 스페이스는 이벤트 허브를 입력 하 고 hello toocommunicate hello 이벤트 허브 응용 프로그램에서 필요로 하는 관리 자격 증명을 가져옵니다. toocreate 네임 스페이스 및 이벤트 허브 hello 절차에 따라 [이 여기서](event-hubs-create.md), 다음 hello이이 자습서에서는 다음 단계를 진행 합니다.

## <a name="create-a-sender-console-application"></a>보낸 사람 콘솔 응용 프로그램 만들기

이 섹션에서는 이벤트 tooyour 이벤트 허브를 전송 하는 Windows 콘솔 앱을 작성 합니다.

1. Visual Studio에서 hello를 사용 하 여 새 Visual C# 데스크톱 앱 프로젝트를 만듭니다 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **보낸 사람**합니다.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **보낸 사람** 프로젝트를 마우스 클릭 **솔루션에 대 한 NuGet 패키지 관리**합니다. 
3. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 클릭 **설치**, hello 사용 약관을 수락 합니다. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio 다운로드, 설치 및 추가 참조 toohello [Azure 서비스 버스 라이브러리 NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus)합니다.
4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. 다음 필드 toohello hello 추가 **프로그램** 클래스를 이전에 저장 하는 hello 네임 스페이스 수준 연결 문자열 및 hello 이전 섹션에서 만든 hello 이벤트 허브 hello 이름의 hello 자리 표시자 값으로 대체 합니다.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  이 메서드는 200 ms 지연 된 이벤트 tooyour 이벤트 허브를 지속적으로 보냅니다.
7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Hello 프로그램을 실행 하 고 오류가 없는지 확인 하십시오.
  
축하합니다. 이제 메시지 tooan 이벤트 허브를 보냈을.

## <a name="next-steps"></a>다음 단계
이벤트 허브를 만들고 데이터를 전송 하는 작업 중인 응용 프로그램을 작성할 했으므로 toohello 다음 시나리오에서 이동할 수 있습니다.

* [이벤트 프로세서 호스트 hello를 사용 하 여 이벤트를 수신 합니다.](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [이벤트 프로세서 호스트 참조](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

