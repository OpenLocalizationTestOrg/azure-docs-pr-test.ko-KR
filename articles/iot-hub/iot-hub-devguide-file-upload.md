---
title: "Azure IoT Hub 파일 업로드 이해 | Microsoft Docs"
description: "개발자 가이드 - IoT Hub의 파일 업로드 기능을 사용하여 장치에서 Azure Storage blob 컨테이너로 파일 업로드를 관리합니다."
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
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="8ad1f-103">IoT Hub를 사용하여 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="8ad1f-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="8ad1f-104">[IoT Hub 끝점][lnk-endpoints] 문서에서 설명한 대로 장치는 장치 지향 끝점(**/devices/{deviceId}/files**)을 통해 알림을 전송하여 파일 업로드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="8ad1f-105">장치가 IoT Hub에 완료된 업로드를 알리면 IoT Hub는 **/messages/servicebound/filenotifications** 서비스 지향 끝점을 통해 파일 업로드 알림 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="8ad1f-106">IoT Hub 자체를 통한 브로커 메시지 대신 IoT Hub는 연결된 Azure 저장소 계정에 대한 디스패처로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="8ad1f-107">장치는 장치가 업로드하려는 파일에 특정된 IoT Hub의 저장소 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="8ad1f-108">장치는 SAS URI를 사용하여 저장소에 파일을 업로드하고 업로드가 완료되면 장치는 IoT Hub에 완료 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="8ad1f-109">IoT Hub는 파일 업로드가 완료되었는지 확인한 다음 서비스 지향 파일 알림 끝점에 파일 업로드 알림 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="8ad1f-110">장치에서 IoT Hub로 파일을 업로드하려면 먼저 [Azure Storage 계정을 연결][lnk-associate-storage]하여 허브를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="8ad1f-111">그런 다음 장치에서 [업로드를 초기화][lnk-initialize]한 후 업로드가 완료되면 [IoT Hub에 알릴][lnk-notify] 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="8ad1f-112">필요에 따라 장치에서 IoT Hub에 업로드가 완료되었음을 알리면 서비스에서 [알림 메시지][lnk-service-notification]를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="8ad1f-113">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="8ad1f-113">When to use</span></span>

