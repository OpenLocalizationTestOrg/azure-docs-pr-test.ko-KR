---
title: "빨리 만들기는 Windows Server 2016 VM aaaAzure CLI 스크립트 샘플-| Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Windows Server 2016 VM 빠른 생성"
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
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="21891-103">Hello Azure CLI로 가상 컴퓨터를 빨리 만들기</span><span class="sxs-lookup"><span data-stu-id="21891-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="21891-104">이 스크립트는 Windows Server 2016을 실행하는 Azure Virtual Machine을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21891-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="21891-105">Hello 스크립트를 실행 한 후 원격 데스크톱 연결을 통해 hello 가상 컴퓨터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21891-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="21891-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="21891-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="21891-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="21891-107">Clean up deployment</span></span> 

<span data-ttu-id="21891-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="21891-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="21891-109">Script explanation</span></span>

<span data-ttu-id="21891-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="21891-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="21891-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="21891-112">명령</span><span class="sxs-lookup"><span data-stu-id="21891-112">Command</span></span> | <span data-ttu-id="21891-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="21891-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21891-114">az group create</span><span class="sxs-lookup"><span data-stu-id="21891-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="21891-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21891-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21891-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="21891-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="21891-117">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="21891-118">이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="21891-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="21891-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="21891-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="21891-120">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21891-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21891-121">Next steps</span></span>

<span data-ttu-id="21891-122">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="21891-123">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="21891-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
