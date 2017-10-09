---
title: "aaaSave IoT hub tooAzure 데이터 저장소를 메시지 | Microsoft Docs"
description: "Azure 함수 앱 toosave IoT 허브 메시지 tooyour Azure 테이블 저장소를 사용 합니다. hello IoT 허브 메시지 IoT 장치에서 전송 된 센서 데이터가 같은 정보를 포함 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 데이터 저장소, IoT 센서 데이터 저장소"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a>센서 데이터 tooyour Azure 테이블 저장소를 포함 하는 IoT 허브 메시지 저장

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a>학습 내용

어떻게 toocreate Azure 저장소 계정 및 Azure 테이블 저장소에 앱 toostore IoT 허브 메시지 작동 방법을 배웁니다.

## <a name="what-you-do"></a>수행할 작업

- Azure 저장소 계정 만들기
- 연결 tooread 메시지가 IoT hub를 준비 합니다.
- Azure 함수 앱 만들기 및 배포

## <a name="what-you-need"></a>필요한 항목

- [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello 요구 사항:
  - 활성 Azure 구독
  - 구독 중인 IoT Hub 
  - 메시지 tooyour IoT 허브에서 전송 하는 실행 중인 응용 프로그램

## <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **저장소** > **저장소 계정**  >   **만들**합니다.

2. Hello hello 저장소 계정에 대 한 필요한 정보를 입력 합니다.

   ![Hello Azure 포털에서에서 저장소 계정 만들기](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * **이름**: hello hello 저장소 계정의 이름입니다. hello 이름은 전역적으로 고유 해야 합니다.

   * **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   * **Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.

3. **만들기**를 클릭합니다.

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a>연결 tooread 메시지가 IoT hub를 준비 합니다.

IoT 허브는 기본 제공 이벤트 허브 호환 끝점 tooenable 응용 프로그램 tooread IoT 허브 메시지를 표시합니다. 한편, 응용 프로그램에서 IoT hub 소비자 그룹 tooread 데이터를 사용합니다. IoT hub에서 Azure 함수 앱 tooread 데이터를 만들기 전에 다음 hello지 않습니다.

- IoT hub 끝점의 hello 연결 문자열을 가져옵니다.
- IoT Hub에 대한 소비자 그룹 만들기

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a>IoT hub 끝점의 hello 연결 문자열 가져오기

1. IoT Hub를 엽니다.

2. Hello에 **IoT Hub** 창 아래에서 **메시징**, 클릭 **끝점**합니다.

3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **기본 제공 끝점**, 클릭 **이벤트**합니다.

4. Hello에 **속성** 창에서 다음 값에 참고 hello:
   - Event Hub 호환 끝점
   - Event Hub 호환 이름

   ![IoT hub 끝점의 연결 문자열 hello hello Azure 포털에서 가져오기](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. Hello에 **IoT Hub** 창 아래에서 **설정**, 클릭 **공유 액세스 정책을**합니다.

6. **iothubowner**를 클릭합니다.

7. 참고 hello **기본 키** 값입니다.

8. IoT hub 끝점의 hello 연결 문자열을 다음과 같이 만듭니다.

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > 대체 `<Event Hub-compatible endpoint>` 및 `<Primary key>` hello 값이 앞에서 설명한 것입니다.

### <a name="create-a-consumer-group-for-your-iot-hub"></a>IoT Hub에 대한 소비자 그룹 만들기

1. IoT Hub를 엽니다.

2. Hello에 **IoT Hub** 창 아래에서 **메시징**, 클릭 **끝점**합니다.

3. Hello에서 마우스 오른쪽 단추로 창 아래에서 **기본 제공 끝점**, 클릭 **이벤트**합니다.

4. Hello에 **속성** 창 아래에서 **소비자 그룹**는 이름을 입력 한 다음 확인을 기록 합니다.

5. **Save**를 클릭합니다.

## <a name="create-and-deploy-an-azure-function-app"></a>Azure 함수 앱 만들기 및 배포

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **계산** > **함수 앱**  >   **만들**합니다.

2. Hello hello 함수 앱에 대 한 필요한 정보를 입력 합니다.

   ![Hello Azure 포털에서에서 함수 앱 만들기](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * **응용 프로그램 이름**: hello 이름 hello 함수 앱입니다. hello 이름은 전역적으로 고유 해야 합니다.

   * **리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.

   * **저장소 계정**: hello 만든 저장소 계정입니다.

   * **Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 toohello 함수 앱에 대 한이 옵션을 선택 합니다.

3. **만들기**를 클릭합니다.

4. Hello 함수 앱을 만든 후이 엽니다.

5. Hello 함수 응용 프로그램에서 hello 다음을 수행 하 여 새 함수를 만듭니다.

   a. **새 함수**를 클릭합니다.

   b. **언어**에서 **JavaScript**를 선택하고, **시나리오**에서 **데이터 처리**를 선택합니다.

   c. **이 함수 만들기**를 클릭한 다음, **새 함수**를 클릭합니다.

   d. 선택 **JavaScript** hello 언어에 대 한 및 **데이터 처리** hello 시나리오에 대 한 합니다.

   e. Hello 클릭 **EventHubTrigger JavaScript** 템플릿.

   f. Hello hello 서식 파일에 대 한 필요한 정보를 입력 합니다.

      * **함수 이름을**: hello hello 함수의 이름입니다.

      * **이벤트 허브 이름**: hello 이벤트 허브 호환 이름 앞에서 설명한 것입니다.

      * **이벤트 허브 연결**: 사용자가 만든 hello IoT hub 끝점의 tooadd hello 연결 문자열 클릭 **새로**합니다.

   g. **만들기**를 클릭합니다.

6. Hello 다음을 수행 하 여 hello 함수의 출력을 구성 합니다.

   a. **통합** > **새 출력** > **Azure Table Storage** > **선택**을 차례로 클릭합니다.

      ![테이블 저장소 tooyour 함수 앱 hello Azure 포털에 추가](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   b. Hello 필요한 정보를 입력 합니다.

      * **테이블 매개 변수 이름**: 사용 `outputTable`, Azure hello에 사용 되는 함수의 코드입니다.
      
      * **테이블 이름**: `deviceData`를 사용합니다.

      * **저장소 계정 연결**: **새로 만들기**를 클릭하고 저장소 계정을 선택하거나 입력합니다. Hello 저장소 계정이 표시 되지 않으면 참조 [저장소 계정 요구 사항](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)합니다.
      
   c. **Save**를 클릭합니다.

7. **트리거** 아래에서 **Azure Event Hub(eventHubMessages)**를 클릭합니다.

8. 아래 **이벤트 허브 소비자 그룹**를 생성 하 고 클릭 hello 소비자 그룹의 hello 이름을 입력 **저장**합니다.

9. 왼쪽 hello에 만든 hello 함수를 클릭 한 다음 클릭 **파일 보기** hello 오른쪽에 있습니다.

10. hello 코드 `index.js` hello 다음과 같이 합니다.

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. **Save**를 클릭합니다.

이제 hello 함수 응용 프로그램을 작성 했습니다. 이 앱은 IoT Hub에서 받는 메시지를 Table Storage에 저장합니다.

> [!NOTE]
> Hello를 사용할 수 있습니다 **실행** 단추 tootest hello 함수 앱. 클릭할 때 **실행**, hello 테스트 메시지를 tooyour IoT 허브를 보냅니다. hello 메시지의 도착 hello hello 함수 앱 toostart 트리거할 하 고 hello 메시지 tooyour 테이블 저장소를 저장 해야 합니다. hello **로그** 창 hello 프로세스의 hello 세부 정보를 기록 합니다.

## <a name="verify-your-message-in-your-table-storage"></a>테이블 저장소에 있는 메시지 확인

1. 장치 toosend 메시지 tooyour IoT 허브에서 hello 샘플 응용 프로그램을 실행 합니다.

2. [Azure Storage 탐색기를 다운로드하고 설치](http://storageexplorer.com/)합니다.

3. 저장소 탐색기를 열고 **Azure 계정 추가** > **로그인**, tooyour Azure 계정에에서 로그인 합니다.

4. Azure 구독 > **저장소 계정** > 저장소 계정 > **테이블** > **deviceData**를 차례로 클릭합니다.

   Hello에 기록 하 여 장치 tooyour IoT 허브에서 보낸 메시지를 표시 되어야 `deviceData` 테이블입니다.

## <a name="next-steps"></a>다음 단계

Azure Storage 계정과 Azure 함수 앱을 만들어 IoT Hub에서 받는 메시지를 Table Storage에 저장하도록 했습니다.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
