---
title: "Azure Portal을 사용하여 VM으로 포트 열기 | Microsoft Docs"
description: "Azure 포털의 Resource Manager 배포 모델을 사용하여 Windows VM에 대한 포트를 열고 끝점을 만드는 방법 알아보기"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="91316-103">Azure Portal을 사용하여 가상 컴퓨터에 대한 포털을 여는 방법</span><span class="sxs-lookup"><span data-stu-id="91316-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="91316-104">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="91316-104">Quick commands</span></span>
<span data-ttu-id="91316-105">[Azure PowerShell을 사용하여 수행할 수도 있습니다](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="91316-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="91316-106">먼저 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91316-106">First, create your Network Security Group.</span></span> <span data-ttu-id="91316-107">포털에서 리소스 그룹을 선택하고 **추가**를 선택한 후 **네트워크 보안 그룹**을 검색하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![네트워크 보안 그룹 추가](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="91316-109">네트워크 보안 그룹의 이름을 입력하고, 리소스 그룹을 선택하거나 만들고, 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="91316-110">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-110">Select **Create** when finished:</span></span>

![네트워크 보안 그룹 만들기](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="91316-112">새 네트워크 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-112">Select your new Network Security Group.</span></span> <span data-ttu-id="91316-113">'인바운드 보안 규칙'을 선택한 다음 **추가** 단추를 선택하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91316-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![인바운드 규칙 추가](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="91316-115">드롭다운 메뉴에서 공통 **서비스**를 선택합니다(예: *HTTP*).</span><span class="sxs-lookup"><span data-stu-id="91316-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="91316-116">*사용자 지정*을 선택하여 사용할 특정 포트를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="91316-117">원하는 경우 우선 순위 또는 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-117">If desired, change the priority or name.</span></span> <span data-ttu-id="91316-118">이 우선 순위는 규칙이 적용되는 순서에 영향을 줍니다. 숫자 값이 적을수록 규칙이 먼저 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91316-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="91316-119">이 화면 맨 위에서 **고급**을 선택하여 특정 원본 IP 블록 또는 포트 범위 등을 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="91316-120">준비되면 **확인**을 선택하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91316-120">When you are ready, select **OK** to create the rule:</span></span>

![인바운드 규칙 만들기](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="91316-122">마지막 단계는 네트워크 보안 그룹을 서브넷 또는 특정 네트워크 인터페이스에 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91316-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="91316-123">서브넷에 네트워크 보안 그룹을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="91316-124">**서브넷**을 선택한 후 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-124">Select **Subnets**, then choose **Associate**:</span></span>

![서브넷에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="91316-126">가상 네트워크를 선택하고 적절한 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![가상 네트워킹에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="91316-128">이제 네트워크 보안 그룹을 만들고, 포트 80에서 트래픽을 허용하는 인바운드 규칙을 만들었으며 해당 규칙을 서브넷과 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="91316-129">해당 서브넷에 연결하는 모든 VM은 포트 80에 연결할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91316-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="91316-130">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="91316-130">More information on Network Security Groups</span></span>
<span data-ttu-id="91316-131">여기서 빠른 명령을 사용하면 VM으로 트래픽이 이동되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="91316-132">네트워크 보안 그룹은 리소스에 대한 액세스를 제어하는 많은 기능과 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="91316-133">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="91316-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="91316-134">고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91316-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="91316-135">부하 분산 장치는 트래픽 필터링을 제공하는 네트워크 보안 그룹으로 트래픽을 VM에 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="91316-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="91316-136">자세한 내용은 [Azure의 Linux 가상 컴퓨터 부하를 분산하여 고가용성 응용 프로그램을 만드는 방법](tutorial-load-balancer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91316-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91316-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91316-137">Next steps</span></span>
<span data-ttu-id="91316-138">이 예제에서는 HTTP 트래픽을 허용하는 간단한 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="91316-139">다음 문서에서 보다 자세한 환경을 만들기 위한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91316-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="91316-140">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="91316-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="91316-141">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="91316-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)