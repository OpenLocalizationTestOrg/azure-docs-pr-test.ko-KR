---
title: "Azure에서 cloud-init를 사용하여 생성 중인 Linux VM 사용자 지정 | Microsoft Docs"
description: "Azure CLI 1.0에서 cloud-init를 사용하여 생성 중인 Linux VM을 사용자 지정하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="b4a78-103">Azure CLI 1.0에서 cloud-init를 사용하여 생성 중인 Linux VM 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b4a78-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="b4a78-104">이 문서에서는 cloud-init 스크립트를 사용하여 호스트 이름 설정, 설치된 패키지 업데이트, 사용자 계정 관리를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="b4a78-105">VM을 만드는 중에 Azure CLI에서 cloud-init 스크립트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="b4a78-106">이 문서의 내용을 실행하기 위해 필요한 사항:</span><span class="sxs-lookup"><span data-stu-id="b4a78-106">The article requires:</span></span>

* <span data-ttu-id="b4a78-107">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="b4a78-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b4a78-108">`azure login`으로 로그인된 [Azure CLI](../../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="b4a78-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b4a78-109">Azure Resource Manager 모드 `azure config mode arm`으로 *있어야 하는* Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4a78-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b4a78-110">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="b4a78-110">CLI versions to complete the task</span></span>
<span data-ttu-id="b4a78-111">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b4a78-112">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="b4a78-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b4a78-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="b4a78-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b4a78-114">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="b4a78-114">Quick Commands</span></span>
<span data-ttu-id="b4a78-115">호스트 이름을 설정하고, 모든 패키지를 업데이트하고, Linux에 sudo 사용자를 추가하는 cloud-init.txt 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
<span data-ttu-id="b4a78-116">VM을 시작할 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b4a78-117">cloud-init을 사용해 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b4a78-118">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="b4a78-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="b4a78-119">소개</span><span class="sxs-lookup"><span data-stu-id="b4a78-119">Introduction</span></span>
<span data-ttu-id="b4a78-120">새 Linux VM을 시작하면 사용자 지정된 사항이나 사용자의 요구에 맞게 준비된 기능이 없는 표준 Linux VM이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="b4a78-121">[cloud-init](https://cloudinit.readthedocs.org) 은 Linux VM을 처음으로 부팅할 때 해당 VM에 스크립트 또는 구성 설정을 삽입하는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="b4a78-122">Azure에서는 다음의 세 가지 방법으로 배포 또는 부팅 중인 Linux VM을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="b4a78-123">cloud-init을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="b4a78-124">Azure [VMAccess 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="b4a78-125">Azure 템플릿을 사용합니다(cloud-init 사용).</span><span class="sxs-lookup"><span data-stu-id="b4a78-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="b4a78-126">Azure 템플릿을 사용합니다( [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)사용).</span><span class="sxs-lookup"><span data-stu-id="b4a78-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b4a78-127">부팅 후에 언제든지 스크립트를 삽입하려면 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="b4a78-128">SSH를 통해 명령을 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-128">SSH to run commands directly</span></span>
* <span data-ttu-id="b4a78-129">Azure [VMAccess 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 명령적으로 또는 Azure 템플릿에서 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="b4a78-130">Ansible, Salt, Chef, Puppet 등의 구성 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a78-131">: VMAccess 확장은 SSH를 사용할 때와 같은 방식으로 스크립트를 루트로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="b4a78-132">그러나 VM 확장 사용 시에는 시나리오에 따라 유용할 수 있는 다양한 Azure 제공 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="b4a78-133">Azure VM 빨리 만들기 이미지 별칭에 대한 cloud-init 사용 가능 여부</span><span class="sxs-lookup"><span data-stu-id="b4a78-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="b4a78-134">Alias</span><span class="sxs-lookup"><span data-stu-id="b4a78-134">Alias</span></span> | <span data-ttu-id="b4a78-135">게시자</span><span class="sxs-lookup"><span data-stu-id="b4a78-135">Publisher</span></span> | <span data-ttu-id="b4a78-136">제안</span><span class="sxs-lookup"><span data-stu-id="b4a78-136">Offer</span></span> | <span data-ttu-id="b4a78-137">SKU</span><span class="sxs-lookup"><span data-stu-id="b4a78-137">SKU</span></span> | <span data-ttu-id="b4a78-138">버전</span><span class="sxs-lookup"><span data-stu-id="b4a78-138">Version</span></span> | <span data-ttu-id="b4a78-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="b4a78-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b4a78-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4a78-140">CentOS</span></span> |<span data-ttu-id="b4a78-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b4a78-141">OpenLogic</span></span> |<span data-ttu-id="b4a78-142">Centos</span><span class="sxs-lookup"><span data-stu-id="b4a78-142">Centos</span></span> |<span data-ttu-id="b4a78-143">7.2</span><span class="sxs-lookup"><span data-stu-id="b4a78-143">7.2</span></span> |<span data-ttu-id="b4a78-144">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-144">latest</span></span> |<span data-ttu-id="b4a78-145">no</span><span class="sxs-lookup"><span data-stu-id="b4a78-145">no</span></span> |
| <span data-ttu-id="b4a78-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4a78-146">CoreOS</span></span> |<span data-ttu-id="b4a78-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4a78-147">CoreOS</span></span> |<span data-ttu-id="b4a78-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4a78-148">CoreOS</span></span> |<span data-ttu-id="b4a78-149">Stable</span><span class="sxs-lookup"><span data-stu-id="b4a78-149">Stable</span></span> |<span data-ttu-id="b4a78-150">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-150">latest</span></span> |<span data-ttu-id="b4a78-151">yes</span><span class="sxs-lookup"><span data-stu-id="b4a78-151">yes</span></span> |
| <span data-ttu-id="b4a78-152">Debian</span><span class="sxs-lookup"><span data-stu-id="b4a78-152">Debian</span></span> |<span data-ttu-id="b4a78-153">credativ</span><span class="sxs-lookup"><span data-stu-id="b4a78-153">credativ</span></span> |<span data-ttu-id="b4a78-154">Debian</span><span class="sxs-lookup"><span data-stu-id="b4a78-154">Debian</span></span> |<span data-ttu-id="b4a78-155">8</span><span class="sxs-lookup"><span data-stu-id="b4a78-155">8</span></span> |<span data-ttu-id="b4a78-156">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-156">latest</span></span> |<span data-ttu-id="b4a78-157">no</span><span class="sxs-lookup"><span data-stu-id="b4a78-157">no</span></span> |
| <span data-ttu-id="b4a78-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b4a78-158">openSUSE</span></span> |<span data-ttu-id="b4a78-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="b4a78-159">SUSE</span></span> |<span data-ttu-id="b4a78-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b4a78-160">openSUSE</span></span> |<span data-ttu-id="b4a78-161">13.2</span><span class="sxs-lookup"><span data-stu-id="b4a78-161">13.2</span></span> |<span data-ttu-id="b4a78-162">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-162">latest</span></span> |<span data-ttu-id="b4a78-163">no</span><span class="sxs-lookup"><span data-stu-id="b4a78-163">no</span></span> |
| <span data-ttu-id="b4a78-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4a78-164">RHEL</span></span> |<span data-ttu-id="b4a78-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="b4a78-165">Redhat</span></span> |<span data-ttu-id="b4a78-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4a78-166">RHEL</span></span> |<span data-ttu-id="b4a78-167">7.2</span><span class="sxs-lookup"><span data-stu-id="b4a78-167">7.2</span></span> |<span data-ttu-id="b4a78-168">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-168">latest</span></span> |<span data-ttu-id="b4a78-169">no</span><span class="sxs-lookup"><span data-stu-id="b4a78-169">no</span></span> |
| <span data-ttu-id="b4a78-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="b4a78-170">UbuntuLTS</span></span> |<span data-ttu-id="b4a78-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="b4a78-171">Canonical</span></span> |<span data-ttu-id="b4a78-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b4a78-172">UbuntuServer</span></span> |<span data-ttu-id="b4a78-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="b4a78-173">14.04.4-LTS</span></span> |<span data-ttu-id="b4a78-174">최신</span><span class="sxs-lookup"><span data-stu-id="b4a78-174">latest</span></span> |<span data-ttu-id="b4a78-175">yes</span><span class="sxs-lookup"><span data-stu-id="b4a78-175">yes</span></span> |

<span data-ttu-id="b4a78-176">Microsoft는 파트너와 협력하여 파트너가 Azure에 제공하는 이미지에 cloud-init를 포함하고 이러한 이미지에서 cloud-init가 작동하도록 설정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="b4a78-177">Azure CLI를 사용하여 VM 생성에 cloud-init 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="b4a78-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="b4a78-178">Azure에서 VM을 만들 때 cloud-init 스크립트를 시작하려면 Azure CLI `--custom-data` 스위치를 사용하여 cloud-init 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="b4a78-179">VM을 시작할 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b4a78-180">cloud-init을 사용해 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="b4a78-181">cloud-init 스크립트를 만들어 Linux VM의 호스트 이름 설정</span><span class="sxs-lookup"><span data-stu-id="b4a78-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="b4a78-182">Linux VM의 가장 간단하고 중요한 설정 중 하나는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="b4a78-183">이 스크립트와 함께 cloud-init을 사용하여 손쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="b4a78-184">예제 cloud-init 스크립트 `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="b4a78-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="b4a78-185">VM을 처음 시작하는 동안 이 cloud-init 스크립트는 호스트 이름을 `myservername`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="b4a78-186">로그인한 다음 새 VM의 호스트 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="b4a78-187">Linux를 업데이트하기 위한 cloud-init 만들기</span><span class="sxs-lookup"><span data-stu-id="b4a78-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="b4a78-188">보안상의 이유로 최초 부팅 시 Ubuntu VM을 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="b4a78-189">사용 중인 Linux 배포에 따라 다음 스크립트와 cloud-init을 사용하여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="b4a78-190">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_apt_upgrade.txt`</span><span class="sxs-lookup"><span data-stu-id="b4a78-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="b4a78-191">Linux가 부팅되고 나면 설치된 모든 패키지가 `apt-get`을 통해 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="b4a78-192">로그인한 다음 모든 패키지가 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="b4a78-193">Linux에 사용자를 추가하기 위한 cloud-init 만들기</span><span class="sxs-lookup"><span data-stu-id="b4a78-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="b4a78-194">새 Linux VM에서 가장 먼저 해야 할 작업 중 하나는 사용자 자신을 추가하는 것이며, 그렇지 않을 경우 `root`를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="b4a78-195">보안 및 유용성 측면의 모범 사례인 SSH 키를 사용하는 것이 좋습니다. SSH 키는 이 cloud-init 스크립트와 함께 `~/.ssh/authorized_keys` 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="b4a78-196">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="b4a78-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="b4a78-197">Linux가 부팅되고 나면 나열된 모든 사용자가 작성되어 sudo 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="b4a78-198">로그인한 다음 새로 생성된 사용자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="b4a78-199">출력</span><span class="sxs-lookup"><span data-stu-id="b4a78-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="b4a78-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4a78-200">Next Steps</span></span>
<span data-ttu-id="b4a78-201">cloud-init은 부팅 시 Linux VM을 수정하는 표준 방식의 하나로 자리잡고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="b4a78-202">Azure에는 부팅 시에 또는 실행 중에 Linux VM을 수정할 수 있는 VM 확장도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="b4a78-203">예를 들어 VM을 실행하는 동안 Azure VMAccessExtension을 사용하여 SSH 또는 사용자 정보를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="b4a78-204">cloud-init을 사용하는 경우 암호를 다시 설정하려면 VM을 다시 부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a78-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="b4a78-205">가상 컴퓨터 확장 및 기능 정보</span><span class="sxs-lookup"><span data-stu-id="b4a78-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b4a78-206">VMAccess 확장을 사용하여 사용자, SSH 관리 및 Azure Linux VM의 디스크 검사 또는 복구</span><span class="sxs-lookup"><span data-stu-id="b4a78-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

