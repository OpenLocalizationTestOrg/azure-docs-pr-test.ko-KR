---
title: "hello Azure CLI를 사용 하 여 사용자 지정 VM 이미지를 aaaCreate | Microsoft Docs"
description: "자습서-hello Azure CLI를 사용 하 여 사용자 지정 VM 이미지를 만듭니다."
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="12c77-103">Hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="12c77-104">사용자 지정 이미지는 Marketplace 이미지와 같지만 직접 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="12c77-105">사용자 지정 이미지에는 응용 프로그램, 응용 프로그램 구성 및 기타 운영 체제 구성을 미리 로드 하는 등 사용된 toobootstrap 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="12c77-106">이 자습서에서는 Azure Virtual Machines의 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="12c77-107">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12c77-108">VM 프로비전 해제 및 일반화</span><span class="sxs-lookup"><span data-stu-id="12c77-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="12c77-109">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-109">Create a custom image</span></span>
> * <span data-ttu-id="12c77-110">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="12c77-111">구독에서 모든 hello 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="12c77-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="12c77-112">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="12c77-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="12c77-113">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="12c77-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="12c77-114">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="12c77-115">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="12c77-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="12c77-116">Before you begin</span></span>

<span data-ttu-id="12c77-117">다음 hello 단계 tootake 기존 VM 및 설정에 재사용 가능한 사용자 지정 이미지를 toocreate 새 VM 인스턴스 사용 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="12c77-118">이 자습서에서는 toocomplete hello 예제에서는 기존 가상 컴퓨터 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="12c77-119">필요한 경우 이 [스크립트 샘플](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md)을 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="12c77-120">Hello 자습서를 통해 작업 대체 필요한 경우 hello 리소스 그룹 및 VM 이름 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="12c77-121">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-121">Create a custom image</span></span>

<span data-ttu-id="12c77-122">가상 컴퓨터의 이미지 toocreate tooprepare hello VM 프로 비전 해제, 할당 해제, 다음 hello 소스 일반화 된 것과 같이 VM을 표시 하 여 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="12c77-123">한 번 VM 준비 된 hello, 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="12c77-124">Hello VM을 프로 비전 해제</span><span class="sxs-lookup"><span data-stu-id="12c77-124">Deprovision hello VM</span></span> 

<span data-ttu-id="12c77-125">컴퓨터 관련 정보를 제거 하 여 hello VM을 일반화 프로 비전 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="12c77-126">이 일반화 가능한 toodeploy를 사용 하면 단일 이미지에서 많은 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="12c77-127">Hello 호스트 이름이 너무 재설정, 프로 비전 해제 하는 동안*localhost.localdomain*합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="12c77-128">SSH 호스트 키, 이름 서버 구성, 루트 암호 및 캐시된 DHCP 임대도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="12c77-129">VM을 toodeprovision hello hello Azure VM 에이전트 (waagent)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="12c77-130">hello Azure VM 에이전트 hello VM에 설치 하 고 프로 비전 하 고 hello Azure 패브릭 컨트롤러와의 상호 작용을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="12c77-131">자세한 내용은 참조 hello [Azure Linux 에이전트 사용자 가이드](agent-user-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="12c77-132">Tooyour VM 연결 SSH 및 실행된 hello 명령 toodeprovision hello VM 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="12c77-133">Hello로 `+user` 인수, hello 마지막 프로 비전 된 사용자 계정 및 관련된 데이터도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="12c77-134">VM의 공용 IP 주소 hello와 hello 예제 IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="12c77-135">SSH toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="12c77-136">Hello VM을 프로 비전 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="12c77-137">Hello SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="12c77-138">할당을 취소 하 고 hello VM 일반화 된 대로 표시</span><span class="sxs-lookup"><span data-stu-id="12c77-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="12c77-139">이미지 toocreate hello VM toobe 할당 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="12c77-140">사용 하 여 hello VM 할당을 취소 [az vm 할당을 취소](/cli//azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="12c77-141">마지막으로 사용 하 여 일반화할 대로 hello VM의 hello 상태를 설정 [az vm 일반화](/cli//azure/vm#generalize) hello Azure 플랫폼에서 VM 일반화 된 hello 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="12c77-142">일반화된 VM에서만 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="12c77-143">Hello 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-143">Create hello image</span></span>

<span data-ttu-id="12c77-144">사용 하 여 hello VM의 이미지를 만들 수 이제 [az 이미지 만들기](/cli//azure/image#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="12c77-145">hello 다음 예제에서는 명명 된 이미지 *myImage* 라는 VM에서 *myVM*합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="12c77-146">Hello 이미지에서 Vm 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-146">Create VMs from hello image</span></span>

<span data-ttu-id="12c77-147">이미지를가지고 사용 하 여 hello 이미지에서 하나 이상의 새 Vm을 만들 수 있습니다 [az vm 만들기](/cli/azure/vm#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="12c77-148">hello 다음 예제에서는 V *myVMfromImage* 라는 hello 이미지에서 *myImage*합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="12c77-149">이미지 관리</span><span class="sxs-lookup"><span data-stu-id="12c77-149">Image management</span></span> 

<span data-ttu-id="12c77-150">다음은 일반 이미지 관리 작업의 몇 가지 예제와 방법을 toocomplete hello Azure CLI를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="12c77-151">모든 이미지를 테이블 형식으로 이름별로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="12c77-152">이미지 삭제를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-152">Delete an image.</span></span> <span data-ttu-id="12c77-153">이 예에서는 삭제 hello 라는 이미지 *myOldImage* hello에서 *myResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="12c77-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12c77-154">Next steps</span></span>

<span data-ttu-id="12c77-155">이 자습서에서는 사용자 지정 VM 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="12c77-156">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="12c77-157">VM 프로비전 해제 및 일반화</span><span class="sxs-lookup"><span data-stu-id="12c77-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="12c77-158">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-158">Create a custom image</span></span>
> * <span data-ttu-id="12c77-159">사용자 지정 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="12c77-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="12c77-160">구독에서 모든 hello 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="12c77-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="12c77-161">이미지 삭제</span><span class="sxs-lookup"><span data-stu-id="12c77-161">Delete an image</span></span>

<span data-ttu-id="12c77-162">항상 사용 가능한 가상 컴퓨터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c77-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="12c77-163">[고가용성 VM 만들기](tutorial-availability-sets.md)</span><span class="sxs-lookup"><span data-stu-id="12c77-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

