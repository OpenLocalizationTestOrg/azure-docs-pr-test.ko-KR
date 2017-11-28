---
title: "Azure에서 Linux VM aaaDifferent 방법 toocreate | Microsoft Azure"
description: "Hello 다양 한 방법 toocreate 링크 tootools 등 각 방법에 대 한 자습서는 Azure에서 Linux 가상 컴퓨터에 알아봅니다."
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
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="184d7-103">다양 한 방법 toocreate Linux VM</span><span class="sxs-lookup"><span data-stu-id="184d7-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="184d7-104">에 유연성이 있습니다 hello Azure toocreate 능숙 tooyou 도구 및 워크플로 사용 하 여 Linux 가상 컴퓨터 (VM).</span><span class="sxs-lookup"><span data-stu-id="184d7-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="184d7-105">이 문서에는 이러한 차이점과 hello Azure CLI 2.0을 포함 하 여 Linux Vm을 만들기 위한 예제가 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="184d7-106">Hello를 포함 하 여 만들기 옵션을 볼 수 있습니다 [Azure CLI 1.0](creation-choices-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="184d7-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) npm 패키지, 패키지, distro 제공 또는 Docker 컨테이너를 통해 플랫폼에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="184d7-108">사용자 환경에 대 한 hello 가장 적합 한 빌드를 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="184d7-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="184d7-109">Hello Azure CLI 2.0 여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="184d7-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="184d7-110">*myResourceGroup*이라는 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="184d7-111">사용 하 여 VM 만들기 [az vm 만들기](/cli/azure/vm#create) 라는 *myVM* 최신 hello를 사용 하 여 *UbuntuLTS* 이미지에 이미 존재 하지 않는 경우 SSH 키를 생성 및 *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="184d7-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="184d7-112">Azure 템플릿을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="184d7-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="184d7-113">hello 다음 예제에서는 [az 그룹 배포 만들기](/cli/azure/group/deployment#create) toocreate GitHub에 저장 된 템플릿에서 VM:</span><span class="sxs-lookup"><span data-stu-id="184d7-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="184d7-114">Linux VM을 만들고 cloud-init를 사용하여 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="184d7-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="184d7-115">여러 Linux VM에서 부하가 분산된 고가용성 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="184d7-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="184d7-116">Azure portal</span><span class="sxs-lookup"><span data-stu-id="184d7-116">Azure portal</span></span>
<span data-ttu-id="184d7-117">hello [Azure 포털](https://portal.azure.com) 있습니다 tooquickly 없기 때문에 VM을 만들 tooinstall 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="184d7-118">Hello Azure 포털 toocreate hello VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="184d7-119">Hello Azure 포털을 사용 하 여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="184d7-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="184d7-120">운영 체제 및 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="184d7-120">Operating system and image choices</span></span>
<span data-ttu-id="184d7-121">VM을 만들 때 운영 체제 toorun 원하는 hello를 기반으로 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="184d7-122">Azure 및 해당 파트너는 미리 설치된 응용 프로그램 및 도구를 포함하는 여러 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="184d7-123">또는 사용자 고유의 이미지 중 하나를 업로드 (참조 [섹션 다음 hello](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="184d7-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="184d7-124">Azure 이미지</span><span class="sxs-lookup"><span data-stu-id="184d7-124">Azure images</span></span>
<span data-ttu-id="184d7-125">사용 하 여 hello [az vm 이미지](/cli/azure/vm/image) 게시자, distro 릴리스 및 빌드에 따라 사용 가능한 란 toosee 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="184d7-126">사용 가능한 게시자 나열:</span><span class="sxs-lookup"><span data-stu-id="184d7-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="184d7-127">지정된 게시자에 사용 가능한 제품(제품) 나열:</span><span class="sxs-lookup"><span data-stu-id="184d7-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="184d7-128">지정된 제품 중 사용 가능한 SKU(배포판 릴리스) 나열:</span><span class="sxs-lookup"><span data-stu-id="184d7-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="184d7-129">지정된 릴리스에 사용 가능한 모든 이미지 나열:</span><span class="sxs-lookup"><span data-stu-id="184d7-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="184d7-130">검색 및 사용 가능한 이미지를 사용 하 여 더 많은 예제를 참조 하십시오. [탐색 하 고 hello Azure CLI를 사용 하 여 Azure 가상 컴퓨터 이미지 선택](cli-ps-findimage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="184d7-131">hello [az vm 만들기](/cli/azure/vm#create) 명령 tooquickly 액세스를 사용 하 여 별칭에는 일반적인 배포판 및 최신 버전의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="184d7-132">별칭을 사용 하 여 hello 게시자, 제품, SKU 및 버전을 지정 하는 VM을 만들 때 보다 신속 하 게 관리가:</span><span class="sxs-lookup"><span data-stu-id="184d7-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="184d7-133">Alias</span><span class="sxs-lookup"><span data-stu-id="184d7-133">Alias</span></span> | <span data-ttu-id="184d7-134">게시자</span><span class="sxs-lookup"><span data-stu-id="184d7-134">Publisher</span></span> | <span data-ttu-id="184d7-135">제안</span><span class="sxs-lookup"><span data-stu-id="184d7-135">Offer</span></span> | <span data-ttu-id="184d7-136">SKU</span><span class="sxs-lookup"><span data-stu-id="184d7-136">SKU</span></span> | <span data-ttu-id="184d7-137">버전</span><span class="sxs-lookup"><span data-stu-id="184d7-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="184d7-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="184d7-138">CentOS</span></span> |<span data-ttu-id="184d7-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="184d7-139">OpenLogic</span></span> |<span data-ttu-id="184d7-140">Centos</span><span class="sxs-lookup"><span data-stu-id="184d7-140">Centos</span></span> |<span data-ttu-id="184d7-141">7.2</span><span class="sxs-lookup"><span data-stu-id="184d7-141">7.2</span></span> |<span data-ttu-id="184d7-142">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-142">latest</span></span> |
| <span data-ttu-id="184d7-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="184d7-143">CoreOS</span></span> |<span data-ttu-id="184d7-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="184d7-144">CoreOS</span></span> |<span data-ttu-id="184d7-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="184d7-145">CoreOS</span></span> |<span data-ttu-id="184d7-146">Stable</span><span class="sxs-lookup"><span data-stu-id="184d7-146">Stable</span></span> |<span data-ttu-id="184d7-147">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-147">latest</span></span> |
| <span data-ttu-id="184d7-148">Debian</span><span class="sxs-lookup"><span data-stu-id="184d7-148">Debian</span></span> |<span data-ttu-id="184d7-149">credativ</span><span class="sxs-lookup"><span data-stu-id="184d7-149">credativ</span></span> |<span data-ttu-id="184d7-150">Debian</span><span class="sxs-lookup"><span data-stu-id="184d7-150">Debian</span></span> |<span data-ttu-id="184d7-151">8</span><span class="sxs-lookup"><span data-stu-id="184d7-151">8</span></span> |<span data-ttu-id="184d7-152">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-152">latest</span></span> |
| <span data-ttu-id="184d7-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="184d7-153">openSUSE</span></span> |<span data-ttu-id="184d7-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="184d7-154">SUSE</span></span> |<span data-ttu-id="184d7-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="184d7-155">openSUSE</span></span> |<span data-ttu-id="184d7-156">13.2</span><span class="sxs-lookup"><span data-stu-id="184d7-156">13.2</span></span> |<span data-ttu-id="184d7-157">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-157">latest</span></span> |
| <span data-ttu-id="184d7-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="184d7-158">RHEL</span></span> |<span data-ttu-id="184d7-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="184d7-159">Redhat</span></span> |<span data-ttu-id="184d7-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="184d7-160">RHEL</span></span> |<span data-ttu-id="184d7-161">7.2</span><span class="sxs-lookup"><span data-stu-id="184d7-161">7.2</span></span> |<span data-ttu-id="184d7-162">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-162">latest</span></span> |
| <span data-ttu-id="184d7-163">SLES</span><span class="sxs-lookup"><span data-stu-id="184d7-163">SLES</span></span> |<span data-ttu-id="184d7-164">SLES</span><span class="sxs-lookup"><span data-stu-id="184d7-164">SLES</span></span> |<span data-ttu-id="184d7-165">SLES</span><span class="sxs-lookup"><span data-stu-id="184d7-165">SLES</span></span> |<span data-ttu-id="184d7-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="184d7-166">12-SP1</span></span> |<span data-ttu-id="184d7-167">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-167">latest</span></span> |
| <span data-ttu-id="184d7-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="184d7-168">UbuntuLTS</span></span> |<span data-ttu-id="184d7-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="184d7-169">Canonical</span></span> |<span data-ttu-id="184d7-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="184d7-170">UbuntuServer</span></span> |<span data-ttu-id="184d7-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="184d7-171">14.04.4-LTS</span></span> |<span data-ttu-id="184d7-172">최신</span><span class="sxs-lookup"><span data-stu-id="184d7-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="184d7-173">사용자 고유의 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="184d7-173">Use your own image</span></span>
<span data-ttu-id="184d7-174">특정 사용자 지정이 필요한 경우 해당 VM을 캡처하여 기존 Azure VM을 기반으로 하는 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="184d7-175">이미지로 만든 온-프레미스를 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="184d7-176">지원 되는 배포판에 대 한 자세한 내용은 toouse 사용자 고유의 이미지를 확인 하려면 어떻게 해야 하 고 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="184d7-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="184d7-177">Azure 인증 배포</span><span class="sxs-lookup"><span data-stu-id="184d7-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="184d7-178">보증되지 않는 배포에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="184d7-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="184d7-179">[어떻게 toocreate 기존 Azure VM에서 이미지](tutorial-custom-images.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="184d7-180">빠른 시작 예제에서는 기존 Azure VM에서 이미지 toocreate 명령:</span><span class="sxs-lookup"><span data-stu-id="184d7-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="184d7-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="184d7-181">Next steps</span></span>
* <span data-ttu-id="184d7-182">Hello로 Linux VM을 만들 [CLI](quick-create-cli.md), hello에서 [포털](quick-create-portal.md), 또는 사용 하는 [Azure 리소스 관리자 템플릿](../windows/cli-deploy-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="184d7-183">Linux VM을 만든 후 [Azure 디스크 및 저장소에 대해 알아봅니다](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="184d7-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="184d7-184">빠른 단계 너무[암호 또는 SSH 키를 다시 설정 하 고 사용자 관리](using-vmaccess-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="184d7-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
