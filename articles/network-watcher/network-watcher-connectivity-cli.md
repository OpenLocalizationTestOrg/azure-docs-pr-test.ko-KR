---
title: "Azure Network Watcher를 사용하여 연결 확인 - Azure CLI 2.0 | Microsoft Docs"
description: "이 페이지에서는 Azure CLI 2.0을 사용하여 Network Watcher를 통해 연결 확인을 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="124e7-103">Azure CLI 2.0을 사용하여 Azure Network Watcher를 통해 연결 확인</span><span class="sxs-lookup"><span data-stu-id="124e7-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="124e7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="124e7-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="124e7-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="124e7-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="124e7-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="124e7-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="124e7-107">연결을 사용하여 가상 컴퓨터에서 지정된 끝점으로의 직접 TCP 연결을 설정할 수 있는지를 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="124e7-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="124e7-108">Before you begin</span></span>

<span data-ttu-id="124e7-109">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="124e7-110">연결을 확인하려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="124e7-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="124e7-111">연결을 확인하는 데 사용할 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="124e7-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="124e7-112">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="124e7-113">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="124e7-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="124e7-114">미리 보기 기능 등록</span><span class="sxs-lookup"><span data-stu-id="124e7-114">Register the preview capability</span></span> 

<span data-ttu-id="124e7-115">연결 확인은 현재 공개 미리 보기로, 등록해야 이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="124e7-116">이렇게 하려면 다음 CLI 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="124e7-117">등록이 성공했는지 확인하려면 다음 CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="124e7-118">기능이 올바르게 등록된 경우 출력은 다음과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-118">If the feature was properly registered, the output should match the following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="124e7-119">가상 컴퓨터에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="124e7-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="124e7-120">이 예제에서는 포트 80을 통해 대상 가상 컴퓨터에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="124e7-121">예제</span><span class="sxs-lookup"><span data-stu-id="124e7-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="124e7-122">응답</span><span class="sxs-lookup"><span data-stu-id="124e7-122">Response</span></span>

<span data-ttu-id="124e7-123">다음 응답은 이전 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-123">The following response is from the previous example.</span></span>  <span data-ttu-id="124e7-124">이 응답에서 `ConnectionStatus`는 **Unreachable**입니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="124e7-125">전송된 모든 프로브가 실패한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="124e7-126">포트 80에서 들어오는 트래픽을 차단하도록 구성된, 사용자가 구성한 **UserRule_Port80**이라는 `NetworkSecurityRule`로 인해 가상 어플라이언스에서 연결이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="124e7-127">이 정보는 연결 문제를 조사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-127">This information can be used to research connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="124e7-128">라우팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="124e7-128">Validate routing issues</span></span>

<span data-ttu-id="124e7-129">이 예제에서는 가상 컴퓨터와 원격 끝점 간의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="124e7-130">예제</span><span class="sxs-lookup"><span data-stu-id="124e7-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="124e7-131">응답</span><span class="sxs-lookup"><span data-stu-id="124e7-131">Response</span></span>

<span data-ttu-id="124e7-132">다음 예제에서 `connectionStatus`는 **Unreachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="124e7-133">`hops` 세부 정보의 `issues`에서 트래픽이 `UserDefinedRoute`로 인해 차단되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="124e7-134">웹 사이트 대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="124e7-134">Check website latency</span></span>

<span data-ttu-id="124e7-135">다음 예제에서는 웹 사이트에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="124e7-136">예제</span><span class="sxs-lookup"><span data-stu-id="124e7-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="124e7-137">응답</span><span class="sxs-lookup"><span data-stu-id="124e7-137">Response</span></span>

<span data-ttu-id="124e7-138">다음 응답에서 `connectionStatus`가 **Reachable**로 표시된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="124e7-139">연결에 성공하면 대기 시간 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="124e7-140">저장소 끝점에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="124e7-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="124e7-141">다음 예제에서는 가상 컴퓨터에서 BLOB 저장소 계정으로의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="124e7-142">예제</span><span class="sxs-lookup"><span data-stu-id="124e7-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="124e7-143">응답</span><span class="sxs-lookup"><span data-stu-id="124e7-143">Response</span></span>

<span data-ttu-id="124e7-144">다음 json은 이전 cmdlet 실행에서 가져온 예제 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="124e7-145">확인에 성공했으므로 `connectionStatus` 속성이 **Reachable**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="124e7-146">저장소 BLOB 및 대기 시간에 도달하는 데 필요한 홉 수에 대한 세부 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="124e7-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="124e7-147">Next steps</span></span>

<span data-ttu-id="124e7-148">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="124e7-149">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="124e7-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
