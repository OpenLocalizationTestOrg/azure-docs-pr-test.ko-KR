---
title: "Azure Resource Manager 템플릿 및 PowerShell을 사용하여 랩 자동 생성 또는 수정 | Microsoft Docs"
description: "Azure Resource Manager 템플릿 및 PowerShell을 사용하여 DevTest 랩에서 랩을 자동으로 생성 또는 수정하는 방법에 대해 배웁니다"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: cea4531175df2cc39790497dc049d27e23ffa0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="2c69b-103">Azure Resource Manager 템플릿 및 PowerShell을 사용하여 랩 자동 생성 또는 수정</span><span class="sxs-lookup"><span data-stu-id="2c69b-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="2c69b-104">DevTest Labs는 새 랩을 빠르게 자동 생성하거나 기존 랩을 수정한 다음 이러한 리소스를 배포하는 데 유용한 여러 Azure Resource Manager 템플릿 및 PowerShell 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="2c69b-105">이 문서는 이러한 템플릿과 스크립트를 사용하여 랩의 생성, 수정, 배포를 자동화하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="2c69b-106">이 문서는 PowerShell을 사용하여 DevTest Labs에서 몇 가지 일반적인 작업을 수행하는 방법에 대한 자세한 정보를 찾을 수 있는 위치를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="2c69b-107">1단계: 템플릿 및 스크립트 수집</span><span class="sxs-lookup"><span data-stu-id="2c69b-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="2c69b-108">공용 [Github 리포지토리](https://github.com/Azure/azure-devtestlab)에서 미리 만들어진 [Azure Resource Manager 템플릿](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) 및 [PowerShell 스크립트](https://github.com/Azure/azure-devtestlab/tree/master/Scripts)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="2c69b-109">그대로 사용하거나 요구 사항에 맞게 사용자 지정하고 [개인 Git 리포지토리](devtest-lab-add-artifact-repo.md)에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="2c69b-110">2단계: Azure Resource Manager 템플릿 수정</span><span class="sxs-lookup"><span data-stu-id="2c69b-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="2c69b-111">이전에 템플릿을 만든 적이 없는 경우 [첫 번째 Azure Resource Manager 템플릿 만들기](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)에 나온 단계를 수행하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="2c69b-112">또한 [Azure Resource Manager 템플릿 작성에 대한 모범 사례](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)에 안정적이고 사용하기 쉬운 Azure Resource Manager 템플릿을 만드는 데 도움이 되는 다양한 지침과 제안이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="2c69b-113">일반적으로 제공되는 접근 방식 또는 예제 중 하나의 변형을 사용하고 사용자 필요에 따라 템플릿을 수정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="2c69b-114">3단계: PowerShell로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="2c69b-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="2c69b-115">템플릿과 스크립트를 사용자 지정한 후 [Resource Manager 템플릿 및 Azure PowerShell로 리소스를 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)하는 데 필요한 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2c69b-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="2c69b-116">이 문서는 Azure Resource Manager 템플릿과 Azure PowerShell을 사용하여 Azure에 리소스를 배포하는 방법에 대한 일반 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="2c69b-117">PowerShell을 사용하여 DevTest 랩에서 수행할 수 있는 일반 작업</span><span class="sxs-lookup"><span data-stu-id="2c69b-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="2c69b-118">PowerShell을 사용하여 자동화할 수 있는 다양한 일반 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="2c69b-119">다음 섹션에서는 이러한 작업을 수행하는 데 필요한 단계에 대해 간단히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="2c69b-120">PowerShell을 사용하여 VHD 파일에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="2c69b-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="2c69b-121">PowerShell을 사용하여 랩의 저장소 계정에 VHD 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="2c69b-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="2c69b-122">PowerShell을 사용하여 랩에 외부 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="2c69b-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="2c69b-123">PowerShell을 사용하여 랩 사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="2c69b-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="2c69b-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c69b-124">Next steps</span></span>
* <span data-ttu-id="2c69b-125">사용자 지정한 템플릿 또는 스크립트를 저장할 수 있는 [개인 Git 리포지토리](devtest-lab-add-artifact-repo.md)를 만드는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="2c69b-126">[Azure 빠른 시작 템플릿 갤러리의 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates)(영문)을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="2c69b-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
