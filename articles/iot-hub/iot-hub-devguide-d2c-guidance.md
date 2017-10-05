---
title: "Azure IoT Hub 장치-클라우드 옵션 | Microsoft Docs"
description: "개발자 가이드 - 장치-클라우드 메시지, reported 속성 또는 클라우드-장치 통신을 위한 파일 업로드를 사용하는 경우에 대한 지침입니다."
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
ms.openlocfilehash: a36283053939ccd53856a394cd9efb66285271ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-communications-guidance"></a><span data-ttu-id="ec36d-103">장치-클라우드 통신 지침</span><span class="sxs-lookup"><span data-stu-id="ec36d-103">Device-to-cloud communications guidance</span></span>
<span data-ttu-id="ec36d-104">장치 앱에서 솔루션 백 엔드로 정보를 전송할 때 IoT Hub은 다음 세 가지 옵션을 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-104">When sending information from the device app to the solution back end, IoT Hub exposes three options:</span></span>

* <span data-ttu-id="ec36d-105">[장치-클라우드 메시지][lnk-d2c] 시계열 원격 분석 및 경고의 경우</span><span class="sxs-lookup"><span data-stu-id="ec36d-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span></span>
* <span data-ttu-id="ec36d-106">[보고된 속성][lnk-twins] 장기 실행 워크플로의 사용 가능한 기능, 조건 또는 상태와 같은 장치 상태 정보를 보고하는 경우</span><span class="sxs-lookup"><span data-stu-id="ec36d-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or the state of long-running workflows.</span></span> <span data-ttu-id="ec36d-107">예를 들어 구성 및 소프트웨어 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-107">For example, configuration and software updates.</span></span>
* <span data-ttu-id="ec36d-108">[파일 업로드][lnk-fileupload] 간헐적으로 연결된 장치로 업로드되거나 대역폭을 절약하기 위해 압축된 미디어 파일 및 대형 원격 분석 배치의 경우</span><span class="sxs-lookup"><span data-stu-id="ec36d-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="ec36d-109">다음은 다양한 장치-클라우드 통신 옵션에 대해 자세히 비교하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-109">Here is a detailed comparison of the various device-to-cloud communication options.</span></span>

