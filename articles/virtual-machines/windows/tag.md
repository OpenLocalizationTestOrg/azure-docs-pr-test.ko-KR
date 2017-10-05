---
title: "Azure에서 Windows VM 리소스에 태그 지정 | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 Azure에서 만든 Windows 가상 컴퓨터에 태그를 지정하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 5f00c4265cea3db02dbb09a7f81be636a3fdd3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="97ff3-103">Azure에서 Windows 가상 컴퓨터에 태그를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="97ff3-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="97ff3-104">이 문서에서는 리소스 관리자 배포 모델을 통해 Azure의 Windows 가상 컴퓨터에 태그를 지정하는 다양한 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="97ff3-105">태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="97ff3-106">Azure는 현재 리소스 및 리소스 그룹당 최대 15개의 태그를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="97ff3-107">태그를 만들 때 리소스에 배치하거나 기존 리소스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="97ff3-108">태그는 리소스 관리자 배포 모델을 통해 만든 리소스에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="97ff3-109">Linux 가상 컴퓨터에 태그를 지정하려는 경우 [Azure에서 Linux 가상 컴퓨터에 태그를 지정하는 방법](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97ff3-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="97ff3-110">PowerShell을 사용한 태그 지정</span><span class="sxs-lookup"><span data-stu-id="97ff3-110">Tagging with PowerShell</span></span>
<span data-ttu-id="97ff3-111">PowerShell을 통해 태그를 만들고 추가 및 삭제하려면 먼저 [Azure Resource Manager를 사용하여 PowerShell 환경][PowerShell environment with Azure Resource Manager]을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="97ff3-112">설정을 완료한 후 계산, 네트워크 및 저장소 리소스를 만들 때 또는 PowerShell을 통해 리소스를 만든 후에 태그를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="97ff3-113">이 문서에서는 가상 컴퓨터에 배치된 태그 보기/편집을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="97ff3-114">먼저 `Get-AzureRmVM` cmdlet을 통해 가상 컴퓨터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="97ff3-115">가상 컴퓨터에 이미 태그가 포함되어 있는 경우 해당 리소스의 모든 태그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="97ff3-116">PowerShell을 통해 태그를 추가하려는 경우 `Set-AzureRmResource` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="97ff3-117">PowerShell을 통해 태그를 업데이트하는 경우 태그가 전체적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="97ff3-118">따라서 이미 태그가 있는 리소스에 하나의 태그를 추가하는 경우 리소스에 배치하려는 모든 태그를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="97ff3-119">다음은 PowerShell Cmdlet을 통해 리소스에 태그를 더 추가하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="97ff3-120">첫 번째 cmdlet은 `Get-AzureRmResource` 및 `Tags` 속성을 사용하여 *MyTestVM*에 배치된 모든 태그를 *$tags* 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="97ff3-121">두 번째 명령은 지정된 변수에 대한 태그를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="97ff3-122">세 번째 명령은 *$tags* 변수에 태그를 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="97ff3-123">**+=** 을 사용하여 *$tags* 목록에 새로운 키/값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="97ff3-124">네 번째 명령은 *$tags* 변수에 정의된 모든 태그를 지정된 리소스로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="97ff3-125">이 경우 MyTestVM입니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="97ff3-126">다섯 번째 명령은 리소스의 모든 태그를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="97ff3-127">여기서 볼 수 있듯이 *위치*가 이제 값이 *MyLocation*인 태그로 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97ff3-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="97ff3-128">PowerShell을 통해 태그를 지정하는 방법에 대한 자세한 내용은 [Azure 리소스 Cmdlet][Azure Resource Cmdlets]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97ff3-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="97ff3-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97ff3-129">Next steps</span></span>
* <span data-ttu-id="97ff3-130">Azure 리소스에 태그를 지정하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요][Azure Resource Manager Overview] 및 [태그를 사용하여 Azure 리소스 구성][Using Tags to organize your Azure Resources]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97ff3-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="97ff3-131">태그로 Azure 리소스의 사용을 관리하는 방법은 [Azure 청구서 이해][Understanding your Azure Bill] 및 [Microsoft Azure 리소스 소비에 대한 정보 얻기][Gain insights into your Microsoft Azure resource consumption]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97ff3-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
