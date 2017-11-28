---
title: "Azure CLI 스크립트 샘플 - 네트워크 가상 어플라이언스를 통한 트래픽 라우팅 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 방화벽 네트워크 가상 어플라이언스를 통해 트래픽을 라우팅합니다."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="9d269-103">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="9d269-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="9d269-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9d269-105">또한 두 서브넷 간에 트래픽을 라우팅할 수 있게 하는 IP 전달을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="9d269-106">스크립트를 실행한 후에 방화벽 응용 프로그램과 같은 네트워크 소프트웨어를 VM에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="9d269-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="9d269-107">Sample script</span></span>


<span data-ttu-id="9d269-108">[!code-azurecli-interactive[주](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "네트워크 가상 어플라이언스를 통한 트래픽 라우팅")]</span><span class="sxs-lookup"><span data-stu-id="9d269-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9d269-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="9d269-109">Clean up deployment</span></span> 

<span data-ttu-id="9d269-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9d269-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="9d269-111">Script explanation</span></span>

<span data-ttu-id="9d269-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="9d269-113">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="9d269-114">명령</span><span class="sxs-lookup"><span data-stu-id="9d269-114">Command</span></span> | <span data-ttu-id="9d269-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9d269-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d269-116">az group create</span><span class="sxs-lookup"><span data-stu-id="9d269-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="9d269-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d269-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="9d269-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="9d269-119">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="9d269-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="9d269-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="9d269-121">백 엔드 및 DMZ 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="9d269-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="9d269-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="9d269-123">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="9d269-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="9d269-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="9d269-125">가상 네트워크 인터페이스를 만들고 이 인터페이스를 위해 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="9d269-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="9d269-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="9d269-127">NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="9d269-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="9d269-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="9d269-129">VM에 대한 인바운드 HTTP 및 HTTPS 포트를 허용하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="9d269-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="9d269-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="9d269-131">NSG 및 경로 테이블을 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="9d269-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="9d269-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="9d269-133">모든 경로에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="9d269-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="9d269-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="9d269-135">VM을 통해 서브넷과 인터넷 간 트래픽을 라우팅하는 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="9d269-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="9d269-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="9d269-137">가상 컴퓨터를 만들고 NIC를 이 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="9d269-138">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="9d269-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="9d269-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="9d269-140">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d269-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d269-141">Next steps</span></span>

<span data-ttu-id="9d269-142">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d269-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="9d269-143">추가 네트워킹 CLI 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d269-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>