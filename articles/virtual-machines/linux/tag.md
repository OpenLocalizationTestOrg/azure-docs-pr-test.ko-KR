---
title: "aaaHow tootag Azure Linux 가상 컴퓨터 | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Azure Linux 가상 컴퓨터는 태그를 지정 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="b7169-103">어떻게 tootag Azure에서 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="b7169-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="b7169-104">이 문서에서는 다양 한 방법 tootag hello 리소스 관리자 배포 모델을 통해 Azure에서 Linux 가상 컴퓨터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="b7169-105">태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="b7169-106">현재 azure 리소스 및 리소스 그룹 당 too15 태그를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="b7169-107">태그 생성 hello 시 리소스에 배치 될 수 있습니다 또는 tooan 기존 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="b7169-108">하십시오 note, hello 리소스 관리자 배포 모델만을 통해 생성 된 리소스에 대 한 태그는 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="b7169-109">Azure CLI를 사용하여 태그 지정</span><span class="sxs-lookup"><span data-stu-id="b7169-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="b7169-110">toobegin, 필요한 hello 최신 [Azure CLI 2.0 (미리 보기)](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b7169-111">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b7169-112">Hello 태그를 포함 하 여,이 명령을 사용 하 여 지정 된 가상 컴퓨터에 대 한 모든 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="b7169-113">hello Azure CLI를 통해 새 VM 태그 tooadd hello를 사용할 수 있습니다 `azure vm update` hello 태그 매개 변수와 함께 명령 **-설정**:</span><span class="sxs-lookup"><span data-stu-id="b7169-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="b7169-114">tooremove 태그 hello를 사용할 수 있습니다 **-제거** hello에 대 한 매개 변수 `azure vm update` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="b7169-115">태그 tooour 리소스 Azure CLI 적용 하 고 포털 hello, 살펴보겠습니다는 hello 사용량 세부 정보 toosee hello 태그 hello 청구 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b7169-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="b7169-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7169-116">Next steps</span></span>
* <span data-ttu-id="b7169-117">Azure 리소스 태그에 대 한 자세한 toolearn 참조 [Azure 리소스 관리자 개요] [ Azure Resource Manager Overview] 및 [tooorganize 태그를 사용 하 여 Azure 리소스] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="b7169-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="b7169-118">toosee 태그 수 Azure 리소스의 사용을 관리 하는 방법 참조 [Azure 청구서 이해] [ Understanding your Azure Bill] 및 [Microsoft Azure 리소스 소비량에 대 한 이해력] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="b7169-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
