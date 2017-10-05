---
title: "관리 디스크를 Azure 가상 컴퓨터 확장 집합과 함께 사용 | Microsoft Docs"
description: "관리 디스크를 가상 컴퓨터 확장 집합과 함께 사용하는 이유 및 방법 알아보기"
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
ms.openlocfilehash: 3ab1d432a2f90db57b99f0e7d419d85e2958c308
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="d97b3-103">Azure VM 확장 집합 및 관리 디스크</span><span class="sxs-lookup"><span data-stu-id="d97b3-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="d97b3-104">Azure [가상 컴퓨터 확장 집합](/azure/virtual-machine-scale-sets/)에서는 관리 디스크가 있는 가상 컴퓨터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="d97b3-105">확장 집합이 있는 관리 디스크를 사용하면 다음과 같은 여러 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="d97b3-106">확장 집합 VM에 대한 OS 디스크를 저장하기 위해 더 이상 저장소 계정을 미리 만들어서 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span></span>

* <span data-ttu-id="d97b3-107">확장 집합에 관리 데이터 디스크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-107">You can attach managed data disks to the scale set.</span></span>

* <span data-ttu-id="d97b3-108">관리 디스크를 사용하면 확장 집합이 플랫폼 이미지 기반인 경우 VM 1,000대, 사용자 지정 이미지 기반인 경우 VM 100대의 용량을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="d97b3-109">시작</span><span class="sxs-lookup"><span data-stu-id="d97b3-109">Get started</span></span>

<span data-ttu-id="d97b3-110">관리 디스크 확장 집합을 시작하는 간단한 방법은 Azure Portal에서 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span></span> <span data-ttu-id="d97b3-111">자세한 내용은 [이 문서](./virtual-machine-scale-sets-portal-create.md)(영문)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="d97b3-112">또 다른 간단한 방법은 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)을 사용하여 확장 집합을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span></span> <span data-ttu-id="d97b3-113">다음 예에서는 VM이 10대이고 각 VM에 50GB 및 100GB 데이터 디스크가 포함된 Ubuntu 기반 확장 집합을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="d97b3-114">또는 `vmss`가 포함된 폴더에 대한 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)에서 확장 집합을 배포하는 미리 작성된 템플릿 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="d97b3-115">이미 관리 디스크를 사용하는 템플릿을 알아보려면 [이 목록](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d97b3-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d97b3-116">Next steps</span></span>

<span data-ttu-id="d97b3-117">일반적인 관리 디스크에 대한 자세한 내용은 [이 문서](../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="d97b3-118">Resource Manager 템플릿을 변환하여 확장 집합에 관리 디스크를 프로비전하는 방법은 [이 문서](./virtual-machine-scale-sets-convert-template-to-md.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-118">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="d97b3-119">Resource Manager 템플릿의 수정 사항은 Azure REST API에도 똑같이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d97b3-119">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span></span>

<span data-ttu-id="d97b3-120">관리 디스크를 확장 집합과 함께 사용하는 자세한 방법은 [이 문서](./virtual-machine-scale-sets-attached-disks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-120">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="d97b3-121">대규모 확장 집합을 시작하려면 [이 문서](./virtual-machine-scale-sets-placement-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d97b3-121">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


