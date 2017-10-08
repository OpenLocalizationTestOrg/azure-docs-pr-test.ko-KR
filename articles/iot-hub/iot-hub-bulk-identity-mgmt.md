---
title: "Azure IoT Hub 장치 id의 aaaImport 내보내기 | Microsoft Docs"
description: "어떻게 toouse hello Azure IoT 서비스 SDK tooperform 대량 hello identity 레지스트리 tooimport에 대해 작업 하 고 장치 id를 내보냅니다. 가져오기 작업을 사용 하면 toocreate, 업데이트 및 대량에서 삭제 장치 id입니다."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>대량으로 IoT Hub 장치 ID를 관리합니다.

각 IoT 허브 toocreate 장치 리소스를 사용 하 여 hello 서비스에서 id 레지스트리에에 있습니다. hello id 레지스트리에 에서도 toocontrol 액세스 toohello 장치 쪽 끝점 수 있습니다. 이 문서에서는 tooimport 및 내보내기 장치 id에 identity 레지스트리에서 tooand 대량 하는 방법을 설명 합니다.

가져오기 및 내보내기 작업의 hello 컨텍스트에서 수행 *작업* IoT 허브에 대해 tooexecute 대량 서비스 작업 수 있는 합니다.

hello **RegistryManager** 클래스 포함 hello **ExportDevicesAsync** 및 **ImportDevicesAsync** hello를 사용 하는 메서드 **작업** 프레임 워크입니다. 이러한 메서드를 사용 하면 tooexport, 가져오기, 고 IoT 허브 id 레지스트리에 hello 전체를 동기화 합니다.

## <a name="what-are-jobs"></a>작업이란?

Identity 레지스트리 작업 hello를 사용 하 여 **작업** 시스템 때 작업을 hello:

* 잠재적으로 긴 실행 시간에 toostandard 런타임 작업을 비교 합니다.
* 많은 양의 데이터 toohello 사용자를 반환합니다.

단일 API 호출 기다리거나 hello 연산의 hello 결과 차단 하는 대신 hello 작업이 비동기적으로 만듭니다는 **작업** 해당 IoT 허브에 대 한 합니다. hello 작업 다음 즉시 반환은 **JobProperties** 개체입니다.

다음 C# hello 코드 조각과 방법을 toocreate 내보내기 작업의 경우:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> toouse hello **RegistryManager** C# 코드에서 클래스, 추가 hello **Microsoft.Azure.Devices** NuGet 패키지 tooyour 프로젝트. hello **RegistryManager** 클래스가 hello 중인 **Microsoft.Azure.Devices** 네임 스페이스입니다.

Hello를 사용할 수 있습니다 **RegistryManager** tooquery hello 상태의 hello 클래스 **작업** 반환 hello를 사용 하 여 **JobProperties** 메타 데이터입니다.

hello 다음 C# 코드 조각 표시 방법을 toopoll 마다 5 초 toosee 경우 hello 작업의 실행이 완료:

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a>내보내기 장치

