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
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a>PowerShell에서 Azure Network Watcher를 사용하여 패킷 캡처 관리

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다. 필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다. 패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다. 통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다. 이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.

이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.

- [**패킷 캡처 시작**](#start-a-packet-capture)
- [**패킷 캡처 중지**](#stop-a-packet-capture)
- [**패킷 캡처 삭제**](#delete-a-packet-capture)
- [**패킷 캡처 다운로드**](#download-a-packet-capture)

## <a name="before-you-begin"></a>시작하기 전에

이 문서에서는 다음 리소스는 hello 있는 가정 합니다.

* 인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처

* Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.

> [!IMPORTANT]
> 패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다. Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).

## <a name="install-vm-extension"></a>VM 확장 설치

### <a name="step-1"></a>1단계

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a>2단계

hello 검색 hello 확장 정보는 다음 예제에서는 필요한 toorun hello `Set-AzureRmVMExtension` cmdlet. 이 cmdlet은 hello 게스트 가상 컴퓨터에서 hello 패킷 캡처 에이전트를 설치 합니다.

> [!NOTE]
> hello `Set-AzureRmVMExtension` cmdlet에는 몇 분 toocomplete 걸릴 수 있습니다.

Windows Virtual Machines의 경우:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

Linux 가상 컴퓨터의 경우:

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

hello 다음 예제는 성공적인 응답 hello를 실행 한 후 `Set-AzureRmVMExtension` cmdlet.

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a>3단계

에이전트 hello tooensure가 설치 되어 실행 hello `Get-AzureRmVMExtension` cmdlet hello 가상 컴퓨터 이름 및 hello 확장 이름을 전달 합니다.

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

hello 다음 샘플은 실행에서 hello 응답의 예`Get-AzureRmVMExtension`

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

## <a name="start-a-packet-capture"></a>패킷 캡처 시작

Hello 앞의 단계 완료 되 면 hello 패킷 캡처 에이전트가 hello 가상 컴퓨터에 설치 됩니다.

### <a name="step-1"></a>1단계

hello 다음 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다. 이 변수 toohello 전달 `New-AzureRmNetworkWatcherPacketCapture` 4 단계에서 cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a>2단계

저장소 계정을 검색합니다. 이 저장소 계정은 사용 되는 toostore hello 패킷 캡처 파일입니다.

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a>3단계

필터에 사용 되는 toolimit hello 저장 된 데이터를 hello 패킷 캡처 수 있습니다. hello 다음 예제에서는 두 개의 필터를  Toodestination 포트 20, 80 및 443 로컬 IP 10.0.0.3 에서만에서 트래픽을 나가는 TCP 필터가 두 개를 수집 합니다.  두 번째 필터 hello UDP 트래픽을 수집합니다.

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> 패킷 캡처를 위해 여러 필터를 정의할 수 있습니다.

### <a name="step-4"></a>4단계

Hello 실행 `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello 패킷 캡처 프로세스와 hello 이전 단계에서에서 검색 된 hello 필요한 값을 전달 합니다.
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

hello 다음 예제는 hello 예상 실행 한 출력의 hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.

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

## <a name="get-a-packet-capture"></a>패킷 캡처 가져오기

Hello 실행 `Get-AzureRmNetworkWatcherPacketCapture` cmdlet은 현재 실행 중이거나 완료 된 패킷 캡처의 hello 상태를 검색 합니다.

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

hello 다음 예제는 hello hello 출력 `Get-AzureRmNetworkWatcherPacketCapture` cmdlet. hello 다음 예제는 hello 캡처 완료 된 후. TimeExceeded StopReason hello PacketCaptureStatus 값 중지 됩니다. 이 값을 보여 줍니다 hello 패킷 캡처 성공적으로 실행 된 시간.
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

## <a name="stop-a-packet-capture"></a>패킷 캡처 중지

Hello를 실행 하 여 `Stop-AzureRmNetworkWatcherPacketCapture` 캡처 세션이 진행 중인 경우이 cmdlet을 중지 합니다.

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> hello cmdlet 반환 응답이 없는 경우 현재 실행 중인 캡처 세션 또는 이미 중지 된 기존 세션에서 실행 합니다.

## <a name="delete-a-packet-capture"></a>패킷 캡처 삭제

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> 패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.

## <a name="download-a-packet-capture"></a>패킷 캡처 다운로드

패킷 캡처 세션이 완료 되 면 hello 캡처 파일 업로드 tooblob tooa 또는 저장소에 로컬 파일 hello VM 수 있습니다. hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다. 저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/

저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>다음 단계

어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)

[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.

<!-- Image references -->














