---
title: "CLI 2.0을 사용하여 Azure에서 Linux VM의 이미지 캡처 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 대량 배포에 사용할 Azure VM의 이미지를 캡처합니다."
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
ms.openlocfilehash: 19b573f77f2ee84600955d00d30bdb16c84e3623
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="55ea7-103">가상 컴퓨터 또는 VHD의 이미지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55ea7-103">How to create an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of the tutorial-->

<span data-ttu-id="55ea7-104">Azure에서 사용할 가상 컴퓨터(VM)의 복사본을 여러 개 만들려면 VM 또는 OS VHD의 이미지를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span></span> <span data-ttu-id="55ea7-105">이미지를 만들려면 개인 계정 정보를 제거해야 합니다. 이렇게 해야 여러 번 배포하는 데 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span></span> <span data-ttu-id="55ea7-106">다음 단계에서는 기존 VM의 프로비전을 해제하고, 할당을 취소하고, 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="55ea7-107">이 이미지를 사용하여 구독 내의 모든 리소스 그룹에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-107">You can use this image to create VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="55ea7-108">백업 또는 디버깅을 위해 기존 Linux VM의 복사본을 만들거나 온-프레미스 VM에서 특수한 Linux VHD를 업로드하려면 [사용자 지정 디스크 이미지에서 Linux VM 업로드 및 만들기](upload-vhd.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ea7-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="55ea7-109">**Packer**를 사용하여 사용자 지정 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-109">You can also use **Packer** to create your custom configuration.</span></span> <span data-ttu-id="55ea7-110">Packer 사용에 대한 자세한 내용은 [Azure에서 Packer를 사용하여 Linux 가상 컴퓨터 이미지를 만드는 방법](build-image-with-packer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ea7-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="55ea7-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="55ea7-111">Before you begin</span></span>
<span data-ttu-id="55ea7-112">다음 필수 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-112">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="55ea7-113">관리 디스크를 사용하여 Resource Manager 배포 모델에서 만든 Azure VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="55ea7-114">Linux VM을 만들지 않은 경우 [포털](quick-create-portal.md), [Azure CLI](quick-create-cli.md) 또는 [Resource Manager 템플릿](create-ssh-secured-vm-from-template.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="55ea7-115">필요에 따라 VM을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-115">Configure the VM as needed.</span></span> <span data-ttu-id="55ea7-116">예를 들어 [데이터 디스크를 추가하고](add-disk.md), 업데이트를 적용하고, 응용 프로그램을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="55ea7-117">또한 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)이 설치되어 있어 [az login](/cli/azure/#login)으로 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="55ea7-118">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="55ea7-118">Quick commands</span></span>

<span data-ttu-id="55ea7-119">이 항목에 대한 간소화된 설명이나 Azure VM에 대한 테스트, 평가 또는 학습에 대해 알아보려면 [CLI를 사용하여 Azure VM의 사용자 지정 이미지 만들기](tutorial-custom-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ea7-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-the-vm"></a><span data-ttu-id="55ea7-120">1단계: VM 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="55ea7-120">Step 1: Deprovision the VM</span></span>
<span data-ttu-id="55ea7-121">Azure VM 에이전트로 VM 프로비전을 해제하여 컴퓨터 특정 파일 및 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span></span> <span data-ttu-id="55ea7-122">원본 Linux VM에서 *-deprovision+user* 매개 변수와 함께 `waagent` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="55ea7-123">자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../windows/agent-user-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ea7-123">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="55ea7-124">SSH 클라이언트를 사용하여 Linux VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-124">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="55ea7-125">SSH 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-125">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="55ea7-126">이미지로 캡처하려는 VM에서만 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-126">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="55ea7-127">이 과정이 이미지에서 중요한 정보가 모두 지워졌다거나 재배포에 적합하다는 것을 보장하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="55ea7-128">*+user* 매개 변수는 마지막 프로비전된 사용자 계정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-128">The *+user* parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="55ea7-129">VM에 계정 자격 증명을 유지하려면 *-deprovision*을 사용하여 사용자 계정을 현재 위치에 유지하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span></span>
 
3. <span data-ttu-id="55ea7-130">계속하려면 **y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-130">Type **y** to continue.</span></span> <span data-ttu-id="55ea7-131">이 확인 단계를 피하려면 **-force** 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-131">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="55ea7-132">명령이 완료된 후 **exit**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-132">After the command completes, type **exit**.</span></span> <span data-ttu-id="55ea7-133">이 단계는 SSH 클라이언트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-133">This step closes the SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="55ea7-134">2단계: VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="55ea7-134">Step 2: Create VM image</span></span>
<span data-ttu-id="55ea7-135">Azure CLI 2.0을 사용하여 VM을 일반화된 항목으로 표시하고 이미지를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span></span> <span data-ttu-id="55ea7-136">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-136">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="55ea7-137">예제 매개 변수 이름에는 *myResourceGroup*, *myVnet*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="55ea7-138">[az vm deallocate](/cli//azure/vm#deallocate)로 프로비전 해제한 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="55ea7-139">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM의 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="55ea7-140">[az vm generalize](/cli//azure/vm#generalize)를 사용하여 VM을 일반화된 항목으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="55ea7-141">다음 예제에서는 리소스 그룹 *myResourceGroup*에서 *myVM*이라는 VM을 일반화된 항목으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-141">The following example marks the the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="55ea7-142">이제 [az image create](/cli//azure/image#create)로 VM 리소스의 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-142">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="55ea7-143">다음 예제에서는 *myVM*이라는 VM 리소스를 사용하여 *myResourceGroup*이라는 리소스 그룹에서 *myImage*라는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="55ea7-144">이미지는 원본 VM과 동일한 리소스 그룹에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-144">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="55ea7-145">이 이미지에서 구독 내의 모든 리소스 그룹에 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="55ea7-146">관리 측면에서 VM 리소스 및 이미지에 대한 특정 리소스 그룹을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="55ea7-147">3단계: 캡처한 이미지로부터 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="55ea7-147">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="55ea7-148">[az vm create](/cli/azure/vm#create)로 만든 이미지를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-148">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="55ea7-149">다음 예제에서는 *myImage*라는 이미지에서 *myVMDeployed*라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-149">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-the-vm-in-another-resource-group"></a><span data-ttu-id="55ea7-150">다른 리소스 그룹에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="55ea7-150">Creating the VM in another resource group</span></span> 

<span data-ttu-id="55ea7-151">구독 내 모든 리소스 그룹의 이미지에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="55ea7-152">이미지와 다른 리소스 그룹에 VM을 만들려면 이미지에 완전한 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-152">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="55ea7-153">[az image list](/cli/azure/image#list)를 사용하여 이미지 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-153">Use [az image list](/cli/azure/image#list) to view a list of images.</span></span> <span data-ttu-id="55ea7-154">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-154">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="55ea7-155">다음 예제에서는 이미지 리소스 ID를 지정하여 원본 이미지와 다른 리소스 그룹에 VM을 만드는 [az vm create](/cli/azure/vm#create)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-155">The following example uses [az vm create](/cli/azure/vm#create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-the-deployment"></a><span data-ttu-id="55ea7-156">4단계: 배포 확인</span><span class="sxs-lookup"><span data-stu-id="55ea7-156">Step 4: Verify the deployment</span></span>

<span data-ttu-id="55ea7-157">생성한 가상 컴퓨터에 SSH를 실행하여 배포를 확인하고 새 VM 사용을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-157">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="55ea7-158">SSH를 통해 연결하려면 [az vm show](/cli/azure/vm#show)로 VM의 IP 주소 또는 FQDN을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-158">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="55ea7-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55ea7-159">Next steps</span></span>
<span data-ttu-id="55ea7-160">원본 VM 이미지에서 여러 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="55ea7-161">이미지를 변경해야 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="55ea7-161">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="55ea7-162">사용자 이미지에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-162">Create a VM from your image.</span></span>
- <span data-ttu-id="55ea7-163">모든 업데이트 또는 구성 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="55ea7-164">단계에 따라 이미지를 다시 프로비전 해제, 할당 취소, 일반화하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-164">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="55ea7-165">향후 배포에서 이 새로운 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-165">Use this new image for future deployments.</span></span> <span data-ttu-id="55ea7-166">원하는 경우에 원본 이미지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="55ea7-166">If desired, delete the original image.</span></span>

<span data-ttu-id="55ea7-167">CLI를 사용하여 VM을 관리하는 방법에 대한 자세한 내용은 [Azure CLI 2.0](/cli/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55ea7-167">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
