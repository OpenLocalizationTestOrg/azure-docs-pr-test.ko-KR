---
title: "cloud-init를 사용하여 Linux VM 사용자 지정 | Microsoft Docs"
description: "Azure CLI 2.0에서 cloud-init를 사용하여 생성 중인 Linux VM을 사용자 지정하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="75c9f-103">cloud-init를 사용하여 생성 중인 Linux VM 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="75c9f-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="75c9f-104">이 문서에서는 cloud-init 스크립트를 사용하여 Azure CLI 2.0에서 호스트 이름 설정, 설치된 패키지 업데이트, 사용자 계정 관리를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="75c9f-105">Azure CLI에서 VM(가상 컴퓨터)을 만드는 중에 cloud-init 스크립트가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="75c9f-106">응용 프로그램 설치, 구성 파일 작성 및 Key Vault의 키 삽입에 대한 보다 깊이 있는 개요를 보려면 [이 자습서](tutorial-automate-vm-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75c9f-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="75c9f-107">[Azure CLI 1.0](using-cloud-init-nodejs.md)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="75c9f-108">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="75c9f-108">Quick commands</span></span>
<span data-ttu-id="75c9f-109">호스트 이름을 설정하고, 모든 패키지를 업데이트하고, Linux에 sudo 사용자를 추가하는 cloud-init.txt 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```yaml
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

<span data-ttu-id="75c9f-110">[az group create](/cli/azure/group#create)를 사용하여 VM을 시작하려면 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="75c9f-111">다음 예제에서는 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="75c9f-112">cloud-init을 사용하여 [az vm create](/cli/azure/vm#create)로 Linux VM을 만든 후 `--custom-data` 매개 변수를 사용하여 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="75c9f-113">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="75c9f-113">Detailed walkthrough</span></span>
<span data-ttu-id="75c9f-114">새 Linux VM을 시작하면 사용자 지정된 사항이나 사용자의 요구에 맞게 준비된 기능이 없는 표준 Linux VM이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="75c9f-115">[cloud-init](https://cloudinit.readthedocs.org) 은 Linux VM을 처음으로 부팅할 때 해당 VM에 스크립트 또는 구성 설정을 삽입하는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="75c9f-116">Azure에서는 다음의 몇 가지 방법으로 배포 또는 부팅 중인 Linux VM을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="75c9f-117">cloud-init을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="75c9f-118">Azure [VMAccess 확장](using-vmaccess-extension.md)을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="75c9f-119">Azure 템플릿을 사용합니다(cloud-init 사용).</span><span class="sxs-lookup"><span data-stu-id="75c9f-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="75c9f-120">Azure 템플릿을 사용합니다( [CustomScriptExtention](extensions-customscript.md)사용).</span><span class="sxs-lookup"><span data-stu-id="75c9f-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="75c9f-121">부팅 후에 언제든지 스크립트를 삽입하려면 다음 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="75c9f-122">SSH를 통해 명령을 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-122">SSH to run commands directly</span></span>
* <span data-ttu-id="75c9f-123">Azure [VMAccess 확장](using-vmaccess-extension.md)을 사용하여 명령적으로 또는 Azure 템플릿에서 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="75c9f-124">Ansible, Salt, Chef, Puppet 등의 구성 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="75c9f-125">VMAccess 확장은 SSH를 사용할 때와 같은 방식으로 스크립트를 루트로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="75c9f-126">그러나 VM 확장 사용 시에는 시나리오에 따라 유용할 수 있는 다양한 Azure 제공 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="75c9f-127">Azure VM 빨리 만들기 이미지 별칭에 대한 cloud-init 사용 가능 여부</span><span class="sxs-lookup"><span data-stu-id="75c9f-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="75c9f-128">Alias</span><span class="sxs-lookup"><span data-stu-id="75c9f-128">Alias</span></span> | <span data-ttu-id="75c9f-129">게시자</span><span class="sxs-lookup"><span data-stu-id="75c9f-129">Publisher</span></span> | <span data-ttu-id="75c9f-130">제안</span><span class="sxs-lookup"><span data-stu-id="75c9f-130">Offer</span></span> | <span data-ttu-id="75c9f-131">SKU</span><span class="sxs-lookup"><span data-stu-id="75c9f-131">SKU</span></span> | <span data-ttu-id="75c9f-132">버전</span><span class="sxs-lookup"><span data-stu-id="75c9f-132">Version</span></span> | <span data-ttu-id="75c9f-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="75c9f-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="75c9f-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="75c9f-134">CentOS</span></span> |<span data-ttu-id="75c9f-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="75c9f-135">OpenLogic</span></span> |<span data-ttu-id="75c9f-136">Centos</span><span class="sxs-lookup"><span data-stu-id="75c9f-136">Centos</span></span> |<span data-ttu-id="75c9f-137">7.2</span><span class="sxs-lookup"><span data-stu-id="75c9f-137">7.2</span></span> |<span data-ttu-id="75c9f-138">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-138">latest</span></span> |<span data-ttu-id="75c9f-139">no</span><span class="sxs-lookup"><span data-stu-id="75c9f-139">no</span></span> |
| <span data-ttu-id="75c9f-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="75c9f-140">CoreOS</span></span> |<span data-ttu-id="75c9f-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="75c9f-141">CoreOS</span></span> |<span data-ttu-id="75c9f-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="75c9f-142">CoreOS</span></span> |<span data-ttu-id="75c9f-143">Stable</span><span class="sxs-lookup"><span data-stu-id="75c9f-143">Stable</span></span> |<span data-ttu-id="75c9f-144">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-144">latest</span></span> |<span data-ttu-id="75c9f-145">yes</span><span class="sxs-lookup"><span data-stu-id="75c9f-145">yes</span></span> |
| <span data-ttu-id="75c9f-146">Debian</span><span class="sxs-lookup"><span data-stu-id="75c9f-146">Debian</span></span> |<span data-ttu-id="75c9f-147">credativ</span><span class="sxs-lookup"><span data-stu-id="75c9f-147">credativ</span></span> |<span data-ttu-id="75c9f-148">Debian</span><span class="sxs-lookup"><span data-stu-id="75c9f-148">Debian</span></span> |<span data-ttu-id="75c9f-149">8</span><span class="sxs-lookup"><span data-stu-id="75c9f-149">8</span></span> |<span data-ttu-id="75c9f-150">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-150">latest</span></span> |<span data-ttu-id="75c9f-151">no</span><span class="sxs-lookup"><span data-stu-id="75c9f-151">no</span></span> |
| <span data-ttu-id="75c9f-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="75c9f-152">openSUSE</span></span> |<span data-ttu-id="75c9f-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="75c9f-153">SUSE</span></span> |<span data-ttu-id="75c9f-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="75c9f-154">openSUSE</span></span> |<span data-ttu-id="75c9f-155">13.2</span><span class="sxs-lookup"><span data-stu-id="75c9f-155">13.2</span></span> |<span data-ttu-id="75c9f-156">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-156">latest</span></span> |<span data-ttu-id="75c9f-157">no</span><span class="sxs-lookup"><span data-stu-id="75c9f-157">no</span></span> |
| <span data-ttu-id="75c9f-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="75c9f-158">RHEL</span></span> |<span data-ttu-id="75c9f-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="75c9f-159">Redhat</span></span> |<span data-ttu-id="75c9f-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="75c9f-160">RHEL</span></span> |<span data-ttu-id="75c9f-161">7.2</span><span class="sxs-lookup"><span data-stu-id="75c9f-161">7.2</span></span> |<span data-ttu-id="75c9f-162">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-162">latest</span></span> |<span data-ttu-id="75c9f-163">no</span><span class="sxs-lookup"><span data-stu-id="75c9f-163">no</span></span> |
| <span data-ttu-id="75c9f-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="75c9f-164">UbuntuLTS</span></span> |<span data-ttu-id="75c9f-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="75c9f-165">Canonical</span></span> |<span data-ttu-id="75c9f-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="75c9f-166">UbuntuServer</span></span> |<span data-ttu-id="75c9f-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="75c9f-167">14.04.4-LTS</span></span> |<span data-ttu-id="75c9f-168">최신</span><span class="sxs-lookup"><span data-stu-id="75c9f-168">latest</span></span> |<span data-ttu-id="75c9f-169">yes</span><span class="sxs-lookup"><span data-stu-id="75c9f-169">yes</span></span> |

<span data-ttu-id="75c9f-170">당사는 파트너와 협력하여 파트너가 Azure에 제공하는 이미지에 cloud-init를 포함하고 이러한 이미지에서 cloud-init가 작동하도록 설정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="75c9f-171">Azure CLI를 사용하여 VM 생성에 cloud-init 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="75c9f-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="75c9f-172">Azure에서 VM을 만들 때 cloud-init 스크립트를 시작하려면 Azure CLI `--custom-data` 스위치를 사용하여 cloud-init 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="75c9f-173">[az group create](/cli/azure/group#create)를 사용하여 VM을 시작하려면 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="75c9f-174">다음 예제에서는 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="75c9f-175">cloud-init을 사용하여 [az vm create](/cli/azure/vm#create)로 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="75c9f-176">cloud-init 스크립트를 만들어 Linux VM의 호스트 이름 설정</span><span class="sxs-lookup"><span data-stu-id="75c9f-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="75c9f-177">Linux VM의 가장 간단하고 중요한 설정 중 하나는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="75c9f-178">이 스크립트와 함께 cloud-init을 사용하여 손쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="75c9f-179">예제 cloud-init 스크립트 `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="75c9f-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="75c9f-180">VM을 처음 시작하는 동안 이 cloud-init 스크립트는 호스트 이름을 *myservername*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="75c9f-181">cloud-init을 사용하여 [az vm create](/cli/azure/vm#create)로 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="75c9f-182">로그인한 다음 새 VM의 호스트 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="75c9f-183">cloud-init 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="75c9f-183">Create a cloud-init script</span></span>
<span data-ttu-id="75c9f-184">보안상의 이유로 최초 부팅 시 Ubuntu VM을 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="75c9f-185">사용 중인 Linux 배포에 따라 다음 스크립트와 cloud-init을 사용하여 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="75c9f-186">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_apt_upgrade.txt`</span><span class="sxs-lookup"><span data-stu-id="75c9f-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="75c9f-187">Linux가 부팅되고 나면 설치된 모든 패키지가 **apt-get**을 통해 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="75c9f-188">cloud-init을 사용하여 [az vm create](/cli/azure/vm#create)로 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="75c9f-189">로그인한 다음 모든 패키지가 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="75c9f-190">Linux에 사용자를 추가하기 위한 cloud-init 만들기</span><span class="sxs-lookup"><span data-stu-id="75c9f-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="75c9f-191">새 Linux VM에서 가장 먼저 해야 할 작업 중 하나는 사용자 자신을 추가하는 것이며, 그렇지 않을 경우 *root*를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="75c9f-192">보안 및 유용성 측면의 모범 사례인 SSH 키를 사용하는 것이 좋습니다. SSH 키는 이 cloud-init 스크립트와 함께 *~/.ssh/authorized_keys* 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="75c9f-193">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="75c9f-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="75c9f-194">Linux가 부팅되고 나면 나열된 모든 사용자가 작성되어 sudo 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="75c9f-195">cloud-init을 사용하여 [az vm create](/cli/azure/vm#create)로 Linux VM을 만들어서 부팅 중에 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="75c9f-196">로그인한 다음 새로 생성된 사용자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="75c9f-197">출력</span><span class="sxs-lookup"><span data-stu-id="75c9f-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="75c9f-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75c9f-198">Next steps</span></span>
<span data-ttu-id="75c9f-199">cloud-init은 부팅 시 Linux VM을 수정하는 표준 방식의 하나로 자리잡고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="75c9f-200">Azure에는 부팅 시에 또는 실행 중에 Linux VM을 수정할 수 있는 VM 확장도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="75c9f-201">예를 들어 VM을 실행하는 동안 Azure VMAccessExtension을 사용하여 SSH 또는 사용자 정보를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="75c9f-202">cloud-init을 사용하는 경우 암호를 다시 설정하려면 VM을 다시 부팅해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c9f-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="75c9f-203">가상 컴퓨터 확장 및 기능 정보</span><span class="sxs-lookup"><span data-stu-id="75c9f-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="75c9f-204">VMAccess 확장을 사용하여 사용자, SSH 관리 및 Azure Linux VM의 디스크 검사 또는 복구</span><span class="sxs-lookup"><span data-stu-id="75c9f-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)