---
title: "aaaAzure CLI 스크립트 샘플-Windows Server VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Windows Server VM 만들기"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="3af90-103">Hello Azure CLI로 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="3af90-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="3af90-104">이 스크립트는 Windows Server 2016을 실행하는 Azure Virtual Machine을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="3af90-105">Hello 스크립트를 실행 한 후 원격 데스크톱 연결을 통해 hello 가상 컴퓨터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3af90-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3af90-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3af90-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3af90-107">Clean up deployment</span></span> 

<span data-ttu-id="3af90-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3af90-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3af90-109">Script explanation</span></span>

<span data-ttu-id="3af90-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3af90-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3af90-112">명령</span><span class="sxs-lookup"><span data-stu-id="3af90-112">Command</span></span> | <span data-ttu-id="3af90-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3af90-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3af90-114">az group create</span><span class="sxs-lookup"><span data-stu-id="3af90-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3af90-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3af90-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="3af90-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="3af90-117">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3af90-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="3af90-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="3af90-119">고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="3af90-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="3af90-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="3af90-121">Hello 인터넷 및 hello 가상 컴퓨터 간의 보안 경계를 네트워크 보안 그룹 (NSG)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="3af90-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="3af90-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="3af90-123">가상 네트워크 카드를 만들고 toohello 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="3af90-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="3af90-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="3af90-125">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3af90-126">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="3af90-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="3af90-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3af90-128">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3af90-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3af90-129">Next steps</span></span>

<span data-ttu-id="3af90-130">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3af90-131">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af90-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
