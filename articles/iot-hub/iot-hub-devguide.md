---
title: "IoT Hub에 대한 개발자 가이드 | Microsoft Docs"
description: "Azure IoT Hub 개발자 가이드는 끝점의 토론, 보안, ID 레지스트리, 장치 관리, 직접 메서드, 장치 쌍, 파일 업로드, 작업, IoT Hub 쿼리 언어 및 메시징을 포함합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: adb9a12899e9040cd83d522c734448989636fe29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="737b7-103">Azure IoT Hub 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="737b7-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="737b7-104">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="737b7-105">Azure IoT Hub는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="737b7-106">장치 단위 보안 자격 증명 및 액세스 제어를 사용하여 보안 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="737b7-107">다수의 장치-클라우드 및 클라우드-장치 하이퍼스케일(hyper-scale) 통신 옵션.</span><span class="sxs-lookup"><span data-stu-id="737b7-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="737b7-108">장치별 상태 정보 및 메타데이터를 쿼리할 수 있는 저장소</span><span class="sxs-lookup"><span data-stu-id="737b7-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="737b7-109">가장 인기 있는 언어 및 플랫폼에 대한 장치 라이브러리로 쉽게 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-109">Easy device connectivity with device libraries for the most popular languages and platforms.</span></span>

<span data-ttu-id="737b7-110">이 IoT Hub 개발자 가이드는 다음 문서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-110">This IoT Hub developer guide includes the following articles:</span></span>

