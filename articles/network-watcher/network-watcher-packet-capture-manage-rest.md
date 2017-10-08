---
title: "aaaManage 패킷 캡처 Azure 네트워크 감시자-REST API를 | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello Azure REST API를 사용 하 여 네트워크 감시자의 패킷 캡처 기능을 설명 합니다."
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="94f40-103">Azure REST API를 사용하여 Azure Network Watcher로 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="94f40-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="94f40-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="94f40-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="94f40-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94f40-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="94f40-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="94f40-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="94f40-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94f40-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="94f40-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="94f40-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="94f40-109">네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="94f40-110">필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="94f40-111">패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="94f40-112">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="94f40-113">이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="94f40-114">이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="94f40-115">**패킷 캡처 가져오기**</span><span class="sxs-lookup"><span data-stu-id="94f40-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="94f40-116">**모든 패킷 캡처 나열**</span><span class="sxs-lookup"><span data-stu-id="94f40-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="94f40-117">**패킷 캡처 hello 상태 쿼리**</span><span class="sxs-lookup"><span data-stu-id="94f40-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="94f40-118">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="94f40-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="94f40-119">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="94f40-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="94f40-120">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="94f40-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="94f40-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="94f40-121">Before you begin</span></span>

<span data-ttu-id="94f40-122">이 시나리오에서는 IP 확인 흐름 hello 네트워크 감시자 Rest API toorun을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="94f40-123">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="94f40-124">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="94f40-125">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="94f40-126">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="94f40-127">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="94f40-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="94f40-128">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="94f40-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="94f40-129">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="94f40-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="94f40-130">다음 스크립트 tooreturn hello 가상 컴퓨터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="94f40-131">패킷 캡처를 시작하기 위해 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="94f40-132">hello 다음 코드에 필요한 변수:</span><span class="sxs-lookup"><span data-stu-id="94f40-132">hello following code needs variables:</span></span>

- <span data-ttu-id="94f40-133">**subscriptionId** -hello로도 hello 구독 id를 검색할 수 **Get AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="94f40-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="94f40-134">**resourceGroupName** -hello 가상 컴퓨터를 포함 하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="94f40-135">Hello 다음과 같은 출력에서 hello 가상 컴퓨터의 hello id hello 다음 예제에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="94f40-136">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="94f40-136">Get a packet capture</span></span>

<span data-ttu-id="94f40-137">hello 다음 예제에서는 hello의 상태를 가져옵니다 단일 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="94f40-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="94f40-138">hello 다음 응답은 일반적으로 패킷 캡처의 hello 상태를 쿼리할 때 반환 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="94f40-139">모든 패킷 캡처 나열</span><span class="sxs-lookup"><span data-stu-id="94f40-139">List all packet captures</span></span>

<span data-ttu-id="94f40-140">다음 예제는 hello 영역의 모든 패킷 캡처 세션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="94f40-141">hello 다음 응답은 일반적으로 모든 패킷을 가져올 때 반환 된 응답의 예가 캡처</span><span class="sxs-lookup"><span data-stu-id="94f40-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="94f40-142">패킷 캡처 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="94f40-142">Query packet capture status</span></span>

<span data-ttu-id="94f40-143">다음 예제는 hello 영역의 모든 패킷 캡처 세션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="94f40-144">hello 다음 응답은 일반적으로 패킷 캡처의 hello 상태를 쿼리할 때 반환 된 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="94f40-145">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="94f40-145">Start packet capture</span></span>

<span data-ttu-id="94f40-146">다음 예제는 hello 가상 컴퓨터에서 패킷 캡처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="94f40-147">hello 예는 예제를 만들 유연성에 대 한 매개 변수가 있는 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="94f40-148">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="94f40-148">Stop packet capture</span></span>

<span data-ttu-id="94f40-149">다음 예제는 hello 가상 컴퓨터에서 패킷 캡처를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="94f40-150">hello 예는 예제를 만들 유연성에 대 한 매개 변수가 있는 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="94f40-151">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="94f40-151">Delete packet capture</span></span>

<span data-ttu-id="94f40-152">다음 예에서는 hello 가상 컴퓨터에서 패킷 캡처를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="94f40-153">hello 예는 예제를 만들 유연성에 대 한 매개 변수가 있는 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="94f40-154">패킷 캡처를 삭제 해도 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="94f40-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94f40-155">Next steps</span></span>

<span data-ttu-id="94f40-156">Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="94f40-157">사용할 수 있는 다른 도구는 저장소 탐색기입니다.</span><span class="sxs-lookup"><span data-stu-id="94f40-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="94f40-158">저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="94f40-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="94f40-159">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="94f40-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













