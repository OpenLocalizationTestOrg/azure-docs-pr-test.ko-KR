---
title: "aaaAzure IoT Suite 및 논리 앱 | Microsoft Docs"
description: "방법에 대 한 자습서 toohook 비즈니스 프로세스에 대 한 논리 앱 tooAzure IoT Suite를 구성 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>자습서: 논리 앱 tooyour Azure IoT Suite 원격 모니터링 미리 구성 된 솔루션에 연결
hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] 원격 모니터링 미리 구성 된 솔루션은 훌륭한 방법 tooget 사용을 빠르게 시작할 IoT 솔루션은 예는 종단 간 기능 집합입니다. 이 자습서에서는 tooadd 논리 앱 tooyour Microsoft Azure IoT Suite 원격 모니터링 솔루션 미리 방법을 구성 합니다. 이러한 단계를 보여 줍니다 tooa 비즈니스 프로세스를 연결 하 여 더욱 해소 하면 IoT 솔루션 취할 수 있습니다.

*원격 모니터링 tooprovision 미리 솔루션을 구성 하는 방법을 보여주는 연습은 찾고 있는 경우 참조 [자습서: hello 미리 구성 된 IoT 솔루션 시작][lnk-getstarted]합니다.*

이 자습서를 시작하기 전에 먼저 다음을 수행해야 합니다.

