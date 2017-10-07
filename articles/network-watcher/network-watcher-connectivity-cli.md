---
title: "Azure 네트워크 감시자-Azure CLI 2.0와의 연결을 aaaCheck | Microsoft Docs"
description: "이 페이지에서는 Azure CLI 2.0을 사용 하 여 네트워크 감시자를 toouse 연결을 확인 하는 방법을 설명 합니다."
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
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="13f40-103">Azure CLI 2.0을 사용하여 Azure Network Watcher를 통해 연결 확인</span><span class="sxs-lookup"><span data-stu-id="13f40-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="13f40-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f40-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="13f40-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="13f40-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="13f40-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="13f40-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="13f40-107">Toouse 연결 tooverify 경우 끝점에 지정 된 가상 컴퓨터 tooa의 직접 TCP 연결 수 설정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="13f40-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="13f40-108">Before you begin</span></span>

<span data-ttu-id="13f40-109">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="13f40-110">인스턴스 toocheck 연결 hello 지역에 대 한 네트워크 감시자의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="13f40-111">가상 컴퓨터와 toocheck 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="13f40-112">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="13f40-113">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="13f40-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="13f40-114">Hello 미리 보기 기능 등록</span><span class="sxs-lookup"><span data-stu-id="13f40-114">Register hello preview capability</span></span> 

<span data-ttu-id="13f40-115">연결성 확인 기능은 현재 공개 미리 보기 상태, toouse이 등록 toobe 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="13f40-116">toodo CLI 샘플 다음이 실행된 hello</span><span class="sxs-lookup"><span data-stu-id="13f40-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="13f40-117">tooverify hello 등록에 성공 했다는 hello 다음 CLI 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="13f40-118">Hello 기능 제대로 등록 된 경우 hello 출력 hello 다음과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="13f40-119">연결 tooa 가상 컴퓨터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="13f40-120">이 예제에서는 포트 80 통한 연결 tooa 대상 가상 컴퓨터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="13f40-121">예제</span><span class="sxs-lookup"><span data-stu-id="13f40-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="13f40-122">응답</span><span class="sxs-lookup"><span data-stu-id="13f40-122">Response</span></span>

<span data-ttu-id="13f40-123">다음 응답 hello hello 이전 예제에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="13f40-124">이 응답에 hello `ConnectionStatus` 은 **연결할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="13f40-125">실패 한 전송 하는 프로브를 hello 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="13f40-126">hello 연결 hello 가상 기기에서 실패 했습니다 사용자가 구성한 due tooa `NetworkSecurityRule` 라는 **UserRule_Port80**, tooblock 들어오는 트래픽을 포트 80에 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="13f40-127">이 정보에 사용 되는 tooresearch 연결 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-127">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="13f40-128">라우팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="13f40-128">Validate routing issues</span></span>

<span data-ttu-id="13f40-129">가상 컴퓨터와 원격 끝점 간의 연결을 확인 하는 hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="13f40-130">예제</span><span class="sxs-lookup"><span data-stu-id="13f40-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="13f40-131">응답</span><span class="sxs-lookup"><span data-stu-id="13f40-131">Response</span></span>

<span data-ttu-id="13f40-132">다음 예제는 hello에서 hello `connectionStatus` 으로 표시 되 고 **연결할 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="13f40-133">Hello에 `hops` 세부 정보를 아래에서 확인할 수 있습니다 `issues` hello 트래픽 인해 차단 된 tooa `UserDefinedRoute`합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="13f40-134">웹 사이트 대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="13f40-134">Check website latency</span></span>

<span data-ttu-id="13f40-135">hello 다음 예제에서는 hello 연결 tooa 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="13f40-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="13f40-136">예제</span><span class="sxs-lookup"><span data-stu-id="13f40-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="13f40-137">응답</span><span class="sxs-lookup"><span data-stu-id="13f40-137">Response</span></span>

<span data-ttu-id="13f40-138">다음 응답 hello, hello를 볼 수 있습니다 `connectionStatus` 표시 **Reachable**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="13f40-139">연결에 성공하면 대기 시간 값이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-139">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="13f40-140">연결 tooa 저장소 끝점 확인</span><span class="sxs-lookup"><span data-stu-id="13f40-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="13f40-141">hello 다음 예제에서는 가상 컴퓨터 tooa 블로그 저장소 계정에서 hello 연결</span><span class="sxs-lookup"><span data-stu-id="13f40-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="13f40-142">예제</span><span class="sxs-lookup"><span data-stu-id="13f40-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="13f40-143">응답</span><span class="sxs-lookup"><span data-stu-id="13f40-143">Response</span></span>

<span data-ttu-id="13f40-144">hello 다음 json은 hello hello 이전 cmdlet을 실행 하는 예제 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="13f40-145">Hello 확인 되 면 대로 hello `connectionStatus` 속성으로 표시 **Reachable**합니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="13f40-146">Hello 수 홉 필요한 tooreach hello 저장소 blob 및 대기 시간에 관한 hello 세부 정보를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="13f40-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13f40-147">Next steps</span></span>

<span data-ttu-id="13f40-148">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="13f40-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="13f40-149">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="13f40-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
