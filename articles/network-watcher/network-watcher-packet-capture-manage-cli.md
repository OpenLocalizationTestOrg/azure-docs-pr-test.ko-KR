---
title: "Azure Network Watcher를 사용하여 패킷 캡처 관리 - Azure CLI 2.0 | Microsoft Docs"
description: "이 페이지에서는 Azure CLI 2.0을 사용하여 Network Watcher의 패킷 캡처 기능을 관리하는 방법에 대해 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="6b496-103">Azure CLI 2.0에서 Azure Network Watcher를 사용하여 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="6b496-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6b496-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="6b496-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="6b496-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b496-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="6b496-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6b496-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="6b496-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6b496-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="6b496-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="6b496-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="6b496-109">Network Watcher 패킷 캡처를 사용하면 가상 컴퓨터 간에 트래픽을 추적하는 캡처 세션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="6b496-110">원하는 트래픽만 캡처할 수 있도록 캡처 세션에 대 한 필터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="6b496-111">패킷 캡처를 통해 사후 및 사전 대응적으로 네트워크 예외를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="6b496-112">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="6b496-113">이 기능은 원격으로 패킷 캡처를 트리거할 수 있게 하여 원하는 컴퓨터에서 수동으로 패킷 캡처를 실행하는 부담을 줄이고 시간을 단축합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="6b496-114">이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="6b496-115">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="6b496-116">이 문서에서는 패킷 캡처를 위해 현재 사용할 수 있는 여러 관리 태스크를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="6b496-117">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="6b496-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="6b496-118">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="6b496-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="6b496-119">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="6b496-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="6b496-120">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="6b496-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="6b496-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6b496-121">Before you begin</span></span>

<span data-ttu-id="6b496-122">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="6b496-123">패킷 캡처를 만들려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="6b496-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="6b496-124">패킷 캡처 확장을 사용하는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="6b496-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b496-125">패킷 캡처에는 가상 컴퓨터에서 실행되는 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="6b496-126">에이전트는 확장으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="6b496-127">VM 확장에 대한 지침은 [Virtual Machine 확장 및 기능](../virtual-machines/windows/extensions-features.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b496-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="6b496-128">VM 확장 설치</span><span class="sxs-lookup"><span data-stu-id="6b496-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-129">1단계</span><span class="sxs-lookup"><span data-stu-id="6b496-129">Step 1</span></span>

<span data-ttu-id="6b496-130">`az vm extension set` cmdlet을 실행하여 게스트 가상 컴퓨터에 패킷 캡처 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="6b496-131">Windows Virtual Machines의 경우:</span><span class="sxs-lookup"><span data-stu-id="6b496-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="6b496-132">Linux 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="6b496-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="6b496-133">2단계:</span><span class="sxs-lookup"><span data-stu-id="6b496-133">Step 2</span></span>

<span data-ttu-id="6b496-134">에이전트가 설치되어 있는지 확인하려면 `vm extension get` cmdlet을 실행하고 리소스 그룹과 가상 컴퓨터 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="6b496-135">결과 목록을 확인하여 에이전트가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="6b496-136">다음 샘플은 실행 중인 `az vm extension show`에서 응답의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-136">The following sample is an example of the response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="6b496-137">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="6b496-137">Start a packet capture</span></span>

<span data-ttu-id="6b496-138">이전 단계가 완료되면 패킷 캡처 에이전트는 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-139">1단계</span><span class="sxs-lookup"><span data-stu-id="6b496-139">Step 1</span></span>

<span data-ttu-id="6b496-140">다음 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="6b496-141">Network Watcher의 이름이 4단계의 `az network watcher show` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="6b496-142">2단계</span><span class="sxs-lookup"><span data-stu-id="6b496-142">Step 2</span></span>

<span data-ttu-id="6b496-143">저장소 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-143">Retrieve a storage account.</span></span> <span data-ttu-id="6b496-144">이 저장소 계정은 패킷 캡처 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="6b496-145">3단계</span><span class="sxs-lookup"><span data-stu-id="6b496-145">Step 3</span></span>

<span data-ttu-id="6b496-146">패킷 캡처에 의해 저장되는 데이터를 제한하는 데 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="6b496-147">다음 예제에서는 몇 가지 필터를 사용하여 패킷 캡처를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="6b496-148">처음 세 개의 필터는 로컬 IP 10.0.0.3에서 대상 포트 20, 80 및 443으로 나가는 TCP 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="6b496-149">마지막 필터는 UDP 트래픽만을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="6b496-150">다음 예제는 `az network watcher packet-capture create` cmdlet 실행 시 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="6b496-151">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b496-151">Get a packet capture</span></span>

<span data-ttu-id="6b496-152">`az network watcher packet-capture show` cmdlet을 실행하고 현재 실행 중이거나 완료된 패킷 캡처의 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="6b496-153">다음 예제는 `az network watcher packet-capture show` cmdlet의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="6b496-154">다음 예제는 캡처를 완료한 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="6b496-155">PacketCaptureStatus 값은 TimeExceeded의 StopReason과 함께 중지됨입니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="6b496-156">이 값은 패킷 캡처가 성공했으며 해당 시간을 실행했음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-156">This value shows that the packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="6b496-157">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="6b496-157">Stop a packet capture</span></span>

<span data-ttu-id="6b496-158">`az network watcher packet-capture stop` cmdlet을 실행하여 캡처 세션이 진행 중인 경우 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="6b496-159">cmdlet은 현재 실행 중인 캡처 세션 또는 이미 중지된 기존 세션에서 실행되는 경우 응답을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="6b496-160">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="6b496-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="6b496-161">패킷 캡처를 삭제하면 저장소 계정에서 파일을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="6b496-162">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="6b496-162">Download a packet capture</span></span>

<span data-ttu-id="6b496-163">패킷 캡처 세션이 완료되면 캡처 파일을 Blob Storage 또는 VM의 로컬 파일에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="6b496-164">패킷 캡처의 저장 위치는 세션 생성 시 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="6b496-165">저장소 계정에 저장되는 이러한 캡처 파일에 액세스하는 편리한 도구는 Microsoft Azure Storage 탐색기이며 http://storageexplorer.com/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="6b496-166">저장소 계정이 지정되어 있으면 패킷 캡처 파일은 다음 위치에서 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="6b496-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b496-167">Next steps</span></span>

<span data-ttu-id="6b496-168">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="6b496-169">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b496-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
