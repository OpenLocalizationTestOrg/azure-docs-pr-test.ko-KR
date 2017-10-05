---
title: "OpenBSD VM 이미지 만들기 및 Azure로 업로드 | Microsoft Docs"
description: "OpenBSD 운영 체제가 포함된 VHD(가상 하드 디스크)를 만들고 업로드하여 Azure CLI를 통해 Azure 가상 컴퓨터를 만드는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 716c07f6a738189d6cf2b3caafa16b753927d182
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-to-azure"></a><span data-ttu-id="0c600-103">OpenBSD 디스크 이미지 만들기 및 Azure로 업로드</span><span class="sxs-lookup"><span data-stu-id="0c600-103">Create and Upload an OpenBSD disk image to Azure</span></span>
<span data-ttu-id="0c600-104">이 문서에서는 OpenBSD 운영 체제가 포함된 VHD(가상 하드 디스크)를 만들고 업로드하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the OpenBSD operating system.</span></span> <span data-ttu-id="0c600-105">VHD를 업로드한 후에는 VHD를 사용자 고유의 이미지로 사용하여 Azure CLI를 통해 Azure에서 VM(가상 컴퓨터)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0c600-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0c600-106">Prerequisites</span></span>
<span data-ttu-id="0c600-107">이 문서에서는 사용자에게 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-107">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="0c600-108">**Azure 구독** - 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="0c600-109">MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="0c600-110">그렇지 않으면 [무료 평가판 계정 만들기](https://azure.microsoft.com/pricing/free-trial/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-110">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="0c600-111">**Azure CLI 2.0** - 최신 [Azure CLI 2.0](/cli/azure/install-azure-cli)을 설치했고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-111">**Azure CLI 2.0** - Make sure you have the latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in to your Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="0c600-112">**.vhd 파일에 설치된 OpenBSD 운영 체제** - 가상 하드 디스크에 지원되는 OpenBSD 운영 체제(6.1 버전)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed to a virtual hard disk.</span></span> <span data-ttu-id="0c600-113">.vhd 파일을 만드는 도구는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-113">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="0c600-114">예를 들어 Hyper-V와 같은 가상화 솔루션을 사용하여 .vhd 파일을 만들고 운영 체제를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-114">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="0c600-115">Hyper-V를 설치하고 사용하는 방법에 대한 자세한 내용은 [Hyper-V 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-115">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="0c600-116">OpenBSD 이미지를 Azure에 사용하도록 준비</span><span class="sxs-lookup"><span data-stu-id="0c600-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="0c600-117">Hyper-V 지원을 추가한, OpenBSD 운영 체제 6.1을 설치한 VM에서 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-117">On the VM where you installed the OpenBSD operating system 6.1, which added Hyper-V support, complete the following procedures:</span></span>

1. <span data-ttu-id="0c600-118">설치하는 동안 DHCP가 사용하도록 설정되지 않은 경우 다음과 같이 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-118">If DHCP is not enabled during installation, enable the service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="0c600-119">다음과 같이 직렬 콘솔을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="0c600-120">다음과 같이 패키지 설치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="0c600-121">기본적으로 `root` 사용자는 Azure의 가상 컴퓨터에서는 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-121">By default, the `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="0c600-122">사용자는 OpenBSD VM에서 `doas` 명령을 사용하여 상승된 권한으로 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-122">Users can run commands with elevated privileges by using the `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="0c600-123">Doas는 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-123">Doas is enabled by default.</span></span> <span data-ttu-id="0c600-124">자세한 내용은 [doas.conf](http://man.openbsd.org/doas.conf.5)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="0c600-125">다음과 같이 Azure 에이전트에 대한 필수 구성 요소를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-125">Install and configure prerequisites for the Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="0c600-126">언제든지 최신 버전의 Azure 에이전트를 [Github](https://github.com/Azure/WALinuxAgent/releases)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-126">The latest release of the Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="0c600-127">다음과 같이 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-127">Install the agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0c600-128">Azure 에이전트를 설치한 후 다음과 같이 에이전트가 실행 중인지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-128">After you install Azure Agent, it's a good idea to verify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="0c600-129">시스템을 프로비전 해제하여 다시 프로비전하기에 적합한 상태로 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-129">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="0c600-130">다음 명령은 마지막으로 프로비전된 사용자 계정 및 관련 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-130">The following command also deletes the last provisioned user account and the associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="0c600-131">이제 VM을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-131">Now you can shut down your VM.</span></span>


## <a name="prepare-the-vhd"></a><span data-ttu-id="0c600-132">VHD 준비</span><span class="sxs-lookup"><span data-stu-id="0c600-132">Prepare the VHD</span></span>
<span data-ttu-id="0c600-133">VHDX 형식은 Azure에서 지원되지 않습니다. **고정된 VHD**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-133">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="0c600-134">Hyper-V 관리자 또는 Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet을 사용하여 디스크를 고정 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-134">You can convert the disk to fixed VHD format using Hyper-V Manager or the Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="0c600-135">예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="0c600-136">저장소 리소스 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="0c600-136">Create storage resources and upload</span></span>
<span data-ttu-id="0c600-137">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0c600-138">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0c600-139">VHD를 업로드하려면 [az storage account create](/cli/azure/storage/account#create)를 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-139">To upload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="0c600-140">저장소 계정 이름은 고유해야 하므로 자신만의 이름을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="0c600-141">다음 예제에서는 *mystorageaccount*라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-141">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="0c600-142">저장소 계정에 대한 액세스를 제어하려면 다음과 같이 [az storage account key list](/cli/azure/storage/account/keys#list)를 사용하여 저장소 키를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-142">To control access to the storage account, obtain the storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="0c600-143">업로드하는 VHD를 논리적으로 분리하려면 [az storage container create](/cli/azure/storage/container#create)를 사용하여 저장소 계정 내에서 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-143">To logically separate the VHDs you upload, create a container within the storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="0c600-144">마지막으로 다음과 같이 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="0c600-145">VHD에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0c600-145">Create VM from your VHD</span></span>
<span data-ttu-id="0c600-146">[샘플 스크립트](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md)를 사용하거나 직접 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0c600-147">업로드한 OpenBSD VHD를 지정하려면 다음과 같이 `--image` 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-147">To specify the OpenBSD VHD you uploaded, use the `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="0c600-148">다음과 같이 [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses)를 사용하여 OpenBSD VM의 IP 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-148">Obtain the IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="0c600-149">이제 정상적으로 OpenBSD VM에 SSH할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c600-149">Now you can SSH to your OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="0c600-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c600-150">Next steps</span></span>
<span data-ttu-id="0c600-151">OpenBSD6.1의 Hyper-V 지원에 대한 자세한 내용은 [OpenBSD 6.1](https://www.openbsd.org/61.html) 및 [hyperv.4](http://man.openbsd.org/hyperv.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-151">If you want to know more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="0c600-152">관리 디스크에서 VM을 만들려면 [az disk](/cli/azure/disk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c600-152">If you want to create a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 