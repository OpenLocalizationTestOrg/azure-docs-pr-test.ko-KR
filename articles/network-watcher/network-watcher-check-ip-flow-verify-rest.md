---
title: "Azure Network Watcher IP 흐름 확인을 사용하여 트래픽 확인 - REST | Microsoft Docs"
description: "이 문서에서는 가상 컴퓨터 간에 트래픽을 허용하는지 아니면 거부하는지를 확인하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="ceb38-103">Azure Network Watcher의 구성 요소인 IP 흐름 확인을 사용하여 트래픽을 허용하는지 아니면 거부하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ceb38-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ceb38-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="ceb38-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceb38-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="ceb38-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ceb38-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="ceb38-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ceb38-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="ceb38-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="ceb38-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="ceb38-109">IP 흐름 확인은 가상 컴퓨터 간에 트래픽을 허용하는지를 확인할 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="ceb38-110">들어오거나 나가는 트래픽에 대해 유효성 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="ceb38-111">이 시나리오는 가상 컴퓨터가 외부 리소스 또는 백 엔드에 연결할 수 있는지에 대한 현재 상태를 가져올 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="ceb38-112">IP 흐름 확인은 NSG(네트워크 보안 그룹) 규칙이 모두 제대로 구성되었는지 확인하고 NSG 규칙에 의해 차단되는 흐름 문제를 해결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="ceb38-113">IP 흐름 확인을 사용하여 차단하려는 트래픽이 NSG에서 제대로 차단되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ceb38-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ceb38-114">Before you begin</span></span>

<span data-ttu-id="ceb38-115">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="ceb38-116">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="ceb38-117">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="ceb38-118">시나리오</span><span class="sxs-lookup"><span data-stu-id="ceb38-118">Scenario</span></span>

<span data-ttu-id="ceb38-119">이 시나리오에서는 IP 흐름 확인을 사용하여 가상 컴퓨터가 포트 443을 통해 다른 컴퓨터와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="ceb38-120">트래픽이 거부된 경우 해당 트래픽을 거부하는 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="ceb38-121">IP 흐름 확인에 대한 자세한 내용을 보려면 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ceb38-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="ceb38-122">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-122">In this scenario, you:</span></span>

* <span data-ttu-id="ceb38-123">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="ceb38-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="ceb38-124">IP 흐름 확인 호출</span><span class="sxs-lookup"><span data-stu-id="ceb38-124">Call IP flow verify</span></span>
* <span data-ttu-id="ceb38-125">결과 확인</span><span class="sxs-lookup"><span data-stu-id="ceb38-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="ceb38-126">ARMClient로 로그인</span><span class="sxs-lookup"><span data-stu-id="ceb38-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="ceb38-127">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="ceb38-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="ceb38-128">다음 스크립트를 실행하여 가상 컴퓨터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="ceb38-129">다음 코드에는 다음 변수에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="ceb38-130">**subscriptionId** - 사용할 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="ceb38-131">**resourceGroupName** - 가상 컴퓨터를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="ceb38-132">필요한 정보는 유형 `Microsoft.Compute/virtualMachines` 아래의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="ceb38-133">결과는 다음 코드 샘플과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="ceb38-134">IP 흐름 확인 호출</span><span class="sxs-lookup"><span data-stu-id="ceb38-134">Call IP flow Verify</span></span>

<span data-ttu-id="ceb38-135">다음 예제에서는 지정된 가상 컴퓨터에 대한 트래픽을 확인하는 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="ceb38-136">응답은 트래픽이 허용되는 경우 또는 트래픽이 거부되는 경우를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="ceb38-137">트래픽이 거부되는 경우 어떤 규칙에서 트래픽을 차단하는지 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="ceb38-138">IP 흐름 확인에서는 VM 리소스가 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="ceb38-139">스크립트에는 가상 컴퓨터의 리소스 ID 및 가상 컴퓨터에 있는 네트워크 인터페이스 카드의 리소스 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="ceb38-140">위의 출력에서 이러한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="ceb38-141">Network Watcher REST 호출의 경우 요청 URI에 있는 리소스 그룹 이름은 진단 작업을 수행하는 리소스가 아니라, Network Watcher 인스턴스를 포함하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="ceb38-142">결과 이해</span><span class="sxs-lookup"><span data-stu-id="ceb38-142">Understanding the results</span></span>

<span data-ttu-id="ceb38-143">사용자가 받는 응답은 트래픽의 허용 또는 거부 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="ceb38-144">응답은 다음 예제 중 하나와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="ceb38-145">**허용됨**</span><span class="sxs-lookup"><span data-stu-id="ceb38-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="ceb38-146">**거부됨**</span><span class="sxs-lookup"><span data-stu-id="ceb38-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="ceb38-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ceb38-147">Next steps</span></span>

<span data-ttu-id="ceb38-148">트래픽이 차단되지 않아야 하는데 차단된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 네트워크 보안 그룹에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ceb38-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












