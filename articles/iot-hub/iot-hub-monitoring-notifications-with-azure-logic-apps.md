---
title: "aaaIoT 원격 모니터링 및 Azure 논리 앱을 사용 하 여 알림을 | Microsoft Docs"
description: "IoT hub 및 자동으로 IoT 온도 모니터링에 대 한 Azure 논리 앱을 사용 하 여 검색 하는 모든 예외에 대 한 전자 메일 알림을 tooyour 사서함을 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 모니터링, iot 알림, iot 온도 모니터링"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a>Azure Logic Apps으로 IoT Hub와 사서함을 연결하여 IoT 원격 모니터링 및 알림

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Azure 논리 앱 숨기는 일련의 단계로 tooautomate 프로세스입니다. 논리 앱은 다양한 서비스 및 프로토콜을 통해 연결할 수 있습니다. '계정이 추가되면' 같은 트리거로 시작하여 '푸시 알림 전송' 같은 작업 조합이 이어집니다. 이 기능 덕분에 Logic Apps은 다른 여러 사용 시나리오도 지원하지만 특히 이상을 지속적으로 감지할 수 있다는 점에서 IoT 모니터링을 위한 완벽한 IoT 솔루션입니다.

## <a name="what-you-learn"></a>학습 내용

배웁니다 어떻게 toocreate IoT hub 및 온도 모니터링 및 알림에 대 한 사서함을 연결 하는 논리 앱입니다. Hello 온도 30 C 위에 이면 hello 클라이언트 응용 프로그램 표시 `temperatureAlert = "true"` tooyour IoT hub hello 메시지에서 보냅니다. 트리거 논리 앱 toosend hello hello 메시지 전자 메일 알림을 있습니다.

## <a name="what-you-do"></a>수행할 작업

* 서비스 버스 네임 스페이스를 만들고 큐 tooit를 추가 합니다.
* 끝점 및 라우팅 규칙 tooyour IoT 허브를 추가 합니다.
* 논리 앱을 만들고, 구성하고, 테스트합니다.

## <a name="what-you-need"></a>필요한 항목

* 자습서 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료는 hello 요구 사항에 대해 설명 합니다.
  * 활성 Azure 구독.
  * 구독 중인 Azure IoT Hub
  * 메시지 tooyour Azure IoT 허브에서 전송 하는 클라이언트 응용 프로그램입니다.

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a>서비스 버스 네임 스페이스를 만들고 큐 tooit 추가

### <a name="create-a-service-bus-namespace"></a>Service Bus 네임스페이스 만들기

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **엔터프라이즈 통합** > **서비스 버스**합니다.
1. Hello 다음 정보를 제공 합니다.

   **이름**: hello 서비스 버스의 hello 이름입니다.

   **가격 책정 계층**: **기본** > **선택**을 클릭합니다. hello 기본 계층은이 자습서 충분 합니다.

   **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   **위치**: 동일 사용 하 여 hello IoT 허브를 사용 하는 위치입니다.
