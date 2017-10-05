---
title: "Azure에서 Linux VM을 만드는 다양한 방법 | Microsoft Azure"
description: "각 방법에 대한 도구 및 자습서를 비롯하여 Azure에 Linux 가상 컴퓨터를 만드는 다양한 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="07f5a-103">Linux VM을 만드는 다양한 방법</span><span class="sxs-lookup"><span data-stu-id="07f5a-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="07f5a-104">Azure에는 편리한 도구와 워크플로를 사용하여 Linux VM(가상 컴퓨터)을 만드는 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="07f5a-105">이 문서에서는 Azure CLI 2.0을 포함하여 Linux 가상 컴퓨터를 만드는 경우의 차이점과 옵션을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="07f5a-106">[Azure CLI 1.0](creation-choices-nodejs.md)을 포함하여 만들기 선택 항목을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="07f5a-107">[Azure CLI 2.0](/cli/azure/install-az-cli2)은 npm 패키지, 배포판 제공 패키지 또는 Docker 컨테이너를 통해 여러 플랫폼에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="07f5a-108">[az login](/cli/azure/#login)을 사용하여 Azure 계정에 환경 및 로그인에 가장 적합한 빌드를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="07f5a-109">Azure CLI 2.0을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="07f5a-109">Create a Linux VM with the Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="07f5a-110">*myResourceGroup*이라는 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="07f5a-111">최신 *UbuntuLTS* 이미지를 사용하여 *myVM*이라는 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들고 *~/.ssh*에 없는 경우 SSH 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="07f5a-112">Azure 템플릿을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="07f5a-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="07f5a-113">다음 예제에서는 GitHub에 저장된 템플릿에서 VM을 만들기 위해 [az group deployment create](/cli/azure/group/deployment#create)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="07f5a-114">Linux VM을 만들고 cloud-init를 사용하여 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="07f5a-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="07f5a-115">여러 Linux VM에서 부하가 분산된 고가용성 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="07f5a-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="07f5a-116">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="07f5a-116">Azure portal</span></span>
<span data-ttu-id="07f5a-117">[Azure Portal](https://portal.azure.com) 을 사용하면 시스템에 설치할 프로그램이 없으므로 VM을 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="07f5a-118">Azure 포털을 사용하여 다음과 같이 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="07f5a-119">Azure 포털을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="07f5a-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="07f5a-120">운영 체제 및 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="07f5a-120">Operating system and image choices</span></span>
<span data-ttu-id="07f5a-121">VM을 만드는 경우 실행하려는 운영 체제에 따라 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="07f5a-122">Azure 및 해당 파트너는 미리 설치된 응용 프로그램 및 도구를 포함하는 여러 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="07f5a-123">또는 사용자 고유의 이미지 중 하나를 업로드합니다( [다음 섹션](#use-your-own-image)을 참조).</span><span class="sxs-lookup"><span data-stu-id="07f5a-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="07f5a-124">Azure 이미지</span><span class="sxs-lookup"><span data-stu-id="07f5a-124">Azure images</span></span>
<span data-ttu-id="07f5a-125">[az vm image](/cli/azure/vm/image) 명령을 사용하여 게시자, 배포판 릴리스 및 빌드에 따라 사용 가능한 기능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="07f5a-126">사용 가능한 게시자 나열:</span><span class="sxs-lookup"><span data-stu-id="07f5a-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="07f5a-127">지정된 게시자에 사용 가능한 제품(제품) 나열:</span><span class="sxs-lookup"><span data-stu-id="07f5a-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="07f5a-128">지정된 제품 중 사용 가능한 SKU(배포판 릴리스) 나열:</span><span class="sxs-lookup"><span data-stu-id="07f5a-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="07f5a-129">지정된 릴리스에 사용 가능한 모든 이미지 나열:</span><span class="sxs-lookup"><span data-stu-id="07f5a-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="07f5a-130">사용 가능한 이미지 검색 및 사용에 대한 추가 예제는 [Azure CLI를 사용하여 Azure 가상 컴퓨터 이미지 탐색 및 선택](cli-ps-findimage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07f5a-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="07f5a-131">[az vm create](/cli/azure/vm#create) 명령에는 일반적인 배포판 및 해당 최신 릴리스에 빠르게 액세스하는 데 사용할 수 있는 몇 가지 별칭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="07f5a-132">별칭을 사용하는 방법이 VM을 만들 때마다 게시자, 제품, SKU 및 버전을 지정하는 것보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="07f5a-133">Alias</span><span class="sxs-lookup"><span data-stu-id="07f5a-133">Alias</span></span> | <span data-ttu-id="07f5a-134">게시자</span><span class="sxs-lookup"><span data-stu-id="07f5a-134">Publisher</span></span> | <span data-ttu-id="07f5a-135">제안</span><span class="sxs-lookup"><span data-stu-id="07f5a-135">Offer</span></span> | <span data-ttu-id="07f5a-136">SKU</span><span class="sxs-lookup"><span data-stu-id="07f5a-136">SKU</span></span> | <span data-ttu-id="07f5a-137">버전</span><span class="sxs-lookup"><span data-stu-id="07f5a-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="07f5a-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="07f5a-138">CentOS</span></span> |<span data-ttu-id="07f5a-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="07f5a-139">OpenLogic</span></span> |<span data-ttu-id="07f5a-140">Centos</span><span class="sxs-lookup"><span data-stu-id="07f5a-140">Centos</span></span> |<span data-ttu-id="07f5a-141">7.2</span><span class="sxs-lookup"><span data-stu-id="07f5a-141">7.2</span></span> |<span data-ttu-id="07f5a-142">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-142">latest</span></span> |
| <span data-ttu-id="07f5a-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="07f5a-143">CoreOS</span></span> |<span data-ttu-id="07f5a-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="07f5a-144">CoreOS</span></span> |<span data-ttu-id="07f5a-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="07f5a-145">CoreOS</span></span> |<span data-ttu-id="07f5a-146">Stable</span><span class="sxs-lookup"><span data-stu-id="07f5a-146">Stable</span></span> |<span data-ttu-id="07f5a-147">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-147">latest</span></span> |
| <span data-ttu-id="07f5a-148">Debian</span><span class="sxs-lookup"><span data-stu-id="07f5a-148">Debian</span></span> |<span data-ttu-id="07f5a-149">credativ</span><span class="sxs-lookup"><span data-stu-id="07f5a-149">credativ</span></span> |<span data-ttu-id="07f5a-150">Debian</span><span class="sxs-lookup"><span data-stu-id="07f5a-150">Debian</span></span> |<span data-ttu-id="07f5a-151">8</span><span class="sxs-lookup"><span data-stu-id="07f5a-151">8</span></span> |<span data-ttu-id="07f5a-152">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-152">latest</span></span> |
| <span data-ttu-id="07f5a-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="07f5a-153">openSUSE</span></span> |<span data-ttu-id="07f5a-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="07f5a-154">SUSE</span></span> |<span data-ttu-id="07f5a-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="07f5a-155">openSUSE</span></span> |<span data-ttu-id="07f5a-156">13.2</span><span class="sxs-lookup"><span data-stu-id="07f5a-156">13.2</span></span> |<span data-ttu-id="07f5a-157">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-157">latest</span></span> |
| <span data-ttu-id="07f5a-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="07f5a-158">RHEL</span></span> |<span data-ttu-id="07f5a-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="07f5a-159">Redhat</span></span> |<span data-ttu-id="07f5a-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="07f5a-160">RHEL</span></span> |<span data-ttu-id="07f5a-161">7.2</span><span class="sxs-lookup"><span data-stu-id="07f5a-161">7.2</span></span> |<span data-ttu-id="07f5a-162">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-162">latest</span></span> |
| <span data-ttu-id="07f5a-163">SLES</span><span class="sxs-lookup"><span data-stu-id="07f5a-163">SLES</span></span> |<span data-ttu-id="07f5a-164">SLES</span><span class="sxs-lookup"><span data-stu-id="07f5a-164">SLES</span></span> |<span data-ttu-id="07f5a-165">SLES</span><span class="sxs-lookup"><span data-stu-id="07f5a-165">SLES</span></span> |<span data-ttu-id="07f5a-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="07f5a-166">12-SP1</span></span> |<span data-ttu-id="07f5a-167">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-167">latest</span></span> |
| <span data-ttu-id="07f5a-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="07f5a-168">UbuntuLTS</span></span> |<span data-ttu-id="07f5a-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="07f5a-169">Canonical</span></span> |<span data-ttu-id="07f5a-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="07f5a-170">UbuntuServer</span></span> |<span data-ttu-id="07f5a-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="07f5a-171">14.04.4-LTS</span></span> |<span data-ttu-id="07f5a-172">최신</span><span class="sxs-lookup"><span data-stu-id="07f5a-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="07f5a-173">사용자 고유의 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="07f5a-173">Use your own image</span></span>
<span data-ttu-id="07f5a-174">특정 사용자 지정이 필요한 경우 해당 VM을 캡처하여 기존 Azure VM을 기반으로 하는 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="07f5a-175">이미지로 만든 온-프레미스를 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="07f5a-176">지원되는 배포판 및 사용자 고유의 이미지를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07f5a-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="07f5a-177">Azure 인증 배포</span><span class="sxs-lookup"><span data-stu-id="07f5a-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="07f5a-178">보증되지 않는 배포에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="07f5a-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="07f5a-179">[기존 Azure VM에서 이미지를 만드는 방법](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="07f5a-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="07f5a-180">기존 Azure VM에서 이미지를 만드는 빠른 시작 예제 명령:</span><span class="sxs-lookup"><span data-stu-id="07f5a-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="07f5a-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07f5a-181">Next steps</span></span>
* <span data-ttu-id="07f5a-182">[CLI](quick-create-cli.md)로 [포털](quick-create-portal.md)에서 Linux VM을 만들거나 [Azure Resource Manager 템플릿](../windows/cli-deploy-templates.md)을 사용하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07f5a-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="07f5a-183">Linux VM을 만든 후 [Azure 디스크 및 저장소에 대해 알아봅니다](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="07f5a-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="07f5a-184">[암호 또는 SSH 키를 다시 설정하고 사용자를 관리](using-vmaccess-extension.md)하는 빠른 단계.</span><span class="sxs-lookup"><span data-stu-id="07f5a-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
