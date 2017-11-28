---
title: "Visual Studio를 사용 하 여 가상 컴퓨터 크기 집합 aaaDeploy | Microsoft Docs"
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
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="dc192-103">어떻게 toocreate 가상 컴퓨터 크기는 Visual Studio와 함께 집합</span><span class="sxs-lookup"><span data-stu-id="dc192-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="dc192-104">이 문서에 어떻게 toodeploy는 Azure 가상 컴퓨터 크기 집합 Visual Studio 리소스 그룹 배포를 사용 하 여 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="dc192-105">[Azure 가상 컴퓨터 크기 집합](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) 는 Azure 계산 리소스 toodeploy의 자동 크기 조정와 유사한 가상 컴퓨터의 컬렉션을 관리 및 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="dc192-106">[Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates)을 사용하여 가상 컴퓨터 확장 집합을 프로비전하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="dc192-107">Azure Resource Manager 템플릿은 Azure CLI, PowerShell, REST를 사용하여 배포가 가능하고 Visual Studio에서 직접 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="dc192-108">Visual Studio는 Azure 리소스 그룹 배포 프로젝트의 일부로 배포될 수 있는 예제 템플릿 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="dc192-109">Azure 리소스 그룹 배포 방법은 toogroup 이며 단일 배포 작업에 관련된 Azure 리소스의 집합을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="dc192-110">자세한 내용은 [Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc192-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="dc192-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dc192-111">Pre-requisites</span></span>
<span data-ttu-id="dc192-112">Visual Studio에서 가상 컴퓨터 크기 집합 배포를 시작 하는 tooget, hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="dc192-113">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="dc192-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="dc192-114">Azure SDK 2.7, 2.8 또는 2.9</span><span class="sxs-lookup"><span data-stu-id="dc192-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="dc192-115">이 지침은 사용자가 [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)과 Visual Studio를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="dc192-116">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="dc192-116">Creating a Project</span></span>
1. <span data-ttu-id="dc192-117">Visual Studio에서 **파일 | 새로 만들기 | 프로젝트**를 선택하여 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![파일 새로 만들기][file_new]

2. <span data-ttu-id="dc192-119">**Visual C# | 클라우드**, 선택 **Azure 리소스 관리자** toocreate Azure 리소스 관리자 템플릿을 배포 하기 위한 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![프로젝트 만들기][create_project]

3. <span data-ttu-id="dc192-121">Hello 템플릿 목록에서 hello Linux 또는 Windows 가상 컴퓨터 크기 조정 설정 템플릿 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![템플릿 선택][select_Template]

