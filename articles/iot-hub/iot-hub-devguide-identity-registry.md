---
title: "aaaUnderstand hello Azure IoT Hub id 레지스트리에 | Microsoft Docs"
description: "개발자 가이드-hello IoT Hub id 레지스트리에 설명은 방법과 toouse 것 toomanage 장치입니다. 대량에 hello 가져오기 및 내보내기 장치 id에 대 한 정보를 포함합니다."
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
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a><span data-ttu-id="eea30-104">IoT hub에 hello id 레지스트리에 이해</span><span class="sxs-lookup"><span data-stu-id="eea30-104">Understand hello identity registry in your IoT hub</span></span>

<span data-ttu-id="eea30-105">모든 IoT hub tooconnect toohello IoT 허브를 허용 하는 hello 장치에 대 한 정보를 저장 하는 id 레지스트리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-105">Every IoT hub has an identity registry that stores information about hello devices permitted tooconnect toohello IoT hub.</span></span> <span data-ttu-id="eea30-106">장치 tooan IoT 허브에 연결할 수 전에 hello IoT hub id 레지스트리에에서 해당 장치에 대 한 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-106">Before a device can connect tooan IoT hub, there must be an entry for that device in hello IoT hub's identity registry.</span></span> <span data-ttu-id="eea30-107">장치 id 레지스트리에 hello에 저장 된 자격 증명에 따라 hello IoT hub와도 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-107">A device must also authenticate with hello IoT hub based on credentials stored in hello identity registry.</span></span>

<span data-ttu-id="eea30-108">hello identity 레지스트리에 저장 된 hello 장치 ID는 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-108">hello device ID stored in hello identity registry is case-sensitive.</span></span>

<span data-ttu-id="eea30-109">상위 수준 hello id 레지스트리에 장치 identity 리소스는 REST 가능 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-109">At a high level, hello identity registry is a REST-capable collection of device identity resources.</span></span> <span data-ttu-id="eea30-110">Hello id 레지스트리에 항목을 추가 하는 경우 IoT 허브는 진행 중인 클라우드-장치 메시지를 포함 하는 hello 큐와 같은 장치 리소스 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-110">When you add an entry in hello identity registry, IoT Hub creates a set of per-device resources such as hello queue that contains in-flight cloud-to-device messages.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="eea30-111">때 toouse</span><span class="sxs-lookup"><span data-stu-id="eea30-111">When toouse</span></span>

<span data-ttu-id="eea30-112">Hello id 레지스트리에을 할 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-112">Use hello identity registry when you need to:</span></span>

* <span data-ttu-id="eea30-113">Tooyour IoT 허브를 연결 하는 장치를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-113">Provision devices that connect tooyour IoT hub.</span></span>
* <span data-ttu-id="eea30-114">장치 액세스 tooyour 허브의 장치에 연결 끝점을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-114">Control per-device access tooyour hub's device-facing endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="eea30-115">hello id 레지스트리에 응용 프로그램별 메타 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-115">hello identity registry does not contain any application-specific metadata.</span></span>

## <a name="identity-registry-operations"></a><span data-ttu-id="eea30-116">ID 레지스트리 작업</span><span class="sxs-lookup"><span data-stu-id="eea30-116">Identity registry operations</span></span>

<span data-ttu-id="eea30-117">IoT Hub id 레지스트리에 hello hello 다음 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-117">hello IoT Hub identity registry exposes hello following operations:</span></span>

* <span data-ttu-id="eea30-118">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="eea30-118">Create device identity</span></span>
* <span data-ttu-id="eea30-119">장치 ID 업데이트</span><span class="sxs-lookup"><span data-stu-id="eea30-119">Update device identity</span></span>
* <span data-ttu-id="eea30-120">ID로 장치 ID 검색</span><span class="sxs-lookup"><span data-stu-id="eea30-120">Retrieve device identity by ID</span></span>
* <span data-ttu-id="eea30-121">장치 ID 삭제</span><span class="sxs-lookup"><span data-stu-id="eea30-121">Delete device identity</span></span>
* <span data-ttu-id="eea30-122">Too1000 identities를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-122">List up too1000 identities</span></span>
* <span data-ttu-id="eea30-123">모든 identities tooAzure blob 저장소 내보내기</span><span class="sxs-lookup"><span data-stu-id="eea30-123">Export all identities tooAzure blob storage</span></span>
* <span data-ttu-id="eea30-124">Azure Blob Storage에서 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="eea30-124">Import identities from Azure blob storage</span></span>