|  | <span data-ttu-id="ec36d-110">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="ec36d-110">Device-to-cloud messages</span></span> | <span data-ttu-id="ec36d-111">reported 속성</span><span class="sxs-lookup"><span data-stu-id="ec36d-111">Reported properties</span></span> | <span data-ttu-id="ec36d-112">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="ec36d-112">File uploads</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="ec36d-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="ec36d-113">Scenario</span></span> | <span data-ttu-id="ec36d-114">원격 분석 시계열 및 알림</span><span class="sxs-lookup"><span data-stu-id="ec36d-114">Telemetry time series and alerts.</span></span> <span data-ttu-id="ec36d-115">예를 들어 256KB의 센서 데이터 배치는 5분마다 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-115">For example, 256-KB sensor data batches sent every 5 minutes.</span></span> | <span data-ttu-id="ec36d-116">사용할 수 있는 기능 및 조건</span><span class="sxs-lookup"><span data-stu-id="ec36d-116">Available capabilities and conditions.</span></span> <span data-ttu-id="ec36d-117">예를 들어 셀룰러 또는 WiFi와 같은 현재 장치 연결 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-117">For example, the current device connectivity mode such as cellular or WiFi.</span></span> <span data-ttu-id="ec36d-118">구성 및 소프트웨어 업데이트와 같이 장기 실행 워크플로 동기화</span><span class="sxs-lookup"><span data-stu-id="ec36d-118">Synchronizing long-running workflows, such as configuration and software updates.</span></span> | <span data-ttu-id="ec36d-119">미디어 파일.</span><span class="sxs-lookup"><span data-stu-id="ec36d-119">Media files.</span></span> <span data-ttu-id="ec36d-120">대형(일반적으로 압축됨) 원격 분석 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="ec36d-120">Large (typically compressed) telemetry batches.</span></span> |
| <span data-ttu-id="ec36d-121">저장 및 검색</span><span class="sxs-lookup"><span data-stu-id="ec36d-121">Storage and retrieval</span></span> | <span data-ttu-id="ec36d-122">IoT Hub에서 일시적으로 최대 7일 동안 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-122">Temporarily stored by IoT Hub, up to 7 days.</span></span> <span data-ttu-id="ec36d-123">순차 읽기만</span><span class="sxs-lookup"><span data-stu-id="ec36d-123">Only sequential reading.</span></span> | <span data-ttu-id="ec36d-124">IoT Hub에서 장치 쌍에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-124">Stored by IoT Hub in the device twin.</span></span> <span data-ttu-id="ec36d-125">[IoT Hub 쿼리 언어][lnk-query]를 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-125">Retrievable using the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="ec36d-126">사용자 제공 Azure Storage 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-126">Stored in user-provided Azure Storage account.</span></span> |
| <span data-ttu-id="ec36d-127">크기</span><span class="sxs-lookup"><span data-stu-id="ec36d-127">Size</span></span> | <span data-ttu-id="ec36d-128">최대 256KB 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-128">Up to 256-KB messages.</span></span> | <span data-ttu-id="ec36d-129">최대 reported 속성 크기는 8KB입니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-129">Maximum reported properties size is 8 KB.</span></span> | <span data-ttu-id="ec36d-130">Azure Blob Storage에서 지원하는 최대 파일 크기</span><span class="sxs-lookup"><span data-stu-id="ec36d-130">Maximum file size supported by Azure Blob Storage.</span></span> |
| <span data-ttu-id="ec36d-131">Frequency(빈도)</span><span class="sxs-lookup"><span data-stu-id="ec36d-131">Frequency</span></span> | <span data-ttu-id="ec36d-132">높음.</span><span class="sxs-lookup"><span data-stu-id="ec36d-132">High.</span></span> <span data-ttu-id="ec36d-133">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec36d-133">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="ec36d-134">중간.</span><span class="sxs-lookup"><span data-stu-id="ec36d-134">Medium.</span></span> <span data-ttu-id="ec36d-135">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec36d-135">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="ec36d-136">낮음.</span><span class="sxs-lookup"><span data-stu-id="ec36d-136">Low.</span></span> <span data-ttu-id="ec36d-137">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec36d-137">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="ec36d-138">프로토콜</span><span class="sxs-lookup"><span data-stu-id="ec36d-138">Protocol</span></span> | <span data-ttu-id="ec36d-139">모든 프로토콜에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-139">Available on all protocols.</span></span> | <span data-ttu-id="ec36d-140">현재 MQTT를 사용할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-140">Currently available only when using MQTT.</span></span> | <span data-ttu-id="ec36d-141">프로토콜을 사용할 때 사용할 수 있지만 장치에 HTTP가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-141">Available when using any protocol, but requires HTTP on the device.</span></span> |

<span data-ttu-id="ec36d-142">응용 프로그램이 원격 분석 시계열 또는 경고로 정보를 보내고 장치 쌍에서 사용할 수 있게 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-142">It is possible that an application requires to both send information as a telemetry time series or alert and also to make it available in the device twin.</span></span> <span data-ttu-id="ec36d-143">이 시나리오에서는 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-143">In this scenario, you can chose one of the following options:</span></span>

* <span data-ttu-id="ec36d-144">장치 앱이 장치-클라우드 메시지를 보내고 속성 변경 사항을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-144">The device app sends a device-to-cloud message and reports a property change.</span></span>
* <span data-ttu-id="ec36d-145">메시지를 받을 때 솔루션 백 엔드가 장치 쌍의 태그에 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-145">The solution back end can store the information in the device twin's tags when it receives the message.</span></span>

<span data-ttu-id="ec36d-146">장치-클라우드 메시지를 사용하면 장치 쌍 업데이트보다 훨씬 높은 처리량이 가능하므로 때로는 모든 장치-클라우드 메시지에 대해 장치 쌍을 업데이트하지 않는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="ec36d-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable to avoid updating the device twin for every device-to-cloud message.</span></span>


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
