---
title: "Visual Studio를 사용하여 가상 컴퓨터 확장 집합 배포 | Microsoft Docs"
description: "Visual Studio 및 Resource Manager 템플릿을 사용하여 가상 컴퓨터 확장 집합 배포 | Microsoft Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="790f3-103">Visual Studio에서 가상 컴퓨터 확장 집합을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="790f3-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="790f3-104">이 문서는 Visual Studio 리소스 그룹 배포를 사용하여 Azure 가상 컴퓨터 규모 집합을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="790f3-105">[Azure 가상 컴퓨터 확장 집합](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/)은 자동 크기 조정 및 부하 분산을 사용하여 유사한 가상 컴퓨터 컬렉션을 배포하고 관리하기 위한 Azure 계산 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="790f3-106">[Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates)을 사용하여 가상 컴퓨터 확장 집합을 프로비전하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="790f3-107">Azure Resource Manager 템플릿은 Azure CLI, PowerShell, REST를 사용하여 배포가 가능하고 Visual Studio에서 직접 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="790f3-108">Visual Studio는 Azure 리소스 그룹 배포 프로젝트의 일부로 배포될 수 있는 예제 템플릿 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="790f3-109">Azure 리소스 그룹 배포는 단일 배포 작업을 통해 관련된 Azure 리소스 집합을 그룹화하여 게시하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="790f3-110">자세한 내용은 [Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="790f3-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="790f3-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="790f3-111">Pre-requisites</span></span>
<span data-ttu-id="790f3-112">Visual Studio에서 가상 컴퓨터 확장 집합 배포를 시작하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="790f3-113">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="790f3-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="790f3-114">Azure SDK 2.7, 2.8 또는 2.9</span><span class="sxs-lookup"><span data-stu-id="790f3-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="790f3-115">이 지침은 사용자가 [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)과 Visual Studio를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="790f3-116">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="790f3-116">Creating a Project</span></span>
1. <span data-ttu-id="790f3-117">Visual Studio에서 **파일 | 새로 만들기 | 프로젝트**를 선택하여 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![파일 새로 만들기][file_new]

2. <span data-ttu-id="790f3-119">**Visual C# | 클라우드**에서 **Azure Resource Manager**를 선택하여 Azure Resource Manager 템플릿을 배포하는 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![프로젝트 만들기][create_project]

3. <span data-ttu-id="790f3-121">템플릿 목록에서 Linux 또는 Windows 가상 컴퓨터 규모 집합 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![템플릿 선택][select_Template]

4. <span data-ttu-id="790f3-123">프로젝트가 만들어지면 PowerShell 배포 스크립트, Azure Resource Manager 템플릿, 가상 컴퓨터 확장 집합의 매개 변수 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![솔루션 탐색기][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="790f3-125">프로젝트 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="790f3-125">Customize your project</span></span>
<span data-ttu-id="790f3-126">이제 템플릿을 편집하여 응용 프로그램의 요구(예: VM 확장 속성 추가 또는 부하 분산 규칙 편집 등)에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="790f3-127">기본적으로 가상 컴퓨터 확장 집합 템플릿은 자동 크기 조정 규칙을 손쉽게 추가할 수 있게 AzureDiagnostics 확장을 배포하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="790f3-128">또한 인바운드 NAT 규칙을 사용하여 구성된 공용 IP 주소를 가진 부하 분산 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="790f3-129">부하 분산 장치를 통해 SSH(Linux) 또는 RDP(Windows)를 사용하여 VM 인스턴스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="790f3-130">프런트 엔드 포트 범위는 50000에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="790f3-131">즉, Linux의 경우 포트 50000에 SSH하는 경우 확장 집합에 있는 첫 번째 VM의 포트 22에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="790f3-132">50001 포트로 연결하면 두 번째 VM의 22 포트로 라우팅되며 이런 방식으로 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="790f3-133">Visual Studio에서 템플릿을 편집하는 좋은 방법은 JSON 개요를 사용하여 매개 변수, 변수, 리소스를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="790f3-134">스키마에 대한 이해를 바탕으로, Visual Studio는 템플릿을 배포하기 전에 거기에 포함된 오류를 알려줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON 탐색기][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="790f3-136">프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="790f3-136">Deploy the project</span></span>
1. <span data-ttu-id="790f3-137">Azure Resource Manager 템플릿을 배포하여 가상 컴퓨터 확장 집합 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="790f3-138">프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **배포 | 새 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![템플릿 배포][5deploy_Template]
    
2. <span data-ttu-id="790f3-140">“리소스 그룹에 배포” 대화 상자에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![템플릿 배포][6deploy_Template]

3. <span data-ttu-id="790f3-142">여기에서 템플릿을 배포할 Azure 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![새 리소스 그룹][new_resource]

4. <span data-ttu-id="790f3-144">그런 다음 **매개 변수 편집**을 클릭하여 템플릿에 전달되는 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="790f3-145">배포하는 데 필요한 OS의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="790f3-146">PowerShell Tools for Visual Studio가 설치되지 않았다면 **암호 저장**을 확인하여 숨겨진 PowerShell 명령줄 프롬프트를 방지하하거나 [keyvault 지원](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![매개 변수 편집][edit_parameters]

5. <span data-ttu-id="790f3-148">이제 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-148">Now click **Deploy**.</span></span> <span data-ttu-id="790f3-149">**출력** 창에 배포 진행률이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="790f3-150">작업이 **Deploy-AzureResourceGroup.ps1** 스크립트를 실행 중입니다</span><span class="sxs-lookup"><span data-stu-id="790f3-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![출력 창][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="790f3-152">가상 컴퓨터 확장 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="790f3-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="790f3-153">배포가 완료되면 Visual Studio **클라우드 탐색기**에서(목록 새로 고침) 새로운 가상 컴퓨터 확장 집합을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="790f3-154">Cloud Explorer를 사용하면 응용 프로그램을 배포하는 동안 Visual Studio에서 Azure 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="790f3-155">[Azure Portal](https://portal.azure.com) 및 [Azure 리소스 탐색기](https://resources.azure.com/)에서 가상 컴퓨터 확장 집합을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="790f3-157">포털은 웹 브라우저를 사용하여 Azure 인프라를 시각적으로 관리하는 최고의 방법을 제공하며, Azure 리소스 탐색기는 Azure 리소스를 탐색하고 디버그하는 손쉬운 방법을 제공하고, “인스턴스 뷰”에 대한 창을 제공하며 표시되는 리소스에 대한 PowerShell 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="790f3-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="790f3-158">Next steps</span></span>
<span data-ttu-id="790f3-159">Visual Studio를 통해 가상 컴퓨터 확장 집합을 성공적으로 배포하면 응용 프로그램 요구 사항에 맞게 프로젝트를 추가로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="790f3-160">예를 들어, **Insights** 리소스를 추가하거나, 독립 실행형 VM처럼 템플릿에 인프라를 추가하거나, 사용자 지정 스크립트 확장을 사용하는 응용 프로그램을 배포하여 자동 크기 조정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="790f3-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="790f3-161">[Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates) GitHub 리포지토리에서 유용한 예제 템플릿을 찾을 수 있습니다("vmss" 검색).</span><span class="sxs-lookup"><span data-stu-id="790f3-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
