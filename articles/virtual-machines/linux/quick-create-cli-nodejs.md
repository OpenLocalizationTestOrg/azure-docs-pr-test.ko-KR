---
title: "Azure CLI 1.0을 사용하여 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 Azure에서 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="0febc-103">Azure CLI 1.0을 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0febc-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="0febc-104">이 문서에서는 Azure 명령줄 인터페이스(CLI)의 `azure vm quick-create` 명령을 사용하여 Azure에서 Linux 가상 컴퓨터(VM)를 신속하게 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="0febc-105">`quick-create` 명령은 개념을 신속하게 프로토타입하거나 테스트하는 데 사용할 수 있는 기본 인프라 내에 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="0febc-106">Azure CLI 2.0을 사용하여 VM을 만들려면 [Azure CLI를 사용하여 VM 만들기](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0febc-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0febc-107">[Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 Linux VM을 신속히 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0febc-108">이 문서에는 [SSH 공용 및 개인 키 파일](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="0febc-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="0febc-109">Quick commands</span></span>

<span data-ttu-id="0febc-110">다음 예제에서는 CoreOS VM을 배포하고 SSH(Secure Shell)를 연결하는 방법을 보여줍니다(사용자의 인수는 다를 수 있음).</span><span class="sxs-lookup"><span data-stu-id="0febc-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0febc-111">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="0febc-111">Detailed walkthrough</span></span>

<span data-ttu-id="0febc-112">다음 연습에는 단계별로 각 단계에서 수행할 작업을 설명하면서 배포되는 UbuntuLTS VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="0febc-113">VM quick-create 별칭</span><span class="sxs-lookup"><span data-stu-id="0febc-113">VM quick-create aliases</span></span>

<span data-ttu-id="0febc-114">배포를 선택하는 빠른 방법은 가장 일반적인 OS 배포에 매핑된 Azure CLI 별칭을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="0febc-115">다음 테이블에 별칭이 나열되어 있습니다(Azure CLI 버전 0.10 현재).</span><span class="sxs-lookup"><span data-stu-id="0febc-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="0febc-116">`quick-create`을 사용하는 모든 배포는 기본적으로 더 빠른 프로비전 및 고성능 디스크 액세스를 제공하는 SSD(반도체 드라이브) 저장소에서 지원되는 VM에 대해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="0febc-117">(이러한 별칭은 Azure에 사용할 수 있는 배포의 작은 부분을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="0febc-118">[웹에서](https://azure.microsoft.com/marketplace/virtual-machines/) [PowerShell을 통해 이미지를 검색](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)하여 Azure Marketplace에 있는 이미지를 더 많이 찾거나 [고유의 사용자 지정 이미지를 업로드합니다](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="0febc-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="0febc-119">Alias</span><span class="sxs-lookup"><span data-stu-id="0febc-119">Alias</span></span> | <span data-ttu-id="0febc-120">게시자</span><span class="sxs-lookup"><span data-stu-id="0febc-120">Publisher</span></span> | <span data-ttu-id="0febc-121">제안</span><span class="sxs-lookup"><span data-stu-id="0febc-121">Offer</span></span> | <span data-ttu-id="0febc-122">SKU</span><span class="sxs-lookup"><span data-stu-id="0febc-122">SKU</span></span> | <span data-ttu-id="0febc-123">버전</span><span class="sxs-lookup"><span data-stu-id="0febc-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0febc-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="0febc-124">CentOS</span></span> |<span data-ttu-id="0febc-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0febc-125">OpenLogic</span></span> |<span data-ttu-id="0febc-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="0febc-126">CentOS</span></span> |<span data-ttu-id="0febc-127">7.2</span><span class="sxs-lookup"><span data-stu-id="0febc-127">7.2</span></span> |<span data-ttu-id="0febc-128">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-128">latest</span></span> |
| <span data-ttu-id="0febc-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0febc-129">CoreOS</span></span> |<span data-ttu-id="0febc-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0febc-130">CoreOS</span></span> |<span data-ttu-id="0febc-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0febc-131">CoreOS</span></span> |<span data-ttu-id="0febc-132">Stable</span><span class="sxs-lookup"><span data-stu-id="0febc-132">Stable</span></span> |<span data-ttu-id="0febc-133">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-133">latest</span></span> |
| <span data-ttu-id="0febc-134">Debian</span><span class="sxs-lookup"><span data-stu-id="0febc-134">Debian</span></span> |<span data-ttu-id="0febc-135">credativ</span><span class="sxs-lookup"><span data-stu-id="0febc-135">credativ</span></span> |<span data-ttu-id="0febc-136">Debian</span><span class="sxs-lookup"><span data-stu-id="0febc-136">Debian</span></span> |<span data-ttu-id="0febc-137">8</span><span class="sxs-lookup"><span data-stu-id="0febc-137">8</span></span> |<span data-ttu-id="0febc-138">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-138">latest</span></span> |
| <span data-ttu-id="0febc-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0febc-139">openSUSE</span></span> |<span data-ttu-id="0febc-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="0febc-140">SUSE</span></span> |<span data-ttu-id="0febc-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0febc-141">openSUSE</span></span> |<span data-ttu-id="0febc-142">13.2</span><span class="sxs-lookup"><span data-stu-id="0febc-142">13.2</span></span> |<span data-ttu-id="0febc-143">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-143">latest</span></span> |
| <span data-ttu-id="0febc-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="0febc-144">RHEL</span></span> |<span data-ttu-id="0febc-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="0febc-145">Red Hat</span></span> |<span data-ttu-id="0febc-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="0febc-146">RHEL</span></span> |<span data-ttu-id="0febc-147">7.2</span><span class="sxs-lookup"><span data-stu-id="0febc-147">7.2</span></span> |<span data-ttu-id="0febc-148">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-148">latest</span></span> |
| <span data-ttu-id="0febc-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0febc-149">UbuntuLTS</span></span> |<span data-ttu-id="0febc-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="0febc-150">Canonical</span></span> |<span data-ttu-id="0febc-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="0febc-151">Ubuntu Server</span></span> |<span data-ttu-id="0febc-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="0febc-152">14.04.4-LTS</span></span> |<span data-ttu-id="0febc-153">최신</span><span class="sxs-lookup"><span data-stu-id="0febc-153">latest</span></span> |

<span data-ttu-id="0febc-154">다음 섹션에서는 **ImageURN** 옵션(`-Q`)에 `UbuntuLTS` 별칭을 사용하여 Ubuntu 14.04.4 LTS Server를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="0febc-155">이전 `quick-create` 예제에서는 SSH 암호를 비활성화하는 동안 업로드할 SSH 공개 키를 식별하기 위해 `-M` 플래그만 호출했으므로, 다음 인수를 묻는 메시지가 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="0febc-156">리소스 그룹 이름(일반적으로 첫 번째 Azure 리소스 그룹에 대해서는 어떤 문자열이든 적합함).</span><span class="sxs-lookup"><span data-stu-id="0febc-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="0febc-157">VM 이름</span><span class="sxs-lookup"><span data-stu-id="0febc-157">VM name</span></span>
* <span data-ttu-id="0febc-158">위치(좋은 기본값은 `westus` 또는 `westeurope`입니다.)</span><span class="sxs-lookup"><span data-stu-id="0febc-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="0febc-159">linux(원하는 OS가 무엇인지 Azure에 알림)</span><span class="sxs-lookup"><span data-stu-id="0febc-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="0febc-160">username</span><span class="sxs-lookup"><span data-stu-id="0febc-160">username</span></span>

<span data-ttu-id="0febc-161">다음 예제는 추가 메시지 표시가 필요하지 않도록 모든 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="0febc-162">`~/.ssh/id_rsa.pub`을 ssh-rsa 형식의 공개 키 파일로 포함하고 있으면 해당 파일은 있는 그대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="0febc-163">출력에는 다음과 같은 출력 블록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="0febc-164">새 VM에 로그인</span><span class="sxs-lookup"><span data-stu-id="0febc-164">Log in to the new VM</span></span>
<span data-ttu-id="0febc-165">출력에 나열된 공용 IP 주소를 사용하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="0febc-166">나열된 FQDN(정규화된 도메인 이름)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="0febc-167">로그인 프로세스는 다음 출력 블록과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="0febc-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0febc-168">Next steps</span></span>
<span data-ttu-id="0febc-169">`azure vm quick-create` 명령은 Bash 셸에 로그인하고 작업할 수 있도록 VM을 신속하게 배포하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="0febc-170">그러나 `vm quick-create` 를 사용하면 광범위한 제어가 불가능하며 더 복잡한 환경을 만들 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="0febc-171">이러한 문서 중 하나를 수행하여 인프라에 대해 사용자 지정된 Linux VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0febc-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="0febc-172">Azure CLI 명령을 직접 사용하여 Linux VM에 대한 고유한 사용자 지정 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="0febc-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0febc-173">템플릿을 사용하여 Azure에서 SSH 보안 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0febc-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="0febc-174">[다양한 명령으로 `docker-machine` Azure 드라이버를 사용하여 Linux VM을 Docker 호스트로 신속하게 만들 수 있습니다](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0febc-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
