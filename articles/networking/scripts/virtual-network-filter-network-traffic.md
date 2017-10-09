---
title: "aaaAzure CLI 스크립트 샘플 필터 VM 네트워크 트래픽 | Microsoft Docs"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="13950-103">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="13950-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="13950-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="13950-105">인바운드 네트워크 트래픽을 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP, HTTPS 및 SSH, 동안 아웃 바운드 트래픽을 toohello hello 백 엔드 서브넷에서 인터넷을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13950-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="13950-106">Hello 스크립트를 실행 한 후 두 개의 Nic 하나의 가상 컴퓨터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="13950-107">각 NIC가 연결 된 tooa 다른 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="13950-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="13950-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="13950-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="13950-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="13950-109">Clean up deployment</span></span> 

<span data-ttu-id="13950-110">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="13950-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="13950-111">Script explanation</span></span>

<span data-ttu-id="13950-112">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="13950-113">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="13950-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="13950-114">명령</span><span class="sxs-lookup"><span data-stu-id="13950-114">Command</span></span> | <span data-ttu-id="13950-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="13950-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="13950-116">az group create</span><span class="sxs-lookup"><span data-stu-id="13950-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="13950-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="13950-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="13950-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="13950-119">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="13950-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="13950-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="13950-121">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="13950-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="13950-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="13950-123">Toosubnets Nsg를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="13950-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="13950-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="13950-125">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="13950-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="13950-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="13950-127">가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="13950-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="13950-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="13950-129">네트워크 보안 그룹 (NSG) 관련된 toohello 프런트 엔드 및 백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="13950-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="13950-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="13950-131">NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13950-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="13950-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="13950-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="13950-133">가상 컴퓨터를 만들고 NIC tooeach VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="13950-134">이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="13950-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="13950-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="13950-136">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13950-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13950-137">Next steps</span></span>

<span data-ttu-id="13950-138">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="13950-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="13950-139">추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="13950-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
