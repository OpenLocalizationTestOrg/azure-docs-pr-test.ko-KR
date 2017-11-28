---
title: "Azure 네트워크 감시자 IP 흐름 확인-Azure CLI aaaVerify 트래픽 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocheck 가상 컴퓨터에서 트래픽 tooor 허용 또는 Azure CLI를 사용 하 여 거부 된 경우"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="2a655-103">트래픽은 허용 되거나 Azure 네트워크 감시자의 구성 요소는 VM과 IP 확인 흐름에서 tooor을 거부 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2a655-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2a655-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="2a655-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a655-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="2a655-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2a655-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="2a655-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2a655-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="2a655-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="2a655-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="2a655-109">IP 흐름은 tooor 가상 컴퓨터에서 트래픽을 허용 하는 경우 tooverify 수 있는 네트워크 감시자의 기능 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="2a655-110">이 시나리오는 유용한 tooget tooan 외부 리소스 또는 백 엔드 가상 컴퓨터를 서로 연결할 수 있는지 여부의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="2a655-111">IP 흐름 보안 그룹 NSG (네트워크) 규칙에 올바르게 구성 되어 NSG 규칙에 의해 차단 되는 흐름 문제를 해결 하는 경우 사용 되는 tooverify 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="2a655-112">IP를 사용 하는 또 다른 이유 흐름 tooensure 트래픽이 차단 되도록 제대로 hello NSG 차단 하 고이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="2a655-113">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a655-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2a655-114">Before you begin</span></span>

<span data-ttu-id="2a655-115">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 네트워크 감시자의 기존 인스턴스가 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="2a655-116">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2a655-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="2a655-117">Scenario</span></span>

<span data-ttu-id="2a655-118">이 시나리오는 가상 컴퓨터 수와 통신 tooa 알려진 경우 IP 확인 흐름 tooverify 사용 하 여 Bing IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="2a655-119">Hello 트래픽이 거부 되 면 해당 트래픽을 거부 하는 hello 보안 규칙을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="2a655-120">IP 확인 흐름에 대 한 자세한 toolearn 방문 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2a655-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="2a655-121">VM 확인</span><span class="sxs-lookup"><span data-stu-id="2a655-121">Get a VM</span></span>

<span data-ttu-id="2a655-122">IP 흐름에서의 원격 대상에서 가상 컴퓨터 tooor IP 주소를 트래픽 tooor 테스트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="2a655-123">가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="2a655-124">가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="2a655-125">Hello NIC 가져오기</span><span class="sxs-lookup"><span data-stu-id="2a655-125">Get hello NICS</span></span>

<span data-ttu-id="2a655-126">hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때.</span><span class="sxs-lookup"><span data-stu-id="2a655-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="2a655-127">원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="2a655-128">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="2a655-128">Run IP flow verify</span></span>

<span data-ttu-id="2a655-129">Hello 았 hello 정보 toorun hello 필요한 cmdlet을 실행할 `network watcher ip-flow-verify` cmdlet tootest hello 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="2a655-130">이 예제에서 사용 하 여 첫 번째 IP 주소가 hello hello 첫 번째 NIC에서</span><span class="sxs-lookup"><span data-stu-id="2a655-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="2a655-131">IP 흐름 hello VM 리소스 toorun가 할당 되는 필요한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="2a655-132">결과 검토</span><span class="sxs-lookup"><span data-stu-id="2a655-132">Review Results</span></span>

<span data-ttu-id="2a655-133">실행 된 후 `network watcher ip-flow-verify` hello 다음 예제는 hello 앞 단계에서에서 반환 된 hello 결과, hello 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="2a655-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a655-134">Next steps</span></span>

<span data-ttu-id="2a655-135">트래픽을 차단 하지 않아야 하는 경우 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello 네트워크 보안 그룹 및 보안 정의 된 규칙을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="2a655-136">방문 하 여 tooaudit NSG 설정을 알아봅니다 [감사 보안 그룹 NSG (네트워크)와 네트워크 감시자](network-watcher-nsg-auditing-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a655-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
