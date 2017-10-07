---
title: "Azure IoT 허브 가격 책정 aaaUnderstand | Microsoft Docs"
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
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a><span data-ttu-id="f58af-103">Azure IoT Hub 가격 책정 정보</span><span class="sxs-lookup"><span data-stu-id="f58af-103">Azure IoT Hub pricing information</span></span>

<span data-ttu-id="f58af-104">[Azure IoT 허브 가격 책정] [ lnk-pricing] 다른 Sku 및 IoT 허브에 대 한 가격 책정에 hello 일반 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-104">[Azure IoT Hub pricing][lnk-pricing] provides hello general information on different SKUs and pricing for IoT Hub.</span></span> <span data-ttu-id="f58af-105">이 문서는 IoT 허브에서 IoT Hub에 다양 한 기능으로 요금이 부과 되며 hello 메시지 하는 방법을 대 한 자세한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-105">This article contains additional details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>

## <a name="charges-per-operation"></a><span data-ttu-id="f58af-106">작업당 요금</span><span class="sxs-lookup"><span data-stu-id="f58af-106">Charges per operation</span></span>

| <span data-ttu-id="f58af-107">작업</span><span class="sxs-lookup"><span data-stu-id="f58af-107">Operation</span></span> | <span data-ttu-id="f58af-108">대금 청구 정보</span><span class="sxs-lookup"><span data-stu-id="f58af-108">Billing information</span></span> | 
| --------- | ------------------- |
| <span data-ttu-id="f58af-109">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="f58af-109">Identity registry operations</span></span> <br/> <span data-ttu-id="f58af-110">(만들기, 검색, 목록, 업데이트, 삭제)</span><span class="sxs-lookup"><span data-stu-id="f58af-110">(create, retrieve, list, update, delete)</span></span> | <span data-ttu-id="f58af-111">요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-111">Not charged.</span></span> |
| <span data-ttu-id="f58af-112">장치-클라우드 메시지</span><span class="sxs-lookup"><span data-stu-id="f58af-112">Device-to-cloud messages</span></span> | <span data-ttu-id="f58af-113">IoT Hub에 수신 시, 성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-113">Successfully sent messages are charged in 4-KB chunks on ingress into IoT Hub, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="f58af-114">클라우드-장치 메시지</span><span class="sxs-lookup"><span data-stu-id="f58af-114">Cloud-to-device messages</span></span> | <span data-ttu-id="f58af-115">성공적으로 전송된 메시지는 4KB 청크 단위로 요금이 청구됩니다. 예를 들어 6KB 메시지에는 2개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-115">Successfully sent messages are charged in 4-KB chunks, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="f58af-116">파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f58af-116">File uploads</span></span> | <span data-ttu-id="f58af-117">IoT Hub에서 파일 전송 tooAzure 저장소 유료일 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-117">File transfer tooAzure Storage is not metered by IoT Hub.</span></span> <span data-ttu-id="f58af-118">파일 전송 시작 및 완료 메시지는 4KB 증분으로 측정되어 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-118">File transfer initiation and completion messages are charged as messaged metered in 4-KB increments.</span></span> <span data-ttu-id="f58af-119">예를 들어 10MB 파일 전송 더하기 toohello Azure 저장소 비용을에서 두 개의 메시지 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-119">For instance, transferring a 10-MB file is charged two messages in addition toohello Azure Storage cost.</span></span> |
| <span data-ttu-id="f58af-120">직접 메서드</span><span class="sxs-lookup"><span data-stu-id="f58af-120">Direct methods</span></span> | <span data-ttu-id="f58af-121">성공적인 메서드 요청은 4KB 청크 단위로 요금이 청구됩니다. 본문이 비어 있지 않은 응답은 추가 메시지로서 4KB 단위로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-121">Successful method requests are charged in 4-KB chunks, responses with non-empty bodies are charged in 4-KB as additional messages.</span></span> <span data-ttu-id="f58af-122">요청 toodisconnected 장치 4KB 청크로 메시지로 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-122">Requests toodisconnected devices are charged as messages in 4-KB chunks.</span></span> <span data-ttu-id="f58af-123">응답 본문이 없는 hello 장치에서 발생 하는 6 KB 본문이 있는 메서드를; 두 개의 메시지로 요금이 부과 됩니다 예를 들어, 1KB 응답 hello 장치에서 발생 하는 6 KB 본문이 있는 메서드는 hello 요청에 대 한 두 개의 메시지 + hello 응답에 대 한 다른 메시지도 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-123">For instance, a method with a 6-KB body that results in a response with no body from hello device, is charged as two messages; a method with a 6-KB body that results in a 1-KB response from hello device is charged as two messages for hello request plus another message for hello response.</span></span> |
| <span data-ttu-id="f58af-124">장치 쌍 읽기</span><span class="sxs-lookup"><span data-stu-id="f58af-124">Device twin reads</span></span> | <span data-ttu-id="f58af-125">장치로 이중 읽고 hello 장치에서 다시 hello 솔루션에서 끝 512 바이트 청크에서 메시지로 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-125">Device twin reads from hello device and from hello solution back end are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="f58af-126">예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-126">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="f58af-127">장치 쌍 업데이트(태그 및 속성)</span><span class="sxs-lookup"><span data-stu-id="f58af-127">Device twin updates (tags and properties)</span></span> | <span data-ttu-id="f58af-128">Hello 장치와 hello 장치에서 장치로 이중 업데이트는 512 바이트 청크에서 메시지로 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-128">Device twin updates from hello device and hello device are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="f58af-129">예를 들어 6KB 장치 쌍 읽기는 12개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-129">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="f58af-130">장치 쌍 쿼리</span><span class="sxs-lookup"><span data-stu-id="f58af-130">Device twin queries</span></span> | <span data-ttu-id="f58af-131">쿼리는 512 바이트 청크에서 hello 결과 크기에 따라 메시지로 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-131">Queries are charged as messages depending on hello result size in 512-byte chunks.</span></span> |
| <span data-ttu-id="f58af-132">작업 연산</span><span class="sxs-lookup"><span data-stu-id="f58af-132">Jobs operations</span></span> <br/> <span data-ttu-id="f58af-133">(만들기, 업데이트, 나열, 삭제)</span><span class="sxs-lookup"><span data-stu-id="f58af-133">(create, update, list, delete)</span></span> | <span data-ttu-id="f58af-134">요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-134">Not charged.</span></span> |
| <span data-ttu-id="f58af-135">장치 단위 작업 연산</span><span class="sxs-lookup"><span data-stu-id="f58af-135">Jobs per-device operations</span></span> | <span data-ttu-id="f58af-136">작업 연산(예: 장치 쌍 업데이트 및 메서드)은 정상적으로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-136">Jobs operations (such as device twin updates, and methods) are charged as normal.</span></span> <span data-ttu-id="f58af-137">예를 들어 1000개 메서드 호출로 1KB 요청 및 비어 있는 본문 응답을 야기하는 작업은 1000개 메시지로 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-137">For instance, a job resulting in 1000 method calls with 1-KB requests and empty-body responses is charged 1000 messages.</span></span> |