사용 하 여 hello **ExportDevicesAsync** 메서드는 IoT 허브 identity 레지스트리 tooan tooexport hello 전체 [Azure 저장소](../storage/index.md) 사용 하 여 blob 컨테이너는 [공유 액세스 서명을](../storage/common/storage-security-guide.md#data-plane-security)합니다.

이 방법을 사용 하면 사용자가 제어 하는 blob 컨테이너에 장치 정보 toocreate 신뢰할 수 있는 백업을 있습니다.

hello **ExportDevicesAsync** 메서드에 두 개의 매개 변수가 필요 합니다.

* Blob 컨테이너의 URI가 포함된 *문자열* . 이 URI는 toohello 컨테이너 쓰기 액세스 권한을 부여 하는 SAS 토큰을 포함 해야 합니다. hello 작업이 컨테이너 toostore 직렬화 hello 내보내기 장치 데이터에 블록 blob을 만듭니다. hello SAS 토큰에는 이러한 사용 권한을 포함 해야 합니다.

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A *부울* 표시 하는 경우 tooexclude 인증 키 내보내기 데이터에서 합니다. **false**인 경우 인증 키가 내보내기 출력에 포함됩니다. 그렇지 않으면 키는 **null**로 내보내집니다.

hello 다음 C# 코드 조각 표시 방법을 tooinitiate hello에서 장치 인증 키를 포함 하는 내보내기 작업의 데이터를 내보내고 완료에 대 한 다음 폴링:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

hello 작업 저장 출력 hello 제공 된 blob 컨테이너에서 hello 이름의 블록 blob으로 **devices.txt**합니다. JSON으로 직렬화 된 장치 데이터 hello 출력 데이터 줄당 하나씩으로 구성 됩니다.

hello 다음 예제는 hello 출력 데이터.

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

장치에로 이중 데이터가 hello로 이중 데이터 hello 장치 데이터와 함께 내보낼도 됩니다. hello 다음 예제에서는이 형식을 Hello 끝까지 hello "twinETag" 줄의 모든 데이터는로 이중 데이터입니다.

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

코드의 toothis 데이터에 액세스 해야 하는 경우 쉽게 hello를 사용 하 여이 데이터를 deserialize 수 **ExportImportDevice** 클래스입니다. hello C# 만드는 코드는 이전에 내보낸 tooa 블록 blob를 어떻게 있던 tooread 장치 정보:

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> Hello를 사용할 수도 있습니다 **GetDevicesAsync** hello 방식의 **RegistryManager** 클래스 toofetch 장치의 목록입니다. 그러나이 방법 hello 반환 되는 장치 개체 수에 1000의 하드 캡에. hello 예상 hello에 대 한 사용 사례 **GetDevicesAsync** 메서드는 개발 시나리오 tooaid 디버깅 및 프로덕션 작업에 권장 되지 않습니다.

## <a name="import-devices"></a>장치 가져오기

hello **ImportDevicesAsync** hello에 대 한 메서드 **RegistryManager** 클래스 IoT 허브 id 레지스트리에의 tooperform 대량 가져오기 및 동기화 작업을 수 있습니다. Hello 처럼 **ExportDevicesAsync** 메서드, hello **ImportDevicesAsync** 방법은 hello를 사용 하 여 **작업** 프레임 워크입니다.

Hello를 사용 하 여 주의 **ImportDevicesAsync** 메서드 추가 tooprovisioning 새 장치에서 identity 레지스트리에서 또한 업데이트 및 기존 장치를 삭제 하기 때문에 있습니다.

> [!WARNING]
> 가져오기 작업은 실행 취소할 수 없습니다. 항상 hello를 사용 하 여 기존 데이터를 백업 **ExportDevicesAsync** 메서드 tooanother blob 컨테이너 대량 하기 전에 tooyour identity 레지스트리를 변경 합니다.

hello **ImportDevicesAsync** 메서드는 두 개의 매개 변수를 사용 합니다.

* A *문자열* 의 URI를 포함 하는 [Azure 저장소](../storage/index.md) blob으로 컨테이너 toouse *입력* toohello 작업 합니다. 이 URI는 toohello 컨테이너 읽기 액세스 권한을 부여 하는 SAS 토큰을 포함 해야 합니다. 이 컨테이너에서 hello 이름의 blob를 포함 해야 **devices.txt** identity 레지스트리로 직렬화 하는 hello 장치 데이터 tooimport를 포함 하 합니다. hello 데이터 가져오기 정보를 포함 해야 장치 hello에 동일한 JSON 형식을 해당 hello **ExportImportDevice** 를 만들 때 작업에 사용 하 여 한 **devices.txt** blob입니다. hello SAS 토큰에는 이러한 사용 권한을 포함 해야 합니다.

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A *문자열* 의 URI를 포함 하는 [Azure 저장소](https://azure.microsoft.com/documentation/services/storage/) blob으로 컨테이너 toouse *출력* hello 작업에서. hello 작업 블록 blob이 컨테이너 toostore의 오류 정보에서에서 만듭니다 완료 hello 가져오기 **작업**합니다. hello SAS 토큰에는 이러한 사용 권한을 포함 해야 합니다.

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> hello 두 매개 변수는 toohello를 가리킬 수 같은 blob 컨테이너입니다. hello 별도 매개 변수는 단순히 hello 출력 컨테이너의 추가 사용 권한이 필요에 따라 더 많이 제어할 데이터를 사용 합니다.

다음 C# hello 코드 조각과 방법을 tooinitiate 가져오기 작업:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

이 메서드는 hello 장치로 이중에 대 한 사용된 tooimport hello 데이터 될 수도 있습니다. hello 데이터 입력에 대 한 hello 형식은 동일 hello 형식 hello에 표시 된 것으로 hello **ExportDevicesAsync** 섹션. 이러한 방식으로 hello 내보낸 데이터를 다시 가져올 수 있습니다. hello **$metadata** 선택 사항입니다.

## <a name="import-behavior"></a>가져오기 동작

Hello를 사용할 수 있습니다 **ImportDevicesAsync** 메서드 tooperform hello 다음 대량 작업 id 레지스트리에에서:

* 새 장치 대량 등록
* 기존 장치의 대량 삭제
* 대량으로 상태 변경(장치를 사용 또는 사용하지 않도록 설정)
* 새 장치 인증 키의 대량 할당
* 장치 인증 키의 대량 자동 다시 생성
* 쌍으로 된 데이터의 대량 업데이트

어떠한 조합의 hello 앞에 단일 내에서 작업을 수행할 수 있습니다 **ImportDevicesAsync** 호출 합니다. 예를 들어 새 장치를 등록 하 고 삭제 하거나 업데이트할 수 있습니다 hello에 대 한 기존 장치 같은 시간입니다. Hello와 함께 사용할 경우 **ExportDevicesAsync** 메서드를 한 IoT 허브 tooanother에서 모든 장치를 완전히 마이그레이션할 수 있습니다.

파일 가져오기 hello로 이중 메타 데이터를 포함 하는 경우이 메타 데이터는 hello 기존의 이중 메타 데이터를 덮어씁니다. Hello 파일 가져오기로 이중 메타 데이터를 포함 하지 않는 경우 다음만 hello `lastUpdateTime` 현재 시간 hello를 사용 하 여 메타 데이터가 업데이트 됩니다.

사용 하 여 hello 선택적 **importMode** hello 각 장치 toocontrol hello 가져오기 프로세스 당 장치에 대 한 serialization 데이터 가져오기에에서는 속성입니다. hello **importMode** 속성에는 다음 옵션 hello:

| importMode | 설명 |
| --- | --- |
| **createOrUpdate** |장치를 지정 하는 hello로 존재 하지 않는 경우 **id**, 새로 등록 됩니다. <br/>Hello 장치에 이미 있으면 기존 정보를 toohello와 관계 없이 입력된 데이터를 제공 하는 hello로 덮어씁니다 **ETag** 값입니다. <br> hello 사용자 hello 장치 데이터와 함께 이중 데이터를 지정할 수 있습니다. hello로 이중 etag은 지정 하는 경우는 독립적으로 처리할 hello 장치 etag에서 합니다. Hello 기존로 이중 etag와 일치 하지 않습니다 이면 오류가 toohello 로그 파일을 기록 됩니다. |
| **create** |장치를 지정 하는 hello로 존재 하지 않는 경우 **id**, 새로 등록 됩니다. <br/>Hello 장치에 이미 있으면 오류가 toohello 로그 파일을 기록 됩니다. <br> hello 사용자 hello 장치 데이터와 함께 이중 데이터를 지정할 수 있습니다. hello로 이중 etag은 지정 하는 경우는 독립적으로 처리할 hello 장치 etag에서 합니다. Hello 기존로 이중 etag와 일치 하지 않습니다 이면 오류가 toohello 로그 파일을 기록 됩니다. |
| **update** |장치를 지정 하는 hello로 이미 있는 경우 **id**, toohello와 관계 없이 입력된 데이터를 제공 하는 hello로 기존 정보를 덮어씁니다 **ETag** 값입니다. <br/>Hello 장치가 없는 경우 오류가 toohello 로그 파일을 기록 됩니다. |
| **updateIfMatchETag** |장치를 지정 하는 hello로 이미 있는 경우 **id**, 경우에 입력된 데이터를 제공 하는 hello로 기존 정보를 덮어씁니다는 **ETag** 일치 합니다. <br/>Hello 장치가 없는 경우 오류가 toohello 로그 파일을 기록 됩니다. <br/>없는 경우는 **ETag** 불일치 오류가 toohello 로그 파일을 기록 됩니다. |
| **createOrUpdateIfMatchETag** |장치를 지정 하는 hello로 존재 하지 않는 경우 **id**, 새로 등록 됩니다. <br/>경우에 입력된 데이터를 제공 하는 hello로 기존 정보를 덮어씁니다 hello 장치에 이미 있으면는 **ETag** 일치 합니다. <br/>없는 경우는 **ETag** 불일치 오류가 toohello 로그 파일을 기록 됩니다. <br> hello 사용자 hello 장치 데이터와 함께 이중 데이터를 지정할 수 있습니다. hello로 이중 etag은 지정 하는 경우는 독립적으로 처리할 hello 장치 etag에서 합니다. Hello 기존로 이중 etag와 일치 하지 않습니다 이면 오류가 toohello 로그 파일을 기록 됩니다. |
| **delete** |장치를 지정 하는 hello로 이미 있는 경우 **id**, 큰지에 toohello 없이 삭제 됩니다 **ETag** 값입니다. <br/>Hello 장치가 없는 경우 오류가 toohello 로그 파일을 기록 됩니다. |
| **deleteIfMatchETag** |장치를 지정 하는 hello로 이미 있는 경우 **id**, 경우에 삭제 되는 **ETag** 일치 합니다. Hello 장치가 없는 경우 오류가 toohello 로그 파일을 기록 됩니다. <br/>ETag 불일치 이면 오류가 toohello 로그 파일을 기록 됩니다. |

> [!NOTE]
> Hello serialization 데이터 명시적으로 정의 하지 않는 경우는 **importMode** 플래그는 장치에 대 한 기본값 너무**createOrUpdate** hello 동안 가져오기 작업입니다.

## <a name="import-devices-example--bulk-device-provisioning"></a>장치 가져오기 예제 – 대량 장치 프로비저닝

hello 다음 C# 코드 예제에서는 어떻게 toogenerate 여러 장치 id입니다.

* 인증 키를 포함합니다.
* 해당 장치 정보 tooa 블록 blob를 작성 합니다.
* Hello id 레지스트리에로 hello 장치를 가져옵니다.

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a>장치 가져오기 예제 – 대량 삭제

hello 다음 코드 샘플 표시 방법을 사용 하 여 추가한 toodelete hello 장치 hello 앞의 코드 예제:

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a>Hello 컨테이너 SAS URI 가져오기

hello 다음 코드 샘플에서는 toogenerate는 [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) 읽기, 쓰기 및 blob 컨테이너에 대 한 권한을 삭제 합니다.

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a>다음 단계

이 문서에서는 tooperform 대량 IoT 허브에서 id 레지스트리에 hello에 대 한 작업 하는 방법을 배웠습니다. 이러한 링크 toolearn Azure IoT Hub를 관리 하는 방법에 대 한 자세한를 수행 합니다.

* [IoT Hub 메트릭][lnk-metrics]
* [작업 모니터링][lnk-monitor]

toofurther는 IoT Hub의 hello 기능을 참조 하십시오.

* [IoT Hub 개발자 가이드][lnk-devguide]
* [IoT Edge에서 장치 시뮬레이션][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