* 프로 비전 hello 원격 Azure 구독에서 미리 구성 된 솔루션을 모니터링 합니다.
* SendGrid 계정 tooenable 만들기 toosend 비즈니스 프로세스를 트리거하는 전자 메일입니다. [SendGrid](https://sendgrid.com/) 에서 **무료 평가판**을 클릭하여 무료 평가판 계정을 등록할 수 있습니다. Toocreate 무료 평가판 계정을 등록 한 후 해야는 [API 키](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) 에서 SendGrid toosend 메일 사용 권한을 부여 합니다. Hello 자습서의 뒷부분에서이 API 키가 필요 합니다.

toocomplete이이 자습서에서는 Visual Studio 2015 또는 Visual Studio 2017 toomodify hello 동작 hello 미리 구성 된 솔루션에 대 한 백 엔드에 필요 합니다.

Hello에서 해당 솔루션에 대 한 toohello 리소스 그룹을 이동 하 여 미리 구성 된 솔루션을 원격 모니터링 이미 배포 된 것으로 가정 [Azure 포털][lnk-azureportal]합니다. hello 리소스 그룹에 hello hello 솔루션 이름을 동일 이름을 원격 모니터링 솔루션 프로 비전 할 때 선택 했습니다. Hello 리소스 그룹에서 모든 hello hello hello Azure 클래식 포털에서에서 찾을 수 있는 Azure Active Directory 응용 프로그램을 제외 하 고 솔루션에 대 한 Azure 리소스를 프로 비전을 볼 수 있습니다. hello 다음 스크린 샷에서 예가 나와 **리소스 그룹** 블레이드 원격 모니터링에 대 한 미리 솔루션 구성:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, hello로 hello 논리 앱 toouse 설정 솔루션을 미리 구성 합니다.

## <a name="set-up-hello-logic-app"></a>논리 앱 hello 설정
1. 클릭 **추가** hello Azure 포털에서에서 리소스 그룹 블레이드의 hello 위쪽에 있습니다.
2. **Logic App**을 검색하여 선택한 후 **만들기**를 클릭합니다.
3. Hello 채울 **이름** 동일 사용 하 여 hello 및 **구독** 및 **리소스 그룹** 원격 모니터링 솔루션을 프로 비전 할 때 사용 하 합니다. **만들기**를 클릭합니다.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. 배포 완료 되 면 리소스 그룹에서 논리 앱 나열 된 hello 자원으로 볼 수 있습니다.
5. Hello 논리 앱 toonavigate toohello 논리 앱 블레이드, 선택 hello 클릭 **빈 논리 앱** 템플릿 tooopen hello **논리 앱 디자이너**합니다.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. **요청**을 선택합니다. 이 작업은 특정 JSON 형식 페이로드와 함께 들어오는 HTTP 요청이 트리거로 작동하도록 지정합니다.
7. Hello를 hello 요청 본문이 JSON 스키마에 코드를 다음에 붙여 넣습니다.
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > Hello 논리 앱을 저장 한 후 작업을 추가 해야 하는 먼저 hello HTTP post에 대 한 hello URL을 복사할 수 있습니다.
   > 
   > 
8. 수동 트리거 아래에서 **+ 새 단계**를 클릭합니다. 그런 다음 **작업 추가**를 클릭합니다.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. **SendGrid - 메일 보내기** 를 검색하여 클릭합니다.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. 같은 hello 연결에 대 한 이름을 입력 **SendGridConnection**, hello 입력 **SendGrid API 키** SendGrid 계정을 설정 하 고 클릭 때 만든 **만들기**합니다.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. 전자 메일 주소 자체 tooboth hello 추가 **에서** 및 **를** 필드입니다. 추가 **원격 모니터링 경고 [DeviceId]** toohello **주체** 필드입니다. Hello에 **전자 메일 본문** 필드에서 추가 **장치 [DeviceId]에서 [measurementName] [measuredValue] 값으로 보고 합니다.** 추가할 수 있습니다 **[DeviceId]**, **[measurementName]**, 및 **[measuredValue]** hello에서 클릭 하 여 **이전단계에서데이터를삽입할수**섹션.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. 클릭 **저장** hello 최상위 메뉴에 있습니다.
13. Hello 클릭 **요청** 트리거와 복사 hello **Http Post toothis URL** 값입니다. 이 URL은 자습서의 뒷부분에서 필요합니다.

> [!NOTE]
> 논리 앱 사용 toorun [다양 한 유형의 작업] [ lnk-logic-apps-actions] Office 365의 동작을 포함 합니다. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Hello EventProcessor 웹 작업 설정
이 섹션에서는 미리 구성 된 솔루션 toohello 만든 논리 앱에 연결할 수 있습니다. toocomplete hello URL tootrigger hello 논리 앱 toohello 동작 장치 센서 값 임계값을 초과할 때 발생 하는 추가이 작업을 합니다.

1. Git 클라이언트 tooclone hello 최신 버전의 hello 사용 하 여 [azure iot-원격 액세스 모니터링 github 리포지토리][lnk-rmgithub]합니다. 예:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. Visual Studio에서 열고 hello **RemoteMonitoring.sln** hello hello 저장소의 로컬 복사본에서 합니다.
3. 열기 hello **ActionRepository.cs** hello에 대 한 파일 **인프라\\리포지토리** 폴더입니다.
4. 업데이트 hello **actionIds** hello 사용 하 여 사전 **Http Post toothis URL** 논리 앱에서 다음과 같이 설명 합니다.
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. 솔루션의 hello 변경 내용을 저장 하 고 Visual Studio를 종료 합니다.

## <a name="deploy-from-hello-command-line"></a>Hello 명령줄에서 배포
이 섹션에서는 hello 원격 모니터링 솔루션 tooreplace hello 버전의 Azure에서 현재 실행 중인 업데이트 된 버전을 배포 합니다.

1. Hello 다음 [개발자 설치] [ lnk-devsetup] 환 결 배포에 대 한 지침 tooset 합니다.
2. toodeploy를 로컬로 수행 hello [로컬 배포] [ lnk-localdeploy] 지시 합니다.
3. toodeploy toohello 고 클라우드를 기존 클라우드 배포 업데이트 hello에 따라 [배포 클라우드] [ lnk-clouddeploy] 지시 합니다. 원래 배포의 hello 이름을 hello 배포 이름으로 사용 합니다. 예를 들어 hello 원래 배포가 호출 되 면 **demologicapp**, hello 다음 명령을 사용 하 여:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   Hello 스크립트 실행을 구축 해야 toouse hello 동일한 Azure 계정, 구독, 지역 및 Active Directory 인스턴스에서 hello 솔루션을 프로 비전 할 때 사용 합니다.

## <a name="see-your-logic-app-in-action"></a>작업에서 논리 앱 참조
hello 원격 미리 구성 된 솔루션을 모니터링 하는 솔루션을 프로 비전 할 때 기본적으로 설정 하는 두 개의 규칙에 있습니다. 두 규칙은 hello에 **SampleDevice001** 장치:

* 온도 > 38.00
* 습도 > 48.00

hello 온도 규칙이 hello 트리거합니다 **경보 발생** 작업과 hello 습도 규칙 트리거합니다 hello **SendMessage** 동작 합니다. 두 작업 hello에 대 한 동일한 URL hello 사용한 가정 **ActionRepository** 어느 한쪽의 규칙에 대 한 논리 앱 트리거에 클래스입니다. 규칙이 모두 사용 하 여 SendGrid toosend 메일 toohello **를** hello 경고의 세부 정보와 함께 주소입니다.

> [!NOTE]
> 논리 앱 hello hello 임계값이 충족 될 때마다 tootrigger를 계속 합니다. tooavoid 불필요 한 전자 메일을 비활성화 하거나 hello 규칙에서 사용자 솔루션 포털 또는 사용 안 함 논리 앱에에서 hello hello [Azure 포털][lnk-azureportal]합니다.
> 
> 

또한 tooreceiving 전자 메일을 볼 수도 있습니다 hello 논리 앱 hello 포털에서 실행 될 때:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>다음 단계
논리 앱 tooconnect hello 미리 구성 된 솔루션 tooa 비즈니스 프로세스를 사용한 이제 hello 미리 구성 된 솔루션을 사용자 지정 하기 위한 hello 옵션에 대 한 보다 자세히 배울 수 있습니다.

* [동적 원격 분석을 사용 하 여 원격 미리 구성 된 솔루션을 모니터링 하는 hello로][lnk-dynamic]
* [Hello 원격 모니터링 미리 구성 된 솔루션에서에서 장치 정보 메타 데이터][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
