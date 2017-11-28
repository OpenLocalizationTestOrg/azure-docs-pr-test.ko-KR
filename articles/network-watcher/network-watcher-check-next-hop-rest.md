---
title: "Azure 네트워크 감시자 다음 홉-REST와 다음 홉 aaaFind | Microsoft Docs"
description: "이 문서는 어떤 hello 다음 홉 형식 및 ip 주소를 사용 하 여 다음 홉을 사용 하 여 hello Azure REST API를 찾는 방법을 설명 합니다."
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
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="8ee55-103">어떤 hello 다음 홉 형식이 Aure 네트워크 감시자 Azure REST API를 사용 하 여 hello 다음 홉 기능을 사용 하는 확인</span><span class="sxs-lookup"><span data-stu-id="8ee55-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8ee55-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8ee55-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="8ee55-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ee55-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="8ee55-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ee55-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="8ee55-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ee55-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="8ee55-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="8ee55-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="8ee55-109">다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="8ee55-110">이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ee55-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8ee55-111">Before you begin</span></span>

<span data-ttu-id="8ee55-112">ARMclient는 PowerShell을 사용 하 여 사용 되는 toocall hello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="8ee55-113">ARMClient는 [Chocolatey의 ARMClient](https://chocolatey.org/packages/ARMClient)에서 chocolatey에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="8ee55-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="8ee55-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="8ee55-115">Scenario</span></span>

<span data-ttu-id="8ee55-116">이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="8ee55-117">다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="8ee55-118">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-118">In this scenario, you will:</span></span>

* <span data-ttu-id="8ee55-119">가상 컴퓨터에 대 한 다음 홉 hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="8ee55-120">ARMClient에 로그인</span><span class="sxs-lookup"><span data-stu-id="8ee55-120">Log in with ARMClient</span></span>

<span data-ttu-id="8ee55-121">Tooarmclient Azure 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="8ee55-122">가상 컴퓨터 검색</span><span class="sxs-lookup"><span data-stu-id="8ee55-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="8ee55-123">다음 스크립트 tooreturn hello 가상 컴퓨터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="8ee55-124">다음 홉을 실행하는 데 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="8ee55-125">hello 코드 다음 변수에 따라 hello에 대 한 값을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="8ee55-126">**subscriptionId** -구독 Id toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="8ee55-127">**resourceGroupName** -hello 가상 컴퓨터를 포함 하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="8ee55-128">Hello 다음과 같은 출력에서 hello 가상 컴퓨터의 hello id는 다음 예제는 hello에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="8ee55-129">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="8ee55-129">Get Next Hop</span></span>

<span data-ttu-id="8ee55-130">Hello 권한 부여 헤더를 만든 후에 가상 컴퓨터에서 다음 홉 hello를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="8ee55-131">hello 다음 값 바꾸어야 코드 예제에서는 toowork hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="8ee55-132">네트워크 감시자 REST API에 대 한 호출 hello hello 요청 URI는 hello 진단 작업에서 수행 하는 hello 리소스가 아닌 hello 네트워크 감시자를 포함 하는 hello 리소스 그룹에에서 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

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
> <span data-ttu-id="8ee55-133">다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="8ee55-134">결과</span><span class="sxs-lookup"><span data-stu-id="8ee55-134">Results</span></span>

<span data-ttu-id="8ee55-135">hello 다음 코드 조각은 수신 하는 hello 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="8ee55-136">hello 결과는 다음 값에는 hello 포함:</span><span class="sxs-lookup"><span data-stu-id="8ee55-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="8ee55-137">**nextHopType** -이 값은 hello 다음 값 중 하나: 인터넷, virtualappliance 인, VirtualNetworkGateway, VnetLocal, HyperNetGateway, 또는 None입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="8ee55-138">**nextHopIpAddress** -hello hello 다음 홉의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="8ee55-139">**routeTableId** hello 값은 hello 경로와 연결 된 hello 경로 테이블에 대 한 uri 또는 경로의 정의 된 hello 값이 사용자 정의 하지 않는 경우- *시스템 경로* 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="8ee55-140">hello 다음은 hello 결과를 json 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8ee55-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="8ee55-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ee55-141">Next steps</span></span>

<span data-ttu-id="8ee55-142">가상 컴퓨터에 대 한 다음 홉 hello 아웃 수 toofind 되 면 방문 하 여 네트워크 리소스의 보안을 hello를 볼 수 있습니다 [보안 보기 개요](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8ee55-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














