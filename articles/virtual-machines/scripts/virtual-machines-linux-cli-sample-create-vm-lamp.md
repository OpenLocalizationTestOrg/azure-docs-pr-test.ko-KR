---
title: "CLI 스크립트 샘플-aaaAzure hello Load-Balanced 가상 Machin 크기 집합의 LAMP 스택 배포 | Microsoft Docs"
description: "사용자 지정 스크립트 확장 toodeploy hello LAMP 스택 부하에서를 사용 하 여 Azure에서 설정 하는 분산 된 가상 컴퓨터 크기 = 합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="57c4b-103">부하 분산 된 가상 컴퓨터 크기 집합의 hello LAMP 스택 배포</span><span class="sxs-lookup"><span data-stu-id="57c4b-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="57c4b-104">이 예제에서는 가상 컴퓨터 크기 집합을 만들고 hello 크기 집합의 각 가상 컴퓨터에서 사용자 지정 스크립트 toodeploy hello LAMP 스택을 실행 하는 확장을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="57c4b-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="57c4b-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="57c4b-106">연결</span><span class="sxs-lookup"><span data-stu-id="57c4b-106">Connect</span></span>

<span data-ttu-id="57c4b-107">이 코드 toosee tooconnect tooyour Vm 및 눈금 설정 하는 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="57c4b-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="57c4b-108">Clean up deployment</span></span> 

<span data-ttu-id="57c4b-109">Hello 명령 tooremove hello 리소스 그룹, hello 크기 집합, Vm 및 관련 된 모든 리소스 따라를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="57c4b-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="57c4b-110">Script explanation</span></span>

<span data-ttu-id="57c4b-111">이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="57c4b-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="57c4b-113">명령</span><span class="sxs-lookup"><span data-stu-id="57c4b-113">Command</span></span> | <span data-ttu-id="57c4b-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="57c4b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="57c4b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="57c4b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="57c4b-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="57c4b-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="57c4b-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="57c4b-118">가상 컴퓨터 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="57c4b-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="57c4b-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="57c4b-120">부하가 분산된 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="57c4b-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="57c4b-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="57c4b-122">VM의 배포에서 hello 사용자 지정 스크립트를 실행 하는 hello 확장 만들기</span><span class="sxs-lookup"><span data-stu-id="57c4b-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="57c4b-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="57c4b-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="57c4b-124">Hello 확장 적용 하기 전에 배포 된 hello VM 인스턴스에서 hello 사용자 지정 스크립트를 실행 toohello 크기 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="57c4b-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="57c4b-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="57c4b-126">Hello에 크기 집합 VM 인스턴스를 더 추가 하 여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="57c4b-127">hello 사용자 지정 스크립트는 배포 하는 경우 이러한 이벤트에 대해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="57c4b-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="57c4b-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="57c4b-129">Hello hello 샘플에서 만들어진 Vm의 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="57c4b-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="57c4b-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="57c4b-131">Hello 프런트 엔드 및 백 엔드 hello 부하 분산 장치에서 사용 하는 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="57c4b-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57c4b-132">Next steps</span></span>

<span data-ttu-id="57c4b-133">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="57c4b-134">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="57c4b-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
