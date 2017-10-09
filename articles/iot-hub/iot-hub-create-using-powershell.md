---
title: "PowerShell cmdlet을 사용 하 여 Azure IoT Hub aaaCreate | Microsoft Docs"
description: "어떻게 toouse PowerShell cmdlet toocreate IoT hub 합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>새로 만들기-AzureRmIotHub hello cmdlet을 사용 하 여 IoT 허브를 만듭니다.

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>소개

Azure PowerShell cmdlet toocreate를 사용 하 고 Azure IoT hub를 관리할 수 있습니다. 이 자습서에서는 PowerShell과 함께 IoT hub toocreate 합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다. 이 문서에서는 hello Azure 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. <br/>계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.
* [Azure PowerShell cmdlet][lnk-powershell-install]

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

## <a name="create-resource-group"></a>리소스 그룹 만들기

리소스 그룹 toodeploy IoT hub 필요합니다. 기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.

다음 명령은 toodiscover hello 위치 IoT hub를 배포할 수 있는 hello를 사용할 수 있습니다.

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

IoT 허브를 hello 중 하나에 대 한 리소스 그룹 toocreate IoT 허브, 다음 명령을 사용 하 여 hello에 대 한 위치를 지원 합니다. 이 예에서는 라는 리소스 그룹을 만든 **MyIoTRG1** hello에 **미국 동부** 영역:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>IoT Hub 만들기

다음 명령을 사용 하 여 hello hello 이전 단계에서 만든 hello 리소스 그룹에서 IoT hub toocreate 합니다. 이 예제에서는 만듭니다는 **S1** 호출할 허브 **MyTestIoTHub** hello에 **미국 동부** 영역:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

hello IoT 허브의 hello 이름은 고유 해야 합니다.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


다음 명령을 hello를 사용 하 여 구독에서 모든 hello IoT 허브를 나열할 수 있습니다.

```powershell
Get-AzureRmIotHub
```

청구는 S1 표준 IoT Hub를 추가 하는 hello 이전 예제입니다. 다음 명령을 hello를 사용 하 여 hello IoT 허브를 삭제할 수 있습니다.

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

또는, 리소스 그룹을 제거할 수 있습니다 하 고 모든 hello hello 다음 명령을 사용 하 여 포함 된 리소스:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>다음 단계

이제 PowerShell cmdlet을 사용 하 여 IoT hub를 배포한 tooexplore 더 이상 사용할 수 있습니다.

* [IoT Hub로 작업하기 위한 다른 PowerShell cmdlet][lnk-iothub-cmdlets]을 검색합니다.
* Hello의 hello 기능에 대 한 읽기 [IoT 허브 리소스 공급자 REST API][lnk-rest-api]합니다.

IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.

* [소개 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
