---
title: "aaaManage 패킷 캡처를 Azure 네트워크 감시자-PowerShell | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello 패킷 캡처 기능은 PowerShell을 사용 하 여 네트워크 감시자 설명"
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
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="4cfe3-103">PowerShell에서 Azure Network Watcher를 사용하여 패킷 캡처 관리</span><span class="sxs-lookup"><span data-stu-id="4cfe3-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4cfe3-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4cfe3-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="4cfe3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cfe3-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="4cfe3-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4cfe3-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="4cfe3-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4cfe3-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="4cfe3-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="4cfe3-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="4cfe3-109">네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="4cfe3-110">필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="4cfe3-111">패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="4cfe3-112">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="4cfe3-113">이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="4cfe3-114">이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="4cfe3-115">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="4cfe3-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="4cfe3-116">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="4cfe3-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="4cfe3-117">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="4cfe3-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="4cfe3-118">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="4cfe3-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="4cfe3-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4cfe3-119">Before you begin</span></span>

<span data-ttu-id="4cfe3-120">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="4cfe3-121">인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="4cfe3-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="4cfe3-122">Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cfe3-123">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="4cfe3-124">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="4cfe3-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="4cfe3-125">VM 확장 설치</span><span class="sxs-lookup"><span data-stu-id="4cfe3-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="4cfe3-126">1단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="4cfe3-127">2단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-127">Step 2</span></span>

<span data-ttu-id="4cfe3-128">hello 검색 hello 확장 정보는 다음 예제에서는 필요한 toorun hello `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="4cfe3-129">이 cmdlet은 hello 게스트 가상 컴퓨터에서 hello 패킷 캡처 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="4cfe3-130">hello `Set-AzureRmVMExtension` cmdlet에는 몇 분 toocomplete 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="4cfe3-131">Windows Virtual Machines의 경우:</span><span class="sxs-lookup"><span data-stu-id="4cfe3-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="4cfe3-132">Linux 가상 컴퓨터의 경우:</span><span class="sxs-lookup"><span data-stu-id="4cfe3-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="4cfe3-133">hello 다음 예제는 성공적인 응답 hello를 실행 한 후 `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="4cfe3-134">3단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-134">Step 3</span></span>

<span data-ttu-id="4cfe3-135">에이전트 hello tooensure가 설치 되어 실행 hello `Get-AzureRmVMExtension` cmdlet hello 가상 컴퓨터 이름 및 hello 확장 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="4cfe3-136">hello 다음 샘플은 실행에서 hello 응답의 예`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="4cfe3-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="4cfe3-137">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="4cfe3-137">Start a packet capture</span></span>

<span data-ttu-id="4cfe3-138">Hello 앞의 단계 완료 되 면 hello 패킷 캡처 에이전트가 hello 가상 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="4cfe3-139">1단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-139">Step 1</span></span>

<span data-ttu-id="4cfe3-140">hello 다음 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="4cfe3-141">이 변수 toohello 전달 `New-AzureRmNetworkWatcherPacketCapture` 4 단계에서 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="4cfe3-142">2단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-142">Step 2</span></span>

<span data-ttu-id="4cfe3-143">저장소 계정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-143">Retrieve a storage account.</span></span> <span data-ttu-id="4cfe3-144">이 저장소 계정은 사용 되는 toostore hello 패킷 캡처 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="4cfe3-145">3단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-145">Step 3</span></span>

<span data-ttu-id="4cfe3-146">필터에 사용 되는 toolimit hello 저장 된 데이터를 hello 패킷 캡처 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="4cfe3-147">hello 다음 예제에서는 두 개의 필터를</span><span class="sxs-lookup"><span data-stu-id="4cfe3-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="4cfe3-148">Toodestination 포트 20, 80 및 443 로컬 IP 10.0.0.3 에서만에서 트래픽을 나가는 TCP 필터가 두 개를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="4cfe3-149">두 번째 필터 hello UDP 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="4cfe3-150">패킷 캡처를 위해 여러 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="4cfe3-151">4단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-151">Step 4</span></span>

<span data-ttu-id="4cfe3-152">Hello 실행 `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello 패킷 캡처 프로세스와 hello 이전 단계에서에서 검색 된 hello 필요한 값을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="4cfe3-153">hello 다음 예제는 hello 예상 실행 한 출력의 hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="4cfe3-154">패킷 캡처 가져오기</span><span class="sxs-lookup"><span data-stu-id="4cfe3-154">Get a packet capture</span></span>

<span data-ttu-id="4cfe3-155">Hello 실행 `Get-AzureRmNetworkWatcherPacketCapture` cmdlet은 현재 실행 중이거나 완료 된 패킷 캡처의 hello 상태를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="4cfe3-156">hello 다음 예제는 hello hello 출력 `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="4cfe3-157">hello 다음 예제는 hello 캡처 완료 된 후.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="4cfe3-158">TimeExceeded StopReason hello PacketCaptureStatus 값 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="4cfe3-159">이 값을 보여 줍니다 hello 패킷 캡처 성공적으로 실행 된 시간.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="4cfe3-160">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="4cfe3-160">Stop a packet capture</span></span>

<span data-ttu-id="4cfe3-161">Hello를 실행 하 여 `Stop-AzureRmNetworkWatcherPacketCapture` 캡처 세션이 진행 중인 경우이 cmdlet을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="4cfe3-162">hello cmdlet 반환 응답이 없는 경우 현재 실행 중인 캡처 세션 또는 이미 중지 된 기존 세션에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="4cfe3-163">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="4cfe3-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="4cfe3-164">패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="4cfe3-165">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="4cfe3-165">Download a packet capture</span></span>

<span data-ttu-id="4cfe3-166">패킷 캡처 세션이 완료 되 면 hello 캡처 파일 업로드 tooblob tooa 또는 저장소에 로컬 파일 hello VM 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="4cfe3-167">hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="4cfe3-168">저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="4cfe3-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="4cfe3-169">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="4cfe3-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4cfe3-170">Next steps</span></span>

<span data-ttu-id="4cfe3-171">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="4cfe3-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="4cfe3-172">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4cfe3-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














