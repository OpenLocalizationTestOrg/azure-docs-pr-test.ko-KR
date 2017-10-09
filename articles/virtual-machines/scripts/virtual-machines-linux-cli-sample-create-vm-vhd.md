---
title: "aaaAzure CLI 스크립트 샘플-VHD와 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 가상 하드 디스크를 사용하여 VM 만들기."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="fae6b-103">가상 하드 디스크를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fae6b-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="fae6b-104">이 예제는 VHD를 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="fae6b-105">리소스 그룹, 저장소 계정 및 컨테이너를 생성 한 다음 hello VHD toohello 컨테이너를 업로드 하 여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="fae6b-106">대체 hello ssh 공용 액세스 toohello VM 수 있도록 공개 키로 키입니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="fae6b-107">부팅 가능 VHD가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="fae6b-108">Https://azclisamples.blob.core.windows.net/vhds/sample.vhd에서 hello 사용 된 VHD를 다운로드 하거나 사용자 고유의 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="fae6b-109">이 스크립트 hello `~/sample.vhd`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fae6b-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="fae6b-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fae6b-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="fae6b-111">Clean up deployment</span></span> 

<span data-ttu-id="fae6b-112">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="fae6b-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="fae6b-113">Script explanation</span></span>

<span data-ttu-id="fae6b-114">이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="fae6b-115">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fae6b-116">명령</span><span class="sxs-lookup"><span data-stu-id="fae6b-116">Command</span></span> | <span data-ttu-id="fae6b-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fae6b-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fae6b-118">az group create</span><span class="sxs-lookup"><span data-stu-id="fae6b-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fae6b-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fae6b-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="fae6b-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="fae6b-121">저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="fae6b-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="fae6b-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="fae6b-123">저장소 계정 이름이 유효하고 이미 존재하는 계정인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="fae6b-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="fae6b-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="fae6b-125">Hello 저장소 계정에 대 한 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="fae6b-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="fae6b-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="fae6b-127">Hello blob의 존재 여부 확인</span><span class="sxs-lookup"><span data-stu-id="fae6b-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="fae6b-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="fae6b-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="fae6b-129">저장소 계정으로 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="fae6b-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="fae6b-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="fae6b-131">VHD 업로드 hello 여 hello 컨테이너에 blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="fae6b-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="fae6b-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="fae6b-133">함께 사용할 `--query` hello VM 이름을 사용 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="fae6b-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="fae6b-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="fae6b-135">Hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="fae6b-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="fae6b-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="fae6b-137">Hello SSH 키 toogive hello 현재 사용자 액세스 toohello VM을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="fae6b-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="fae6b-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="fae6b-139">Hello 생성 된 VM의 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fae6b-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fae6b-140">Next steps</span></span>

<span data-ttu-id="fae6b-141">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fae6b-142">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="fae6b-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
