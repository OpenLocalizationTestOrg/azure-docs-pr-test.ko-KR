---
title: "가상 컴퓨터의 Azure Resource Manager 템플릿 보기 및 사용 | Microsoft Docs"
description: "가상 컴퓨터에서 Azure Resource Manager 템플릿을 사용하여 다른 VM을 만드는 방법을 알아봅니다."
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: 12cdb61667f77215c894800d5c439235e767a26b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a><span data-ttu-id="c94c3-103">가상 컴퓨터의 Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="c94c3-103">Use a virtual machine's Azure Resource Manager template</span></span>

<span data-ttu-id="c94c3-104">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)을 통해 DevTest Labs에서 VM(가상 컴퓨터)을 만드는 경우 VM을 저장하기 전에 Azure Resource Manager 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-104">When you are creating a virtual machine (VM) in DevTest Labs through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view the Azure Resource Manager template before you save the VM.</span></span> <span data-ttu-id="c94c3-105">그런 다음 템플릿을 기초로 사용해서 동일한 설정으로 더 많은 랩 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-105">The template can then be used as a basis to create more lab VMs with the same settings.</span></span>

<span data-ttu-id="c94c3-106">이 문서에서는 VM을 만들 때 Resource Manager 템플릿을 보는 방법 및 나중에 템플릿을 배포하여 동일한 VM의 생성을 자동화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-106">This article describes how to view the Resource Manager template when creating a VM, and how to deploy it later to automate creation of the same VM.</span></span>

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a><span data-ttu-id="c94c3-107">다중 VM 및 단일 VM Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c94c3-107">Multi-VM vs. single-VM Resource Manager templates</span></span>
<span data-ttu-id="c94c3-108">Resource Manager 템플릿을 사용하여 DevTest Labs에서 VM을 만드는 두 가지 방법은 Microsoft.DevTestLab/labs/virtualmachines 리소스를 프로비전하거나 Microsoft.Commpute/virtualmachines 리소스를 프로비전하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-108">There are two ways to create VMs in DevTest Labs using a Resource Manager template: provision the Microsoft.DevTestLab/labs/virtualmachines resource or provision the Microsoft.Commpute/virtualmachines resource.</span></span> <span data-ttu-id="c94c3-109">각 방법은 서로 다른 시나리오에서 사용되며, 필요한 사용 권한도 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-109">Each is used in different scenarios and require different permissions.</span></span>

