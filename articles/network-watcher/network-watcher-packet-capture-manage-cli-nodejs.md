---
title: "aaaManage 패킷 캡처를 Azure 네트워크 감시자-Azure CLI 1.0 | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello Azure CLI 1.0을 사용 하 여 네트워크 감시자의 패킷 캡처 기능을 설명 합니다."
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="130f1-103">Azure CLI 1.0에서 Azure Network Watcher를 사용하여 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="130f1-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="130f1-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="130f1-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="130f1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="130f1-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="130f1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="130f1-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="130f1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="130f1-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="130f1-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="130f1-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="130f1-109">네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="130f1-110">필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="130f1-111">패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="130f1-112">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="130f1-113">이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="130f1-114">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="130f1-115">이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="130f1-116">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="130f1-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="130f1-117">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="130f1-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="130f1-118">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="130f1-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="130f1-119">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="130f1-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="130f1-120">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="130f1-120">Before you begin</span></span>

<span data-ttu-id="130f1-121">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="130f1-122">인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="130f1-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="130f1-123">Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="130f1-124">패킷 캡처 hello 가상 컴퓨터에서 실행 하는 에이전트 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="130f1-125">hello 에이전트 확장으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="130f1-126">VM 확장에 대한 지침은 [Virtual Machine 확장 및 기능](../virtual-machines/windows/extensions-features.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="130f1-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="130f1-127">VM 확장 설치</span><span class="sxs-lookup"><span data-stu-id="130f1-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="130f1-128">1단계</span><span class="sxs-lookup"><span data-stu-id="130f1-128">Step 1</span></span>

<span data-ttu-id="130f1-129">Hello 실행 `azure vm extension set` hello 게스트 가상 컴퓨터에서 cmdlet tooinstall hello 패킷 캡처 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="130f1-130">Windows Virtual Machines의 경우:</span><span class="sxs-lookup"><span data-stu-id="130f1-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="130f1-131">Linux 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="130f1-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="130f1-132">2단계</span><span class="sxs-lookup"><span data-stu-id="130f1-132">Step 2</span></span>

<span data-ttu-id="130f1-133">에이전트 hello tooensure가 설치 되어 실행 hello `vm extension get` cmdlet hello 리소스 그룹 및 가상 컴퓨터 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="130f1-134">Hello 결과 목록 tooensure hello 에이전트가 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="130f1-135">hello 다음 샘플은 실행에서 hello 응답의 예`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="130f1-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="130f1-136">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="130f1-136">Start a packet capture</span></span>

<span data-ttu-id="130f1-137">Hello 앞의 단계 완료 되 면 hello 패킷 캡처 에이전트가 hello 가상 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="130f1-138">1단계</span><span class="sxs-lookup"><span data-stu-id="130f1-138">Step 1</span></span>

<span data-ttu-id="130f1-139">hello 다음 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="130f1-140">이 변수 toohello 전달 `network watcher show` 4 단계에서 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="130f1-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="130f1-141">2단계</span><span class="sxs-lookup"><span data-stu-id="130f1-141">Step 2</span></span>

<span data-ttu-id="130f1-142">저장소 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-142">Retrieve a storage account.</span></span> <span data-ttu-id="130f1-143">이 저장소 계정은 사용 되는 toostore hello 패킷 캡처 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="130f1-144">3단계</span><span class="sxs-lookup"><span data-stu-id="130f1-144">Step 3</span></span>

<span data-ttu-id="130f1-145">필터에 사용 되는 toolimit hello 저장 된 데이터를 hello 패킷 캡처 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="130f1-146">hello 다음 예제에서는 설정 패킷 캡처 여러 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="130f1-147">hello 처음 세 개의 필터 수집 나가는 TCP 트래픽을 로컬 IP 10.0.0.3 에서만에서 toodestination 포트 20, 80 및 443입니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="130f1-148">hello 있는 마지막 필터가 있는 UDP 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="130f1-149">패킷 캡처를 위해 여러 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="130f1-150">복잡 한 필터 구조를 사용 하는 경우 더 나은 toouse 필터로 json 파일 tooavoid 구문 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="130f1-151">예를 들어 hello 플래그를 사용 하 여 "-r" (대신 "-f") hello 다음 필터를 포함 하는 json 파일의 hello 위치를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="130f1-152">hello 다음 예제는 hello 예상 실행 한 출력의 hello `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="130f1-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="130f1-153">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="130f1-153">Get a packet capture</span></span>

<span data-ttu-id="130f1-154">Hello 실행 `network watcher packet-capture show` cmdlet은 현재 실행 중이거나 완료 된 패킷 캡처의 hello 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="130f1-155">hello 다음 예제는 hello hello 출력 `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="130f1-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="130f1-156">hello 다음 예제는 hello 캡처 완료 된 후.</span><span class="sxs-lookup"><span data-stu-id="130f1-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="130f1-157">TimeExceeded StopReason hello PacketCaptureStatus 값 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="130f1-158">이 값을 보여 줍니다 hello 패킷 캡처 성공적으로 실행 된 시간.</span><span class="sxs-lookup"><span data-stu-id="130f1-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="130f1-159">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="130f1-159">Stop a packet capture</span></span>

<span data-ttu-id="130f1-160">Hello를 실행 하 여 `network watcher packet-capture stop` 캡처 세션이 진행 중인 경우이 cmdlet을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="130f1-161">hello cmdlet 반환 응답이 없는 경우 현재 실행 중인 캡처 세션 또는 이미 중지 된 기존 세션에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="130f1-162">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="130f1-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="130f1-163">패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="130f1-164">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="130f1-164">Download a packet capture</span></span>

<span data-ttu-id="130f1-165">패킷 캡처 세션이 완료 되 면 hello 캡처 파일 업로드 tooblob tooa 또는 저장소에 로컬 파일 hello VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="130f1-166">hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="130f1-167">저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="130f1-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="130f1-168">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="130f1-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="130f1-169">Next steps</span></span>

<span data-ttu-id="130f1-170">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="130f1-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="130f1-171">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="130f1-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
