---
title: "Visual Studio Azure 리소스 그룹 프로젝트 | Microsoft Docs"
description: "Visual Studio를 사용하여 Azure 리소스 그룹 프로젝트를 만들고 Azure에 리소스를 배포합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: f82f59f363507b69a729580302c2d11202e93a87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="9e3e6-103">Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="9e3e6-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="9e3e6-104">Visual Studio 및 [Azure SDK](https://azure.microsoft.com/downloads/)를 사용하여 Azure로 인프라 및 코드를 배포하는 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-104">With Visual Studio and the [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code to Azure.</span></span> <span data-ttu-id="9e3e6-105">예를 들어 앱에 대한 웹 호스트, 웹 사이트 및 데이터베이스를 정의하고 코드와 함께 해당 인프라를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span></span> <span data-ttu-id="9e3e6-106">또는 가상 컴퓨터, 가상 네트워크 및 저장소 계정을 정의하고 가상 컴퓨터에서 실행되는 스크립트와 함께 해당 인프라를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span></span> <span data-ttu-id="9e3e6-107">**Azure 리소스 그룹** 배포 프로젝트는 하나의 반복 작업에 필요한 모든 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-107">The **Azure Resource Group** deployment project enables you to deploy all the needed resources in a single, repeatable operation.</span></span> <span data-ttu-id="9e3e6-108">리소스 배포 및 관리에 대한 자세한 내용은 [Azure 리소스 관리자 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="9e3e6-109">Azure 리소스 그룹 프로젝트는 Azure에 배포한 리소스를 정의하는 Azure Resource Manager JSON 템플릿을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define the resources that you deploy to Azure.</span></span> <span data-ttu-id="9e3e6-110">리소스 관리자 템플릿의 요소에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-110">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="9e3e6-111">Visual Studio는 이러한 템플릿을 편집할 수 있도록 하고 템플릿으로 작업을 간소화하는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-111">Visual Studio enables you to edit these templates, and provides tools that simplify working with templates.</span></span>

<span data-ttu-id="9e3e6-112">이 문서에서는 웹앱 및 SQL Database를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-112">In this article, you deploy a web app and SQL Database.</span></span> <span data-ttu-id="9e3e6-113">그러나 모든 종류의 리소스에 대해서도 거의 동일한 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-113">However, the steps are almost the same for any type resource.</span></span> <span data-ttu-id="9e3e6-114">가상 컴퓨터와 관련된 리소스를 손쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-114">You can as easily deploy a Virtual Machine and its related resources.</span></span> <span data-ttu-id="9e3e6-115">Visual Studio는 일반 시나리오를 배포하기 위한 다양한 서로 다른 시작 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-115">Visual Studio provides many different starter templates for deploying common scenarios.</span></span>

<span data-ttu-id="9e3e6-116">이 문서에서는 Visual Studio 2017을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-116">This article shows Visual Studio 2017.</span></span> <span data-ttu-id="9e3e6-117">Visual Studio 2015 업데이트 2 및 Microsoft Azure SDK for .NET 2.9 또는 Azure SDK 2.9와 함께 Visual Studio 2013을 사용하는 경우 환경은 대부분 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span></span> <span data-ttu-id="9e3e6-118">Azure SDK 2.6 이상의 버전을 사용할 수 있지만 사용자 인터페이스 환경이 이 문서에 표시된 것과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-118">You can use versions of the Azure SDK from 2.6 or later; however, your experience of the user interface may be different than the user interface shown in this article.</span></span> <span data-ttu-id="9e3e6-119">이 단계를 시작하기 전에 최신 버전의 [Azure SDK](https://azure.microsoft.com/downloads/) 를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-119">We strongly recommend that you install the latest version of the [Azure SDK](https://azure.microsoft.com/downloads/) before starting the steps.</span></span> 

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="9e3e6-120">Azure 리소스 그룹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9e3e6-120">Create Azure Resource Group project</span></span>
<span data-ttu-id="9e3e6-121">이 절차에서 **웹앱 + SQL** 템플릿으로 Azure 리소스 그룹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="9e3e6-122">Visual Studio에서 **파일**, **새 프로젝트**를 선택하고 **C#** 또는 **Visual Basic**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span></span> <span data-ttu-id="9e3e6-123">그런 다음 **클라우드**, **Azure 리소스 그룹** 프로젝트를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-123">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![Cloud Deployment 프로젝트](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="9e3e6-125">Azure 리소스 관리자에 배포하려는 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-125">Choose the template that you want to deploy to Azure Resource Manager.</span></span> <span data-ttu-id="9e3e6-126">배포하려는 프로젝트의 유형에 따라 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-126">Notice there are many different options based on the type of project you wish to deploy.</span></span> <span data-ttu-id="9e3e6-127">이 문서의 경우 **웹앱 + SQL** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-127">For this article, choose the **Web app + SQL** template.</span></span>
   
    ![템플릿 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="9e3e6-129">선택한 템플릿은 시작 지점일 뿐이며 시나리오를 충족하는 리소스를 추가 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-129">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9e3e6-130">Visual Studio은 온라인에서 사용 가능한 템플릿 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-130">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="9e3e6-131">목록은 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-131">The list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="9e3e6-132">Visual Studio는 웹앱 및 SQL 데이터베이스에 대한 리소스 그룹 배포 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-132">Visual Studio creates a resource group deployment project for the web app and SQL database.</span></span>
3. <span data-ttu-id="9e3e6-133">만든 항목을 보려면 배포 프로젝트에서 노드를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-133">To see what you created, look at the node in the deployment project.</span></span>
   
    ![노드 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="9e3e6-135">이 예제에 대한 웹앱 + SQL 템플릿을 선택한 후 다음 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-135">Since we chose the Web app + SQL template for this example, you see the following files:</span></span> 
   
   | <span data-ttu-id="9e3e6-136">파일 이름</span><span class="sxs-lookup"><span data-stu-id="9e3e6-136">File name</span></span> | <span data-ttu-id="9e3e6-137">설명</span><span class="sxs-lookup"><span data-stu-id="9e3e6-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="9e3e6-138">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="9e3e6-138">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="9e3e6-139">Azure Resource Manager를 배포할 PowerShell 명령을 호출하는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-139">A PowerShell script that invokes PowerShell commands to deploy to Azure Resource Manager.</span></span><br /><span data-ttu-id="9e3e6-140">**참고** 이 PowerShell 스크립트는 Visual Studio에서 템플릿을 배포하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-140">**Note** Visual Studio uses this PowerShell script to deploy your template.</span></span> <span data-ttu-id="9e3e6-141">이 스크립트를 변경하면 Visual Studio의 배포에 영향이 있으므로 신중해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-141">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="9e3e6-142">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="9e3e6-142">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="9e3e6-143">Azure에 배포하려는 인프라를 정의하는 Resource Manager 템플릿 및 배포하는 동안 제공할 수 있는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-143">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span></span> <span data-ttu-id="9e3e6-144">또한 Resource Manager가 리소스를 올바른 순서로 배포하도록 리소스 간의 종속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-144">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span></span> |
   | <span data-ttu-id="9e3e6-145">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="9e3e6-145">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="9e3e6-146">템플릿에 필요한 값을 포함하는 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-146">A parameters file that contains values needed by the template.</span></span> <span data-ttu-id="9e3e6-147">각 배포를 사용자 지정하는 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-147">You pass in parameter values to customize each deployment.</span></span> |
   
    <span data-ttu-id="9e3e6-148">모든 리소스 그룹 배포 프로젝트는 이러한 기본 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-148">All resource group deployment projects contain these basic files.</span></span> <span data-ttu-id="9e3e6-149">다른 프로젝트는 다른 기능을 지원하는 추가 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-149">Other projects may contain additional files to support other functionality.</span></span>

## <a name="customize-the-resource-manager-template"></a><span data-ttu-id="9e3e6-150">리소스 관리자 템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9e3e6-150">Customize the Resource Manager template</span></span>
<span data-ttu-id="9e3e6-151">배포하려는 리소스를 설명하는 JSON 템플릿 파일을 수정하여 배포 프로젝트를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-151">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span></span> <span data-ttu-id="9e3e6-152">JSON은 JavaScript Object Notation의 약어로, 쉽게 작업할 수 있는 직렬화된 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span></span> <span data-ttu-id="9e3e6-153">JSON 파일은 각 파일의 위쪽에서 참조하는 스키마를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-153">The JSON files use a schema that you reference at the top of each file.</span></span> <span data-ttu-id="9e3e6-154">스키마를 이해하려면 다운로드하여 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-154">If you want to understand the schema, you can download and analyze it.</span></span> <span data-ttu-id="9e3e6-155">스키마는 유효한 요소, 필드의 형식 및 포맷, 열거형 값의 가능한 값 등을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-155">The schema defines what elements are valid, the types and formats of fields, the possible values of enumerated values, and so on.</span></span> <span data-ttu-id="9e3e6-156">리소스 관리자 템플릿의 요소에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-156">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9e3e6-157">템플릿에서 작업하려면 **WebSiteSQLDatabase.json**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-157">To work on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="9e3e6-158">Visual Studio 편집기는 Resource Manager 템플릿 편집에 도움이 되는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-158">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span></span> <span data-ttu-id="9e3e6-159">**JSON 개요** 창을 통해 템플릿에 정의된 요소를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-159">The **JSON Outline** window makes it easy to see the elements defined in your template.</span></span>

![JSON 개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="9e3e6-161">개요에서 요소 중 하나를 선택하면 템플릿의 해당 부분으로 이동하고 해당 JSON을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-161">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span></span>

![JSON로 이동](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="9e3e6-163">JSON 개요 창의 맨 위에 있는 **리소스 추가** 버튼을 선택하거나 **리소스**를 마우스 오른쪽 단추로 클릭하고 **새 리소스 추가**를 선택하여 리소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-163">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="9e3e6-165">이 자습서의 경우 **저장소 계정** 을 선택하고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-165">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="9e3e6-166">11개 미만의 문자이며 숫자 및 소문자만을 포함하는 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![저장소 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="9e3e6-168">추가된 리소스 뿐만 아니라 형식 저장소 계정에 대한 매개 변수 및 저장소 계정 이름에 대한 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-168">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span></span>

![개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="9e3e6-170">**storageType** 매개 변수는 허용되는 형식 및 기본 형식을 사용하여 미리 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-170">The **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="9e3e6-171">이러한 값을 유지하거나 시나리오에 대해 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-171">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="9e3e6-172">이 템플릿을 통해 **Premium_LRS** 저장소 계정을 배포하지 않으려는 경우 허용된 형식에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-172">If you do not want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span></span> 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

<span data-ttu-id="9e3e6-173">Visual Studio는 또한 템플릿을 편집하는 경우 사용 가능한 속성을 이해할 수 있도록 intellisense를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-173">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span></span> <span data-ttu-id="9e3e6-174">예를 들어 App Service 계획에 대한 속성을 편집하려면 **HostingPlan** 리소스로 이동하고 **속성**에 대한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-174">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span></span> <span data-ttu-id="9e3e6-175">intellisense는 사용 가능한 값을 표시하고 해당 값에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-175">Notice that intellisense shows the available values and provides a description of that value.</span></span>

![intellisense 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="9e3e6-177">**numberOfWorkers** 를 1로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-177">You can set **numberOfWorkers** to 1.</span></span>

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-the-resource-group-project-to-azure"></a><span data-ttu-id="9e3e6-178">Azure에 리소스 그룹 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="9e3e6-178">Deploy the Resource Group project to Azure</span></span>
<span data-ttu-id="9e3e6-179">이제 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-179">You are now ready to deploy your project.</span></span> <span data-ttu-id="9e3e6-180">Azure 리소스 그룹 프로젝트를 배포할 때 Azure 리소스 그룹에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-180">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span></span> <span data-ttu-id="9e3e6-181">리소스 그룹은 공통 수명 주기를 공유하는 리소스의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-181">The resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="9e3e6-182">배포 프로젝트 노드의 바로 가기 메뉴에서 **배포** > **새 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-182">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![배포, 새 배포 메뉴 항목](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="9e3e6-184">**리소스 그룹에 배포** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-184">The **Deploy to Resource Group** dialog box appears.</span></span>
   
    ![리소스 그룹에 배포 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="9e3e6-186">**리소스 그룹** 드롭다운 상자에서 기존 리소스 그룹을 선택하거나 새 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-186">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="9e3e6-187">리소스 그룹을 만들려면 **리소스 그룹** 드롭다운 상자를 열고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-187">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![리소스 그룹에 배포 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="9e3e6-189">**리소스 그룹 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-189">The **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="9e3e6-190">그룹에 이름 및 위치를 지정하고 **만들기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-190">Give your group a name and location, and select the **Create** button.</span></span>
   
    ![리소스 그룹 만들기 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="9e3e6-192">**매개 변수 편집** 단추를 선택하여 배포에 대한 매개 변수를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-192">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span></span>
   
    ![매개 변수 편집 단추](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="9e3e6-194">비어 있는 매개 변수에 값을 제공하고 **저장** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-194">Provide values for the empty parameters and select the **Save** button.</span></span> <span data-ttu-id="9e3e6-195">비어 있는 매개 변수는 **hostingPlanName**, **administratorLogin**, **administratorLoginPassword** 및 **databaseName**입니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-195">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="9e3e6-196">**hostingPlanName** 은 만들려는 [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-196">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span></span> 
   
    <span data-ttu-id="9e3e6-197">**administratorLogin** 은 SQL Server 관리자의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-197">**administratorLogin** specifies the user name for the SQL Server administrator.</span></span> <span data-ttu-id="9e3e6-198">**sa** 또는 **admin**과 같은 일반 관리자 이름을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-198">Do not use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="9e3e6-199">**administratorLoginPassword** 는 SQL Server 관리자의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-199">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="9e3e6-200">**암호를 매개 변수 파일에 일반 텍스트로 저장** 옵션은 안전하지 않으므로 이 옵션을 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-200">The **Save passwords as plain text in the parameters file** option is not secure; therefore, do not select this option.</span></span> <span data-ttu-id="9e3e6-201">암호는 일반 텍스트로 저장되지 않으므로 배포 중에 이 암호를 다시 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-201">Since the password is not saved as plain text, you need to provide this password again during deployment.</span></span> 
   
    <span data-ttu-id="9e3e6-202">**databaseName** 은 만들 데이터베이스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-202">**databaseName** specifies a name for the database to create.</span></span> 
   
    ![매개 변수 편집 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="9e3e6-204">**배포** 단추를 선택하여 Azure에 프로젝트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-204">Choose the **Deploy** button to deploy the project to Azure.</span></span> <span data-ttu-id="9e3e6-205">Visual Studio 인스턴스의 외부에서 PowerShell 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-205">A PowerShell console opens outside of the Visual Studio instance.</span></span> <span data-ttu-id="9e3e6-206">메시지가 표시되면 PowerShell 콘솔에 SQL Server 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-206">Enter the SQL Server administrator password in the PowerShell console when prompted.</span></span> <span data-ttu-id="9e3e6-207">**PowerShell 콘솔은 다른 항목 뒤에 숨겨지거나 작업 표시줄에서 최소화될 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="9e3e6-207">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span></span> <span data-ttu-id="9e3e6-208">이 콘솔을 찾아서 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-208">Look for this console and select it to provide the password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9e3e6-209">Visual Studio에서는 Azure PowerShell cmdlet을 설치하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-209">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9e3e6-210">리소스 그룹을 성공적으로 배포하려면 Azure PowerShell cmdlet이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-210">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span></span> <span data-ttu-id="9e3e6-211">메시지가 표시되면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-211">If prompted, install them.</span></span>
   > 
   > 
6. <span data-ttu-id="9e3e6-212">배포는 몇 분 정도가 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-212">The deployment may take a few minutes.</span></span> <span data-ttu-id="9e3e6-213">**출력** 창에 배포의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-213">In the **Output** windows, you see the status of the deployment.</span></span> <span data-ttu-id="9e3e6-214">배포가 완료되면 마지막 메시지는 다음과 유사한 내용으로 성공적인 배포를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-214">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' to resource group 'DemoSiteGroup'.
7. <span data-ttu-id="9e3e6-215">브라우저에서 [Azure Portal](https://portal.azure.com/) 을 열고 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-215">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span></span> <span data-ttu-id="9e3e6-216">리소스 그룹을 보려면 **리소스 그룹** 및 배포한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-216">To see the resource group, select **Resource groups** and the resource group you deployed to.</span></span>
   
    ![그룹 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="9e3e6-218">배포된 리소스가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-218">You see all the deployed resources.</span></span> <span data-ttu-id="9e3e6-219">저장소 계정의 이름은 해당 리소스를 추가할 때 지정한 것과 일치하지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-219">Notice that the name of the storage account is not exactly what you specified when adding that resource.</span></span> <span data-ttu-id="9e3e6-220">저장소 계정은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-220">The storage account must be unique.</span></span> <span data-ttu-id="9e3e6-221">고유한 이름을 제공하기 위해 템플릿은 자동으로 사용자가 제공한 이름에 문자의 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-221">The template automatically adds a string of characters to the name you provided to provide a unique name.</span></span> 
   
    ![리소스 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="9e3e6-223">프로젝트를 변경하고 다시 배포할 경우, Azure 리소스 그룹 프로젝트의 바로 가기 메뉴에서 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-223">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="9e3e6-224">바로 가기 메뉴에서 **배포**를 선택한 다음 배포한 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-224">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span></span>
   
    ![배포된 Azure 리소스 그룹](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="9e3e6-226">인프라를 사용하여 코드 배포</span><span class="sxs-lookup"><span data-stu-id="9e3e6-226">Deploy code with your infrastructure</span></span>
<span data-ttu-id="9e3e6-227">이 시점에서 앱에 대한 인프라를 배포했지만 프로젝트와 함께 배포된 실제 코드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-227">At this point, you have deployed the infrastructure for your app, but there is no actual code deployed with the project.</span></span> <span data-ttu-id="9e3e6-228">이 문서에서는 배포하는 동안 웹앱 및 SQL Database 테이블을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-228">This article shows how to deploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="9e3e6-229">웹앱 대신 가상 컴퓨터를 배포하는 경우 배포의 일부로 컴퓨터에 일부 코드를 실행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-229">If you are deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span></span> <span data-ttu-id="9e3e6-230">웹앱에 대한 코드 배포 또는 가상 컴퓨터 설정을 위한 절차는 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-230">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span></span>

1. <span data-ttu-id="9e3e6-231">Visual Studio 솔루션에 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-231">Add a project to your Visual Studio solution.</span></span> <span data-ttu-id="9e3e6-232">솔루션을 마우스 오른쪽 단추로 클릭하고 **추가** > **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-232">Right-click the solution, and select **Add** > **New Project**.</span></span>
   
    ![프로젝트 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="9e3e6-234">**ASP.NET 웹 응용 프로그램**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-234">Add an **ASP.NET Web Application**.</span></span> 
   
    ![웹앱 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="9e3e6-236">**MVC**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-236">Select **MVC**.</span></span>
   
    ![MVC 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="9e3e6-238">Visual Studio에서 웹앱을 만든 후에 솔루션에 두 프로젝트가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-238">After Visual Studio creates your web app, you see both projects in the solution.</span></span>
   
    ![프로젝트 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="9e3e6-240">이제, 리소스 그룹 프로젝트가 새 프로젝트를 인식하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-240">Now, you need to make sure your resource group project is aware of the new project.</span></span> <span data-ttu-id="9e3e6-241">리소스 그룹 프로젝트(AzureResourceGroup1)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-241">Go back to your resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="9e3e6-242">**참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-242">Right-click **References** and select **Add Reference**.</span></span>
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="9e3e6-244">만든 웹앱 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-244">Select the web app project that you created.</span></span>
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="9e3e6-246">참조를 추가하여 리소스 그룹 프로젝트에 웹앱 프로젝트에 연결하고 자동으로 세 가지 주요 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-246">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="9e3e6-247">참조를 위한 **속성** 창에서 이러한 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-247">You see these properties in the **Properties** window for the reference.</span></span>
   
      ![참조 보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="9e3e6-249">속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-249">The properties are:</span></span>
   
   * <span data-ttu-id="9e3e6-250">**추가 속성** 은 Azure Storage에 푸시되는 웹 배포 패키지 준비 위치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-250">The **Additional Properties** contains the web deployment package staging location that is pushed to the Azure Storage.</span></span> <span data-ttu-id="9e3e6-251">폴더(ExampleApp) 및 파일(package.zip)을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-251">Note the folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="9e3e6-252">이러한 값은 앱을 배포할 때 매개 변수로 제공하므로 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-252">You need to know these values because you provide them as parameters when deploying the app.</span></span> 
   * <span data-ttu-id="9e3e6-253">**파일 경로 포함** 은 패키지를 만들 경로를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-253">The **Include File Path** contains the path where the package is created.</span></span> <span data-ttu-id="9e3e6-254">**대상 포함** 은 배포가 실행할 명령을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-254">The **Include Targets** contains the command that deployment executes.</span></span> 
   * <span data-ttu-id="9e3e6-255">**빌드;패키지** 의 기본값을 통해 배포는 웹 배포 패키지(package.zip)를 빌드하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-255">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="9e3e6-256">배포는 패키지를 만드는 속성에서 필요한 정보를 얻게 되므로 게시 프로필이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-256">You do not need a publish profile as the deployment gets the necessary information from the properties to create the package.</span></span>
7. <span data-ttu-id="9e3e6-257">WebSiteSQLDatabase.json으로 돌아와서 템플릿에 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-257">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span></span>
   
    ![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="9e3e6-259">이번에는 **Web Apps에 대한 웹 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-259">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="9e3e6-261">리소스 그룹에 리소스 그룹 프로젝트를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-261">Redeploy your resource group project to the resource group.</span></span> <span data-ttu-id="9e3e6-262">이번에는 몇 가지 새로운 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-262">This time there are some new parameters.</span></span> <span data-ttu-id="9e3e6-263">자동으로 생성되므로 **_artifactsLocation** 또는 **_artifactsLocationSasToken**에 대한 값을 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-263">You do not need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="9e3e6-264">그러나 폴더와 파일 이름을 배포 패키지를 포함하는 경로로 설정해야 합니다(다음 이미지에서 **ExampleAppPackageFolder** 및 **ExampleAppPackageFileName**으로 나타남).</span><span class="sxs-lookup"><span data-stu-id="9e3e6-264">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span></span> <span data-ttu-id="9e3e6-265">앞서 참조 속성에서 확인한 값을 제공합니다(**ExampleApp** 및 **package.zip**).</span><span class="sxs-lookup"><span data-stu-id="9e3e6-265">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="9e3e6-267">**아티팩트 저장소 계정**의 경우 이 리소스 그룹과 함께 배포된 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-267">For the **Artifact storage account**, select the one deployed with this resource group.</span></span>
10. <span data-ttu-id="9e3e6-268">배포가 완료된 후에 포털에서 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-268">After the deployment has finished, select your web app in the portal.</span></span> <span data-ttu-id="9e3e6-269">URL을 선택하여 사이트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-269">Select the URL to browse to the site.</span></span>
    
     ![사이트 찾아보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="9e3e6-271">기본 ASP.NET 앱을 성공적으로 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-271">Notice that you have successfully deployed the default ASP.NET app.</span></span>
    
     ![배포된 앱 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a><span data-ttu-id="9e3e6-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e3e6-273">Next steps</span></span>
* <span data-ttu-id="9e3e6-274">포털을 통한 리소스 관리에 대한 내용은 [Azure Portal을 사용하여 Azure 리소스 관리](resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-274">To learn about managing your resources through the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="9e3e6-275">템플릿에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e3e6-275">To learn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