<span data-ttu-id="8ad1f-114">파일 업로드를 사용하여 간헐적으로 연결된 장치로 업로드되거나 대역폭을 절약하기 위해 압축된 미디어 파일과 대형 원격 분석 배치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="8ad1f-115">reported 속성, 장치-클라우드 메시지 또는 파일 업로드 사용에 대해 궁금한 점이 있으면 [장치-클라우드 통신 지침][lnk-d2c-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="8ad1f-116">Azure Storage 계정을 IoT Hub와 연결</span><span class="sxs-lookup"><span data-stu-id="8ad1f-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="8ad1f-117">파일 업로드 기능을 사용하려면 먼저 Azure 저장소 계정을 IoT Hub에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="8ad1f-118">[Azure Portal][lnk-management-portal]을 통하거나 [IoT Hub 리소스 공급자 REST API][lnk-resource-provider-apis]를 통해 프로그래밍 방식으로 이 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="8ad1f-119">Azure Storage 계정을 IoT Hub와 연결하면 서비스는 장치가 파일 업로드 요청을 시작할 때 장치에 SAS URI를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="8ad1f-120">[Azure IoT SDK][lnk-sdks]는 SAS URI 검색, 파일 업로드 및 IoT Hub에 완료된 업로드 알림을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="8ad1f-121">파일 업로드 초기화</span><span class="sxs-lookup"><span data-stu-id="8ad1f-121">Initialize a file upload</span></span>
<span data-ttu-id="8ad1f-122">IoT Hub는 파일을 업로드하기 위해 저장소에 대한 SAS URI를 요청하는 특히 장치에 대한 끝점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="8ad1f-123">파일 업로드 프로세스를 시작하기 위해 장치는 다음 JSON 본문을 사용하여 `{iot hub}.azure-devices.net/devices/{deviceId}/files`(으)로 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="8ad1f-124">IoT Hub는 파일을 업로드하기 위해 장치에서 사용할 다음 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="8ad1f-125">사용되지 않음: GET으로 파일 업로드 초기화</span><span class="sxs-lookup"><span data-stu-id="8ad1f-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="8ad1f-126">이 섹션에서는 IoT Hub에서 SAS URI를 수신하는 방법으로 더 이상 사용되지 않는 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="8ad1f-127">앞에서 설명한 POST 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-127">Use the POST method described previously.</span></span>

<span data-ttu-id="8ad1f-128">IoT Hub는 파일 업로드를 지원하는 두 개의 REST 끝점을 가집니다. 하나는 저장소에 대한 SAS URI를 가져오기 위한 것이고 다른 하나는 IoT Hub에 업로드 완료를 알리기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="8ad1f-129">장치는 `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`에서 IoT Hub에 GET을 전송하여 파일 업로드 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="8ad1f-130">IoT Hub는 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-130">The IoT hub returns:</span></span>

* <span data-ttu-id="8ad1f-131">업로드되는 파일에 해당하는 SAS URI.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="8ad1f-132">업로드가 완료되면 사용될 상관 관계 ID.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="8ad1f-133">IoT Hub에 완료된 파일 업로드 알림</span><span class="sxs-lookup"><span data-stu-id="8ad1f-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="8ad1f-134">장치는 Azure 저장소 SDK를 사용하여 저장소에 파일을 업로드하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="8ad1f-135">업로드가 완료되면 장치는 다음 JSON 본문으로 `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications`에 POST 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="8ad1f-136">`isSuccess` 값은 Boolean이며 파일이 성공적으로 업로드되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="8ad1f-137">`statusCode`에 대한 상태 코드는 파일을 저장소에 업로드하기 위한 상태이고 `statusDescription`은 `statusCode`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="8ad1f-138">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="8ad1f-138">Reference topics:</span></span>

<span data-ttu-id="8ad1f-139">다음 참조 항목에서는 장치에서 파일 업로드에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="8ad1f-140">파일 업로드 알림</span><span class="sxs-lookup"><span data-stu-id="8ad1f-140">File upload notifications</span></span>

<span data-ttu-id="8ad1f-141">선택적으로, 장치가 IoT Hub에 업로드가 완료되었음을 알릴 때 IoT Hub는 파일의 이름 및 저장 위치가 포함된 알림 메시지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="8ad1f-142">[끝점][lnk-endpoints]에서 설명한 대로 IoT Hub는 서비스 지향 끝점(**/messages/servicebound/fileuploadnotifications**)을 통해 파일 업로드 알림을 메시지로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="8ad1f-143">파일 업로드 알림에 대한 수신 의미 체계는 클라우드-장치 메시지의 경우와 동일하며 동일한 [메시지 수명 주기][lnk-lifecycle]를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="8ad1f-144">파일 업로드 알림 끝점에서 검색된 각 메시지는 다음 속성을 가진 JSON 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="8ad1f-145">속성</span><span class="sxs-lookup"><span data-stu-id="8ad1f-145">Property</span></span> | <span data-ttu-id="8ad1f-146">설명</span><span class="sxs-lookup"><span data-stu-id="8ad1f-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ad1f-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="8ad1f-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="8ad1f-148">알림을 만든 시간을 나타내는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="8ad1f-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="8ad1f-149">DeviceId</span></span> |<span data-ttu-id="8ad1f-150">**DeviceId** 입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="8ad1f-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="8ad1f-151">BlobUri</span></span> |<span data-ttu-id="8ad1f-152">업로드된 파일의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="8ad1f-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="8ad1f-153">BlobName</span></span> |<span data-ttu-id="8ad1f-154">업로드된 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="8ad1f-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="8ad1f-155">LastUpdatedTime</span></span> |<span data-ttu-id="8ad1f-156">파일이 마지막으로 업데이트된 시간을 나타내는 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="8ad1f-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="8ad1f-157">BlobSizeInBytes</span></span> |<span data-ttu-id="8ad1f-158">업로드된 파일의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="8ad1f-159">**예제**.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-159">**Example**.</span></span> <span data-ttu-id="8ad1f-160">이 예제는 파일 업로드 알림 메시지의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-160">This example shows the body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="8ad1f-161">파일 업로드 알림 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="8ad1f-161">File upload notification configuration options</span></span>

<span data-ttu-id="8ad1f-162">각 IoT Hub는 파일 업로드 알림에 다음 구성 옵션을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="8ad1f-163">속성</span><span class="sxs-lookup"><span data-stu-id="8ad1f-163">Property</span></span> | <span data-ttu-id="8ad1f-164">설명</span><span class="sxs-lookup"><span data-stu-id="8ad1f-164">Description</span></span> | <span data-ttu-id="8ad1f-165">범위 및 기본값</span><span class="sxs-lookup"><span data-stu-id="8ad1f-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ad1f-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="8ad1f-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="8ad1f-167">파일 업로드 알림이 파일 알림 끝점에 작성되는지를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="8ad1f-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-168">Bool.</span></span> <span data-ttu-id="8ad1f-169">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-169">Default: True.</span></span> |
| <span data-ttu-id="8ad1f-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="8ad1f-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="8ad1f-171">파일 업로드 알림에 대한 기본 TTL입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="8ad1f-172">최대 48H(최소 1 분)까지 ISO_8601 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="8ad1f-173">기본값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="8ad1f-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="8ad1f-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="8ad1f-175">파일 업로드 알림 큐에 대한 잠금 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="8ad1f-176">5에서 300초(최소 5초)입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="8ad1f-177">기본값은 60초입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="8ad1f-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="8ad1f-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="8ad1f-179">파일 업로드 알림 큐에 대한 최대 배달 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="8ad1f-180">1에서 100까지입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-180">1 to 100.</span></span> <span data-ttu-id="8ad1f-181">기본값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="8ad1f-182">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="8ad1f-182">Additional reference material</span></span>

<span data-ttu-id="8ad1f-183">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="8ad1f-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="8ad1f-184">[IoT Hub 끝점][lnk-endpoints] - 각 IoT Hub에서 런타임 및 관리 작업에 대해 공개하는 다양한 끝점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="8ad1f-185">[제한 및 할당량][lnk-quotas]은 IoT Hub 서비스에 적용되는 할당량과 제한 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="8ad1f-186">[Azure IoT 장치 및 서비스 SDK][lnk-sdks] - IoT Hub와 상호 작용하는 장치 및 서비스 앱 모두를 개발할 때 사용할 수 있는 다양한 언어 SDK를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="8ad1f-187">[IoT Hub 쿼리 언어][lnk-query]는 IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용할 수 있는 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="8ad1f-188">[IoT Hub MQTT 지원][lnk-devguide-mqtt] - MQTT 프로토콜에 대한 IoT Hub 지원에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ad1f-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ad1f-189">Next steps</span></span>

<span data-ttu-id="8ad1f-190">IoT Hub를 사용하여 장치에서 파일을 업로드하는 방법에 대해 알아봤으니 다음 IoT Hub 개발자 가이드 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="8ad1f-191">[IoT Hub에서 장치 ID 관리][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="8ad1f-192">[IoT Hub에 대한 액세스 제어][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="8ad1f-193">[장치 쌍을 사용하여 상태 및 구성 동기화][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="8ad1f-194">[장치에서 직접 메서드 호출][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="8ad1f-195">[여러 장치에서 jobs 예약][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="8ad1f-196">이 문서에서 설명한 일부 개념을 시도해 보려면 다음과 같은 IoT Hub 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="8ad1f-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="8ad1f-197">[IoT Hub를 사용하여 장치에서 클라우드로 파일을 업로드하는 방법][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="8ad1f-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
