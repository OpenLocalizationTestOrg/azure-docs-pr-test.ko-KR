---
title: "Azure Network Watcher IP 흐름 확인을 사용하여 트래픽 확인 - Azure Portal | Microsoft Docs"
description: "이 문서에서는 가상 컴퓨터 간에 트래픽을 허용하는지 아니면 거부하는지를 확인하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f24ce-103">Azure Network Watcher의 구성 요소인 IP 흐름 확인을 사용하여 VM 간에 트래픽을 허용하는지 아니면 거부하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f24ce-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f24ce-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f24ce-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f24ce-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f24ce-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f24ce-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f24ce-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f24ce-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f24ce-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="f24ce-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f24ce-109">IP 흐름 확인은 가상 컴퓨터 간에 트래픽을 허용하는지를 확인할 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="f24ce-110">들어오거나 나가는 트래픽에 대해 유효성 검사를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="f24ce-111">이 시나리오는 가상 컴퓨터가 외부 리소스 또는 다른 리소스에 연결할 수 있는지에 대한 현재 상태를 가져올 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="f24ce-112">IP 흐름 확인은 NSG(네트워크 보안 그룹) 규칙이 모두 제대로 구성되었는지 확인하고 NSG 규칙에 의해 차단되는 흐름 문제를 해결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f24ce-113">IP 흐름 확인을 사용하여 차단하려는 트래픽이 NSG에서 제대로 차단되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f24ce-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f24ce-114">Before you begin</span></span>

<span data-ttu-id="f24ce-115">이 시나리오에서는 사용자가 Network Watcher를 만들거나 Network Watcher의 기존 인스턴스를 가져오는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f24ce-116">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f24ce-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="f24ce-117">Scenario</span></span>

<span data-ttu-id="f24ce-118">이 시나리오에서는 IP 확인 흐름을 사용하여 가상 컴퓨터가 포트 443을 통해 다른 컴퓨터와 통신할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="f24ce-119">트래픽이 거부된 경우 해당 트래픽을 거부하는 보안 규칙을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="f24ce-120">IP 흐름 확인에 대한 자세한 내용을 보려면 [IP 흐름 확인 개요](network-watcher-ip-flow-verify-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ce-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="f24ce-121">IP 흐름 확인 실행</span><span class="sxs-lookup"><span data-stu-id="f24ce-121">Run IP flow verify</span></span>

<span data-ttu-id="f24ce-122">Network Watcher로 이동하고 **IP 흐름 확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="f24ce-123">트래픽을 확인하려는 가상 컴퓨터 및 네트워크 인터페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="f24ce-124">추가 필터링 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="f24ce-125">**확인**을 클릭하면 사용자가 제공한 기준에 따라 흐름이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="f24ce-126">결과는 **액세스 허용됨** 또는 **액세스 거부됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="f24ce-127">액세스가 거부되면 트래픽을 차단하는 NSG(네트워크 보안 그룹) 및 보안 규칙이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="f24ce-128">트래픽 거부가 예상되는 동작인 경우 규칙이 성공한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="f24ce-129">IP 흐름 확인에서는 VM 리소스가 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="f24ce-130">다음 이미지에서 볼 수 있는 것처럼 아웃바운드 HTTPS 트래픽이 허용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![IP 흐름 확인 개요][1]

<span data-ttu-id="f24ce-132">다음 이미지에 표시된 것처럼 트래픽은 인바운드로 변경되고 인바운드 포트는 123으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="f24ce-133">트래픽이 거부되면 트래픽을 거부하는 네트워크 보안 그룹 및 보안 규칙이 함께 "액세스 거부됨" 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![IP 흐름 결과][2]

## <a name="next-steps"></a><span data-ttu-id="f24ce-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f24ce-135">Next steps</span></span>

<span data-ttu-id="f24ce-136">트래픽이 차단되지 않아야 하는데 차단된 경우 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)를 참조하여 정의된 네트워크 보안 그룹 및 보안 규칙을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ce-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













