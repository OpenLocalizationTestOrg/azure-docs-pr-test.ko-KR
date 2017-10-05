---
title: "Azure CLI로 Linux VM 만들기 및 관리 | Microsoft Docs"
description: "자습서 - Azure CLI로 Linux VM 만들기 및 관리"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a><span data-ttu-id="85167-103">Azure CLI로 Linux VM 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="85167-103">Create and Manage Linux VMs with the Azure CLI</span></span>

<span data-ttu-id="85167-104">Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="85167-105">이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="85167-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85167-107">VM 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="85167-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="85167-108">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="85167-108">Select and use VM images</span></span>
> * <span data-ttu-id="85167-109">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="85167-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="85167-110">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="85167-110">Resize a VM</span></span>
> * <span data-ttu-id="85167-111">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="85167-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="85167-112">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="85167-113">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="85167-114">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85167-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="85167-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="85167-115">Create resource group</span></span>

<span data-ttu-id="85167-116">[az group create](https://docs.microsoft.com/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85167-116">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="85167-117">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="85167-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="85167-118">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="85167-119">이 예제에서는 *eastus* 지역에 *myResourceGroupVM*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85167-119">In this example, a resource group named *myResourceGroupVM* is created in the *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="85167-120">리소스 그룹은 VM을 만들거나 수정할 때 지정되며 이 자습서 전체에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="85167-121">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="85167-121">Create virtual machine</span></span>

<span data-ttu-id="85167-122">[az vm create](https://docs.microsoft.com/cli/azure/vm#create) 명령을 사용하여 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85167-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="85167-123">가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="85167-124">이 예제에서는 Ubuntu Server를 실행하는 *myVM*이라는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85167-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="85167-125">VM이 만들어지면 Azure CLI에서 VM에 대한 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-125">Once the VM has been created, the Azure CLI outputs information about the VM.</span></span> <span data-ttu-id="85167-126">`publicIpAddress`를 메모해 둡니다. 이 주소는 가상 컴퓨터에 액세스하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-126">Take note of the `publicIpAddress`, this address can be used to access the virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-to-vm"></a><span data-ttu-id="85167-127">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="85167-127">Connect to VM</span></span>

<span data-ttu-id="85167-128">이제 SSH를 사용하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-128">You can now connect to the VM using SSH.</span></span> <span data-ttu-id="85167-129">예제 IP 주소를 이전 단계에서 메모한 `publicIpAddress`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="85167-129">Replace the example IP address with the `publicIpAddress` noted in the previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="85167-130">VM 작업을 완료했으면 SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-130">Once finished with the VM, close the SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="85167-131">VM 이미지 이해</span><span class="sxs-lookup"><span data-stu-id="85167-131">Understand VM images</span></span>

<span data-ttu-id="85167-132">Azure Marketplace에는 VM을 만드는 데 사용할 수 있는 여러 VM 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-132">The Azure marketplace includes many images that can be used to create VMs.</span></span> <span data-ttu-id="85167-133">이전 단계에서는 Ubuntu 이미지를 사용하여 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-133">In the previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="85167-134">이 단계에서는 Azure CLI를 사용하여 Marketplace에서 CentOS 이미지를 검색한 후 두 번째 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-134">In this step, the Azure CLI is used to search the marketplace for a CentOS image, which is then used to deploy a second virtual machine.</span></span>  

<span data-ttu-id="85167-135">가장 일반적으로 사용되는 이미지 목록을 보려면 [az vm image list](/cli/azure/vm/image#list) 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="85167-135">To see a list of the most commonly used images, use the [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="85167-136">명령 출력은 Azure에서 가장 인기 있는 VM 이미지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-136">The command output returns the most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="85167-137">전체 목록은 `--all` 인수를 추가하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-137">A full list can be seen by adding the `--all` argument.</span></span> <span data-ttu-id="85167-138">이미지 목록은 `--publisher` 또는 `–-offer`로 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-138">The image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="85167-139">이 예제에서는 *CentOS*와 일치하는 제품이 있는 모든 이미지에 대해 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-139">In this example, the list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="85167-140">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="85167-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="85167-141">특정 이미지를 사용하여 VM을 배포하려면 *Urn* 열에서 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="85167-141">To deploy a VM using a specific image, take note of the value in the *Urn* column.</span></span> <span data-ttu-id="85167-142">이미지를 지정하면 이미지 버전 번호는 최신 버전의 배포를 선택하도록 “최신”으로 대체될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-142">When specifying the image, the image version number can be replaced with “latest”, which selects the latest version of the distribution.</span></span> <span data-ttu-id="85167-143">이 예제에서는 CentOS 6.5 이미지의 최신 버전을 지정하기 위해 `--image` 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-143">In this example, the `--image` argument is used to specify the latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="85167-144">VM 크기 이해</span><span class="sxs-lookup"><span data-stu-id="85167-144">Understand VM sizes</span></span>

<span data-ttu-id="85167-145">가상 컴퓨터 크기에 따라 CPU, GPU, 메모리 등 가상 컴퓨터에 사용할 수 있는 계산 리소스의 양이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-145">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="85167-146">가상 컴퓨터는 예상되는 워크로드에 맞게 적절히 크기 조정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-146">Virtual machines need to be sized appropriately for the expected work load.</span></span> <span data-ttu-id="85167-147">워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="85167-148">VM 크기</span><span class="sxs-lookup"><span data-stu-id="85167-148">VM Sizes</span></span>

<span data-ttu-id="85167-149">다음 표에서는 크기를 사용 사례로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-149">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="85167-150">형식</span><span class="sxs-lookup"><span data-stu-id="85167-150">Type</span></span>                     | <span data-ttu-id="85167-151">크기</span><span class="sxs-lookup"><span data-stu-id="85167-151">Sizes</span></span>           |    <span data-ttu-id="85167-152">설명</span><span class="sxs-lookup"><span data-stu-id="85167-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="85167-153">범용</span><span class="sxs-lookup"><span data-stu-id="85167-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="85167-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="85167-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="85167-155">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="85167-156">개발/테스트와 소규모에서 중간 정도의 응용 프로그램 및 데이터 솔루션에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-156">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| [<span data-ttu-id="85167-157">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="85167-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="85167-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="85167-158">Fs, F</span></span>             | <span data-ttu-id="85167-159">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-159">High CPU-to-memory.</span></span> <span data-ttu-id="85167-160">트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="85167-161">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="85167-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="85167-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="85167-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="85167-163">메모리 대 코어 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-163">High memory-to-core.</span></span> <span data-ttu-id="85167-164">관계형 데이터베이스, 중대형 캐시 및 메모리 내 분석에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-164">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="85167-165">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="85167-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="85167-166">Ls</span><span class="sxs-lookup"><span data-stu-id="85167-166">Ls</span></span>                | <span data-ttu-id="85167-167">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="85167-167">High disk throughput and IO.</span></span> <span data-ttu-id="85167-168">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="85167-169">GPU</span><span class="sxs-lookup"><span data-stu-id="85167-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="85167-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="85167-170">NV, NC</span></span>            | <span data-ttu-id="85167-171">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="85167-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="85167-172">고성능</span><span class="sxs-lookup"><span data-stu-id="85167-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="85167-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="85167-173">H, A8-11</span></span>          | <span data-ttu-id="85167-174">당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="85167-175">사용 가능한 VM 크기 찾기</span><span class="sxs-lookup"><span data-stu-id="85167-175">Find available VM sizes</span></span>

<span data-ttu-id="85167-176">특정 지역에서 사용할 수 있는 VM 크기의 목록을 보려면 [az vm list-sizes](/cli/azure/vm#list-sizes) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-176">To see a list of VM sizes available in a particular region, use the [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="85167-177">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="85167-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="85167-178">특정 크기로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="85167-178">Create VM with specific size</span></span>

<span data-ttu-id="85167-179">이전 VM 만들기 예제에서는 크기가 제공되지 않았으므로 기본 크기가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-179">In the previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="85167-180">[az vm create](/cli/azure/vm#create) 및 `--size` 인수를 사용하여 만들 때 VM 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and the `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="85167-181">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="85167-181">Resize a VM</span></span>

<span data-ttu-id="85167-182">VM을 배포한 후에 크기를 조정하여 리소스 할당을 늘리거나 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-182">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="85167-183">VM의 크기를 조정하기 전에 원하는 크기를 현재 Azure 클러스터에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-183">Before resizing a VM, check if the desired size is available on the current Azure cluster.</span></span> <span data-ttu-id="85167-184">[az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) 명령은 크기 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-184">The [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns the list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="85167-185">원하는 크기를 사용할 수 있는 경우 전원이 켜진 상태에서 VM 크기를 조정할 수 있지만 작업 중 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-185">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span> <span data-ttu-id="85167-186">[az vm resize]( /cli/azure/vm#resize) 명령을 사용하여 크기 조정을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-186">Use the [az vm resize]( /cli/azure/vm#resize) command to perform the resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="85167-187">원하는 크기가 현재 클러스터에 없는 경우 크기 조정 작업 전에 VM 할당을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-187">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="85167-188">[az vm deallocate]( /cli/azure/vm#deallocate) 명령을 사용하여 VM을 중지하고 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-188">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span> <span data-ttu-id="85167-189">참고로 VM의 전원이 다시 켜지면 임시 디스크의 모든 데이터가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-189">Note, when the VM is powered back on, any data on the temp disk may be removed.</span></span> <span data-ttu-id="85167-190">고정 IP 주소를 사용하지 않는 한 공용 IP 주소도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-190">The public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="85167-191">할당 취소되면 크기 조정이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-191">Once deallocated, the resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="85167-192">크기를 조정한 후 VM을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-192">After the resize, the VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="85167-193">VM 전원 상태</span><span class="sxs-lookup"><span data-stu-id="85167-193">VM power states</span></span>

<span data-ttu-id="85167-194">Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="85167-195">이 상태는 하이퍼바이저의 관점에서 VM의 현재 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-195">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="85167-196">전원 상태</span><span class="sxs-lookup"><span data-stu-id="85167-196">Power states</span></span>

| <span data-ttu-id="85167-197">전원 상태</span><span class="sxs-lookup"><span data-stu-id="85167-197">Power State</span></span> | <span data-ttu-id="85167-198">설명</span><span class="sxs-lookup"><span data-stu-id="85167-198">Description</span></span>
|----|----|
| <span data-ttu-id="85167-199">Starting</span><span class="sxs-lookup"><span data-stu-id="85167-199">Starting</span></span> | <span data-ttu-id="85167-200">가상 컴퓨터가 시작되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-200">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="85167-201">실행 중</span><span class="sxs-lookup"><span data-stu-id="85167-201">Running</span></span> | <span data-ttu-id="85167-202">가상 컴퓨터가 실행되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-202">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="85167-203">중지 중</span><span class="sxs-lookup"><span data-stu-id="85167-203">Stopping</span></span> | <span data-ttu-id="85167-204">가상 컴퓨터가 중지되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-204">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="85167-205">중지됨</span><span class="sxs-lookup"><span data-stu-id="85167-205">Stopped</span></span> | <span data-ttu-id="85167-206">가상 컴퓨터가 중지되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-206">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="85167-207">중지됨 상태의 가상 컴퓨터에도 여전히 계산 요금이 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-207">Virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="85167-208">할당 취소 중</span><span class="sxs-lookup"><span data-stu-id="85167-208">Deallocating</span></span> | <span data-ttu-id="85167-209">가상 컴퓨터의 할당이 취소되고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-209">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="85167-210">할당 취소됨</span><span class="sxs-lookup"><span data-stu-id="85167-210">Deallocated</span></span> | <span data-ttu-id="85167-211">가상 컴퓨터가 하이퍼바이저에서 제거되었지만 제어 영역에서 계속 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-211">Indicates that the virtual machine is removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="85167-212">할당 취소됨 상태의 가상 컴퓨터에는 계산 요금이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-212">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="85167-213">가상 컴퓨터의 전원 상태가 알 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85167-213">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="85167-214">전원 상태 찾기</span><span class="sxs-lookup"><span data-stu-id="85167-214">Find power state</span></span>

<span data-ttu-id="85167-215">특정 VM의 상태를 검색하려면 [az vm get instance-view](/cli/azure/vm#get-instance-view) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-215">To retrieve the state of a particular VM, use the [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="85167-216">가상 컴퓨터 및 리소스 그룹에 대한 올바른 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-216">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="85167-217">출력:</span><span class="sxs-lookup"><span data-stu-id="85167-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="85167-218">관리 작업</span><span class="sxs-lookup"><span data-stu-id="85167-218">Management tasks</span></span>

<span data-ttu-id="85167-219">가상 컴퓨터의 수명 주기 동안 가상 컴퓨터 시작, 중지 또는 삭제 등의 관리 작업을 실행하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-219">During the life-cycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="85167-220">또한 반복적이거나 복잡한 작업을 자동화하는 스크립트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-220">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="85167-221">Azure CLI를 사용하여 명령줄이나 스크립트에서 여러 가지 일반적인 관리 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-221">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="85167-222">IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="85167-222">Get IP address</span></span>

<span data-ttu-id="85167-223">이 명령은 가상 컴퓨터의 개인 및 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-223">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="85167-224">가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="85167-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="85167-225">가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="85167-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="85167-226">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="85167-226">Delete resource group</span></span>

<span data-ttu-id="85167-227">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="85167-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="85167-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85167-228">Next steps</span></span>

<span data-ttu-id="85167-229">이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="85167-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85167-230">VM 만들기 및 연결</span><span class="sxs-lookup"><span data-stu-id="85167-230">Create and connect to a VM</span></span>
> * <span data-ttu-id="85167-231">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="85167-231">Select and use VM images</span></span>
> * <span data-ttu-id="85167-232">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="85167-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="85167-233">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="85167-233">Resize a VM</span></span>
> * <span data-ttu-id="85167-234">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="85167-234">View and understand VM state</span></span>

<span data-ttu-id="85167-235">VM 디스크에 대해 자세히 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="85167-235">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="85167-236">VM 디스크 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="85167-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
