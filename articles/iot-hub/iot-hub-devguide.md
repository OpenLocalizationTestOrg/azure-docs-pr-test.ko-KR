---
title: "Azure IoT 허브에 대 한 aaaDeveloper 가이드 | Microsoft Docs"
description: "hello Azure IoT 허브 개발자 가이드에는 끝점, 보안, hello id 레지스트리에, 장치 관리, 직접 메서드, 장치 트윈스, 파일 업로드, 작업, hello IoT Hub 쿼리 언어 및 메시징에 대해 포함 되어 있습니다."
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
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a><span data-ttu-id="feffd-103">Azure IoT Hub 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="feffd-103">Azure IoT Hub developer guide</span></span>

<span data-ttu-id="feffd-104">Azure IoT Hub는 수백만 개의 장치와 솔루션 백 엔드 간에 안정적이고 안전한 양방향 통신이 가능하도록 지원하는 완전히 관리되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-104">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="feffd-105">Azure IoT Hub는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-105">Azure IoT Hub provides you with:</span></span>

* <span data-ttu-id="feffd-106">장치 단위 보안 자격 증명 및 액세스 제어를 사용하여 보안 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-106">Secure communications by using per-device security credentials and access control.</span></span>
* <span data-ttu-id="feffd-107">다수의 장치-클라우드 및 클라우드-장치 하이퍼스케일(hyper-scale) 통신 옵션.</span><span class="sxs-lookup"><span data-stu-id="feffd-107">Multiple device-to-cloud and cloud-to-device hyper-scale communication options.</span></span>
* <span data-ttu-id="feffd-108">장치별 상태 정보 및 메타데이터를 쿼리할 수 있는 저장소</span><span class="sxs-lookup"><span data-stu-id="feffd-108">Queryable storage of per-device state information and meta-data.</span></span>
* <span data-ttu-id="feffd-109">Hello 가장 인기 있는 언어 및 플랫폼에 대 한 장치 라이브러리와 쉽게 장치 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-109">Easy device connectivity with device libraries for hello most popular languages and platforms.</span></span>

<span data-ttu-id="feffd-110">이 IoT 허브 개발자 가이드 문서 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-110">This IoT Hub developer guide includes hello following articles:</span></span>

* <span data-ttu-id="feffd-111">[장치-클라우드 통신 지침][lnk-d2c-guidance] - 장치-클라우드 메시지, 장치 쌍의 reported 속성, 파일 업로드 중에 하나를 선택하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-111">[Device-to-cloud communication guidance][lnk-d2c-guidance] helps you choose between device-to-cloud messages, device twin's reported properties, and file upload.</span></span>
* <span data-ttu-id="feffd-112">[클라우드-장치 통신 지침][lnk-c2d-guidance] - 직접 메서드, 장치 쌍의 desired 속성, 클라우드-장치 메시지 중 하나를 선택할 수 있도록 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-112">[Cloud-to-device communication guidance][lnk-c2d-guidance] helps you choose between direct methods, device twin's desired properties, and cloud-to-device messages.</span></span>
* <span data-ttu-id="feffd-113">[장치-클라우드 및 클라우드-장치 IoT Hub와 메시징] [ devguide-messaging] hello 메시징 기능 (장치-클라우드 및 클라우드-장치)에 IoT Hub 노출에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-113">[Device-to-cloud and cloud-to-device messaging with IoT Hub][devguide-messaging] describes hello messaging features (device-to-cloud and cloud-to-device) that IoT Hub exposes.</span></span>
  * <span data-ttu-id="feffd-114">[장치-클라우드 메시지 tooIoT 허브 보내기][devguide-messages-d2c]합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-114">[Send device-to-cloud messages tooIoT Hub][devguide-messages-d2c].</span></span>
  * <span data-ttu-id="feffd-115">[Hello 기본 제공 끝점에서 장치-클라우드 메시지를 읽은][devguide-builtin]합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-115">[Read device-to-cloud messages from hello built-in endpoint][devguide-builtin].</span></span>
  * <span data-ttu-id="feffd-116">[장치-클라우드 메시지에 대한 사용자 지정 끝점 및 라우팅 규칙 사용][devguide-custom]</span><span class="sxs-lookup"><span data-stu-id="feffd-116">[Use custom endpoints and routing rules for device-to-cloud messages][devguide-custom].</span></span>
  * <span data-ttu-id="feffd-117">[IoT Hub에서 클라우드-장치 메시지 보내기][devguide-messages-c2d]</span><span class="sxs-lookup"><span data-stu-id="feffd-117">[Send cloud-to-device messages from IoT Hub][devguide-messages-c2d].</span></span>
  * <span data-ttu-id="feffd-118">[IoT Hub 메시지 만들기 및 읽기][devguide-format]</span><span class="sxs-lookup"><span data-stu-id="feffd-118">[Create and read IoT Hub messages][devguide-format].</span></span>