1. **만들기**를 클릭합니다.

   ![Hello Azure 포털에서에서 서비스 버스 네임 스페이스 만들기](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a>Service Bus 큐 추가

1. Hello 서비스 버스 네임 스페이스를 열고 클릭 **+ 큐**합니다.
1. Hello 큐에 대 한 이름을 입력 한 다음 클릭 **만들기**합니다.
1. Hello 서비스 버스 큐를 열고 클릭 **공유 액세스 정책을** > **+ 추가**합니다.
1. Hello 정책, 검사에 대 한 이름을 입력 **관리**, 클릭 하 고 **만들기**합니다.

   ![Hello Azure 포털에서에서 서비스 버스 큐 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a>끝점 및 라우팅 규칙 tooyour IoT hub 추가

### <a name="add-an-endpoint"></a>끝점 추가

1. IoT Hub를 열고 끝점 > + 추가를 클릭합니다.
1. Hello 다음 정보를 입력 합니다.

   **이름**: hello 끝점의 hello 이름입니다.

   **끝점 유형**: **Service Bus 큐**를 선택합니다.

   **서비스 버스 네임 스페이스**: 만든 hello 네임 스페이스를 선택 합니다.

   **서비스 버스 큐**: 만든 선택 hello 큐입니다.
1. **확인**을 클릭합니다.

   ![Hello Azure 포털에서에서 끝점 tooyour IoT hub 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a>라우팅 규칙 추가

1. IoT Hub에서 **경로** > **+ 추가**를 클릭합니다.
1. Hello 다음 정보를 입력 합니다.

   **이름**: hello 이름 hello 라우팅 규칙입니다.

   **데이터 원본**: **DeviceMessages**를 선택합니다.

   **끝점**: 만든 hello 끝점을 선택 합니다.

   **쿼리 문자열**: `temperatureAlert = "true"`를 입력합니다.
1. **Save**를 클릭합니다.

   ![Hello Azure 포털에에서는 라우팅 규칙 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a>논리 앱을 만들고 구성

### <a name="create-a-logic-app"></a>논리 앱 만들기

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **엔터프라이즈 통합** > **논리 앱**합니다.
1. Hello 다음 정보를 입력 합니다.

   **이름**: hello 논리 앱의 hello 이름입니다.

   **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   **위치**: 동일 사용 하 여 hello IoT 허브를 사용 하는 위치입니다.
1. **만들기**를 클릭합니다.

### <a name="configure-hello-logic-app"></a>Hello 논리 앱 구성

1. Hello 논리 앱 디자이너에 열립니다 hello 논리 앱을 엽니다.
1. 논리 앱 디자이너 hello 클릭 **빈 논리 앱**합니다.

   ![Hello Azure 포털에서에서 빈 논리 앱 시작](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. **Service Bus**를 클릭합니다.

   ![서비스 버스 toostart hello Azure 포털에서에서 논리 앱 만들기를 선택 합니다.](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. **Service Bus – 큐에 하나 이상의 메시지가 도착하는 경우(자동 완성)**를 클릭합니다.
1. Service Bus 연결을 만듭니다.
   1. 연결 이름을 입력합니다.
   1. 서비스 버스 네임 스페이스 hello 클릭 > 서비스 버스 정책 hello > **만들기**합니다.

      ![Hello Azure 포털에서에서 논리 앱에 대 한 서비스 버스 연결을 만들려면](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. 클릭 **계속** hello 서비스 버스 연결을 만들고 나면 합니다.
   1. 만든 hello 큐를 선택 하 고 입력 `175` 에 대 한 **최대 메시지 수**

      ![논리 앱에서 서비스 버스 연결 hello에 대 한 hello 최대 메시지 수를 지정 합니다.](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. "저장" 단추 toosave hello 변경 클릭 합니다.

1. SMTP 서비스 연결을 만듭니다.
   1. **다음 단계** > **작업 추가**를 클릭합니다.
   1. 형식 `SMTP`, hello 클릭 **SMTP** hello 검색 결과에서 서비스 마우스 클릭 **SMTP-전자 메일 보내기**합니다.

      ![Hello Azure 포털에서에서 논리 앱에 대 한 SMTP 연결 만들기](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. 사서함의 hello SMTP 정보를 입력 한 다음 클릭 **만들기**합니다.

      ![Hello Azure 포털에서에서 응용 프로그램 논리에서에서 SMTP 연결 정보를 입력 하세요.](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      에 대 한 SMTP hello 정보 [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), 및 [Yahoo 메일](https://help.yahoo.com/kb/SLN4075.html)합니다.
   1. **보내는 사람** 및 **받는 사람**의 전자 메일 주소를 입력하고, **제목** 및 **본문**에 `High temperature detected`를 입력합니다.
   1. **Save**를 클릭합니다.

저장할 때 hello 논리 앱 작업 순서로 표시 됩니다.

## <a name="test-hello-logic-app"></a>Hello 논리가 응용 프로그램 테스트

1. Tooyour 장치에 배포 하는 hello 클라이언트 응용 프로그램 시작 [연결 ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md)합니다.
1. 3. 30 위에 hello SensorTag toobe 주위 hello 환경 온도 증가 예를 들어 프로그램 SensorTag 주위 캔 들 밝은 색입니다.
1. Hello 논리 앱에서 보낸 전자 메일 알림을 받게 됩니다.

   > [!NOTE]
   > 전자 메일 서비스 공급자 tooverify hello 보낸 사람 identity toomake 인지 hello 전자 메일을 보내는 사용자 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

IoT Hub와 사서함을 연결하여 온도를 모니터링하고 알림을 보내는 논리 앱을 성공적으로 만들었습니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