> [!NOTE]
> <span data-ttu-id="f58af-138">모든 규모 고려 hello 페이로드 크기 바이트 (프레이밍 프로토콜은 무시 됨)으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-138">All sizes are computed considering hello payload size in bytes (protocol framing is ignored).</span></span> <span data-ttu-id="f58af-139">메시지 (포함 하는 속성 및 본문)의 경우 hello 크기는 계산 프로토콜을 알 수 없는 방식으로 hello에 설명 된 대로 [IoT 허브 개발자 가이드 메시징][lnk-message-size]합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-139">In case of messages (which have properties and body) hello size is computed in a protocol-agnostic way, as described in hello [IoT Hub messaging developer's guide][lnk-message-size].</span></span>

## <a name="example-1"></a><span data-ttu-id="f58af-140">예제 1</span><span class="sxs-lookup"><span data-stu-id="f58af-140">Example #1</span></span>

<span data-ttu-id="f58af-141">장치 분 tooIoT 허브와 Azure Stream Analytics를 읽은 다음 당 하나의 1KB 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-141">A device sends one 1-KB device-to-cloud message per minute tooIoT Hub, which is then read by Azure Stream Analytics.</span></span> <span data-ttu-id="f58af-142">hello 솔루션 백 엔드 메서드 호출 (페이로드를 사용한 512 바이트) hello 장치에 모든 10 분 tootrigger 특정 작업.</span><span class="sxs-lookup"><span data-stu-id="f58af-142">hello solution back end invokes a method (with 512-byte payload) on hello device every ten minutes tootrigger a specific action.</span></span> <span data-ttu-id="f58af-143">hello 장치 toohello 메서드 200 바이트의 결과 함께 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-143">hello device responds toohello method with a result of 200 bytes.</span></span>

<span data-ttu-id="f58af-144">hello 장치가 소비 가능 메시지 1 개 * 60 분 * 24 시간 = hello 장치-클라우드 메시지 2 요청 및 응답에 대 한 하루 1440 메시지 * 시간당 6 번 * 24 시간 = 288 하루 1728 메시지의 총 hello 방법에 대 한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-144">hello device consumes 1 message * 60 minutes * 24 hours = 1440 messages per day for hello device-to-cloud messages, and 2 request plus response * 6 times per hour * 24 hours = 288 messages for hello methods, for a total of 1728 messages per day.</span></span>

## <a name="example-2"></a><span data-ttu-id="f58af-145">예제 2</span><span class="sxs-lookup"><span data-stu-id="f58af-145">Example #2</span></span>

<span data-ttu-id="f58af-146">장치는 1시간마다 하나의 100KB 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-146">A device sends one 100-KB device-to-cloud message every hour.</span></span> <span data-ttu-id="f58af-147">또한 4시간마다 1KB 페이로드로 장치 쌍을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-147">It also updates its device twin with 1-KB payloads every 4 hours.</span></span> <span data-ttu-id="f58af-148">hello 다시 하루에 한 번 읽기 hello 14 KB 장치로 이중 종료 솔루션과 512 바이트 페이로드 toochange 구성으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-148">hello solution back end, once per day, reads hello 14-KB device twin and updates it with 512-byte payloads toochange configurations.</span></span>

<span data-ttu-id="f58af-149">25 (100KB/4KB) 메시지를 사용 하는 hello 장치 * 24 시간 동안 장치-클라우드 메시지와 메시지 1 개 * 6 회 하루 장치로 이중 업데이트에 대 한 하루 156 메시지의 총 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-149">hello device consumes 25 (100KB / 4KB) messages * 24 hours for device-to-cloud messages, plus 1 message * 6 times per day for device twin updates, for a total of 156 messages per day.</span></span>
<span data-ttu-id="f58af-150">hello 솔루션 백 엔드 소비 28 메시지 (KB 14 KB/0.5) tooread hello 장치로 이중 플러스 1 인 메시지 tooupdate 29 메시지의 총 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-150">hello solution back end consumes 28 messages (14KB / 0.5KB) tooread hello device twin, plus 1 message tooupdate it, for a total of 29 messages.</span></span>

<span data-ttu-id="f58af-151">전체적으로 hello 장치와 hello 솔루션 백 엔드 하루 185 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f58af-151">In total, hello device and hello solution back end consume 185 messages per day.</span></span>


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
