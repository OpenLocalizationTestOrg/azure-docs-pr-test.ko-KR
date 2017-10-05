---
title: "Azure CLI 스크립트 샘플 - Azure CLI를 통해 여러 웹 사이트 부하 분산 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 동일한 가상 컴퓨터로 여러 웹 사이트 부하 분산"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="4b61b-103">여러 웹 사이트 부하 분산</span><span class="sxs-lookup"><span data-stu-id="4b61b-103">Load balance multiple websites</span></span>

<span data-ttu-id="4b61b-104">이 스크립트 샘플에서는 가용성 집합의 구성원인 두 개의 VM(가상 컴퓨터)과 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="4b61b-105">부하 분산 장치는 두 VM에 두 개의 별도 IP 주소에 대한 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="4b61b-106">스크립트를 실행한 후 웹 서버 소프트웨어를 VM에 배포하고 여러 웹 사이트를 각각 고유한 IP 주소로 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4b61b-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4b61b-107">Sample script</span></span>


<span data-ttu-id="4b61b-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "여러 웹 사이트 부하 분산")]</span><span class="sxs-lookup"><span data-stu-id="4b61b-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4b61b-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="4b61b-109">Clean up deployment</span></span> 

<span data-ttu-id="4b61b-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="4b61b-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4b61b-111">Script explanation</span></span>

<span data-ttu-id="4b61b-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="4b61b-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4b61b-114">명령</span><span class="sxs-lookup"><span data-stu-id="4b61b-114">Command</span></span> | <span data-ttu-id="4b61b-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4b61b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b61b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="4b61b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4b61b-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b61b-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="4b61b-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="4b61b-119">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="4b61b-120">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="4b61b-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="4b61b-121">고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="4b61b-122">az network lb create</span><span class="sxs-lookup"><span data-stu-id="4b61b-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="4b61b-123">Azure Load Balancer를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="4b61b-124">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="4b61b-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="4b61b-125">부하 분산 장치 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-125">Creates a load balancer probe.</span></span> <span data-ttu-id="4b61b-126">부하 분산 장치 프로브는 부하 분산 장치 집합의 각 VM을 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="4b61b-127">모든 VM이 액세스할 수 없게 되면 트래픽은 VM에 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="4b61b-128">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="4b61b-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="4b61b-129">부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-129">Creates a load balancer rule.</span></span> <span data-ttu-id="4b61b-130">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="4b61b-131">HTTP 트래픽이 부하 분산 장치에 도착하면 부하 분산 장치 집합에서 VM 중 하나인 포트 80에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="4b61b-132">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="4b61b-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="4b61b-133">부하 분산 장치의 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="4b61b-134">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="4b61b-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="4b61b-135">백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="4b61b-136">az network nic create</span><span class="sxs-lookup"><span data-stu-id="4b61b-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="4b61b-137">가상 네트워크 카드를 만들고 가상 네트워크 및 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="4b61b-138">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="4b61b-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="4b61b-139">가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-139">Creates an availability set.</span></span> <span data-ttu-id="4b61b-140">가용성 집합을 사용하면 오류가 발생하는 경우 물리적 리소스 간에 가상 컴퓨터를 분산하여 응용 프로그램 가동 시간을 확인합니다. 전체 집합은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="4b61b-141">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="4b61b-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="4b61b-142">IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-142">Creates an IP confiuration.</span></span> <span data-ttu-id="4b61b-143">구독에서 Microsoft.Network/AllowMultipleIpConfigurationsPerNic 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="4b61b-144">--make-primary 플래그를 사용하여 하나의 구성만 NIC당 기본 IP 구성으로 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="4b61b-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="4b61b-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="4b61b-146">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="4b61b-147">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="4b61b-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="4b61b-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="4b61b-149">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b61b-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b61b-150">Next steps</span></span>

<span data-ttu-id="4b61b-151">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b61b-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4b61b-152">추가 네트워킹 CLI 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b61b-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
