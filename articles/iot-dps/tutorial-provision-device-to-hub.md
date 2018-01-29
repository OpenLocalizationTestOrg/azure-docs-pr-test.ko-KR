---
title: "Azure IoT Hub Device Provisioning Service를 사용하여 장치 프로비전 | Microsoft Docs"
description: "Azure IoT Hub Device Provisioning Service를 사용하여 단일 IoT Hub에 장치를 프로비전"
services: iot-dps
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: bf50699d2dc67294d554ba15713254a8b88d8ade
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="provision-the-device-to-an-iot-hub-using-the-azure-iot-hub-device-provisioning-service"></a>Azure IoT Hub Device Provisioning Service를 사용하여 IoT Hub에 장치를 프로비전

이전 자습서에서 Device Provisioning Service에 연결하기 위해 장치를 설정하는 방법을 배웠습니다. 이 자습서에서는 이 서비스를 사용하여 **_등록 목록_**을 사용하는 단일 IoT Hub에 장치를 프로비전하는 방법을 배웁니다. 이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

> [!div class="checklist"]
> * 장치 등록
> * 장치 시작
> * 장치가 등록되어 있는지 확인

## <a name="prerequisites"></a>필수 조건

계속 진행하기 전에 자습서에 설명된 대로 장치 및 *하드웨어 보안 모듈*을 구성할 수 있는지 확인하고, [Azure IoT Hub Device Provisioning Service를 사용하여 프로비전하도록 장치를 설정](./tutorial-set-up-device.md)합니다.


<a id="enrolldevice"></a>
## <a name="enroll-the-device"></a>장치 등록

이 단계에서는 Device Provisioning Service에 장치의 고유 보안 아티팩트를 추가하는 것이 포함됩니다. 이러한 보안 아티팩트는 다음과 같습니다.