* <span data-ttu-id="feffd-119">[장치에서 파일 업로드][devguide-upload] - 장치에서 파일을 업로드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-119">[Upload files from a device][devguide-upload] describes how you can upload files from a device.</span></span> <span data-ttu-id="feffd-120">hello 문서에는 알림을 hello 업로드 프로세스를 보낼 수 hello 같은 항목에 대 한 정보도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-120">hello article also includes information about topics such as hello notifications hello upload process can send.</span></span>
* <span data-ttu-id="feffd-121">[IoT Hub에서 장치 ID 관리][devguide-identities] - 각 IoT Hub의 ID 레지스트리에 어떤 정보가 저장되고 이것을 어떻게 액세스하고 수정할 수 있는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-121">[Manage device identities in IoT Hub][devguide-identities] describes what information each IoT hub's identity registry stores, and how you can access and modify it.</span></span>
* <span data-ttu-id="feffd-122">[액세스 tooIoT 허브 제어] [ devguide-security] 기능에 설명 hello 보안 사용 되는 모델 toogrant 액세스 tooIoT 허브 장치와 클라우드 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-122">[Control access tooIoT Hub][devguide-security] describes hello security model used toogrant access tooIoT Hub functionality for both devices and cloud components.</span></span> <span data-ttu-id="feffd-123">hello 문서에는 토큰 및 X.509 인증서 및 hello 사용 권한 부여할 수의 세부 정보를 사용 하는 방법에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-123">hello article includes information about using tokens and X.509 certificates, and details of hello permissions you can grant.</span></span>
* <span data-ttu-id="feffd-124">[장치 트윈스 toosynchronize 상태 및 구성을 사용 하 여] [ devguide-device-twins] hello 설명 *장치로 이중* 장치와 해당 장치를 동기화 하는 등 노출 하는 개념 및 hello 기능 로 이중 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-124">[Use device twins toosynchronize state and configurations][devguide-device-twins] describes hello *device twin* concept and hello functionality it exposes such as synchronizing a device with its device twin.</span></span> <span data-ttu-id="feffd-125">hello 문서 장치로 이중에 저장 된 hello 데이터에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-125">hello article includes information about hello data stored in a device twin.</span></span>
* <span data-ttu-id="feffd-126">[장치에서 직접 메서드를 호출] [ devguide-directmethods] hello 수명 주기는 직접적인 방법 tooinvoke 메서드 백 엔드 응용 프로그램 및 핸들 hello에서 장치에 장치에서 메서드를 지시 하는 방법에 대 한 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-126">[Invoke a direct method on a device][devguide-directmethods] describes hello lifecycle of a direct method, information about how tooinvoke methods on a device from your back-end app and handle hello direct method on your device.</span></span>
* <span data-ttu-id="feffd-127">[여러 장치에서 작업 예약][devguide-jobs] - 여러 장치에서 작업을 예약하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-127">[Schedule jobs on multiple devices][devguide-jobs] describes how you can schedule jobs on multiple devices.</span></span> <span data-ttu-id="feffd-128">hello 문서에서는 설명 방법을 toosubmit 작업 하는 장치로 이중을 사용 하 여 장치 업데이트 직접 메서드를 실행 하 고 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-128">hello article describes how toosubmit jobs that perform tasks as executing a direct method, updating a device using a device twin.</span></span> <span data-ttu-id="feffd-129">또한 tooquery 작업의 상태를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-129">It also describes how tooquery hello status of a job.</span></span>
* <span data-ttu-id="feffd-130">[참조-통신 프로토콜 선택] [ devguide-protocol] hello 통신 프로토콜 IoT Hub 장치 통신에 대 한 지원 및 목록 hello이 열려 있어야 하는 포트에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-130">[Reference - choose a communication protocol][devguide-protocol] describes hello communication protocols that IoT Hub supports for device communication and lists hello ports that should be open.</span></span>
* <span data-ttu-id="feffd-131">[IoT Hub 끝점 참조-] [ devguide-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-131">[Reference - IoT Hub endpoints][devguide-endpoints] describes hello various endpoints that each IoT hub exposes for runtime and management operations.</span></span> <span data-ttu-id="feffd-132">hello 대해서도 설명 하 고 IoT 허브에서 추가 끝점을 만들 수 있습니다 방법 toouse 필드 게이트웨이 tooenable 장치 연결 tooyour IoT Hub 비표준 시나리오에서 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-132">hello article also describes how you can create additional endpoints in your IoT hub, and how toouse a field gateway tooenable devices connectivity tooyour IoT Hub endpoints in non-standard scenarios.</span></span>
* <span data-ttu-id="feffd-133">[장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어 참조-] [ devguide-query] 장치 트윈스 및 작업에 대 한 허브에서 tooretrieve 정보 수 있는 해당 IoT Hub 쿼리 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-133">[Reference - IoT Hub query language for device twins, jobs, and message routing][devguide-query] describes that IoT Hub query language that enables you tooretrieve information from your hub about your device twins and jobs.</span></span>
* <span data-ttu-id="feffd-134">[참조-할당량 및 제한] [ devguide-quotas] hello IoT 허브 서비스와 조정 된 할당량을 초과 하면 toosee 기대할 수 있는 동작 hello에서 설정 된 hello 할당량 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-134">[Reference - quotas and throttling][devguide-quotas] summarizes hello quotas set in hello IoT Hub service and hello throttling behavior you can expect toosee when you exceed a quota.</span></span>
* <span data-ttu-id="feffd-135">[참조-가격] [ devguide-pricing] 다른 Sku 및 IoT Hub 및 IoT Hub에서 IoT Hub에 다양 한 기능으로 요금이 부과 되며 hello 메시지 하는 방법을 대 한 세부 정보에 대 한 가격 책정에 일반 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-135">[Reference - pricing][devguide-pricing] provides general information on different SKUs and pricing for IoT Hub and details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>
* <span data-ttu-id="feffd-136">[참조-장치 및 서비스 Sdk] [ devguide-sdks] 목록 hello Azure IoT Sdk toodevelop를 사용할 수 있습니다 IoT hub와 상호 작용 하는 장치 및 서비스 둘 다 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-136">[Reference - Device and service SDKs][devguide-sdks] lists hello Azure IoT SDKs you can use toodevelop both device and service apps that interact with your IoT hub.</span></span> <span data-ttu-id="feffd-137">hello 문서 링크 tooonline API 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-137">hello article includes links tooonline API documentation.</span></span>
* <span data-ttu-id="feffd-138">[참조-IoT 허브 MQTT 지원] [ devguide-mqtt] IoT Hub hello MQTT 프로토콜을 지 원하는 방법에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-138">[Reference - IoT Hub MQTT support][devguide-mqtt] provides detailed information about how IoT Hub supports hello MQTT protocol.</span></span> <span data-ttu-id="feffd-139">hello 문서 hello MQTT 프로토콜 기본 제공 toohello Azure IoT Sdk에 대 한 hello 지원에 설명 하 고 직접 hello MQTT 프로토콜을 사용 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-139">hello article describes hello support for hello MQTT protocol built-in toohello Azure IoT SDKs and provides information about using hello MQTT protocol directly.</span></span>
* <span data-ttu-id="feffd-140">[용어집][devguide-glossary] - 일반적인 IoT Hub 관련 용어 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="feffd-140">[Glossary][devguide-glossary] a list of common IoT Hub-related terms.</span></span>

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
