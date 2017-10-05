---
title: "Azure IoT Hub 크기 조정 | Microsoft Docs"
description: "예상된 메시지 처리량을 지원하도록 IoT hub를 확장하는 방법입니다. 분할을 위한 옵션 및 각 계층에 지원되는 처리량에 대한 요약을 포함합니다."
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
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="53a31-104">IoT Hub 솔루션 크기 조정</span><span class="sxs-lookup"><span data-stu-id="53a31-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="53a31-105">Azure IoT Hub는 동시에 최대 백만 개의 연결된 장치를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="53a31-106">자세한 내용은 [IoT Hub 가격 책정][lnk-pricing]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53a31-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="53a31-107">각 IoT Hub 단위는 특정 개수의 일일 메시지를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="53a31-108">솔루션의 규모를 적절히 조정하려면 IoT Hub의 특정 용도를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="53a31-109">특히 다음과 같은 범주의 작업에 필요한 최대 처리량을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="53a31-110">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="53a31-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="53a31-111">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="53a31-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="53a31-112">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="53a31-112">Identity registry operations</span></span>

<span data-ttu-id="53a31-113">이 처리량 정보 외에도 [IoT Hub 할당량 및 제한][IoT Hub quotas and throttles]을 참조하고 솔루션을 적절히 디자인하세요.</span><span class="sxs-lookup"><span data-stu-id="53a31-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="53a31-114">장치-클라우드 및 클라우드-장치 메시지 처리량</span><span class="sxs-lookup"><span data-stu-id="53a31-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="53a31-115">IoT Hub 솔루션의 크기를 조정하는 가장 적절한 방법은 장치별로 트래픽을 평가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="53a31-116">장치-클라우드 메시지는 다음과 같은 지속적인 처리량 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="53a31-117">계층</span><span class="sxs-lookup"><span data-stu-id="53a31-117">Tier</span></span> | <span data-ttu-id="53a31-118">지속적인 처리량</span><span class="sxs-lookup"><span data-stu-id="53a31-118">Sustained throughput</span></span> | <span data-ttu-id="53a31-119">지속적인 전송 속도</span><span class="sxs-lookup"><span data-stu-id="53a31-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="53a31-120">S1</span><span class="sxs-lookup"><span data-stu-id="53a31-120">S1</span></span> |<span data-ttu-id="53a31-121">장치당 최대 1111KB/분</span><span class="sxs-lookup"><span data-stu-id="53a31-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="53a31-122">(1.5GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="53a31-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="53a31-123">장치당 평균 278메시지/분</span><span class="sxs-lookup"><span data-stu-id="53a31-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="53a31-124">(400,000메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="53a31-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="53a31-125">S2</span><span class="sxs-lookup"><span data-stu-id="53a31-125">S2</span></span> |<span data-ttu-id="53a31-126">장치당 최대 16MB/분</span><span class="sxs-lookup"><span data-stu-id="53a31-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="53a31-127">(22.8GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="53a31-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="53a31-128">장치당 평균 4,167개 메시지/분</span><span class="sxs-lookup"><span data-stu-id="53a31-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="53a31-129">(6백만 개의 메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="53a31-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="53a31-130">S3</span><span class="sxs-lookup"><span data-stu-id="53a31-130">S3</span></span> |<span data-ttu-id="53a31-131">장치당 최대 814MB/분</span><span class="sxs-lookup"><span data-stu-id="53a31-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="53a31-132">(1144.4GB/일/장치)</span><span class="sxs-lookup"><span data-stu-id="53a31-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="53a31-133">장치당 평균 208,333 메시지/분</span><span class="sxs-lookup"><span data-stu-id="53a31-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="53a31-134">(3억 개의 메시지/일/장치당)</span><span class="sxs-lookup"><span data-stu-id="53a31-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="53a31-135">ID 레지스트리 작업 처리량</span><span class="sxs-lookup"><span data-stu-id="53a31-135">Identity registry operation throughput</span></span>
<span data-ttu-id="53a31-136">IoT Hub ID 레지스트리 작업은 대부분이 장치 프로비전과 관련되므로 런타임 작업으로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="53a31-137">관련 버스트 성능 수치는 [IoT Hub 할당량 및 제한][IoT Hub quotas and throttles]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53a31-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="53a31-138">분할</span><span class="sxs-lookup"><span data-stu-id="53a31-138">Sharding</span></span>
<span data-ttu-id="53a31-139">단일 IoT Hub를 수백만 대의 장치로 확장할 수 있기는 하지만, 솔루션에서 단일 IoT Hub에서 보장할 수 없는 특정 성능 특성을 필요로 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="53a31-140">이 경우 여러 IoT Hub로 장치를 분할하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="53a31-141">여러 IoT Hub가 갑작스러운 트래픽 증가를 원활하게 처리하고 필요한 처리량 또는 필요한 작업 속도를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="53a31-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53a31-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53a31-142">Next steps</span></span>
<span data-ttu-id="53a31-143">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53a31-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="53a31-144">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="53a31-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="53a31-145">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="53a31-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
