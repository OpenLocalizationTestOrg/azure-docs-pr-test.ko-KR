---
title: "aaaUse VM에 대 한 내부 DNS 이름 확인 Azure CLI 2.0 hello로 | Microsoft Docs"
description: "Toocreate 가상 네트워크 인터페이스 카드 하 고 Azure CLI 2.0 hello로 Azure에서 VM 이름 확인에 대 한 내부 DNS를 사용 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="f2428-103">가상 네트워크 인터페이스 카드 만들기 및 Azure에서 VM 이름 확인을 위해 내부 DNS 사용</span><span class="sxs-lookup"><span data-stu-id="f2428-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="f2428-104">이 문서 tooset 정적 내부 DNS 이름을 사용 하 여 가상 Linux Vm에 대 한 네트워크 인터페이스 카드 (vNics) 및 Azure CLI 2.0 hello로 DNS 레이블 이름의 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="f2428-105">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f2428-106">정적 DNS 이름은 이 문서에서 사용되는 Jenkins 빌드 서버 또는 Git 서버와 같은 영구 인프라 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="f2428-107">hello 요구 사항은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-107">hello requirements are:</span></span>

* [<span data-ttu-id="f2428-108">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="f2428-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="f2428-109">SSH 공용 및 개인 키 파일</span><span class="sxs-lookup"><span data-stu-id="f2428-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="f2428-110">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="f2428-110">Quick commands</span></span>
<span data-ttu-id="f2428-111">Hello 작업을 수행를 tooquickly가 필요한 경우 다음 단원을 hello 필요한 hello 명령에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="f2428-112">각 단계는 hello 나머지 hello 문서에서에서 확인할 수 있습니다에 대 한 정보와 컨텍스트 상세 [여기 시작](#detailed-walkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="f2428-113">이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f2428-114">사전 요구 사항: 리소스 그룹, 가상 네트워크 및 서브넷, SSH 인바운드가 있는 네트워크 보안 그룹.</span><span class="sxs-lookup"><span data-stu-id="f2428-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="f2428-115">정적 내부 DNS 이름을 가진 가상 네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="f2428-116">만들기와 hello vNic [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="f2428-117">hello `--internal-dns-name` CLI 플래그는 hello hello 가상 네트워크 인터페이스 카드 (vNic)에 대 한 정적 DNS 이름을 제공 하는 설정 hello DNS 레이블에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="f2428-118">hello 다음 예제에서는 명명 된 vNic `myNic`, toohello 연결 `myVnet` 가상 네트워크를 호출 하는 내부 DNS 이름 레코드를 만듭니다 `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="f2428-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="f2428-119">VM을 배포 하 고 hello vNic 연결</span><span class="sxs-lookup"><span data-stu-id="f2428-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="f2428-120">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f2428-121">hello `--nics` hello 배포 tooAzure 중 hello vNic toohello VM을 연결 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="f2428-122">hello 다음 예제에서는 V `myVM` Azure 관리 되는 디스크와 연결 합니다. hello vNic 라는 `myNic` hello 앞 단계에서에서:</span><span class="sxs-lookup"><span data-stu-id="f2428-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f2428-123">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="f2428-123">Detailed walkthrough</span></span>

<span data-ttu-id="f2428-124">전체 연속 통합 및 연속 배포 (CiCd) 인프라를 Azure에서 특정 서버 toobe 정적 또는 수명이 긴 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="f2428-125">가상 네트워크 및 네트워크 보안 그룹 hello와 같은 Azure 자산 정적 이며 거의 배포 되는 리소스를 수명이 긴 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="f2428-126">가상 네트워크에 배포한 후에 부정적인 영향을 줌 toohello 인프라 없이 새 배포 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="f2428-127">Git 리포지토리 서버를 나중에 추가할 수 있습니다 또는 Jenkins 자동화 서버 CiCd toothis 개발 또는 테스트 환경에 대 한 가상 네트워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="f2428-128">내부 DNS 이름은 Azure Virtual Network 내에서만 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="f2428-129">Hello DNS 이름은 내부에 있으므로 추가 보안 toohello 인프라를 제공 하는 인터넷 외부 확인할 toohello 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="f2428-130">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f2428-131">예제 매개 변수 이름에 `myResourceGroup`, `myNic` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="f2428-132">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-132">Create hello resource group</span></span>
<span data-ttu-id="f2428-133">Hello 리소스 그룹을 먼저 만듭니다 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f2428-134">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치:</span><span class="sxs-lookup"><span data-stu-id="f2428-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="f2428-135">Hello 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-135">Create hello virtual network</span></span>

<span data-ttu-id="f2428-136">hello 다음 단계에는 가상 네트워크 toolaunch hello에 대 한 Vm toobuild입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="f2428-137">이 연습에서는 한 서브넷을 포함 하는 hello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="f2428-138">Azure 가상 네트워크에 대 한 자세한 내용은 참조 하십시오. [hello Azure CLI를 사용 하 여 가상 네트워크를 만들](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="f2428-139">Hello 가상 네트워크를 만듭니다 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="f2428-140">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 `myVnet` 와 명명 된 서브넷 `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="f2428-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="f2428-141">Hello 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-141">Create hello Network Security Group</span></span>
<span data-ttu-id="f2428-142">Azure 네트워크 보안 그룹은 hello 네트워크 계층에서 해당 tooa 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="f2428-143">네트워크 보안 그룹에 대 한 자세한 내용은 참조 [어떻게 toocreate Nsg에 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="f2428-144">Hello 네트워크 보안 그룹을 만들 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="f2428-145">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="f2428-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="f2428-146">SSH는 인바운드 규칙 tooallow 추가</span><span class="sxs-lookup"><span data-stu-id="f2428-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="f2428-147">네트워크 보안 그룹을 hello에 대 한 인바운드 규칙 추가 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="f2428-148">hello 다음 예제는 규칙을 만들고 라는 `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="f2428-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="f2428-149">Hello 서브넷 hello 네트워크 보안 그룹을 연결</span><span class="sxs-lookup"><span data-stu-id="f2428-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="f2428-150">tooassociate hello 서브넷 hello 네트워크 보안 그룹을 사용 하 여 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="f2428-151">hello 다음 예제에서는 연결 hello 서브넷 이름 `mySubnet` 네트워크 보안 그룹 이라는 hello로 `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="f2428-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="f2428-152">Hello 가상 네트워크 인터페이스 카드를 만들고 정적 DNS 이름</span><span class="sxs-lookup"><span data-stu-id="f2428-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="f2428-153">Azure는 매우 유연한 방법 이지만 toocreate 가상 네트워크 인터페이스 카드 (vNics) DNS 레이블을 포함 하는 필요한 VM 이름 확인에 대 한 DNS 이름을 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="f2428-154">vNics는 다시 사용할 수 있습니다에 연결 하 여 toodifferent Vm hello 인프라가 수명 주기에 대 때 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="f2428-155">이 방법은 hello Vm 말할 수 하는 동안 정적 리소스로 hello vNic를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="f2428-156">Hello vNic에 레이블을 지정 하는 DNS를 사용 하 여 hello VNet의에서 다른 Vm에서 간단한 이름 확인을 tooenable 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="f2428-157">Hello DNS 이름으로 다른 Vm tooaccess hello 자동화 서버를 사용 하면 확인할 수 있는 이름을 사용 하 여 `Jenkins` 또는 Git 서버 hello `gitrepo`합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="f2428-158">만들기와 hello vNic [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="f2428-159">hello 다음 예제에서는 명명 된 vNic `myNic`, toohello 연결 `myVnet` 이라는 가상 네트워크 `myVnet`를 호출 하는 내부 DNS 이름 레코드를 만듭니다 `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="f2428-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="f2428-160">Hello VM hello 가상 네트워크 인프라에 배포</span><span class="sxs-lookup"><span data-stu-id="f2428-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="f2428-161">했습니다 가상 네트워크 및 서브넷에 역할을 하는 방화벽 tooprotect 우리의 서브넷 SSH, 및 vNic에 대 한 포트 22 제외한 모든 인바운드 트래픽 차단 하 여 네트워크 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="f2428-162">이제 이 기존 네트워크 인프라 내에 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="f2428-163">[az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f2428-164">hello 다음 예제에서는 V `myVM` Azure 관리 되는 디스크와 연결 합니다. hello vNic 라는 `myNic` hello 앞 단계에서에서:</span><span class="sxs-lookup"><span data-stu-id="f2428-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="f2428-165">CLI 플래그는 hello를 사용 하 여 기존 리소스를 toocall hello 기존 네트워크 내부 Azure toodeploy hello VM 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="f2428-166">tooreiterate, VNet 및 서브넷에 배포 된 후 있습니다 수로 유지 되 Azure 지역이 내부 정적 지, 영구적인 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2428-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f2428-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2428-167">Next steps</span></span>
* [<span data-ttu-id="f2428-168">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f2428-169">템플릿을 사용하여 Azure에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="f2428-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
