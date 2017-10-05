---
title: "Azure CLI 스크립트 샘플 - 부하가 분산된 가상 컴퓨터 확장 집합에서 LAMP 스택 배포 | Microsoft Docs"
description: "사용자 지정 스크립트 확장을 사용하여 Azure의 부하가 분산된 가상 컴퓨터 확장 집합에서 LAMP 스택을 배포합니다."
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
ms.openlocfilehash: 4007e8c85c0ff24bf5030881eac666582714eae3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="6344a-103">부하가 분산된 가상 컴퓨터 확장 집합에서 LAMP 스택 배포</span><span class="sxs-lookup"><span data-stu-id="6344a-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="6344a-104">이 예제에서는 가상 컴퓨터 확장 집합을 만들고 사용자 지정 스크립트를 실행하는 확장을 적용하여 LAMP 스택을 확장 집합의 각 가상 컴퓨터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="6344a-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="6344a-105">Sample script</span></span>

<span data-ttu-id="6344a-106">[!code-azurecli-interactive[주](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "LAMP 스택을 사용하여 가상 컴퓨터 확장 집합 만들기")]</span><span class="sxs-lookup"><span data-stu-id="6344a-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]</span></span>

## <a name="connect"></a><span data-ttu-id="6344a-107">연결</span><span class="sxs-lookup"><span data-stu-id="6344a-107">Connect</span></span>

<span data-ttu-id="6344a-108">이 코드를 사용하여 VM 및 확장 집합에 연결하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-108">Use this code to see how to connect to your VMs and your scale set.</span></span>

<span data-ttu-id="6344a-109">[!code-azurecli[주](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "가상 컴퓨터 확장 집합에 액세스")]</span><span class="sxs-lookup"><span data-stu-id="6344a-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6344a-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="6344a-110">Clean up deployment</span></span> 

<span data-ttu-id="6344a-111">다음 명령을 실행하여 리소스 그룹, 확장 집합, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-111">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6344a-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="6344a-112">Script explanation</span></span>

<span data-ttu-id="6344a-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-113">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="6344a-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6344a-115">명령</span><span class="sxs-lookup"><span data-stu-id="6344a-115">Command</span></span> | <span data-ttu-id="6344a-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6344a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6344a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6344a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6344a-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6344a-119">az vmss create</span><span class="sxs-lookup"><span data-stu-id="6344a-119">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="6344a-120">가상 컴퓨터 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-120">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="6344a-121">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="6344a-121">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="6344a-122">부하가 분산된 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-122">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="6344a-123">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="6344a-123">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="6344a-124">VM 배포에서 사용자 지정 스크립트를 실행하는 확장을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-124">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="6344a-125">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="6344a-125">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="6344a-126">확장이 확장 집합에 적용되기 전에 배포된 VM 인스턴스에서 사용자 지정 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-126">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="6344a-127">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="6344a-127">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="6344a-128">더 많은 VM 인스턴스를 추가하여 확장 집합의 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-128">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="6344a-129">VM 인스턴스가 배포되면 사용자 지정 스크립트가 해당 VM 인스턴스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-129">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="6344a-130">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="6344a-130">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="6344a-131">샘플에서 만든 VM의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-131">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="6344a-132">az network lb show</span><span class="sxs-lookup"><span data-stu-id="6344a-132">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="6344a-133">부하 분산 장치에서 사용하는 프런트 엔드 포트와 백 엔드 포트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-133">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6344a-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6344a-134">Next steps</span></span>

<span data-ttu-id="6344a-135">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6344a-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6344a-136">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6344a-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
