---
title: "aaaAzure CLI 스크립트 샘플 네트워크 가상 어플라이언스를 통해 트래픽 라우팅할 | Microsoft Docs"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="2f6b0-103">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="2f6b0-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="2f6b0-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="2f6b0-105">또한 hello 두 서브넷 활성화 tooroute 트래픽을 전달 하는 ip는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="2f6b0-106">Hello 스크립트를 실행 한 후 toohello VM 방화벽 응용 프로그램 등의 네트워크 소프트웨어를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="2f6b0-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2f6b0-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2f6b0-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="2f6b0-108">Clean up deployment</span></span> 

<span data-ttu-id="2f6b0-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2f6b0-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2f6b0-110">Script explanation</span></span>

<span data-ttu-id="2f6b0-111">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="2f6b0-112">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="2f6b0-113">명령</span><span class="sxs-lookup"><span data-stu-id="2f6b0-113">Command</span></span> | <span data-ttu-id="2f6b0-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2f6b0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f6b0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2f6b0-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f6b0-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="2f6b0-118">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="2f6b0-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="2f6b0-120">백 엔드 및 DMZ 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="2f6b0-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="2f6b0-122">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="2f6b0-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="2f6b0-124">가상 네트워크 인터페이스를 만들고 이 인터페이스를 위해 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="2f6b0-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="2f6b0-126">NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="2f6b0-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="2f6b0-128">HTTP 및 HTTPS 포트를 인바운드 toohello VM을 허용 하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="2f6b0-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="2f6b0-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="2f6b0-130">Associates Nsg hello 및 경로 toosubnets 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="2f6b0-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="2f6b0-132">모든 경로에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="2f6b0-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="2f6b0-134">서브넷 및 VM hello 통해 인터넷 hello 간의 tooroute 트래픽 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="2f6b0-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="2f6b0-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="2f6b0-136">가상 컴퓨터를 만들고 hello NIC tooit 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="2f6b0-137">이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="2f6b0-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="2f6b0-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="2f6b0-139">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f6b0-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2f6b0-140">Next steps</span></span>

<span data-ttu-id="2f6b0-141">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f6b0-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="2f6b0-142">추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="2f6b0-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
