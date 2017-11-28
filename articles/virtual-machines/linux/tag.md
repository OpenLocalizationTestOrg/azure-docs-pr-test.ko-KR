---
title: "Azure Linux 가상 컴퓨터에 태그를 지정하는 방법 | Microsoft Docs"
description: "Resource Manager 배포 모델을 사용하여 만든 Azure Linux 가상 컴퓨터에 태그를 지정하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="fcbe2-103">Azure에서 Linux 가상 컴퓨터에 태그를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="fcbe2-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="fcbe2-104">이 문서에서는 리소스 관리자 배포 모델을 통해 Azure의 Linux 가상 컴퓨터에 태그를 지정하는 다양한 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="fcbe2-105">태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="fcbe2-106">Azure는 현재 리소스 및 리소스 그룹당 최대 15개의 태그를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="fcbe2-107">태그를 만들 때 리소스에 배치하거나 기존 리소스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="fcbe2-108">태그는 리소스 관리자 배포 모델을 통해 만든 리소스에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="fcbe2-109">Azure CLI를 사용하여 태그 지정</span><span class="sxs-lookup"><span data-stu-id="fcbe2-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="fcbe2-110">먼저 최신 [Azure CLI 2.0(미리 보기)](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="fcbe2-111">[Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fcbe2-112">다음 명령을 사용하여 태그를 비롯한 지정된 가상 컴퓨터의 모든 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="fcbe2-113">Azure CLI를 통해 새 VM 태그를 추가하려면 태그 매개 변수 **--set**과 함께 `azure vm update` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="fcbe2-114">`azure vm update` 명령에 **--remove** 매개 변수를 사용하여 태그를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="fcbe2-115">Azure CLI 및 포털을 통해 리소스에 태그를 적용했으므로 이제 사용량 세부 정보를 확인하여 청구 포털에서 태그를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="fcbe2-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fcbe2-116">Next steps</span></span>
* <span data-ttu-id="fcbe2-117">Azure 리소스에 태그를 지정하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요][Azure Resource Manager Overview] 및 [태그를 사용하여 Azure 리소스 구성][Using Tags to organize your Azure Resources]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="fcbe2-118">태그로 Azure 리소스의 사용을 관리하는 방법은 [Azure 청구서 이해][Understanding your Azure Bill] 및 [Microsoft Azure 리소스 소비에 대한 정보 얻기][Gain insights into your Microsoft Azure resource consumption]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcbe2-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
