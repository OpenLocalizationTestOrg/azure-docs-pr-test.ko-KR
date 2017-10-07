---
title: "Azure 네트워크 감시자-Azure 포털의 aaaCheck 연결 | Microsoft Docs"
description: "이 페이지에서는 방법에 대 한 네트워크 감시자와의 연결을 toocheck hello Azure 포털을 설명 합니다."
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
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="dfac1-103">Hello Azure 포털을 사용 하 여 Azure 네트워크 감시자를 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="dfac1-104">포털</span><span class="sxs-lookup"><span data-stu-id="dfac1-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="dfac1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfac1-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="dfac1-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dfac1-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="dfac1-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="dfac1-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="dfac1-108">Toouse 연결 tooverify 경우 끝점에 지정 된 가상 컴퓨터 tooa의 직접 TCP 연결 수 설정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dfac1-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="dfac1-109">Before you begin</span></span>

<span data-ttu-id="dfac1-110">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="dfac1-111">인스턴스 toocheck 연결 hello 지역에 대 한 네트워크 감시자의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="dfac1-112">가상 컴퓨터와 toocheck 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="dfac1-113">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="dfac1-114">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="dfac1-115">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="dfac1-116">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="dfac1-117">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="dfac1-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="dfac1-118">Hello 미리 보기 기능 등록</span><span class="sxs-lookup"><span data-stu-id="dfac1-118">Register hello preview capability</span></span>

<span data-ttu-id="dfac1-119">연결성 확인 기능은 현재 공개 미리 보기 상태, toouse이 등록 toobe 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="dfac1-120">toodo PowerShell 예제를 따라이, 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="dfac1-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="dfac1-121">tooverify hello 등록에 성공 했다는 hello Powershell 샘플 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="dfac1-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="dfac1-122">Hello 기능 제대로 등록 된 경우 hello 출력 hello 다음과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="dfac1-123">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="dfac1-123">Log in with ARMClient</span></span>

<span data-ttu-id="dfac1-124">Tooarmclient Azure 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="dfac1-125">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="dfac1-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="dfac1-126">다음 스크립트 tooreturn hello 가상 컴퓨터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="dfac1-127">연결을 실행하는 데 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="dfac1-128">hello 코드 다음 변수에 따라 hello에 대 한 값을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="dfac1-129">**subscriptionId** -구독 ID toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="dfac1-130">**resourceGroupName** -hello 가상 컴퓨터를 포함 하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="dfac1-131">Hello 다음과 같은 출력에서 hello 가상 컴퓨터의 hello ID는 다음 예제는 hello에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="dfac1-132">연결 tooa 가상 컴퓨터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="dfac1-133">이 예제에서는 포트 80 통한 연결 tooa 대상 가상 컴퓨터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="dfac1-134">예제</span><span class="sxs-lookup"><span data-stu-id="dfac1-134">Example</span></span>

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

<span data-ttu-id="dfac1-135">이 작업은 오래 하므로 실행 하 고 hello hello 결과 대 한 URI 헤더에 반환 됩니다 hello 응답 hello 응답 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="dfac1-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="dfac1-136">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="dfac1-136">**Important Values**</span></span>

* <span data-ttu-id="dfac1-137">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="dfac1-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="dfac1-138">응답</span><span class="sxs-lookup"><span data-stu-id="dfac1-138">Response</span></span>

<span data-ttu-id="dfac1-139">다음 응답 hello hello 이전 예제에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="dfac1-140">이 응답에 hello `ConnectionStatus` 은 **연결할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="dfac1-141">실패 한 전송 하는 프로브를 hello 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="dfac1-142">hello 연결 hello 가상 기기에서 실패 했습니다 사용자가 구성한 due tooa `NetworkSecurityRule` 라는 **UserRule_Port80**, tooblock 들어오는 트래픽을 포트 80에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="dfac1-143">이 정보에 사용 되는 tooresearch 연결 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-143">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="dfac1-144">라우팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="dfac1-144">Validate routing issues</span></span>