- TPM 기반 장치의 경우:
    - 각 TPM 칩 또는 시뮬레이션에 고유한 *인증 키*입니다. 자세한 정보는 [TPM 인증 키 이해](https://technet.microsoft.com/library/cc770443.aspx)를 읽어보세요.
    - 네임스페이스/범위에서 장치를 고유하게 식별하는 데 사용되는 *등록 ID*입니다. 이는 장치 ID와 같거나 다를 수 있습니다. ID는 모든 장치에 필수입니다. TPM 기반 장치의 경우 등록 ID는 TPM 인증 키의 SHA-256 해시와 같이 TPM 자체에서 파생될 수도 있습니다.

    ![포털에서 TPM에 대한 등록 정보](./media/tutorial-provision-device-to-hub/tpm-device-enrollment.png)

- X.509 기반 장치의 경우:
    - [X.509에 발급된 인증서](https://msdn.microsoft.com/library/windows/desktop/bb540819.aspx) 칩 또는 시뮬레이션입니다. 형식은 *.pem* 또는 *.cer* 파일 중 하나입니다. 개별 등록은 X.509 시스템에 대한 *서명자 인증서*를, 등록 그룹의 경우 *루트 인증서*를 사용해야 합니다.

    ![포털에서 X.509에 대한 등록 정보](./media/tutorial-provision-device-to-hub/x509-device-enrollment.png)


Device Provisioning Service에 장치를 등록하는 방법은 두 가지가 있습니다.

- **등록 그룹** 특정 증명 메커니즘을 공유하는 장치의 그룹을 나타냅니다. 원하는 초기 구성을 공유하는 장치 수가 많은 경우 또는 장치가 모두 동일한 테넌트로 이동하는 경우 등록 그룹을 사용하는 것이 좋습니다.

    ![포털에서 X.509에 대한 등록 그룹](./media/tutorial-provision-device-to-hub/x509-enrollment-groups.png)

- **개별 등록** Device Provisioning Service에 등록할 수도 있는 단일 장치에 대한 항목을 나타냅니다. 개별 등록은 증명 메커니즘으로 x509 인증서 또는 SAS 토큰(실제 또는 가상 TPM) 중 하나를 사용할 수 있습니다. 고유한 초기 구성이 필요한 장치 또는 증명 메커니즘으로 TPM 또는 가상 TPM을 통해 SAS 토큰만을 사용할 수 있는 장치의 경우 개별 등록을 사용하는 것이 좋습니다. 개별 등록은 지정된 원하는 IoT Hub 장치 ID가 있을 수 있습니다.

포털에서 장치를 등록하는 단계는 다음과 같습니다.

1. 장치에서 HSM에 대한 보안 아티팩트를 적어 둡니다. 이전 자습서의 [보안 아티팩트 추출](./tutorial-set-up-device.md#extractsecurity)이란 제목의 섹션에 언급된 API를 개발 환경에서 사용해야 할 수도 있습니다.

1. Azure Portal에 로그인하고, 왼쪽 메뉴에서 **모든 리소스** 단추를 클릭하고, Device Provisioning Service를 엽니다.

1. Device Provisioning Service 요약 블레이드에서 **등록 관리**를 선택합니다. **개별 등록** 탭 또는 **등록 그룹** 탭 중 하나를 장치 설정에 따라 탭합니다. 위쪽에 있는 **추가** 단추를 클릭합니다. **TPM** 또는 **X.509**를 ID 증명 *메커니즘*으로 선택하고, 이전에 설명된 대로 적절한 보안 아티팩트를 입력합니다. 새 **IoT Hub 장치 ID**를 입력할 수도 있습니다. 완료되면 **저장** 단추를 클릭합니다. 

1. 장치를 성공적으로 등록하면 포털에 다음과 같은 화면이 표시됩니다.

    ![포털에서 성공적인 TPM 등록](./media/tutorial-provision-device-to-hub/tpm-enrollment-success.png)


## <a name="start-the-device"></a>장치 시작

이 시점에서 다음 설정이 장치 등록을 위해 준비되었습니다.

1. 장치 또는 장치 그룹이 Device Provisioning Service에 등록되었습니다. 
2. 장치가 Device Provisioning Service 클라이언트 SDK를 사용하여 응용 프로그램을 통해 구성 및 액세스가 가능한 HSM 칩과 함께 준비되어 있습니다.

장치에서 Device Provisioning Service를 통해 등록을 시작하도록 클라이언트 응용 프로그램을 허용합니다.  


## <a name="verify-the-device-is-registered"></a>장치가 등록되어 있는지 확인

장치가 부팅되면 다음 작업이 이루어져야 합니다. 자세한 내용은 TPM 시뮬레이터 샘플 응용 프로그램 [dps_client_sample](https://github.com/Azure/azure-iot-device-auth/blob/master/dps_client/samples/dps_client_sample/dps_client_sample.c)을 참조하세요. 

1. 장치가 Device Provisioning Service에 등록 요청을 보냅니다.
2. TPM 장치의 경우 Device Provisioning Service에서 장치가 응답하는 등록 챌린지를 다시 보냅니다. 
3. 등록에 성공하면 Device Provisioning Service는 IoT Hub URI, 장치 ID 및 암호화된 키를 장치로 다시 보냅니다. 
4. 그러면 장치의 IoT Hub 클라이언트 응용 프로그램이 사용자 허브에 연결됩니다. 
5. 허브에 성공적으로 연결되면 장치가 IoT Hub의 **Device Explorer**에 나타납니다. 

    ![포털에서 허브에 연결 성공](./media/tutorial-provision-device-to-hub/hub-connect-success.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 장치 등록
> * 장치 시작
> * 장치가 등록되어 있는지 확인

부하가 분산된 허브 간 여러 장치를 프로비전하는 방법에 알아보려면 다음 자습서를 진행합니다. 

> [!div class="nextstepaction"]
> [부하가 분산된 IoT Hub 간 장치 프로비전](./tutorial-provision-multiple-hubs.md)
