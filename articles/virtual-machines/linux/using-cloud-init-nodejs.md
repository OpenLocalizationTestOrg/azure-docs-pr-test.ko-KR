---
title: "Azure에서 만드는 동안 Linux VM aaaUsing 클라우드 init toocustomize | Microsoft Docs"
description: "가 Linux VM a toouse 클라우드 init toocustomize Azure CLI 1.0 hello 하는 방법"
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
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="0cec7-103">클라우드 init toocustomize Linux VM을 사용 하 여 Azure CLI 1.0 hello로 만드는 동안</span><span class="sxs-lookup"><span data-stu-id="0cec7-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="0cec7-104">이 문서에서는 toomake 클라우드 초기화 스크립트 tooset hello 호스트 이름, 설치 된 패키지를 업데이트 및 사용자 계정 관리 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="0cec7-105">hello 클라우드 init 스크립트 hello Azure CLI에서 VM 만들 하는 동안 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="0cec7-106">hello 문서에는 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-106">hello article requires:</span></span>

* <span data-ttu-id="0cec7-107">Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="0cec7-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="0cec7-108">hello [Azure CLI](../../cli-install-nodejs.md) 로그인 한 `azure login`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="0cec7-109">hello Azure CLI *에 있어야* Azure Resource Manager 모드 `azure config mode arm`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0cec7-110">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="0cec7-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="0cec7-111">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="0cec7-112">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="0cec7-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0cec7-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="0cec7-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0cec7-114">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="0cec7-114">Quick Commands</span></span>
<span data-ttu-id="0cec7-115">Hello 호스트 이름을 설정 하는 모든 패키지를 업데이트 하 고 sudo 사용자 tooLinux를 추가 하는 클라우드 init.txt 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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
<span data-ttu-id="0cec7-116">리소스 그룹 toolaunch에 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="0cec7-117">클라우드 init tooconfigure를 사용 하 여 Linux VM 만들기 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="0cec7-118">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="0cec7-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="0cec7-119">소개</span><span class="sxs-lookup"><span data-stu-id="0cec7-119">Introduction</span></span>
<span data-ttu-id="0cec7-120">새 Linux VM을 시작하면 사용자 지정된 사항이나 사용자의 요구에 맞게 준비된 기능이 없는 표준 Linux VM이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="0cec7-121">[클라우드 init](https://cloudinit.readthedocs.org) 는 표준 방법 tooinject는 스크립트 또는 구성 설정을 해당 Linux VM에 처음으로 hello에 대해 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="0cec7-122">Azure에서 세 가지 방법으로 toomake 변경 사항이 Linux VM에 중인 배포 되거나 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="0cec7-123">cloud-init을 사용하여 스크립트를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="0cec7-124">Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="0cec7-125">Azure 템플릿을 사용합니다(cloud-init 사용).</span><span class="sxs-lookup"><span data-stu-id="0cec7-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="0cec7-126">Azure 템플릿을 사용합니다( [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)사용).</span><span class="sxs-lookup"><span data-stu-id="0cec7-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0cec7-127">부팅 후 언제 든 지 tooinject 스크립트:</span><span class="sxs-lookup"><span data-stu-id="0cec7-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="0cec7-128">SSH toorun 명령을 직접</span><span class="sxs-lookup"><span data-stu-id="0cec7-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="0cec7-129">Azure hello를 사용 하 여 스크립트 삽입 [VMAccess 확장](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), 명령적으로 또는 Azure 서식 파일</span><span class="sxs-lookup"><span data-stu-id="0cec7-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="0cec7-130">Ansible, Salt, Chef, Puppet 등의 구성 관리 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="0cec7-131">: VMAccess 확장 hello 동일한 루트 대로 스크립트를 실행 합니다. SSH를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="0cec7-132">그러나 hello VM 확장을 사용 하 여 사용 하면 몇 가지 기능 시나리오에 따라 유용할 수 있는 Azure 제공 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="0cec7-133">Azure VM 빨리 만들기 이미지 별칭에 대한 cloud-init 사용 가능 여부</span><span class="sxs-lookup"><span data-stu-id="0cec7-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="0cec7-134">Alias</span><span class="sxs-lookup"><span data-stu-id="0cec7-134">Alias</span></span> | <span data-ttu-id="0cec7-135">게시자</span><span class="sxs-lookup"><span data-stu-id="0cec7-135">Publisher</span></span> | <span data-ttu-id="0cec7-136">제안</span><span class="sxs-lookup"><span data-stu-id="0cec7-136">Offer</span></span> | <span data-ttu-id="0cec7-137">SKU</span><span class="sxs-lookup"><span data-stu-id="0cec7-137">SKU</span></span> | <span data-ttu-id="0cec7-138">버전</span><span class="sxs-lookup"><span data-stu-id="0cec7-138">Version</span></span> | <span data-ttu-id="0cec7-139">cloud-init</span><span class="sxs-lookup"><span data-stu-id="0cec7-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0cec7-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="0cec7-140">CentOS</span></span> |<span data-ttu-id="0cec7-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0cec7-141">OpenLogic</span></span> |<span data-ttu-id="0cec7-142">Centos</span><span class="sxs-lookup"><span data-stu-id="0cec7-142">Centos</span></span> |<span data-ttu-id="0cec7-143">7.2</span><span class="sxs-lookup"><span data-stu-id="0cec7-143">7.2</span></span> |<span data-ttu-id="0cec7-144">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-144">latest</span></span> |<span data-ttu-id="0cec7-145">no</span><span class="sxs-lookup"><span data-stu-id="0cec7-145">no</span></span> |
| <span data-ttu-id="0cec7-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0cec7-146">CoreOS</span></span> |<span data-ttu-id="0cec7-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0cec7-147">CoreOS</span></span> |<span data-ttu-id="0cec7-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0cec7-148">CoreOS</span></span> |<span data-ttu-id="0cec7-149">Stable</span><span class="sxs-lookup"><span data-stu-id="0cec7-149">Stable</span></span> |<span data-ttu-id="0cec7-150">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-150">latest</span></span> |<span data-ttu-id="0cec7-151">yes</span><span class="sxs-lookup"><span data-stu-id="0cec7-151">yes</span></span> |
| <span data-ttu-id="0cec7-152">Debian</span><span class="sxs-lookup"><span data-stu-id="0cec7-152">Debian</span></span> |<span data-ttu-id="0cec7-153">credativ</span><span class="sxs-lookup"><span data-stu-id="0cec7-153">credativ</span></span> |<span data-ttu-id="0cec7-154">Debian</span><span class="sxs-lookup"><span data-stu-id="0cec7-154">Debian</span></span> |<span data-ttu-id="0cec7-155">8</span><span class="sxs-lookup"><span data-stu-id="0cec7-155">8</span></span> |<span data-ttu-id="0cec7-156">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-156">latest</span></span> |<span data-ttu-id="0cec7-157">no</span><span class="sxs-lookup"><span data-stu-id="0cec7-157">no</span></span> |
| <span data-ttu-id="0cec7-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0cec7-158">openSUSE</span></span> |<span data-ttu-id="0cec7-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="0cec7-159">SUSE</span></span> |<span data-ttu-id="0cec7-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0cec7-160">openSUSE</span></span> |<span data-ttu-id="0cec7-161">13.2</span><span class="sxs-lookup"><span data-stu-id="0cec7-161">13.2</span></span> |<span data-ttu-id="0cec7-162">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-162">latest</span></span> |<span data-ttu-id="0cec7-163">no</span><span class="sxs-lookup"><span data-stu-id="0cec7-163">no</span></span> |
| <span data-ttu-id="0cec7-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="0cec7-164">RHEL</span></span> |<span data-ttu-id="0cec7-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="0cec7-165">Redhat</span></span> |<span data-ttu-id="0cec7-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="0cec7-166">RHEL</span></span> |<span data-ttu-id="0cec7-167">7.2</span><span class="sxs-lookup"><span data-stu-id="0cec7-167">7.2</span></span> |<span data-ttu-id="0cec7-168">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-168">latest</span></span> |<span data-ttu-id="0cec7-169">no</span><span class="sxs-lookup"><span data-stu-id="0cec7-169">no</span></span> |
| <span data-ttu-id="0cec7-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0cec7-170">UbuntuLTS</span></span> |<span data-ttu-id="0cec7-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="0cec7-171">Canonical</span></span> |<span data-ttu-id="0cec7-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="0cec7-172">UbuntuServer</span></span> |<span data-ttu-id="0cec7-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="0cec7-173">14.04.4-LTS</span></span> |<span data-ttu-id="0cec7-174">최신</span><span class="sxs-lookup"><span data-stu-id="0cec7-174">latest</span></span> |<span data-ttu-id="0cec7-175">yes</span><span class="sxs-lookup"><span data-stu-id="0cec7-175">yes</span></span> |

<span data-ttu-id="0cec7-176">Microsoft 작업에이 파트너 tooget 클라우드 초기화 포함 되어 tooAzure를 제공 하는 hello 이미지에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="0cec7-177">추가 Azure CLI hello에 대 한 클라우드 초기화 스크립트 toohello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0cec7-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="0cec7-178">hello Azure CLI를 사용 하 여 hello 클라우드 초기화 파일을 지정 하는 azure에서 VM을 만들 때 클라우드 초기화 스크립트 toolaunch `--custom-data` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="0cec7-179">리소스 그룹 toolaunch에 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="0cec7-180">클라우드 init tooconfigure를 사용 하 여 Linux VM 만들기 부팅 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="0cec7-181">Linux VM의 클라우드 초기화 스크립트 tooset hello 호스트 만들기</span><span class="sxs-lookup"><span data-stu-id="0cec7-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="0cec7-182">가장 간단한 hello 및 모든 Linux VM에 대 한 가장 중요 한 설정 중 하나를 hello hostname 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="0cec7-183">이 스크립트와 함께 cloud-init을 사용하여 손쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="0cec7-184">예제 cloud-init 스크립트 `cloud_config_hostname.txt`</span><span class="sxs-lookup"><span data-stu-id="0cec7-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="0cec7-185">이 클라우드 초기화 스크립트의 hello VM hello 초기 시작 하는 동안 hello hostname 너무 설정`myservername`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

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

<span data-ttu-id="0cec7-186">로그인의 hello hello 호스트 이름 확인 및 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="0cec7-187">클라우드 초기화 스크립트 tooupdate Linux 만들기</span><span class="sxs-lookup"><span data-stu-id="0cec7-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="0cec7-188">보안을 위해 hello 처음 부팅할 때 Ubuntu VM tooupdate 프로그램 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="0cec7-189">클라우드 초기화를 사용 하 여 hello로 따르는지 스크립트를 사용 하는 hello Linux 배포에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="0cec7-190">다음 스크립트 예에서는 클라우드 init `cloud_config_apt_upgrade.txt` hello Debian 제품군에 대 한</span><span class="sxs-lookup"><span data-stu-id="0cec7-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="0cec7-191">통해 모든 hello 설치 패키지는 업데이트 Linux 부팅 된 후 `apt-get`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="0cec7-192">로그인한 다음 모든 패키지가 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="0cec7-193">클라우드 초기화 스크립트 tooadd 사용자 tooLinux 만들기</span><span class="sxs-lookup"><span data-stu-id="0cec7-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="0cec7-194">모든 새로운 Linux VM에 있는 hello 첫 번째 작업 중 하나는 tooadd 자신이 나 tooavoid 사용에 대 한 사용자 `root`합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="0cec7-195">SSH 키가 유용성 및 보안에 대 한 모범 사례 및 toohello 추가 될 `~/.ssh/authorized_keys` 이 클라우드 초기화 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="0cec7-196">Debian 제품군용 예제 cloud-init 스크립트 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="0cec7-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="0cec7-197">Linux 부팅 된 후에 모든 나열 된 hello 사용자는 생성 되 고 추가 된 toohello sudo 그룹.</span><span class="sxs-lookup"><span data-stu-id="0cec7-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

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

<span data-ttu-id="0cec7-198">로그인 하 고 hello 새로 만든 사용자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="0cec7-199">출력</span><span class="sxs-lookup"><span data-stu-id="0cec7-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="0cec7-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cec7-200">Next Steps</span></span>
<span data-ttu-id="0cec7-201">클라우드 init은 되 고 하나의 표준 방식으로 toomodify Linux VM에서 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="0cec7-202">Azure에 toomodify 수 있게 해 주는 VM 확장 프로그램 LinuxVM 부팅 또는 실행 되는 동안 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="0cec7-203">예를 들어 hello VM에서 실행 되는 동안 hello Azure VMAccessExtension tooreset SSH 또는 사용자 정보 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="0cec7-204">클라우드-init로 tooreset hello 암호를 다시 부팅 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cec7-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="0cec7-205">가상 컴퓨터 확장 및 기능 정보</span><span class="sxs-lookup"><span data-stu-id="0cec7-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="0cec7-206">사용자, SSH, 및 확인 또는 복구 디스크를 사용 하 여 Azure Linux Vm에서 VMAccess 확장을 환영</span><span class="sxs-lookup"><span data-stu-id="0cec7-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

