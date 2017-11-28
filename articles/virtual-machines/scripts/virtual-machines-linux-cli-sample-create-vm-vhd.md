---
title: "Azure CLI 스크립트 샘플 - VHD를 사용하여 VM 만들기 | Microsoft 문서"
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
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="3a32b-103">가상 하드 디스크를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3a32b-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="3a32b-104">이 예제는 VHD를 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="3a32b-105">리소스 그룹, 저장소 계정 및 컨테이너를 만들고 VHD를 컨테이너로 업로드하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="3a32b-106">VM에 액세스할 수 있도록 SSH 공개 키를 사용자 공개 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="3a32b-107">부팅 가능 VHD가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="3a32b-108">https://azclisamples.blob.core.windows.net/vhds/sample.vhd에서 사용한 VHD를 다운로드하거나 사용자 지정 VHD를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="3a32b-109">스크립트는 `~/sample.vhd`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3a32b-110">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3a32b-110">Sample script</span></span>

<span data-ttu-id="3a32b-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "VHD를 사용하여 VM 만들기")]</span><span class="sxs-lookup"><span data-stu-id="3a32b-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3a32b-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3a32b-112">Clean up deployment</span></span> 

<span data-ttu-id="3a32b-113">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="3a32b-114">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3a32b-114">Script explanation</span></span>

<span data-ttu-id="3a32b-115">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="3a32b-116">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3a32b-117">명령</span><span class="sxs-lookup"><span data-stu-id="3a32b-117">Command</span></span> | <span data-ttu-id="3a32b-118">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3a32b-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a32b-119">az group create</span><span class="sxs-lookup"><span data-stu-id="3a32b-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3a32b-120">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a32b-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="3a32b-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="3a32b-122">저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="3a32b-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="3a32b-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="3a32b-124">저장소 계정 이름이 유효하고 이미 존재하는 계정인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="3a32b-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="3a32b-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="3a32b-126">저장소 계정의 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="3a32b-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="3a32b-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="3a32b-128">Blob이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="3a32b-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="3a32b-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="3a32b-130">저장소 계정으로 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="3a32b-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="3a32b-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="3a32b-132">VHD를 업로드하여 컨테이너에서 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="3a32b-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="3a32b-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="3a32b-134">`--query`와 함께 사용하여 VM 이름이 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="3a32b-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="3a32b-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="3a32b-136">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="3a32b-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="3a32b-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="3a32b-138">현재 사용자에게 VM에 대한 액세스 권한을 부여하도록 SSH 키를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="3a32b-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="3a32b-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="3a32b-140">만들어진 VM의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a32b-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a32b-141">Next steps</span></span>

<span data-ttu-id="3a32b-142">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a32b-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3a32b-143">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a32b-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
