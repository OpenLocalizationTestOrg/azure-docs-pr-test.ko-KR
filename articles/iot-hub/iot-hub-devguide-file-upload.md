---
title: "Azure IoT Hub 파일 업로드 aaaUnderstand | Microsoft Docs"
description: "개발자 가이드-IoT Hub toomanage 장치 tooan Azure 저장소 blob 컨테이너에서 파일 업로드 중 사용 하 여 hello 파일 업로드 기능입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="4e11c-103">IoT Hub를 사용하여 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="4e11c-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="4e11c-104">Hello에 설명 된 대로 [IoT Hub 끝점] [ lnk-endpoints] 문서, 장치를 장치에 연결 끝점을 통해 알림을 전송 하 여 파일 업로드를 시작할 수 있습니다 (**/devices/ {deviceId}파일/**).</span><span class="sxs-lookup"><span data-stu-id="4e11c-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="4e11c-105">IoT Hub hello 통해 파일 업로드 알림 메시지를 보냅니다는 업로드가 완료 되는 되는 장치 IoT Hub을 확인 하면 **/messages/servicebound/filenotifications** 웹 서비스 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="4e11c-106">IoT Hub 자체 IoT 허브를 통해 메시지를 조정 하는 대신 발송자 tooan 연결 된 Azure 저장소 계정으로 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="4e11c-107">장치는 tooupload 하지 않고자 한다면 특정 toohello 파일 hello 장치가 IoT 허브에서 저장소 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="4e11c-108">hello 장치에서 SAS URI tooupload hello 파일 toostorage hello를 사용 하 고 hello 장치 완료 tooIoT 허브에 대 한 알림을 보냅니다 hello 업로드가 완료 되 면 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="4e11c-109">IoT Hub hello 파일 업로드가 완료 되 고 다음 파일 업로드 알림 메시지 toohello 서비스 지향 파일 알림 끝점에 추가 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="4e11c-110">장치에서 파일 tooIoT 허브를 업로드 하기 전에 하 여 허브를 구성 해야 [Azure 저장소 연결] [ lnk-associate-storage] tooit 계정.</span><span class="sxs-lookup"><span data-stu-id="4e11c-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="4e11c-111">그런 다음 다른 장치를 [업로드 초기화] [ lnk-initialize] 차례로 [IoT hub를 알릴] [ lnk-notify] hello 업로드가 완료 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="4e11c-112">필요에 따라 해당 hello 업로드가 완료 되 되는 장치가 IoT Hub을 확인 하면 hello 서비스 수를 생성 한 [알림 메시지][lnk-service-notification]합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="4e11c-113">때 toouse</span><span class="sxs-lookup"><span data-stu-id="4e11c-113">When toouse</span></span>

<span data-ttu-id="4e11c-114">파일 업로드 toosend 미디어 파일 및 간헐적으로 연결 된 장치 또는 압축 된 toosave 대역폭에서 업로드 하는 큰 원격 분석 일괄 처리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="4e11c-115">너무 참조[장치-클라우드 통신 지침] [ lnk-d2c-guidance] 보고 속성, 장치-클라우드 메시지 또는 파일을 업로드 하 여 확실 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="4e11c-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="4e11c-116">Azure Storage 계정을 IoT Hub와 연결</span><span class="sxs-lookup"><span data-stu-id="4e11c-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="4e11c-117">toouse hello 파일 업로드 기능을 먼저 Azure 저장소 계정 toohello IoT 허브 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="4e11c-118">Hello를 통해이 작업을 완료할 수 [Azure 포털][lnk-management-portal], 또는 hello를 통해 프로그래밍 방식으로 [IoT 허브 리소스 공급자 REST Api] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="4e11c-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="4e11c-119">IoT Hub와 Azure 저장소 계정을 연결한 후 hello 서비스 장치를 반납 SAS URI tooa hello 장치 파일 업로드 요청을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="4e11c-120">hello [Azure IoT Sdk] [ lnk-sdks] 자동으로 SAS URI hello 파일을 업로드 하 고 업로드 완료의 IoT 허브를 알리는 hello 핸들을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="4e11c-121">파일 업로드 초기화</span><span class="sxs-lookup"><span data-stu-id="4e11c-121">Initialize a file upload</span></span>
<span data-ttu-id="4e11c-122">IoT Hub에 장치 toorequest 저장소 tooupload 파일에 대 한 SAS URI에 대 한 구체적으로 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="4e11c-123">tooinitiate hello 파일 업로드 프로세스가 hello 전송 하는 장치에 POST 요청 너무`{iot hub}.azure-devices.net/devices/{deviceId}/files` JSON 본문을 수행 하는 hello로:</span><span class="sxs-lookup"><span data-stu-id="4e11c-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="4e11c-124">IoT Hub 같은 tooupload hello 파일을 사용 하 여 hello 장치 데이터가 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="4e11c-125">사용되지 않음: GET으로 파일 업로드 초기화</span><span class="sxs-lookup"><span data-stu-id="4e11c-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="4e11c-126">이 섹션에서는 사용 되지 않는 기능 방법에 대 한 설명 tooreceive IoT 허브에서 SAS URI입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="4e11c-127">앞에서 설명한 hello POST 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="4e11c-128">IoT Hub에 두 개의 REST 끝점 toosupport 파일이 저장소에 대 한 하나의 tooget hello SAS URI를 업로드 하 고 다른 toonotify hello IoT hub 업로드 완료의 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="4e11c-129">hello 장치 시작 hello 파일 업로드 프로세스에서 GET toohello IoT 허브를 전송 하 여 `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="4e11c-130">hello IoT hub를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="4e11c-131">특정 toohello 파일 toobe 업로드 하는 SAS URI입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="4e11c-132">상관 관계 ID toobe hello 업로드를 완료 한 후 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="4e11c-133">IoT Hub에 완료된 파일 업로드 알림</span><span class="sxs-lookup"><span data-stu-id="4e11c-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="4e11c-134">hello 장치는 hello 파일 toostorage hello Azure 저장소 Sdk를 사용 하 여 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="4e11c-135">Hello 장치 너무 POST 요청을 보냅니다 hello 업로드가 완료 되 면`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` JSON 본문을 수행 하는 hello로:</span><span class="sxs-lookup"><span data-stu-id="4e11c-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="4e11c-136">값을 hello `isSuccess` 은 성공적으로 업로드 된 hello 파일이 있는지 여부를 나타내는 Boolean입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="4e11c-137">상태 코드에 대 한 hello `statusCode` hello hello 파일 toostorage의 hello 업로드에 대 한 상태 이며 hello `statusDescription` toohello 해당 `statusCode`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="4e11c-138">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="4e11c-138">Reference topics:</span></span>

<span data-ttu-id="4e11c-139">hello 다음 참조 항목 제공 장치에서 파일을 업로드 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="4e11c-140">파일 업로드 알림</span><span class="sxs-lookup"><span data-stu-id="4e11c-140">File upload notifications</span></span>

<span data-ttu-id="4e11c-141">필요에 따라 장치를 메시지를 표시 IoT 허브는 업로드가 완료 되 IoT Hub hello 파일의 hello 이름 및 저장소 위치를 포함 하는 알림 메시지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="4e11c-142">[끝점][lnk-endpoints]에서 설명한 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/fileuploadnotifications**)을 통해 파일 업로드 알림을 메시지로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="4e11c-143">파일 업로드 알림 되며 클라우드-장치 메시지의 경우와 동일 hello 동일 hello 있는 hello 수신 의미 체계 [메시지 수명 주기][lnk-lifecycle]합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="4e11c-144">Hello 파일 업로드 알림 끝점에서 검색 된 각 메시지는 다음과 같은 속성 hello로 JSON 레코드:</span><span class="sxs-lookup"><span data-stu-id="4e11c-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="4e11c-145">속성</span><span class="sxs-lookup"><span data-stu-id="4e11c-145">Property</span></span> | <span data-ttu-id="4e11c-146">설명</span><span class="sxs-lookup"><span data-stu-id="4e11c-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e11c-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="4e11c-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="4e11c-148">Hello 알림이 생성 될 때를 나타내는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="4e11c-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="4e11c-149">DeviceId</span></span> |<span data-ttu-id="4e11c-150">**DeviceId** hello 장치 hello 파일 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="4e11c-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="4e11c-151">BlobUri</span></span> |<span data-ttu-id="4e11c-152">Hello 업로드 된 파일의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="4e11c-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="4e11c-153">BlobName</span></span> |<span data-ttu-id="4e11c-154">파일을 업로드 하는 hello의 이름.</span><span class="sxs-lookup"><span data-stu-id="4e11c-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="4e11c-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="4e11c-155">LastUpdatedTime</span></span> |<span data-ttu-id="4e11c-156">Hello 파일에 마지막으로 업데이트를 나타내는 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="4e11c-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="4e11c-157">BlobSizeInBytes</span></span> |<span data-ttu-id="4e11c-158">Hello의 크기는 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="4e11c-159">**예제**.</span><span class="sxs-lookup"><span data-stu-id="4e11c-159">**Example**.</span></span> <span data-ttu-id="4e11c-160">이 예제에서는 파일 hello 본문 업로드 알림 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-160">This example shows hello body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="4e11c-161">파일 업로드 알림 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="4e11c-161">File upload notification configuration options</span></span>

<span data-ttu-id="4e11c-162">각 IoT 허브는 다음 구성 옵션에 대 한 파일 업로드 알림 hello를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="4e11c-163">속성</span><span class="sxs-lookup"><span data-stu-id="4e11c-163">Property</span></span> | <span data-ttu-id="4e11c-164">설명</span><span class="sxs-lookup"><span data-stu-id="4e11c-164">Description</span></span> | <span data-ttu-id="4e11c-165">범위 및 기본값</span><span class="sxs-lookup"><span data-stu-id="4e11c-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e11c-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="4e11c-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="4e11c-167">파일 업로드 알림 toohello 파일 notifications 끝점에 기록 되는지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="4e11c-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="4e11c-168">Bool.</span></span> <span data-ttu-id="4e11c-169">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-169">Default: True.</span></span> |
| <span data-ttu-id="4e11c-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="4e11c-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="4e11c-171">파일 업로드 알림에 대한 기본 TTL입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="4e11c-172">Too48H ISO_8601 간격 (최소 1 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="4e11c-173">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="4e11c-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="4e11c-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="4e11c-175">Hello 파일 업로드 알림 큐에 대 한 잠금 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="4e11c-176">5 too300 초 (최소 5 초)입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="4e11c-177">기본값은 60초입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="4e11c-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="4e11c-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="4e11c-179">최대 배달 횟수 hello 파일에 대 한 알림 큐를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="4e11c-180">1 too100 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-180">1 too100.</span></span> <span data-ttu-id="4e11c-181">기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="4e11c-182">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="4e11c-182">Additional reference material</span></span>

<span data-ttu-id="4e11c-183">Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4e11c-184">[IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4e11c-185">[제한 및 할당량] [ lnk-quotas] hello 할당량을 설명 하 고 toohello IoT 허브 서비스에 적용 되는 동작을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="4e11c-186">[Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4e11c-187">[IoT Hub 쿼리 언어] [ lnk-query] 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용할 수는 hello 쿼리 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4e11c-188">[IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e11c-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e11c-189">Next steps</span></span>

<span data-ttu-id="4e11c-190">IoT 허브를 사용 하 여 장치에서 파일을 tooupload 방법 파악 했으므로, 이제 hello 다음 IoT 허브 개발자 가이드 항목에에서 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="4e11c-191">[IoT Hub에서 장치 ID 관리][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="4e11c-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="4e11c-192">[컨트롤 액세스 tooIoT 허브][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="4e11c-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="4e11c-193">[장치 트윈스 toosynchronize 상태 및 구성 사용][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="4e11c-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="4e11c-194">[장치에서 직접 메서드 호출][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="4e11c-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="4e11c-195">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="4e11c-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="4e11c-196">이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e11c-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="4e11c-197">[IoT Hub와 장치 toohello에서 tooupload 파일 클라우드 하는 방법][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4e11c-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