- <span data-ttu-id="c94c3-110">Microsoft.DevTestLab/labs/virtualmachines 리소스 종류(템플릿의 “resource” 속성에 선언됨)를 사용하는 Resource Manager 템플릿은 개별 랩 VM을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in the “resource” property in the template) can provision individual lab VMs.</span></span> <span data-ttu-id="c94c3-111">그러면 각 VM이 DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-111">Each VM then shows up as a single item in the DevTest Labs virtual machines list:</span></span>

   ![DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시되는 VM 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   <span data-ttu-id="c94c3-113">이 형식의 Resource Manager 템플릿은 Azure PowerShell 명령 **New-AzureRmResourceGroupDeployment** 또는 Azure CLI 명령 **az group deployment create**를 통해 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-113">This type of Resource Manager template can be provisioned through the Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through the Azure CLI command **az group deployment create**.</span></span> <span data-ttu-id="c94c3-114">관리자 권한이 필요하므로 DevTest Labs 사용자 역할이 할당된 사용자는 배포를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform the deployment.</span></span> 

- <span data-ttu-id="c94c3-115">Microsoft.Compute/virtualmachines 리소스 종류를 사용하는 Resource Manager 템플릿은 여러 VM을 DevTest Labs 가상 컴퓨터 목록의 단일 환경으로 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in the DevTest Labs virtual machines list:</span></span>

   ![DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 표시되는 VM 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   <span data-ttu-id="c94c3-117">동일한 환경의 VM은 함께 관리할 수 있으며, 동일한 수명 주기를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-117">VMs in the same environment can be managed together and share the same lifecycle.</span></span> <span data-ttu-id="c94c3-118">DevTest Labs 사용자 역할이 할당된 사용자는 이러한 템플릿을 사용하여 환경을 만들 수 있지만 관리자가 해당 방식으로 랩을 구성한 경우에만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as the administrator has configured the lab that way.</span></span>

<span data-ttu-id="c94c3-119">이 문서의 나머지 부분에서는 Mirosoft.DevTestLab/labs/virtualmachines를 사용하는 Resource Manager 템플릿에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-119">The remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span></span> <span data-ttu-id="c94c3-120">이러한 템플릿은 랩 관리자가 랩 VM 생성(예: 클레임 가능한 VM) 또는 골든 이미지 생성(예: 이미지 팩터리)을 자동화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-120">These are used by lab admins to automate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span></span>

<span data-ttu-id="c94c3-121">[Azure Resource Manager 템플릿 작성에 대한 모범 사례](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)에 안정적이고 사용하기 쉬운 Azure Resource Manager 템플릿을 만드는 데 도움이 되는 다양한 지침과 제안이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span>

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a><span data-ttu-id="c94c3-122">가상 컴퓨터의 Resource Manager 템플릿 보기 및 저장</span><span class="sxs-lookup"><span data-stu-id="c94c3-122">View and save a virtual machine's Resource Manager template</span></span>
1. <span data-ttu-id="c94c3-123">[랩에서 첫 번째 VM 만들기](devtest-lab-create-first-vm.md)의 단계에 따라 가상 컴퓨터 생성을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-123">Follow the steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) to begin creating a virtual machine.</span></span>
1. <span data-ttu-id="c94c3-124">가상 컴퓨터에 대한 필요한 정보를 입력하고 이 VM에 사용하려는 아티팩트를 모두 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-124">Enter the required information for your virtual machine and add any artifacts you want for this VM.</span></span>
1. <span data-ttu-id="c94c3-125">설정 구성 창의 맨 아래에서 **ARM 템플릿 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-125">At the bottom of the Configure settings window, choose **View ARM template**.</span></span>

   ![ARM 템플릿 보기 단추](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. <span data-ttu-id="c94c3-127">나중에 다른 가상 컴퓨터를 만드는 데 사용할 Resource Manager 템플릿을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-127">Copy and save the Resource Manager template to use later to create another virtual machine.</span></span>

   ![나중에 사용하기 위해 저장할 Resource Manager 템플릿](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

<span data-ttu-id="c94c3-129">Resource Manager 템플릿을 저장한 후 먼저 템플릿의 매개 변수 섹션을 업데이트해야 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-129">After you have saved the Resource Manager template, you must update the parameters section of the template before you can use it.</span></span> <span data-ttu-id="c94c3-130">실제 Resource Manager 템플릿 외부에서 매개 변수만 사용자 지정하는 parameter.json을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-130">You can create a parameter.json that customizes just the parameters, outside of the actual Resource Manager template.</span></span> 

![JSON 파일을 사용하여 매개 변수 사용자 지정](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-to-create-a-vm"></a><span data-ttu-id="c94c3-132">Resource Manager 템플릿을 배포하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="c94c3-132">Deploy a Resource Manager template to create a VM</span></span>
<span data-ttu-id="c94c3-133">Resource Manager 템플릿을 저장하고 요구에 맞게 사용자 지정한 후 이 템플릿을 사용하여 VM 생성을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-133">After you have saved a Resource Manager template and customized it for your needs, you can use it to automate VM creation.</span></span> <span data-ttu-id="c94c3-134">[Resource Manager 템플릿 및 Azure PowerShell을 사용하여 리소스 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)에서는 Resource Manager 템플릿과 함께 Azure PowerShell을 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-134">[Deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) describes how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="c94c3-135">[Resource Manager 템플릿 및 Azure CLI를 사용하여 리소스 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)에서는 Resource Manager 템플릿과 함께 Azure CLI를 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-135">[Deploy resources with Resource Manager templates and Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) describes how to use Azure CLI with Resource Manager templates to deploy your resources to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="c94c3-136">랩 소유자 권한을 가진 사용자만 Azure PowerShell을 사용하여 Resource Manager 템플릿에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-136">Only a user with lab owner permissions can create VMs from a Resource Manager template by using Azure PowerShell.</span></span> <span data-ttu-id="c94c3-137">Resource Manager 템플릿을 사용하여 VM 생성을 자동화하려고 하는데 사용자 권한만 있는 경우 [CLI의 **az lab vm create** 명령](https://docs.microsoft.com/cli/azure/lab/vm#create)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-137">If you want to automate VM creation using a Resource Manager template and you only have user permissions, you can use the [**az lab vm create** command in the CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>

### <a name="next-steps"></a><span data-ttu-id="c94c3-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c94c3-138">Next steps</span></span>
* <span data-ttu-id="c94c3-139">[Resource Manager 템플릿으로 다중 VM 환경을 만드는](devtest-lab-create-environment-from-arm.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-139">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* <span data-ttu-id="c94c3-140">[공용 DevTest Labs GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)에서 DevTest Labs 자동화를 위한 기타 빠른 시작 Resource Manager 템플릿을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c94c3-140">Explore more quick-start Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