<span data-ttu-id="dfac1-145">가상 컴퓨터와 원격 끝점 간의 연결을 확인 하는 hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="dfac1-146">예제</span><span class="sxs-lookup"><span data-stu-id="dfac1-146">Example</span></span>

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

<span data-ttu-id="dfac1-147">이 작업은 오래 하므로 실행 하 고 hello hello 결과 대 한 URI 헤더에 반환 됩니다 hello 응답 hello 응답 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="dfac1-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="dfac1-148">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="dfac1-148">**Important Values**</span></span>

* <span data-ttu-id="dfac1-149">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="dfac1-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="dfac1-150">응답</span><span class="sxs-lookup"><span data-stu-id="dfac1-150">Response</span></span>

<span data-ttu-id="dfac1-151">다음 예제는 hello에서 hello `connectionStatus` 으로 표시 되 고 **연결할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="dfac1-152">Hello에 `hops` 세부 정보를 아래에서 확인할 수 있습니다 `issues` hello 트래픽 인해 차단 된 tooa `UserDefinedRoute`합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="dfac1-153">웹 사이트 대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="dfac1-153">Check website latency</span></span>

<span data-ttu-id="dfac1-154">hello 다음 예제에서는 hello 연결 tooa 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="dfac1-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="dfac1-155">예제</span><span class="sxs-lookup"><span data-stu-id="dfac1-155">Example</span></span>

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

<span data-ttu-id="dfac1-156">이 작업은 오래 하므로 실행 하 고 hello hello 결과 대 한 URI 헤더에 반환 됩니다 hello 응답 hello 응답 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="dfac1-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="dfac1-157">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="dfac1-157">**Important Values**</span></span>

* <span data-ttu-id="dfac1-158">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="dfac1-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="dfac1-159">응답</span><span class="sxs-lookup"><span data-stu-id="dfac1-159">Response</span></span>

<span data-ttu-id="dfac1-160">다음 응답 hello, hello를 볼 수 있습니다 `connectionStatus` 표시 **Reachable**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="dfac1-161">연결에 성공하면 대기 시간 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-161">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="dfac1-162">연결 tooa 저장소 끝점 확인</span><span class="sxs-lookup"><span data-stu-id="dfac1-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="dfac1-163">hello 다음 예제에서는 가상 컴퓨터 tooa 블로그 저장소 계정에서 hello 연결</span><span class="sxs-lookup"><span data-stu-id="dfac1-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="dfac1-164">예제</span><span class="sxs-lookup"><span data-stu-id="dfac1-164">Example</span></span>

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

<span data-ttu-id="dfac1-165">이 작업은 오래 하므로 실행 하 고 hello hello 결과 대 한 URI 헤더에 반환 됩니다 hello 응답 hello 응답 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="dfac1-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="dfac1-166">**중요한 값**</span><span class="sxs-lookup"><span data-stu-id="dfac1-166">**Important Values**</span></span>

* <span data-ttu-id="dfac1-167">**위치** -hello hello 결과가 있는 경우 hello 작업이 완료 되는 URI가 포함 되어이 속성</span><span class="sxs-lookup"><span data-stu-id="dfac1-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="response"></a><span data-ttu-id="dfac1-168">응답</span><span class="sxs-lookup"><span data-stu-id="dfac1-168">Response</span></span>

<span data-ttu-id="dfac1-169">hello 다음 예제는 hello 응답 hello 이전 API 호출을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="dfac1-170">Hello 확인 되 면 대로 hello `connectionStatus` 속성으로 표시 **Reachable**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="dfac1-171">Hello 수 홉 필요한 tooreach hello 저장소 blob 및 대기 시간에 관한 hello 세부 정보를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dfac1-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfac1-172">Next steps</span></span>

<span data-ttu-id="dfac1-173">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="dfac1-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="dfac1-174">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfac1-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














