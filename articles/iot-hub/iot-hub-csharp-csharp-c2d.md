---
title: "aaaCloud-장치 메시지와 Azure IoT 허브 (.NET) | Microsoft Docs"
description: "어떻게 toosend 클라우드-장치 메시지 tooa 장치 hello Azure IoT Sdk를 사용 하 여.NET 용 Azure IoT 허브에서 설정 합니다. 장치 앱 tooreceive 클라우드-장치 메시지를 수정 하 고 백 엔드 응용 프로그램 toosend hello 클라우드-장치 메시지를 수정 합니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Hello 클라우드 tooyour 장치 IoT 허브 (.NET)와에서 메시지를 전송
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>소개
Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다. hello [IoT 허브 시작] toocreate IoT hub, 장치 id를 프로 비전 하 고 장치-클라우드 메시지를 보내는 장치 앱을 코딩 하는 방법을 보여 주는 자습서입니다.

이 자습서는 [IoT 허브 시작]를 토대로 작성되었습니다. 이 항목에서는 다음 방법을 설명합니다.

* 솔루션 백 엔드에서 IoT 허브를 통해 tooa 단일 장치를 클라우드-장치 메시지를 보냅니다.
* 장치에서 클라우드-장치 메시지를 받습니다.
* 솔루션 백 엔드에서 배달 확인 요청 (*피드백*) IoT 허브에서 메시지 보내는 tooa 장치에 대 한 합니다.

Hello에서 클라우드-장치 메시지에서 자세한 정보를 찾을 수 있습니다 [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.

이 자습서의 hello 끝에 두 개의.NET 콘솔 응용 프로그램 실행합니다.

* **SimulatedDevice**, 수정 된 버전에서 만든 hello 앱의 [IoT 허브 시작], tooyour IoT 허브를 연결 하 고 클라우드-장치 메시지를 수신 합니다.
* **SendCloudToDevice**는 IoT 허브를 통해 클라우드-장치 메시지 toohello 장치 앱을 보내고 해당 배달 승인을 받습니다.

> [!NOTE]
> IoT Hub는 [Azure IoT 장치 SDK]를 통해 많은 장치 플랫폼 및 언어(C, Java 및 Javascript 포함)를 지원합니다. 에 대 한 단계별 지침은 tooconnect 장치 toothis 자습서의 코드 및 일반적으로 tooAzure IoT Hub를 확인 하려면 어떻게 hello [IoT 허브 개발자 가이드]합니다.
> 
> 

toocomplete이이 자습서에서는 다음 hello 필요:

* Visual Studio 2015 또는 Visual Studio 2017
* 활성 Azure 계정. 계정이 없는 경우 몇 분 안에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

## <a name="receive-messages-in-hello-device-app"></a>Hello 장치 응용 프로그램에서 메시지를 수신 합니다.
이 섹션에서는 수정 하면서 간단한 hello 장치 응용 프로그램에서 만든 [IoT 허브 시작] hello IoT hub에서 클라우드-장치 메시지 tooreceive 합니다.

1. Hello에 Visual Studio에서 **SimulatedDevice** 프로젝트에서 다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    hello `ReceiveAsync` 메서드 hello 장치 수신한 hello 시 hello 받은 메시지를 비동기적으로 반환 합니다. 반환 *null* 가능한 제한 시간 후 (이 경우 hello 기본값인 1 분이 사용 됨). Hello 앱을 받을 때는 *null*, toowait 새 메시지에 대 한 이벤트를 계속 합니다. 이 요구 사항은 hello에 대 한 hello 이유 `if (receivedMessage == null) continue` 선입니다.
   
    호출을 너무 hello`CompleteAsync()` hello 메시지를 성공적으로 처리 된 IoT Hub에 알립니다. hello 장치 큐에서 hello 메시지를 안전 하 게 제거할 수 있습니다. Hello hello 메시지 처리를 완료 합니다. 이러한 오류로 hello 장치 앱 무슨 일 경우 IoT Hub 전달 다시 합니다. 해당 메시지 처리 논리 hello 장치 응용 프로그램에는 중요 한 *idempotent*동일한 결과 hello 동일한 메시지를 여러 번 생성 hello 수신 되도록 합니다. 응용 프로그램 hello 메시지 나중에 사용 하기 위해 hello 큐에 그대로 유지 하 고 IoT 허브는 메시지를 일시적으로 중단 수 합니다. 또는 hello 응용 프로그램에는 hello 메시지 hello 큐에서 영구적으로 제거 하는 메시지가 거부 될 수 있습니다. 클라우드-장치 메시지 수명 주기 hello에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.
   
   > [!NOTE]
   > HTTP 대신 MQTT 또는 AMQP를 전송으로를 사용할 때는 hello `ReceiveAsync` 메서드가 즉시 반환 합니다. 클라우드-장치 메시지를 HTTP 지원 hello 패턴은 메시지 자주 (25 분 마다 미만)에 대 한 확인 하는 간헐적으로 연결 된 장치입니다. 더 많은 HTTP 발급 제한 hello 요청 IoT 허브에서에서 결과 받습니다. Hello 차이 MQTT, AMQP 및 HTTP 지원 및 IoT Hub 제한에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.
   > 
   > 
2. Hello hello에서 메서드를 다음 추가 **Main** hello 바로 앞의 메서드 `Console.ReadLine()` 줄:
   
        ReceiveC2dAsync();

> [!NOTE]
> 간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.
> 
> 

## <a name="send-a-cloud-to-device-message"></a>클라우드-장치 메시지 보내기
이 섹션에서는 클라우드-장치 메시지 toohello 장치 응용 프로그램에서 전송 하 여.NET 콘솔 응용 프로그램을 작성할 수 있습니다.

1. Hello 현재 Visual Studio 솔루션의 hello를 사용 하 여 Visual C# 데스크톱 응용 프로그램 프로젝트를 만들 **콘솔 응용 프로그램** 서식 파일 프로젝트. 이름 hello 프로젝트 **SendCloudToDevice**합니다.
   
    ![Visual Studio의 새 프로젝트][20]
2. 솔루션 탐색기에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션에 대 한 NuGet 패키지 관리...** . 
   
    Hello 열립니다 **NuGet 패키지 관리** 창.
3. 검색할 **Microsoft.Azure.Devices**, 클릭 **설치**, hello 사용 약관을 수락 합니다. 
   
    이 다운로드, 설치 하 여 추가 참조 toohello [Azure IoT 서비스 SDK NuGet 패키지]합니다.

4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices;
5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. 대체 된 hello IoT 허브 연결 문자열에서 자리 표시자 값 hello [IoT 허브 시작]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    이 메서드는 전송 hello ID 사용 하 여 새 클라우드-장치 메시지 toohello 장치 `myFirstDevice`합니다. 사용 되는 hello에서 수정 하는 경우에이 매개 변수를 변경 [IoT 허브 시작]합니다.
7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. Visual Studio 내에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정...**을 선택합니다. 선택 **여러 개의 시작 프로젝트**을 선택한 후 hello **시작** 에 대 한 작업 **ReadDeviceToCloudMessages**, **SimulatedDevice**, 및 **SendCloudToDevice**합니다.
9. **F5**키를 누릅니다. 세 응용 프로그램이 모두 시작됩니다. 선택 hello **SendCloudToDevice** 창과 키를 눌러 **Enter**합니다. Hello 장치 응용 프로그램에서 수신 되는 hello 메시지를 표시 되어야 합니다.
   
   ![앱 메시지 수신][21]

## <a name="receive-delivery-feedback"></a>배달 피드백 받기
각 클라우드-장치 메시지에 대 한 IoT 허브에서의 가능한 toorequest 배달 (또는 만료) 승인을 이며합니다 이 옵션 사용 hello 솔루션 백 엔드 tooeasily 다시 시도 또는 보정 논리를 게 알립니다. 클라우드-장치 피드백에 대 한 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][IoT Hub developer guide - C2D]합니다.

