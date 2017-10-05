---
title: "Azure IoT Hub 장치 ID 가져오기 및 내보내기 | Microsoft Docs"
description: "Azure IoT 서비스 SDK를 사용하여 ID 레지스트리에 대한 대량 작업을 수행하고 장치 ID를 가져오기 및 내보내기를 수행하는 방법입니다. 가져오기 작업을 사용하여 대량으로 장치 ID를 생성, 업데이트 및 삭제할 수 있습니다."
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
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="51bea-104">대량으로 IoT Hub 장치 ID를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="51bea-105">각 IoT Hub에는 서비스에서 장치마다 리소스를 만드는 데 사용할 수 있는 ID 레지스트리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="51bea-106">또한 ID 레지스트리를 통해 장치 지향 끝점에 대한 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="51bea-107">이 문서에서는 ID 레지스트리에서 장치 ID를 대량으로 가져오고 내보내는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="51bea-108">가져오기 및 내보내기 작업은 사용자가 IoT Hub에 대해 대량 서비스 작업을 실행할 수 있는 *작업* 상황에서 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="51bea-109">**RegistryManager** 클래스는 **Job** 프레임워크를 사용하는 **ExportDevicesAsync** 및 **ImportDevicesAsync** 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="51bea-110">이러한 메서드를 사용하면 전체 IoT Hub ID 레지스트리를 내보내고, 가져오고, 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="51bea-111">작업이란?</span><span class="sxs-lookup"><span data-stu-id="51bea-111">What are jobs?</span></span>

<span data-ttu-id="51bea-112">ID 레지스트리 작업은 다음 작업을 수행할 때 **작업** 시스템을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="51bea-113">표준 런타임 작업에 비해 잠재적으로 실행 시간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="51bea-114">사용자에게 많은 양의 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="51bea-115">단일 API 호출을 기다리거나 작업 결과를 차단하는 대신에 작업은 비동기적으로 해당 IoT Hub에 대한 **작업**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="51bea-116">그런 다음 즉시 **JobProperties** 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="51bea-117">다음 C# 코드 조각은 작업을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="51bea-118">C# 코드에서 **RegistryManager** 클래스를 사용하려면 프로젝트에 **Microsoft.Azure.Devices** NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="51bea-119">**RegistryManager** 클래스는 **Microsoft.Azure.Devices** 네임스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="51bea-120">**RegistryManager** 클래스를 사용하면 반환된 **JobProperties** 메타데이터를 사용하는 **작업**의 상태를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="51bea-121">다음 C# 코드 조각은 매 5초마다 폴링하여 작업이 실행을 마쳤는지 여부를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="51bea-122">내보내기 장치</span><span class="sxs-lookup"><span data-stu-id="51bea-122">Export devices</span></span>

