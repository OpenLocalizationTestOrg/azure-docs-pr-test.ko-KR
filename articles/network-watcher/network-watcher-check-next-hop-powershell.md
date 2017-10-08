---
title: "Azure 네트워크 감시자 다음 홉-PowerShell aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서는 다음 홉 형식 어떤 hello 및 PowerShell을 사용 하 여 다음 홉 ip 주소를 사용 하 여를 찾는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하는 PowerShell을 사용 하 여 Azure 네트워크 감시자 확인

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다. 이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 Azure 포털 toofind hello 다음 홉 형식이 hello 및 IP 주소를 사용 합니다.

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다. hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.

## <a name="scenario"></a>시나리오

이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다. 다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.

## <a name="retrieve-network-watcher"></a>Network Watcher 검색

hello 첫 번째 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다. hello `$networkWatcher` 변수 toohello 다음 홉 전달 되는 cmdlet를 확인 합니다.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>가상 컴퓨터 가져오기

다음 홉 가상 컴퓨터에서 다음 홉 hello 및 hello hello 다음 홉 IP 주소를 반환합니다. 가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다. 가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> 다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.

## <a name="get-hello-network-interfaces"></a>Hello 네트워크 인터페이스 가져오기

hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때. 원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>다음 홉 가져오기

Hello 이라고 이제 `Get-AzureRmNetworkWatcherNextHop` cmdlet. 원본 IP 주소 및 대상 IP 주소를 hello cmdlet hello 네트워크 감시자 가상 컴퓨터 Id 통과 했습니다. 이 예제에서는 hello 대상 IP 주소는 다른 가상 네트워크에 VM tooa 합니다. Hello 두 가상 네트워크 간의 가상 네트워크 게이트웨이는 없습니다.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>결과 검토

완료 되 면 hello 결과가 제공 됩니다. hello 다음 홉 IP 주소는 리소스의 hello 형식을 반환 됩니다. 이 시나리오에서 hello hello 가상 네트워크 게이트웨이의 공용 IP 주소는 것입니다.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

hello 다음 목록은 hello 현재 사용 가능한 NextHopType 값.

**다음 홉 유형**

* 인터넷
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* 없음

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)

















