---
title: "Azure IoT Hub ID 레지스트리 이해 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub ID 레지스트리 및 장치 관리에 레지스트리를 사용하는 방법 설명 대량으로 장치 ID 가져오기 및 내보내기에 대한 정보를 포함합니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6e9c7b71fa6fc78f97c0144c735fc44778181d8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="understand-the-identity-registry-in-your-iot-hub"></a><span data-ttu-id="21b63-104">IoT Hub의 ID 레지스트리 이해</span><span class="sxs-lookup"><span data-stu-id="21b63-104">Understand the identity registry in your IoT hub</span></span>

<span data-ttu-id="21b63-105">모든 IoT Hub에는 IoT Hub에 연결이 허용된 장치에 대한 정보를 저장하는 ID 레지스트리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-105">Every IoT hub has an identity registry that stores information about the devices permitted to connect to the IoT hub.</span></span> <span data-ttu-id="21b63-106">장치를 IoT Hub에 연결할 수 있으려면 IoT Hub의 ID 레지스트리에 해당 장치에 대한 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-106">Before a device can connect to an IoT hub, there must be an entry for that device in the IoT hub's identity registry.</span></span> <span data-ttu-id="21b63-107">또한 장치는 ID 레지스트리에 저장된 자격 증명에 따라 IoT Hub로 인증되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-107">A device must also authenticate with the IoT hub based on credentials stored in the identity registry.</span></span>

<span data-ttu-id="21b63-108">ID 레지스트리에 저장된 장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-108">The device ID stored in the identity registry is case-sensitive.</span></span>

<span data-ttu-id="21b63-109">높은 수준에서 ID 레지스트리는 장치 ID 리소스의 REST를 지원하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-109">At a high level, the identity registry is a REST-capable collection of device identity resources.</span></span> <span data-ttu-id="21b63-110">ID 레지스트리에 항목을 추가하면 IoT Hub가 진행 중인 클라우드-장치 메시지를 포함하는 큐 등의 장치별 리소스 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-110">When you add an entry in the identity registry, IoT Hub creates a set of per-device resources such as the queue that contains in-flight cloud-to-device messages.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="21b63-111">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="21b63-111">When to use</span></span>

<span data-ttu-id="21b63-112">다음과 같은 작업이 필요할 때 ID 레지스트리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-112">Use the identity registry when you need to:</span></span>

* <span data-ttu-id="21b63-113">IoT Hub에 연결되는 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-113">Provision devices that connect to your IoT hub.</span></span>
* <span data-ttu-id="21b63-114">허브의 장치 지향 끝점에 대한 장치별 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-114">Control per-device access to your hub's device-facing endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="21b63-115">ID 레지스트리에는 응용 프로그램별 메타데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-115">The identity registry does not contain any application-specific metadata.</span></span>

## <a name="identity-registry-operations"></a><span data-ttu-id="21b63-116">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="21b63-116">Identity registry operations</span></span>

<span data-ttu-id="21b63-117">IoT Hub ID 레지스트리는 다음과 같은 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-117">The IoT Hub identity registry exposes the following operations:</span></span>

* <span data-ttu-id="21b63-118">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="21b63-118">Create device identity</span></span>
* <span data-ttu-id="21b63-119">장치 ID 업데이트</span><span class="sxs-lookup"><span data-stu-id="21b63-119">Update device identity</span></span>
* <span data-ttu-id="21b63-120">ID로 장치 ID 검색</span><span class="sxs-lookup"><span data-stu-id="21b63-120">Retrieve device identity by ID</span></span>
* <span data-ttu-id="21b63-121">장치 ID 삭제</span><span class="sxs-lookup"><span data-stu-id="21b63-121">Delete device identity</span></span>
* <span data-ttu-id="21b63-122">최대 1000개의 ID 목록</span><span class="sxs-lookup"><span data-stu-id="21b63-122">List up to 1000 identities</span></span>
* <span data-ttu-id="21b63-123">모든 ID를 Azure Blob Storage로 내보내기</span><span class="sxs-lookup"><span data-stu-id="21b63-123">Export all identities to Azure blob storage</span></span>
* <span data-ttu-id="21b63-124">Azure Blob Storage에서 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="21b63-124">Import identities from Azure blob storage</span></span>

