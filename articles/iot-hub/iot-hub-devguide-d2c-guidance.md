---
title: "IoT Hub 장치-클라우드 aaaAzure 옵션 | Microsoft Docs"
description: "개발자 가이드-클라우드-장치 통신에 대 한 toouse 장치-클라우드 메시지, 보고 된 속성 또는 파일 업로드 하는 경우에 대 한 지침입니다."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a><span data-ttu-id="10869-103">장치-클라우드 통신 지침</span><span class="sxs-lookup"><span data-stu-id="10869-103">Device-to-cloud communications guidance</span></span>
<span data-ttu-id="10869-104">Hello 장치 앱 toohello 솔루션 백 엔드에서 정보를 보낼 때 IoT 허브는 다음 세 가지 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-104">When sending information from hello device app toohello solution back end, IoT Hub exposes three options:</span></span>

* <span data-ttu-id="10869-105">[장치-클라우드 메시지][lnk-d2c] 시계열 원격 분석 및 경고의 경우</span><span class="sxs-lookup"><span data-stu-id="10869-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span></span>
* <span data-ttu-id="10869-106">[속성을 보고] [ lnk-twins] 사용할 수 있는 기능, 조건, 장기 실행 워크플로 hello 상태 등과 같은 장치 상태 정보를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or hello state of long-running workflows.</span></span> <span data-ttu-id="10869-107">예를 들어 구성 및 소프트웨어 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="10869-107">For example, configuration and software updates.</span></span>
* <span data-ttu-id="10869-108">[파일 업로드] [ lnk-fileupload] 미디어에 대 한 파일 및 원격 분석 큰 일괄 처리 간헐적으로 연결 된 장치에서 업로드 또는 toosave 대역폭을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="10869-109">여기의 hello 자세히 비교 하려면 다양 한 장치-클라우드 통신 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="10869-109">Here is a detailed comparison of hello various device-to-cloud communication options.</span></span>

