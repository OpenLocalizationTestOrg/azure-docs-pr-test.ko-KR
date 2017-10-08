---
title: "Azure CLI (azure.js)를 사용 하 여 IoT hub aaaCreate | Microsoft Docs"
description: "어떻게 사용 하 여 Azure IoT 허브 toocreate hello 플랫폼 간 Azure CLI (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 IoT 허브를 만듭니다.

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>소개

Azure CLI (azure.js) toocreate를 사용 하 여 수 있으며, Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다. 이 문서에서는 어떻게 toouse hello Azure CLI (azure.js) toocreate IoT hub를 보여 줍니다.

Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

* Azure CLI (azure.js) – hello CLI 클래식 hello와이 문서에 설명 된 대로 리소스 관리 배포 모델에 대 한 합니다.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -차세대 CLI hello 리소스 관리 배포 모델에 대 한 hello 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.
* [Azure CLI 0.10.4][lnk-CLI-install] 이상 설치 된 Azure CLI hello 이미 있는 경우 다음 명령을 hello로 hello hello 명령 프롬프트에서 현재 버전을 확인할 수 있습니다.

```azurecli
azure --version
```

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Azure Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. hello Azure CLI Azure Resource Manager 모드에 있어야 합니다.
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Azure 계정 및 구독 설정

1. Hello 명령 프롬프트에서 다음 명령을 hello를 입력 하 여 로그인:

   ```azurecli
    azure login
   ```

   Hello 제안 된 웹 브라우저와 코드 tooauthenticate 사용 합니다.
1. 여러 Azure 구독이 있는 경우 tooAzure 연결 액세스 권한을 부여 tooall hello 자격 증명으로 연결 된 Azure 구독. 볼 수 있습니다 hello Azure 구독 및 hello 명령을 사용 하 여 hello 기본적으로는 어떤 것을 식별 합니다.

   ```azurecli
    azure account list
   ```

   tooset hello 구독 상황에 맞는 hello toorun hello 나머지 원하는 명령을 사용 합니다.

   ```azurecli
    azure account set <subscription name>
   ```

1. 리소스 그룹이 없으면 **exampleResourceGroup**이라는 이름의 리소스 그룹을 만들 수 있습니다.

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> hello 문서 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹] [ lnk-CLI-arm] toouse Azure CLI toomanage Azure hello 하는 방법에 대 한 자세한 정보를 제공 리소스입니다.

## <a name="create-an-iot-hub"></a>IoT Hub 만들기

필수 매개 변수:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resource-group**: hello 리소스 그룹 이름입니다. hello 형식은 소문자 영숫자, 밑줄 및 하이픈, 1-64 길이입니다.
* **이름**. 만든 hello IoT 허브 toobe의 hello 이름입니다. hello 형식은 소문자 영숫자, 밑줄 및 하이픈, 3-50 길이입니다.
* **location**: hello 위치 (azure 지역/데이터 센터) tooprovision hello IoT 허브입니다.
* **sku-name**: 중 하나는 hello sku의 hello 이름: [F1, S1, S2, S3]. 최신 전체 목록을 hello toohello IoT 허브에 대 한 가격 책정 페이지를 참조 하십시오.
* **units**: hello 프로 비전 된 단위 수입니다. 범위: F1[1-1], S1, S2[1-200], S3[1-10]. IoT Hub 단위 기반 tooconnect 원하는 장치에 총 메시지 수와 hello 수 있습니다.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee 모든 hello 작성할 수 있는 매개 변수, 명령 프롬프트에서 hello 도움말 명령을 사용할 수 있습니다.

```azurecli
azure iothub create -h
```

간단한 예: IoT 허브 호출 toocreate **exampleIoTHubName** hello 리소스 그룹에 **exampleResourceGroup**실행 hello 다음 명령을:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> 이 Azure CLI 명령은 대금이 청구되는 S1 표준 IoT Hub를 만듭니다. Hello IoT 허브를 삭제할 수 있습니다 **exampleIoTHubName** 다음 명령을 사용 하 여:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>다음 단계

toolearn IoT 허브에 대 한 개발에 대 한 더 hello 다음 문서를 참조 하세요.

* [IoT SDK][lnk-sdks]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure 포털 toomanage IoT Hub hello를 사용 하 여][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
