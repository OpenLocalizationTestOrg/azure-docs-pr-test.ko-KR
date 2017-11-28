---
title: "Azure IoT Hub 클라우드-장치 옵션 | Microsoft Docs"
description: "개발자 가이드 - 직접 메서드, 장치 쌍의 desired 속성 또는 클라우드-장치 통신을 위한 클라우드-장치 메시지를 사용하는 경우에 대한 지침입니다."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: e6cd4880c9bfcc670bd116d3dd8e5245d70f85cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-to-device-communications-guidance"></a><span data-ttu-id="cc07f-103">클라우드-장치 통신 지침</span><span class="sxs-lookup"><span data-stu-id="cc07f-103">Cloud-to-device communications guidance</span></span>
<span data-ttu-id="cc07f-104">IoT Hub는 백 엔드 앱에 기능을 공개하는 세 가지 옵션을 장치 앱에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-104">IoT Hub provides three options for device apps to expose functionality to a back-end app:</span></span>

* <span data-ttu-id="cc07f-105">[직접 메서드][lnk-methods] 결과를 즉시 확인해야 하는 통신의 경우</span><span class="sxs-lookup"><span data-stu-id="cc07f-105">[Direct methods][lnk-methods] for communications that require immediate confirmation of the result.</span></span> <span data-ttu-id="cc07f-106">대화형 장치 제어(예: 선풍기 켜기)에 대해 직접 메서드를 자주 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-106">Direct methods are often used for interactive control of devices such as turning on a fan.</span></span>
* <span data-ttu-id="cc07f-107">[쌍의 원하는 속성][lnk-twins] 장치를 원하는 특정 상태로 만들려는 장기 실행 명령의 경우</span><span class="sxs-lookup"><span data-stu-id="cc07f-107">[Twin's desired properties][lnk-twins] for long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="cc07f-108">예를 들어 원격 분석 송신 간격을 30분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-108">For example, set the telemetry send interval to 30 minutes.</span></span>
* <span data-ttu-id="cc07f-109">[클라우드-장치 메시지][lnk-c2d] 장치 앱에 대한 단방향 알림의 경우</span><span class="sxs-lookup"><span data-stu-id="cc07f-109">[Cloud-to-device messages][lnk-c2d] for one-way notifications to the device app.</span></span>

<span data-ttu-id="cc07f-110">다음은 다양한 클라우드-장치 통신 옵션에 대해 자세히 비교하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-110">Here is a detailed comparison of the various cloud-to-device communication options.</span></span>

|  | <span data-ttu-id="cc07f-111">직접 메서드</span><span class="sxs-lookup"><span data-stu-id="cc07f-111">Direct methods</span></span> | <span data-ttu-id="cc07f-112">쌍의 desired 속성</span><span class="sxs-lookup"><span data-stu-id="cc07f-112">Twin's desired properties</span></span> | <span data-ttu-id="cc07f-113">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="cc07f-113">Cloud-to-device messages</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="cc07f-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="cc07f-114">Scenario</span></span> | <span data-ttu-id="cc07f-115">즉각적인 확인이 필요한 명령(예: 팬 작동)</span><span class="sxs-lookup"><span data-stu-id="cc07f-115">Commands that require immediate confirmation, such as turning on a fan.</span></span> | <span data-ttu-id="cc07f-116">장치를 원하는 상태로 만들려는 장기 실행 명령.</span><span class="sxs-lookup"><span data-stu-id="cc07f-116">Long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="cc07f-117">예를 들어 원격 분석 송신 간격을 30분으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-117">For example, set the telemetry send interval to 30 minutes.</span></span> | <span data-ttu-id="cc07f-118">장치 앱에 대한 단방향 알림</span><span class="sxs-lookup"><span data-stu-id="cc07f-118">One-way notifications to the device app.</span></span> |
| <span data-ttu-id="cc07f-119">데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="cc07f-119">Data flow</span></span> | <span data-ttu-id="cc07f-120">양방향.</span><span class="sxs-lookup"><span data-stu-id="cc07f-120">Two-way.</span></span> <span data-ttu-id="cc07f-121">장치 앱에서 메서드에 즉시 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-121">The device app can respond to the method right away.</span></span> <span data-ttu-id="cc07f-122">솔루션 백 엔드에서 컨텍스트에 따라 요청에 대한 결과를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-122">The solution back end receives the outcome contextually to the request.</span></span> | <span data-ttu-id="cc07f-123">단방향.</span><span class="sxs-lookup"><span data-stu-id="cc07f-123">One-way.</span></span> <span data-ttu-id="cc07f-124">장치 앱에서 속성 변경 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-124">The device app receives a notification with the property change.</span></span> | <span data-ttu-id="cc07f-125">단방향.</span><span class="sxs-lookup"><span data-stu-id="cc07f-125">One-way.</span></span> <span data-ttu-id="cc07f-126">장치 앱에서 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-126">The device app receives the message</span></span>
| <span data-ttu-id="cc07f-127">내구성</span><span class="sxs-lookup"><span data-stu-id="cc07f-127">Durability</span></span> | <span data-ttu-id="cc07f-128">연결이 끊긴 장치는 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-128">Disconnected devices are not contacted.</span></span> <span data-ttu-id="cc07f-129">장치가 연결되어 있지 않다고 솔루션 백 엔드에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-129">The solution back end is notified that the device is not connected.</span></span> | <span data-ttu-id="cc07f-130">속성 값은 장치 쌍에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-130">Property values are preserved in the device twin.</span></span> <span data-ttu-id="cc07f-131">다음에 다시 연결할 때 장치에서 이 알림을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-131">Device will read it at next reconnection.</span></span> <span data-ttu-id="cc07f-132">속성 값은 [IoT Hub 쿼리 언어][lnk-query]로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-132">Property values are retrievable with the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="cc07f-133">메시지는 최대 48시간 동안 IoT Hub에 보관될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-133">Messages can be retained by IoT Hub for up to 48 hours.</span></span> |
| <span data-ttu-id="cc07f-134">대상</span><span class="sxs-lookup"><span data-stu-id="cc07f-134">Targets</span></span> | <span data-ttu-id="cc07f-135">**deviceId**를 사용하는 단일 장치 또는 [jobs][lnk-jobs]를 사용하는 여러 장치</span><span class="sxs-lookup"><span data-stu-id="cc07f-135">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="cc07f-136">**deviceId**를 사용하는 단일 장치 또는 [jobs][lnk-jobs]를 사용하는 여러 장치</span><span class="sxs-lookup"><span data-stu-id="cc07f-136">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="cc07f-137">**deviceId**를 사용하는 단일 장치</span><span class="sxs-lookup"><span data-stu-id="cc07f-137">Single device by **deviceId**.</span></span> |
| <span data-ttu-id="cc07f-138">크기</span><span class="sxs-lookup"><span data-stu-id="cc07f-138">Size</span></span> | <span data-ttu-id="cc07f-139">최대 8KB 요청 및 최대 8KB 응답</span><span class="sxs-lookup"><span data-stu-id="cc07f-139">Up to 8KB requests and 8KB responses.</span></span> | <span data-ttu-id="cc07f-140">최대 desired 속성 크기는 8KB입니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-140">Maximum desired properties size is 8KB.</span></span> | <span data-ttu-id="cc07f-141">최대 64KB 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-141">Up to 64KB messages.</span></span> |
| <span data-ttu-id="cc07f-142">Frequency(빈도)</span><span class="sxs-lookup"><span data-stu-id="cc07f-142">Frequency</span></span> | <span data-ttu-id="cc07f-143">높음.</span><span class="sxs-lookup"><span data-stu-id="cc07f-143">High.</span></span> <span data-ttu-id="cc07f-144">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc07f-144">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="cc07f-145">중간.</span><span class="sxs-lookup"><span data-stu-id="cc07f-145">Medium.</span></span> <span data-ttu-id="cc07f-146">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc07f-146">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="cc07f-147">낮음.</span><span class="sxs-lookup"><span data-stu-id="cc07f-147">Low.</span></span> <span data-ttu-id="cc07f-148">자세한 내용은 [IoT Hub 제한][lnk-quotas]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc07f-148">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="cc07f-149">프로토콜</span><span class="sxs-lookup"><span data-stu-id="cc07f-149">Protocol</span></span> | <span data-ttu-id="cc07f-150">현재 MQTT를 사용할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-150">Currently available only when using MQTT.</span></span> | <span data-ttu-id="cc07f-151">현재 MQTT를 사용할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-151">Currently available only when using MQTT.</span></span> | <span data-ttu-id="cc07f-152">모든 프로토콜에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-152">Available on all protocols.</span></span> <span data-ttu-id="cc07f-153">HTTP를 사용할 경우 장치에서 폴링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc07f-153">Device must poll when using HTTP.</span></span> |

<span data-ttu-id="cc07f-154">다음 자습서에서 직접 메서드, desired 속성 및 클라우드-장치 메시지를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cc07f-154">Learn how to use direct methods, desired properties, and cloud-to-device messages in the following tutorials:</span></span>

* <span data-ttu-id="cc07f-155">[직접 메서드 사용][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc07f-155">[Use direct methods][lnk-methods-tutorial], for direct methods;</span></span>
* <span data-ttu-id="cc07f-156">장치 쌍의 desired 속성에 대해 [desired 속성을 사용하여 장치 구성][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="cc07f-156">[Use desired properties to configure devices][lnk-twin-properties], for device twin's desired properties;</span></span> 
* <span data-ttu-id="cc07f-157">[클라우드-장치 메시지 보내기][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="cc07f-157">[Send cloud-to-device messages][lnk-c2d-tutorial], for cloud-to-device messages.</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
