---
title: "Azure Network Watcher IP 흐름 확인을 사용하여 트래픽 확인 - Azure CLI | Microsoft Docs"
description: "이 문서에서는 Azure CLI를 사용하여 가상 컴퓨터 간에 트래픽을 허용하는지 아니면 거부하는지를 확인하는 방법을 설명합니다."
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
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="8bd5f-103">Azure Network Watcher의 구성 요소인 IP 흐름 확인을 사용하여 VM 간에 트래픽을 허용하는지 아니면 거부하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8bd5f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8bd5f-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="8bd5f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd5f-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="8bd5f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8bd5f-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="8bd5f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8bd5f-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="8bd5f-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="8bd5f-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="8bd5f-109">IP 흐름 확인은 가상 컴퓨터 간에 트래픽을 허용하는지를 확인할 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="8bd5f-110">이 시나리오는 가상 컴퓨터가 외부 리소스 또는 백 엔드에 연결할 수 있는지에 대한 현재 상태를 가져올 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="8bd5f-111">IP 흐름 확인은 NSG(네트워크 보안 그룹) 규칙이 모두 제대로 구성되었는지 확인하고 NSG 규칙에 의해 차단되는 흐름 문제를 해결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="8bd5f-112">IP 흐름 확인을 사용하여 차단하려는 트래픽이 NSG에서 제대로 차단되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="8bd5f-113">이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8bd5f-114">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8bd5f-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8bd5f-115">Before you begin</span></span>

<span data-ttu-id="8bd5f-116">이 시나리오에서는 사용자가 Network Watcher를 만들거나 Network Watcher의 기존 인스턴스를 가져오는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="8bd5f-117">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8bd5f-118">시나리오</span><span class="sxs-lookup"><span data-stu-id="8bd5f-118">Scenario</span></span>

<span data-ttu-id="8bd5f-119">이 시나리오에서는 IP 확인 흐름을 사용하여 가상 컴퓨터가 알려진 Bing IP 주소에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="8bd5f-120">트래픽이 거부된 경우 해당 트래픽을 거부하는 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="8bd5f-121">IP 흐름 확인에 대한 자세한 내용을 보려면 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="8bd5f-122">VM 확인</span><span class="sxs-lookup"><span data-stu-id="8bd5f-122">Get a VM</span></span>

<span data-ttu-id="8bd5f-123">IP 흐름 확인은 원격 대상 간에 가상 컴퓨터의 트래픽 또는 IP 주소를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="8bd5f-124">가상 컴퓨터의 ID가 cmdlet에 대해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="8bd5f-125">사용할 가상 컴퓨터의 ID를 이미 알고 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="8bd5f-126">NIC 가져오기</span><span class="sxs-lookup"><span data-stu-id="8bd5f-126">Get the NICS</span></span>

<span data-ttu-id="8bd5f-127">가상 컴퓨터에 있는 NIC의 IP 주소가 필요합니다. 이 예제에서는 가상 컴퓨터의 NIC를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="8bd5f-128">가상 컴퓨터에서 테스트하려는 IP 주소를 이미 알고 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="8bd5f-129">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="8bd5f-129">Run IP flow verify</span></span>

<span data-ttu-id="8bd5f-130">이제 cmdlet을 실행하는 데 필요한 정보가 있으므로 `az network watcher test-ip-flow` cmdlet을 실행하여 트래픽을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="8bd5f-131">이 예제에서는 첫 번째 NIC에 있는 첫 번째 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="8bd5f-132">IP 흐름 확인에서는 VM 리소스가 실행되기 위해 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="8bd5f-133">결과 검토</span><span class="sxs-lookup"><span data-stu-id="8bd5f-133">Review Results</span></span>

<span data-ttu-id="8bd5f-134">다음 예제는 결과가 반환된 `az network watcher test-ip-flow`을 실행한 후에 이전 단계에서 반환된 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="8bd5f-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bd5f-135">Next steps</span></span>

<span data-ttu-id="8bd5f-136">트래픽이 차단되지 않아야 하는데 차단된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 정의된 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="8bd5f-137">[Network Watcher를 사용하여 NSG(네트워크 보안 그룹) 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 NSG 설정을 감사하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8bd5f-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
