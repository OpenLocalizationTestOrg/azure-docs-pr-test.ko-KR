---
title: "Azure 네트워크 감시자-PowerShell와의 연결을 aaaCheck | Microsoft Docs"
description: "이 페이지에서는 설명 어떻게 PowerShell을 사용 하 여 네트워크 감시자의 tootest 연결"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a>PowerShell을 사용하여 Azure Network Watcher를 통해 연결 확인

> [!div class="op_single_selector"]
> - [포털](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

Toouse 연결 tooverify 경우 끝점에 지정 된 가상 컴퓨터 tooa의 직접 TCP 연결 수 설정 하는 방법에 대해 알아봅니다.

## <a name="before-you-begin"></a>시작하기 전에

이 문서에서는 다음 리소스는 hello 있는 가정 합니다.

* 인스턴스 toocheck 연결 hello 지역에 대 한 네트워크 감시자의 원하는 합니다.

* 가상 컴퓨터와 toocheck 연결 합니다.

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> 연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다. Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).

## <a name="register-hello-preview-capability"></a>Hello 미리 보기 기능 등록

연결 기능은 현재 공개 미리 보기 상태, toouse이 등록 toobe 필요한입니다. toodo PowerShell 예제를 따라이, 실행된 hello:

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

tooverify hello 등록에 성공 했다는 hello Powershell 샘플 다음 실행:

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

Hello 기능 제대로 등록 된 경우 hello 출력 hello 다음과 일치 해야 합니다.

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a>연결 tooa 가상 컴퓨터를 확인 합니다.

이 예제에서는 포트 80 통한 연결 tooa 대상 가상 컴퓨터를 확인합니다.

### <a name="example"></a>예제

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a>응답

다음 응답 hello hello 이전 예제에서 시작 됩니다.  이 응답에 hello `ConnectionStatus` 은 **연결할 수 없는**합니다. 실패 한 전송 하는 프로브를 hello 모두 볼 수 있습니다. hello 연결 hello 가상 기기에서 실패 했습니다 사용자가 구성한 due tooa `NetworkSecurityRule` 라는 **UserRule_Port80**, tooblock 들어오는 트래픽을 포트 80에 구성 합니다. 이 정보에 사용 되는 tooresearch 연결 문제 수 있습니다.

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a>라우팅 문제 확인

가상 컴퓨터와 원격 끝점 간의 연결을 확인 하는 hello 예제입니다.

### <a name="example"></a>예제

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a>응답

다음 예제는 hello에서 hello `ConnectionStatus` 으로 표시 되 고 **연결할 수 없는**합니다. Hello에 `Hops` 세부 정보를 아래에서 확인할 수 있습니다 `Issues` hello 트래픽 인해 차단 된 tooa `UserDefinedRoute`합니다. 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a>웹 사이트 대기 시간 확인

hello 다음 예제에서는 hello 연결 tooa 웹 사이트

### <a name="example"></a>예제

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a>응답

다음 응답 hello, hello를 볼 수 있습니다 `ConnectionStatus` 표시 **Reachable**합니다. 연결에 성공하면 대기 시간 값이 제공됩니다.

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a>연결 tooa 저장소 끝점 확인

다음 예에서는 hello 가상 컴퓨터 tooa 블로그 저장소 계정에서 hello 연결을 테스트 합니다.

### <a name="example"></a>예제

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a>응답

hello 다음 json은 hello hello 이전 cmdlet을 실행 하는 예제 응답입니다. 연결할 수 있는 hello 대상 그대로 hello `ConnectionStatus` 속성으로 표시 **Reachable**합니다.  Hello 수 홉 필요한 tooreach hello 저장소 blob 및 대기 시간에 관한 hello 세부 정보를 제공 됩니다.

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a>다음 단계

[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.

트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.

<!-- Image references -->














