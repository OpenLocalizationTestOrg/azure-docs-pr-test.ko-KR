---
title: "aaaHow tooresize hello Azure CLI 1.0을 사용 하 여 Linux VM | Microsoft Docs"
description: "어떻게를 tooscale 또는 비율을 변경 하 여 Linux 가상 컴퓨터를 hello VM 크기입니다."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="978af-103">Azure CLI 1.0을 사용하여 Linux VM의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="978af-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="978af-104">개요</span><span class="sxs-lookup"><span data-stu-id="978af-104">Overview</span></span>

<span data-ttu-id="978af-105">가상 컴퓨터 (VM)를 프로 비전 한 후 확장할 수 있습니다 hello VM 위로 또는 아래로 hello를 변경 하 여 [VM 크기][vm-sizes]합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="978af-106">경우에 따라 할당을 취소 해야 hello VM 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="978af-107">이 새 크기 hello hello VM을 호스팅하는 hello 하드웨어 클러스터에 사용할 수 없는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978af-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="978af-108">이 문서에서는 어떻게 hello를 사용 하 여 Linux VM a tooresize [Azure CLI][azure-cli]합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="978af-109">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="978af-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="978af-110">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978af-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="978af-111">[Azure CLI 1.0](#resize-a-linux-vm) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="978af-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="978af-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="978af-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="978af-113">Linux VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="978af-113">Resize a Linux VM</span></span>
<span data-ttu-id="978af-114">VM을 tooresize hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="978af-115">Hello 다음 CLI 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-115">Run hello following CLI command.</span></span> <span data-ttu-id="978af-116">이 명령은 hello VM 호스팅되는 hello 하드웨어 클러스터에서 사용할 수 있는 hello VM 크기를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="978af-117">Hello 원하는 크기 나열 된 경우 다음 명령을 tooresize hello VM hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="978af-118">이 프로세스 동안 hello VM 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="978af-118">hello VM will restart during this process.</span></span> <span data-ttu-id="978af-119">Hello 다시 시작한 후 기존 OS 및 데이터 디스크 다시 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="978af-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="978af-120">Hello 임시 디스크에 있는 모든 내용을 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="978af-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="978af-121">사용 하 여 hello `--enable-boot-diagnostics` 옵션을 사용 하면 [진단 부팅][boot-diagnostics], toolog 모든 오류 관련된 toostartup 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="978af-122">그렇지 않으면 hello 크기 나열 되지 않으면 원하는 경우 hello 다음 명령을 toodeallocate hello VM 크기를 변경 하 고 hello VM을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="978af-123">또한 할당 해제 hello VM toohello VM을 할당 하는 동적 IP 주소를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="978af-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="978af-124">hello OS 및 데이터 디스크 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="978af-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="978af-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="978af-125">Next steps</span></span>
<span data-ttu-id="978af-126">확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다. 자세한 내용은 [가상 컴퓨터 확장 집합에서 Linux 컴퓨터 자동 확장][scale-set]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978af-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
