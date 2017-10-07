---
title: "aaaAzure CLI 스크립트 샘플-DSC를 사용 하 여 IIS와 Windows Server 2016 VM을 만듭니다. | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - DSC를 사용하는 IIS로 Windows Server 2016 VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="c6751-103">DSC를 사용하는 IIS로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c6751-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="c6751-104">이 스크립트 가상 컴퓨터 및 Azure 가상 컴퓨터 DSC 사용자 지정 스크립트 확장 tooinstall hello를 사용 하 여 만들고 IIS를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c6751-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c6751-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c6751-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c6751-106">Clean up deployment</span></span> 

<span data-ttu-id="c6751-107">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c6751-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c6751-108">Script explanation</span></span>

<span data-ttu-id="c6751-109">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c6751-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c6751-111">명령</span><span class="sxs-lookup"><span data-stu-id="c6751-111">Command</span></span> | <span data-ttu-id="c6751-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c6751-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c6751-113">az group create</span><span class="sxs-lookup"><span data-stu-id="c6751-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c6751-114">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c6751-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="c6751-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c6751-116">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c6751-117">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c6751-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="c6751-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c6751-119">스크립트 tooinstall IIS를 호출 하는 hello 사용자 지정 스크립트 확장 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="c6751-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="c6751-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="c6751-121">네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="c6751-122">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="c6751-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="c6751-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c6751-124">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6751-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6751-125">Next steps</span></span>

<span data-ttu-id="c6751-126">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c6751-127">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6751-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