4. <span data-ttu-id="dc192-123">프로젝트가 만들어지면 PowerShell 배포 스크립트는 Azure 리소스 관리자 템플릿 및 가상 컴퓨터 크기 집합 hello에 대 한 매개 변수 파일을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![솔루션 탐색기][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="dc192-125">프로젝트 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="dc192-125">Customize your project</span></span>
<span data-ttu-id="dc192-126">Hello 템플릿 toocustomize를 편집할 수 이제 VM 확장 속성을 추가 하거나 편집 같은 응용 프로그램의 요구 사항에 대해 부하 분산 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="dc192-127">기본적으로 hello 가상 컴퓨터 크기 조정 설정 템플릿을 쉽게 tooadd 자동 크기 조정 규칙 하므로 구성 된 toodeploy hello AzureDiagnostics 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="dc192-128">또한 인바운드 NAT 규칙을 사용하여 구성된 공용 IP 주소를 가진 부하 분산 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="dc192-129">hello 부하 분산 장치 (Windows) RDP 또는 SSH (Linux) toohello VM 인스턴스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="dc192-130">hello 프런트 엔드 포트 범위가 50000 이상에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="dc192-131">Linux 용 즉의 라우트된 tooport 22는 하면 SSH tooport 50000, 첫 번째 VM 크기 집합 hello에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="dc192-132">연결 하는 tooport 50001는 hello의 라우트된 tooport 22 등 VM의 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="dc192-133">좋은 방법 tooedit Visual Studio와 함께 서식 파일은 toouse hello JSON 개요 tooorganize hello 매개 변수, 변수 및 리소스.</span><span class="sxs-lookup"><span data-stu-id="dc192-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="dc192-134">배포 하기 전에 hello 이해 스키마 Visual Studio 서식 파일에서 오류 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON 탐색기][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="dc192-136">Hello 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="dc192-136">Deploy hello project</span></span>
1. <span data-ttu-id="dc192-137">Hello Azure 리소스 관리자 템플릿 toocreate hello 가상 컴퓨터 크기 집합 리소스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="dc192-138">Hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **배포 | 새 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![템플릿 배포][5deploy_Template]
    
2. <span data-ttu-id="dc192-140">Hello "배포 tooResource 그룹" 대화 상자에서 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![템플릿 배포][6deploy_Template]

3. <span data-ttu-id="dc192-142">여기에서는 Azure 리소스 그룹 toodeploy 서식 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![새 리소스 그룹][new_resource]

4. <span data-ttu-id="dc192-144">그런 다음 클릭 **매개 변수 편집** tooyour 서식 파일을 전달 되는 tooenter 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="dc192-145">Hello 필요한 toocreate hello 배포는 운영 체제에 대 한 hello 사용자 이름 및 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="dc192-146">Visual Studio가 설치에 대 한 PowerShell 도구 없다면 것이 좋습니다 toocheck **암호를 저장** tooavoid 숨겨진된 PowerShell 명령줄 프롬프트를 사용 하 여 또는 [keyvault 지원](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![매개 변수 편집][edit_parameters]

5. <span data-ttu-id="dc192-148">이제 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-148">Now click **Deploy**.</span></span> <span data-ttu-id="dc192-149">hello **출력** 창 hello 배포 진행률을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="dc192-150">Hello 동작의 hello 실행 하는 참고 **deploy-azureresourcegroup.ps1 스크립트로** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![출력 창][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="dc192-152">가상 컴퓨터 확장 집합 탐색</span><span class="sxs-lookup"><span data-stu-id="dc192-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="dc192-153">Hello 배포가 완료 된 후 볼 수 있습니다 hello Visual Studio에서에서 새 가상 컴퓨터 크기 집합 hello **클라우드 탐색기** (새로 고침 hello 목록).</span><span class="sxs-lookup"><span data-stu-id="dc192-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="dc192-154">Cloud Explorer를 사용하면 응용 프로그램을 배포하는 동안 Visual Studio에서 Azure 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="dc192-155">Hello에 가상 컴퓨터 크기 집합을 볼 수 [Azure 포털](https://portal.azure.com) 및 [Azure 리소스 탐색기](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="dc192-157">hello 포털 toovisually Azure 리소스 탐색기를 쉽게 tooexplore을 제공 하지만 웹 브라우저에서 Azure 인프라를 관리 하는 hello 가장 좋은 방법은 제공 및 Azure 리소스를 디버그, "인스턴스 보기" hello에 창을 제공 하 고 보여 주는 PowerShell 원하는 hello 리소스에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc192-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc192-158">Next steps</span></span>
<span data-ttu-id="dc192-159">Visual Studio를 통해 가상 컴퓨터 크기 집합 성공적으로 배포 되 면 프로젝트 toosuit를 응용 프로그램 요구 사항 추가로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="dc192-160">예를 들어, 추가 하 여 자동 크기 조정 구성는 **Insights** 리소스, 인프라 tooyour 서식 파일 (예: 독립 실행형 Vm)를 추가 하거나 hello 사용자 지정 스크립트 확장을 사용 하 여 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc192-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="dc192-161">Hello에 좋은 예 템플릿 있습니다 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates) GitHub 리포지토리 ("vmss" 검색).</span><span class="sxs-lookup"><span data-stu-id="dc192-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