<span data-ttu-id="21b63-125">이러한 모든 작업은 [RFC7232][lnk-rfc7232]에 지정된 낙관적 동시성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-125">All these operations can use optimistic concurrency, as specified in [RFC7232][lnk-rfc7232].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21b63-126">IoT Hub의 ID 레지스트리에서 모든 ID를 검색하는 유일한 방법은 [내보내기][lnk-export] 기능을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-126">The only way to retrieve all identities in an IoT hub's identity registry is to use the [Export][lnk-export] functionality.</span></span>

<span data-ttu-id="21b63-127">IoT Hub ID 레지스트리:</span><span class="sxs-lookup"><span data-stu-id="21b63-127">An IoT Hub identity registry:</span></span>

* <span data-ttu-id="21b63-128">응용 프로그램 메타 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-128">Does not contain any application metadata.</span></span>
* <span data-ttu-id="21b63-129">**deviceId** 를 키로 사용하여 사전처럼 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-129">Can be accessed like a dictionary, by using the **deviceId** as the key.</span></span>
* <span data-ttu-id="21b63-130">표현 쿼리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-130">Does not support expressive queries.</span></span>

<span data-ttu-id="21b63-131">IoT 솔루션에는 일반적으로 응용 프로그램 관련 메타데이터가 포함된 별도의 솔루션 관련 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-131">An IoT solution typically has a separate solution-specific store that contains application-specific metadata.</span></span> <span data-ttu-id="21b63-132">예를 들어 스마트 건물 솔루션의 솔루션 관련 저장소는 온도 센서가 배포된 방을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-132">For example, the solution-specific store in a smart building solution would record the room in which a temperature sensor is deployed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21b63-133">장치 관리 및 프로비전 작업에 대해서는 ID 레지스트리만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-133">Only use the identity registry for device management and provisioning operations.</span></span> <span data-ttu-id="21b63-134">런타임 시 처리량이 높은 작업은 ID 레지스트리에서 수행하는 작업에 따라 달라지지 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-134">High throughput operations at run time should not depend on performing operations in the identity registry.</span></span> <span data-ttu-id="21b63-135">예를 들어 명령을 보내기 전에 장치의 연결 상태를 검사하는 것은 지원되는 패턴이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-135">For example, checking the connection state of a device before sending a command is not a supported pattern.</span></span> <span data-ttu-id="21b63-136">ID 레지스트리에 대한 [제한 속도][lnk-quotas]와 [장치 하트비트][lnk-guidance-heartbeat] 패턴을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-136">Make sure to check the [throttling rates][lnk-quotas] for the identity registry, and the [device heartbeat][lnk-guidance-heartbeat] pattern.</span></span>

## <a name="disable-devices"></a><span data-ttu-id="21b63-137">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="21b63-137">Disable devices</span></span>

<span data-ttu-id="21b63-138">ID 레지스트리에서 ID의 **상태** 속성을 업데이트하여 장치를 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-138">You can disable devices by updating the **status** property of an identity in the identity registry.</span></span> <span data-ttu-id="21b63-139">일반적으로 이 속성은 두 가지 시나리오에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-139">Typically, you use this property in two scenarios:</span></span>

* <span data-ttu-id="21b63-140">오케스트레이션 과정을 프로비전하는 동안입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-140">During a provisioning orchestration process.</span></span> <span data-ttu-id="21b63-141">자세한 내용은 [장치 프로비전][lnk-guidance-provisioning]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-141">For more information, see [Device Provisioning][lnk-guidance-provisioning].</span></span>
* <span data-ttu-id="21b63-142">어떤 이유로든 손상되거나 권한이 없는 장치를 사용하도록 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-142">If, for any reason, you consider a device is compromised or has become unauthorized.</span></span>

## <a name="import-and-export-device-identities"></a><span data-ttu-id="21b63-143">장치 ID 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="21b63-143">Import and export device identities</span></span>

<span data-ttu-id="21b63-144">[IoT Hub 리소스 공급자 끝점][lnk-endpoints]에서 비동기 작업을 사용하여 IoT Hub의 ID 레지스트리에서 장치 ID를 대량으로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-144">You can export device identities in bulk from an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="21b63-145">내보내기는 고객이 제공한 Blob 컨테이너를 사용하여 ID 레지스터에서 읽은 장치 ID 데이터를 저장하는 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-145">Exports are long-running jobs that use a customer-supplied blob container to save device identity data read from the identity registry.</span></span>

