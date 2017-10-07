---
title: "aaaView 가상 컴퓨터의 Azure 리소스 관리자 템플릿을 사용 하 고 | Microsoft Docs"
description: "어떻게 toouse hello 가상 컴퓨터 toocreate에서 Azure 리소스 관리자 템플릿을 다른 Vm에 알아봅니다"
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
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a><span data-ttu-id="69b7b-103">가상 컴퓨터의 Azure Resource Manager 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="69b7b-103">Use a virtual machine's Azure Resource Manager template</span></span>

<span data-ttu-id="69b7b-104">만들 때 가상 컴퓨터 (VM)에서 DevTest Labs hello를 통해 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040), hello VM을 저장 하기 전에 hello Azure 리소스 관리자 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-104">When you are creating a virtual machine (VM) in DevTest Labs through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view hello Azure Resource Manager template before you save hello VM.</span></span> <span data-ttu-id="69b7b-105">hello 템플릿을 사용할 수 있습니다 별로 toocreate로 더 랩 Vm을 동일한 설정을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-105">hello template can then be used as a basis toocreate more lab VMs with hello same settings.</span></span>

<span data-ttu-id="69b7b-106">이 문서에서 설명 하는 방식 및에 VM을 만들 때 리소스 관리자 템플릿을 tooview hello 하는 방법을 toodeploy 것의 나중에 tooautomate 만들 hello 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-106">This article describes how tooview hello Resource Manager template when creating a VM, and how toodeploy it later tooautomate creation of hello same VM.</span></span>

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a><span data-ttu-id="69b7b-107">다중 VM 및 단일 VM Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="69b7b-107">Multi-VM vs. single-VM Resource Manager templates</span></span>
<span data-ttu-id="69b7b-108">두 가지 toocreate Vm의 리소스 관리자 템플릿을 사용 하 여 DevTest Labs: hello Microsoft.DevTestLab/labs/virtualmachines 리소스를 프로 비전 하거나 hello Microsoft.Commpute/virtualmachines 리소스를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-108">There are two ways toocreate VMs in DevTest Labs using a Resource Manager template: provision hello Microsoft.DevTestLab/labs/virtualmachines resource or provision hello Microsoft.Commpute/virtualmachines resource.</span></span> <span data-ttu-id="69b7b-109">각 방법은 서로 다른 시나리오에서 사용되며, 필요한 사용 권한도 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-109">Each is used in different scenarios and require different permissions.</span></span>