|  | <span data-ttu-id="10869-110">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="10869-110">Device-to-cloud messages</span></span> | <span data-ttu-id="10869-111">reported 속성</span><span class="sxs-lookup"><span data-stu-id="10869-111">Reported properties</span></span> | <span data-ttu-id="10869-112">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="10869-112">File uploads</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="10869-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="10869-113">Scenario</span></span> | <span data-ttu-id="10869-114">원격 분석 시계열 및 알림</span><span class="sxs-lookup"><span data-stu-id="10869-114">Telemetry time series and alerts.</span></span> <span data-ttu-id="10869-115">예를 들어 256KB의 센서 데이터 배치는 5분마다 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-115">For example, 256-KB sensor data batches sent every 5 minutes.</span></span> | <span data-ttu-id="10869-116">사용할 수 있는 기능 및 조건</span><span class="sxs-lookup"><span data-stu-id="10869-116">Available capabilities and conditions.</span></span> <span data-ttu-id="10869-117">예를 들어 hello 현재 장치 연결 모드 셀룰러 같은 또는 WiFi 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-117">For example, hello current device connectivity mode such as cellular or WiFi.</span></span> <span data-ttu-id="10869-118">구성 및 소프트웨어 업데이트와 같이 장기 실행 워크플로 동기화</span><span class="sxs-lookup"><span data-stu-id="10869-118">Synchronizing long-running workflows, such as configuration and software updates.</span></span> | <span data-ttu-id="10869-119">미디어 파일.</span><span class="sxs-lookup"><span data-stu-id="10869-119">Media files.</span></span> <span data-ttu-id="10869-120">대형(일반적으로 압축됨) 원격 분석 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="10869-120">Large (typically compressed) telemetry batches.</span></span> |
| <span data-ttu-id="10869-121">저장 및 검색</span><span class="sxs-lookup"><span data-stu-id="10869-121">Storage and retrieval</span></span> | <span data-ttu-id="10869-122">Too7 일을 IoT Hub에서 일시적으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-122">Temporarily stored by IoT Hub, up too7 days.</span></span> <span data-ttu-id="10869-123">순차 읽기만</span><span class="sxs-lookup"><span data-stu-id="10869-123">Only sequential reading.</span></span> | <span data-ttu-id="10869-124">Hello 장치로 이중에 IoT Hub가 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-124">Stored by IoT Hub in hello device twin.</span></span> <span data-ttu-id="10869-125">Hello를 사용 하 여 검색할 수 [IoT Hub 쿼리 언어][lnk-query]합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-125">Retrievable using hello [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="10869-126">사용자 제공 Azure Storage 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="10869-126">Stored in user-provided Azure Storage account.</span></span> |
| <span data-ttu-id="10869-127">크기</span><span class="sxs-lookup"><span data-stu-id="10869-127">Size</span></span> | <span data-ttu-id="10869-128">Too256 KB 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="10869-128">Up too256-KB messages.</span></span> | <span data-ttu-id="10869-129">최대 reported 속성 크기는 8KB입니다.</span><span class="sxs-lookup"><span data-stu-id="10869-129">Maximum reported properties size is 8 KB.</span></span> | <span data-ttu-id="10869-130">Azure Blob Storage에서 지원하는 최대 파일 크기</span><span class="sxs-lookup"><span data-stu-id="10869-130">Maximum file size supported by Azure Blob Storage.</span></span> |
| <span data-ttu-id="10869-131">Frequency(빈도)</span><span class="sxs-lookup"><span data-stu-id="10869-131">Frequency</span></span> | <span data-ttu-id="10869-132">높음.</span><span class="sxs-lookup"><span data-stu-id="10869-132">High.</span></span> <span data-ttu-id="10869-133">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10869-133">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="10869-134">중간.</span><span class="sxs-lookup"><span data-stu-id="10869-134">Medium.</span></span> <span data-ttu-id="10869-135">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10869-135">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="10869-136">낮음.</span><span class="sxs-lookup"><span data-stu-id="10869-136">Low.</span></span> <span data-ttu-id="10869-137">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10869-137">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="10869-138">프로토콜</span><span class="sxs-lookup"><span data-stu-id="10869-138">Protocol</span></span> | <span data-ttu-id="10869-139">모든 프로토콜에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-139">Available on all protocols.</span></span> | <span data-ttu-id="10869-140">현재 MQTT를 사용할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-140">Currently available only when using MQTT.</span></span> | <span data-ttu-id="10869-141">HTTP hello 장치에 필요 하지만 모든 프로토콜을 사용 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-141">Available when using any protocol, but requires HTTP on hello device.</span></span> |

<span data-ttu-id="10869-142">응용 프로그램에 원격 분석 시계열 또는 경고 및로 toomake tooboth 송신 정보 필요한 수 hello 장치로 이중 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-142">It is possible that an application requires tooboth send information as a telemetry time series or alert and also toomake it available in hello device twin.</span></span> <span data-ttu-id="10869-143">이 시나리오에서는 hello 다음 옵션 중 하나를 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-143">In this scenario, you can chose one of hello following options:</span></span>

* <span data-ttu-id="10869-144">hello 장치 응용 프로그램 장치-클라우드 메시지를 보내고 속성 변경 사항을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="10869-144">hello device app sends a device-to-cloud message and reports a property change.</span></span>
* <span data-ttu-id="10869-145">hello 메시지를 받을 때 hello 솔루션 백 엔드 hello 장치로 이중의 태그에 hello 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10869-145">hello solution back end can store hello information in hello device twin's tags when it receives hello message.</span></span>

<span data-ttu-id="10869-146">장치-클라우드 메시지 장치로 이중 업데이트 보다 훨씬 더 높은 처리량을 사용 하도록 설정 되므로 경우에 따라 바람직하지 tooavoid 업데이트 hello 장치로 이중 모든 장치-클라우드 메시지에 대 한.</span><span class="sxs-lookup"><span data-stu-id="10869-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable tooavoid updating hello device twin for every device-to-cloud message.</span></span>


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
