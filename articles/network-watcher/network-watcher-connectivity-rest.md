---
title: "Azure Network Watcher를 사용하여 연결 확인 - Azure Portal | Microsoft Docs"
description: "이 페이지에서는 Azure Portal에서 Network Watcher를 사용하여 연결을 확인하는 방법을 설명합니다."
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
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: ca62bea581acb59d3c3c0b8a204cc9d42de2b27f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="71050-103">Azure Portal을 사용하여 Azure Network Watcher를 통해 연결 확인</span><span class="sxs-lookup"><span data-stu-id="71050-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="71050-104">포털</span><span class="sxs-lookup"><span data-stu-id="71050-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="71050-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71050-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="71050-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="71050-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="71050-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="71050-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="71050-108">연결을 사용하여 가상 컴퓨터에서 지정된 끝점으로의 직접 TCP 연결을 설정할 수 있는지를 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="71050-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71050-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="71050-109">Before you begin</span></span>

<span data-ttu-id="71050-110">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="71050-111">연결을 확인하려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="71050-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="71050-112">연결을 확인하는 데 사용할 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="71050-112">Virtual machines to check connectivity with.</span></span>

<span data-ttu-id="71050-113">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="71050-114">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="71050-115">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="71050-116">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="71050-117">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="71050-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="71050-118">미리 보기 기능 등록</span><span class="sxs-lookup"><span data-stu-id="71050-118">Register the preview capability</span></span>

<span data-ttu-id="71050-119">연결 확인은 현재 공개 미리 보기로, 등록해야 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-119">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="71050-120">이 작업을 수행하려면 다음 PowerShell 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-120">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="71050-121">등록이 성공했는지 확인하려면 다음 Powershell 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-121">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="71050-122">기능이 올바르게 등록된 경우 출력은 다음과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-122">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="71050-123">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="71050-123">Log in with ARMClient</span></span>

<span data-ttu-id="71050-124">Azure 자격 증명으로 armclient에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="71050-125">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="71050-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="71050-126">다음 스크립트를 실행하여 가상 컴퓨터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-126">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="71050-127">연결을 실행하는 데 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="71050-128">다음 코드에는 다음 변수에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-128">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="71050-129">**subscriptionId** - 사용할 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="71050-129">**subscriptionId** - The subscription ID to use.</span></span>
- <span data-ttu-id="71050-130">**resourceGroupName** - 가상 컴퓨터를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="71050-130">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="71050-131">다음 출력에서는 다음 예제에 가상 컴퓨터의 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-131">From the following output, the ID of the virtual machine is used in the following example:</span></span>

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="71050-132">가상 컴퓨터에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="71050-132">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="71050-133">이 예제에서는 포트 80을 통해 대상 가상 컴퓨터에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-133">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="71050-134">예제</span><span class="sxs-lookup"><span data-stu-id="71050-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="71050-135">이 작업은 장기 실행되므로 결과의 URI는 다음 응답에 표시된 것처럼 응답 헤더에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-135">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="71050-136">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="71050-136">**Important Values**</span></span>

* <span data-ttu-id="71050-137">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-137">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="71050-138">응답</span><span class="sxs-lookup"><span data-stu-id="71050-138">Response</span></span>

<span data-ttu-id="71050-139">다음 응답은 이전 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="71050-139">The following response is from the previous example.</span></span>  <span data-ttu-id="71050-140">이 응답에서 `ConnectionStatus`는 **Unreachable**입니다.</span><span class="sxs-lookup"><span data-stu-id="71050-140">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="71050-141">전송된 모든 프로브가 실패한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-141">You can see that all the probes sent failed.</span></span> <span data-ttu-id="71050-142">포트 80에서 들어오는 트래픽을 차단하도록 구성된, 사용자가 구성한 **UserRule_Port80**이라는 `NetworkSecurityRule`로 인해 가상 어플라이언스에서 연결이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-142">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="71050-143">이 정보는 연결 문제를 조사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-143">This information can be used to research connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="71050-144">라우팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="71050-144">Validate routing issues</span></span>

<span data-ttu-id="71050-145">이 예제에서는 가상 컴퓨터와 원격 끝점 간의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-145">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="71050-146">예제</span><span class="sxs-lookup"><span data-stu-id="71050-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="71050-147">이 작업은 장기 실행되므로 결과의 URI는 다음 응답에 표시된 것처럼 응답 헤더에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-147">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="71050-148">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="71050-148">**Important Values**</span></span>

* <span data-ttu-id="71050-149">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-149">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="71050-150">응답</span><span class="sxs-lookup"><span data-stu-id="71050-150">Response</span></span>

<span data-ttu-id="71050-151">다음 예제에서 `connectionStatus`는 **Unreachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-151">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="71050-152">`hops` 세부 정보의 `issues`에서 트래픽이 `UserDefinedRoute`로 인해 차단되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-152">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="71050-153">웹 사이트 대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="71050-153">Check website latency</span></span>

<span data-ttu-id="71050-154">다음 예제에서는 웹 사이트에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-154">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="71050-155">예제</span><span class="sxs-lookup"><span data-stu-id="71050-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="71050-156">이 작업은 장기 실행되므로 결과의 URI는 다음 응답에 표시된 것처럼 응답 헤더에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-156">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="71050-157">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="71050-157">**Important Values**</span></span>

* <span data-ttu-id="71050-158">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-158">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="71050-159">응답</span><span class="sxs-lookup"><span data-stu-id="71050-159">Response</span></span>

<span data-ttu-id="71050-160">다음 응답에서 `connectionStatus`가 **Reachable**로 표시된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71050-160">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="71050-161">연결에 성공하면 대기 시간 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="71050-162">저장소 끝점에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="71050-162">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="71050-163">다음 예제에서는 가상 컴퓨터에서 BLOB 저장소 계정으로의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-163">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="71050-164">예제</span><span class="sxs-lookup"><span data-stu-id="71050-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="71050-165">이 작업은 장기 실행되므로 결과의 URI는 다음 응답에 표시된 것처럼 응답 헤더에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-165">Since this operation is long running, the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="71050-166">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="71050-166">**Important Values**</span></span>

* <span data-ttu-id="71050-167">**위치** - 이 속성에는 작업이 완료될 때 결과가 있는 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="71050-167">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="71050-168">응답</span><span class="sxs-lookup"><span data-stu-id="71050-168">Response</span></span>

<span data-ttu-id="71050-169">다음 예제는 이전 API 호출 실행에서 가져온 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="71050-169">The following example is the response from running the previous API call.</span></span> <span data-ttu-id="71050-170">확인에 성공했으므로 `connectionStatus` 속성이 **Reachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-170">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="71050-171">저장소 BLOB 및 대기 시간에 도달하는 데 필요한 홉 수에 대한 세부 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="71050-171">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="71050-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71050-172">Next steps</span></span>

<span data-ttu-id="71050-173">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="71050-173">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="71050-174">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="71050-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














