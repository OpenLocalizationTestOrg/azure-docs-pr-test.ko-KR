---
title: "CLI 스크립트 샘플-aaaAzure 부하를 분산 hello Azure CLI로 여러 웹 사이트 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-을 부하 분산 여러 웹 사이트 toohello 동일한 가상 컴퓨터"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="c4cea-103">여러 웹 사이트 부하 분산</span><span class="sxs-lookup"><span data-stu-id="c4cea-103">Load balance multiple websites</span></span>

<span data-ttu-id="c4cea-104">이 스크립트 샘플에서는 가용성 집합의 구성원인 두 개의 VM(가상 컴퓨터)과 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="c4cea-105">부하 분산 장치에 대 한 두 개의 별도 트래픽을 전송 IP 주소 2 toohello Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="c4cea-106">Hello 스크립트를 실행 한 후 웹 서버 소프트웨어 toohello Vm을 배포 하 고 각각 자체 IP 주소를 가진 여러 웹 사이트를 호스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c4cea-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c4cea-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4cea-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c4cea-108">Clean up deployment</span></span> 

<span data-ttu-id="c4cea-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c4cea-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c4cea-110">Script explanation</span></span>

<span data-ttu-id="c4cea-111">이 스크립트 명령 toocreate 리소스 그룹에서 가상 네트워크 부하 분산 장치, 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="c4cea-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4cea-113">명령</span><span class="sxs-lookup"><span data-stu-id="c4cea-113">Command</span></span> | <span data-ttu-id="c4cea-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c4cea-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4cea-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c4cea-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c4cea-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c4cea-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="c4cea-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="c4cea-118">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="c4cea-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="c4cea-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="c4cea-120">고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="c4cea-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="c4cea-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="c4cea-122">Azure Load Balancer를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="c4cea-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="c4cea-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="c4cea-124">부하 분산 장치 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-124">Creates a load balancer probe.</span></span> <span data-ttu-id="c4cea-125">부하 분산 장치 검색은 사용 되는 toomonitor hello 부하 분산 장치 집합의 각 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="c4cea-126">모든 VM에 액세스할 수 없게 됩니다, 트래픽 라우팅된 toohello VM 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="c4cea-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="c4cea-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="c4cea-128">부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-128">Creates a load balancer rule.</span></span> <span data-ttu-id="c4cea-129">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="c4cea-130">HTTP 트래픽을 hello 부하 분산 장치에 도착 하면 때 라우트된 tooport 80 hello 부하 분산 장치 집합의 hello Vm 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="c4cea-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="c4cea-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="c4cea-132">Hello 부하 분산 장치에 대 한 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="c4cea-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="c4cea-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="c4cea-134">백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="c4cea-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="c4cea-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="c4cea-136">가상 네트워크 카드를 만들고 toohello 가상 네트워크 및 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="c4cea-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="c4cea-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="c4cea-138">가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-138">Creates an availability set.</span></span> <span data-ttu-id="c4cea-139">가용성 집합으로 오류가 발생 하면 전체 집합 hello 영향을 받지 않습니다 되도록 hello 가상 컴퓨터는 실제 리소스 분배 하 여 응용 프로그램의 가동 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="c4cea-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="c4cea-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="c4cea-141">IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-141">Creates an IP confiuration.</span></span> <span data-ttu-id="c4cea-142">Hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic 기능을 구독에 대해 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="c4cea-143">하나의 구성만 hello-기본 편집기로 지정 플래그를 사용 하 여 NIC 당 기본 IP 구성 hello로 지정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="c4cea-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="c4cea-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="c4cea-145">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c4cea-146">이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="c4cea-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="c4cea-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c4cea-148">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4cea-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4cea-149">Next steps</span></span>

<span data-ttu-id="c4cea-150">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c4cea-151">추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4cea-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
