---
title: "Azure Network Watcher를 사용하여 연결 확인 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 PowerShell을 사용하여 Network Watcher를 통해 연결을 테스트하는 방법을 설명합니다."
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
ms.openlocfilehash: a8f936cd23838759dc30b04688d3c6544e4895cc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="1332e-103">PowerShell을 사용하여 Azure Network Watcher를 통해 연결 확인</span><span class="sxs-lookup"><span data-stu-id="1332e-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1332e-104">포털</span><span class="sxs-lookup"><span data-stu-id="1332e-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="1332e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1332e-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="1332e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1332e-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="1332e-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="1332e-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="1332e-108">연결을 사용하여 가상 컴퓨터에서 지정된 끝점으로의 직접 TCP 연결을 설정할 수 있는지를 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1332e-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1332e-109">Before you begin</span></span>

<span data-ttu-id="1332e-110">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="1332e-111">연결을 확인하려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="1332e-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="1332e-112">연결을 확인하는 데 사용할 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1332e-112">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="1332e-113">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1332e-114">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1332e-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="1332e-115">미리 보기 기능 등록</span><span class="sxs-lookup"><span data-stu-id="1332e-115">Register the preview capability</span></span>

<span data-ttu-id="1332e-116">연결은 현재 공개 미리 보기로 제공되며, 등록해야 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-116">Connectivity is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="1332e-117">이 작업을 수행하려면 다음 PowerShell 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-117">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="1332e-118">등록이 성공했는지 확인하려면 다음 Powershell 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-118">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="1332e-119">기능이 올바르게 등록된 경우 출력은 다음과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-119">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="1332e-120">가상 컴퓨터에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="1332e-120">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="1332e-121">이 예제에서는 포트 80을 통해 대상 가상 컴퓨터에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-121">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="1332e-122">예제</span><span class="sxs-lookup"><span data-stu-id="1332e-122">Example</span></span>

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

### <a name="response"></a><span data-ttu-id="1332e-123">응답</span><span class="sxs-lookup"><span data-stu-id="1332e-123">Response</span></span>

<span data-ttu-id="1332e-124">다음 응답은 이전 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-124">The following response is from the previous example.</span></span>  <span data-ttu-id="1332e-125">이 응답에서 `ConnectionStatus`는 **Unreachable**입니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-125">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="1332e-126">전송된 모든 프로브가 실패한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-126">You can see that all the probes sent failed.</span></span> <span data-ttu-id="1332e-127">포트 80에서 들어오는 트래픽을 차단하도록 구성된, 사용자가 구성한 **UserRule_Port80**이라는 `NetworkSecurityRule`로 인해 가상 어플라이언스에서 연결이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-127">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="1332e-128">이 정보는 연결 문제를 조사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-128">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="1332e-129">라우팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="1332e-129">Validate routing issues</span></span>

<span data-ttu-id="1332e-130">이 예제에서는 가상 컴퓨터와 원격 끝점 간의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-130">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="1332e-131">예제</span><span class="sxs-lookup"><span data-stu-id="1332e-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="1332e-132">응답</span><span class="sxs-lookup"><span data-stu-id="1332e-132">Response</span></span>

<span data-ttu-id="1332e-133">다음 예제에서 `ConnectionStatus`는 **Unreachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-133">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="1332e-134">`Hops` 세부 정보의 `Issues`에서 트래픽이 `UserDefinedRoute`로 인해 차단되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-134">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

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

## <a name="check-website-latency"></a><span data-ttu-id="1332e-135">웹 사이트 대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="1332e-135">Check website latency</span></span>

<span data-ttu-id="1332e-136">다음 예제에서는 웹 사이트에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-136">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="1332e-137">예제</span><span class="sxs-lookup"><span data-stu-id="1332e-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="1332e-138">응답</span><span class="sxs-lookup"><span data-stu-id="1332e-138">Response</span></span>

<span data-ttu-id="1332e-139">다음 응답에서 `ConnectionStatus`가 **Reachable**로 표시된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-139">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="1332e-140">연결에 성공하면 대기 시간 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-140">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="1332e-141">저장소 끝점에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="1332e-141">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="1332e-142">다음 예제에서는 가상 컴퓨터에서 BLOB 저장소 계정으로의 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-142">The following example tests the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="1332e-143">예제</span><span class="sxs-lookup"><span data-stu-id="1332e-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="1332e-144">응답</span><span class="sxs-lookup"><span data-stu-id="1332e-144">Response</span></span>

<span data-ttu-id="1332e-145">다음 json은 이전 cmdlet 실행에서 가져온 예제 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-145">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="1332e-146">대상에 연결할 수 있으므로 `ConnectionStatus` 속성은 **Reachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-146">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="1332e-147">저장소 BLOB 및 대기 시간에 도달하는 데 필요한 홉 수에 대한 세부 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-147">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1332e-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1332e-148">Next steps</span></span>

<span data-ttu-id="1332e-149">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="1332e-150">트래픽이 차단되지 않아야 하는데 차단된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 정의된 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1332e-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<!-- Image references -->