- <span data-ttu-id="69b7b-110">(Hello 템플릿에서 hello "resource" 속성에서 선언 됨) 처럼 Microsoft.DevTestLab/labs/virtualmachines 리소스 종류를 사용 하는 리소스 관리자 템플릿을 개별 랩 Vm 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in hello “resource” property in hello template) can provision individual lab VMs.</span></span> <span data-ttu-id="69b7b-111">각 VM는 다음 hello DevTest Labs 가상 컴퓨터 목록에서 단일 항목으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-111">Each VM then shows up as a single item in hello DevTest Labs virtual machines list:</span></span>

   ![Hello DevTest Labs 가상 컴퓨터 목록에 있는 단일 항목으로 Vm의 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   <span data-ttu-id="69b7b-113">이 유형의 리소스 관리자 템플릿 hello Azure PowerShell 명령을 통해 프로 비전 할 수 **새로 AzureRmResourceGroupDeployment** 또는 hello Azure CLI 명령을 통해 **az 그룹 배포 만들기** .</span><span class="sxs-lookup"><span data-stu-id="69b7b-113">This type of Resource Manager template can be provisioned through hello Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through hello Azure CLI command **az group deployment create**.</span></span> <span data-ttu-id="69b7b-114">DevTest Labs 사용자 역할에 할당 된 사용자는 hello 배포를 수행할 수 없는 관리자 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform hello deployment.</span></span> 

- <span data-ttu-id="69b7b-115">Microsoft.Compute/virtualmachines 리소스 종류를 사용 하는 리소스 관리자 템플릿을 hello DevTest Labs 가상 컴퓨터 목록에는 단일 환경으로 여러 Vm을 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in hello DevTest Labs virtual machines list:</span></span>

   ![Hello DevTest Labs 가상 컴퓨터 목록에 있는 단일 항목으로 Vm의 목록](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   <span data-ttu-id="69b7b-117">동일한 환경을 함께 관리할 수는 hello 및 공유에서 Vm hello 같은 수명 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-117">VMs in hello same environment can be managed together and share hello same lifecycle.</span></span> <span data-ttu-id="69b7b-118">DevTest Labs 사용자 역할에 할당 된 사용자에는 hello 관리자가 구성한 hello 랩 방법으로 이러한 템플릿을 사용 하 여 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as hello administrator has configured hello lab that way.</span></span>

<span data-ttu-id="69b7b-119">이 문서의 나머지 부분에서는 hello Mirosoft.DevTestLab/labs/virtualmachines를 사용 하는 리소스 관리자 템플릿을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-119">hello remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span></span> <span data-ttu-id="69b7b-120">이러한 랩 관리자 tooautomate 랩 VM 만들기 (예를 들어 claimable Vm) 또는 골든 이미지를 생성 (예를 들어 이미지 팩터리)에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-120">These are used by lab admins tooautomate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span></span>

<span data-ttu-id="69b7b-121">[Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) 많은 지침과 제안 사항 toohelp 제공 신뢰할 수 있는 쉽고 toouse은 Azure 리소스 관리자 템플릿을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions toohelp you create Azure Resource Manager templates that are reliable and easy toouse.</span></span>

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a><span data-ttu-id="69b7b-122">가상 컴퓨터의 Resource Manager 템플릿 보기 및 저장</span><span class="sxs-lookup"><span data-stu-id="69b7b-122">View and save a virtual machine's Resource Manager template</span></span>
1. <span data-ttu-id="69b7b-123">Hello 단계에 따라 [랩에서 첫 번째 VM을 만들](devtest-lab-create-first-vm.md) toobegin 가상 컴퓨터를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-123">Follow hello steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) toobegin creating a virtual machine.</span></span>
1. <span data-ttu-id="69b7b-124">가상 컴퓨터에 대 한 hello 필요한 정보를 입력 하 고이 VM에 대해 원하는 모든 아티팩트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-124">Enter hello required information for your virtual machine and add any artifacts you want for this VM.</span></span>
1. <span data-ttu-id="69b7b-125">Hello 구성 설정 창의 hello 맨 아래에 선택 **보기 ARM 템플릿을**합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-125">At hello bottom of hello Configure settings window, choose **View ARM template**.</span></span>

   ![ARM 템플릿 보기 단추](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. <span data-ttu-id="69b7b-127">복사 하 고 hello 리소스 관리자 템플릿 toouse 저장 이후 toocreate 다른 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="69b7b-127">Copy and save hello Resource Manager template toouse later toocreate another virtual machine.</span></span>

   ![나중에 사용할 리소스 관리자 템플릿 toosave](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

<span data-ttu-id="69b7b-129">Hello 리소스 관리자 서식 파일을 저장 한 후 사용 하기 전에 hello 템플릿의 hello 매개 변수 섹션을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-129">After you have saved hello Resource Manager template, you must update hello parameters section of hello template before you can use it.</span></span> <span data-ttu-id="69b7b-130">방금 hello 매개 변수를 hello 실제 리소스 관리자 템플릿 외부에서 사용자 지정 하는 parameter.json를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-130">You can create a parameter.json that customizes just hello parameters, outside of hello actual Resource Manager template.</span></span> 

![JSON 파일을 사용하여 매개 변수 사용자 지정](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a><span data-ttu-id="69b7b-132">리소스 관리자 템플릿 toocreate VM 배포</span><span class="sxs-lookup"><span data-stu-id="69b7b-132">Deploy a Resource Manager template toocreate a VM</span></span>
<span data-ttu-id="69b7b-133">리소스 관리자 템플릿을 저장 하 고 요구에 맞게 사용자 지정한 후 tooautomate VM 만들기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-133">After you have saved a Resource Manager template and customized it for your needs, you can use it tooautomate VM creation.</span></span> <span data-ttu-id="69b7b-134">[리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) 설명 방식을 리소스 관리자 템플릿 toodeploy와 Azure PowerShell toouse 리소스 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-134">[Deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) describes how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="69b7b-135">[리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) 설명 방식을 리소스 관리자 템플릿 toodeploy와 Azure CLI toouse 리소스 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-135">[Deploy resources with Resource Manager templates and Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) describes how toouse Azure CLI with Resource Manager templates toodeploy your resources tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="69b7b-136">랩 소유자 권한을 가진 사용자만 Azure PowerShell을 사용하여 Resource Manager 템플릿에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-136">Only a user with lab owner permissions can create VMs from a Resource Manager template by using Azure PowerShell.</span></span> <span data-ttu-id="69b7b-137">리소스 관리자 템플릿을 사용 하 여 tooautomate VM 만들기 및 사용자 권한을 하기만 하면, hello를 사용할 수 있습니다 [ **az 랩 vm 만들기** hello CLI 명령을](https://docs.microsoft.com/cli/azure/lab/vm#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-137">If you want tooautomate VM creation using a Resource Manager template and you only have user permissions, you can use hello [**az lab vm create** command in hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>

### <a name="next-steps"></a><span data-ttu-id="69b7b-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69b7b-138">Next steps</span></span>
* <span data-ttu-id="69b7b-139">너무 방법에 대해 알아봅니다[리소스 관리자 템플릿을 다중 VM 환경을 만들](devtest-lab-create-environment-from-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-139">Learn how too[Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* <span data-ttu-id="69b7b-140">Hello에서 DevTest Labs 자동화에 대 한 더 많은 빠른 시작 리소스 관리자 템플릿 탐색 [공용 DevTest Labs GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="69b7b-140">Explore more quick-start Resource Manager templates for DevTest Labs automation from hello [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