<span data-ttu-id="21b63-146">[IoT Hub 리소스 공급자 끝점][lnk-endpoints]에서 비동기 작업을 사용하여 IoT Hub의 ID 레지스트리로 장치 ID를 대량으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-146">You can import device identities in bulk to an IoT hub's identity registry, by using asynchronous operations on the [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="21b63-147">가져오기는 고객이 제공한 Blob 컨테이너의 데이터를 사용하여 장치 ID 데이터를 ID 레지스트리에 쓰는 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-147">Imports are long-running jobs that use data in a customer-supplied blob container to write device identity data into the identity registry.</span></span>

* <span data-ttu-id="21b63-148">API를 가져오고 내보내는 작업에 대한 자세한 정보는 [IoT Hub 리소스 공급자 REST API][lnk-resource-provider-apis]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-148">For detailed information about the import and export APIs, see [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span>
* <span data-ttu-id="21b63-149">가져오기 및 내보내기 작업 실행에 대한 자세한 내용은 [IoT Hub 장치 ID의 대량 관리][lnk-bulk-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-149">To learn more about running import and export jobs, see [Bulk management of IoT Hub device identities][lnk-bulk-identity].</span></span>

## <a name="device-provisioning"></a><span data-ttu-id="21b63-150">장치 프로비전</span><span class="sxs-lookup"><span data-stu-id="21b63-150">Device provisioning</span></span>

<span data-ttu-id="21b63-151">지정된 IoT 솔루션이 저장하는 장치 데이터는 해당 솔루션의 요구 사항에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-151">The device data that a given IoT solution stores depends on the specific requirements of that solution.</span></span> <span data-ttu-id="21b63-152">하지만 어떤 솔루션이든 최소한 장치 ID와 인증 키를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-152">But, as a minimum, a solution must store device identities and authentication keys.</span></span> <span data-ttu-id="21b63-153">Azure IoT Hub는 ID, 인증 키 및 상태 코드와 같은 각 장치에 대한 값을 저장할 수 있는 ID 레지스트리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-153">Azure IoT Hub includes an identity registry that can store values for each device such as IDs, authentication keys, and status codes.</span></span> <span data-ttu-id="21b63-154">솔루션은 Table Storage, Blob Storage 또는 Cosmos DB와 같은 기타 Azure 서비스를 사용하여 추가 장치 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-154">A solution can use other Azure services such as table storage, blob storage, or Cosmos DB to store any additional device data.</span></span>

<span data-ttu-id="21b63-155">*장치 프로비전* 은 솔루션 저장소에 초기 장치 데이터를 추가하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-155">*Device provisioning* is the process of adding the initial device data to the stores in your solution.</span></span> <span data-ttu-id="21b63-156">새 장치를 허브에 연결하도록 하려면 장치 ID 및 키를 IoT Hub ID 레지스트리에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-156">To enable a new device to connect to your hub, you must add a device ID and keys to the IoT Hub identity registry.</span></span> <span data-ttu-id="21b63-157">프로비전 프로세스의 일부로, 다른 솔루션 저장소에서 장치 특정 데이터를 초기화해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-157">As part of the provisioning process, you might need to initialize device-specific data in other solution stores.</span></span>

## <a name="device-heartbeat"></a><span data-ttu-id="21b63-158">장치 하트비트</span><span class="sxs-lookup"><span data-stu-id="21b63-158">Device heartbeat</span></span>

<span data-ttu-id="21b63-159">IoT Hub ID 레지스트리는 **connectionState**라는 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-159">The IoT Hub identity registry contains a field called **connectionState**.</span></span> <span data-ttu-id="21b63-160">개발 및 디버깅하는 동안 **connectionState** 필드만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-160">Only use the **connectionState** field during development and debugging.</span></span> <span data-ttu-id="21b63-161">IoT 솔루션은 런타임에 필드를 쿼리하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-161">IoT solutions should not query the field at run time.</span></span> <span data-ttu-id="21b63-162">예를 들어 클라우드-장치 메시지 또는 SMS를 보내기 전에 장치가 연결되었는지 확인하기 위해 **connectionState** 필드를 쿼리하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-162">For example, do not query the **connectionState** field to check if a device is connected before you send a cloud-to-device message or an SMS.</span></span>

<span data-ttu-id="21b63-163">IoT 솔루션에서 장치가 연결되었는지 여부를 알아야 하는 경우 *하트비트 패턴*을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-163">If your IoT solution needs to know if a device is connected, you should implement the *heartbeat pattern*.</span></span>

<span data-ttu-id="21b63-164">하트비트 패턴에서 장치는 정해진 시간에 최소 한 번(예: 1시간마다 최소 한 번) 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-164">In the heartbeat pattern, the device sends device-to-cloud messages at least once every fixed amount of time (for example, at least once every hour).</span></span> <span data-ttu-id="21b63-165">따라서 장치가 보낼 데이터가 없는 경우 빈 장치-클라우드 메시지(이를 하트비트로 식별하는 속성을 가짐)라도 보낸다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-165">Therefore, even if a device does not have any data to send, it still sends an empty device-to-cloud message (usually with a property that identifies it as a heartbeat).</span></span> <span data-ttu-id="21b63-166">서비스 쪽에서 솔루션은 각 장치에 대해 받은 마지막 하트비트와 함께 맵을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-166">On the service side, the solution maintains a map with the last heartbeat received for each device.</span></span> <span data-ttu-id="21b63-167">솔루션은 예상된 시간 내에 장치에서 보낸 하트비트 메시지를 받지 않을 경우 장치에 문제가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-167">If the solution does not receive a heartbeat message within the expected time from the device, it assumes that there is a problem with the device.</span></span>

<span data-ttu-id="21b63-168">좀 더 복잡한 구현에서는 연결 또는 통신을 시도했지만 실패한 장치를 식별하기 위해 [작업 모니터링][lnk-devguide-opmon] 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-168">A more complex implementation could include the information from [operations monitoring][lnk-devguide-opmon] to identify devices that are trying to connect or communicate but failing.</span></span> <span data-ttu-id="21b63-169">하트비트 패턴을 구현하는 경우 [IoT Hub 할당량 및 제한][lnk-quotas]을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-169">When you implement the heartbeat pattern, make sure to check [IoT Hub Quotas and Throttles][lnk-quotas].</span></span>

> [!NOTE]
> <span data-ttu-id="21b63-170">IoT 솔루션에서 연결 상태만 사용하여 클라우드-장치 메시지를 보낼지 여부를 결정해야 하고 메시지가 큰 장치 집합으로 브로드캐스트되지 않는 경우 단순한 *짧은 만료 시간* 패턴 사용을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-170">If an IoT solution uses the connection state solely to determine whether to send cloud-to-device messages, and messages are not broadcast to large sets of devices, consider using the simpler *short expiry time* pattern.</span></span> <span data-ttu-id="21b63-171">이렇게 하면 이 패턴은 더 효율적으로 유지되면서 하트비트 패턴을 사용하여 장치 연결 상태 레지스트리를 유지 관리하는 것과 동일한 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-171">This pattern achieves the same result as maintaining a device connection state registry using the heartbeat pattern, while being more efficient.</span></span> <span data-ttu-id="21b63-172">메시지 승인을 요청하면 IoT Hub는 메시지를 수신할 수 있는 장치와 수신할 수 없는 장치에 대해 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-172">If you request message acknowledgements, IoT Hub can notify you about which devices are able to receive messages and which are not.</span></span>

## <a name="device-lifecycle-notifications"></a><span data-ttu-id="21b63-173">장치 수명 주기 알림</span><span class="sxs-lookup"><span data-stu-id="21b63-173">Device lifecycle notifications</span></span>

<span data-ttu-id="21b63-174">장치 ID가 생성 또는 삭제되면 IoT Hub에서 장치 수명 주기 알림을 전송하여 IoT 솔루션에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-174">IoT Hub can notify your IoT solution when a device identity is created or deleted by sending device lifecycle notifications.</span></span> <span data-ttu-id="21b63-175">이를 수행하려면 IoT 솔루션이 경로를 만들고 데이터 원본을 *DeviceLifecycleEvents*와 동일하게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-175">To do so, your IoT solution needs to create a route and to set the Data Source equal to *DeviceLifecycleEvents*.</span></span> <span data-ttu-id="21b63-176">기본적으로 수명 주기 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-176">By default, no lifecycle notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="21b63-177">알림 메시지는 속성과 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-177">The notification message includes properties, and body.</span></span>

<span data-ttu-id="21b63-178">속성: 메시지 시스템 속성 앞에 `'$'` 기호를 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-178">Properties: Message system properties are prefixed with the `'$'` symbol.</span></span>

| <span data-ttu-id="21b63-179">이름</span><span class="sxs-lookup"><span data-stu-id="21b63-179">Name</span></span> | <span data-ttu-id="21b63-180">값</span><span class="sxs-lookup"><span data-stu-id="21b63-180">Value</span></span> |
| --- | --- |
<span data-ttu-id="21b63-181">$content-type</span><span class="sxs-lookup"><span data-stu-id="21b63-181">$content-type</span></span> | <span data-ttu-id="21b63-182">application/json</span><span class="sxs-lookup"><span data-stu-id="21b63-182">application/json</span></span> |
<span data-ttu-id="21b63-183">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="21b63-183">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="21b63-184">알림이 전송된 시간</span><span class="sxs-lookup"><span data-stu-id="21b63-184">Time when the notification was sent</span></span> |
<span data-ttu-id="21b63-185">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="21b63-185">$iothub-message-source</span></span> | <span data-ttu-id="21b63-186">deviceLifecycleEvents</span><span class="sxs-lookup"><span data-stu-id="21b63-186">deviceLifecycleEvents</span></span> |
<span data-ttu-id="21b63-187">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="21b63-187">$content-encoding</span></span> | <span data-ttu-id="21b63-188">utf-8</span><span class="sxs-lookup"><span data-stu-id="21b63-188">utf-8</span></span> |
<span data-ttu-id="21b63-189">opType</span><span class="sxs-lookup"><span data-stu-id="21b63-189">opType</span></span> | <span data-ttu-id="21b63-190">**createDeviceIdentity** 또는 **deleteDeviceIdentity**</span><span class="sxs-lookup"><span data-stu-id="21b63-190">**createDeviceIdentity** or **deleteDeviceIdentity**</span></span> |
<span data-ttu-id="21b63-191">hubName</span><span class="sxs-lookup"><span data-stu-id="21b63-191">hubName</span></span> | <span data-ttu-id="21b63-192">IoT Hub의 이름</span><span class="sxs-lookup"><span data-stu-id="21b63-192">Name of IoT Hub</span></span> |
<span data-ttu-id="21b63-193">deviceId</span><span class="sxs-lookup"><span data-stu-id="21b63-193">deviceId</span></span> | <span data-ttu-id="21b63-194">장치의 ID</span><span class="sxs-lookup"><span data-stu-id="21b63-194">ID of the device</span></span> |
<span data-ttu-id="21b63-195">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="21b63-195">operationTimestamp</span></span> | <span data-ttu-id="21b63-196">작업의 ISO8601 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="21b63-196">ISO8601 timestamp of operation</span></span> |
<span data-ttu-id="21b63-197">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="21b63-197">iothub-message-schema</span></span> | <span data-ttu-id="21b63-198">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="21b63-198">deviceLifecycleNotification</span></span> |

<span data-ttu-id="21b63-199">본문: 이 섹션은 JSON 형식이며, 생성된 장치 ID 쌍을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-199">Body: This section is in JSON format and represents the twin of the created device identity.</span></span> <span data-ttu-id="21b63-200">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-200">For example,</span></span>

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a><span data-ttu-id="21b63-201">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="21b63-201">Reference topics:</span></span>

<span data-ttu-id="21b63-202">다음 참조 항목에서는 ID 레지스트리에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-202">The following reference topics provide you with more information about the identity registry.</span></span>

## <a name="device-identity-properties"></a><span data-ttu-id="21b63-203">장치 ID 속성</span><span class="sxs-lookup"><span data-stu-id="21b63-203">Device identity properties</span></span>

<span data-ttu-id="21b63-204">장치 ID는 다음 속성을 사용하여 JSON 문서로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-204">Device identities are represented as JSON documents with the following properties:</span></span>

| <span data-ttu-id="21b63-205">속성</span><span class="sxs-lookup"><span data-stu-id="21b63-205">Property</span></span> | <span data-ttu-id="21b63-206">옵션</span><span class="sxs-lookup"><span data-stu-id="21b63-206">Options</span></span> | <span data-ttu-id="21b63-207">설명</span><span class="sxs-lookup"><span data-stu-id="21b63-207">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21b63-208">deviceId</span><span class="sxs-lookup"><span data-stu-id="21b63-208">deviceId</span></span> |<span data-ttu-id="21b63-209">필요한 경우 업데이트에서 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-209">required, read-only on updates</span></span> |<span data-ttu-id="21b63-210">ASCII 7 비트 영숫자 문자 + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`의 대/소문자 구분 문자열(최대 길이 128자)입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-210">A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="21b63-211">generationId</span><span class="sxs-lookup"><span data-stu-id="21b63-211">generationId</span></span> |<span data-ttu-id="21b63-212">필요한 경우 읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-212">required, read-only</span></span> |<span data-ttu-id="21b63-213">IoT Hub에서 생성된 최대 128자의 대/소문자 구분 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-213">An IoT hub-generated, case-sensitive string up to 128 characters long.</span></span> <span data-ttu-id="21b63-214">이 값은 삭제되고 다시 만들 때와 동일한 **deviceId**로 장치를 구분하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-214">This value is used to distinguish devices with the same **deviceId**, when they have been deleted and re-created.</span></span> |
| <span data-ttu-id="21b63-215">etag</span><span class="sxs-lookup"><span data-stu-id="21b63-215">etag</span></span> |<span data-ttu-id="21b63-216">필요한 경우 읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-216">required, read-only</span></span> |<span data-ttu-id="21b63-217">[RFC7232][lnk-rfc7232]에 따라 장치 ID에 대해 약한 ETag를 나타내는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-217">A string representing a weak ETag for the device identity, as per [RFC7232][lnk-rfc7232].</span></span> |
| <span data-ttu-id="21b63-218">auth</span><span class="sxs-lookup"><span data-stu-id="21b63-218">auth</span></span> |<span data-ttu-id="21b63-219">선택 사항</span><span class="sxs-lookup"><span data-stu-id="21b63-219">optional</span></span> |<span data-ttu-id="21b63-220">인증 정보 및 보안 자료를 포함하는 복합 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-220">A composite object containing authentication information and security materials.</span></span> |
| <span data-ttu-id="21b63-221">auth.symkey</span><span class="sxs-lookup"><span data-stu-id="21b63-221">auth.symkey</span></span> |<span data-ttu-id="21b63-222">선택 사항</span><span class="sxs-lookup"><span data-stu-id="21b63-222">optional</span></span> |<span data-ttu-id="21b63-223">base64 형식으로 저장된 기본 및 보조 키를 포함하는 복합 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-223">A composite object containing a primary and a secondary key, stored in base64 format.</span></span> |
| <span data-ttu-id="21b63-224">status</span><span class="sxs-lookup"><span data-stu-id="21b63-224">status</span></span> |<span data-ttu-id="21b63-225">필수</span><span class="sxs-lookup"><span data-stu-id="21b63-225">required</span></span> |<span data-ttu-id="21b63-226">액세스 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-226">An access indicator.</span></span> <span data-ttu-id="21b63-227">**사용** 또는 **사용 안 함**으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-227">Can be **Enabled** or **Disabled**.</span></span> <span data-ttu-id="21b63-228">**사용**이면 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-228">If **Enabled**, the device is allowed to connect.</span></span> <span data-ttu-id="21b63-229">**사용 안 함**이면 이 장치는 장치 연결 끝점에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-229">If **Disabled**, this device cannot access any device-facing endpoint.</span></span> |
| <span data-ttu-id="21b63-230">statusReason</span><span class="sxs-lookup"><span data-stu-id="21b63-230">statusReason</span></span> |<span data-ttu-id="21b63-231">선택 사항</span><span class="sxs-lookup"><span data-stu-id="21b63-231">optional</span></span> |<span data-ttu-id="21b63-232">장치 ID 상태의 원인을 저장하는 128자 길이의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-232">A 128 character-long string that stores the reason for the device identity status.</span></span> <span data-ttu-id="21b63-233">UTF-8 문자를 모두 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-233">All UTF-8 characters are allowed.</span></span> |
| <span data-ttu-id="21b63-234">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="21b63-234">statusUpdateTime</span></span> |<span data-ttu-id="21b63-235">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-235">read-only</span></span> |<span data-ttu-id="21b63-236">마지막 상태 업데이트의 시간과 날짜를 보여 주는 임시 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-236">A temporal indicator, showing the date and time of the last status update.</span></span> |
| <span data-ttu-id="21b63-237">connectionState</span><span class="sxs-lookup"><span data-stu-id="21b63-237">connectionState</span></span> |<span data-ttu-id="21b63-238">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-238">read-only</span></span> |<span data-ttu-id="21b63-239">연결 상태를 나타내는 필드: **연결됨** 또는 **연결 끊김**.</span><span class="sxs-lookup"><span data-stu-id="21b63-239">A field indicating connection status: either **Connected** or **Disconnected**.</span></span> <span data-ttu-id="21b63-240">이 필드는 장치 연결 상태의 IoT Hub 뷰를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-240">This field represents the IoT Hub view of the device connection status.</span></span> <span data-ttu-id="21b63-241">**중요**: 이 필드는 개발/디버깅 용도로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-241">**Important**: This field should be used only for development/debugging purposes.</span></span> <span data-ttu-id="21b63-242">연결 상태는 MQTT 또는 AMQP를 사용하여 장치에 대해서만 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-242">The connection state is updated only for devices using MQTT or AMQP.</span></span> <span data-ttu-id="21b63-243">또한 이는 프로토콜 수준의 ping(MQTT ping 또는 AMQP ping)을 기반으로 하고 있으며 최대 5분 동안만 지연이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-243">Also, it is based on protocol-level pings (MQTT pings, or AMQP pings), and it can have a maximum delay of only 5 minutes.</span></span> <span data-ttu-id="21b63-244">이러한 이유로, 연결되었지만 연결이 끊긴 것으로 보고된 장치와 같이 거짓 긍정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-244">For these reasons, there can be false positives, such as devices reported as connected but that are disconnected.</span></span> |
| <span data-ttu-id="21b63-245">connectionStateUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="21b63-245">connectionStateUpdatedTime</span></span> |<span data-ttu-id="21b63-246">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-246">read-only</span></span> |<span data-ttu-id="21b63-247">연결 상태가 마지막으로 업데이트된 날짜 및 시간을 표시하는 임시 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-247">A temporal indicator, showing the date and last time the connection state was updated.</span></span> |
| <span data-ttu-id="21b63-248">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="21b63-248">lastActivityTime</span></span> |<span data-ttu-id="21b63-249">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="21b63-249">read-only</span></span> |<span data-ttu-id="21b63-250">장치 연결이 마지막으로 연결되거나 메시지를 받거나 보낸 날짜 및 시간을 표시하는 임시 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-250">A temporal indicator, showing the date and last time the device connected, received, or sent a message.</span></span> |

> [!NOTE]
> <span data-ttu-id="21b63-251">연결 상태는 연결 상태의 IoT Hub 뷰만을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-251">Connection state can only represent the IoT Hub view of the status of the connection.</span></span> <span data-ttu-id="21b63-252">이 상태에 대한 업데이트는 네트워크 상태 및 구성에 따라 지연될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-252">Updates to this state may be delayed, depending on network conditions and configurations.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="21b63-253">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="21b63-253">Additional reference material</span></span>

<span data-ttu-id="21b63-254">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="21b63-254">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="21b63-255">[IoT Hub 끝점][lnk-endpoints] - 각 IoT Hub에서 런타임 및 관리 작업에 대해 공개하는 다양한 끝점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-255">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="21b63-256">[제한 및 할당량][lnk-quotas]은 IoT Hub 서비스에 적용되는 할당량과 제한 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-256">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="21b63-257">[Azure IoT 장치 및 서비스 SDK][lnk-sdks] - IoT Hub와 상호 작용하는 장치 및 서비스 앱 모두를 개발할 때 사용할 수 있는 다양한 언어 SDK를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-257">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="21b63-258">[IoT Hub 쿼리 언어][lnk-query]는 IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용할 수 있는 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-258">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="21b63-259">[IoT Hub MQTT 지원][lnk-devguide-mqtt] - MQTT 프로토콜에 대한 IoT Hub 지원에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="21b63-259">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21b63-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21b63-260">Next steps</span></span>

<span data-ttu-id="21b63-261">IoT Hub ID 레지스트리를 사용하는 방법에 대해 알아봤으니 다음 IoT Hub 개발자 가이드 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-261">Now you have learned how to use the IoT Hub identity registry, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="21b63-262">[IoT Hub에 대한 액세스 제어][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="21b63-262">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="21b63-263">[장치 쌍을 사용하여 상태 및 구성 동기화][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="21b63-263">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="21b63-264">[장치에서 직접 메서드 호출][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="21b63-264">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="21b63-265">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="21b63-265">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="21b63-266">이 문서에서 설명한 일부 개념을 시도해 보려면 다음과 같은 IoT Hub 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="21b63-266">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="21b63-267">[Azure IoT Hub 시작][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="21b63-267">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
