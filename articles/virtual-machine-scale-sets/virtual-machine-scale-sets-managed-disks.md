---
title: "aaaUsing 관리 되는 디스크와 Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "관리 되는 디스크를 가상 컴퓨터 크기 집합 toouse 근거, 방법에 대해 알아봅니다"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="d2e63-103">Azure VM 확장 집합 및 관리 디스크</span><span class="sxs-lookup"><span data-stu-id="d2e63-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="d2e63-104">Azure [가상 컴퓨터 확장 집합](/azure/virtual-machine-scale-sets/)에서는 관리 디스크가 있는 가상 컴퓨터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="d2e63-105">확장 집합이 있는 관리 디스크를 사용하면 다음과 같은 여러 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="d2e63-106">Toopre 더 이상 필요-만들고 hello 크기 집합 Vm에 대 한 저장소 계정을 toostore hello OS 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="d2e63-107">관리 되는 데이터 디스크 toohello 크기 집합을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="d2e63-108">관리 디스크를 사용하면 확장 집합이 플랫폼 이미지 기반인 경우 VM 1,000대, 사용자 지정 이미지 기반인 경우 VM 100대의 용량을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="d2e63-109">시작</span><span class="sxs-lookup"><span data-stu-id="d2e63-109">Get started</span></span>

<span data-ttu-id="d2e63-110">간단한 방법을 관리 되는 디스크 크기 집합 시작 tooget는 hello Azure 포털에서에서 toodeploy 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="d2e63-111">자세한 내용은 [이 문서](./virtual-machine-scale-sets-portal-create.md)(영문)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="d2e63-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="d2e63-112">또 다른 간단한 방법은 tooget 시작은 toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy 소수 자릿수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="d2e63-113">hello 다음 보여 주는 예제는 Ubuntu toocreate 된 50GB 및 100GB 데이터 디스크를 각각 10 개의 Vm 크기 집합을 따라 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="d2e63-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="d2e63-114">Hello에 표시 될 수 있습니다 또는 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) 포함 하는 폴더에 대 한 `vmss` toosee 미리 만들어진 크기 집합을 배포 하는 템플릿의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="d2e63-115">서식 파일에서 관리 하는 디스크를 이미 사용 중인 tootell를 참조할 수 있습니다 너무[이 목록](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2e63-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2e63-116">Next steps</span></span>

<span data-ttu-id="d2e63-117">일반적인 관리 디스크에 대한 자세한 내용은 [이 문서](../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2e63-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="d2e63-118">toosee tooconvert 사용 하 여 리소스 관리자 템플릿 tooprovision 눈금 집합에 디스크를 관리 하는 방법은 참조 [이 여기서](./virtual-machine-scale-sets-convert-template-to-md.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="d2e63-119">hello 동일한 수정 toohello 리소스 관리자 템플릿 적용 toohello Azure REST API도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="d2e63-120">관리 되는 데이터 디스크를 사용 하 여 눈금 집합에 대해 자세히 toolearn 참조 [이 여기서](./virtual-machine-scale-sets-attached-disks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="d2e63-121">규모가 큰 집합으로 작업할 toobegin 너무 참조[이 여기서](./virtual-machine-scale-sets-placement-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e63-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


