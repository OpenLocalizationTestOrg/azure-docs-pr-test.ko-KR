---
title: "Azure CLI 1.0을 사용하여 Linux VM에 포트 열기 | Microsoft Docs"
description: "Azure Resource Manager 배포 모드 및 Azure CLI 1.0을 사용하여 Linux VM에 대한 포트를 열고 끝점을 만드는 방법 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="89320-103">Azure CLI 1.0을 사용하여 Azure에서 Linux VM에 대한 끝점 및 포트 열기</span><span class="sxs-lookup"><span data-stu-id="89320-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="89320-104">서브넷 또는 VM 네트워크 인터페이스에서 네트워크 필터를 만들어, Azure에서 VM(가상 컴퓨터)에 대한 포트를 열거나 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89320-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="89320-105">인바운드 및 아웃바운드 트래픽을 모두 제어하는 이러한 필터를 트래픽을 수신하는 리소스에 연결된 네트워크 보안 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="89320-106">포트 80에서 웹 트래픽의 일반적인 예제를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="89320-107">이 문서는 Azure CLI 1.0을 사용하여 VM에 포트를 여는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="89320-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="89320-108">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="89320-108">CLI versions to complete the task</span></span>
<span data-ttu-id="89320-109">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="89320-110">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="89320-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="89320-111">[Azure CLI 2.0](nsg-quickstart.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="89320-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="89320-112">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="89320-112">Quick commands</span></span>
<span data-ttu-id="89320-113">네트워크 보안 그룹과 규칙을 만들려면 [Azure CLI 1.0](../../cli-install-nodejs.md)이 설치되어 있어야 하고 다음과 같은 Resource Manager 모드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="89320-114">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89320-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="89320-115">예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="89320-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="89320-116">고유한 이름 및 위치를 적절히 입력하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89320-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="89320-117">다음 예제에서는 *eastus* 위치에 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89320-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="89320-118">웹 서버에 대한 HTTP 트래픽을 허용하는 규칙을 추가하거나 SSH 액세스 또는 데이터베이스 연결 등 사용자 고유의 시나리오에 맞게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="89320-119">다음 예제에서는 포트 80의 TCP 트래픽을 허용하도록 *myNetworkSecurityGroupRule*이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89320-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="89320-120">네트워크 보안 그룹을 VM의 네트워크 인터페이스(NIC)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="89320-121">다음 예제에서는 *myNic*라는 기존 NIC를 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="89320-122">또는 네트워크 보안 그룹을 단일 VM의 네트워크 인터페이스가 아니라 가상 네트워크 서브넷에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="89320-123">다음 예제에서는 *myVnet* 가상 네트워크에 있는 *mySubnet*이라는 기존 서브넷을 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="89320-124">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="89320-124">More information on Network Security Groups</span></span>
<span data-ttu-id="89320-125">여기서 빠른 명령을 사용하면 VM으로 트래픽이 이동되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="89320-126">네트워크 보안 그룹은 리소스에 대한 액세스를 제어하는 많은 기능과 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="89320-127">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="89320-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="89320-128">네트워크 보안 그룹 및 ACL 규칙을 Azure Resource Manager 템플릿의 일부로 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="89320-129">[템플릿을 사용하여 네트워크 보안 그룹 만들기](../../virtual-network/virtual-networks-create-nsg-arm-template.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="89320-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="89320-130">포트 전달을 사용하여 고유한 외부 포트를 VM의 내부 포트에 매핑해야 하는 경우 부하 분산 장치 및 NAT(네트워크 주소 변환) 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89320-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="89320-131">예를 들어 TCP 포트 8080을 외부에 노출하고 트래픽이 VM의 TCP 포트 80으로 전달되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="89320-132">[인터넷 연결 부하 분산 장치 만들기](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89320-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89320-133">Next steps</span></span>
<span data-ttu-id="89320-134">이 예제에서는 HTTP 트래픽을 허용하는 간단한 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="89320-135">다음 문서에서 보다 자세한 환경을 만들기 위한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89320-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="89320-136">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="89320-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="89320-137">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="89320-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="89320-138">부하 분산 장치에 대한 Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="89320-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