Hello이이 섹션에서 수정 **SendCloudToDevice** 앱 toorequest 사용자 의견 및 IoT 허브에서 수신 합니다.

1. Hello에 Visual Studio에서 **SendCloudToDevice** 프로젝트에서 다음 메서드 toohello hello 추가 **프로그램** 클래스입니다.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    이 수신 패턴 hello 장치 응용 프로그램에서 같은 하나의 사용 되는 tooreceive 클라우드-장치 메시지 hello는 참고 합니다.
2. Hello hello에서 메서드를 다음 추가 **Main** hello 바로 뒤의 메서드 `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` 줄:
   
        ReceiveFeedbackAsync();
3. 클라우드-장치 메시지 배달이 hello에 대 한 피드백 toorequest toospecify 속성에에서 있는 hello **SendCloudToDeviceMessageAsync** 메서드. 다음 줄을 시작 오른쪽 hello 후 hello 추가 `var commandMessage = new Message(...);` 줄:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. 키를 눌러 앱을 hello 실행 **F5**합니다. 세 응용 프로그램이 모두 시작됩니다. 선택 hello **SendCloudToDevice** 창과 키를 눌러 **Enter**합니다. 표시 되어야 하 고 몇 초 후 hello 장치 응용 프로그램에서 수신 메시지를 환영 피드백 메시지가 수신 된 hello 프로그램 **SendCloudToDevice** 응용 프로그램입니다.
   
   ![앱 메시지 수신][22]

> [!NOTE]
> 간단히 하기 위해 이 자습서에서는 재시도 정책을 구현하지 않습니다. 프로덕션 코드에 다시 시도 정책 (예: 지 수 형식의 백오프) hello MSDN 문서에 설명 된 대로 구현 해야 [일시적인 오류 처리]합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
이 자습서에서는 방법에 대해 배웠습니다 toosend 및 클라우드-장치 메시지를 수신 합니다. 

IoT 허브를 사용 하는 완벽 한 종단 간 솔루션의 toosee 예 참조 [Azure IoT Suite]합니다.

IoT 허브를 사용 하 여 솔루션 개발에 대 한 더 toolearn 참조 hello [IoT 허브 개발자 가이드]합니다.

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT 서비스 SDK NuGet 패키지]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[일시적인 오류 처리]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[IoT 허브 개발자 가이드]: iot-hub-devguide.md
[IoT 허브 시작]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IoT 장치 SDK]: iot-hub-devguide-sdks.md