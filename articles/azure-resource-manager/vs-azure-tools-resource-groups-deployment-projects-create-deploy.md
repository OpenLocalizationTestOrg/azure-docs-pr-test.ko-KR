---
title: "aaaVisual Studio Azure 리소스 그룹 프로젝트 | Microsoft Docs"
description: "Visual Studio toocreate Azure 리소스 그룹 프로젝트를 사용 하 하 고 hello 리소스 tooAzure 배포."
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
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="57ed5-103">Visual Studio를 통해 Azure 리소스 그룹 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="57ed5-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="57ed5-104">Visual Studio 및 hello [Azure SDK](https://azure.microsoft.com/downloads/), 인프라 및 코드 tooAzure를 배포 하는 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-104">With Visual Studio and hello [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code tooAzure.</span></span> <span data-ttu-id="57ed5-105">예를 들어 응용 프로그램에 대 한 hello 웹 호스트, 웹 사이트 및 데이터베이스를 정의 하 고 hello 코드와 함께 해당 인프라를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-105">For example, you can define hello web host, web site, and database for your app, and deploy that infrastructure along with hello code.</span></span> <span data-ttu-id="57ed5-106">또는 가상 컴퓨터, 가상 네트워크 및 저장소 계정을 정의하고 가상 컴퓨터에서 실행되는 스크립트와 함께 해당 인프라를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span></span> <span data-ttu-id="57ed5-107">hello **Azure 리소스 그룹** 배포 프로젝트를 반복 가능한 단일 작업에서 모든 필요한 hello 리소스가 toodeploy 있습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-107">hello **Azure Resource Group** deployment project enables you toodeploy all hello needed resources in a single, repeatable operation.</span></span> <span data-ttu-id="57ed5-108">리소스 배포 및 관리에 대한 자세한 내용은 [Azure 리소스 관리자 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57ed5-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="57ed5-109">Azure 리소스 그룹 프로젝트 tooAzure를 배포 하는 hello 리소스를 정의 하는 Azure 리소스 관리자 JSON 템플릿이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define hello resources that you deploy tooAzure.</span></span> <span data-ttu-id="57ed5-110">toolearn hello 리소스 관리자 템플릿 hello 요소에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-110">toolearn about hello elements of hello Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="57ed5-111">Visual Studio tooedit 있습니다 이러한 서식 파일을 사용 하 고 서식 파일 사용을 단순화 하는 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-111">Visual Studio enables you tooedit these templates, and provides tools that simplify working with templates.</span></span>

<span data-ttu-id="57ed5-112">이 문서에서는 웹앱 및 SQL Database를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-112">In this article, you deploy a web app and SQL Database.</span></span> <span data-ttu-id="57ed5-113">그러나 hello 단계 거의 모든 종류의 리소스에 대 한 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-113">However, hello steps are almost hello same for any type resource.</span></span> <span data-ttu-id="57ed5-114">가상 컴퓨터와 관련된 리소스를 손쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-114">You can as easily deploy a Virtual Machine and its related resources.</span></span> <span data-ttu-id="57ed5-115">Visual Studio는 일반 시나리오를 배포하기 위한 다양한 서로 다른 시작 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-115">Visual Studio provides many different starter templates for deploying common scenarios.</span></span>

<span data-ttu-id="57ed5-116">이 문서에서는 Visual Studio 2017을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-116">This article shows Visual Studio 2017.</span></span> <span data-ttu-id="57ed5-117">.NET 2.9에 대 한 Visual Studio 2015 업데이트 2와 Microsoft Azure SDK를 사용 하거나 Azure SDK 2.9에서는 환경 Visual Studio 2013은 주로 경우 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely hello same.</span></span> <span data-ttu-id="57ed5-118">Hello Azure SDK 2.6 이상;의 버전을 사용할 수 있습니다. 그러나 hello 사용자 인터페이스의 경험이이 문서에 표시 된 hello 사용자 인터페이스 보다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-118">You can use versions of hello Azure SDK from 2.6 or later; however, your experience of hello user interface may be different than hello user interface shown in this article.</span></span> <span data-ttu-id="57ed5-119">최신 버전의 hello hello를 설치 하는 것이 좋습니다 [Azure SDK](https://azure.microsoft.com/downloads/) hello 단계를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="57ed5-119">We strongly recommend that you install hello latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/) before starting hello steps.</span></span> 

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="57ed5-120">Azure 리소스 그룹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="57ed5-120">Create Azure Resource Group project</span></span>
<span data-ttu-id="57ed5-121">이 절차에서 **웹앱 + SQL** 템플릿으로 Azure 리소스 그룹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="57ed5-122">Visual Studio에서 **파일**, **새 프로젝트**를 선택하고 **C#** 또는 **Visual Basic**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span></span> <span data-ttu-id="57ed5-123">그런 다음 **클라우드**, **Azure 리소스 그룹** 프로젝트를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-123">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![Cloud Deployment 프로젝트](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="57ed5-125">Hello 템플릿 선택 toodeploy tooAzure 리소스 관리자 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-125">Choose hello template that you want toodeploy tooAzure Resource Manager.</span></span> <span data-ttu-id="57ed5-126">프로젝트의 다양 한 옵션 hello에 따라 입력는 공지 toodeploy를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-126">Notice there are many different options based on hello type of project you wish toodeploy.</span></span> <span data-ttu-id="57ed5-127">이 문서에 대 한 선택 hello **웹 응용 프로그램 + SQL** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="57ed5-127">For this article, choose hello **Web app + SQL** template.</span></span>
   
    ![템플릿 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="57ed5-129">선택 하는 hello 서식 파일은 이제 시작 지점입니다. 추가 하 고 리소스 toofulfill 시나리오를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-129">hello template you pick is just a starting point; you can add and remove resources toofulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="57ed5-130">Visual Studio은 온라인에서 사용 가능한 템플릿 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-130">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="57ed5-131">hello 목록 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-131">hello list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="57ed5-132">Visual Studio hello web app 및 SQL 데이터베이스에 대 한 리소스 그룹 배포 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-132">Visual Studio creates a resource group deployment project for hello web app and SQL database.</span></span>
3. <span data-ttu-id="57ed5-133">toosee 작성, 봐 hello 배포 프로젝트의 hello 노드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-133">toosee what you created, look at hello node in hello deployment project.</span></span>
   
    ![노드 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="57ed5-135">이 예제에 대 한 SQL 템플릿 + hello 웹 응용 프로그램을 선택 했으므로 hello 다음 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-135">Since we chose hello Web app + SQL template for this example, you see hello following files:</span></span> 
   
   | <span data-ttu-id="57ed5-136">파일 이름</span><span class="sxs-lookup"><span data-stu-id="57ed5-136">File name</span></span> | <span data-ttu-id="57ed5-137">설명</span><span class="sxs-lookup"><span data-stu-id="57ed5-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="57ed5-138">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="57ed5-138">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="57ed5-139">PowerShell 명령 toodeploy tooAzure 리소스 관리자를 호출 하는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-139">A PowerShell script that invokes PowerShell commands toodeploy tooAzure Resource Manager.</span></span><br /><span data-ttu-id="57ed5-140">**참고** Visual Studio에서는이 PowerShell 스크립트 toodeploy 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-140">**Note** Visual Studio uses this PowerShell script toodeploy your template.</span></span> <span data-ttu-id="57ed5-141">모든 변경 사항은 toothis 스크립트 Visual Studio에서 배포에 영향을 주의 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-141">Any changes you make toothis script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="57ed5-142">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="57ed5-142">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="57ed5-143">tooAzure, 배포할 hello 인프라 및 배포 하는 동안 제공할 수 있습니다 hello 매개 변수를 정의 하는 hello 리소스 관리자 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-143">hello Resource Manager template that defines hello infrastructure you want deploy tooAzure, and hello parameters you can provide during deployment.</span></span> <span data-ttu-id="57ed5-144">또한 리소스 관리자 hello 올바른 순서로 hello 리소스를 배포 하도록 hello 리소스 간의 hello 종속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-144">It also defines hello dependencies between hello resources so Resource Manager deploys hello resources in hello correct order.</span></span> |
   | <span data-ttu-id="57ed5-145">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="57ed5-145">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="57ed5-146">Hello 서식 파일에 필요한 값을 포함 하는 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-146">A parameters file that contains values needed by hello template.</span></span> <span data-ttu-id="57ed5-147">각 배포 매개 변수 값 toocustomize에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-147">You pass in parameter values toocustomize each deployment.</span></span> |
   
    <span data-ttu-id="57ed5-148">모든 리소스 그룹 배포 프로젝트는 이러한 기본 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-148">All resource group deployment projects contain these basic files.</span></span> <span data-ttu-id="57ed5-149">다른 프로젝트는 다른 기능 추가 파일 toosupport 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-149">Other projects may contain additional files toosupport other functionality.</span></span>

## <a name="customize-hello-resource-manager-template"></a><span data-ttu-id="57ed5-150">Hello 리소스 관리자 템플릿을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="57ed5-150">Customize hello Resource Manager template</span></span>
<span data-ttu-id="57ed5-151">원하는 toodeploy hello 리소스를 설명 하는 hello JSON 템플릿을 수정 하 여 배포 프로젝트를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-151">You can customize a deployment project by modifying hello JSON templates that describe hello resources you want toodeploy.</span></span> <span data-ttu-id="57ed5-152">JSON에 대 한 JavaScript 개체 Object Notation 의미 하 고는와 쉽게 toowork 있는 serialize 된 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy toowork with.</span></span> <span data-ttu-id="57ed5-153">hello JSON 파일에서 각 파일의 맨 위에 hello 참조 하는 스키마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-153">hello JSON files use a schema that you reference at hello top of each file.</span></span> <span data-ttu-id="57ed5-154">Toounderstand hello 스키마를 사용 하도록 하려는 경우 다운로드 하 고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-154">If you want toounderstand hello schema, you can download and analyze it.</span></span> <span data-ttu-id="57ed5-155">hello 스키마 정의 어떤 요소가 유효한 hello 형식 및 필드의 형식 열거형된 값의 가능한 값 hello 하 고, 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-155">hello schema defines what elements are valid, hello types and formats of fields, hello possible values of enumerated values, and so on.</span></span> <span data-ttu-id="57ed5-156">toolearn hello 리소스 관리자 템플릿 hello 요소에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-156">toolearn about hello elements of hello Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="57ed5-157">서식 파일을에 toowork 열고 **WebSiteSQLDatabase.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-157">toowork on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="57ed5-158">hello 편집기에서는 Visual Studio 도구 tooassist 리소스 관리자 템플릿을 hello 편집 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-158">hello Visual Studio editor provides tools tooassist you with editing hello Resource Manager template.</span></span> <span data-ttu-id="57ed5-159">hello **JSON 개요** 창을 사용 하 여 서식 파일에 정의 된 쉽게 toosee hello 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-159">hello **JSON Outline** window makes it easy toosee hello elements defined in your template.</span></span>

![JSON 개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="57ed5-161">Hello 개요에서 hello 요소 중 하나를 선택 하면 hello 템플릿의 toothat 일부를 사용 하 고 JSON에 해당 하는 hello를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-161">Selecting any of hello elements in hello outline takes you toothat part of hello template and highlights hello corresponding JSON.</span></span>

![JSON로 이동](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="57ed5-163">중 하나가 선택 hello 여 리소스를 추가할 수 있습니다 **리소스 추가** hello JSON 개요 창의 하거나 마우스 오른쪽 단추로 클릭 하 여 hello 위쪽에 단추 **리소스** 선택 하 고 **새 리소스 추가**.</span><span class="sxs-lookup"><span data-stu-id="57ed5-163">You can add a resource by either selecting hello **Add Resource** button at hello top of hello JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="57ed5-165">이 자습서의 경우 **저장소 계정** 을 선택하고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-165">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="57ed5-166">11개 미만의 문자이며 숫자 및 소문자만을 포함하는 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![저장소 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="57ed5-168">Hello 리소스 추가 된 뿐만 아니라 hello에 대 한 매개 변수 입력 저장소 계정과의 hello 저장소 계정 이름 hello에 대 한 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-168">Notice that not only was hello resource added, but also a parameter for hello type storage account, and a variable for hello name of hello storage account.</span></span>

![개요 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="57ed5-170">hello **storageType** 매개 변수는 미리 정의 된 허용된 유형 및 기본 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-170">hello **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="57ed5-171">이러한 값을 유지하거나 시나리오에 대해 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-171">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="57ed5-172">하지 않을 경우 모든 사용자 toodeploy는 **Premium_LRS** 이 서식 파일을 통해 저장소 계정 hello 허용 되는 형식에서에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-172">If you do not want anyone toodeploy a **Premium_LRS** storage account through this template, remove it from hello allowed types.</span></span> 

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

<span data-ttu-id="57ed5-173">Visual Studio intellisense toohelp 어떤 속성을 이해 하는 hello 템플릿을 편집 하는 경우에 사용할 수 또한 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-173">Visual Studio also provides intellisense toohelp you understand what properties are available when editing hello template.</span></span> <span data-ttu-id="57ed5-174">앱 서비스 계획에 대 한 tooedit hello 속성 toohello를 이동 하는 예를 들어 **HostingPlan** 리소스 hello에 대 한 값을 추가 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-174">For example, tooedit hello properties for your App Service plan, navigate toohello **HostingPlan** resource, and add a value for hello **properties**.</span></span> <span data-ttu-id="57ed5-175">Hello 사용 가능한 값을 표시 하 고 해당 값에 대 한 설명을 제공 하는 intellisense를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-175">Notice that intellisense shows hello available values and provides a description of that value.</span></span>

![intellisense 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="57ed5-177">설정할 수 있습니다 **작업자** too1 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-177">You can set **numberOfWorkers** too1.</span></span>

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a><span data-ttu-id="57ed5-178">리소스 그룹 프로젝트 tooAzure hello 배포</span><span class="sxs-lookup"><span data-stu-id="57ed5-178">Deploy hello Resource Group project tooAzure</span></span>
<span data-ttu-id="57ed5-179">사용자는 이제 준비 toodeploy 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-179">You are now ready toodeploy your project.</span></span> <span data-ttu-id="57ed5-180">Azure 리소스 그룹 프로젝트를 배포 하면 tooan Azure 리소스 그룹을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-180">When you deploy an Azure Resource Group project, you deploy it tooan Azure resource group.</span></span> <span data-ttu-id="57ed5-181">hello 리소스 그룹은 일반적인 수명 주기를 공유 하는 리소스의 논리적 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-181">hello resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="57ed5-182">Hello hello 배포 프로젝트 노드의 바로 가기 메뉴를 선택 **배포** > **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-182">On hello shortcut menu of hello deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![배포, 새 배포 메뉴 항목](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="57ed5-184">hello **tooResource 그룹 배포** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-184">hello **Deploy tooResource Group** dialog box appears.</span></span>
   
    ![TooResource 그룹 대화 상자 배포](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="57ed5-186">Hello에 **리소스 그룹** 드롭다운 상자에서 기존 리소스 그룹을 선택 하거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-186">In hello **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="57ed5-187">리소스 그룹 toocreate 열기 hello **리소스 그룹** 드롭다운 확인란을 선택한 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-187">toocreate a resource group, open hello **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![TooResource 그룹 대화 상자 배포](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="57ed5-189">hello **리소스 그룹 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-189">hello **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="57ed5-190">이름 및 위치, 사용자 그룹을 지정 하 고 hello 선택 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-190">Give your group a name and location, and select hello **Create** button.</span></span>
   
    ![리소스 그룹 만들기 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="57ed5-192">Hello를 선택 하 여 hello 배포에 대 한 hello 매개 변수를 편집 **매개 변수 편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-192">Edit hello parameters for hello deployment by selecting hello **Edit Parameters** button.</span></span>
   
    ![매개 변수 편집 단추](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="57ed5-194">Hello 빈 매개 변수 값을 제공 하 고 hello 선택 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-194">Provide values for hello empty parameters and select hello **Save** button.</span></span> <span data-ttu-id="57ed5-195">hello 빈 매개 변수는 **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, 및 **databaseName**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-195">hello empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="57ed5-196">**hostingPlanName** hello에 대 한 이름을 지정 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-196">**hostingPlanName** specifies a name for hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate.</span></span> 
   
    <span data-ttu-id="57ed5-197">**administratorLogin** hello SQL Server 관리자에 대 한 hello 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-197">**administratorLogin** specifies hello user name for hello SQL Server administrator.</span></span> <span data-ttu-id="57ed5-198">**sa** 또는 **admin**과 같은 일반 관리자 이름을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-198">Do not use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="57ed5-199">hello **administratorLoginPassword** SQL Server 관리자에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-199">hello **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="57ed5-200">hello **hello 매개 변수 파일에 일반 텍스트로 암호를 저장** 옵션 없는 보안; 이므로이 옵션을 선택 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="57ed5-200">hello **Save passwords as plain text in hello parameters file** option is not secure; therefore, do not select this option.</span></span> <span data-ttu-id="57ed5-201">Hello 암호를 일반 텍스트로 저장 되지 않으면 해야 tooprovide이이 암호 다시 배포 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="57ed5-201">Since hello password is not saved as plain text, you need tooprovide this password again during deployment.</span></span> 
   
    <span data-ttu-id="57ed5-202">**databaseName** 데이터베이스 toocreate hello에 대 한 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-202">**databaseName** specifies a name for hello database toocreate.</span></span> 
   
    ![매개 변수 편집 대화 상자](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="57ed5-204">Hello 선택 **배포** 단추 toodeploy hello 프로젝트 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-204">Choose hello **Deploy** button toodeploy hello project tooAzure.</span></span> <span data-ttu-id="57ed5-205">Hello Visual Studio 인스턴스 외부에서 PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-205">A PowerShell console opens outside of hello Visual Studio instance.</span></span> <span data-ttu-id="57ed5-206">메시지가 표시 되 면 hello PowerShell 콘솔에 hello SQL Server 관리자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-206">Enter hello SQL Server administrator password in hello PowerShell console when prompted.</span></span> <span data-ttu-id="57ed5-207">**PowerShell 콘솔 다른 항목 뒤 숨기 거 나 hello 작업 표시줄에 최소화 될 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="57ed5-207">**Your PowerShell console may be hidden behind other items or minimized in hello task bar.**</span></span> <span data-ttu-id="57ed5-208">이 콘솔 살펴보고 tooprovide hello 암호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-208">Look for this console and select it tooprovide hello password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="57ed5-209">Visual Studio tooinstall hello Azure PowerShell cmdlet을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-209">Visual Studio may ask you tooinstall hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="57ed5-210">Azure PowerShell hello 필요한 cmdlet toosuccessfully 리소스 그룹을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-210">You need hello Azure PowerShell cmdlets toosuccessfully deploy resource groups.</span></span> <span data-ttu-id="57ed5-211">메시지가 표시되면 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-211">If prompted, install them.</span></span>
   > 
   > 
6. <span data-ttu-id="57ed5-212">hello 배포는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-212">hello deployment may take a few minutes.</span></span> <span data-ttu-id="57ed5-213">Hello에 **출력** windows hello 배포의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-213">In hello **Output** windows, you see hello status of hello deployment.</span></span> <span data-ttu-id="57ed5-214">Hello 배포 완료 되 면 hello 마지막 메시지와 유사한 항목을 성공적으로 배포를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-214">When hello deployment has finished, hello last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. <span data-ttu-id="57ed5-215">브라우저를 열고 hello [Azure 포털](https://portal.azure.com/) tooyour 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-215">In a browser, open hello [Azure portal](https://portal.azure.com/) and sign in tooyour account.</span></span> <span data-ttu-id="57ed5-216">toosee hello 리소스 그룹을 선택 **리소스 그룹** 및 hello 리소스 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-216">toosee hello resource group, select **Resource groups** and hello resource group you deployed to.</span></span>
   
    ![그룹 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="57ed5-218">배포 된 hello 리소스를 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-218">You see all hello deployed resources.</span></span> <span data-ttu-id="57ed5-219">저장소 계정이 아닙니다 정확히 어떤 사용자가 해당 리소스를 추가할 때 지정한 hello의 해당 hello 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-219">Notice that hello name of hello storage account is not exactly what you specified when adding that resource.</span></span> <span data-ttu-id="57ed5-220">hello 저장소 계정은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-220">hello storage account must be unique.</span></span> <span data-ttu-id="57ed5-221">hello 템플릿을 자동으로 추가 하는 문자열 문자 toohello 이름의 있습니다 tooprovide 고유 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-221">hello template automatically adds a string of characters toohello name you provided tooprovide a unique name.</span></span> 
   
    ![리소스 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="57ed5-223">변경을 수행 하 고 프로젝트 tooredeploy를 원하는 경우 hello Azure 리소스 그룹 프로젝트 바로 가기 메뉴에서 hello 기존 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-223">If you make changes and want tooredeploy your project, choose hello existing resource group from hello shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="57ed5-224">Hello 바로 가기 메뉴에서 선택 **배포**, 배포 된 hello 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-224">On hello shortcut menu, choose **Deploy**, and then choose hello resource group you deployed.</span></span>
   
    ![배포된 Azure 리소스 그룹](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="57ed5-226">인프라를 사용하여 코드 배포</span><span class="sxs-lookup"><span data-stu-id="57ed5-226">Deploy code with your infrastructure</span></span>
<span data-ttu-id="57ed5-227">이 시점에서 응용 프로그램에 대 한 hello 인프라를 배포한 있지만 hello 프로젝트와 함께 배포 실제 코드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-227">At this point, you have deployed hello infrastructure for your app, but there is no actual code deployed with hello project.</span></span> <span data-ttu-id="57ed5-228">이 문서에서는 어떻게 toodeploy 웹 응용 프로그램 및 SQL 데이터베이스 테이블을 배포 하는 동안 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-228">This article shows how toodeploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="57ed5-229">웹 앱 대신 가상 컴퓨터를 배포 하는 경우 배포의 일부로 hello 시스템에서 일부 코드 toorun 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-229">If you are deploying a Virtual Machine instead of a web app, you want toorun some code on hello machine as part of deployment.</span></span> <span data-ttu-id="57ed5-230">웹 앱에 대 한 코드를 배포 하기 위한 프로세스 hello 또는 거의 가상 컴퓨터를 설정에 대 한 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-230">hello process for deploying code for a web app or for setting up a Virtual Machine is almost hello same.</span></span>

1. <span data-ttu-id="57ed5-231">프로젝트 tooyour Visual Studio 솔루션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-231">Add a project tooyour Visual Studio solution.</span></span> <span data-ttu-id="57ed5-232">Hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-232">Right-click hello solution, and select **Add** > **New Project**.</span></span>
   
    ![프로젝트 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="57ed5-234">**ASP.NET 웹 응용 프로그램**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-234">Add an **ASP.NET Web Application**.</span></span> 
   
    ![웹앱 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="57ed5-236">**MVC**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-236">Select **MVC**.</span></span>
   
    ![MVC 선택](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="57ed5-238">Visual Studio에서 웹 앱을 만드는 hello 솔루션의 두 프로젝트가 모두 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-238">After Visual Studio creates your web app, you see both projects in hello solution.</span></span>
   
    ![프로젝트 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="57ed5-240">이제, 리소스 그룹 프로젝트는 hello 새 프로젝트를 인식 하는지 toomake를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-240">Now, you need toomake sure your resource group project is aware of hello new project.</span></span> <span data-ttu-id="57ed5-241">Tooyour 리소스 그룹 프로젝트 (AzureResourceGroup1)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-241">Go back tooyour resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="57ed5-242">**참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-242">Right-click **References** and select **Add Reference**.</span></span>
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="57ed5-244">만든 hello 웹 응용 프로그램 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-244">Select hello web app project that you created.</span></span>
   
    ![참조 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="57ed5-246">참조를 추가 하 여 hello 웹 응용 프로그램 프로젝트 toohello 리소스 그룹 프로젝트를 연결 하 고 자동으로 세 가지 주요 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-246">By adding a reference, you link hello web app project toohello resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="57ed5-247">Hello에서 이러한 속성을 참조 **속성** hello 참조에 대 한 창.</span><span class="sxs-lookup"><span data-stu-id="57ed5-247">You see these properties in hello **Properties** window for hello reference.</span></span>
   
      ![참조 보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="57ed5-249">hello 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-249">hello properties are:</span></span>
   
   * <span data-ttu-id="57ed5-250">hello **추가 속성** hello 웹 배포 패키지를 스테이징 밀어넣어 toohello Azure 저장소 위치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-250">hello **Additional Properties** contains hello web deployment package staging location that is pushed toohello Azure Storage.</span></span> <span data-ttu-id="57ed5-251">참고 hello 폴더 (ExampleApp) 및 (package.zip) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-251">Note hello folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="57ed5-252">이 값이 필요 하면 tooknow 이러한 제공 하기 때문에 이러한 매개 변수를 배포할 때 hello 응용 프로그램으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-252">You need tooknow these values because you provide them as parameters when deploying hello app.</span></span> 
   * <span data-ttu-id="57ed5-253">hello **포함 파일 경로** hello 경로 hello 패키지를 만들 위치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-253">hello **Include File Path** contains hello path where hello package is created.</span></span> <span data-ttu-id="57ed5-254">hello **포함 대상** 배포를 실행 하는 hello 명령이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-254">hello **Include Targets** contains hello command that deployment executes.</span></span> 
   * <span data-ttu-id="57ed5-255">기본값을 hello **빌드합니다. 패키지** 배포 toobuild hello를 사용 하 고 웹 배포 패키지 (package.zip)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-255">hello default value of **Build;Package** enables hello deployment toobuild and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="57ed5-256">Hello 배포 hello 속성 toocreate hello 패키지에서 필요한 정보를 hello 가져옵니다으로 게시 프로필을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-256">You do not need a publish profile as hello deployment gets hello necessary information from hello properties toocreate hello package.</span></span>
7. <span data-ttu-id="57ed5-257">TooWebSiteSQLDatabase.json 돌아가서 리소스 toohello 템플릿을 추가 하십시오.</span><span class="sxs-lookup"><span data-stu-id="57ed5-257">Go back tooWebSiteSQLDatabase.json and add a resource toohello template.</span></span>
   
    ![리소스 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="57ed5-259">이번에는 **Web Apps에 대한 웹 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-259">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="57ed5-261">리소스 그룹 프로젝트 toohello 리소스 그룹을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-261">Redeploy your resource group project toohello resource group.</span></span> <span data-ttu-id="57ed5-262">이번에는 몇 가지 새로운 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-262">This time there are some new parameters.</span></span> <span data-ttu-id="57ed5-263">Tooprovide 값에 대 한 불필요 **_artifactsLocation** 또는 **_artifactsLocationSasToken** Visual Studio 해당 값을 자동으로 생성 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-263">You do not need tooprovide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="57ed5-264">그러나 tooset hello 폴더 및 hello 배포 패키지를 포함 하는 파일 이름 toohello 경로 있을 (으로 표시 **ExampleAppPackageFolder** 및 **ExampleAppPackageFileName** hello 이미지 뒤에 ).</span><span class="sxs-lookup"><span data-stu-id="57ed5-264">However, you have tooset hello folder and file name toohello path that contains hello deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in hello following image).</span></span> <span data-ttu-id="57ed5-265">이전에 본 hello 값 hello 참조 속성을 제공 (**ExampleApp** 및 **package.zip**).</span><span class="sxs-lookup"><span data-stu-id="57ed5-265">Provide hello values you saw earlier in hello reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![웹 배포 추가](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="57ed5-267">Hello에 대 한 **아티팩트 저장소 계정**, 선택 hello 하나이 리소스 그룹을 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-267">For hello **Artifact storage account**, select hello one deployed with this resource group.</span></span>
10. <span data-ttu-id="57ed5-268">Hello 배포가 완료 된 후 hello 포털에서 웹 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-268">After hello deployment has finished, select your web app in hello portal.</span></span> <span data-ttu-id="57ed5-269">Hello URL toobrowse toohello 사이트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-269">Select hello URL toobrowse toohello site.</span></span>
    
     ![사이트 찾아보기](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="57ed5-271">Hello 기본 ASP.NET 앱을 정상적으로 배포 된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-271">Notice that you have successfully deployed hello default ASP.NET app.</span></span>
    
     ![배포된 앱 표시](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a><span data-ttu-id="57ed5-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57ed5-273">Next steps</span></span>
* <span data-ttu-id="57ed5-274">toolearn hello 포털을 통해 리소스를 관리 하는 방법에 대 한 참조 [사용 하 여 Azure 리소스를 Azure 포털 toomanage hello](resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-274">toolearn about managing your resources through hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="57ed5-275">서식 파일에 대해 자세히 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57ed5-275">toolearn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