<span data-ttu-id="eea30-125">이러한 모든 작업은 [RFC7232][lnk-rfc7232]에 지정된 낙관적 동시성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-125">All these operations can use optimistic concurrency, as specified in [RFC7232][lnk-rfc7232].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eea30-126">방법은 tooretrieve만 hello id 레지스트리에 IoT 허브에서 모든 id는 toouse hello [내보내기] [ lnk-export] 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-126">hello only way tooretrieve all identities in an IoT hub's identity registry is toouse hello [Export][lnk-export] functionality.</span></span>

<span data-ttu-id="eea30-127">IoT Hub ID 레지스트리:</span><span class="sxs-lookup"><span data-stu-id="eea30-127">An IoT Hub identity registry:</span></span>

* <span data-ttu-id="eea30-128">응용 프로그램 메타 데이터가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-128">Does not contain any application metadata.</span></span>
* <span data-ttu-id="eea30-129">Hello를 사용 하 여 사전 처럼 액세스할 수 **deviceId** hello 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-129">Can be accessed like a dictionary, by using hello **deviceId** as hello key.</span></span>
* <span data-ttu-id="eea30-130">표현 쿼리를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-130">Does not support expressive queries.</span></span>

<span data-ttu-id="eea30-131">IoT 솔루션에는 일반적으로 응용 프로그램 관련 메타데이터가 포함된 별도의 솔루션 관련 저장소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-131">An IoT solution typically has a separate solution-specific store that contains application-specific metadata.</span></span> <span data-ttu-id="eea30-132">예를 들어 hello 스마트 건물 솔루션에서 솔루션 별 저장소 기록 온도 센서 배포 된 hello 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-132">For example, hello solution-specific store in a smart building solution would record hello room in which a temperature sensor is deployed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eea30-133">장치 관리 및 프로비저닝 작업에 대 한 hello id 레지스트리에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-133">Only use hello identity registry for device management and provisioning operations.</span></span> <span data-ttu-id="eea30-134">처리량이 높은 작업 실행 시 hello id 레지스트리에에서 작업을 수행 신뢰 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-134">High throughput operations at run time should not depend on performing operations in hello identity registry.</span></span> <span data-ttu-id="eea30-135">예를 들어 명령을 전송 하기 전에 장치의 hello 연결 상태를 확인 하지 지원 되는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-135">For example, checking hello connection state of a device before sending a command is not a supported pattern.</span></span> <span data-ttu-id="eea30-136">있는지 toocheck hello 확인 [제한을] [ lnk-quotas] hello id 레지스트리 및 hello에 대 한 [장치 하트 비트] [ lnk-guidance-heartbeat] 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-136">Make sure toocheck hello [throttling rates][lnk-quotas] for hello identity registry, and hello [device heartbeat][lnk-guidance-heartbeat] pattern.</span></span>

## <a name="disable-devices"></a><span data-ttu-id="eea30-137">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="eea30-137">Disable devices</span></span>

<span data-ttu-id="eea30-138">Hello를 업데이트 하 여 장치를 비활성화할 수 **상태** hello identity 레지스트리에 id의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-138">You can disable devices by updating hello **status** property of an identity in hello identity registry.</span></span> <span data-ttu-id="eea30-139">일반적으로 이 속성은 두 가지 시나리오에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-139">Typically, you use this property in two scenarios:</span></span>

