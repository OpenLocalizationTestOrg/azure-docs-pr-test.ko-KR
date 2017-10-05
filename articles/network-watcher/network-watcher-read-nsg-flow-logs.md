---
title: "NSG 흐름 로그 읽기 | Microsoft 문서"
description: "이 문서에서는 NSG 흐름 로그를 구문 분석하는 방법을 설명합니다."
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
ms.openlocfilehash: 9bb48157b2b8e483e063058f761c3a8f531927f9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="a43ee-103">NSG 흐름 로그 읽기</span><span class="sxs-lookup"><span data-stu-id="a43ee-103">Read NSG flow logs</span></span>

<span data-ttu-id="a43ee-104">PowerShell을 사용하여 NSG 흐름 로그 항목을 읽는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-104">Learn how to read NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="a43ee-105">NSG 흐름 로그는 저장소 계정의 [블록 Blob](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="a43ee-106">블록 Blob는 더 작은 여러 블록으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="a43ee-107">각 로그는 1시간마다 생성되는 개별 블록 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="a43ee-108">1시간마다 새 로그가 생성되며 몇 분마다 로그가 새 항목으로 업데이트되어 최신 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-108">New logs are generated every hour, the logs are updated with new entries every few minutes with the latest data.</span></span> <span data-ttu-id="a43ee-109">이 문서에서는 흐름 로그의 각 부분을 읽는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-109">In this article you learn how to read portions of the flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="a43ee-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="a43ee-110">Scenario</span></span>

<span data-ttu-id="a43ee-111">다음 시나리오에서는 저장소 계정에 저장된 예제 흐름 로그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-111">In the following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="a43ee-112">NSG 흐름 로그에서 최신 이벤트를 선택적으로 읽을 수 있는 방법을 단계적으로 확인할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-112">we step through how you can selectively read the latest events in NSG flow logs.</span></span> <span data-ttu-id="a43ee-113">이 문서에서는 PowerShell을 사용하지만 여기서 설명하는 개념은 프로그래밍 언어에만 국한되지 않으며, Azure Storage API가 지원하는 모든 언어에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-113">In this article we will use PowerShell, however, the concepts discussed in the article are not limited to the programming language and are applicable to all languages supported by the Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="a43ee-114">설정</span><span class="sxs-lookup"><span data-stu-id="a43ee-114">Setup</span></span>

