---
title: aaaUnderstand hello Azure IoT Sdk | Microsoft Docs
description: "개발자 가이드-에 대 한 정보 및 링크 toohello toobuild 장치 앱과 백 엔드를 사용할 수 있는 다양 한 Azure IoT 장치 및 서비스 Sdk입니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>Azure IoT SDK 이해 및 사용

IoT Hub를 사용하기 위한 SDK에는 다음 세 가지 범주가 있습니다.

* **장치 Sdk** IoT 장치에서 실행 되는 toobuild 앱을 사용 합니다. 이러한 응용 프로그램 원격 분석 tooyour IoT hub를 보내고 필요에 따라 IoT 허브에서 메시지를 수신 합니다.

* **서비스 Sdk** 있습니다 toomanage IoT 허브를 사용 하 고 필요에 따라 메시지를 tooyour IoT 장치 보냅니다.

* **Azure IoT 가장자리** 하면 toobuild 게이트웨이 tooenable 장치 hello 지원 되는 프로토콜 중 하나를 사용 하지 않는 하 또는 tooprocess 메시지 hello 가장자리를 중지 해야 합니다.

Sdk는 toosupport 여러 프로그래밍 언어를 제공 합니다.

## <a name="azure-iot-device-sdks"></a>Azure IoT 장치 SDK

Microsoft Azure IoT 장치 Sdk hello 건물 장치를 용이 하 게 하는 코드가 들어 및 tooand 연결 하는 응용 프로그램은 Azure IoT 허브 서비스에서 관리 합니다.

hello 다음 Azure IoT 장치 Sdk는 GitHub에서 사용할 수 있는 toodownload:

* [C용 Azure IoT 장치 SDK][lnk-c-device-sdk] - 이식성과 광범위한 플랫폼 호환성을 위해 ANSI C(C99)로 작성되었습니다. 두 개의 장치 클라이언트 라이브러리, C에 대 한 hello 하위 수준 **iothub_client** 및 hello **serializer**합니다.
* [.NET용 Azure IoT 장치 SDK][lnk-dotnet-device-sdk]
* [Java용 Azure IoT 장치 SDK][lnk-java-device-sdk]
* [Node.js용 Azure IoT 장치 SDK][lnk-node-device-sdk]
* [Python용 Azure IoT 장치 SDK][lnk-python-device-sdk]

> [!NOTE]
> 개발 컴퓨터에서 언어와 플랫폼별 패키지 관리자 tooinstall 이진 파일 및 종속성을 사용 하는 방법에 대 한 정보에 대 한 hello GitHub 리포지토리에 hello 추가 정보 파일을 참조 하십시오.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>OS 플랫폼 및 하드웨어 호환성

SDK 호환성 특정 하드웨어 장치에 대 한 자세한 내용은 참조 hello [Azure IoT 장치 카탈로그에 대 한 인증][lnk-certified]합니다.

## <a name="azure-iot-service-sdks"></a>Azure IoT 서비스 SDK

hello Azure IoT 서비스 Sdk에 포함 되어 코드 toofacilitate IoT Hub toomanage 장치 및 보안와 직접 상호 작용 하는 응용 프로그램을 구축 합니다.

hello 다음 Azure IoT 서비스 Sdk는 GitHub에서 사용할 수 있는 toodownload:

* [.NET용 Azure IoT 서비스 SDK][lnk-dotnet-service-sdk]
* [Node.js용 Azure IoT 서비스 SDK][lnk-node-service-sdk]
* [Java용 Azure IoT 서비스 SDK][lnk-java-service-sdk]
* [Python용 Azure IoT 서비스 SDK][lnk-python-service-sdk]
* [C용 Azure IoT 서비스 SDK][lnk-c-service-sdk]

> [!NOTE]
> 개발 컴퓨터에서 언어와 플랫폼별 패키지 관리자 tooinstall 이진 파일 및 종속성을 사용 하는 방법에 대 한 정보에 대 한 hello GitHub 리포지토리에 hello 추가 정보 파일을 참조 하십시오.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT 가장자리 hello 인프라 및 모듈 toocreate IoT 게이트웨이 솔루션을 포함합니다. IoT 가장자리 toocreate 게이트웨이 맞춤형된 tooany 종단 간 시나리오를 확장할 수 있습니다.

GitHub에서 [Azure IoT Edge][lnk-iot-edge]를 다운로드할 수 있습니다.

## <a name="online-api-reference-documentation"></a>온라인 API 참조 설명서

hello 다음 목록은 Azure IoT 장치, 서비스 및 게이트웨이 라이브러리에 대 한 링크 tooonline API 참조 문서.

* [IoT(사물 인터넷) .NET][lnk-dotnet-ref]
* [IoT Hub REST][lnk-rest-ref]
* [C용 Azure IoT 장치 SDK][lnk-c-ref]
* [Java용 Azure IoT 장치 SDK][lnk-java-ref]
* [Java용 Azure IoT 서비스 SDK][lnk-java-service-ref]
* [Node.js용 Azure IoT 장치 SDK][lnk-node-ref]
* [Node.js용 Azure IoT 서비스 SDK][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>다음 단계

이 IoT Hub 개발자 가이드의 다른 참조 자료:

* [IoT Hub 끝점][lnk-devguide-endpoints]
* [장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][lnk-devguide-query]
* [할당량 및 제한][lnk-devguide-quotas]
* [IoT Hub MQTT 지원][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