* <span data-ttu-id="eea30-140">오케스트레이션 과정을 프로비전하는 동안입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-140">During a provisioning orchestration process.</span></span> <span data-ttu-id="eea30-141">자세한 내용은 [장치 프로비전][lnk-guidance-provisioning]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eea30-141">For more information, see [Device Provisioning][lnk-guidance-provisioning].</span></span>
* <span data-ttu-id="eea30-142">어떤 이유로든 손상되거나 권한이 없는 장치를 사용하도록 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-142">If, for any reason, you consider a device is compromised or has become unauthorized.</span></span>

## <a name="import-and-export-device-identities"></a><span data-ttu-id="eea30-143">장치 ID 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="eea30-143">Import and export device identities</span></span>

<span data-ttu-id="eea30-144">Hello에 대 한 비동기 작업을 사용 하 여 IoT 허브의 id 레지스트리에에서 대량에서 장치 id를 내보낼 수 [IoT 허브 리소스 공급자 끝점][lnk-endpoints]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-144">You can export device identities in bulk from an IoT hub's identity registry, by using asynchronous operations on hello [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="eea30-145">내보내기는 장기 실행 hello identity 레지스트리에서 고객이 제공한 blob 컨테이너 toosave 장치 id 데이터를 사용 하는 작업을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-145">Exports are long-running jobs that use a customer-supplied blob container toosave device identity data read from hello identity registry.</span></span>

<span data-ttu-id="eea30-146">Hello에 대 한 비동기 작업을 사용 하 여 대량 tooan IoT hub id 레지스트리에에서 장치 id를 가져올 수 있습니다 [IoT 허브 리소스 공급자 끝점][lnk-endpoints]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-146">You can import device identities in bulk tooan IoT hub's identity registry, by using asynchronous operations on hello [IoT Hub resource provider endpoint][lnk-endpoints].</span></span> <span data-ttu-id="eea30-147">가져오기는 hello identity 레지스트리에 고객이 제공한 blob 컨테이너 toowrite 장치 id 데이터에서 데이터를 사용 하는 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-147">Imports are long-running jobs that use data in a customer-supplied blob container toowrite device identity data into hello identity registry.</span></span>

