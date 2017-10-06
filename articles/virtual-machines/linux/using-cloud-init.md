---
title: "Linux VM aaaUse 클라우드 init toocustomize | Microsoft Docs"
description: "가 Linux VM a toouse 클라우드 init toocustomize Azure CLI 2.0 hello 하는 방법"
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
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="519ee-103">클라우드 init toocustomize Linux VM을 만드는 동안 사용</span><span class="sxs-lookup"><span data-stu-id="519ee-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="519ee-104">이 문서에서는 방법 toomake 클라우드 초기화 스크립트 tooset hello 호스트 이름, 설치 된 패키지를 업데이트 및 Azure CLI 2.0 hello로 사용자 계정을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="519ee-105">hello 클라우드 초기화 스크립트는 Azure CLI에서 가상 컴퓨터 (VM)를 만들 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="519ee-106">응용 프로그램 설치, 구성 파일 작성 및 Key Vault의 키 삽입에 대한 보다 깊이 있는 개요를 보려면 [이 자습서](tutorial-automate-vm-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="519ee-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="519ee-107">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](using-cloud-init-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="519ee-108">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="519ee-108">Quick commands</span></span>
<span data-ttu-id="519ee-109">Hello 호스트 이름을 설정 하는 모든 패키지를 업데이트 하 고 sudo 사용자 tooLinux를 추가 하는 클라우드 init.txt 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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

<span data-ttu-id="519ee-110">리소스 그룹 toolaunch에 Vm을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="519ee-111">hello 다음 예제에서는 명명 된 hello 리소스 그룹 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="519ee-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="519ee-112">사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 hello로 부팅 하는 동안 그 `--custom-data` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="519ee-113">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="519ee-113">Detailed walkthrough</span></span>
<span data-ttu-id="519ee-114">새 Linux VM을 시작하면 사용자 지정된 사항이나 사용자의 요구에 맞게 준비된 기능이 없는 표준 Linux VM이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="519ee-115">[클라우드 init](https://cloudinit.readthedocs.org) 는 표준 방법 tooinject는 스크립트 또는 구성 설정을 해당 Linux VM에 처음으로 hello에 대해 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="519ee-116">Azure에서 몇 가지 여러 가지 Linux VM에 toomake 변경 중인 배포 되거나 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="519ee-117">cloud-init을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="519ee-118">Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="519ee-119">Azure 템플릿을 사용합니다(cloud-init 사용).</span><span class="sxs-lookup"><span data-stu-id="519ee-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="519ee-120">Azure 템플릿을 사용합니다( [CustomScriptExtention](extensions-customscript.md)사용).</span><span class="sxs-lookup"><span data-stu-id="519ee-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="519ee-121">부팅 후 언제 든 지 tooinject 스크립트:</span><span class="sxs-lookup"><span data-stu-id="519ee-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="519ee-122">SSH toorun 명령을 직접</span><span class="sxs-lookup"><span data-stu-id="519ee-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="519ee-123">Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md), 명령적으로 또는 Azure 서식 파일</span><span class="sxs-lookup"><span data-stu-id="519ee-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="519ee-124">Ansible, Salt, Chef, Puppet 등의 구성 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="519ee-125">VMAccess 확장 hello 동일한 루트 대로 스크립트를 실행 합니다. SSH를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="519ee-126">그러나 hello VM 확장을 사용 하 여 사용 하면 몇 가지 기능 시나리오에 따라 유용할 수 있는 Azure 제공 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="519ee-127">Azure VM 빨리 만들기 이미지 별칭에 대한 cloud-init 사용 가능 여부</span><span class="sxs-lookup"><span data-stu-id="519ee-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="519ee-128">Alias</span><span class="sxs-lookup"><span data-stu-id="519ee-128">Alias</span></span> | <span data-ttu-id="519ee-129">게시자</span><span class="sxs-lookup"><span data-stu-id="519ee-129">Publisher</span></span> | <span data-ttu-id="519ee-130">제안</span><span class="sxs-lookup"><span data-stu-id="519ee-130">Offer</span></span> | <span data-ttu-id="519ee-131">SKU</span><span class="sxs-lookup"><span data-stu-id="519ee-131">SKU</span></span> | <span data-ttu-id="519ee-132">버전</span><span class="sxs-lookup"><span data-stu-id="519ee-132">Version</span></span> | <span data-ttu-id="519ee-133">cloud-init</span><span class="sxs-lookup"><span data-stu-id="519ee-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="519ee-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="519ee-134">CentOS</span></span> |<span data-ttu-id="519ee-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="519ee-135">OpenLogic</span></span> |<span data-ttu-id="519ee-136">Centos</span><span class="sxs-lookup"><span data-stu-id="519ee-136">Centos</span></span> |<span data-ttu-id="519ee-137">7.2</span><span class="sxs-lookup"><span data-stu-id="519ee-137">7.2</span></span> |<span data-ttu-id="519ee-138">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-138">latest</span></span> |<span data-ttu-id="519ee-139">no</span><span class="sxs-lookup"><span data-stu-id="519ee-139">no</span></span> |
| <span data-ttu-id="519ee-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="519ee-140">CoreOS</span></span> |<span data-ttu-id="519ee-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="519ee-141">CoreOS</span></span> |<span data-ttu-id="519ee-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="519ee-142">CoreOS</span></span> |<span data-ttu-id="519ee-143">Stable</span><span class="sxs-lookup"><span data-stu-id="519ee-143">Stable</span></span> |<span data-ttu-id="519ee-144">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-144">latest</span></span> |<span data-ttu-id="519ee-145">yes</span><span class="sxs-lookup"><span data-stu-id="519ee-145">yes</span></span> |
| <span data-ttu-id="519ee-146">Debian</span><span class="sxs-lookup"><span data-stu-id="519ee-146">Debian</span></span> |<span data-ttu-id="519ee-147">credativ</span><span class="sxs-lookup"><span data-stu-id="519ee-147">credativ</span></span> |<span data-ttu-id="519ee-148">Debian</span><span class="sxs-lookup"><span data-stu-id="519ee-148">Debian</span></span> |<span data-ttu-id="519ee-149">8</span><span class="sxs-lookup"><span data-stu-id="519ee-149">8</span></span> |<span data-ttu-id="519ee-150">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-150">latest</span></span> |<span data-ttu-id="519ee-151">no</span><span class="sxs-lookup"><span data-stu-id="519ee-151">no</span></span> |
| <span data-ttu-id="519ee-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="519ee-152">openSUSE</span></span> |<span data-ttu-id="519ee-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="519ee-153">SUSE</span></span> |<span data-ttu-id="519ee-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="519ee-154">openSUSE</span></span> |<span data-ttu-id="519ee-155">13.2</span><span class="sxs-lookup"><span data-stu-id="519ee-155">13.2</span></span> |<span data-ttu-id="519ee-156">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-156">latest</span></span> |<span data-ttu-id="519ee-157">no</span><span class="sxs-lookup"><span data-stu-id="519ee-157">no</span></span> |
| <span data-ttu-id="519ee-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="519ee-158">RHEL</span></span> |<span data-ttu-id="519ee-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="519ee-159">Redhat</span></span> |<span data-ttu-id="519ee-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="519ee-160">RHEL</span></span> |<span data-ttu-id="519ee-161">7.2</span><span class="sxs-lookup"><span data-stu-id="519ee-161">7.2</span></span> |<span data-ttu-id="519ee-162">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-162">latest</span></span> |<span data-ttu-id="519ee-163">no</span><span class="sxs-lookup"><span data-stu-id="519ee-163">no</span></span> |
| <span data-ttu-id="519ee-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="519ee-164">UbuntuLTS</span></span> |<span data-ttu-id="519ee-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="519ee-165">Canonical</span></span> |<span data-ttu-id="519ee-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="519ee-166">UbuntuServer</span></span> |<span data-ttu-id="519ee-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="519ee-167">14.04.4-LTS</span></span> |<span data-ttu-id="519ee-168">최신</span><span class="sxs-lookup"><span data-stu-id="519ee-168">latest</span></span> |<span data-ttu-id="519ee-169">yes</span><span class="sxs-lookup"><span data-stu-id="519ee-169">yes</span></span> |

<span data-ttu-id="519ee-170">TooAzure를 제공 하는 hello 이미지에서 작업 및 우리의 파트너 tooget 클라우드 초기화 포함을 사용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="519ee-171">추가 Azure CLI hello에 대 한 클라우드 초기화 스크립트 toohello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="519ee-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="519ee-172">hello Azure CLI를 사용 하 여 hello 클라우드 초기화 파일을 지정 하는 azure에서 VM을 만들 때 클라우드 초기화 스크립트 toolaunch `--custom-data` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="519ee-173">리소스 그룹 toolaunch에 Vm을 만들 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="519ee-174">hello 다음 예제에서는 명명 된 hello 리소스 그룹 *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="519ee-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="519ee-175">사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="519ee-176">Linux VM의 클라우드 초기화 스크립트 tooset hello 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="519ee-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="519ee-177">가장 간단한 hello 및 모든 Linux VM에 대 한 가장 중요 한 설정 중 하나를 hello hostname 것입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="519ee-178">이 스크립트와 함께 cloud-init을 사용하여 손쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="519ee-179">예제 cloud-init 스크립트 `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="519ee-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="519ee-180">이 클라우드 초기화 스크립트의 hello VM hello 초기 시작 하는 동안 hello hostname 너무 설정*myservername*합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="519ee-181">사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="519ee-182">로그인의 hello hello 호스트 이름 확인 및 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="519ee-183">cloud-init 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="519ee-183">Create a cloud-init script</span></span>
<span data-ttu-id="519ee-184">보안을 위해 hello 처음 부팅할 때 Ubuntu VM tooupdate 프로그램 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="519ee-185">클라우드 초기화를 사용 하 여 hello로 따르는지 스크립트를 사용 하는 hello Linux 배포에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="519ee-186">다음 스크립트 예에서는 클라우드 init `cloud_config_apt_upgrade.txt` hello Debian 제품군에 대 한</span><span class="sxs-lookup"><span data-stu-id="519ee-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="519ee-187">통해 모든 hello 설치 패키지는 업데이트 Linux 부팅 된 후 **apt get**합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="519ee-188">사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="519ee-189">로그인한 다음 모든 패키지가 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="519ee-190">클라우드 초기화 스크립트 tooadd 사용자 tooLinux 만들기</span><span class="sxs-lookup"><span data-stu-id="519ee-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="519ee-191">모든 새로운 Linux VM에 있는 hello 첫 번째 작업 중 하나는 tooadd 자신이 나 tooavoid 사용에 대 한 사용자 *루트*합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="519ee-192">SSH 키가 유용성 및 보안에 대 한 모범 사례 및 toohello 추가 될 *~/.ssh/authorized_keys* 이 클라우드 초기화 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="519ee-193">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="519ee-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="519ee-194">Linux 부팅 된 후에 모든 나열 된 hello 사용자는 생성 되 고 추가 된 toohello sudo 그룹.</span><span class="sxs-lookup"><span data-stu-id="519ee-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="519ee-195">사용 하 여 Linux VM을 만들 [az vm 만들기](/cli/azure/vm#create) 클라우드 init tooconfigure를 사용 하 여 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="519ee-196">로그인 하 고 hello 새로 만든 사용자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="519ee-197">출력</span><span class="sxs-lookup"><span data-stu-id="519ee-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="519ee-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="519ee-198">Next steps</span></span>
<span data-ttu-id="519ee-199">클라우드 init은 되 고 하나의 표준 방식으로 toomodify Linux VM에서 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="519ee-200">Azure에 toomodify 수 있게 해 주는 VM 확장 프로그램 LinuxVM 부팅 또는 실행 되는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="519ee-201">예를 들어 hello VM에서 실행 되는 동안 hello Azure VMAccessExtension tooreset SSH 또는 사용자 정보 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="519ee-202">클라우드-init로 tooreset hello 암호를 다시 부팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="519ee-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="519ee-203">가상 컴퓨터 확장 및 기능 정보</span><span class="sxs-lookup"><span data-stu-id="519ee-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="519ee-204">사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영</span><span class="sxs-lookup"><span data-stu-id="519ee-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
