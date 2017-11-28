---
title: "Azure CLI 스크립트 샘플 - VM 네트워크 트래픽 필터링 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 인바운드 및 아웃바운드 VM 네트워크 트래픽을 필터링합니다."
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
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="546b4-103">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="546b4-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="546b4-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="546b4-105">프런트 엔드 서브넷에 대한 인바운드 네트워크 트래픽은 HTTP, HTTPS 및 SSH로 제한되지만, 백 엔드 서브넷에서 인터넷으로의 아웃바운드 트래픽은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="546b4-106">스크립트를 실행한 후에는 두 개의 NIC가 있는 하나의 가상 컴퓨터가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="546b4-107">각 NIC는 서로 다른 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="546b4-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="546b4-108">Sample script</span></span>


<span data-ttu-id="546b4-109">[!code-azurecli-interactive[주](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "VM 네트워크 트래픽 필터링")]</span><span class="sxs-lookup"><span data-stu-id="546b4-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="546b4-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="546b4-110">Clean up deployment</span></span> 

<span data-ttu-id="546b4-111">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="546b4-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="546b4-112">Script explanation</span></span>

<span data-ttu-id="546b4-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="546b4-114">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="546b4-115">명령</span><span class="sxs-lookup"><span data-stu-id="546b4-115">Command</span></span> | <span data-ttu-id="546b4-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="546b4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="546b4-117">az group create</span><span class="sxs-lookup"><span data-stu-id="546b4-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="546b4-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="546b4-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="546b4-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="546b4-120">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="546b4-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="546b4-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="546b4-122">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="546b4-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="546b4-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="546b4-124">NSG를 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="546b4-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="546b4-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="546b4-126">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="546b4-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="546b4-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="546b4-128">가상 네트워크 인터페이스를 만들고 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="546b4-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="546b4-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="546b4-130">프런트 엔드 및 백 엔드 서브넷과 연결되는 NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="546b4-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="546b4-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="546b4-132">특정 포트를 특정 서브넷에 허용하거나 차단하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="546b4-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="546b4-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="546b4-134">가상 컴퓨터를 만들고 각 VM에 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="546b4-135">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="546b4-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="546b4-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="546b4-137">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="546b4-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="546b4-138">Next steps</span></span>

<span data-ttu-id="546b4-139">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="546b4-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="546b4-140">추가 네트워킹 CLI 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="546b4-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>