* <span data-ttu-id="eea30-148">Hello 가져오기 및 내보내기 Api에 대 한 자세한 내용은 참조 [IoT 허브 리소스 공급자 REST Api][lnk-resource-provider-apis]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-148">For detailed information about hello import and export APIs, see [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span>
* <span data-ttu-id="eea30-149">toolearn 실행에 대 한 자세한 가져오기 및 내보내기 작업을 참조 하십시오 [IoT Hub 장치 id 관리 대량][lnk-bulk-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-149">toolearn more about running import and export jobs, see [Bulk management of IoT Hub device identities][lnk-bulk-identity].</span></span>

## <a name="device-provisioning"></a><span data-ttu-id="eea30-150">장치 프로비전</span><span class="sxs-lookup"><span data-stu-id="eea30-150">Device provisioning</span></span>

<span data-ttu-id="eea30-151">지정된 된 IoT 솔루션을 저장 하는 hello 장치 데이터 hello 해당 솔루션의 특정 요구 사항에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-151">hello device data that a given IoT solution stores depends on hello specific requirements of that solution.</span></span> <span data-ttu-id="eea30-152">하지만 어떤 솔루션이든 최소한 장치 ID와 인증 키를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-152">But, as a minimum, a solution must store device identities and authentication keys.</span></span> <span data-ttu-id="eea30-153">Azure IoT Hub는 ID, 인증 키 및 상태 코드와 같은 각 장치에 대한 값을 저장할 수 있는 ID 레지스트리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-153">Azure IoT Hub includes an identity registry that can store values for each device such as IDs, authentication keys, and status codes.</span></span> <span data-ttu-id="eea30-154">솔루션 추가 장치 데이터 Cosmos DB toostore 테이블 저장소, blob 저장소 등 다른 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-154">A solution can use other Azure services such as table storage, blob storage, or Cosmos DB toostore any additional device data.</span></span>

<span data-ttu-id="eea30-155">*장치 프로 비전* hello 프로세스 솔루션의 hello 초기 장치 데이터 toohello 매장을 추가 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-155">*Device provisioning* is hello process of adding hello initial device data toohello stores in your solution.</span></span> <span data-ttu-id="eea30-156">새 장치 tooconnect tooyour 허브 tooenable 장치 ID와 키 toohello IoT Hub id 레지스트리에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-156">tooenable a new device tooconnect tooyour hub, you must add a device ID and keys toohello IoT Hub identity registry.</span></span> <span data-ttu-id="eea30-157">Hello 프로 비전 프로세스의 일환으로, 다른 솔루션 저장소에 tooinitialize 장치 관련 데이터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-157">As part of hello provisioning process, you might need tooinitialize device-specific data in other solution stores.</span></span>

## <a name="device-heartbeat"></a><span data-ttu-id="eea30-158">장치 하트비트</span><span class="sxs-lookup"><span data-stu-id="eea30-158">Device heartbeat</span></span>

<span data-ttu-id="eea30-159">hello IoT Hub id 레지스트리에 필드가 들어 **connectionState**합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-159">hello IoT Hub identity registry contains a field called **connectionState**.</span></span> <span data-ttu-id="eea30-160">만 hello를 사용 하 여 **connectionState** 개발 및 디버깅 하는 동안 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-160">Only use hello **connectionState** field during development and debugging.</span></span> <span data-ttu-id="eea30-161">IoT 솔루션에서 런타임에 hello 필드를 쿼리할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-161">IoT solutions should not query hello field at run time.</span></span> <span data-ttu-id="eea30-162">예를 들어 hello 쿼리하지 않는 **connectionState** 필드 toocheck 클라우드-장치 메시지 또는 SMS 보내기 전에 장치가 연결 된 경우.</span><span class="sxs-lookup"><span data-stu-id="eea30-162">For example, do not query hello **connectionState** field toocheck if a device is connected before you send a cloud-to-device message or an SMS.</span></span>

<span data-ttu-id="eea30-163">Hello를 구현 해야 하면 IoT 솔루션을 필요한 경우 tooknow 장치가 연결 된 경우 *하트 비트 패턴*합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-163">If your IoT solution needs tooknow if a device is connected, you should implement hello *heartbeat pattern*.</span></span>

<span data-ttu-id="eea30-164">Hello 하트 비트 패턴을 한 번 이상 (예: 매 시간 마다 적어도 한 번) 시간의 모든 고정 된 숫자일 hello 장치 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-164">In hello heartbeat pattern, hello device sends device-to-cloud messages at least once every fixed amount of time (for example, at least once every hour).</span></span> <span data-ttu-id="eea30-165">따라서 장치에 모든 데이터 toosend 없는 경우에 여전히 일반적으로 (하트 비트도 식별 하는 속성)를 사용 하는 빈 장치-클라우드 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-165">Therefore, even if a device does not have any data toosend, it still sends an empty device-to-cloud message (usually with a property that identifies it as a heartbeat).</span></span> <span data-ttu-id="eea30-166">Hello 솔루션 hello 서비스 쪽에서는 각 장치에 대 한 수신 hello 마지막 하트 비트와 지도 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-166">On hello service side, hello solution maintains a map with hello last heartbeat received for each device.</span></span> <span data-ttu-id="eea30-167">Hello 솔루션 hello 장치에서 hello 예상 시간 안에 하트 비트 메시지를 받지 않을 경우 hello 장치 문제 임을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-167">If hello solution does not receive a heartbeat message within hello expected time from hello device, it assumes that there is a problem with hello device.</span></span>

<span data-ttu-id="eea30-168">더 복잡 한 구현에서 hello 정보를 포함할 수 [작업 모니터링] [ lnk-devguide-opmon] tooidentify 장치 tooconnect 또는 통신에 실패 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-168">A more complex implementation could include hello information from [operations monitoring][lnk-devguide-opmon] tooidentify devices that are trying tooconnect or communicate but failing.</span></span> <span data-ttu-id="eea30-169">Hello 하트 비트 패턴을 구현 하는 경우 확인 되었는지 toocheck [IoT 허브 할당량 및 제한을][lnk-quotas]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-169">When you implement hello heartbeat pattern, make sure toocheck [IoT Hub Quotas and Throttles][lnk-quotas].</span></span>

> [!NOTE]
> <span data-ttu-id="eea30-170">IoT 솔루션 사용 하 여 hello 연결 상태만 toodetermine 여부 경우 toosend 클라우드-장치 메시지, 메시지는 하지 장치 집합이 toolarge 브로드캐스트, 간단 hello를 사용 하는 것이 좋습니다 *짧은 만료 시간* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-170">If an IoT solution uses hello connection state solely toodetermine whether toosend cloud-to-device messages, and messages are not broadcast toolarge sets of devices, consider using hello simpler *short expiry time* pattern.</span></span> <span data-ttu-id="eea30-171">이 패턴 hello hello 하트 비트 패턴을 사용 하 여 보다 효율적인를 사용 하는 장치 연결 상태 레지스트리를 유지 관리와 같은 결과 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-171">This pattern achieves hello same result as maintaining a device connection state registry using hello heartbeat pattern, while being more efficient.</span></span> <span data-ttu-id="eea30-172">메시지 승인이 요청 하는 경우 IoT Hub 있는 장치 수 tooreceive 메시지 이며 하지 않은 알릴 수 있음.</span><span class="sxs-lookup"><span data-stu-id="eea30-172">If you request message acknowledgements, IoT Hub can notify you about which devices are able tooreceive messages and which are not.</span></span>

## <a name="device-lifecycle-notifications"></a><span data-ttu-id="eea30-173">장치 수명 주기 알림</span><span class="sxs-lookup"><span data-stu-id="eea30-173">Device lifecycle notifications</span></span>

<span data-ttu-id="eea30-174">장치 ID가 생성 또는 삭제되면 IoT Hub에서 장치 수명 주기 알림을 전송하여 IoT 솔루션에 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-174">IoT Hub can notify your IoT solution when a device identity is created or deleted by sending device lifecycle notifications.</span></span> <span data-ttu-id="eea30-175">toodo, 하면 IoT 솔루션 필요한 등 toocreate 경로 및 tooset hello 데이터 소스 같음 너무*DeviceLifecycleEvents*합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-175">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*DeviceLifecycleEvents*.</span></span> <span data-ttu-id="eea30-176">기본적으로 수명 주기 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-176">By default, no lifecycle notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="eea30-177">hello 알림 메시지에 속성 및 본문에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-177">hello notification message includes properties, and body.</span></span>

<span data-ttu-id="eea30-178">속성: 메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-178">Properties: Message system properties are prefixed with hello `'$'` symbol.</span></span>

| <span data-ttu-id="eea30-179">이름</span><span class="sxs-lookup"><span data-stu-id="eea30-179">Name</span></span> | <span data-ttu-id="eea30-180">값</span><span class="sxs-lookup"><span data-stu-id="eea30-180">Value</span></span> |
| --- | --- |
<span data-ttu-id="eea30-181">$content-type</span><span class="sxs-lookup"><span data-stu-id="eea30-181">$content-type</span></span> | <span data-ttu-id="eea30-182">application/json</span><span class="sxs-lookup"><span data-stu-id="eea30-182">application/json</span></span> |
<span data-ttu-id="eea30-183">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="eea30-183">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="eea30-184">Hello 알림을 전송 시간</span><span class="sxs-lookup"><span data-stu-id="eea30-184">Time when hello notification was sent</span></span> |
<span data-ttu-id="eea30-185">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="eea30-185">$iothub-message-source</span></span> | <span data-ttu-id="eea30-186">deviceLifecycleEvents</span><span class="sxs-lookup"><span data-stu-id="eea30-186">deviceLifecycleEvents</span></span> |
<span data-ttu-id="eea30-187">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="eea30-187">$content-encoding</span></span> | <span data-ttu-id="eea30-188">utf-8</span><span class="sxs-lookup"><span data-stu-id="eea30-188">utf-8</span></span> |
<span data-ttu-id="eea30-189">opType</span><span class="sxs-lookup"><span data-stu-id="eea30-189">opType</span></span> | <span data-ttu-id="eea30-190">**createDeviceIdentity** 또는 **deleteDeviceIdentity**</span><span class="sxs-lookup"><span data-stu-id="eea30-190">**createDeviceIdentity** or **deleteDeviceIdentity**</span></span> |
<span data-ttu-id="eea30-191">hubName</span><span class="sxs-lookup"><span data-stu-id="eea30-191">hubName</span></span> | <span data-ttu-id="eea30-192">IoT Hub의 이름</span><span class="sxs-lookup"><span data-stu-id="eea30-192">Name of IoT Hub</span></span> |
<span data-ttu-id="eea30-193">deviceId</span><span class="sxs-lookup"><span data-stu-id="eea30-193">deviceId</span></span> | <span data-ttu-id="eea30-194">Hello 장치의 ID</span><span class="sxs-lookup"><span data-stu-id="eea30-194">ID of hello device</span></span> |
<span data-ttu-id="eea30-195">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="eea30-195">operationTimestamp</span></span> | <span data-ttu-id="eea30-196">작업의 ISO8601 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="eea30-196">ISO8601 timestamp of operation</span></span> |
<span data-ttu-id="eea30-197">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="eea30-197">iothub-message-schema</span></span> | <span data-ttu-id="eea30-198">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="eea30-198">deviceLifecycleNotification</span></span> |

<span data-ttu-id="eea30-199">본문:이 섹션 JSON 형식으로는 고 장치 id를 생성 하는 hello의 hello로 이중을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-199">Body: This section is in JSON format and represents hello twin of hello created device identity.</span></span> <span data-ttu-id="eea30-200">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-200">For example,</span></span>

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

## <a name="reference-topics"></a><span data-ttu-id="eea30-201">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="eea30-201">Reference topics:</span></span>

<span data-ttu-id="eea30-202">hello 다음 참조 항목 제공 hello id 레지스트리에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-202">hello following reference topics provide you with more information about hello identity registry.</span></span>

## <a name="device-identity-properties"></a><span data-ttu-id="eea30-203">장치 ID 속성</span><span class="sxs-lookup"><span data-stu-id="eea30-203">Device identity properties</span></span>

<span data-ttu-id="eea30-204">장치 id가 다음과 같은 속성 hello로 JSON 문서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-204">Device identities are represented as JSON documents with hello following properties:</span></span>

| <span data-ttu-id="eea30-205">속성</span><span class="sxs-lookup"><span data-stu-id="eea30-205">Property</span></span> | <span data-ttu-id="eea30-206">옵션</span><span class="sxs-lookup"><span data-stu-id="eea30-206">Options</span></span> | <span data-ttu-id="eea30-207">설명</span><span class="sxs-lookup"><span data-stu-id="eea30-207">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eea30-208">deviceId</span><span class="sxs-lookup"><span data-stu-id="eea30-208">deviceId</span></span> |<span data-ttu-id="eea30-209">필요한 경우 업데이트에서 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-209">required, read-only on updates</span></span> |<span data-ttu-id="eea30-210">ASCII 7 비트 영숫자 문자 (위쪽 too128 자)는 대/소문자 구분 문자열 + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-210">A case-sensitive string (up too128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="eea30-211">generationId</span><span class="sxs-lookup"><span data-stu-id="eea30-211">generationId</span></span> |<span data-ttu-id="eea30-212">필요한 경우 읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-212">required, read-only</span></span> |<span data-ttu-id="eea30-213">IoT 허브에서 생성 된, 대/소문자 구분 문자열을 too128 자입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-213">An IoT hub-generated, case-sensitive string up too128 characters long.</span></span> <span data-ttu-id="eea30-214">이 값은 hello로 사용 되는 toodistinguish 장치 동일한 **deviceId**삭제 및 다시 생성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="eea30-214">This value is used toodistinguish devices with hello same **deviceId**, when they have been deleted and re-created.</span></span> |
| <span data-ttu-id="eea30-215">etag</span><span class="sxs-lookup"><span data-stu-id="eea30-215">etag</span></span> |<span data-ttu-id="eea30-216">필요한 경우 읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-216">required, read-only</span></span> |<span data-ttu-id="eea30-217">기준으로 hello 장치 id에 대 한 약한 ETag를 나타내는 문자열 [RFC7232][lnk-rfc7232]합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-217">A string representing a weak ETag for hello device identity, as per [RFC7232][lnk-rfc7232].</span></span> |
| <span data-ttu-id="eea30-218">auth</span><span class="sxs-lookup"><span data-stu-id="eea30-218">auth</span></span> |<span data-ttu-id="eea30-219">선택 사항</span><span class="sxs-lookup"><span data-stu-id="eea30-219">optional</span></span> |<span data-ttu-id="eea30-220">인증 정보 및 보안 자료를 포함하는 복합 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-220">A composite object containing authentication information and security materials.</span></span> |
| <span data-ttu-id="eea30-221">auth.symkey</span><span class="sxs-lookup"><span data-stu-id="eea30-221">auth.symkey</span></span> |<span data-ttu-id="eea30-222">선택 사항</span><span class="sxs-lookup"><span data-stu-id="eea30-222">optional</span></span> |<span data-ttu-id="eea30-223">base64 형식으로 저장된 기본 및 보조 키를 포함하는 복합 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-223">A composite object containing a primary and a secondary key, stored in base64 format.</span></span> |
| <span data-ttu-id="eea30-224">status</span><span class="sxs-lookup"><span data-stu-id="eea30-224">status</span></span> |<span data-ttu-id="eea30-225">필수</span><span class="sxs-lookup"><span data-stu-id="eea30-225">required</span></span> |<span data-ttu-id="eea30-226">액세스 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-226">An access indicator.</span></span> <span data-ttu-id="eea30-227">**사용** 또는 **사용 안 함**으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-227">Can be **Enabled** or **Disabled**.</span></span> <span data-ttu-id="eea30-228">경우 **Enabled**, hello 장치 tooconnect ï ´ ù.</span><span class="sxs-lookup"><span data-stu-id="eea30-228">If **Enabled**, hello device is allowed tooconnect.</span></span> <span data-ttu-id="eea30-229">**사용 안 함**이면 이 장치는 장치 연결 끝점에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-229">If **Disabled**, this device cannot access any device-facing endpoint.</span></span> |
| <span data-ttu-id="eea30-230">statusReason</span><span class="sxs-lookup"><span data-stu-id="eea30-230">statusReason</span></span> |<span data-ttu-id="eea30-231">선택 사항</span><span class="sxs-lookup"><span data-stu-id="eea30-231">optional</span></span> |<span data-ttu-id="eea30-232">128 문자 길이의 문자열 hello 장치 id 상태에 대 한 해당 저장소 hello 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-232">A 128 character-long string that stores hello reason for hello device identity status.</span></span> <span data-ttu-id="eea30-233">UTF-8 문자를 모두 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-233">All UTF-8 characters are allowed.</span></span> |
| <span data-ttu-id="eea30-234">statusUpdateTime</span><span class="sxs-lookup"><span data-stu-id="eea30-234">statusUpdateTime</span></span> |<span data-ttu-id="eea30-235">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-235">read-only</span></span> |<span data-ttu-id="eea30-236">상태 업데이트를 마지막 hello의 hello 날짜 및 시간을 보여 주는 임시 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-236">A temporal indicator, showing hello date and time of hello last status update.</span></span> |
| <span data-ttu-id="eea30-237">connectionState</span><span class="sxs-lookup"><span data-stu-id="eea30-237">connectionState</span></span> |<span data-ttu-id="eea30-238">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-238">read-only</span></span> |<span data-ttu-id="eea30-239">연결 상태를 나타내는 필드: **연결됨** 또는 **연결 끊김**.</span><span class="sxs-lookup"><span data-stu-id="eea30-239">A field indicating connection status: either **Connected** or **Disconnected**.</span></span> <span data-ttu-id="eea30-240">이 필드는 hello를 IoT Hub 보기의 hello 장치 연결 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-240">This field represents hello IoT Hub view of hello device connection status.</span></span> <span data-ttu-id="eea30-241">**중요**: 이 필드는 개발/디버깅 용도로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-241">**Important**: This field should be used only for development/debugging purposes.</span></span> <span data-ttu-id="eea30-242">hello 연결 상태가 MQTT 또는 AMQP를 사용 하 여 장치에 대해서만 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-242">hello connection state is updated only for devices using MQTT or AMQP.</span></span> <span data-ttu-id="eea30-243">또한 이는 프로토콜 수준의 ping(MQTT ping 또는 AMQP ping)을 기반으로 하고 있으며 최대 5분 동안만 지연이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-243">Also, it is based on protocol-level pings (MQTT pings, or AMQP pings), and it can have a maximum delay of only 5 minutes.</span></span> <span data-ttu-id="eea30-244">이러한 이유로, 연결되었지만 연결이 끊긴 것으로 보고된 장치와 같이 거짓 긍정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-244">For these reasons, there can be false positives, such as devices reported as connected but that are disconnected.</span></span> |
| <span data-ttu-id="eea30-245">connectionStateUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="eea30-245">connectionStateUpdatedTime</span></span> |<span data-ttu-id="eea30-246">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-246">read-only</span></span> |<span data-ttu-id="eea30-247">Hello 날짜 및 마지막 시간 hello 연결 상태와 함께 임시 표시기가 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-247">A temporal indicator, showing hello date and last time hello connection state was updated.</span></span> |
| <span data-ttu-id="eea30-248">lastActivityTime</span><span class="sxs-lookup"><span data-stu-id="eea30-248">lastActivityTime</span></span> |<span data-ttu-id="eea30-249">읽기 전용</span><span class="sxs-lookup"><span data-stu-id="eea30-249">read-only</span></span> |<span data-ttu-id="eea30-250">Hello 날짜 및 마지막 시간 hello 장치 연결 받거나 보낸 메시지와 함께 임시 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-250">A temporal indicator, showing hello date and last time hello device connected, received, or sent a message.</span></span> |

> [!NOTE]
> <span data-ttu-id="eea30-251">연결 상태 hello hello 연결의 hello 상태에 대 한 IoT Hub 보기 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-251">Connection state can only represent hello IoT Hub view of hello status of hello connection.</span></span> <span data-ttu-id="eea30-252">네트워크 상태 및 구성에 따라 업데이트 toothis 상태 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-252">Updates toothis state may be delayed, depending on network conditions and configurations.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="eea30-253">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="eea30-253">Additional reference material</span></span>

<span data-ttu-id="eea30-254">Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-254">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="eea30-255">[IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-255">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="eea30-256">[제한 및 할당량] [ lnk-quotas] hello 할당량을 설명 하 고 toohello IoT 허브 서비스에 적용 되는 동작을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-256">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="eea30-257">[Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-257">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="eea30-258">[IoT Hub 쿼리 언어] [ lnk-query] 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용할 수는 hello 쿼리 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-258">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="eea30-259">[IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-259">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eea30-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eea30-260">Next steps</span></span>

<span data-ttu-id="eea30-261">이제 어떻게 toouse hello IoT Hub id 레지스트리에 관심이 있을 수 있습니다 hello 다음 IoT 허브 개발자 가이드 항목에에서는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-261">Now you have learned how toouse hello IoT Hub identity registry, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="eea30-262">[컨트롤 액세스 tooIoT 허브][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="eea30-262">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="eea30-263">[장치 트윈스 toosynchronize 상태 및 구성 사용][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="eea30-263">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="eea30-264">[장치에서 직접 메서드 호출][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="eea30-264">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="eea30-265">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="eea30-265">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="eea30-266">이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea30-266">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="eea30-267">[Azure IoT Hub 시작][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="eea30-267">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>

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
