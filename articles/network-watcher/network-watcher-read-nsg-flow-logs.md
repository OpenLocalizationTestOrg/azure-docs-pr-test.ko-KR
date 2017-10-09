---
title: "NSG aaaRead 로그 흐름 | Microsoft Docs"
description: "이 문서에서는 tooparse NSG 흐름 기록 하는 방법을 보여 줍니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a>NSG 흐름 로그 읽기

Tooread NSG 흐름 PowerShell로 항목을 기록 하는 방법에 대해 알아봅니다.

NSG 흐름 로그는 저장소 계정의 [블록 Blob](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs)에 저장됩니다. 블록 Blob는 더 작은 여러 블록으로 구성되어 있습니다. 각 로그는 1시간마다 생성되는 개별 블록 Blob입니다. 새 로그는 매 시간 마다 생성 되며, hello 로그 hello 최신 데이터로 몇 분 마다 새 항목으로 업데이트 됩니다. 이 문서에서는 hello의 tooread 일부 로그 흐름 하는 방법을 설명 합니다.

## <a name="scenario"></a>시나리오

시나리오를 따르는 hello는 저장소 계정에 저장 하는 예제 흐름 로그를 사용할 수 있습니다. म NSG 흐름 로그의 최신 이벤트 hello 선택적으로 읽을 수는 방법을 단계별로 설명 합니다. 그러나이 문서의 PowerShell 사용, hello hello 문서에서 설명한 제한 toohello 프로그래밍 언어에 한정 되지 않는 개념과 hello Azure 저장소 Api에서 지 원하는 해당 tooall 언어는

## <a name="setup"></a>설정

시작하기 전에 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다. 네트워크 보안을 사용 하도록 설정에 대 한 지침은 로그 흐름 toohello 다음 문서를 참조 하십시오: [네트워크 보안 그룹에 대 한 소개 tooflow 로깅을](network-watcher-nsg-flow-logging-overview.md)합니다.

## <a name="retrieve-hello-block-list"></a>Hello 차단 목록 검색

다음 PowerShell 집합 hello 변수를 필요한 tooquery hello NSG 흐름 로그 hello 내에서 blob 및 목록 hello 블록이 hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) 블록 blob입니다. Hello 스크립트 toocontain 사용자 환경에 대 한 유효한 값을 업데이트 합니다.

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

hello `$blockList` 변수 hello blob에 hello 블록의 목록을 반환 합니다. 각 블록 Blob에는 블록이 두 개 이상 포함되어 있습니다.  hello 첫 번째 블록의 길이는 `21` 바이트,이 블록 hello hello json 로그의 대괄호를 열고가 포함 되어 있습니다. hello 다른 hello 닫는 괄호 있으며 블록의 길이 `9` 바이트입니다.  볼 수 있듯이 hello 다음 예제에서는 로그에는 7 개 항목, 각각 개별 항목입니다. Hello 로그의 모든 새로운 항목 toohello 끝 hello 최종 블록 바로 앞에 추가 됩니다.

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a>Hello 블록 blob 읽기

Tooread hello 해야 `$blocklist` 변수 tooretrieve hello 데이터입니다. Hello 차단 목록에서 반복 하는 것이 예제에서는 각 블록에서 hello 바이트를 읽고 배열에 해당 스토리 합니다. 사용 하 여 hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) 메서드 tooretrieve hello 데이터입니다.

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

이제 hello `$valuearray` 배열 각 블록의 hello 문자열 값을 포함 합니다. tooverify hello 항목, get hello 두 번째 toohello 마지막 값을 실행 하 여 hello 배열에서 `$valuearray[$valuearray.Length-2]`합니다. Hello 마지막 값이 hello 닫는 괄호 바로 하는 것은 원치지 않습니다.

이 값의 hello 결과 hello 다음 예제에에서 나와 있습니다.

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

이 시나리오는 NSG의 tooread 항목 로그 tooparse hello 전체 로그 필요 없이 흐름이 하는 방법의 예입니다. Hello 블록 ID를 사용 하 여 또는 hello 블록 blob에 저장 된 블록의 hello 길이 추적 하 여 작성 된 대로 hello 로그에 새 항목을 읽을 수 있습니다. 이렇게 하면 tooread hello 새 항목만 있습니다.


## <a name="next-steps"></a>다음 단계

방문 [오픈 소스 도구를 사용 하 여 Azure 네트워크 감시자 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn 다른 방법으로 tooview NSG에 대 한 자세한 로그를 전달 합니다.

저장소 blob에 대 한 자세한 방문 toolearn: [함수 Azure Blob 저장소 바인딩](../azure-functions/functions-bindings-storage-blob.md)
