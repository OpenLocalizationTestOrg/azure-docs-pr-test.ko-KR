---
title: "Azure IoT Hub 가격 책정 이해 | Microsoft Docs"
description: "개발자 가이드 - 작동 예제를 비롯하여 IoT Hub에서 측정 및 가격 책정이 진행되는 방식에 대한 정보를 제공합니다."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: 3470473e1b2aa107c32643a66092b68bfafd1a37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-pricing-information"></a><span data-ttu-id="000eb-103">Azure IoT Hub 가격 책정 정보</span><span class="sxs-lookup"><span data-stu-id="000eb-103">Azure IoT Hub pricing information</span></span>

<span data-ttu-id="000eb-104">[Azure IoT Hub 가격 책정][lnk-pricing]에서는 IoT Hub에 대한 기타 SKU 및 가격 책정에 대한 일반적인 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-104">[Azure IoT Hub pricing][lnk-pricing] provides the general information on different SKUs and pricing for IoT Hub.</span></span> <span data-ttu-id="000eb-105">이 문서에서는 IoT Hub에서 다양한 IoT Hub 기능이 메시지로 측정되는 방식에 대한 자세한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-105">This article contains additional details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>

## <a name="charges-per-operation"></a><span data-ttu-id="000eb-106">작업당 요금</span><span class="sxs-lookup"><span data-stu-id="000eb-106">Charges per operation</span></span>

| <span data-ttu-id="000eb-107">작업</span><span class="sxs-lookup"><span data-stu-id="000eb-107">Operation</span></span> | <span data-ttu-id="000eb-108">대금 청구 정보</span><span class="sxs-lookup"><span data-stu-id="000eb-108">Billing information</span></span> | 
| --------- | ------------------- |
| <span data-ttu-id="000eb-109">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="000eb-109">Identity registry operations</span></span> <br/> <span data-ttu-id="000eb-110">(만들기, 검색, 목록, 업데이트, 삭제)</span><span class="sxs-lookup"><span data-stu-id="000eb-110">(create, retrieve, list, update, delete)</span></span> | <span data-ttu-id="000eb-111">요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-111">Not charged.</span></span> |
| <span data-ttu-id="000eb-112">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="000eb-112">Device-to-cloud messages</span></span> | <span data-ttu-id="000eb-113">IoT Hub에 수신 시, 성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-113">Successfully sent messages are charged in 4-KB chunks on ingress into IoT Hub, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="000eb-114">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="000eb-114">Cloud-to-device messages</span></span> | <span data-ttu-id="000eb-115">성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-115">Successfully sent messages are charged in 4-KB chunks, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="000eb-116">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="000eb-116">File uploads</span></span> | <span data-ttu-id="000eb-117">Azure Storage에 대한 파일 전송은 IoT Hub에서 측정되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-117">File transfer to Azure Storage is not metered by IoT Hub.</span></span> <span data-ttu-id="000eb-118">파일 전송 시작 및 완료 메시지는 4KB 증분으로 측정되어 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-118">File transfer initiation and completion messages are charged as messaged metered in 4-KB increments.</span></span> <span data-ttu-id="000eb-119">예를 들어 10MB 파일을 전송하는 경우 Azure Storage 비용 외에 2개의 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-119">For instance, transferring a 10-MB file is charged two messages in addition to the Azure Storage cost.</span></span> |
| <span data-ttu-id="000eb-120">직접 메서드</span><span class="sxs-lookup"><span data-stu-id="000eb-120">Direct methods</span></span> | <span data-ttu-id="000eb-121">성공적인 메서드 요청은 4KB 청크 단위로 요금이 청구됩니다. 본문이 비어 있지 않은 응답은 추가 메시지로서 4KB 단위로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-121">Successful method requests are charged in 4-KB chunks, responses with non-empty bodies are charged in 4-KB as additional messages.</span></span> <span data-ttu-id="000eb-122">연결이 끊긴 장치에 대한 요청은 4KB 청크 단위 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-122">Requests to disconnected devices are charged as messages in 4-KB chunks.</span></span> <span data-ttu-id="000eb-123">예를 들어 본문이 없는 장치 응답을 초래하는 6KB 본문의 메서드는 2개 메시지로 요금이 청구됩니다. 1KB의 장치 응답을 초래하는 6KB 본문의 메서드는 요청에 해당하는 2개 메시지와 응답에 대한 2개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-123">For instance, a method with a 6-KB body that results in a response with no body from the device, is charged as two messages; a method with a 6-KB body that results in a 1-KB response from the device is charged as two messages for the request plus another message for the response.</span></span> |
| <span data-ttu-id="000eb-124">장치 쌍 읽기</span><span class="sxs-lookup"><span data-stu-id="000eb-124">Device twin reads</span></span> | <span data-ttu-id="000eb-125">장치 및 솔루션 백 엔드에서의 장치 쌍 읽기는 512바이트 청크 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-125">Device twin reads from the device and from the solution back end are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="000eb-126">예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-126">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="000eb-127">장치 쌍 업데이트(태그 및 속성)</span><span class="sxs-lookup"><span data-stu-id="000eb-127">Device twin updates (tags and properties)</span></span> | <span data-ttu-id="000eb-128">두 장치에서의 장치 쌍 읽기는 512바이트 청크 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-128">Device twin updates from the device and the device are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="000eb-129">예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-129">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="000eb-130">장치 쌍 쿼리</span><span class="sxs-lookup"><span data-stu-id="000eb-130">Device twin queries</span></span> | <span data-ttu-id="000eb-131">쿼리는 결과 크기에 따라 512바이트 청크 단위 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-131">Queries are charged as messages depending on the result size in 512-byte chunks.</span></span> |
| <span data-ttu-id="000eb-132">작업 연산</span><span class="sxs-lookup"><span data-stu-id="000eb-132">Jobs operations</span></span> <br/> <span data-ttu-id="000eb-133">(만들기, 업데이트, 나열, 삭제)</span><span class="sxs-lookup"><span data-stu-id="000eb-133">(create, update, list, delete)</span></span> | <span data-ttu-id="000eb-134">요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-134">Not charged.</span></span> |
| <span data-ttu-id="000eb-135">장치 단위 작업 연산</span><span class="sxs-lookup"><span data-stu-id="000eb-135">Jobs per-device operations</span></span> | <span data-ttu-id="000eb-136">작업 연산(예: 장치 쌍 업데이트 및 메서드)은 정상적으로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-136">Jobs operations (such as device twin updates, and methods) are charged as normal.</span></span> <span data-ttu-id="000eb-137">예를 들어 1000개 메서드 호출로 1KB 요청 및 비어 있는 본문 응답을 야기하는 작업은 1000개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-137">For instance, a job resulting in 1000 method calls with 1-KB requests and empty-body responses is charged 1000 messages.</span></span> |