<span data-ttu-id="a43ee-115">시작하기 전에 계정에 있는 하나 이상의 네트워크 보안 그룹에서 네트워크 보안 그룹 흐름 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="a43ee-116">네트워크 보안 흐름 로그를 사용하도록 설정하는 방법에 대한 지침은 [네트워크 보안 그룹에 대한 흐름 로깅 소개](network-watcher-nsg-flow-logging-overview.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a43ee-116">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-the-block-list"></a><span data-ttu-id="a43ee-117">블록 목록 검색</span><span class="sxs-lookup"><span data-stu-id="a43ee-117">Retrieve the block list</span></span>

<span data-ttu-id="a43ee-118">다음 PowerShell은 NSG 흐름 로그 Blob를 쿼리하는 데 필요한 변수를 설정하고 [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) 블록 Blob 내의 블록을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-118">The following PowerShell sets up the variables needed to query the NSG flow log blob and list the blocks within the [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="a43ee-119">실제 환경에서 사용되는 값을 포함하여 스크립트를 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="a43ee-119">Update the script to contain valid values for your environment.</span></span>

```powershell
# The SubscriptionID to use
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains the Network Security Group
$resourceGroupName = "<resourceGroupName>"

# The name of the Network Security Group
$nsgName = "NSGName"

# The storage account name that contains the NSG logs
$storageAccountName = "<storageAccountName>" 

# The date and time for the log to be queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve the primary storage account key to access the NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context to be used to query the logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of the blob that contains the NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets the storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets the block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from the storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores the block list in a variable from the block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="a43ee-120">`$blockList` 변수는 Blob의 블록 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-120">The `$blockList` variable returns a list of the blocks in the blob.</span></span> <span data-ttu-id="a43ee-121">각 블록 Blob에는 블록이 두 개 이상 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="a43ee-122">첫 번째 블록은 길이가 `21`바이트이며 json 로그의 여는 괄호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-122">The first block has a length of `21` bytes, this block contains the opening brackets of the json log.</span></span> <span data-ttu-id="a43ee-123">나머지 블록은 닫는 괄호이며 길이가 `9`바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-123">The other block is the closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="a43ee-124">보시다시피 다음 예제 로그에는 개별 항목 7개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-124">As you can see the following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="a43ee-125">로그의 모든 새 항목은 최종 블록 앞의 오른쪽 끝에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-125">All new entries in the log are added to the end right before the final block.</span></span>

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

## <a name="read-the-block-blob"></a><span data-ttu-id="a43ee-126">블록 Blob 읽기</span><span class="sxs-lookup"><span data-stu-id="a43ee-126">Read the block blob</span></span>

<span data-ttu-id="a43ee-127">다음으로는 `$blocklist` 변수를 읽어 데이터를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-127">Next we need to read the `$blocklist` variable to retrieve the data.</span></span> <span data-ttu-id="a43ee-128">이 예제에서는 블록 목록을 반복 검색하면서 각 블록의 바이트를 읽어 배열에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-128">In this example we iterate through the blocklist, read the bytes from each block and story them in an array.</span></span> <span data-ttu-id="a43ee-129">이때 [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) 메서드를 사용하여 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-129">We use the [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method to retrieve the data.</span></span>

```powershell
# Set the size of the byte array to the largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array to store values in
$valuearray = @()

# Define the starting index to track the current block being read
$index = 0

# Loop through each block in the block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object to story the bytes from the block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download the data into the ByteArray, starting with the current index, for the number of bytes in the current block. Index is increased by 3 when reading to remove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment the index by adding the current block length to the previous index
$index = $index + $blockList[$i].Length

# Retrieve the string from the byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add the log entry to the value array
$valuearray += $value
}
```

<span data-ttu-id="a43ee-130">현재 `$valuearray` 배열에는 각 블록의 문자열 값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-130">Now the `$valuearray` array contains the string value of each block.</span></span> <span data-ttu-id="a43ee-131">항목을 확인하려면 `$valuearray[$valuearray.Length-2]`를 실행하여 배열의 마지막에서 두 번째 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-131">To verify the entry, get the second to the last value from the array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="a43ee-132">마지막 값은 닫는 괄호이므로 가져올 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-132">We do not want the last value is just the closing bracket.</span></span>

<span data-ttu-id="a43ee-133">이 값의 결과가 다음 예제에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-133">The results of this value are shown in the following example:</span></span>

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

<span data-ttu-id="a43ee-134">이 시나리오는 전체 로그를 구문 분석할 필요 없이 NSG 흐름 로그의 항목을 읽는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-134">This scenario is an example of how to read entries in NSG flow logs without having to parse the entire log.</span></span> <span data-ttu-id="a43ee-135">블록 Blob에 저장된 블록의 길이를 추적하거나 블록 ID를 사용하면 로그에 작성되는 새 항목을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-135">You can read new entries in the log as they are written by using the block ID or by tracking the length of blocks stored in the block blob.</span></span> <span data-ttu-id="a43ee-136">이 방법을 사용하면 새 항목만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a43ee-136">This allows you to read only the new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a43ee-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a43ee-137">Next steps</span></span>

<span data-ttu-id="a43ee-138">[오픈 소스 도구를 사용하여 Azure Network Watcher NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)를 방문해 NSG 흐름 로그를 확인하는 다른 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a43ee-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) to learn more about other ways to view NSG flow logs.</span></span>

<span data-ttu-id="a43ee-139">저장소 Blob에 대해 자세히 알아보려면 [Azure Functions Blob Storage 바인딩](../azure-functions/functions-bindings-storage-blob.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="a43ee-139">To learn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>