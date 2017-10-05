---
title: "Azure CLI 1.0을 사용하여 Linux VM을 만드는 다양한 방법 | Microsoft Docs"
description: "각 방법에 대한 도구 및 자습서를 비롯하여 Azure에 Linux 가상 컴퓨터를 만드는 다양한 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="26f52-103">Azure에서 Linux 가상 컴퓨터를 만드는 다양한 방법</span><span class="sxs-lookup"><span data-stu-id="26f52-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="26f52-104">Azure에는 편리한 도구와 워크플로를 사용하여 Linux VM(가상 컴퓨터)을 만드는 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="26f52-105">이 문서에서는 Linux 가상 컴퓨터를 만드는 경우의 차이점과 옵션을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="26f52-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26f52-106">Azure CLI</span></span>
<span data-ttu-id="26f52-107">다음 CLI 버전 중 하나를 사용하여 Azure에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="26f52-108">Azure CLI 1.0 - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="26f52-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="26f52-109">[Azure CLI 2.0](../windows/creation-choices.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="26f52-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="26f52-110">Azure CLI 1.0은 npm 패키지, 배포판 제공 패키지 또는 Docker 컨테이너를 통해 여러 플랫폼에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="26f52-111">[Azure CLI를 설치하고 구성하는 방법](../../cli-install-nodejs.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="26f52-112">다음 자습서에서는 Azure CLI 1.0을 사용하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="26f52-113">다음과 같이 표시되는 CLI 빠른 시작 명령에 대한 자세한 내용은 각 문서를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="26f52-114">개발 및 테스트를 위해 Azure CLI에서 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="26f52-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="26f52-115">다음 예제에서는 *azure_id_rsa.pub*라는 공개 키를 사용하여 CoreOS VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="26f52-116">Azure 템플릿을 사용하여 안전한 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="26f52-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="26f52-117">다음 예제에서는 GitHub에 저장된 템플릿을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="26f52-118">Azure CLI를 사용하여 완전한 Linux 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="26f52-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="26f52-119">가용성 집합에서 부하 분산 장치 및 여러 VM을 만드는 방법이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="26f52-120">Linux VM에 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="26f52-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="26f52-121">다음 예제에서는 *myVM*라는 기존 VM에 *5*GB 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="26f52-122">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="26f52-122">Azure portal</span></span>
<span data-ttu-id="26f52-123">[Azure Portal](https://portal.azure.com) 을 사용하면 시스템에 설치할 프로그램이 없으므로 VM을 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="26f52-124">Azure 포털을 사용하여 다음과 같이 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="26f52-125">Azure 포털을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="26f52-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="26f52-126">운영 체제 및 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="26f52-126">Operating system and image choices</span></span>
<span data-ttu-id="26f52-127">VM을 만드는 경우 실행하려는 운영 체제에 따라 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="26f52-128">Azure 및 해당 파트너는 미리 설치된 응용 프로그램 및 도구를 포함하는 여러 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="26f52-129">또는 사용자 고유의 이미지 중 하나를 업로드합니다( [다음 섹션](#use-your-own-image)을 참조).</span><span class="sxs-lookup"><span data-stu-id="26f52-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="26f52-130">Azure 이미지</span><span class="sxs-lookup"><span data-stu-id="26f52-130">Azure images</span></span>
<span data-ttu-id="26f52-131">`azure vm image` CLI 명령을 사용하여 게시자, 배포판 릴리스 및 빌드에 따라 사용 가능한 기능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="26f52-132">사용 가능한 게시자를 다음과 같이 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="26f52-133">지정된 게시자에 사용 가능한 제품(제품)을 다음과 같이 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="26f52-134">지정된 제품 중 사용 가능한 SKU(배포판 릴리스)를 다음과 같이 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="26f52-135">지정된 릴리스에 사용 가능한 모든 이미지를 다음과 같이 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="26f52-136">`azure vm quick-create` 및 `azure vm create` 명령에는 일반적인 배포판 및 해당 최신 릴리스에 신속하게 액세스하는 데 사용할 수 있는 몇 가지 별칭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="26f52-137">별칭을 사용하는 방법이 VM을 만들 때마다 게시자, 제품, SKU 및 버전을 지정하는 것보다 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="26f52-138">Alias</span><span class="sxs-lookup"><span data-stu-id="26f52-138">Alias</span></span> | <span data-ttu-id="26f52-139">게시자</span><span class="sxs-lookup"><span data-stu-id="26f52-139">Publisher</span></span> | <span data-ttu-id="26f52-140">제안</span><span class="sxs-lookup"><span data-stu-id="26f52-140">Offer</span></span> | <span data-ttu-id="26f52-141">SKU</span><span class="sxs-lookup"><span data-stu-id="26f52-141">SKU</span></span> | <span data-ttu-id="26f52-142">버전</span><span class="sxs-lookup"><span data-stu-id="26f52-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="26f52-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="26f52-143">CentOS</span></span> |<span data-ttu-id="26f52-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="26f52-144">OpenLogic</span></span> |<span data-ttu-id="26f52-145">Centos</span><span class="sxs-lookup"><span data-stu-id="26f52-145">Centos</span></span> |<span data-ttu-id="26f52-146">7.2</span><span class="sxs-lookup"><span data-stu-id="26f52-146">7.2</span></span> |<span data-ttu-id="26f52-147">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-147">latest</span></span> |
| <span data-ttu-id="26f52-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26f52-148">CoreOS</span></span> |<span data-ttu-id="26f52-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26f52-149">CoreOS</span></span> |<span data-ttu-id="26f52-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26f52-150">CoreOS</span></span> |<span data-ttu-id="26f52-151">Stable</span><span class="sxs-lookup"><span data-stu-id="26f52-151">Stable</span></span> |<span data-ttu-id="26f52-152">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-152">latest</span></span> |
| <span data-ttu-id="26f52-153">Debian</span><span class="sxs-lookup"><span data-stu-id="26f52-153">Debian</span></span> |<span data-ttu-id="26f52-154">credativ</span><span class="sxs-lookup"><span data-stu-id="26f52-154">credativ</span></span> |<span data-ttu-id="26f52-155">Debian</span><span class="sxs-lookup"><span data-stu-id="26f52-155">Debian</span></span> |<span data-ttu-id="26f52-156">8</span><span class="sxs-lookup"><span data-stu-id="26f52-156">8</span></span> |<span data-ttu-id="26f52-157">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-157">latest</span></span> |
| <span data-ttu-id="26f52-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="26f52-158">openSUSE</span></span> |<span data-ttu-id="26f52-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="26f52-159">SUSE</span></span> |<span data-ttu-id="26f52-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="26f52-160">openSUSE</span></span> |<span data-ttu-id="26f52-161">13.2</span><span class="sxs-lookup"><span data-stu-id="26f52-161">13.2</span></span> |<span data-ttu-id="26f52-162">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-162">latest</span></span> |
| <span data-ttu-id="26f52-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="26f52-163">RHEL</span></span> |<span data-ttu-id="26f52-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="26f52-164">Redhat</span></span> |<span data-ttu-id="26f52-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="26f52-165">RHEL</span></span> |<span data-ttu-id="26f52-166">7.2</span><span class="sxs-lookup"><span data-stu-id="26f52-166">7.2</span></span> |<span data-ttu-id="26f52-167">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-167">latest</span></span> |
| <span data-ttu-id="26f52-168">SLES</span><span class="sxs-lookup"><span data-stu-id="26f52-168">SLES</span></span> |<span data-ttu-id="26f52-169">SLES</span><span class="sxs-lookup"><span data-stu-id="26f52-169">SLES</span></span> |<span data-ttu-id="26f52-170">SLES</span><span class="sxs-lookup"><span data-stu-id="26f52-170">SLES</span></span> |<span data-ttu-id="26f52-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="26f52-171">12-SP1</span></span> |<span data-ttu-id="26f52-172">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-172">latest</span></span> |
| <span data-ttu-id="26f52-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="26f52-173">UbuntuLTS</span></span> |<span data-ttu-id="26f52-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="26f52-174">Canonical</span></span> |<span data-ttu-id="26f52-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="26f52-175">UbuntuServer</span></span> |<span data-ttu-id="26f52-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="26f52-176">14.04.4-LTS</span></span> |<span data-ttu-id="26f52-177">최신</span><span class="sxs-lookup"><span data-stu-id="26f52-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="26f52-178">사용자 고유의 이미지 사용</span><span class="sxs-lookup"><span data-stu-id="26f52-178">Use your own image</span></span>
<span data-ttu-id="26f52-179">특정 사용자 지정이 필요한 경우 해당 VM을 *캡처* 하여 기존 Azure VM을 기반으로 하는 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="26f52-180">이미지로 만든 온-프레미스를 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="26f52-181">지원되는 배포판 및 사용자 고유의 이미지를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26f52-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="26f52-182">Azure 인증 배포</span><span class="sxs-lookup"><span data-stu-id="26f52-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="26f52-183">보증되지 않는 배포에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="26f52-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="26f52-184">사용자 지정 디스크 이미지에서 Linux VM 업로드 및 만들기</span><span class="sxs-lookup"><span data-stu-id="26f52-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="26f52-185">[Linux 가상 컴퓨터를 Resource Manager 템플릿으로 캡처하는 방법](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="26f52-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="26f52-186">기존 VM을 캡처하는 빠른 시작 예제 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="26f52-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26f52-187">Next steps</span></span>
* <span data-ttu-id="26f52-188">[CLI](quick-create-cli.md)로 [포털](quick-create-portal.md)에서 Linux VM을 만들거나 [Azure Resource Manager 템플릿](../windows/cli-deploy-templates.md)을 사용하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26f52-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="26f52-189">Linux VM을 만든 후에 [데이터 디스크를 추가합니다](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="26f52-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="26f52-190">[암호 또는 SSH 키 다시 설정 및 사용자 관리](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="26f52-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