> [!NOTE]
> <span data-ttu-id="000eb-138">모든 크기는 바이트 단위의 페이로드 크기를 고려해서 계산됩니다(프로토콜 프레이밍은 무시됨).</span><span class="sxs-lookup"><span data-stu-id="000eb-138">All sizes are computed considering the payload size in bytes (protocol framing is ignored).</span></span> <span data-ttu-id="000eb-139">메시지(속성 및 본문 포함)의 경우 크기는 [IoT Hub 메시징 개발자 가이드][lnk-message-size]에 설명된 대로 프로토콜 독립적인 방식으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-139">In case of messages (which have properties and body) the size is computed in a protocol-agnostic way, as described in the [IoT Hub messaging developer's guide][lnk-message-size].</span></span>

## <a name="example-1"></a><span data-ttu-id="000eb-140">예제 1</span><span class="sxs-lookup"><span data-stu-id="000eb-140">Example #1</span></span>

<span data-ttu-id="000eb-141">장치가 분당 1개의 1KB 장치-클라우드 메시지를 IoT Hub로 전송하면 Azure Stream Analytics에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-141">A device sends one 1-KB device-to-cloud message per minute to IoT Hub, which is then read by Azure Stream Analytics.</span></span> <span data-ttu-id="000eb-142">솔루션 백 엔드는 10분 간격으로 장치에서 메서드(512바이트 페이로드)를 호출하여 특정 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-142">The solution back end invokes a method (with 512-byte payload) on the device every ten minutes to trigger a specific action.</span></span> <span data-ttu-id="000eb-143">장치는 200바이트의 결과로 메서드에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-143">The device responds to the method with a result of 200 bytes.</span></span>

<span data-ttu-id="000eb-144">장치는 장치-클라우드 메시지에 대해 하루에 1개의 메시지 * 60분 * 24시간 = 1440개 메시지를 사용하고, 메서드에 대해 2개의 요청 + 응답 * 시간당 6번 * 24시간 = 288개 메시지, 하루에 총 1728개의 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-144">The device consumes 1 message * 60 minutes * 24 hours = 1440 messages per day for the device-to-cloud messages, and 2 request plus response * 6 times per hour * 24 hours = 288 messages for the methods, for a total of 1728 messages per day.</span></span>

## <a name="example-2"></a><span data-ttu-id="000eb-145">예제 2</span><span class="sxs-lookup"><span data-stu-id="000eb-145">Example #2</span></span>

<span data-ttu-id="000eb-146">장치는 1시간마다 하나의 100KB 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-146">A device sends one 100-KB device-to-cloud message every hour.</span></span> <span data-ttu-id="000eb-147">또한 4시간마다 1KB 페이로드로 장치 쌍을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-147">It also updates its device twin with 1-KB payloads every 4 hours.</span></span> <span data-ttu-id="000eb-148">솔루션 백 엔드는 하루에 1번, 14KB의 장치 쌍을 읽고 512바이트 페이로드로 업데이트하여 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-148">The solution back end, once per day, reads the 14-KB device twin and updates it with 512-byte payloads to change configurations.</span></span>

<span data-ttu-id="000eb-149">장치는 장치-클라우드 메시지에 대해 25개(100KB/4KB) 메시지 * 24시간을 사용하고, 장치 쌍 업데이트에 대해 하루에 1개 메시지 * 6번, 하루에 총 156개 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-149">The device consumes 25 (100KB / 4KB) messages * 24 hours for device-to-cloud messages, plus 1 message * 6 times per day for device twin updates, for a total of 156 messages per day.</span></span>
<span data-ttu-id="000eb-150">솔루션 백 엔드는 장치 쌍을 읽기 위한 28개 메시지(14KB/0.5KB)와 업데이트하기 위한 1개 메시지, 총 29개의 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-150">The solution back end consumes 28 messages (14KB / 0.5KB) to read the device twin, plus 1 message to update it, for a total of 29 messages.</span></span>

<span data-ttu-id="000eb-151">전체적으로 장치 및 솔루션 백 엔드는 하루에 185개 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="000eb-151">In total, the device and the solution back end consume 185 messages per day.</span></span>


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
