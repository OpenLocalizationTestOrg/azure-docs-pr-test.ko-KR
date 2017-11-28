---
title: "aaaOpen 포트 tooa Azure CLI 2.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Linux VM 만들기 / hello Azure 리소스 관리자 배포를 사용 하 여 모델을 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="c701f-103">Hello Azure CLI가 있는 포트와 끝점 tooa Linux VM을 열려면</span><span class="sxs-lookup"><span data-stu-id="c701f-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="c701f-104">포트를 열거나 끝점을 만들 tooa (VM) Azure에서 가상 컴퓨터는 서브넷 또는 VM 네트워크 인터페이스에 네트워크 필터를 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="c701f-105">Hello 트래픽을 수신 하는 연결 된 네트워크 보안 그룹 toohello 리소스에서 인바운드 및 아웃 바운드 트래픽을 제어 하는 데 이러한 필터를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="c701f-106">포트 80에서 웹 트래픽의 일반적인 예제를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="c701f-107">이 문서에서는 Azure CLI 2.0 hello로 포트 tooa VM tooopen 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="c701f-108">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](nsg-quickstart-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="c701f-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="c701f-109">Quick commands</span></span>
<span data-ttu-id="c701f-110">toocreate 네트워크 보안 그룹 및 규칙 필요한 최신 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c701f-111">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c701f-112">예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="c701f-113">Hello 네트워크 보안 그룹을 만들 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="c701f-114">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="c701f-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="c701f-115">사용 하 여 규칙을 추가할 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 트래픽 tooyour 웹 서버 (또는 SSH 액세스 또는 데이터베이스 연결 등의 고유한 시나리오에 대 한 조정) tooallow HTTP입니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="c701f-116">hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow TCP 포트 80에서 트래픽을:</span><span class="sxs-lookup"><span data-stu-id="c701f-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="c701f-117">VM의 네트워크 인터페이스 (NIC)와 hello 네트워크 보안 그룹 연결 [az 네트워크 nic 업데이트](/cli/azure/network/nic#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="c701f-118">hello 다음 예제에서는 연결 라는 기존 NIC *myNic* hello 라는 네트워크 보안 그룹으로 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c701f-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="c701f-119">또는 네트워크 보안 그룹 사용 하 여 가상 네트워크 서브넷과 연결할 수 있습니다 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update) 방금 toohello 네트워크 인터페이스에는 단일 VM 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="c701f-120">hello 다음 예제에서는 연결 라는 기존 서브넷 *mySubnet* hello에 *myVnet* hello 라는 네트워크 보안 그룹을 사용 하 여 가상 네트워크 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c701f-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="c701f-121">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="c701f-121">More information on Network Security Groups</span></span>
<span data-ttu-id="c701f-122">빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="c701f-123">네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="c701f-124">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](tutorial-virtual-network.md#secure-network-traffic)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c701f-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="c701f-125">고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="c701f-126">hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="c701f-127">자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c701f-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c701f-128">Next steps</span></span>
<span data-ttu-id="c701f-129">이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="c701f-130">Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c701f-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="c701f-131">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="c701f-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="c701f-132">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="c701f-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
