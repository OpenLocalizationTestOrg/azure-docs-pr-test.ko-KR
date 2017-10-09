---
title: "Azure 포털 hello aaaOpen 포트 tooa 사용 하 여 VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Windows VM을 만들 / hello 리소스 관리자 배포 모델을 사용 하 여 hello Azure 포털에서"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="b5c48-103">Tooopen은 tooa hello Azure 포털 사용 하는 가상 컴퓨터 포트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="b5c48-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="b5c48-104">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="b5c48-104">Quick commands</span></span>
<span data-ttu-id="b5c48-105">[Azure PowerShell을 사용하여 수행할 수도 있습니다](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5c48-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="b5c48-106">먼저 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-106">First, create your Network Security Group.</span></span> <span data-ttu-id="b5c48-107">Hello 포털에서 리소스 그룹을 선택, 선택 **추가**다음 검색 하 고 선택 **네트워크 보안 그룹**:</span><span class="sxs-lookup"><span data-stu-id="b5c48-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![네트워크 보안 그룹 추가](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="b5c48-109">네트워크 보안 그룹의 이름을 입력하고, 리소스 그룹을 선택하거나 만들고, 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="b5c48-110">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-110">Select **Create** when finished:</span></span>

![네트워크 보안 그룹 만들기](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="b5c48-112">새 네트워크 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-112">Select your new Network Security Group.</span></span> <span data-ttu-id="b5c48-113">'인바운드 보안 규칙'를 선택 하 고 hello 선택 **추가** 단추 toocreate 규칙:</span><span class="sxs-lookup"><span data-stu-id="b5c48-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![인바운드 규칙 추가](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="b5c48-115">공통 선택 **서비스** hello 드롭 다운 메뉴에서와 같은 *HTTP*합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="b5c48-116">선택할 수도 있습니다 *사용자 지정* tooprovide 특정 포트 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="b5c48-117">원하는 경우 hello 우선 순위 또는 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="b5c48-118">hello 우선 순위에 영향을 hello 순서-규칙이 적용 되는 hello 숫자 값이 낮을수록 hello hello 이전 hello 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="b5c48-119">선택할 수도 있습니다 **고급** 특정 hello 위쪽이 화면 tooenter에 IP 블록 또는 포트 범위 예를 들어 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="b5c48-120">준비 되 면 선택 **확인** toocreate hello 규칙:</span><span class="sxs-lookup"><span data-stu-id="b5c48-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![인바운드 규칙 만들기](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="b5c48-122">마지막 단계는 tooassociate 서브넷 또는 특정 네트워크 인터페이스를 네트워크 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="b5c48-123">서브넷과 hello 네트워크 보안 그룹을 연결 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="b5c48-124">**서브넷**을 선택한 후 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-124">Select **Subnets**, then choose **Associate**:</span></span>

![서브넷에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="b5c48-126">가상 네트워크를 선택 하 고 hello 적절 한 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![가상 네트워킹에 네트워크 보안 그룹 연결](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="b5c48-128">이제 네트워크 보안 그룹을 만들고, 포트 80에서 트래픽을 허용하는 인바운드 규칙을 만들었으며 해당 규칙을 서브넷과 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="b5c48-129">Toothat 서브넷 연결 모든 Vm은 포트 80에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="b5c48-130">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="b5c48-130">More information on Network Security Groups</span></span>
<span data-ttu-id="b5c48-131">빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="b5c48-132">네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="b5c48-133">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="b5c48-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="b5c48-134">고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="b5c48-135">hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="b5c48-136">자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5c48-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b5c48-137">Next steps</span></span>
<span data-ttu-id="b5c48-138">이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="b5c48-139">Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c48-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="b5c48-140">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="b5c48-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="b5c48-141">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="b5c48-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)