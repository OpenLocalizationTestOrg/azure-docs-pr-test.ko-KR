---
title: "Azure CLI (az.py)를 사용 하 여 IoT Hub aaaCreate | Microsoft Docs"
description: "어떻게 사용 하 여 Azure IoT 허브 toocreate hello 플랫폼 간 Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0을 사용 하 여 IoT 허브를 만듭니다.

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>소개

Azure CLI 2.0 (az.py) toocreate를 사용 하 여 수 있으며, Azure IoT 허브를 프로그래밍 방식으로 관리할 수 있습니다. 이 문서에서는 어떻게 toouse hello Azure CLI 2.0 (az.py) toocreate IoT hub를 보여 줍니다.

Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – CLI hello 클래식 및 리소스 관리 배포 모델에 대 한 hello 합니다.
* Azure CLI 2.0 (az.py)-이 문서에 설명 된 대로 hello 리소스 관리 배포 모델에 대 한 차세대 CLI hello 합니다.

toocomplete이이 자습서에서는 다음 hello 필요:

* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Azure 계정 로그인 및 설정

Azure 계정 tooyour 하 고 구독을 선택 합니다.

1. Hello 명령 프롬프트에서 실행 hello [로그인 명령][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Hello 코드를 사용 하 여 hello 지침 tooauthenticate 따르고 tooyour 웹 브라우저를 통해 Azure 계정에에서 로그인 합니다.

2. TooAzure 로그인 여러 Azure 구독이 있는 경우 tooall 액세스 부여 hello 자격 증명으로 연결 된 Azure 계정. Hello 다음을 사용 하 여 [명령 toolist hello Azure 계정] [ lnk-az-account-command] toouse 있습니다 사용할 수 있습니다.
    
    ```azurecli
    az account list 
    ```

    다음 명령은 tooselect 구독 toouse toorun hello 명령을 toocreate IoT 허브를 지정 하는 hello를 사용 합니다. Hello 이전 명령의 hello 출력에서 hello 구독 이름 또는 ID를 사용할 수 있습니다.

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>IoT Hub 만들기

Hello Azure CLI toocreate 리소스 그룹을 사용 하 하 고 IoT hub를 추가 키를 누릅니다.

1. IoT Hub는 리소스 그룹에서 만들어야 합니다. 기존 리소스 그룹을 사용 하거나 다음에 hello 실행할 [명령 toocreate 리소스 그룹][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > hello 앞의 예제는 hello West US 위치에에서 hello 리소스 그룹을 만듭니다. Hello 명령을 실행 하 여 사용할 수 있는 위치의 목록을 볼 수 있습니다 `az account list-locations -o table`합니다.
    >
    >

2. Hello 다음 실행 [명령 toocreate IoT hub] [ lnk-az-iot-command] 리소스 그룹에서 IoT 허브에 대 한 전역 고유 이름을 사용 하 여:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> hello 이전 명령은 hello S1 가격 책정 계층 청구 됩니다에 IoT 허브를 만듭니다. 자세한 내용은 [Azure IoT Hub 가격 책정][lnk-iot-pricing]을 참조하세요.
>
>

## <a name="remove-an-iot-hub"></a>IoT Hub 제거

Hello Azure CLI도 사용할 수 있습니다[개별 리소스를 삭제][lnk-az-resource-command], IoT 허브 또는 삭제와 같은 리소스 그룹 및 모든 IoT 허브를 포함 하 여 모든 리소스를 합니다.

toodelete IoT hub hello 다음 명령을 실행 하는 중:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete 리소스 그룹 및 모든 리소스를 다음 실행된 hello 명령 수 있습니다.

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>다음 단계
IoT 허브에 대 한 개발에 대 한 더 toolearn hello 다음 문서를 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [Azure 포털 toomanage IoT Hub hello를 사용 하 여][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
