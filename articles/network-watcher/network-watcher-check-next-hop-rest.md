---
title: "Azure Network Watcher Next Hop을 사용하여 다음 홉 찾기 - REST | Microsoft Docs"
description: "이 문서에서는 Azure REST API로 Next Hop을 사용하여 다음 홉 유형 및 IP 주소를 찾을 수 있는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="60bde-103">Azure REST API를 사용하는 Azure Network Watcher에서 Next Hop 기능을 사용하는 다음 홉이 무엇인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="60bde-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="60bde-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="60bde-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60bde-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="60bde-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="60bde-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="60bde-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60bde-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="60bde-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="60bde-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="60bde-109">Next Hop은 Network Watcher의 기능으로 지정된 가상 컴퓨터를 기반으로 하는 다음 홉 유형 및 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="60bde-110">이 기능은 가상 컴퓨터에서 나가는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크를 트래버스하여 대상에 도달할지 여부를 결정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="60bde-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="60bde-111">Before you begin</span></span>

<span data-ttu-id="60bde-112">PowerShell을 사용하여 REST API를 호출하는 데 ARMclient가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="60bde-113">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="60bde-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="60bde-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="60bde-115">Scenario</span></span>

<span data-ttu-id="60bde-116">이 문서에서 다루는 시나리오는 리소스에 대한 다음 홉 유형 및 IP 주소를 찾는 Network Watcher의 기능인 Next Hop을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="60bde-117">Next Hop에 대한 자세한 내용을 보려면 [Next Hop 개요](network-watcher-next-hop-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="60bde-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="60bde-118">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-118">In this scenario, you will:</span></span>

* <span data-ttu-id="60bde-119">가상 컴퓨터에 대한 다음 홉을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="60bde-120">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="60bde-120">Log in with ARMClient</span></span>

<span data-ttu-id="60bde-121">Azure 자격 증명으로 armclient에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="60bde-122">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="60bde-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="60bde-123">다음 스크립트를 실행하여 가상 컴퓨터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="60bde-124">다음 홉을 실행하는 데 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="60bde-125">다음 코드에는 다음 변수에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="60bde-126">**subscriptionId** - 사용할 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="60bde-127">**resourceGroupName** - 가상 컴퓨터를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="60bde-128">다음 출력에서는 다음 예제에 가상 컴퓨터의 ID가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="60bde-129">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="60bde-129">Get Next Hop</span></span>

<span data-ttu-id="60bde-130">권한 부여 헤더가 생성되면 가상 컴퓨터의 다음 홉을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="60bde-131">작동할 코드 예에 대해 다음 값을 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="60bde-132">Network Watcher REST API 호출의 경우 요청 URI에 있는 리소스 그룹 이름은 진단 작업이 수행되는 리소스가 아니라, Network Watcher를 포함하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="60bde-133">다음 홉에서는 VM 리소스가 실행되기 위해 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="60bde-134">결과</span><span class="sxs-lookup"><span data-stu-id="60bde-134">Results</span></span>

<span data-ttu-id="60bde-135">다음 코드 조각은 수신된 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="60bde-136">결과에는 다음 값이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-136">The results contain the following values:</span></span>

* <span data-ttu-id="60bde-137">**nextHopType** - 이 값은 Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway 또는 None 값 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="60bde-138">**nextHopIpAddress** - 다음 홉의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="60bde-139">**routeTableId** - 이 값은 경로와 연결된 경로 테이블에 대한 URI이거나 사용자 정의 경로가 정의되지 않은 경우 *System Route* 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="60bde-140">다음은 json 형식의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="60bde-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60bde-141">Next steps</span></span>

<span data-ttu-id="60bde-142">가상 컴퓨터에 대해 다음 홉을 확인할 수 있으려면 [보안 보기 개요](network-watcher-security-group-view-overview.md)를 방문하여 네트워크 리소스의 보안을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60bde-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














