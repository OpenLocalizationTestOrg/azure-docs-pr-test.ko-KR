---
title: "Azure 논리 앱에 대 한 배포 템플릿을 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a><span data-ttu-id="386d9-103">논리 앱 배포 및 릴리스 관리용 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="386d9-103">Create templates for logic apps deployment and release management</span></span>

<span data-ttu-id="386d9-104">Toocreate 경우가 논리 앱을 만든 후 Azure 리소스 관리자 템플릿으로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-104">After a logic app has been created, you might want toocreate it as an Azure Resource Manager template.</span></span>
<span data-ttu-id="386d9-105">이러한 방식으로 할 수 있는 리소스 그룹 또는 hello 논리 앱 tooany 환경을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-105">This way, you can easily deploy hello logic app tooany environment or resource group where you might need it.</span></span>
<span data-ttu-id="386d9-106">Resource Manager 템플릿에 대한 자세한 내용은 [Azure Resource Manager 작성](../azure-resource-manager/resource-group-authoring-templates.md) 및 [Azure Resource Manager 템플릿을 사용하여 리소스 배포](../azure-resource-manager/resource-group-template-deploy.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="386d9-106">For more about Resource Manager templates, see [authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) and [deploying resources by using Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="logic-app-deployment-template"></a><span data-ttu-id="386d9-107">논리 앱 배포 템플릿</span><span class="sxs-lookup"><span data-stu-id="386d9-107">Logic app deployment template</span></span>

<span data-ttu-id="386d9-108">논리 앱은 세 가지 기본 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-108">A logic app has three basic components:</span></span>

* <span data-ttu-id="386d9-109">**논리 앱 리소스**: 계획, 위치 및 hello 워크플로 정의 가격 등의 작업에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-109">**Logic app resource**: Contains information about things like pricing plan, location, and hello workflow definition.</span></span>
* <span data-ttu-id="386d9-110">**워크플로 정의**: 논리 앱 워크플로 단계 및 hello 논리 앱 엔진 해야 hello 워크플로 실행 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-110">**Workflow definition**: Describes your logic app's workflow steps and how hello Logic Apps engine should execute hello workflow.</span></span>
<span data-ttu-id="386d9-111">논리 앱의 **코드 보기** 창에서 이 정의를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-111">You can view this definition in your logic app's **Code View** window.</span></span>
<span data-ttu-id="386d9-112">Hello 논리 앱 리소스를 찾을 수 있습니다이 정의 hello에 `definition` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-112">In hello logic app resource, you can find this definition in hello `definition` property.</span></span>
* <span data-ttu-id="386d9-113">**연결**: 연결 문자열 및 액세스 토큰 등의 모든 커넥터 연결에 대 한 메타 데이터를 안전 하 게 저장 tooseparate 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-113">**Connections**: Refers tooseparate resources that securely store metadata about any connector connections, such as a connection string and an access token.</span></span>
<span data-ttu-id="386d9-114">논리 앱 hello 논리 앱 리소스에서 hello에 이러한 리소스를 참조 `parameters` 섹션.</span><span class="sxs-lookup"><span data-stu-id="386d9-114">In hello logic app resource, your logic app references these resources in hello `parameters` section.</span></span>

<span data-ttu-id="386d9-115">[Azure Resource Explorer](http://resources.azure.com)와 같은 도구를 사용하여 기존 Logic Apps에 대한 이런 모든 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-115">You can view all these pieces of existing logic apps by using a tool like [Azure Resource Explorer](http://resources.azure.com).</span></span>

<span data-ttu-id="386d9-116">템플릿 toomake 논리 앱 toouse 리소스 그룹 배포에 대 한 hello 리소스 정의 및 필요에 따라 매개 변수화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-116">toomake a template for a logic app toouse with resource group deployments, you must define hello resources and parameterize as needed.</span></span>
<span data-ttu-id="386d9-117">예를 들어 tooa 개발, 테스트 및 프로덕션 환경을 배포 하는 경우 사용할 수도 있습니다 각 환경에 toouse 다른 연결 문자열 tooa SQL 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="386d9-117">For example, if you're deploying tooa development, test, and production environment, you likely want toouse different connection strings tooa SQL database in each environment.</span></span>
<span data-ttu-id="386d9-118">또는 서로 다른 구독 또는 리소스 그룹 내에서 toodeploy 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-118">Or, you might want toodeploy within different subscriptions or resource groups.</span></span>  

## <a name="create-a-logic-app-deployment-template"></a><span data-ttu-id="386d9-119">논리 앱 배포 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="386d9-119">Create a logic app deployment template</span></span>

<span data-ttu-id="386d9-120">hello 가장 쉬운 방법은 toohave 유효한 논리 앱 배포 템플릿에 toouse는 [논리 앱 용 도구 Visual Studio](logic-apps-deploy-from-vs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-120">hello easiest way toohave a valid logic app deployment template is toouse the [Visual Studio Tools for Logic Apps](logic-apps-deploy-from-vs.md).</span></span>
<span data-ttu-id="386d9-121">Visual Studio tools hello 위치 또는 구독에서 사용할 수 있는 올바른 배포 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-121">hello Visual Studio tools generate a valid deployment template that can be used across any subscription or location.</span></span>

<span data-ttu-id="386d9-122">논리 앱 배포 템플릿을 만들 때 도움을 받을 수 있는 다른 몇 가지 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-122">A few other tools can assist you as you create a logic app deployment template.</span></span>
<span data-ttu-id="386d9-123">직접 작성할 수 있습니다, 즉, hello를 사용 하 여 리소스 이미 여기에 설명 toocreate 매개 변수가 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-123">You can author by hand, that is, by using hello resources already discussed here toocreate parameters as needed.</span></span>
<span data-ttu-id="386d9-124">두 번째 방법은 toouse는 [논리 앱 템플릿 작성자](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-124">Another option is toouse a [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator) PowerShell module.</span></span> <span data-ttu-id="386d9-125">이 오픈 소스 모듈에는 먼저 hello 논리 앱 및 모든 연결을 사용 하는 다음 배포에 대 한 hello 필요한 매개 변수를 사용 하 여 템플릿 리소스를 생성 하 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-125">This open-source module first evaluates hello logic app and any connections that it is using, and then generates template resources with hello necessary parameters for deployment.</span></span>
<span data-ttu-id="386d9-126">예를 들어 Azure 서비스 버스 큐에서 메시지를 받은 데이터 tooan Azure SQL 데이터베이스를 추가 하는 논리 앱이 있는 경우 hello 도구 모든 hello 오케스트레이션 논리를 유지 하 고 설정할 수 있도록 SQL hello 및 서비스 버스 연결 문자열을 매개 변수화 에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-126">For example, if you have a logic app that receives a message from an Azure Service Bus queue and adds data tooan Azure SQL database, hello tool preserves all hello orchestration logic and parameterizes hello SQL and Service Bus connection strings so that they can be set at deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="386d9-127">연결 hello 내에 있어야 합니다. 논리 앱 hello와 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-127">Connections must be within hello same resource group as hello logic app.</span></span>
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a><span data-ttu-id="386d9-128">Hello 논리 앱 템플릿을 PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="386d9-128">Install hello logic app template PowerShell module</span></span>
<span data-ttu-id="386d9-129">hello를 통해 hello 가장 쉬운 방법은 tooinstall hello 모듈은 [PowerShell 갤러리](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), hello 명령을 사용 하 여 `Install-Module -Name LogicAppTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-129">hello easiest way tooinstall hello module is via hello [PowerShell Gallery](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), by using hello command `Install-Module -Name LogicAppTemplate`.</span></span>  

<span data-ttu-id="386d9-130">또한 수동으로 설치할 수 있습니다 hello PowerShell 모듈:</span><span class="sxs-lookup"><span data-stu-id="386d9-130">You also can install hello PowerShell module manually:</span></span>

1. <span data-ttu-id="386d9-131">Hello 최신 릴리스의 hello 다운로드 [논리 앱 템플릿 작성자](https://github.com/jeffhollan/LogicAppTemplateCreator/releases)합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-131">Download hello latest release of hello [logic app template creator](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).</span></span>  
2. <span data-ttu-id="386d9-132">PowerShell 모듈 폴더에 있는 hello 폴더 (일반적으로 `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span><span class="sxs-lookup"><span data-stu-id="386d9-132">Extract hello folder in your PowerShell module folder (usually `%UserProfile%\Documents\WindowsPowerShell\Modules`).</span></span>

<span data-ttu-id="386d9-133">모든 테 넌 트 및 구독 액세스 권한이 있는 모듈 toowork hello에 대 한 hello로 사용할 토큰, 권장 [ARMClient](https://github.com/projectkudu/ARMClient) 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-133">For hello module toowork with any tenant and subscription access token, we recommend that you use it with hello [ARMClient](https://github.com/projectkudu/ARMClient) command-line tool.</span></span>  <span data-ttu-id="386d9-134">이 [블로그 게시물](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html)은 ARMClient에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-134">This [blog post](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) discusses ARMClient in more detail.</span></span>

### <a name="generate-a-logic-app-template-by-using-powershell"></a><span data-ttu-id="386d9-135">PowerShell을 사용하여 논리 앱 템플릿 생성</span><span class="sxs-lookup"><span data-stu-id="386d9-135">Generate a logic app template by using PowerShell</span></span>
<span data-ttu-id="386d9-136">PowerShell을 설치한 후 다음 명령을 hello를 사용 하 여 서식 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-136">After PowerShell is installed, you can generate a template by using hello following command:</span></span>

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

<span data-ttu-id="386d9-137">`$SubscriptionId`hello Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-137">`$SubscriptionId` is hello Azure subscription ID.</span></span> <span data-ttu-id="386d9-138">이 줄 먼저 액세스 토큰 ARMClient를 통해 다음 toohello PowerShell 스크립트를 통해 파이프을 가져오고 JSON 파일에 hello 서식 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-138">This line first gets an access token via ARMClient, then pipes it through toohello PowerShell script, and then creates hello template in a JSON file.</span></span>

## <a name="add-parameters-tooa-logic-app-template"></a><span data-ttu-id="386d9-139">Tooa 논리 앱 템플릿은 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-139">Add parameters tooa logic app template</span></span>
<span data-ttu-id="386d9-140">논리 앱 템플릿을 만든 후 tooadd 계속 하거나 필요할 수 있는 매개 변수를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-140">After you create your logic app template, you can continue tooadd or modify parameters that you might need.</span></span> <span data-ttu-id="386d9-141">예를 들어 정의 리소스 ID tooan Azure 함수 또는 toodeploy를 단일 배포를 계획 하는 중첩 된 워크플로 포함 하는 경우 더 많은 리소스 tooyour 서식 파일을 추가 및 필요에 따라 Id를 매개 변수화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-141">For example, if your definition includes a resource ID tooan Azure function or nested workflow that you plan toodeploy in a single deployment, you can add more resources tooyour template and parameterize IDs as needed.</span></span> <span data-ttu-id="386d9-142">hello 마찬가지 tooany 참조 toocustom Api 또는 Swagger 끝점 toodeploy 각 리소스 그룹으로 예상입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-142">hello same applies tooany references toocustom APIs or Swagger endpoints you expect toodeploy with each resource group.</span></span>

## <a name="deploy-a-logic-app-template"></a><span data-ttu-id="386d9-143">논리 앱 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="386d9-143">Deploy a logic app template</span></span>

<span data-ttu-id="386d9-144">PowerShell, REST API와 같은 도구를 사용 하 여 서식 파일을 배포할 수 있습니다 [Visual Studio Team Services Release Management](#team-services), 및 hello Azure 포털을 통해 템플릿 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-144">You can deploy your template by using any tools like PowerShell, REST API, [Visual Studio Team Services Release Management](#team-services), and template deployment through hello Azure portal.</span></span>
<span data-ttu-id="386d9-145">또한 toostore hello 매개 변수 값을, 좋습니다 만드는 [매개 변수 파일](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-145">Also, toostore hello values for parameters, we recommend that you create a [parameter file](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).</span></span>
<span data-ttu-id="386d9-146">너무 방법에 대해 알아봅니다[Azure 리소스 관리자 템플릿 및 PowerShell을 사용 하 여 리소스를 배포](../azure-resource-manager/resource-group-template-deploy.md) 또는 [Azure 리소스 관리자 템플릿 사용 하 여 리소스를 배포 하 고 Azure 포털 hello](../azure-resource-manager/resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-146">Learn how too[deploy resources with Azure Resource Manager templates and PowerShell](../azure-resource-manager/resource-group-template-deploy.md) or [deploy resources with Azure Resource Manager templates and hello Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

### <a name="authorize-oauth-connections"></a><span data-ttu-id="386d9-147">OAuth 연결 권한 부여</span><span class="sxs-lookup"><span data-stu-id="386d9-147">Authorize OAuth connections</span></span>

<span data-ttu-id="386d9-148">배포 후 hello 논리 앱 종단 유효한 매개 변수와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-148">After deployment, hello logic app works end-to-end with valid parameters.</span></span>
<span data-ttu-id="386d9-149">그러나 OAuth 연결 toogenerate 유효한 액세스 토큰이 아직 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-149">However, you must still authorize OAuth connections toogenerate a valid access token.</span></span>
<span data-ttu-id="386d9-150">tooauthorize OAuth 연결 hello 논리 앱을 열고 hello 논리 앱 디자이너에서에서 이러한 연결 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-150">tooauthorize OAuth connections, open hello logic app in hello Logic Apps Designer, and authorize these connections.</span></span> <span data-ttu-id="386d9-151">또는 자동화 된 배포 스크립트 tooconsent tooeach OAuth 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-151">Or for automated deployment, you can use a script tooconsent tooeach OAuth connection.</span></span>
<span data-ttu-id="386d9-152">GitHub에 [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) 프로젝트라는 예시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-152">There's an example script on GitHub under the [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) project.</span></span>

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a><span data-ttu-id="386d9-153">Visual Studio Team Services 릴리스 관리</span><span class="sxs-lookup"><span data-stu-id="386d9-153">Visual Studio Team Services Release Management</span></span>

<span data-ttu-id="386d9-154">배포 및 관리 환경에 대 한 일반적인 시나리오에는 toouse 논리 앱 배포 템플릿 사용 하 여 Visual Studio Team Services에서 Release Management와 같은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-154">A common scenario for deploying and managing an environment is toouse a tool like Release Management in Visual Studio Team Services, with a logic app deployment template.</span></span> <span data-ttu-id="386d9-155">Visual Studio Team Services에 포함 되어는 [Azure 리소스 그룹 배포](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) 작업 tooany 빌드 추가할 수 또는 파이프라인을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-155">Visual Studio Team Services includes a [Deploy Azure Resource Group](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) task that you can add tooany build or release pipeline.</span></span> <span data-ttu-id="386d9-156">Toohave 필요는 [서비스 사용자](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) 권한 부여 toodeploy, 한 다음 생성할 수 있으며, hello 릴리스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-156">You need toohave a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) for authorization toodeploy, and then you can generate hello release definition.</span></span>

1. <span data-ttu-id="386d9-157">릴리스 관리에서 빈 정의를 생성할 수 있도록 **비어 있음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-157">In Release Management, select **Empty** so that you create an empty definition.</span></span>

    ![빈 정의 만들기][1]

2. <span data-ttu-id="386d9-159">빌드 프로세스에이 가장 가능성이 높은 포함 하 여 hello 논리 앱 템플릿은 수동으로 또는 hello의 일부로 생성 되는 필요한 모든 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-159">Choose any resources you need for this, most likely including hello logic app template that is generated manually or as part of hello build process.</span></span>
3. <span data-ttu-id="386d9-160">**Azure 리소스 그룹 배포** 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-160">Add an **Azure Resource Group Deployment** task.</span></span>
4. <span data-ttu-id="386d9-161">사용 하 여 구성는 [서비스 사용자](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), hello 템플릿과 템플릿 매개 변수 파일을 참조 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-161">Configure with a [service principal](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/), and reference hello Template and Template Parameters files.</span></span>
5. <span data-ttu-id="386d9-162">다른 환경, 자동화 된 테스트 또는 필요에 따라 승인자에 대 한 hello 릴리스 프로세스에서 toobuild 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="386d9-162">Continue toobuild out steps in hello release process for any other environment, automated test, or approvers as needed.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