<span data-ttu-id="51bea-123">**ExportDevicesAsync** 메서드를 사용하여 [공유 액세스 서명](../storage/common/storage-security-guide.md#data-plane-security)을 사용하는 [Azure Storage](../storage/index.md) Blob 컨테이너에 전체 IoT Hub ID 레지스트리를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="51bea-124">이 메서드를 사용하면 사용자가 제어하는 blob에 장치 정보의 신뢰할 수 있는 백업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="51bea-125">**ExportDevicesAsync** 메서드에 매개변수 두 개를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="51bea-126">Blob 컨테이너의 URI가 포함된 *문자열* .</span><span class="sxs-lookup"><span data-stu-id="51bea-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="51bea-127">이 URI는 컨테이너에 대한 쓰기 액세스 권한을 부여하는 SAS 토큰을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="51bea-128">작업은 직렬화된 내보내기 장치 데이터를 저장하기 위해 이 컨테이너에 블록 blob를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="51bea-129">SAS 토큰은 이러한 사용 권한을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="51bea-130">내보내기 데이터에서 인증 키를 제외하려는지 여부를 나타내는 *부울* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="51bea-131">**false**인 경우 인증 키가 내보내기 출력에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="51bea-132">그렇지 않으면 키는 **null**로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="51bea-133">다음 C# 코드 조각은 내보내기 데이터에 장치 인증 키를 포함하고 있는 내보내기 작업을 시작한 다음 완료를 폴링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

<span data-ttu-id="51bea-134">작업은 출력을 제공된 blob 컨테이너에 이름 **devices.txt**의 블록 blob로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="51bea-135">출력 데이터는 JSON 직렬화된 장치 데이터로 구성되며 한 장치가 한 줄에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="51bea-136">다음 예제에서는 출력 데이터를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

장치에 쌍으로 된 데이터가 있는 경우 장치 데이터와 함께 내보내집니다. 다음 예제는 이러한 형식을 보여줍니다. <span data-ttu-id="51bea-139">"twinETag" 줄의 모든 데이터는 끝까지 쌍으로 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-139">All data from the "twinETag" line until the end are twin data.</span></span>

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

<span data-ttu-id="51bea-140">코드에서 이 데이터에 액세스해야 하는 경우 **ExportImportDevice** 클래스를 사용하여 이 데이터를 쉽게 역직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="51bea-141">다음 C# 코드 조각은 이전에 블록 blob에 내보낸 장치 정보를 읽는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

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
> <span data-ttu-id="51bea-142">**RegistryManager** 클래스의 **GetDevicesAsync** 메서드를 사용하여 장치의 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="51bea-143">그러나 이 방법은 반환되는 장치 개체의 수에 1000의 하드 캡이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="51bea-144">**GetDevicesAsync** 메서드에 대해 예상되는 사용 사례는 디버깅을 돕는 개발 시나리오에 대한 것이며 생산 워크로드에는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="51bea-145">장치 가져오기</span><span class="sxs-lookup"><span data-stu-id="51bea-145">Import devices</span></span>

<span data-ttu-id="51bea-146">**RegistryManager** 클래스의 **ImportDevicesAsync** 메서드를 사용하여 IoT Hub ID 레지스트리에서 대량 가져오기 및 동기화 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="51bea-147">**ExportDevicesAsync** 메서드와 마찬가지로 **ImportDevicesAsync** 메서드도 **작업** 프레임워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="51bea-148">ID 레지스트리에 새 장치를 프로비전할 뿐만 아니라 기존 장치를 업데이트 및 삭제할 수도 있으므로 **ImportDevicesAsync** 메서드를 사용할 때 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="51bea-149">가져오기 작업은 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-149">An import operation cannot be undone.</span></span> <span data-ttu-id="51bea-150">ID 레지스트리를 대량 변경하기 전에 항상 **ExportDevicesAsync** 메서드를 사용하여 기존 데이터를 다른 Blob 컨테이너에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="51bea-151">**ImportDevicesAsync** 메서드에 매개 변수 두 개를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="51bea-152">작업에 대한 *입력*으로 [Azure Storage](../storage/index.md) Blob 컨테이너의 URI가 포함된 *문자열*.</span><span class="sxs-lookup"><span data-stu-id="51bea-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="51bea-153">이 URI는 컨테이너에 대한 읽기 액세스 권한을 부여하는 SAS 토큰을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="51bea-154">이 컨테이너에는 ID 레지스트리에 가져올 직렬화된 장치 데이터가 포함된 **devices.txt** 이름의 Blob이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="51bea-155">가져오기 데이터는 **ExportImportDevice** 작업이 **devices.txt** Blob을 생성할 때 사용하는 것과 같은 JSON 형식의 장치 정보를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="51bea-156">SAS 토큰은 이러한 사용 권한을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="51bea-157">작업에서 *출력*으로 사용할 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob 컨테이너의 URI가 포함된 *문자열*.</span><span class="sxs-lookup"><span data-stu-id="51bea-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="51bea-158">작업은 이 컨테이너에 완료된 가져오기 **작업**에서 나온 오류 정보를 저장하기 위한 블록 blob를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="51bea-159">SAS 토큰은 이러한 사용 권한을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="51bea-160">두 매개 변수가 같은 blob 컨테이너를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="51bea-161">단순히 별도 매개 변수를 사용하여 출력 컨테이너에 추가 사용 권한이 필요할 때 데이터를 더 강력하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="51bea-162">다음 C# 코드 조각은 가져오기 작업을 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="51bea-163">장치 쌍에 데이터를 가져오는 데도 이 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="51bea-164">데이터 입력의 형식은 **ExportDevicesAsync** 섹션에 나온 형식과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="51bea-165">이러한 방식으로 내보낸 데이터를 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="51bea-166">**$metadata**는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="51bea-167">가져오기 동작</span><span class="sxs-lookup"><span data-stu-id="51bea-167">Import behavior</span></span>

<span data-ttu-id="51bea-168">**ImportDevicesAsync** 메서드를 사용하여 ID 레지스트리에서 다음 대량 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="51bea-169">새 장치 대량 등록</span><span class="sxs-lookup"><span data-stu-id="51bea-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="51bea-170">기존 장치의 대량 삭제</span><span class="sxs-lookup"><span data-stu-id="51bea-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="51bea-171">대량으로 상태 변경(장치를 사용 또는 사용하지 않도록 설정)</span><span class="sxs-lookup"><span data-stu-id="51bea-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="51bea-172">새 장치 인증 키의 대량 할당</span><span class="sxs-lookup"><span data-stu-id="51bea-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="51bea-173">장치 인증 키의 대량 자동 다시 생성</span><span class="sxs-lookup"><span data-stu-id="51bea-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="51bea-174">쌍으로 된 데이터의 대량 업데이트</span><span class="sxs-lookup"><span data-stu-id="51bea-174">Bulk update of twin data</span></span>

<span data-ttu-id="51bea-175">단일 **ImportDevicesAsync** 호출 내에서 이전 작업의 조합을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="51bea-176">예를 들어 새 장치를 등록하는 동시에 기존 장치를 삭제 또는 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="51bea-177">**ExportDevicesAsync** 메서드와 함께 사용하는 경우 모든 장치를 한 IoT Hub에서 다른 IoT Hub로 완전히 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="51bea-178">가져오기 파일에 쌍으로 된 메타데이터가 있는 경우 이 메타데이터는 쌍의 기존 메타데이터를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="51bea-179">가져오기 파일에 쌍 메타데이터가 포함되지 않은 경우 `lastUpdateTime` 메타데이터는 현재 시간을 사용하여 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="51bea-180">각 장치에 대한 가져오기 직렬화 데이터에 선택적 **importMode** 속성을 사용하여 가져오기 프로세스를 장치별로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="51bea-181">**importMode** 속성에 다음과 같은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="51bea-182">importMode</span><span class="sxs-lookup"><span data-stu-id="51bea-182">importMode</span></span> | <span data-ttu-id="51bea-183">설명</span><span class="sxs-lookup"><span data-stu-id="51bea-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51bea-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="51bea-184">**createOrUpdate**</span></span> |<span data-ttu-id="51bea-185">지정된 **ID**를 가진 장치가 존재하지 않는 경우, 새로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="51bea-186">장치가 이미 존재하는 경우 **ETag** 값과 관계 없이 제공된 입력 데이터가 기존 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="51bea-187">사용자는 장치 데이터와 함께 쌍으로 된 데이터를 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="51bea-188">쌍의 ETag을 지정하는 경우 장치의 ETag에서 독립적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="51bea-189">기존 쌍의 ETag와 일치하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-190">**create**</span><span class="sxs-lookup"><span data-stu-id="51bea-190">**create**</span></span> |<span data-ttu-id="51bea-191">지정된 **ID**를 가진 장치가 존재하지 않는 경우, 새로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="51bea-192">장치에 이미 존재하는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="51bea-193">사용자는 장치 데이터와 함께 쌍으로 된 데이터를 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="51bea-194">쌍의 ETag을 지정하는 경우 장치의 ETag에서 독립적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="51bea-195">기존 쌍의 ETag와 일치하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-196">**update**</span><span class="sxs-lookup"><span data-stu-id="51bea-196">**update**</span></span> |<span data-ttu-id="51bea-197">지정된 **ID**를 가진 장치가 이미 존재하는 경우 **ETag** 값과 관계 없이 제공된 입력 데이터가 기존 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="51bea-198">장치가 존재하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="51bea-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="51bea-200">지정된 **ID**를 가진 장치가 이미 존재하는 경우 **ETag**가 일치하는 경우에만 제공된 입력 데이터가 기존 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="51bea-201">장치가 존재하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="51bea-202">**ETag** 가 일치하지 않는 경우 불일치 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="51bea-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="51bea-204">지정된 **ID**를 가진 장치가 존재하지 않는 경우, 새로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="51bea-205">장치가 이미 존재하는 경우 **ETag** 가 일치하는 경우에만 제공된 입력 데이터가 기존 정보를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="51bea-206">**ETag** 가 일치하지 않는 경우 불일치 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="51bea-207">사용자는 장치 데이터와 함께 쌍으로 된 데이터를 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="51bea-208">쌍의 ETag을 지정하는 경우 장치의 ETag에서 독립적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="51bea-209">기존 쌍의 ETag와 일치하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-210">**delete**</span><span class="sxs-lookup"><span data-stu-id="51bea-210">**delete**</span></span> |<span data-ttu-id="51bea-211">지정된 **ID**를 가진 장치가 이미 존재하는 경우, **ETag** 값과 관계 없이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="51bea-212">장치가 존재하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="51bea-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="51bea-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="51bea-214">지정된 **ID**를 가진 장치가 이미 존재하는 경우, **ETag**가 일치하는 경우에만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="51bea-215">장치가 존재하지 않는 경우 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="51bea-216">ETag가 일치하지 않는 경우 불일치 오류가 로그 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="51bea-217">직렬화 데이터가 장치에 대한 **importMode** 플래그를 명시적으로 정의하는 경우 가져오기 작업 중에 기본적으로 **createOrUpdate**를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="51bea-218">장치 가져오기 예제 – 대량 장치 프로비저닝</span><span class="sxs-lookup"><span data-stu-id="51bea-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="51bea-219">다음 C# 코드 예제에서는 다음과 같은 여러 장치 ID를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="51bea-220">인증 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-220">Include authentication keys.</span></span>
* <span data-ttu-id="51bea-221">블록 Blob에 해당 장치 정보를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="51bea-222">장치를 ID 레지스트리로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="51bea-223">장치 가져오기 예제 – 대량 삭제</span><span class="sxs-lookup"><span data-stu-id="51bea-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="51bea-224">다음 코드 샘플은 이전 코드 샘플을 사용하여 추가한 장치를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="51bea-225">컨테이너 SAS URI 가져오기</span><span class="sxs-lookup"><span data-stu-id="51bea-225">Get the container SAS URI</span></span>

<span data-ttu-id="51bea-226">다음 코드 샘플은 blob 컨테이너에 대한 읽기, 쓰기 및 삭제 사용 권한을 가진 [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="51bea-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51bea-227">Next steps</span></span>

<span data-ttu-id="51bea-228">이 문서에서는 IoT Hub의 ID 레지스트리에 대한 대량 작업을 수행하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="51bea-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="51bea-229">Azure IoT Hub를 관리하는 방법에 대한 자세한 내용을 알아보려면 다음 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="51bea-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="51bea-230">[IoT Hub 메트릭][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="51bea-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="51bea-231">[작업 모니터링][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="51bea-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="51bea-232">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51bea-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="51bea-233">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="51bea-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="51bea-234">[IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="51bea-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
