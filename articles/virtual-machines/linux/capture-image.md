---
title: "CLI 2.0을 사용 하 여 Azure에서 Linux VM의 이미지 aaaCapture | Microsoft Docs"
description: "Hello Azure CLI 2.0을 사용 하 여 대용량 배포에는 Azure VM toouse의 이미지를 캡처하십시오."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="bb372-103">어떻게 toocreate 가상 컴퓨터 또는 VHD의 이미지</span><span class="sxs-lookup"><span data-stu-id="bb372-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="bb372-104">toocreate azure에서 가상 컴퓨터 (VM) toouse의 여러 복사본 hello VM의 이미지를 캡처하거나 운영 체제 VHD hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="bb372-105">toocreate 이미지 하므로 더 안전 하 게 toodeploy 여러 번 개인 계정 정보를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="bb372-106">기존 VM을 프로 비전 해제 하는 단계를 수행 하는 hello, 이미지 만들기 및 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="bb372-107">구독 내에서 모든 리소스 그룹에 걸쳐이 이미지 toocreate Vm을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="bb372-108">Toocreate 기존 Linux VM의 복사본을 백업 또는 디버깅에 사용할 온-프레미스 VM에서 특수 한 Linux VHD를 업로드 하거나, 참조 [업로드 한 사용자 지정 디스크 이미지에서 Linux VM을 만들](upload-vhd.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="bb372-109">사용할 수도 있습니다 **Packer** toocreate 사용자 지정 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="bb372-110">Packer 사용에 대 한 자세한 내용은 참조 하십시오. [toouse Packer toocreate Linux 가상 컴퓨터를 Azure에서 이미지 어떻게](build-image-with-packer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="bb372-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="bb372-111">Before you begin</span></span>
<span data-ttu-id="bb372-112">Hello 다음 필수 구성 요소를 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="bb372-113">Azure VM 관리 하는 디스크를 사용 하 여 hello 리소스 관리자 배포 모델에서 만든 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="bb372-114">Linux VM을 만들지 않은 경우에 hello을 사용할 수 있습니다 [포털](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), 또는 [리소스 관리자 템플릿을](create-ssh-secured-vm-from-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="bb372-115">필요에 따라 VM hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-115">Configure hello VM as needed.</span></span> <span data-ttu-id="bb372-116">예를 들어 [데이터 디스크를 추가하고](add-disk.md), 업데이트를 적용하고, 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="bb372-117">또한 해야 toohave hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 tooan Azure 계정에 기록 될 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="bb372-118">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="bb372-118">Quick commands</span></span>

<span data-ttu-id="bb372-119">테스트를 위해이 항목의 단순화 된 버전에 대 한 평가 또는 Azure에서 Vm에 대해 알아보기, 참조 [hello CLI를 사용 하 여 Azure VM의 사용자 지정 이미지를 만드는](tutorial-custom-images.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="bb372-120">1 단계: hello VM 프로 비전 해제</span><span class="sxs-lookup"><span data-stu-id="bb372-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="bb372-121">Hello hello Azure VM 에이전트, toodelete 컴퓨터에 대 한 특정 파일 및 데이터를 사용 하 여 VM을 프로 비전 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="bb372-122">사용 하 여 hello `waagent` hello로 명령을 *-deprovision + 사용자* 소스 Linux VM에 대 한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="bb372-123">자세한 내용은 참조 hello [Azure Linux 에이전트 사용자 가이드](../windows/agent-user-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="bb372-124">Tooyour SSH 클라이언트를 사용 하 여 Linux VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="bb372-125">Hello SSH 창의 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="bb372-126">만 toocapture 이미지 형식으로 하려는 VM에서이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="bb372-127">Hello 이미지가 중요 한 정보를 모두 선택 취소 되어 또는 재배포를 위해 적합 한 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="bb372-128">hello *+ 사용자* 매개 변수는 또한 hello 마지막 프로 비전 된 사용자 계정을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="bb372-129">Hello VM에에서 tookeep 계정 자격 증명을 사용 하도록 하려는 경우 사용 *-deprovision* tooleave hello 사용자 계정을 준비에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="bb372-130">형식 **y** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-130">Type **y** toocontinue.</span></span> <span data-ttu-id="bb372-131">Hello를 추가할 수 있습니다 **-강제로** 매개 변수 tooavoid이 확인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="bb372-132">Hello 명령이 완료 된 후 입력 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="bb372-133">이 단계는 hello SSH 클라이언트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="bb372-134">2단계: VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="bb372-134">Step 2: Create VM image</span></span>
<span data-ttu-id="bb372-135">일반화 된 대로 Azure CLI 2.0 hello toomark hello VM use 하 고 hello 이미지를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="bb372-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="bb372-136">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="bb372-137">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="bb372-138">Hello를 프로 비전 된 VM을 할당 취소 [az vm 할당을 취소](/cli//azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="bb372-139">hello 다음 예제에서는 할당 취소 hello 라는 VM *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="bb372-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="bb372-140">표시 hello와 일반화 된 것과 같이 VM [az vm 일반화](/cli//azure/vm#generalize)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="bb372-141">다음 예제에서는 부호 hello hello VM 라는 hello *myVM* 이라는 hello 리소스 그룹에 *myResourceGroup* 일반화 된 대로:</span><span class="sxs-lookup"><span data-stu-id="bb372-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="bb372-142">지금 사용 하 여 hello VM 리소스의 이미지를 만들어 [az 이미지 만들기](/cli//azure/image#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="bb372-143">hello 다음 예제에서는 명명 된 이미지 *myImage* 이라는 hello 리소스 그룹에 *myResourceGroup* 라는 hello VM 리소스를 사용 하 여 *myVM*:</span><span class="sxs-lookup"><span data-stu-id="bb372-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="bb372-144">hello 이미지가 만들어지고 hello에서 동일한 원본 VM으로 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="bb372-145">이 이미지에서 구독 내의 모든 리소스 그룹에 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="bb372-146">관리 측면에서 toocreate VM 리소스와 이미지에 대 한 특정 리소스 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="bb372-147">3 단계: hello 캡처된 이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="bb372-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="bb372-148">사용 하 여 만든 hello 이미지를 사용 하 여 VM 만들기 [az vm 만들기](/cli/azure/vm#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bb372-149">hello 다음 예제에서는 V *myVMDeployed* 라는 hello 이미지에서 *myImage*:</span><span class="sxs-lookup"><span data-stu-id="bb372-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="bb372-150">다른 리소스 그룹에 hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="bb372-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="bb372-151">구독 내 모든 리소스 그룹의 이미지에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="bb372-152">hello 이미지 보다 다른 리소스 그룹에서 VM toocreate hello 전체 리소스 ID tooyour 이미지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="bb372-153">사용 하 여 [az 이미지 목록](/cli/azure/image#list) tooview 이미지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="bb372-154">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="bb372-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="bb372-155">hello 다음 예제에서는 [az vm 만들기](/cli/azure/vm#create) toocreate hello 이미지 리소스 ID를 지정 하 여 hello 소스 이미지 보다 다른 리소스 그룹에서 VM:</span><span class="sxs-lookup"><span data-stu-id="bb372-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="bb372-156">4 단계: hello 배포를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="bb372-157">이제 SSH toohello 가상 컴퓨터 tooverify hello 배포 및 시작에 사용 하 여 만든 새 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="bb372-158">SSH 통해 tooconnect hello IP 주소 또는 FQDN으로 VM 찾을 [az vm 표시](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="bb372-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="bb372-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb372-159">Next steps</span></span>
<span data-ttu-id="bb372-160">원본 VM 이미지에서 여러 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="bb372-161">변경 내용을 tooyour 이미지 toomake 필요한 경우:</span><span class="sxs-lookup"><span data-stu-id="bb372-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="bb372-162">사용자 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-162">Create a VM from your image.</span></span>
- <span data-ttu-id="bb372-163">모든 업데이트 또는 구성 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="bb372-164">에 따라 hello 단계를 다시 toodeprovision, 할당 취소를 일반화 및 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="bb372-165">향후 배포에서 이 새로운 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-165">Use this new image for future deployments.</span></span> <span data-ttu-id="bb372-166">원하는 경우 hello 원본 이미지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="bb372-167">CLI hello로 Vm 관리에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 2.0](/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="bb372-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
