---
title: "aaaManage 패킷 캡처를 Azure 네트워크 감시자-Azure CLI 2.0 | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello Azure CLI 2.0을 사용 하 여 네트워크 감시자의 패킷 캡처 기능을 설명 합니다."
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="972fa-103">Azure CLI 2.0에서 Azure Network Watcher를 사용하여 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="972fa-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="972fa-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="972fa-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="972fa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="972fa-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="972fa-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="972fa-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="972fa-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="972fa-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="972fa-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="972fa-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="972fa-109">네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="972fa-110">필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="972fa-111">패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="972fa-112">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="972fa-113">이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="972fa-114">이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="972fa-115">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="972fa-116">이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="972fa-117">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="972fa-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="972fa-118">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="972fa-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="972fa-119">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="972fa-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="972fa-120">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="972fa-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="972fa-121">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="972fa-121">Before you begin</span></span>

<span data-ttu-id="972fa-122">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="972fa-123">인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="972fa-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="972fa-124">Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="972fa-125">패킷 캡처 hello 가상 컴퓨터에서 실행 하는 에이전트 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="972fa-126">hello 에이전트 확장으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="972fa-127">VM 확장에 대한 지침은 [Virtual Machine 확장 및 기능](../virtual-machines/windows/extensions-features.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="972fa-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="972fa-128">VM 확장 설치</span><span class="sxs-lookup"><span data-stu-id="972fa-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="972fa-129">1단계</span><span class="sxs-lookup"><span data-stu-id="972fa-129">Step 1</span></span>

<span data-ttu-id="972fa-130">Hello 실행 `az vm extension set` hello 게스트 가상 컴퓨터에서 cmdlet tooinstall hello 패킷 캡처 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="972fa-131">Windows Virtual Machines의 경우:</span><span class="sxs-lookup"><span data-stu-id="972fa-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="972fa-132">Linux 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="972fa-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="972fa-133">2단계</span><span class="sxs-lookup"><span data-stu-id="972fa-133">Step 2</span></span>

<span data-ttu-id="972fa-134">에이전트 hello tooensure가 설치 되어 실행 hello `vm extension get` cmdlet hello 리소스 그룹 및 가상 컴퓨터 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="972fa-135">Hello 결과 목록 tooensure hello 에이전트가 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="972fa-136">hello 다음 샘플은 실행에서 hello 응답의 예`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="972fa-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="972fa-137">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="972fa-137">Start a packet capture</span></span>

<span data-ttu-id="972fa-138">Hello 앞의 단계 완료 되 면 hello 패킷 캡처 에이전트가 hello 가상 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="972fa-139">1단계</span><span class="sxs-lookup"><span data-stu-id="972fa-139">Step 1</span></span>

<span data-ttu-id="972fa-140">hello 다음 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="972fa-141">네트워크 감시자 hello 구성 제품 이름을 toohello 전달 `az network watcher show` 4 단계에서 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="972fa-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="972fa-142">2단계</span><span class="sxs-lookup"><span data-stu-id="972fa-142">Step 2</span></span>

<span data-ttu-id="972fa-143">저장소 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-143">Retrieve a storage account.</span></span> <span data-ttu-id="972fa-144">이 저장소 계정은 사용 되는 toostore hello 패킷 캡처 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="972fa-145">3단계</span><span class="sxs-lookup"><span data-stu-id="972fa-145">Step 3</span></span>

<span data-ttu-id="972fa-146">필터에 사용 되는 toolimit hello 저장 된 데이터를 hello 패킷 캡처 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="972fa-147">hello 다음 예제에서는 설정 패킷 캡처 여러 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="972fa-148">hello 처음 세 개의 필터 수집 나가는 TCP 트래픽을 로컬 IP 10.0.0.3 에서만에서 toodestination 포트 20, 80 및 443입니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="972fa-149">hello 있는 마지막 필터가 있는 UDP 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="972fa-150">hello 다음 예제는 hello 예상 실행 한 출력의 hello `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="972fa-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="972fa-151">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="972fa-151">Get a packet capture</span></span>

<span data-ttu-id="972fa-152">Hello 실행 `az network watcher packet-capture show` cmdlet은 현재 실행 중이거나 완료 된 패킷 캡처의 hello 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="972fa-153">hello 다음 예제는 hello hello 출력 `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="972fa-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="972fa-154">hello 다음 예제는 hello 캡처 완료 된 후.</span><span class="sxs-lookup"><span data-stu-id="972fa-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="972fa-155">TimeExceeded StopReason hello PacketCaptureStatus 값 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="972fa-156">이 값을 보여 줍니다 hello 패킷 캡처 성공적으로 실행 된 시간.</span><span class="sxs-lookup"><span data-stu-id="972fa-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="972fa-157">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="972fa-157">Stop a packet capture</span></span>

<span data-ttu-id="972fa-158">Hello를 실행 하 여 `az network watcher packet-capture stop` 캡처 세션이 진행 중인 경우이 cmdlet을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="972fa-159">hello cmdlet 반환 응답이 없는 경우 현재 실행 중인 캡처 세션 또는 이미 중지 된 기존 세션에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="972fa-160">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="972fa-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="972fa-161">패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="972fa-162">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="972fa-162">Download a packet capture</span></span>

<span data-ttu-id="972fa-163">패킷 캡처 세션이 완료 되 면 hello 캡처 파일 업로드 tooblob tooa 또는 저장소에 로컬 파일 hello VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="972fa-164">hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="972fa-165">저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="972fa-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="972fa-166">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="972fa-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="972fa-167">Next steps</span></span>

<span data-ttu-id="972fa-168">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="972fa-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="972fa-169">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="972fa-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
