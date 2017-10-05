---
title: "Azure IoT SDK 이해 | Microsoft Docs"
description: "개발자 가이드 - 장치 및 백 엔드 앱을 빌드하는데 사용할 수 있는 다양한 Azure IoT 장치 및 서비스 SDK에 대한 링크 정보입니다."
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
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="6b012-103">Azure IoT SDK 이해 및 사용</span><span class="sxs-lookup"><span data-stu-id="6b012-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="6b012-104">IoT Hub를 사용하기 위한 SDK에는 다음 세 가지 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="6b012-105">**장치 SDK**를 사용하면 IoT 장치에서 실행되는 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="6b012-106">이러한 앱은 IoT Hub로 원격 분석을 보내고, 필요에 따라 IoT Hub에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="6b012-107">**서비스 SDK**를 사용하면 IoT Hub를 관리하고, 필요에 따라 IoT 장치로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="6b012-108">**Azure IoT Edge**를 사용하면 지원되는 프로토콜 중 하나를 사용하지 않거나 에지에서 메시지를 처리해야 할 때 장치를 활성화하도록 게이트웨이를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="6b012-109">SDK는 여러 프로그래밍 언어를 지원하기 위해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="6b012-110">Azure IoT 장치 SDK</span><span class="sxs-lookup"><span data-stu-id="6b012-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="6b012-111">Microsoft Azure IoT 장치 SDK에는 Azure IoT Hub 서비스에 연결되고 Azure IoT Hub 서비스에서 관리하는 장치와 응용 프로그램의 빌드를 용이하게 하는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="6b012-112">다음 Azure IoT 장치 SDK는 GitHub에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="6b012-113">[C용 Azure IoT 장치 SDK][lnk-c-device-sdk] - 이식성과 광범위한 플랫폼 호환성을 위해 ANSI C(C99)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="6b012-114">C용 장치 클라이언트 라이브러리에는 하위 수준 **iothub_client** 및 **serializer**의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="6b012-115">[.NET용 Azure IoT 장치 SDK][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="6b012-116">[Java용 Azure IoT 장치 SDK][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="6b012-117">[Node.js용 Azure IoT 장치 SDK][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="6b012-118">[Python용 Azure IoT 장치 SDK][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="6b012-119">언어 및 플랫폼 특정 패키지 관리자를 사용하여 개발 컴퓨터에서 이진 파일 및 종속성을 설치하는 방법에 대한 정보는 GitHub 리포지토리의 추가 정보 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b012-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="6b012-120">OS 플랫폼 및 하드웨어 호환성</span><span class="sxs-lookup"><span data-stu-id="6b012-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="6b012-121">특정 하드웨어 장치와의 SDK 호환성에 대한 자세한 내용은 [IoT용 Azure Certified 장치 카탈로그][lnk-certified]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b012-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="6b012-122">Azure IoT 서비스 SDK</span><span class="sxs-lookup"><span data-stu-id="6b012-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="6b012-123">Azure IoT 서비스 SDK에는 장치와 보안을 관리하기 위해 IoT Hub 서비스를 직접 조작하는 응용 프로그램의 빌드를 용이하게 하는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="6b012-124">다음 Azure IoT 서비스 SDK는 GitHub에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="6b012-125">[.NET용 Azure IoT 서비스 SDK][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="6b012-126">[Node.js용 Azure IoT 서비스 SDK][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="6b012-127">[Java용 Azure IoT 서비스 SDK][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="6b012-128">[Python용 Azure IoT 서비스 SDK][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="6b012-129">[C용 Azure IoT 서비스 SDK][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="6b012-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="6b012-130">언어 및 플랫폼 특정 패키지 관리자를 사용하여 개발 컴퓨터에서 이진 파일 및 종속성을 설치하는 방법에 대한 정보는 GitHub 리포지토리의 추가 정보 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b012-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="6b012-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="6b012-131">Azure IoT Edge</span></span>

<span data-ttu-id="6b012-132">Azure IoT Edge에는 IoT 게이트웨이 솔루션을 만들기 위한 인프라 및 모듈이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="6b012-133">IoT Edge를 확장하여 종단 간 시나리오에 맞는 게이트웨이를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="6b012-134">GitHub에서 [Azure IoT Edge][lnk-iot-edge]를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="6b012-135">온라인 API 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="6b012-135">Online API reference documentation</span></span>

<span data-ttu-id="6b012-136">다음 목록은 Azure IoT 장치, 서비스 및 게이트웨이 라이브러리용 온라인 API 참조 설명서에 대한 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b012-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="6b012-137">[IoT(사물 인터넷) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="6b012-138">[IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="6b012-139">[C용 Azure IoT 장치 SDK][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="6b012-140">[Java용 Azure IoT 장치 SDK][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="6b012-141">[Java용 Azure IoT 서비스 SDK][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="6b012-142">[Node.js용 Azure IoT 장치 SDK][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="6b012-143">[Node.js용 Azure IoT 서비스 SDK][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="6b012-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="6b012-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b012-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b012-145">Next steps</span></span>

<span data-ttu-id="6b012-146">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="6b012-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="6b012-147">[IoT Hub 끝점][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="6b012-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="6b012-148">[장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="6b012-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="6b012-149">[할당량 및 제한][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="6b012-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="6b012-150">[IoT Hub MQTT 지원][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="6b012-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
