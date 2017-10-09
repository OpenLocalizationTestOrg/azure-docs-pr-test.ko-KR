---
title: "aaaCreate 및 업로드 OpenBSD VM 이미지 tooAzure | Microsoft Docs"
description: "어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello OpenBSD 운영 체제 toocreate Azure CLI를 통해 Azure 가상 컴퓨터에 알아봅니다"
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
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="77210-103">만들기 및 업로드 OpenBSD 디스크 이미지 tooAzure</span><span class="sxs-lookup"><span data-stu-id="77210-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="77210-104">이 문서에서는 어떻게 toocreate 및 업로드를 포함 하는 가상 하드 디스크 (VHD) hello OpenBSD 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="77210-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="77210-105">를 업로드 한 후에 사용자 고유의 이미지 toocreate Azure CLI를 통해 Azure에서 가상 컴퓨터 (VM)으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="77210-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="77210-106">Prerequisites</span></span>
<span data-ttu-id="77210-107">이 문서에서는 다음 항목 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="77210-108">**Azure 구독** - 계정이 없는 경우 몇 분 만에 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="77210-109">MSDN 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77210-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="77210-110">그렇지 않은 경우 너무 방법을 알아보려면[무료 평가판 계정을 만들](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="77210-111">**Azure CLI 2.0** -있는지 hello 최신 [Azure CLI 2.0](/cli/azure/install-azure-cli) 설치 하 고 tooyour 된 Azure 계정 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="77210-112">**.Vhd 파일에 설치 된 OpenBSD 운영 체제** -지원 되는 OpenBSD 운영 체제 (버전 6.1) 설치 된 tooa 가상 하드 디스크 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="77210-113">여러 도구 toocreate.vhd 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="77210-114">예를 들어 Hyper-v toocreate hello.vhd 파일 등 가상화 솔루션을 사용 하 고 hello 운영 체제를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="77210-115">Tooinstall 및 Hyper-v를 사용 하 여 참조 하는 방법에 대 한 지침은 [Hyper-v 설치 및 가상 컴퓨터 만들기](http://technet.microsoft.com/library/hh846766.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="77210-116">OpenBSD 이미지를 Azure에 사용하도록 준비</span><span class="sxs-lookup"><span data-stu-id="77210-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="77210-117">Hello hello OpenBSD 운영 체제 6.1, Hyper-v 지원 추가 설치한 VM hello 다음 절차를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="77210-118">DHCP를 설치 하는 동안 사용 하지 않는 hello 서비스를 다음과 같이 설정.</span><span class="sxs-lookup"><span data-stu-id="77210-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="77210-119">다음과 같이 직렬 콘솔을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="77210-120">다음과 같이 패키지 설치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="77210-121">기본적으로 hello `root` Azure의 가상 컴퓨터에서 사용자가 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="77210-122">사용자가 hello를 사용 하 여 상승 된 권한으로 명령에 실행할 수 `doas` OpenBSD VM에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="77210-123">Doas는 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="77210-123">Doas is enabled by default.</span></span> <span data-ttu-id="77210-124">자세한 내용은 [doas.conf](http://man.openbsd.org/doas.conf.5)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77210-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="77210-125">설치 및 hello Azure 에이전트에 대 한 필수 구성 요소를 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="77210-126">항상 hello hello Azure 에이전트의 최신 릴리스를 찾을 수 [Github](https://github.com/Azure/WALinuxAgent/releases)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="77210-127">다음과 같이 hello 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="77210-128">Azure 에이전트를 설치한 후 다음과 같이 실행 하는 것이 좋습니다 tooverify 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77210-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="77210-129">프로 비전 해제 하 고 확인 시스템 tooclean hello 다시 프로 비전에 대 한 적합 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77210-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="77210-130">hello 다음 명령은 삭제 hello 마지막 프로 비전 된 사용자 계정과 연결 된 hello 데이터:</span><span class="sxs-lookup"><span data-stu-id="77210-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="77210-131">이제 VM을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="77210-132">Hello VHD를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-132">Prepare hello VHD</span></span>
<span data-ttu-id="77210-133">hello VHDX 형식은 지원 되지 않습니다 Azure에서만 **고정 VHD**합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="77210-134">Hyper-v 관리자를 사용 하 여 hello 디스크 toofixed VHD 형식으로 변환 하거나 Powershell hello 수 [convert vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77210-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="77210-135">예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="77210-136">저장소 리소스 만들기 및 업로드</span><span class="sxs-lookup"><span data-stu-id="77210-136">Create storage resources and upload</span></span>
<span data-ttu-id="77210-137">먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77210-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="77210-138">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="77210-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="77210-139">tooupload VHD를 사용 하는 저장소 계정 만들기 [az 저장소 계정에 create](/cli/azure/storage/account#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="77210-140">저장소 계정 이름은 고유해야 하므로 자신만의 이름을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="77210-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="77210-141">hello 다음 예제에서는 저장소 계정인 *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="77210-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="77210-142">toocontrol toohello 저장소 계정에 액세스를 사용 하 여 hello 저장소 키를 받아야 [az 저장소 계정 키 목록](/cli/azure/storage/account/keys#list) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="77210-143">toologically 별도 hello Vhd를 업로드 된 hello 저장소 계정 내에서 컨테이너를 만들 [az 저장소 컨테이너 만들기](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="77210-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="77210-144">마지막으로 다음과 같이 [az storage blob upload](/cli/azure/storage/blob#upload)를 사용하여 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="77210-145">VHD에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="77210-145">Create VM from your VHD</span></span>
<span data-ttu-id="77210-146">[샘플 스크립트](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md)를 사용하거나 직접 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="77210-147">toospecify hello OpenBSD VHD 업로드를 사용 하 여 hello `--image` 다음과 같이 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="77210-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="77210-148">Hello IP 주소를 사용 하 여 OpenBSD VM에 대 한 가져오기 [az vm 목록-ip-주소](/cli/azure/vm#list-ip-addresses) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="77210-149">이제 일반적인 방법으로 SSH tooyour OpenBSD VM에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77210-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="77210-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77210-150">Next steps</span></span>
<span data-ttu-id="77210-151">Tooknow OpenBSD6.1에서 Hyper-v에 대 한 자세한 정보를 지원 하려면 읽기 [OpenBSD 6.1](https://www.openbsd.org/61.html) 및 [hyperv.4](http://man.openbsd.org/hyperv.4)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="77210-152">관리 되는 디스크에서 VM toocreate 읽을 [az 디스크](/cli/azure/disk)합니다.</span><span class="sxs-lookup"><span data-stu-id="77210-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
