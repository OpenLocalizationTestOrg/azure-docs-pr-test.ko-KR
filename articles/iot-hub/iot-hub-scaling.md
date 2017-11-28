---
title: "aaaAzure IoT 허브를 크기 조정 | Microsoft Docs"
description: "어떻게 tooscale IoT 허브 toosupport 예상된 메시지 처리량입니다. 각 계층에 대 한 지원 hello 처리량 및 분할에 대 한 옵션에 대 한 요약을 포함합니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="679ee-104">IoT Hub 솔루션 크기 조정</span><span class="sxs-lookup"><span data-stu-id="679ee-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="679ee-105">Azure IoT Hub tooa 백만 동시에 연결 된 장치를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="679ee-106">자세한 내용은 [IoT Hub 가격 책정][lnk-pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="679ee-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="679ee-107">각 IoT Hub 단위는 특정 개수의 일일 메시지를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="679ee-108">tooproperly는 솔루션 확장, IoT 허브의 특정 용도 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="679ee-109">특히 다음 범주의 작업 hello에 대 한 필요한 hello 최대 처리량을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="679ee-110">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="679ee-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="679ee-111">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="679ee-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="679ee-112">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="679ee-112">Identity registry operations</span></span>

<span data-ttu-id="679ee-113">또한 toothis 처리량 정보에서 참조 [IoT Hub 할당량 및 제한을] [ IoT Hub quotas and throttles] 및 그에 따라 솔루션을 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="679ee-114">장치-클라우드 및 클라우드-장치 메시지 처리량</span><span class="sxs-lookup"><span data-stu-id="679ee-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="679ee-115">hello 가장 좋은 방법은 toosize IoT Hub 솔루션에는 단위 별로 tooevaluate hello 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="679ee-116">장치-클라우드 메시지는 다음과 같은 지속적인 처리량 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="679ee-117">계층</span><span class="sxs-lookup"><span data-stu-id="679ee-117">Tier</span></span> | <span data-ttu-id="679ee-118">지속적인 처리량</span><span class="sxs-lookup"><span data-stu-id="679ee-118">Sustained throughput</span></span> | <span data-ttu-id="679ee-119">지속적인 전송 속도</span><span class="sxs-lookup"><span data-stu-id="679ee-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="679ee-120">S1</span><span class="sxs-lookup"><span data-stu-id="679ee-120">S1</span></span> |<span data-ttu-id="679ee-121">단위당 KB too1111 수/분</span><span class="sxs-lookup"><span data-stu-id="679ee-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="679ee-122">(1.5GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="679ee-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="679ee-123">장치당 평균 278메시지/분</span><span class="sxs-lookup"><span data-stu-id="679ee-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="679ee-124">(400,000메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="679ee-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="679ee-125">S2</span><span class="sxs-lookup"><span data-stu-id="679ee-125">S2</span></span> |<span data-ttu-id="679ee-126">Too16 MB/분 단위 당를</span><span class="sxs-lookup"><span data-stu-id="679ee-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="679ee-127">(22.8GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="679ee-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="679ee-128">장치당 평균 4,167개 메시지/분</span><span class="sxs-lookup"><span data-stu-id="679ee-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="679ee-129">(6백만 개의 메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="679ee-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="679ee-130">S3</span><span class="sxs-lookup"><span data-stu-id="679ee-130">S3</span></span> |<span data-ttu-id="679ee-131">Too814 MB/분 단위 당를</span><span class="sxs-lookup"><span data-stu-id="679ee-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="679ee-132">(1144.4GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="679ee-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="679ee-133">장치당 평균 208,333 메시지/분</span><span class="sxs-lookup"><span data-stu-id="679ee-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="679ee-134">(3억 개의 메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="679ee-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="679ee-135">ID 레지스트리 작업 처리량</span><span class="sxs-lookup"><span data-stu-id="679ee-135">Identity registry operation throughput</span></span>
<span data-ttu-id="679ee-136">IoT Hub identity 레지스트리 작업 toobe 런타임 작업 멤버인 관련된 toodevice 프로 비전 대부분 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="679ee-137">관련 버스트 성능 수치는 [IoT Hub 할당량 및 제한][IoT Hub quotas and throttles]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="679ee-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="679ee-138">분할</span><span class="sxs-lookup"><span data-stu-id="679ee-138">Sharding</span></span>
<span data-ttu-id="679ee-139">단일 IoT 허브 장치의 toomillions 확장할 수, 하는 동안 솔루션 특정 성능 특성을 단일 IoT 허브 보장할 수 없습니다이 필요한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="679ee-140">이 경우 여러 IoT Hub로 장치를 분할하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="679ee-141">여러 IoT hub 트래픽 급증을 매끄럽게 하 고 hello 필요한 처리량 또는 필요한 작업 속도 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="679ee-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="679ee-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="679ee-142">Next steps</span></span>
<span data-ttu-id="679ee-143">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="679ee-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="679ee-144">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="679ee-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="679ee-145">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="679ee-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
