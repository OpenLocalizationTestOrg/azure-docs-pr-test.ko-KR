---
title: "서식 파일 (PowerShell)을 사용 하 여 Azure IoT Hub aaaCreate | Microsoft Docs"
description: "어떻게 toouse Azure 리소스 관리자 템플릿 toocreate IoT Hub PowerShell 사용 합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Azure Resource Manager 템플릿을 사용하여 IoT Hub 만들기(PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Toocreate Azure 리소스 관리자를 사용 하 고 Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다. 이 자습서에서는 Azure 리소스 관리자 템플릿 toocreate powershell IoT hub toouse 합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다. 이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. <br/>계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.
* [Azure PowerShell 1.0][lnk-powershell-install] 이상.

> [!TIP]
> hello 문서 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와] [ lnk-powershell-arm] 방법에 대 한 자세한 정보를 제공 toouse PowerShell 및 Azure 리소스 관리자 템플릿 toocreate Azure 리소스입니다.

## <a name="connect-tooyour-azure-subscription"></a>Tooyour Azure 구독 연결

PowerShell 명령 프롬프트에 hello 명령 toosign tooyour Azure 구독에서에서 다음을 입력 합니다.

```powershell
Login-AzureRmAccount
```

TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 구독. 다음 명령을 toolist hello 있습니다 사용할 수 있는 Azure 구독 toouse hello를 사용 합니다.

```powershell
Get-AzureRMSubscription
```

다음 명령은 tooselect 구독 toouse toorun hello 명령을 toocreate IoT 허브를 지정 하는 hello를 사용 합니다. Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

Hello 명령을 toodiscover 있는 IoT hub에 배포할 수 있으며 hello 현재 지원 되는 API 버전에 따라 사용할 수 있습니다.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

리소스 그룹 toocontain hello 다음 IoT 허브에 대 한 지원 hello 위치 중 하나에서 명령을 사용 하 여 IoT 허브를 만듭니다. 이 예에서는 **MyIoTRG1**이라는 리소스 그룹을 만듭니다.

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>서식 파일 toocreate IoT hub를 제출 합니다.

리소스 그룹에는 JSON 템플릿을 toocreate IoT 허브를 사용 합니다. Azure 리소스 관리자 템플릿 toomake 변경 tooan 기존 IoT hub를 사용할 수 있습니다.

1. Azure 리소스 관리자 템플릿 이라는 텍스트 편집기 toocreate를 사용 하 여 **template.json** 와 hello 리소스 정의 toocreate 다음 새 표준 IoT 허브입니다. Hello에 hello IoT 허브를 추가 하는이 예제 **미국 동부** 영역, 두 개의 소비자 그룹을 만듭니다 (**cg1** 및 **cg2**) hello 호환 이벤트 허브 끝점을 사용 하 여 hello **2016-02-03** API 버전입니다. 이 템플릿은으로 기대 toopass hello IoT 허브 이름에 호출을 매개 변수로 **hubName**합니다. Hello 현재 목록이 IoT Hub를 지 원하는 위치에 대 한 참조 [Azure 상태][lnk-status]합니다.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. 로컬 컴퓨터의 hello Azure 리소스 관리자 템플릿 파일을 저장 합니다. 이 예제에서는 **c:\templates** 폴더에 저장하는 것으로 가정합니다.

3. 다음 명령 toodeploy hello IoT 허브의 hello 이름을 매개 변수로 전달 새 IoT 허브를 실행 합니다. 이 예제에서는 hello hello IoT hub 이름이 `abcmyiothub`합니다. IoT hub의 hello 이름 전역적으로 고유 해야 합니다.

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. hello 출력 만든 hello IoT 허브에 대 한 hello 키 표시 됩니다.

5. 응용 프로그램이 추가 tooverify hello 새 IoT 허브를 방문 hello [Azure 포털] [ lnk-azure-portal] 및 리소스 목록을 표시 합니다. 또는 hello를 사용 하 여 **Get AzureRmResource** PowerShell cmdlet.

> [!NOTE]
> 이 예제 응용 프로그램은 대금이 청구되는 S1 표준 IoT Hub를 추가합니다. Hello 통해 hello IoT 허브를 삭제할 수 있습니다 [Azure 포털] [ lnk-azure-portal] 또는 hello를 사용 하 여 **제거 AzureRmResource** 했으면 PowerShell cmdlet.

## <a name="next-steps"></a>다음 단계

PowerShell과 함께 Azure 리소스 관리자 템플릿을 사용 하 여 IoT hub를 배포한 이제 tooexplore 더 이상 사용할 수 있습니다.

* Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.
* 읽기 [Azure 리소스 관리자 개요] [ lnk-azure-rm-overview] toolearn hello Azure 리소스 관리자의 기능에 대 한 자세한 합니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.

* [소개 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
