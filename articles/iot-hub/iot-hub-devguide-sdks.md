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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="8b35c-103">Azure IoT SDK 이해 및 사용</span><span class="sxs-lookup"><span data-stu-id="8b35c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="8b35c-104">IoT Hub를 사용하기 위한 SDK에는 다음 세 가지 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="8b35c-105">**장치 Sdk** IoT 장치에서 실행 되는 toobuild 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="8b35c-106">이러한 응용 프로그램 원격 분석 tooyour IoT hub를 보내고 필요에 따라 IoT 허브에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="8b35c-107">**서비스 Sdk** 있습니다 toomanage IoT 허브를 사용 하 고 필요에 따라 메시지를 tooyour IoT 장치 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="8b35c-108">**Azure IoT 가장자리** 하면 toobuild 게이트웨이 tooenable 장치 hello 지원 되는 프로토콜 중 하나를 사용 하지 않는 하 또는 tooprocess 메시지 hello 가장자리를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="8b35c-109">Sdk는 toosupport 여러 프로그래밍 언어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="8b35c-110">Azure IoT 장치 SDK</span><span class="sxs-lookup"><span data-stu-id="8b35c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="8b35c-111">Microsoft Azure IoT 장치 Sdk hello 건물 장치를 용이 하 게 하는 코드가 들어 및 tooand 연결 하는 응용 프로그램은 Azure IoT 허브 서비스에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="8b35c-112">hello 다음 Azure IoT 장치 Sdk는 GitHub에서 사용할 수 있는 toodownload:</span><span class="sxs-lookup"><span data-stu-id="8b35c-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="8b35c-113">[C용 Azure IoT 장치 SDK][lnk-c-device-sdk] - 이식성과 광범위한 플랫폼 호환성을 위해 ANSI C(C99)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="8b35c-114">두 개의 장치 클라이언트 라이브러리, C에 대 한 hello 하위 수준 **iothub_client** 및 hello **serializer**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="8b35c-115">[.NET용 Azure IoT 장치 SDK][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="8b35c-116">[Java용 Azure IoT 장치 SDK][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="8b35c-117">[Node.js용 Azure IoT 장치 SDK][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="8b35c-118">[Python용 Azure IoT 장치 SDK][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="8b35c-119">개발 컴퓨터에서 언어와 플랫폼별 패키지 관리자 tooinstall 이진 파일 및 종속성을 사용 하는 방법에 대 한 정보에 대 한 hello GitHub 리포지토리에 hello 추가 정보 파일을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b35c-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="8b35c-120">OS 플랫폼 및 하드웨어 호환성</span><span class="sxs-lookup"><span data-stu-id="8b35c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="8b35c-121">SDK 호환성 특정 하드웨어 장치에 대 한 자세한 내용은 참조 hello [Azure IoT 장치 카탈로그에 대 한 인증][lnk-certified]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="8b35c-122">Azure IoT 서비스 SDK</span><span class="sxs-lookup"><span data-stu-id="8b35c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="8b35c-123">hello Azure IoT 서비스 Sdk에 포함 되어 코드 toofacilitate IoT Hub toomanage 장치 및 보안와 직접 상호 작용 하는 응용 프로그램을 구축 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="8b35c-124">hello 다음 Azure IoT 서비스 Sdk는 GitHub에서 사용할 수 있는 toodownload:</span><span class="sxs-lookup"><span data-stu-id="8b35c-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="8b35c-125">[.NET용 Azure IoT 서비스 SDK][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="8b35c-126">[Node.js용 Azure IoT 서비스 SDK][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="8b35c-127">[Java용 Azure IoT 서비스 SDK][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="8b35c-128">[Python용 Azure IoT 서비스 SDK][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="8b35c-129">[C용 Azure IoT 서비스 SDK][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="8b35c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="8b35c-130">개발 컴퓨터에서 언어와 플랫폼별 패키지 관리자 tooinstall 이진 파일 및 종속성을 사용 하는 방법에 대 한 정보에 대 한 hello GitHub 리포지토리에 hello 추가 정보 파일을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b35c-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="8b35c-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="8b35c-131">Azure IoT Edge</span></span>

<span data-ttu-id="8b35c-132">Azure IoT 가장자리 hello 인프라 및 모듈 toocreate IoT 게이트웨이 솔루션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="8b35c-133">IoT 가장자리 toocreate 게이트웨이 맞춤형된 tooany 종단 간 시나리오를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="8b35c-134">GitHub에서 [Azure IoT Edge][lnk-iot-edge]를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b35c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="8b35c-135">온라인 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="8b35c-135">Online API reference documentation</span></span>

<span data-ttu-id="8b35c-136">hello 다음 목록은 Azure IoT 장치, 서비스 및 게이트웨이 라이브러리에 대 한 링크 tooonline API 참조 문서.</span><span class="sxs-lookup"><span data-stu-id="8b35c-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="8b35c-137">[IoT(사물 인터넷) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="8b35c-138">[IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="8b35c-139">[C용 Azure IoT 장치 SDK][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="8b35c-140">[Java용 Azure IoT 장치 SDK][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="8b35c-141">[Java용 Azure IoT 서비스 SDK][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="8b35c-142">[Node.js용 Azure IoT 장치 SDK][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="8b35c-143">[Node.js용 Azure IoT 서비스 SDK][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="8b35c-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="8b35c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b35c-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b35c-145">Next steps</span></span>

<span data-ttu-id="8b35c-146">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="8b35c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="8b35c-147">[IoT Hub 끝점][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="8b35c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="8b35c-148">[장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="8b35c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="8b35c-149">[할당량 및 제한][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="8b35c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="8b35c-150">[IoT Hub MQTT 지원][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="8b35c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
