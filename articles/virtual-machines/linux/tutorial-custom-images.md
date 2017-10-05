---
title: "Azure CLI를 사용하여 사용자 지정 VM 이미지 만들기 | Microsoft Docs"
description: "자습서 - Azure CLI를 사용하여 사용자 지정 VM 이미지 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="01619-103">CLI를 사용하여 Azure VM의 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="01619-104">사용자 지정 이미지는 Marketplace 이미지와 같지만 직접 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01619-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="01619-105">응용 프로그램 사전 로드, 응용 프로그램 구성 및 기타 OS 구성과 같은 부트스트랩 구성에 사용자 지정 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="01619-106">이 자습서에서는 Azure Virtual Machines의 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01619-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="01619-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="01619-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="01619-108">VM 프로비전 해제 및 일반화</span><span class="sxs-lookup"><span data-stu-id="01619-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="01619-109">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-109">Create a custom image</span></span>
> * <span data-ttu-id="01619-110">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="01619-111">구독에 모든 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="01619-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="01619-112">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="01619-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01619-113">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="01619-114">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="01619-115">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01619-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="01619-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="01619-116">Before you begin</span></span>

<span data-ttu-id="01619-117">아래 단계에서는 기존 VM을 가져와서 새 VM 인스턴스를 만드는 데 사용할 수 있는 재사용 가능 사용자 지정 이미지로 변환하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="01619-118">이 자습서의 예제를 완료하려면 기존 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="01619-119">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="01619-120">이 자습서를 진행할 때 필요한 경우 리소스 그룹 및 VM 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="01619-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="01619-121">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-121">Create a custom image</span></span>

<span data-ttu-id="01619-122">가상 컴퓨터의 이미지를 만들려면 프로비전을 해제하고 할당을 취소한 후 원본 VM을 일반화된 것으로 표시하여 VM을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="01619-123">VM이 준비되면 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="01619-124">VM 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="01619-124">Deprovision the VM</span></span> 

<span data-ttu-id="01619-125">프로비전을 해제하면 컴퓨터별 정보를 제거하여 VM을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="01619-126">이 일반화를 통해 단일 이미지에서 여러 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="01619-127">프로비전을 해제하는 동안 호스트 이름이 *localhost.localdomain*으로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="01619-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="01619-128">SSH 호스트 키, 이름 서버 구성, 루트 암호 및 캐시된 DHCP 임대도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="01619-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="01619-129">VM 프로비전을 해제하려면 Azure VM 에이전트(waagent)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="01619-130">Azure VM 에이전트는 VM에 설치되고 Azure 패브릭 컨트롤러와의 상호 작용과 프로비전을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="01619-131">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](agent-user-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01619-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="01619-132">SSH를 사용하여 VM에 연결하고 VM 프로비전 해제 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="01619-133">`+user` 인수를 사용하면 마지막으로 프로비전된 사용자 계정 및 관련 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="01619-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="01619-134">예제 IP 주소를 VM의 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="01619-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="01619-135">VM에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="01619-136">VM의 프로비전을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="01619-137">SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="01619-138">할당을 취소하고 VM을 일반화된 것으로 표시</span><span class="sxs-lookup"><span data-stu-id="01619-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="01619-139">이미지를 만들려면 VM을 할당 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="01619-140">[az vm deallocate](/cli//azure/vm#deallocate)를 사용하여 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="01619-141">마지막으로, VM이 일반화된 사실을 Azure 플랫폼이 알 수 있도록 [az vm generalize](/cli//azure/vm#generalize) 명령을 사용하여 VM 상태를 일반화됨으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="01619-142">일반화된 VM에서만 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="01619-143">이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-143">Create the image</span></span>

<span data-ttu-id="01619-144">이제 [az image create](/cli//azure/image#create)를 사용하여 VM의 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="01619-145">다음 예제에서는 *myVM*이라는 VM에서 *myImage*라는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01619-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="01619-146">이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-146">Create VMs from the image</span></span>

<span data-ttu-id="01619-147">이미지가 생겼으니, [az vm create](/cli/azure/vm#create) 명령을 사용하여 이 이미지에서 하나 이상의 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="01619-148">다음 예제에서는 *myImage*라는 이미지에서 *myVMfromImage*라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01619-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="01619-149">이미지 관리</span><span class="sxs-lookup"><span data-stu-id="01619-149">Image management</span></span> 

<span data-ttu-id="01619-150">일반적인 이미지 관리 작업의 몇 가지 예제와 Azure CLI를 사용하여 완료하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="01619-151">모든 이미지를 테이블 형식으로 이름별로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="01619-152">이미지 삭제를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-152">Delete an image.</span></span> <span data-ttu-id="01619-153">이 예제에서는 *myResourceGroup*에서 *myOldImage*라는 이미지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="01619-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01619-154">Next steps</span></span>

<span data-ttu-id="01619-155">이 자습서에서는 사용자 지정 VM 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="01619-156">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="01619-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="01619-157">VM 프로비전 해제 및 일반화</span><span class="sxs-lookup"><span data-stu-id="01619-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="01619-158">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-158">Create a custom image</span></span>
> * <span data-ttu-id="01619-159">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="01619-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="01619-160">구독에 모든 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="01619-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="01619-161">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="01619-161">Delete an image</span></span>

<span data-ttu-id="01619-162">고가용성 가상 컴퓨터에 대해 알아보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="01619-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="01619-163">[고가용성 VM 만들기](tutorial-availability-sets.md)</span><span class="sxs-lookup"><span data-stu-id="01619-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

