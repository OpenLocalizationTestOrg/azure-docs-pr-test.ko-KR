---
title: "Azure Logic Apps용 배포 템플릿 만들기 | Microsoft Docs"
description: "논리 앱 배포 및 릴리스 관리용 Azure Resource Manager 템플릿 만들기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9cfbb294010d48deaf4b4c78c6a6bcd59a387d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a><span data-ttu-id="5a444-103">논리 앱 배포 및 릴리스 관리용 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="5a444-103">Create templates for logic apps deployment and release management</span></span>

<span data-ttu-id="5a444-104">논리 앱을 만든 후 Azure Resource Manager 템플릿으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-104">After a logic app has been created, you might want to create it as an Azure Resource Manager template.</span></span>
<span data-ttu-id="5a444-105">이 방식을 사용하면 필요에 따라 어떤 환경이나 리소스 그룹에도 논리 앱을 손쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-105">This way, you can easily deploy the logic app to any environment or resource group where you might need it.</span></span>
<span data-ttu-id="5a444-106">Resource Manager 템플릿에 대한 자세한 내용은 [Azure Resource Manager 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5a444-106">For more about Resource Manager templates, see [authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) and [deploying resources by using Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="logic-app-deployment-template"></a><span data-ttu-id="5a444-107">논리 앱 배포 템플릿</span><span class="sxs-lookup"><span data-stu-id="5a444-107">Logic app deployment template</span></span>

<span data-ttu-id="5a444-108">논리 앱은 세 가지 기본 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-108">A logic app has three basic components:</span></span>

* <span data-ttu-id="5a444-109">**논리 앱 리소스**: 가격 책정 정책, 위치, 워크플로 정의 등의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-109">**Logic app resource**: Contains information about things like pricing plan, location, and the workflow definition.</span></span>
* <span data-ttu-id="5a444-110">**워크플로 정의**: 논리 앱 워크플로 단계 및 Logic Apps 엔진이 워크플로를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-110">**Workflow definition**: Describes your logic app's workflow steps and how the Logic Apps engine should execute the workflow.</span></span>
<span data-ttu-id="5a444-111">논리 앱의 **코드 보기** 창에서 이 정의를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-111">You can view this definition in your logic app's **Code View** window.</span></span>
<span data-ttu-id="5a444-112">논리 앱 리소스의 `definition` 속성에서 이 정의를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-112">In the logic app resource, you can find this definition in the `definition` property.</span></span>
* <span data-ttu-id="5a444-113">**연결**: 연결 문자열 및 액세스 토큰과 같은 커넥터 연결과 관련된 메타데이터를 안전하게 보관하는 별도의 리소스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-113">**Connections**: Refers to separate resources that securely store metadata about any connector connections, such as a connection string and an access token.</span></span>
<span data-ttu-id="5a444-114">논리 앱 리소스에서 논리 앱은 `parameters` 섹션의 이러한 리소스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-114">In the logic app resource, your logic app references these resources in the `parameters` section.</span></span>

<span data-ttu-id="5a444-115">[Azure Resource Explorer](http://resources.azure.com)와 같은 도구를 사용하여 기존 Logic Apps에 대한 이런 모든 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-115">You can view all these pieces of existing logic apps by using a tool like [Azure Resource Explorer](http://resources.azure.com).</span></span>

<span data-ttu-id="5a444-116">리소스 그룹 배포에 사용할 수 있는 논리 앱 템플릿을 만들려면 리소스를 정의하고 필요에 따라 매개 변수화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-116">To make a template for a logic app to use with resource group deployments, you must define the resources and parameterize as needed.</span></span>
<span data-ttu-id="5a444-117">예를 들어, 개발, 테스트 및 프로덕션 환경에 배포하는 경우 각 환경에서 SQL Database에 대해 다른 연결 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-117">For example, if you're deploying to a development, test, and production environment, you likely want to use different connection strings to a SQL database in each environment.</span></span>
<span data-ttu-id="5a444-118">또는, 다른 구독이나 리소스 그룹 내에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-118">Or, you might want to deploy within different subscriptions or resource groups.</span></span>  

## <a name="create-a-logic-app-deployment-template"></a><span data-ttu-id="5a444-119">논리 앱 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="5a444-119">Create a logic app deployment template</span></span>

<span data-ttu-id="5a444-120">유효한 논리 앱 배포 템플릿을 생성하는 가장 쉬운 방법은 [Logic Apps용 Visual Studio Tools](logic-apps-deploy-from-vs.md)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-120">The easiest way to have a valid logic app deployment template is to use the [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md).</span></span>
<span data-ttu-id="5a444-121">Visual Studio Tools는 구독 또는 위치에서 사용할 수 있는 올바른 배포 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-121">The Visual Studio tools generate a valid deployment template that can be used across any subscription or location.</span></span>

<span data-ttu-id="5a444-122">논리 앱 배포 템플릿을 만들 때 도움을 받을 수 있는 다른 몇 가지 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-122">A few other tools can assist you as you create a logic app deployment template.</span></span>
<span data-ttu-id="5a444-123">템플릿은 손으로 작성할 수 있습니다. 즉, 여기서 논의했던 리소스를 사용하여 필요에 따라 매개 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-123">You can author by hand, that is, by using the resources already discussed here to create parameters as needed.</span></span>
<span data-ttu-id="5a444-124">[논리 앱 템플릿 작성기](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell 모듈을 활용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-124">Another option is to use a [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell module.</span></span> <span data-ttu-id="5a444-125">이 오픈 소스 모듈은 논리 앱과 논리 앱에서 사용하는 모든 연결을 평가하고, 배포에 필요한 매개 변수와 함께 템플릿 리소스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-125">This open-source module first evaluates the logic app and any connections that it is using, and then generates template resources with the necessary parameters for deployment.</span></span>
<span data-ttu-id="5a444-126">예를 들어, Azure Service Bus 큐에서 메시지를 수신하고 Azure SQL Database에 데이터를 추가하는 논리 앱이 있는 경우 이 도구는 모든 오케스트레이션 논리를 보존하고 SQL 및 Service Bus 연결 문자열을 매개 변수화하여 배포 시 설정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-126">For example, if you have a logic app that receives a message from an Azure Service Bus queue and adds data to an Azure SQL database, the tool preserves all the orchestration logic and parameterizes the SQL and Service Bus connection strings so that they can be set at deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="5a444-127">연결은 논리 앱과 동일한 리소스 그룹 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-127">Connections must be within the same resource group as the logic app.</span></span>
>
>

### <a name="install-the-logic-app-template-powershell-module"></a><span data-ttu-id="5a444-128">논리 앱 템플릿 PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5a444-128">Install the logic app template PowerShell module</span></span>
<span data-ttu-id="5a444-129">가장 쉬운 설치 방법은 `Install-Module -Name LogicAppTemplate` 명령을 사용하여 [PowerShell 갤러리](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1)를 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-129">The easiest way to install the module is via the [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), by using the command `Install-Module -Name LogicAppTemplate`.</span></span>  

<span data-ttu-id="5a444-130">또한, PowerShell 모듈을 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-130">You also can install the PowerShell module manually:</span></span>

1. <span data-ttu-id="5a444-131">[논리 앱 템플릿 작성기](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)의 최신 릴리스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-131">Download the latest release of the [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).</span></span>  
2. <span data-ttu-id="5a444-132">PowerShell 모듈 폴더에 폴더를 추출합니다(일반적으로 `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span><span class="sxs-lookup"><span data-stu-id="5a444-132">Extract the folder in your PowerShell module folder (usually `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span></span>

<span data-ttu-id="5a444-133">모듈에서 모든 테넌트 및 구독 액세스 토큰에 대한 작업을 하려면 [ARMClient](https://github.com/projectkudu/ARMClient) 명령줄 도구로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-133">For the module to work with any tenant and subscription access token, we recommend that you use it with the [ARMClient](https://github.com/projectkudu/ARMClient) command-line tool.</span></span>  <span data-ttu-id="5a444-134">이 [블로그 게시물](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html)은 ARMClient에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-134">This [blog post](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) discusses ARMClient in more detail.</span></span>

### <a name="generate-a-logic-app-template-by-using-powershell"></a><span data-ttu-id="5a444-135">PowerShell을 사용하여 논리 앱 템플릿 생성</span><span class="sxs-lookup"><span data-stu-id="5a444-135">Generate a logic app template by using PowerShell</span></span>
<span data-ttu-id="5a444-136">PowerShell을 설치한 후 다음 명령을 사용하여 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-136">After PowerShell is installed, you can generate a template by using the following command:</span></span>

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

<span data-ttu-id="5a444-137">`$SubscriptionId` 은(는) Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-137">`$SubscriptionId` is the Azure subscription ID.</span></span> <span data-ttu-id="5a444-138">이 줄은 ARMClient를 통해 액세스 토큰을 가져온 다음 PowerShell 스크립트로 실행시키고, JSON 파일로 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-138">This line first gets an access token via ARMClient, then pipes it through to the PowerShell script, and then creates the template in a JSON file.</span></span>

## <a name="add-parameters-to-a-logic-app-template"></a><span data-ttu-id="5a444-139">논리 앱 템플릿에 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="5a444-139">Add parameters to a logic app template</span></span>
<span data-ttu-id="5a444-140">논리 앱 템플릿을 만든 다음 필요한 매개 변수를 추가하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-140">After you create your logic app template, you can continue to add or modify parameters that you might need.</span></span> <span data-ttu-id="5a444-141">예를 들어 정의에 단일 배포로 배포할 계획인 중첩된 워크플로 또는 Azure Function에 대한 리소스 ID가 포함된 경우, 템플릿에 추가 리소스를 추가하고 필요에 따라 ID를 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-141">For example, if your definition includes a resource ID to an Azure function or nested workflow that you plan to deploy in a single deployment, you can add more resources to your template and parameterize IDs as needed.</span></span> <span data-ttu-id="5a444-142">각 리소스 그룹과 함께 배포할 예정인 Swagger 끝점 또는 사용자 지정 API에 대한 참조도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-142">The same applies to any references to custom APIs or Swagger endpoints you expect to deploy with each resource group.</span></span>

## <a name="deploy-a-logic-app-template"></a><span data-ttu-id="5a444-143">논리 앱 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="5a444-143">Deploy a logic app template</span></span>

<span data-ttu-id="5a444-144">템플릿을 만든 후에는 PowerShell, REST API, [Visual Studio Team Services Release Management](#team-services), Azure Portal을 통한 템플릿 배포와 같은 여러 도구를 사용하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-144">You can deploy your template by using any tools like PowerShell, REST API, [Visual Studio Team Services Release Management](#team-services), and template deployment through the Azure portal.</span></span>
<span data-ttu-id="5a444-145">또한, 매개 변수 값을 저장할 [매개 변수 파일](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-145">Also, to store the values for parameters, we recommend that you create a [parameter file](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span></span>
<span data-ttu-id="5a444-146">[Azure Resource Manager 템플릿 및 PowerShell로 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md) 또는 [Azure Resource Manager 템플릿 및 Azure Portal로 리소스 배포](../azure-resource-manager/resource-group-template-deploy-portal.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-146">Learn how to [deploy resources with Azure Resource Manager templates and PowerShell](../azure-resource-manager/resource-group-template-deploy.md) or [deploy resources with Azure Resource Manager templates and the Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

### <a name="authorize-oauth-connections"></a><span data-ttu-id="5a444-147">OAuth 연결 권한 부여</span><span class="sxs-lookup"><span data-stu-id="5a444-147">Authorize OAuth connections</span></span>

<span data-ttu-id="5a444-148">배포 후 논리 앱은 유효한 매개 변수와 함께 종단 간에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-148">After deployment, the logic app works end-to-end with valid parameters.</span></span>
<span data-ttu-id="5a444-149">그러나 OAuth 연결이 유효한 액세스 토큰을 생성하도록 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-149">However, you must still authorize OAuth connections to generate a valid access token.</span></span>
<span data-ttu-id="5a444-150">OAuth 연결에 권한을 부여하려면 Logic Apps Designer에서 논리 앱을 열고 이러한 연결에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-150">To authorize OAuth connections, open the logic app in the Logic Apps Designer, and authorize these connections.</span></span> <span data-ttu-id="5a444-151">또는, 자동화 배포의 경우 스크립트를 사용하여 각 OAuth 연결을 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-151">Or for automated deployment, you can use a script to consent to each OAuth connection.</span></span>
<span data-ttu-id="5a444-152">GitHub에 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 프로젝트라는 예시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-152">There's an example script on GitHub under the [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) project.</span></span>

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a><span data-ttu-id="5a444-153">Visual Studio Team Services 릴리스 관리</span><span class="sxs-lookup"><span data-stu-id="5a444-153">Visual Studio Team Services Release Management</span></span>

<span data-ttu-id="5a444-154">환경을 배포 및 관리하는 일반적인 시나리오는 논리 앱 배포 템플릿과 함께 Visual Studio Team Services의 릴리스 관리 등의 도구를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-154">A common scenario for deploying and managing an environment is to use a tool like Release Management in Visual Studio Team Services, with a logic app deployment template.</span></span> <span data-ttu-id="5a444-155">Visual Studio Team Services에는 모든 빌드 또는 릴리스 파이프라인에 추가할 수 있는 [Azure 리소스 그룹 배포](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-155">Visual Studio Team Services includes a [Deploy Azure Resource Group](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) task that you can add to any build or release pipeline.</span></span> <span data-ttu-id="5a444-156">배포 권한 부여를 위해서는 [서비스 주체](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) 가 필요하며 그 다음 릴리스 정의를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-156">You need to have a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) for authorization to deploy, and then you can generate the release definition.</span></span>

1. <span data-ttu-id="5a444-157">릴리스 관리에서 빈 정의를 생성할 수 있도록 **비어 있음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-157">In Release Management, select **Empty** so that you create an empty definition.</span></span>

    ![빈 정의 만들기][1]

2. <span data-ttu-id="5a444-159">수동으로 또는 빌드 프로세스의 일부로 생성된 논리 앱 템플릿을 포함할 가능성이 높은 필요한 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-159">Choose any resources you need for this, most likely including the logic app template that is generated manually or as part of the build process.</span></span>
3. <span data-ttu-id="5a444-160">**Azure 리소스 그룹 배포** 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-160">Add an **Azure Resource Group Deployment** task.</span></span>
4. <span data-ttu-id="5a444-161">[서비스 주체](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)로 구성하고 템플릿 및 템플릿 매개 변수 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-161">Configure with a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), and reference the Template and Template Parameters files.</span></span>
5. <span data-ttu-id="5a444-162">릴리스 프로세스에서 다른 환경, 자동화된 테스트 또는 승인자에 대한 단계를 필요에 따라 계속 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a444-162">Continue to build out steps in the release process for any other environment, automated test, or approvers as needed.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
