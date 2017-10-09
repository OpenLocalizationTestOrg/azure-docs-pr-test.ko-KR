---
title: "Azure에서 Linux 가상 컴퓨터를 관리 되지 않는 aaaConvert toomanaged 디스크-Azure 관리 되는 디스크 디스크 | Microsoft Docs"
description: "Linux VM에서 관리 되지 않는 디스크 toomanaged tooconvert hello 리소스 관리자 배포 모델에서 Azure CLI 2.0을 사용 하 여 디스크 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="83c6f-103">관리 되지 않는 디스크 toomanaged 디스크에서 Linux 가상 컴퓨터 변환</span><span class="sxs-lookup"><span data-stu-id="83c6f-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="83c6f-104">기존 Linux 가상 컴퓨터 (Vm) 관리 되지 않는 디스크를 사용 하는 경우 hello 통해 hello Vm toouse 관리 되는 디스크를 변환할 수 있습니다 [Azure 관리 되는 디스크](../windows/managed-disks-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="83c6f-105">이 프로세스는 hello OS 디스크 및 연결 된 데이터 디스크를 모두 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="83c6f-106">이 문서를 사용 하 여 Vm tooconvert Azure CLI hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="83c6f-107">Tooinstall 필요 하거나 업그레이드할 참조 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="83c6f-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="83c6f-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="83c6f-109">단일 인스턴스 VM 변환</span><span class="sxs-lookup"><span data-stu-id="83c6f-109">Convert single-instance VMs</span></span>
<span data-ttu-id="83c6f-110">이 섹션에서는 tooconvert 단일 인스턴스 Azure Vm에서 관리 되지 않는 toomanaged 디스크 디스크 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="83c6f-111">(Vm 가용성 집합에 있는 경우 hello 다음 섹션 참조 합니다.) 이 프로세스 tooconvert hello Vm (HDD) 표준 또는 프리미엄 (SSD) 관리 되지 않는 디스크 toopremium 관리 되는 디스크에서 관리 되지 않는 디스크 toostandard 관리 되는 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="83c6f-112">VM hello를 사용 하 여 할당 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="83c6f-113">hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="83c6f-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="83c6f-114">사용 하 여 hello VM toomanaged 디스크 변환 [az vm 변환](/cli/azure/vm#convert)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="83c6f-115">변환 프로세스를 수행 하는 hello hello 라는 VM `myVM`hello OS 디스크 및 모든 데이터 디스크를 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="83c6f-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="83c6f-116">사용 하 여 hello 변환 toomanaged 디스크 후 hello VM 시작 [az vm 시작](/cli/azure/vm#start)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="83c6f-117">다음 예에서는 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="83c6f-118">가용성 집합의 VM 변환</span><span class="sxs-lookup"><span data-stu-id="83c6f-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="83c6f-119">경우 tooconvert toomanaged 디스크 가용성 집합에는 원하는 hello Vm을 먼저 tooconvert hello 가용성 집합 tooa 관리 되는 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="83c6f-120">Hello 가용성 집합을 변환 하기 전에 hello 가용성 집합에 있는 모든 Vm은 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="83c6f-121">모든 Vm toomanaged 디스크 hello 공급 후 자체적으로 설정 하는 계획 tooconvert 가용성 집합 관리 되는 변환 된 tooa 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="83c6f-122">그런 다음, 모든 hello Vm을 시작 하 고 계속 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="83c6f-123">[az vm availability-set list](/cli/azure/vm/availability-set#list)를 사용하여 가용성 집합의 모든 VM을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="83c6f-124">hello 다음 예에서는 나열 모든 Vm hello 가용성 명명 된 집합의 `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="83c6f-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="83c6f-125">사용 하 여 모든 hello Vm 할당을 취소 [az vm 할당을 취소](/cli/azure/vm#deallocate)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="83c6f-126">hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="83c6f-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="83c6f-127">사용 하 여 설정 하는 hello 가용성 변환 [az vm 가용성 집합 convert](/cli/azure/vm/availability-set#convert)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="83c6f-128">hello 다음 예제에서는 변환 hello 가용성 명명 된 집합 `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="83c6f-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="83c6f-129">사용 하 여 모든 hello Vm toomanaged 디스크 변환 [az vm 변환](/cli/azure/vm#convert)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="83c6f-130">변환 프로세스를 수행 하는 hello hello 라는 VM `myVM`hello OS 디스크 및 모든 데이터 디스크를 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="83c6f-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="83c6f-131">사용 하 여 hello 변환 toomanaged 디스크 후 모든 hello Vm 시작 [az vm 시작](/cli/azure/vm#start)합니다.</span><span class="sxs-lookup"><span data-stu-id="83c6f-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="83c6f-132">다음 예에서는 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="83c6f-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="83c6f-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83c6f-133">Next steps</span></span>
<span data-ttu-id="83c6f-134">저장소 옵션에 대한 자세한 내용은 [Azure Managed Disks 개요](../windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83c6f-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
