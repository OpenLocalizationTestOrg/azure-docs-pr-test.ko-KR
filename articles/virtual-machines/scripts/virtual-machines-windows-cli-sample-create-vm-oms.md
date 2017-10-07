---
title: "aaaAzure CLI 스크립트 샘플-OMS에서 모니터링 된 Windows Server 2016 VM을 만듭니다. | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - OMS 모니터링을 사용하여 Windows Server 2016 VM 만들기"
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
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="3cc7a-103">Operations Management Suite를 사용하여 VM 모니터링</span><span class="sxs-lookup"><span data-stu-id="3cc7a-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="3cc7a-104">Azure 가상 컴퓨터를 만들고 hello Operations Management Suite (OMS) 에이전트를 설치 hello 시스템 OMS 작업 영역을 등록 하는이 스크립트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="3cc7a-105">Hello 스크립트 실행 되 면 hello 가상 컴퓨터 hello OMS 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3cc7a-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3cc7a-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3cc7a-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3cc7a-107">Clean up deployment</span></span> 

<span data-ttu-id="3cc7a-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3cc7a-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3cc7a-109">Script explanation</span></span>

<span data-ttu-id="3cc7a-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="3cc7a-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3cc7a-112">명령</span><span class="sxs-lookup"><span data-stu-id="3cc7a-112">Command</span></span> | <span data-ttu-id="3cc7a-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3cc7a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3cc7a-114">az group create</span><span class="sxs-lookup"><span data-stu-id="3cc7a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3cc7a-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3cc7a-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="3cc7a-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="3cc7a-117">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3cc7a-118">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="3cc7a-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="3cc7a-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3cc7a-120">가상 컴퓨터에 대한 VM 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="3cc7a-121">이 경우 Operations Management Suite 에이전트 확장 hello 사용 되는 tooinstall hello OMS 에이전트 되며 hello OMS 작업 영역에서 VM을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="3cc7a-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="3cc7a-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3cc7a-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3cc7a-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3cc7a-124">Next steps</span></span>

<span data-ttu-id="3cc7a-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3cc7a-126">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3cc7a-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
