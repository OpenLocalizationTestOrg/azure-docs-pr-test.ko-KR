---
title: "Linux Vm을 관리 하 고 aaaCreate hello Azure CLI | Microsoft Docs"
description: "자습서에서 만들고 있는 Linux Vm 관리 hello Azure CLI"
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
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="e4c89-103">만들고 있는 Linux Vm 관리 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e4c89-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="e4c89-104">Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="e4c89-105">이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="e4c89-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4c89-107">만들고 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="e4c89-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e4c89-108">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="e4c89-108">Select and use VM images</span></span>
> * <span data-ttu-id="e4c89-109">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="e4c89-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e4c89-110">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e4c89-110">Resize a VM</span></span>
> * <span data-ttu-id="e4c89-111">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="e4c89-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e4c89-112">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="e4c89-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e4c89-113">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e4c89-114">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="e4c89-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e4c89-115">Create resource group</span></span>

<span data-ttu-id="e4c89-116">Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="e4c89-117">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e4c89-118">가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="e4c89-119">이 예제에서는 리소스 그룹 이름이 *myResourceGroupVM* hello에서 만든 *eastus* 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="e4c89-120">hello 리소스 그룹은 생성 하거나이 자습서 전체에서 볼 수 있는 VM을 수정할 때 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="e4c89-121">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="e4c89-121">Create virtual machine</span></span>

