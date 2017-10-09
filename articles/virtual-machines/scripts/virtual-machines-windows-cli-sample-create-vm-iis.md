---
title: "aaaAzure CLI 스크립트 샘플-IIS를 설치 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - IIS 설치"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="315a8-103">Hello Azure CLI로 가상 컴퓨터를 빨리 만들기</span><span class="sxs-lookup"><span data-stu-id="315a8-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="315a8-104">이 스크립트는 Windows Server 2016을 실행 하는 Azure 가상 컴퓨터를 만들고 hello Azure 가상 컴퓨터 사용자 지정 스크립트 확장 tooinstall IIS를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="315a8-105">Hello 스크립트를 실행 한 후 hello 기본 IIS 웹 사이트 hello hello 가상 컴퓨터의 공용 IP 주소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="315a8-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="315a8-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="315a8-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="315a8-107">Clean up deployment</span></span> 

<span data-ttu-id="315a8-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="315a8-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="315a8-109">Script explanation</span></span>

<span data-ttu-id="315a8-110">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="315a8-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="315a8-112">명령</span><span class="sxs-lookup"><span data-stu-id="315a8-112">Command</span></span> | <span data-ttu-id="315a8-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="315a8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="315a8-114">az group create</span><span class="sxs-lookup"><span data-stu-id="315a8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="315a8-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="315a8-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="315a8-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="315a8-117">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 네트워크 보안 그룹을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="315a8-118">이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="315a8-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="315a8-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="315a8-120">네트워크 보안 그룹 규칙 tooallow 만듭니다 트래픽 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="315a8-121">이 샘플에서 HTTP 트래픽에 대해 포트 80이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="315a8-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="315a8-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="315a8-123">추가 하 고 가상 컴퓨터 확장 tooa VM을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="315a8-124">이 샘플에서 hello 사용자 지정 스크립트 확장 사용 되는 tooinstall IIS는 합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="315a8-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="315a8-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="315a8-126">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="315a8-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="315a8-127">Next steps</span></span>

<span data-ttu-id="315a8-128">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="315a8-129">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="315a8-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
