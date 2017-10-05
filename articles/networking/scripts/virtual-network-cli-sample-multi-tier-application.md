---
title: "Azure CLI 스크립트 샘플 - 다중 계층 응용 프로그램용 네트워크 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 다중 계층 응용 프로그램을 위한 가상 네트워크를 만듭니다."
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="3cc09-103">다중 계층 응용 프로그램을 위한 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="3cc09-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="3cc09-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="3cc09-105">프런트 엔드 서브넷에 대한 트래픽은 HTTP 및 SSH로 제한되며, 백 엔드 서브넷에 대한 트래픽은 MySQL(3306 포트)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="3cc09-106">스크립트를 실행한 후에는 웹 서버와 MySQL 소프트웨어를 배포할 수 있는 두 개의 가상 컴퓨터가 각 서브넷에 하나씩 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="3cc09-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3cc09-107">Sample script</span></span>


<span data-ttu-id="3cc09-108">[!code-azurecli-interactive[주](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "다중 계층 응용 프로그램용 가상 네트워크")]</span><span class="sxs-lookup"><span data-stu-id="3cc09-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3cc09-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3cc09-109">Clean up deployment</span></span> 

<span data-ttu-id="3cc09-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3cc09-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3cc09-111">Script explanation</span></span>

<span data-ttu-id="3cc09-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="3cc09-113">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="3cc09-114">명령</span><span class="sxs-lookup"><span data-stu-id="3cc09-114">Command</span></span> | <span data-ttu-id="3cc09-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3cc09-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3cc09-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3cc09-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="3cc09-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3cc09-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="3cc09-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="3cc09-119">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="3cc09-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="3cc09-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="3cc09-121">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="3cc09-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="3cc09-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="3cc09-123">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="3cc09-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="3cc09-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="3cc09-125">가상 네트워크 인터페이스를 만들고 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="3cc09-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="3cc09-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="3cc09-127">프런트 엔드 및 백 엔드 서브넷과 연결되는 NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="3cc09-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="3cc09-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="3cc09-129">특정 포트를 특정 서브넷에 허용하거나 차단하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="3cc09-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="3cc09-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="3cc09-131">가상 컴퓨터를 만들고 각 VM에 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="3cc09-132">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="3cc09-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="3cc09-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="3cc09-134">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3cc09-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cc09-135">Next steps</span></span>

<span data-ttu-id="3cc09-136">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3cc09-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="3cc09-137">추가 네트워킹 CLI 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../cli-samples.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3cc09-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>