<span data-ttu-id="e4c89-122">Hello로 가상 컴퓨터를 만들 [az vm 만들기](https://docs.microsoft.com/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="e4c89-123">가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="e4c89-124">이 예제에서는 Ubuntu Server를 실행하는 *myVM*이라는 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="e4c89-125">한 번 VM을 만든 hello, hello Azure CLI hello VM에 대 한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="e4c89-126">Hello를 메모해 `publicIpAddress`,이 주소에서 사용 되는 tooaccess hello 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

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

## <a name="connect-toovm"></a><span data-ttu-id="e4c89-127">TooVM 연결</span><span class="sxs-lookup"><span data-stu-id="e4c89-127">Connect tooVM</span></span>

<span data-ttu-id="e4c89-128">연결할 수 있습니다. VM toohello SSH를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="e4c89-129">Hello로 hello 예제 IP 주소를 교체 `publicIpAddress` hello 이전 단계에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="e4c89-130">VM hello로 완료 되 면 hello SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="e4c89-131">VM 이미지 이해</span><span class="sxs-lookup"><span data-stu-id="e4c89-131">Understand VM images</span></span>

<span data-ttu-id="e4c89-132">hello Azure 마켓플레이스 사용된 toocreate Vm 수 있는 여러 이미지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="e4c89-133">Hello 이전 단계에서 Ubuntu 이미지를 사용 하 여 가상 컴퓨터를 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="e4c89-134">이 단계에서는 Azure CLI는 CentOS 이미지의 경우이 사용 하는 toosearch hello 마켓플레이스는 hello toodeploy 두 번째 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="e4c89-135">hello 목록이 toosee 가장 일반적으로 사용 되는 이미지, hello를 사용 하 여 [az vm 이미지 목록을](/cli/azure/vm/image#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="e4c89-136">Azure의 hello 가장 인기 있는 VM 이미지를 반환 하는 hello 명령 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-136">hello command output returns hello most popular VM images on Azure.</span></span>

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

<span data-ttu-id="e4c89-137">Hello를 추가 하 여 전체 목록을 볼 수 있습니다 `--all` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="e4c89-138">hello 이미지 목록에서 필터링 할 수도 있습니다 `--publisher` 또는 `–-offer`합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="e4c89-139">이 예제에서는 일치 하는 제공 된 모든 이미지에 대 한 hello 목록 필터링 *CentOS*합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="e4c89-140">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="e4c89-140">Partial output:</span></span>

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

<span data-ttu-id="e4c89-141">특정 이미지를 사용 하는 VM toodeploy hello 값에서에서 기록해 hello *Urn* 열입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="e4c89-142">Hello 이미지를 지정할 때는 hello 이미지 버전 번호 수로 바뀝니다 "최신" hello hello 분포의 최신 버전을 선택 하는.</span><span class="sxs-lookup"><span data-stu-id="e4c89-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="e4c89-143">이 예제에서는 hello `--image` 인수는 사용 되는 toospecify hello CentOS 6.5 이미지의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="e4c89-144">VM 크기 이해</span><span class="sxs-lookup"><span data-stu-id="e4c89-144">Understand VM sizes</span></span>

<span data-ttu-id="e4c89-145">가상 컴퓨터 크기는 hello 양의 toohello 사용 가능한 가상 컴퓨터에 적용 된 메모리, CPU 및 GPU, 등 계산 리소스를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="e4c89-146">가상 컴퓨터 작업 부하 예상 hello에 대 한 크기가 적합 toobe를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="e4c89-147">워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="e4c89-148">VM 크기</span><span class="sxs-lookup"><span data-stu-id="e4c89-148">VM Sizes</span></span>

<span data-ttu-id="e4c89-149">다음 표에서 hello 사용 사례에 크기를 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="e4c89-150">형식</span><span class="sxs-lookup"><span data-stu-id="e4c89-150">Type</span></span>                     | <span data-ttu-id="e4c89-151">크기</span><span class="sxs-lookup"><span data-stu-id="e4c89-151">Sizes</span></span>           |    <span data-ttu-id="e4c89-152">설명</span><span class="sxs-lookup"><span data-stu-id="e4c89-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="e4c89-153">범용</span><span class="sxs-lookup"><span data-stu-id="e4c89-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="e4c89-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="e4c89-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="e4c89-155">CPU 대 메모리 비율이 적당합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="e4c89-156">개발에 대 한 이상적인 / 테스트 및 소규모 toomedium 응용 프로그램 및 데이터 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="e4c89-157">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="e4c89-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="e4c89-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="e4c89-158">Fs, F</span></span>             | <span data-ttu-id="e4c89-159">CPU 대 메모리 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-159">High CPU-to-memory.</span></span> <span data-ttu-id="e4c89-160">트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="e4c89-161">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="e4c89-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="e4c89-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="e4c89-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="e4c89-163">메모리 대 코어 비율이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-163">High memory-to-core.</span></span> <span data-ttu-id="e4c89-164">관계형 데이터베이스, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="e4c89-165">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="e4c89-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="e4c89-166">Ls</span><span class="sxs-lookup"><span data-stu-id="e4c89-166">Ls</span></span>                | <span data-ttu-id="e4c89-167">높은 디스크 처리량 및 IO</span><span class="sxs-lookup"><span data-stu-id="e4c89-167">High disk throughput and IO.</span></span> <span data-ttu-id="e4c89-168">빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="e4c89-169">GPU</span><span class="sxs-lookup"><span data-stu-id="e4c89-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="e4c89-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="e4c89-170">NV, NC</span></span>            | <span data-ttu-id="e4c89-171">대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="e4c89-172">고성능</span><span class="sxs-lookup"><span data-stu-id="e4c89-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e4c89-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="e4c89-173">H, A8-11</span></span>          | <span data-ttu-id="e4c89-174">당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="e4c89-175">사용 가능한 VM 크기 찾기</span><span class="sxs-lookup"><span data-stu-id="e4c89-175">Find available VM sizes</span></span>

<span data-ttu-id="e4c89-176">특정 지역에 toosee VM 목록을 사용할 수 있는 크기, hello를 사용 하 여 [az vm 목록 크기](/cli/azure/vm#list-sizes) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="e4c89-177">부분 출력:</span><span class="sxs-lookup"><span data-stu-id="e4c89-177">Partial output:</span></span>

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

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="e4c89-178">특정 크기로 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e4c89-178">Create VM with specific size</span></span>

<span data-ttu-id="e4c89-179">앞의 예에서 hello VM 만들기, 크기를 제공 하지 않았습니다, 결과적 기본 크기.</span><span class="sxs-lookup"><span data-stu-id="e4c89-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="e4c89-180">VM 크기를 사용 하 여 만들 때 선택할 수 있습니다 [az vm 만들기](/cli/azure/vm#create) 및 hello `--size` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="e4c89-181">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e4c89-181">Resize a VM</span></span>

<span data-ttu-id="e4c89-182">VM을 배포한 후 크기가 조정 된 tooincrease 하거나 이동할 수 있습니다 리소스 할당을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="e4c89-183">VM의 크기를 조정 하기 전에 hello 원하는 크기는 hello 현재 Azure 클러스터에서 사용할 수 있는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="e4c89-184">hello [az vm 목록-vm-크기 조정-옵션](/cli/azure/vm#list-vm-resize-options) 명령 반환 hello 크기의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="e4c89-185">Hello 원하는 크기는 사용할 수 있는 경우 hello VM 크기를 조정할 수 전원이 켜진 상태에서 있지만 hello 작업 동안 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="e4c89-186">사용 하 여 hello [az vm 크기를 조정]( /cli/azure/vm#resize) 명령 tooperform hello 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="e4c89-187">Hello 크기를 원하는 경우에 없습니다 hello 현재 클러스터에 VM hello 요구 hello 크기 조정 작업 전에 할당 취소 toobe 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="e4c89-188">사용 하 여 hello [az vm 할당을 취소]( /cli/azure/vm#deallocate) toostop 명령 및 hello VM 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="e4c89-189">참고 때 hello VM의 전원이 켜져 다시, hello 임시 디스크의 모든 데이터가 제거 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="e4c89-190">hello 공용 IP 주소는 고정 IP 주소를 사용 하는 하지 않는 경우에 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="e4c89-191">할당이 취소 되 면 hello 크기 조정 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="e4c89-192">Hello, 크기 조정 hello VM을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="e4c89-193">VM 전원 상태</span><span class="sxs-lookup"><span data-stu-id="e4c89-193">VM power states</span></span>

<span data-ttu-id="e4c89-194">Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="e4c89-195">이 상태를 hello 하이퍼바이저의 hello 관점에서 hello hello VM의 현재 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="e4c89-196">전원 상태</span><span class="sxs-lookup"><span data-stu-id="e4c89-196">Power states</span></span>

| <span data-ttu-id="e4c89-197">전원 상태</span><span class="sxs-lookup"><span data-stu-id="e4c89-197">Power State</span></span> | <span data-ttu-id="e4c89-198">설명</span><span class="sxs-lookup"><span data-stu-id="e4c89-198">Description</span></span>
|----|----|
| <span data-ttu-id="e4c89-199">시작 중</span><span class="sxs-lookup"><span data-stu-id="e4c89-199">Starting</span></span> | <span data-ttu-id="e4c89-200">Hello 가상 컴퓨터가 시작 되 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="e4c89-201">실행 중</span><span class="sxs-lookup"><span data-stu-id="e4c89-201">Running</span></span> | <span data-ttu-id="e4c89-202">Hello 가상 컴퓨터 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="e4c89-203">중지 중</span><span class="sxs-lookup"><span data-stu-id="e4c89-203">Stopping</span></span> | <span data-ttu-id="e4c89-204">Hello 가상 컴퓨터를 중지 하 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="e4c89-205">중지됨</span><span class="sxs-lookup"><span data-stu-id="e4c89-205">Stopped</span></span> | <span data-ttu-id="e4c89-206">Hello 가상 컴퓨터 중지 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="e4c89-207">Hello 중지 상태의 가상 컴퓨터 계산 비용이 계속 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="e4c89-208">할당 취소 중</span><span class="sxs-lookup"><span data-stu-id="e4c89-208">Deallocating</span></span> | <span data-ttu-id="e4c89-209">Hello 가상 컴퓨터를 할당 취소 되 고이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="e4c89-210">할당 취소됨</span><span class="sxs-lookup"><span data-stu-id="e4c89-210">Deallocated</span></span> | <span data-ttu-id="e4c89-211">Hello 가상 컴퓨터는 hello 하이퍼바이저에서 제거 되지만 hello 제어 평면에서 여전히 사용할 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="e4c89-212">Hello 할당 취소 됨 상태에서에서 가상 컴퓨터 계산 비용이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="e4c89-213">Hello 가상 컴퓨터의 전원 상태 hello 알려진 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="e4c89-214">전원 상태 찾기</span><span class="sxs-lookup"><span data-stu-id="e4c89-214">Find power state</span></span>

<span data-ttu-id="e4c89-215">특정 VM 사용 하 여 hello의 tooretrieve hello 상태 [az vm 인스턴스 뷰 가져오기](/cli/azure/vm#get-instance-view) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="e4c89-216">있는지 toospecify 가상 컴퓨터 및 리소스 그룹에 대 한 올바른 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="e4c89-217">출력:</span><span class="sxs-lookup"><span data-stu-id="e4c89-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="e4c89-218">관리 작업</span><span class="sxs-lookup"><span data-stu-id="e4c89-218">Management tasks</span></span>

<span data-ttu-id="e4c89-219">Hello-주기 동안 가상 컴퓨터를 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="e4c89-220">또한 toocreate 스크립트 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="e4c89-221">Hello Azure CLI를 사용 하 여 여러 가지 일반적인 관리 작업 또는 실행할 수 있는 hello 명령줄에서 스크립트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="e4c89-222">IP 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="e4c89-222">Get IP address</span></span>

<span data-ttu-id="e4c89-223">이 명령은 가상 컴퓨터의 hello 개인 및 공용 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="e4c89-224">가상 컴퓨터 중지</span><span class="sxs-lookup"><span data-stu-id="e4c89-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="e4c89-225">가상 컴퓨터 시작</span><span class="sxs-lookup"><span data-stu-id="e4c89-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="e4c89-226">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="e4c89-226">Delete resource group</span></span>

<span data-ttu-id="e4c89-227">리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="e4c89-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4c89-228">Next steps</span></span>

<span data-ttu-id="e4c89-229">이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4c89-230">만들고 tooa VM 연결</span><span class="sxs-lookup"><span data-stu-id="e4c89-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e4c89-231">VM 이미지 선택 및 사용</span><span class="sxs-lookup"><span data-stu-id="e4c89-231">Select and use VM images</span></span>
> * <span data-ttu-id="e4c89-232">특정 VM 크기 보기 및 사용</span><span class="sxs-lookup"><span data-stu-id="e4c89-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e4c89-233">VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e4c89-233">Resize a VM</span></span>
> * <span data-ttu-id="e4c89-234">VM 상태 보기 및 이해</span><span class="sxs-lookup"><span data-stu-id="e4c89-234">View and understand VM state</span></span>

<span data-ttu-id="e4c89-235">VM 디스크에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4c89-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4c89-236">VM 디스크 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e4c89-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