* <span data-ttu-id="737b7-111">[장치-클라우드 통신 지침][lnk-d2c-guidance] - 장치-클라우드 메시지, 장치 쌍의 reported 속성, 파일 업로드 중에 하나를 선택하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="737b7-112">[클라우드-장치 통신 지침][lnk-c2d-guidance] - 직접 메서드, 장치 쌍의 desired 속성, 클라우드-장치 메시지 중 하나를 선택할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="737b7-113">[IoT Hub를 사용한 장치-클라우드 및 클라우드-장치 메시징][devguide-messaging]에서는 IoT Hub가 노출하는 메시징 기능(장치-클라우드 및 클라우드-장치)을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes the messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="737b7-114">[IoT Hub에 장치-클라우드 메시지 보내기][devguide-messages-d2c]</span><span class="sxs-lookup"><span data-stu-id="737b7-114">[Send device-to-cloud messages to IoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="737b7-115">[기본 제공 끝점에서 장치-클라우드 메시지 읽기][devguide-builtin]</span><span class="sxs-lookup"><span data-stu-id="737b7-115">[Read device-to-cloud messages from the built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="737b7-116">[장치-클라우드 메시지에 대한 사용자 지정 끝점 및 라우팅 규칙 사용][devguide-custom]</span><span class="sxs-lookup"><span data-stu-id="737b7-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="737b7-117">[IoT Hub에서 클라우드-장치 메시지 보내기][devguide-messages-c2d]</span><span class="sxs-lookup"><span data-stu-id="737b7-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="737b7-118">[IoT Hub 메시지 만들기 및 읽기][devguide-format]</span><span class="sxs-lookup"><span data-stu-id="737b7-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="737b7-119">[장치에서 파일 업로드][devguide-upload] - 장치에서 파일을 업로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="737b7-120">이 문서에는 업로드 프로세스에서 보낼 수 있는 알림과 같은 항목에 대한 정보도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-120">The article also includes information about topics such as the notifications the upload process can send.</span></span>
* <span data-ttu-id="737b7-121">[IoT Hub에서 장치 ID 관리][devguide-identities] - 각 IoT Hub의 ID 레지스트리에 어떤 정보가 저장되고 이것을 어떻게 액세스하고 수정할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="737b7-122">[IoT Hub에 대한 액세스 제어][devguide-security] - 장치 및 클라우드 구성 요소에 대한 IoT Hub 기능에 액세스 권한을 부여하는 데 사용되는 보안 모델을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-122">[Control access to IoT Hub][devguide-security] describes the security model used to grant access to IoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="737b7-123">이 문서에서는 토큰 및 X.509 인증서 사용에 대한 정보와 부여할 수 있는 권한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-123">The article includes information about using tokens and X.509 certificates, and details of the permissions you can grant.</span></span>
* <span data-ttu-id="737b7-124">[장치 쌍을 사용하여 상태 및 구성 동기화][devguide-device-twins] - *장치 쌍* 개념과 장치와 해당 장치 쌍을 사용한 장치 동기화와 같이 노출되는 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-124">[Use device twins to synchronize state and configurations][devguide-device-twins] describes the *device twin* concept and the functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="737b7-125">이 문서는 장치 쌍에 저장된 데이터에 대한 정보도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-125">The article includes information about the data stored in a device twin.</span></span>
* <span data-ttu-id="737b7-126">[장치에 직접 메서드 호출][devguide-directmethods] - 직접 메서드의 수명 주기, 백 엔드 앱에서 장치에 대한 메서드를 호출하고 장치에서 직접 메서드를 처리하는 방법에 대한 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-126">[Invoke a direct method on a device][devguide-directmethods] describes the lifecycle of a direct method, information about how to invoke methods on a device from your back-end app and handle the direct method on your device.</span></span>
* <span data-ttu-id="737b7-127">[여러 장치에서 작업 예약][devguide-jobs] - 여러 장치에서 작업을 예약하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="737b7-128">이 문서에서는 직접 메서드 실행, 장치 쌍을 사용하여 장치 업데이트와 같은 태스크를 수행하는 작업을 제출하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-128">The article describes how to submit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="737b7-129">또한 작업 상태를 쿼리하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-129">It also describes how to query the status of a job.</span></span>
* <span data-ttu-id="737b7-130">[참조 - 통신 프로토콜 선택][devguide-protocol]에서는 IoT Hub가 장치 통신에 대해 지원하는 통신 프로토콜을 설명하고 열려 있어야 하는 포트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-130">[Reference - choose a communication protocol][devguide-protocol] describes the communication protocols that IoT Hub supports for device communication and lists the ports that should be open.</span></span>
* <span data-ttu-id="737b7-131">[참조 - IoT Hub 끝점][devguide-endpoints] - 각 IoT Hub가 런타임 및 관리 작업에 노출하는 다양한 끝점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes the various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="737b7-132">이 문서에서는 IoT Hub에서 추가 끝점을 만드는 방법과 비표준 시나리오에서 IoT Hub 끝점에 대한 장치 연결을 사용하도록 하는 필드 게이트웨이를 사용하는 방법에 대해서도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-132">The article also describes how you can create additional endpoints in your IoT hub, and how to use a field gateway to enable devices connectivity to your IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="737b7-133">[참조 - 장치 쌍, 작업 및 메시지 라우팅에 대한 IoT Hub 쿼리 언어][devguide-query]에서는 허브에서 장치 쌍 및 작업에 대한 정보를 검색할 수 있는 IoT Hub 쿼리 언어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you to retrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="737b7-134">[참조 - 할당량 및 제한][devguide-quotas] - IoT Hub 서비스에 설정된 할당량과 할당량을 초과할 때 표시될 것으로 예상되는 제한 동작이 요약되어 잇습니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-134">[Reference - quotas and throttling][devguide-quotas] summarizes the quotas set in the IoT Hub service and the throttling behavior you can expect to see when you exceed a quota.</span></span>
* <span data-ttu-id="737b7-135">[참조 – 가격 책정][devguide-pricing] - IoT Hub의 다양한 SKU 및 가격 책정에 대한 일반적인 정보와 IoT Hub에서 다양한 IoT Hub 기능에 대한 요금을 메시지로 적용하는 방식에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="737b7-136">[참조 - 장치 및 서비스 SDK][devguide-sdks] - IoT Hub와 상호 작용하는 장치 앱과 서비스 앱을 개발할 때 사용할 수 있는 Azure IoT SDK를 나열하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-136">[Reference - Device and service SDKs][devguide-sdks] lists the Azure IoT SDKs you can use to develop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="737b7-137">이 문서에는 온라인 API 설명서에 대한 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-137">The article includes links to online API documentation.</span></span>
* <span data-ttu-id="737b7-138">[참조 - IoT Hub MQTT 지원][devguide-mqtt] - IoT Hub가 MQTT 프로토콜을 어떻게 지원하는지에 대한 자세한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports the MQTT protocol.</span></span> <span data-ttu-id="737b7-139">이 문서에서는 Azure IoT SDK에 기본 제공되는 MQTT 프로토콜에 대한 지원을 설명하며 MQTT 프로토콜을 직접 사용하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-139">The article describes the support for the MQTT protocol built-in to the Azure IoT SDKs and provides information about using the MQTT protocol directly.</span></span>
* <span data-ttu-id="737b7-140">[용어집][devguide-glossary] - 일반적인 IoT Hub 관련 용어 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="737b7-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
