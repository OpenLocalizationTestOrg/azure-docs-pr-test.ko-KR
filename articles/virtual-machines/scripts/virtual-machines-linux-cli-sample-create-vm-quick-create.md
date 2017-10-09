---
title: "aaaAzure CLI 스크립트 샘플-빠른 생성 Linux VM | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Linux VM 빠른 생성"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="05389-103">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="05389-103">Create a virtual machine</span></span>

<span data-ttu-id="05389-104">이 스크립트는 Ubuntu 운영 체제 및 관련 네트워킹 리소스에서 Azure Virtual Machine을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05389-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="05389-105">Hello 스크립트를 실행 한 후 가상 컴퓨터 hello SSH를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05389-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="05389-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="05389-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="05389-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="05389-107">Clean up deployment</span></span> 

<span data-ttu-id="05389-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="05389-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="05389-109">Script explanation</span></span>

<span data-ttu-id="05389-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="05389-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="05389-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="05389-112">명령</span><span class="sxs-lookup"><span data-stu-id="05389-112">Command</span></span> | <span data-ttu-id="05389-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="05389-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05389-114">az group create</span><span class="sxs-lookup"><span data-stu-id="05389-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="05389-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05389-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="05389-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="05389-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="05389-117">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="05389-118">이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="05389-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="05389-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="05389-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="05389-120">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05389-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05389-121">Next steps</span></span>

<span data-ttu-id="05389-122">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="05389-123">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="05389-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
