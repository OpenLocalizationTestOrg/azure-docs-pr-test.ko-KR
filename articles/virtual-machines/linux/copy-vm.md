---
title: "Azure CLI 2.0을 사용 하 여 Linux VM aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure CLI 2.0 및 관리 하는 디스크를 사용 하 여 Azure Linux VM의 복사본입니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="c3059-103">Azure CLI 2.0 및 Managed Disks를 사용하여 Linux VM의 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="c3059-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="c3059-104">이 문서에서는 Azure CLI 2.0 및 Azure 리소스 관리자 배포 모델 hello toocreate Linux를 사용 하 여 실행 중인 Azure 가상 컴퓨터 (VM)의 사본을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c3059-105">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c3059-106">[VHD에서 VM을 업로드하고 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3059-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3059-107">Prerequisites</span></span>


-   <span data-ttu-id="c3059-108">[Azure CLI 2.0](/cli/azure/install-az-cli2) 설치</span><span class="sxs-lookup"><span data-stu-id="c3059-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="c3059-109">Tooan 된 Azure 계정 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="c3059-110">Azure VM toouse 복사본에 대 한 hello 소스로 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="c3059-111">1 단계: hello 원본 VM 중지</span><span class="sxs-lookup"><span data-stu-id="c3059-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="c3059-112">사용 하 여 hello 원본 VM을 할당 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="c3059-113">hello 다음 예제에서는 할당 취소 hello 라는 VM **myVM** hello 리소스 그룹에 **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="c3059-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="c3059-114">2 단계: hello 원본 VM 복사</span><span class="sxs-lookup"><span data-stu-id="c3059-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="c3059-115">VM toocopy hello 기본 가상 하드 디스크의 복사본이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="c3059-116">이 프로세스는 hello를 포함 하는 관리 되는 디스크도 특수화 된 VHD를 만듭니다 원본 VM 동일한 구성 및 hello로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="c3059-117">Azure Managed Disks에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3059-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="c3059-118">해당 운영 체제 디스크의 각 VM 및 hello 이름 목록 [az vm 목록](/cli/azure/vm#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="c3059-119">hello 다음 예에서는 나열은 리소스 그룹에 모든 Vm **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="c3059-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="c3059-120">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="c3059-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="c3059-121">디스크를 사용 하 여 새 복사본 hello 디스크 관리 [az 디스크 만들기](/cli/azure/disk#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="c3059-122">hello 다음 예제에서는 명명 된 디스크 **myCopiedDisk** 관리 라는 디스크 hello에서 **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="c3059-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="c3059-123">이제 리소스 그룹에서에서 관리 하는 hello 디스크를 사용 하 여 확인 [az 디스크 목록](/cli/azure/disk#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="c3059-124">hello 다음 예에서는 나열 이라는 hello 리소스 그룹의 관리 되는 hello 디스크 **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="c3059-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="c3059-125">너무 건너뛸["3 단계: 가상 네트워크 설정"](#step-3-set-up-a-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="c3059-126">3단계: 가상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="c3059-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="c3059-127">hello 다음 옵션 단계로 만들 새 가상 네트워크, 서브넷, 공용 IP 주소 및 가상 네트워크 인터페이스 카드 (NIC).</span><span class="sxs-lookup"><span data-stu-id="c3059-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="c3059-128">용도 또는 추가 배포 문제 해결에 대 한 VM을 복사 하는 경우 하지 toouse 기존 가상 네트워크에 VM을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="c3059-129">복사 된 Vm에 대 한 가상 네트워크 인프라 toocreate 하려는 경우에 따라 hello 다음 몇 가지 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="c3059-130">Toocreate 가상 네트워크를 사용 하지 않으려는 경우 너무 건너뜁니다[4 단계: VM 만들기](#step-4-create-a-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="c3059-131">사용 하 여 hello 가상 네트워크 만들기 [az 네트워크 vnet 만들기](/cli/azure/network/vnet#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c3059-132">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 **myVnet** 및 명명 된 서브넷 **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="c3059-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="c3059-133">[az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="c3059-134">hello 다음 예제에서는 명명 된 공용 IP **myPublicIP** 의 hello DNS 이름을 가진 **mypublicdns**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="c3059-135">(이므로 고유 이름을 제공, 고유 해야 hello DNS 이름입니다.)</span><span class="sxs-lookup"><span data-stu-id="c3059-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="c3059-136">Hello NIC를 사용 하 여 만들 [az 네트워크 nic 만들](/cli/azure/network/nic#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="c3059-137">hello 다음 예제에서는 명명 된 NIC **myNic** 는 연결 된 toothe **mySubnet** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="c3059-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="c3059-138">4단계: VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c3059-138">Step 4: Create a VM</span></span>

<span data-ttu-id="c3059-139">이제 [az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="c3059-140">관리 되는 디스크 toouse hello OS 디스크로 복사 하는 hello 지정 (--os-디스크 연결), 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="c3059-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3059-141">Next steps</span></span>

<span data-ttu-id="c3059-142">toolearn 어떻게 toouse Azure CLI toomanage 새 VM 참조 [hello Azure 리소스 관리자에 대 한 Azure CLI 명령을](../azure-cli-arm-commands.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3059-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
