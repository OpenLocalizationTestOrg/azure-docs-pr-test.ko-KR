---
title: "aaaAzure CLI 스크립트 샘플-다중 계층 응용 프로그램에 대 한 네트워크 만들기 | Microsoft Docs"
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="52914-103">다중 계층 응용 프로그램을 위한 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="52914-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="52914-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="52914-105">트래픽 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 SSH, 트래픽 toohello 하는 동안 백 엔드 서브넷은 제한 된 tooMySQL, 3306 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="52914-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="52914-106">Hello 스크립트를 실행 한 후 웹 서버 및 MySQL 소프트웨어를 배포할 수 있는 각 서브넷에 각각 하나씩 두 개의 가상 컴퓨터가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="52914-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="52914-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="52914-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="52914-108">Clean up deployment</span></span> 

<span data-ttu-id="52914-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="52914-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="52914-110">Script explanation</span></span>

<span data-ttu-id="52914-111">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="52914-112">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="52914-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="52914-113">명령</span><span class="sxs-lookup"><span data-stu-id="52914-113">Command</span></span> | <span data-ttu-id="52914-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="52914-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52914-115">az group create</span><span class="sxs-lookup"><span data-stu-id="52914-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="52914-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="52914-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="52914-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="52914-118">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="52914-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="52914-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="52914-120">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="52914-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="52914-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="52914-122">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="52914-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="52914-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="52914-124">가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="52914-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="52914-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="52914-126">네트워크 보안 그룹 (NSG) 관련된 toohello 프런트 엔드 및 백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="52914-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="52914-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="52914-128">NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52914-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="52914-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="52914-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="52914-130">가상 컴퓨터를 만들고 NIC tooeach VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="52914-131">이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="52914-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="52914-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="52914-133">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52914-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52914-134">Next steps</span></span>

<span data-ttu-id="52914-135">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="52914-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="52914-136">추가 네트워킹 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="52914-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
