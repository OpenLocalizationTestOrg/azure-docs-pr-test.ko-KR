---
title: "aaaUse hello Azure PowerShell tooconfigure 파일 업로드 | Microsoft Docs"
description: "연결 된 장치를 어떻게 toouse hello Azure PowerShell cmdlet tooconfigure IoT 허브 tooenable 파일에는에서 업로드 합니다. Hello 대상 Azure 저장소 계정을 구성 하는 방법에 대 한 정보가 포함 됩니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Azure PowerShell을 사용하여 IoT Hub 파일 업로드 구성

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [IoT 허브에서 파일을 업로드 기능][lnk-upload], IoT hub와 Azure 저장소 계정을 연결 해야 합니다. 기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.
* [Azure PowerShell cmdlet][lnk-powershell-install]
* Azure IoT Hub - IoT hub를 설정 하지 않은 경우에 hello을 사용할 수 있습니다 [새로 AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] toocreate 하나 또는 사용 하 여 hello 포털 너무[IoT 허브를 만듭니다.] [ lnk-portal-hub].
* Azure 저장소 계정. Hello를 사용할 수 있는 Azure 저장소 계정이 없는 경우 [Azure 저장소 PowerShell cmdlet] [ lnk-powershell-storage] toocreate 하나 또는 사용 하 여 hello 포털 너무[저장소 계정 만들기] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Azure 계정 로그인 및 설정

Azure 계정 tooyour 하 고 구독을 선택 합니다.

1. Hello PowerShell 프롬프트에서 실행 hello **로그인 AzureRmAccount** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 구독. 다음 명령을 toolist hello 있습니다 사용할 수 있는 Azure 구독 toouse hello를 사용 합니다.

    ```powershell
    Get-AzureRMSubscription
    ```

    다음 명령은 tooselect 구독 toouse toorun hello 명령을 toomanage IoT 허브를 지정 하는 hello를 사용 합니다. Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>저장소 계정 세부 정보 검색

hello 다음 단계에서는 가정 hello를 사용 하 여 저장소 계정을 만든 **리소스 관리자** 배포 모델 및 하지 hello **클래식** 배포 모델입니다.

tooconfigure 파일을 업로드 하 여 장치에서 Azure 저장소 계정에 대 한 연결 문자열 hello를 해야 합니다. 저장소 계정 hello hello에 있어야 합니다. IoT hub와 같은 구독 합니다. Hello 저장소 계정에서 blob 컨테이너의 hello 이름도 필요 합니다. 다음 명령은 tooretrieve hello 저장소 계정 키를 사용 합니다.

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Hello 메모 **key1** 저장소 계정 키 값입니다. 단계를 수행 하는 hello에 있어야 합니다.

파일 업로드에 기존 Blob 컨테이너를 사용하거나 새 Blob 컨테이너를 만들 수 있습니다.

* 저장소 계정의 toolist hello 기존 blob 컨테이너 hello 다음 명령을 사용 합니다.

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* 다음 명령을 사용 하 여 hello 저장소 계정에서 blob 컨테이너 toocreate:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>IoT Hub 구성

IoT 허브 tooenable 구성할 수 있습니다 [파일 업로드 기능] [ lnk-upload] 저장소 계정 세부 정보를 사용 하 여 합니다.

hello 구성에는 다음 값에는 hello를 필요 합니다.

**저장소 컨테이너**: IoT hub와 현재 Azure 구독 tooassociate 프로그램의 Azure 저장소 계정에서 blob 컨테이너입니다. Hello 섹션 앞의 hello 필요한 저장소 계정 정보를 검색 했습니다. IoT Hub 때 자동으로 생성 SAS Uri toouse 장치에 대 한 쓰기 권한 toothis blob 컨테이너로 파일을 업로드 합니다.

**업로드된 파일에 대한 알림 받기**: 파일 업로드 알림을 사용하거나 사용하지 않도록 설정합니다.

**SAS TTL**:이 설정은-time-to-live의 SAS Uri IoT 허브에서 toohello 장치를 반환 하는 hello hello입니다. 기본적으로 tooone 시간을 설정 합니다.

**파일 설정을 기본 TTL 알림**: hello time-to-live 만료 되기 전에 파일 업로드 알림입니다. 기본적으로 tooone 하루를 설정 합니다.

**알림 최대 배달 횟수 파일**: hello 횟수입니다. IoT Hub 시도 toodeliver 파일 업로드 알림 hello 합니다. 기본적으로 too10를 설정 합니다.

IoT hub 상의 PowerShell cmdlet tooconfigure hello 파일 업로드 설정에 따라 hello를 사용 합니다.

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>다음 단계

IoT Hub hello 파일 업로드 기능에 대 한 자세한 내용은 참조 [장치에서 파일을 업로드][lnk-upload]합니다.

이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.

* [IoT 장치 대량 관리][lnk-bulk]
* [IoT Hub 메트릭][lnk-metrics]
* [작업 모니터링][lnk-monitor]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]
* [Hello 접지에서 IoT 솔루션 보안][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md