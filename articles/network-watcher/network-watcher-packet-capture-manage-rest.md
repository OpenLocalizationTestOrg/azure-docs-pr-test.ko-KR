---
title: "Azure Network Watcher를 사용하여 패킷 캡처 관리 - REST API | Microsoft Docs"
description: "이 페이지에서는 Azure REST API를 사용하여 Network Watcher의 패킷 캡처 기능을 관리하는 방법에 대해 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="582ea-103">Azure REST API를 사용하여 Azure Network Watcher로 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="582ea-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="582ea-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="582ea-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="582ea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="582ea-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="582ea-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="582ea-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="582ea-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="582ea-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="582ea-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="582ea-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="582ea-109">Network Watcher 패킷 캡처를 사용하면 가상 컴퓨터 간에 트래픽을 추적하는 캡처 세션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="582ea-110">원하는 트래픽만 캡처할 수 있도록 캡처 세션에 대 한 필터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="582ea-111">패킷 캡처를 통해 사후 및 사전 대응적으로 네트워크 예외를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="582ea-112">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="582ea-113">이 기능은 원격으로 패킷 캡처를 트리거할 수 있게 하여 원하는 컴퓨터에서 수동으로 패킷 캡처를 실행하는 부담을 줄이고 시간을 단축합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="582ea-114">이 문서에서는 패킷 캡처를 위해 현재 사용할 수 있는 여러 관리 태스크를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="582ea-115">**패킷 캡처 가져오기**</span><span class="sxs-lookup"><span data-stu-id="582ea-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="582ea-116">**모든 패킷 캡처 나열**</span><span class="sxs-lookup"><span data-stu-id="582ea-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="582ea-117">**패킷 캡처의 상태 쿼리**</span><span class="sxs-lookup"><span data-stu-id="582ea-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="582ea-118">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="582ea-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="582ea-119">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="582ea-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="582ea-120">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="582ea-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="582ea-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="582ea-121">Before you begin</span></span>

<span data-ttu-id="582ea-122">이 시나리오에서는 Network Watcher Rest API를 호출하여 IP 흐름 확인을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="582ea-123">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="582ea-124">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="582ea-125">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="582ea-126">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="582ea-127">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="582ea-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="582ea-128">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="582ea-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="582ea-129">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="582ea-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="582ea-130">다음 스크립트를 실행하여 가상 컴퓨터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="582ea-131">패킷 캡처를 시작하기 위해 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="582ea-132">다음 코드에는 다음 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-132">The following code needs variables:</span></span>

- <span data-ttu-id="582ea-133">**subscriptionId** - **Get-AzureRMSubscription** cmdlet으로 구독 ID도 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="582ea-134">**resourceGroupName** - 가상 컴퓨터를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="582ea-135">다음 출력에서는 다음 예제에 가상 컴퓨터의 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="582ea-136">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="582ea-136">Get a packet capture</span></span>

<span data-ttu-id="582ea-137">다음 예제에서는 단일 패킷 캡처의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="582ea-138">다음 응답은 패킷 캡처의 상태를 쿼리할 때 반환된 일반적인 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="582ea-139">모든 패킷 캡처 나열</span><span class="sxs-lookup"><span data-stu-id="582ea-139">List all packet captures</span></span>

<span data-ttu-id="582ea-140">다음 예제에서는 지역의 모든 패킷 캡처 세션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="582ea-141">다음 응답은 모든 패킷 캡처를 가져올 때 반환된 일반적인 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="582ea-142">패킷 캡처 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="582ea-142">Query packet capture status</span></span>

<span data-ttu-id="582ea-143">다음 예제에서는 지역의 모든 패킷 캡처 세션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="582ea-144">다음 응답은 패킷 캡처의 상태를 쿼리할 때 반환된 일반적인 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="582ea-145">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="582ea-145">Start packet capture</span></span>

<span data-ttu-id="582ea-146">다음 예제에서는 가상 컴퓨터에서 패킷 캡처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="582ea-147">이 예제는 예제를 만드는 데 유연성을 허용하도록 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="582ea-148">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="582ea-148">Stop packet capture</span></span>

<span data-ttu-id="582ea-149">다음 예제에서는 가상 컴퓨터에서 패킷 캡처를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="582ea-150">이 예제는 예제를 만드는 데 유연성을 허용하도록 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="582ea-151">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="582ea-151">Delete packet capture</span></span>

<span data-ttu-id="582ea-152">다음 예제에서는 가상 컴퓨터에서 패킷 캡처를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="582ea-153">이 예제는 예제를 만드는 데 유연성을 허용하도록 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="582ea-154">패킷 캡처를 삭제해도 저장소 계정에서 파일을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="582ea-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="582ea-155">Next steps</span></span>

<span data-ttu-id="582ea-156">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="582ea-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="582ea-157">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="582ea-158">저장소 탐색기에 대한 자세한 내용은 여기에 있는 [저장소 탐색기](http://storageexplorer.com/) 링크에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="582ea-159">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="582ea-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













