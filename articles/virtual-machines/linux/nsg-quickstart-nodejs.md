---
title: "aaaOpen 포트 tooa Azure CLI 1.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Linux VM 만들기 / hello Azure 리소스 관리자 배포를 사용 하 여 모델을 hello Azure CLI 1.0"
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
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="db337-103">여는 포트와 끝점 tooa Linux VM에서 사용 하 여 Azure hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="db337-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="db337-104">포트를 열거나 끝점을 만들 tooa (VM) Azure에서 가상 컴퓨터는 서브넷 또는 VM 네트워크 인터페이스에 네트워크 필터를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="db337-105">Hello 트래픽을 수신 하는 연결 된 네트워크 보안 그룹 toohello 리소스에서 인바운드 및 아웃 바운드 트래픽을 제어 하는 데 이러한 필터를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="db337-106">포트 80에서 웹 트래픽의 일반적인 예제를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="db337-107">이 문서에 사용 하 여 포트 tooa VM tooopen Azure CLI 1.0 hello 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="db337-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="db337-108">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="db337-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="db337-109">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="db337-110">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="db337-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="db337-111">[Azure CLI 2.0](nsg-quickstart.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="db337-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="db337-112">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="db337-112">Quick commands</span></span>
<span data-ttu-id="db337-113">toocreate 네트워크 보안 그룹 규칙 필요 하 고 [Azure CLI 1.0 hello](../../cli-install-nodejs.md) 설치 및 사용 하 여 리소스 관리자 모드:</span><span class="sxs-lookup"><span data-stu-id="db337-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="db337-114">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="db337-115">예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db337-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="db337-116">고유한 이름 및 위치를 적절히 입력하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db337-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="db337-117">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="db337-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="db337-118">규칙 tooallow HTTP 트래픽 tooyour 웹 서버를 추가 합니다 (또는 SSH 액세스 또는 데이터베이스 연결 등의 고유한 시나리오에 대 한 조정).</span><span class="sxs-lookup"><span data-stu-id="db337-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="db337-119">hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow TCP 포트 80에서 트래픽을:</span><span class="sxs-lookup"><span data-stu-id="db337-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="db337-120">VM의 네트워크 인터페이스 (NIC) hello 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="db337-121">hello 다음 예제에서는 연결 라는 기존 NIC *myNic* hello 라는 네트워크 보안 그룹으로 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="db337-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="db337-122">또는 바로 toohello 네트워크 인터페이스에는 단일 VM 대신 가상 네트워크 서브넷 네트워크 보안 그룹을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="db337-123">hello 다음 예제에서는 연결 라는 기존 서브넷 *mySubnet* hello에 *myVnet* hello 라는 네트워크 보안 그룹을 사용 하 여 가상 네트워크 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="db337-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="db337-124">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="db337-124">More information on Network Security Groups</span></span>
<span data-ttu-id="db337-125">빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="db337-126">네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="db337-127">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="db337-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="db337-128">네트워크 보안 그룹 및 ACL 규칙을 Azure Resource Manager 템플릿의 일부로 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="db337-129">[템플릿을 사용하여 네트워크 보안 그룹 만들기](../../virtual-network/virtual-networks-create-nsg-arm-template.md)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="db337-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="db337-130">VM에 toouse 포트 전달을 toomap 고유한 외부 포트 tooan 내부 포트를 필요한 경우 부하 분산 장치 및 네트워크 주소 변환 (NAT) 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db337-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="db337-131">예를 들어 수 tooexpose TCP 포트 8080 외부에서 VM에 보내지는 트래픽을 tooTCP 포트 80입니다.</span><span class="sxs-lookup"><span data-stu-id="db337-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="db337-132">[인터넷 연결 부하 분산 장치 만들기](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db337-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db337-133">Next steps</span></span>
<span data-ttu-id="db337-134">이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="db337-135">Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db337-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="db337-136">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="db337-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="db337-137">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="db337-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="db337-138">부하 분산 장치에 대한 Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="db337-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

