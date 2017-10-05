---
title: "Azure Network Watcher를 사용하여 패킷 캡처 관리 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 PowerShell을 사용하여 Network Watcher의 패킷 캡처 기능을 관리하는 방법에 대해 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="1c67c-103">PowerShell에서 Azure Network Watcher를 사용하여 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="1c67c-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1c67c-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1c67c-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="1c67c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c67c-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="1c67c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c67c-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="1c67c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c67c-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="1c67c-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="1c67c-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="1c67c-109">Network Watcher 패킷 캡처를 사용하면 가상 컴퓨터 간에 트래픽을 추적하는 캡처 세션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="1c67c-110">원하는 트래픽만 캡처할 수 있도록 캡처 세션에 대 한 필터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="1c67c-111">패킷 캡처를 통해 사후 및 사전 대응적으로 네트워크 예외를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="1c67c-112">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="1c67c-113">이 기능은 원격으로 패킷 캡처를 트리거할 수 있게 하여 원하는 컴퓨터에서 수동으로 패킷 캡처를 실행하는 부담을 줄이고 시간을 단축합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="1c67c-114">이 문서에서는 패킷 캡처를 위해 현재 사용할 수 있는 여러 관리 태스크를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="1c67c-115">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="1c67c-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="1c67c-116">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="1c67c-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="1c67c-117">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="1c67c-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="1c67c-118">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="1c67c-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="1c67c-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1c67c-119">Before you begin</span></span>

<span data-ttu-id="1c67c-120">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="1c67c-121">패킷 캡처를 만들려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="1c67c-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="1c67c-122">패킷 캡처 확장을 사용하는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1c67c-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c67c-123">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1c67c-124">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1c67c-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="1c67c-125">VM 확장 설치</span><span class="sxs-lookup"><span data-stu-id="1c67c-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="1c67c-126">1단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="1c67c-127">2단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-127">Step 2</span></span>

<span data-ttu-id="1c67c-128">다음 예에서는 `Set-AzureRmVMExtension` cmdlet을 실행하는 데 필요한 확장 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="1c67c-129">이 cmdlet을 사용하면 게스트 가상 컴퓨터에 패킷 캡처 에이전트가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="1c67c-130">`Set-AzureRmVMExtension` cmdlet을 완료하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="1c67c-131">Windows 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="1c67c-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="1c67c-132">Linux 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="1c67c-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="1c67c-133">다음 예제는 `Set-AzureRmVMExtension` cmdlet을 실행한 후 성공적인 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="1c67c-134">3단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-134">Step 3</span></span>

<span data-ttu-id="1c67c-135">에이전트가 설치되어 있는지 확인하려면 `Get-AzureRmVMExtension` cmdlet을 실행하고 가상 컴퓨터 이름과 확장 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="1c67c-136">다음 샘플은 실행 중인 `Get-AzureRmVMExtension`에서 응답의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="1c67c-137">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="1c67c-137">Start a packet capture</span></span>

<span data-ttu-id="1c67c-138">이전 단계가 완료되면 패킷 캡처 에이전트는 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="1c67c-139">1단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-139">Step 1</span></span>

<span data-ttu-id="1c67c-140">다음 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="1c67c-141">이 변수는 4단계에서 `New-AzureRmNetworkWatcherPacketCapture` cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="1c67c-142">2단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-142">Step 2</span></span>

<span data-ttu-id="1c67c-143">저장소 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-143">Retrieve a storage account.</span></span> <span data-ttu-id="1c67c-144">이 저장소 계정은 패킷 캡처 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="1c67c-145">3단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-145">Step 3</span></span>

<span data-ttu-id="1c67c-146">패킷 캡처에 의해 저장되는 데이터를 제한하는 데 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="1c67c-147">다음 예제에서는 두 필터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-147">The following example sets up two filters.</span></span>  <span data-ttu-id="1c67c-148">한 필터는 로컬 IP 10.0.0.3에서 대상 포트 20, 80 및 443으로 나가는 TCP 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="1c67c-149">두 번째 필터는 UDP 트래픽만을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="1c67c-150">패킷 캡처를 위해 여러 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="1c67c-151">4단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-151">Step 4</span></span>

<span data-ttu-id="1c67c-152">`New-AzureRmNetworkWatcherPacketCapture` cmdlet을 실행하여 패킷 캡처 프로세스를 시작하고 이전 단계에서 검색한 필수 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="1c67c-153">다음 예제는 `New-AzureRmNetworkWatcherPacketCapture` cmdlet 실행 시 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="1c67c-154">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="1c67c-154">Get a packet capture</span></span>

<span data-ttu-id="1c67c-155">`Get-AzureRmNetworkWatcherPacketCapture` cmdlet을 실행하고 현재 실행 중이거나 완료된 패킷 캡처의 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="1c67c-156">다음 예제는 `Get-AzureRmNetworkWatcherPacketCapture` cmdlet의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="1c67c-157">다음 예제는 캡처를 완료한 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="1c67c-158">PacketCaptureStatus 값은 TimeExceeded의 StopReason과 함께 중지됨입니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="1c67c-159">이 값은 패킷 캡처가 성공했으며 해당 시간을 실행했음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-159">This value shows that the packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="1c67c-160">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="1c67c-160">Stop a packet capture</span></span>

<span data-ttu-id="1c67c-161">`Stop-AzureRmNetworkWatcherPacketCapture` cmdlet을 실행하여 캡처 세션이 진행 중인 경우 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="1c67c-162">cmdlet은 현재 실행 중인 캡처 세션 또는 이미 중지된 기존 세션에서 실행되는 경우 응답을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="1c67c-163">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="1c67c-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="1c67c-164">패킷 캡처를 삭제하면 저장소 계정에서 파일을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="1c67c-165">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="1c67c-165">Download a packet capture</span></span>

<span data-ttu-id="1c67c-166">패킷 캡처 세션이 완료되면 캡처 파일을 Blob Storage 또는 VM의 로컬 파일에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="1c67c-167">패킷 캡처의 저장 위치는 세션 생성 시 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="1c67c-168">저장소 계정에 저장되는 이러한 캡처 파일에 액세스하는 편리한 도구는 Microsoft Azure Storage 탐색기이며 http://storageexplorer.com/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="1c67c-169">저장소 계정이 지정되어 있으면 패킷 캡처 파일은 다음 위치에서 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="1c67c-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c67c-170">Next steps</span></span>

<span data-ttu-id="1c67c-171">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="1c67c-172">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c67c-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














