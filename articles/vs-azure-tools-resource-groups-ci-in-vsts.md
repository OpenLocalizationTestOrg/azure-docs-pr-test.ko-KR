---
title: "Azure 리소스 그룹 프로젝트를 사용하여 VS Team Services에서 연속 통합 | Microsoft Docs"
description: "Visual Studio에서 Azure 리소스 그룹 배포 프로젝트를 사용하여 Visual Studio Team Services에서의 연속 통합을 설정하는 방법을 설명합니다."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: e7d98ca3fa281a136595c37ed9b7e71de0cf7bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a><span data-ttu-id="2d17e-103">Azure 리소스 그룹 배포 프로젝트를 사용하여 Visual Studio Team Services에서 연속 통합</span><span class="sxs-lookup"><span data-stu-id="2d17e-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span></span>
<span data-ttu-id="2d17e-104">Azure 템플릿을 배포하려면 빌드, 테스트, Azure에 복사("준비"라고도 함), 템플릿 배포 등 다양한 단계에서 태스크를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-104">To deploy an Azure template, you perform tasks in various stages: Build, Test, Copy to Azure (also called "Staging"), and Deploy Template.</span></span> <span data-ttu-id="2d17e-105">VS Team Services(Visual Studio Team Services)에 템플릿을 배포하는 방법에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-105">There are two different ways to deploy templates to Visual Studio Team Services (VS Team Services).</span></span> <span data-ttu-id="2d17e-106">두 방법 모두 결과는 같으므로 사용자의 워크플로에 가장 적합한 방법을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-106">Both methods provide the same results, so choose the one that best fits your workflow.</span></span>

1. <span data-ttu-id="2d17e-107">Azure 리소스 그룹 배포 프로젝트(Deploy-AzureResourceGroup.ps1)에 포함된 PowerShell 스크립트를 실행하는 한 단계를 빌드 정의에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-107">Add a single step to your build definition that runs the PowerShell script that’s included in the Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span></span> <span data-ttu-id="2d17e-108">이 스크립트는 아티팩트를 복사한 뒤 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-108">The script copies artifacts and then deploys the template.</span></span>
2. <span data-ttu-id="2d17e-109">각각 단계 작업을 수행하는 여러 VS Team Services 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-109">Add multiple VS Team Services build steps, each one performing a stage task.</span></span>

<span data-ttu-id="2d17e-110">이 문서에서는 두 옵션 모두를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-110">This article demonstrates both options.</span></span> <span data-ttu-id="2d17e-111">첫 번째 옵션은 Visual Studio에서 개발자가 사용하는 것과 동일한 스크립트를 사용하고 전체 수명 주기 동안 일관성을 제공한다는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-111">The first option has the advantage of using the same script used by developers in Visual Studio and providing consistency throughout the lifecycle.</span></span> <span data-ttu-id="2d17e-112">두 번째 옵션은 기본 제공 스크립트보다 편리한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-112">The second option offers a convenient alternative to the built-in script.</span></span> <span data-ttu-id="2d17e-113">두 절차에서는 이미 VS Team Services에 Visual Studio 배포 프로젝트를 체크인했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span></span>

## <a name="copy-artifacts-to-azure"></a><span data-ttu-id="2d17e-114">아티팩트를 Azure로 복사</span><span class="sxs-lookup"><span data-stu-id="2d17e-114">Copy artifacts to Azure</span></span>
<span data-ttu-id="2d17e-115">시나리오에 관계없이 템플릿 배포에 필요한 아티팩트가 있을 경우 해당 항목에 대한 액세스 권한을 Azure Resource Manager에 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-115">Regardless of the scenario, if you have any artifacts that are needed for template deployment, you must give Azure Resource Manager access to them.</span></span> <span data-ttu-id="2d17e-116">이러한 아티팩트에는 다음과 같은 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-116">These artifacts can include files such as:</span></span>

* <span data-ttu-id="2d17e-117">중첩된 템플릿</span><span class="sxs-lookup"><span data-stu-id="2d17e-117">Nested templates</span></span>
* <span data-ttu-id="2d17e-118">구성 스크립트 및 DSC 스크립트 </span><span class="sxs-lookup"><span data-stu-id="2d17e-118">Configuration scripts and DSC scripts</span></span>
* <span data-ttu-id="2d17e-119">응용 프로그램 이진 파일</span><span class="sxs-lookup"><span data-stu-id="2d17e-119">Application binaries</span></span>

### <a name="nested-templates-and-configuration-scripts"></a><span data-ttu-id="2d17e-120">중첩된 템플릿 및 구성 스크립트</span><span class="sxs-lookup"><span data-stu-id="2d17e-120">Nested Templates and Configuration Scripts</span></span>
<span data-ttu-id="2d17e-121">Visual Studio에서 제공하는 템플릿을 사용할 경우(또는 Visual Studio 스니펫으로 빌드한 템플릿) PowerShell 스크립트가 아티팩트를 스테이징할 뿐 아니라, 다른 배포를 위해 리소스에 대한 URI를 매개 변수화합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-121">When you use the templates provided by Visual Studio (or built with Visual Studio snippets), the PowerShell script not only stages the artifacts, it also parameterizes the URI for the resources for different deployments.</span></span> <span data-ttu-id="2d17e-122">그런 다음 스크립트는 아티팩트를 Azure의 보안 컨테이너에 복사하고, 해당 컨테이너에 대한 SaS 토큰을 만든 다음 이 정보를 템플릿 배포에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-122">The script then copies the artifacts to a secure container in Azure, creates a SaS token for that container, and then passes that information on to the template deployment.</span></span> <span data-ttu-id="2d17e-123">중첩된 템플릿에 대한 자세한 내용은 [템플릿 배포 만들기](https://msdn.microsoft.com/library/azure/dn790564.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d17e-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) to learn more about nested templates.</span></span>  <span data-ttu-id="2d17e-124">VS Team Services에서 태스크를 사용하는 경우 템플릿 배포에 적합한 태스크를 선택해야 하며, 필요에 따라 준비 단계의 매개 변수 값을 템플릿 배포에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-124">When using tasks in VS Team Services, you must select the appropriate tasks for your template deployment and if necessary, pass parameter values from the staging step to the template deployment.</span></span>

## <a name="set-up-continuous-deployment-in-vs-team-services"></a><span data-ttu-id="2d17e-125">VS Team Services에서 연속 배포 설정</span><span class="sxs-lookup"><span data-stu-id="2d17e-125">Set up continuous deployment in VS Team Services</span></span>
<span data-ttu-id="2d17e-126">VS Team Services에서 PowerShell 스크립트를 호출하려면 빌드 정의를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-126">To call the PowerShell script in VS Team Services, you need to update your build definition.</span></span> <span data-ttu-id="2d17e-127">이 단계는 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-127">In brief, the steps are:</span></span> 

1. <span data-ttu-id="2d17e-128">빌드 정의를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-128">Edit the build definition.</span></span>
2. <span data-ttu-id="2d17e-129">VS Team Services에서 Azure 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-129">Set up Azure authorization in VS Team Services.</span></span>
3. <span data-ttu-id="2d17e-130">Azure 리소스 그룹 배포 프로젝트에서 PowerShell 스크립트를 참조하는 Azure PowerShell 빌드 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-130">Add an Azure PowerShell build step that references the PowerShell script in the Azure Resource Group deployment project.</span></span>
4. <span data-ttu-id="2d17e-131">VS Team Services에서 빌드한 프로젝트의 작업을 위해 *-ArtifactsStagingDirectory* 매개 변수의 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-131">Set the value of the *-ArtifactsStagingDirectory* parameter to work with a project built in VS Team Services.</span></span>

### <a name="detailed-walkthrough-for-option-1"></a><span data-ttu-id="2d17e-132">옵션1에 대한 자세한 연습</span><span class="sxs-lookup"><span data-stu-id="2d17e-132">Detailed walkthrough for Option 1</span></span>
<span data-ttu-id="2d17e-133">다음 절차에서는 프로젝트의 PowerShell 스크립트를 실행하는 단일 태스크를 사용하여 VS Team Services에서 연속 배포를 구성하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-133">The following procedures walk you through the steps necessary to configure continuous deployment in VS Team Services using a single task that runs the PowerShell script in your project.</span></span> 

1. <span data-ttu-id="2d17e-134">VS Team Services 빌드 정의를 편집하고 Azure PowerShell 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span></span> <span data-ttu-id="2d17e-135">**빌드 정의** 범주 아래에서 빌드 정의를 선택하고 **편집** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-135">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![빌드 정의 편집][0]
2. <span data-ttu-id="2d17e-137">새 **Azure PowerShell** 빌드 단계를 빌드 정의에 추가한 다음 **빌드 단계 추가...** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-137">Add a new **Azure PowerShell** build step to the build definition and then choose the **Add build step…**</span></span> <span data-ttu-id="2d17e-138">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-138">button.</span></span>
   
   ![빌드 단계 추가][1]
3. <span data-ttu-id="2d17e-140">**배포 작업** 범주를 선택한 다음 **Azure PowerShell** 작업을 선택하고 해당 항목의 **추가** 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-140">Choose the **Deploy task** category, select the **Azure PowerShell** task, and then choose its **Add** button.</span></span>
   
   ![작업 추가][2]
4. <span data-ttu-id="2d17e-142">**Azure PowerShell** 빌드 단계를 선택하고 해당 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-142">Choose the **Azure PowerShell** build step and then fill in its values.</span></span>
   
   1. <span data-ttu-id="2d17e-143">이미 VS Team Services에 추가된 Azure 서비스 끝점이 있는 경우 **Azure 구독** 드롭다운 목록 상자에서 구독을 선택하고 다음 섹션으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-143">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop-down list box and then skip to the next section.</span></span> 
      
      <span data-ttu-id="2d17e-144">VS Team Services에 Azure 서비스 끝점이 없으면 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-144">If you don’t have an Azure service endpoint in VS Team Services, you need to add one.</span></span> <span data-ttu-id="2d17e-145">이 하위 섹션에서는 이 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-145">This subsection takes you through the process.</span></span> <span data-ttu-id="2d17e-146">Azure 계정에서 Microsoft 계정(예: Hotmail)을 사용할 경우 다음 단계를 통해 서비스 주체 인증을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-146">If your Azure account uses a Microsoft account (such as Hotmail), you must take the following steps to get a Service Principal authentication.</span></span>
   2. <span data-ttu-id="2d17e-147">**Azure 구독** 드롭다운 목록 상자 옆에 있는 **관리** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-147">Choose the **Manage** link next to the **Azure Subscription** drop-down list box.</span></span>
      
      ![Azure 구독 관리][3]
   3. <span data-ttu-id="2d17e-149">**새 서비스 끝점** 드롭다운 목록 상자에서 **Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-149">Choose **Azure** in the **New Service Endpoint** drop-down list box.</span></span>
      
      ![새 서비스 끝점][4]
   4. <span data-ttu-id="2d17e-151">**Azure 구독 추가** 대화 상자에서 **서비스 사용자** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-151">In the **Add Azure Subscription** dialog box, select the **Service Principal** option.</span></span>
      
      ![서비스 주체 옵션][5]
   5. <span data-ttu-id="2d17e-153">Azure 구독 정보를 **Azure 구독 추가** 대화 상자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-153">Add your Azure subscription information to the **Add Azure Subscription** dialog box.</span></span> <span data-ttu-id="2d17e-154">다음 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-154">You need to provide the following items:</span></span>
      
      * <span data-ttu-id="2d17e-155">구독 ID</span><span class="sxs-lookup"><span data-stu-id="2d17e-155">Subscription Id</span></span>
      * <span data-ttu-id="2d17e-156">구독 이름</span><span class="sxs-lookup"><span data-stu-id="2d17e-156">Subscription Name</span></span>
      * <span data-ttu-id="2d17e-157">서비스 주체 ID</span><span class="sxs-lookup"><span data-stu-id="2d17e-157">Service Principal Id</span></span>
      * <span data-ttu-id="2d17e-158">서비스 주체 키</span><span class="sxs-lookup"><span data-stu-id="2d17e-158">Service Principal Key</span></span>
      * <span data-ttu-id="2d17e-159">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="2d17e-159">Tenant Id</span></span>
   6. <span data-ttu-id="2d17e-160">**구독** 이름 상자 옆에 선택의 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-160">Add a name of your choice to the **Subscription** name box.</span></span> <span data-ttu-id="2d17e-161">이 값은 나중에 VS Team Services의 **Azure 구독** 드롭다운 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-161">This value appears later in the **Azure Subscription** drop-down list in VS Team Services.</span></span> 
   7. <span data-ttu-id="2d17e-162">Azure 구독 ID를 모르는 경우 다음 명령 중 하나를 사용하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-162">If you don’t know your Azure subscription ID, you can use one of the following commands to retrieve it.</span></span>
      
      <span data-ttu-id="2d17e-163">PowerShell 스크립트의 경우 </span><span class="sxs-lookup"><span data-stu-id="2d17e-163">For PowerShell scripts, use:</span></span>
      
      `Get-AzureRmSubscription`
      
      <span data-ttu-id="2d17e-164">Azure CLI의 경우 </span><span class="sxs-lookup"><span data-stu-id="2d17e-164">For Azure CLI, use:</span></span>
      
      `azure account show`
   8. <span data-ttu-id="2d17e-165">서비스 주체 ID, 서비스 주체 키 및 테넌트 ID를 가져오려면 [Active Directory 응용 프로그램 및 서비스 주체 만들기](resource-group-create-service-principal-portal.md) 또는 [Azure Resource Manager를 사용한 서비스 주체 인증](resource-group-authenticate-service-principal.md)의 절차에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-165">To get a Service Principal ID, Service Principal Key, and Tenant ID, follow the procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span></span>
   9. <span data-ttu-id="2d17e-166">서비스 주체 ID, 서비스 주체 키 및 테넌트 ID 값을 **Azure 구독 추가** 대화 상자에 추가한 다음 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-166">Add the Service Principal ID, Service Principal Key, and Tenant ID values to the **Add Azure Subscription** dialog box and then choose the **OK** button.</span></span>
      
      <span data-ttu-id="2d17e-167">이제 Azure PowerShell 스크립트를 실행하는 데 사용할 유효한 서비스 주체를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-167">You now have a valid Service Principal to use to run the Azure PowerShell script.</span></span>
5. <span data-ttu-id="2d17e-168">빌드 정의를 편집하고 **Azure PowerShell** 빌드 단계를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-168">Edit the build definition and choose the **Azure PowerShell** build step.</span></span> <span data-ttu-id="2d17e-169">**Azure 구독** 드롭다운 목록 상자에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-169">Select the subscription in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="2d17e-170">(구독이 나타나지 않으면 **관리** 링크 옆에 있는 **새로 고침** 단추를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="2d17e-170">(If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.)</span></span> 
   
   ![Azure PowerShell 빌드 작업 구성][8]
6. <span data-ttu-id="2d17e-172">Deploy-AzureResourceGroup.ps1 PowerShell 스크립트에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-172">Provide a path to the Deploy-AzureResourceGroup.ps1 PowerShell script.</span></span> <span data-ttu-id="2d17e-173">이 작업을 수행하려면 **스크립트 경로** 상자 옆의 말줄임표(...) 버튼을 선택하고, 프로젝트의 **Scripts** 폴더에서 Deploy-AzureResourceGroup.ps1 PowerShell 스크립트로 이동한 다음 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-173">To do this, choose the ellipsis (…) button next to the **Script Path** box, navigate to the Deploy-AzureResourceGroup.ps1 PowerShell script in the **Scripts** folder of your project, select it, and then choose the **OK** button.</span></span>    
   
   ![스크립트에 대한 경로 선택][9]
7. <span data-ttu-id="2d17e-175">스크립트를 선택한 다음 Build.StagingDirectory에서 실행되도록 스크립트 경로를 업데이트합니다( *ArtifactsLocation* 이 설정된 것과 동일한 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="2d17e-175">After you select the script, update the path to the script so that it’s run from the Build.StagingDirectory (the same directory that *ArtifactsLocation* is set to).</span></span> <span data-ttu-id="2d17e-176">"$(Build.StagingDirectory)/"를 스크립트 경로 앞에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-176">You can do this by adding “$(Build.StagingDirectory)/” to the beginning of the script path.</span></span>
   
    ![스크립트에 대한 경로 편집][10]
8. <span data-ttu-id="2d17e-178">**스크립트 인수** 상자에 다음 매개 변수를 입력합니다(한 줄로).</span><span class="sxs-lookup"><span data-stu-id="2d17e-178">In the **Script Arguments** box, enter the following parameters (in a single line).</span></span> <span data-ttu-id="2d17e-179">Visual Studio에서 스크립트를 실행하면 **출력** 창에서 VS가 매개 변수를 어떻게 사용하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-179">When you run the script in Visual Studio, you can see how VS uses the parameters in the **Output** window.</span></span> <span data-ttu-id="2d17e-180">이 정보를 빌드 단계에서 매개 변수 값을 설정하기 위한 출발점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-180">You can use this as a starting point for setting the parameter values in your build step.</span></span>
   
   | <span data-ttu-id="2d17e-181">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2d17e-181">Parameter</span></span> | <span data-ttu-id="2d17e-182">설명</span><span class="sxs-lookup"><span data-stu-id="2d17e-182">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2d17e-183">-ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="2d17e-183">-ResourceGroupLocation</span></span> |<span data-ttu-id="2d17e-184">리소스 그룹이 위치한 geo-location 값(예: **eastus** 또는 **'East US'**).</span><span class="sxs-lookup"><span data-stu-id="2d17e-184">The geo-location value where the resource group is located, such as **eastus** or **'East US'**.</span></span> <span data-ttu-id="2d17e-185">이름에 공백이 있을 경우 작은따옴표를 추가합니다. 자세한 내용은 [Azure 지역](https://azure.microsoft.com/en-us/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d17e-185">(Add single quotes if there's a space in the name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span></span> |
   | <span data-ttu-id="2d17e-186">-ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2d17e-186">-ResourceGroupName</span></span> |<span data-ttu-id="2d17e-187">이 배포에 사용되는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-187">The name of the resource group used for this deployment.</span></span> |
   | <span data-ttu-id="2d17e-188">-UploadArtifacts</span><span class="sxs-lookup"><span data-stu-id="2d17e-188">-UploadArtifacts</span></span> |<span data-ttu-id="2d17e-189">이 매개 변수가 있는 경우 로컬 시스템에서 Azure에 업로드해야 하는 아티팩트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-189">This parameter, when present, specifies that artifacts that need to be uploaded to Azure from the local system.</span></span> <span data-ttu-id="2d17e-190">템플릿 배포에서 PowerShell 스크립트를 사용하여 스테이징하려는 추가 아티팩트가 필요한 경우에만 이 스위치를 설정합니다(예: 구성 스크립트 또는 중첩된 템플릿).</span><span class="sxs-lookup"><span data-stu-id="2d17e-190">You only need to set this switch if your template deployment requires extra artifacts that you want to stage using the PowerShell script (such as configuration scripts or nested templates).</span></span> |
   | <span data-ttu-id="2d17e-191">-StorageAccountName</span><span class="sxs-lookup"><span data-stu-id="2d17e-191">-StorageAccountName</span></span> |<span data-ttu-id="2d17e-192">이 배포에 대한 스테이지 아티팩트에 사용되는 저장소 계정 이름.</span><span class="sxs-lookup"><span data-stu-id="2d17e-192">The name of the storage account used to stage artifacts for this deployment.</span></span> <span data-ttu-id="2d17e-193">이 매개 변수는 배포에 대한 아티팩트를 준비하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-193">This parameter is only used if you are staging artifacts for deployment.</span></span> <span data-ttu-id="2d17e-194">이 매개 변수가 제공되는 경우 이전 배포 동안 스크립트에서 저장소 계정을 만들지 않은 경우 새 저장소 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-194">If this parameter is supplied, a new storage account is created if the script has not created one during a previous deployment.</span></span> <span data-ttu-id="2d17e-195">매개 변수를 지정하는 경우 저장소 계정이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-195">If the parameter is specified, the storage account must already exist.</span></span> |
   | <span data-ttu-id="2d17e-196">-StorageAccountResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2d17e-196">-StorageAccountResourceGroupName</span></span> |<span data-ttu-id="2d17e-197">저장소 계정과 연결된 리소스 그룹의 이름.</span><span class="sxs-lookup"><span data-stu-id="2d17e-197">The name of the resource group associated with the storage account.</span></span> <span data-ttu-id="2d17e-198">이 매개 변수는 StorageAccountName 매개 변수에 대한 값을 제공하는 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-198">This parameter is required only if you provide a value for the StorageAccountName parameter.</span></span> |
   | <span data-ttu-id="2d17e-199">-TemplateFile</span><span class="sxs-lookup"><span data-stu-id="2d17e-199">-TemplateFile</span></span> |<span data-ttu-id="2d17e-200">Azure 리소스 그룹 배포 프로젝트의 템플릿 파일에 대한 경로.</span><span class="sxs-lookup"><span data-stu-id="2d17e-200">The path to the template file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="2d17e-201">유연성을 증대하려면 이 매개 변수에 절대 경로 대신 PowerShell 스크립트의 위치에 상대적인 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-201">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="2d17e-202">-TemplateParametersFile</span><span class="sxs-lookup"><span data-stu-id="2d17e-202">-TemplateParametersFile</span></span> |<span data-ttu-id="2d17e-203">Azure 리소스 그룹 배포 프로젝트의 매개 변수 파일에 대한 경로.</span><span class="sxs-lookup"><span data-stu-id="2d17e-203">The path to the parameters file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="2d17e-204">유연성을 증대하려면 이 매개 변수에 절대 경로 대신 PowerShell 스크립트의 위치에 상대적인 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-204">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="2d17e-205">-ArtifactStagingDirectory</span><span class="sxs-lookup"><span data-stu-id="2d17e-205">-ArtifactStagingDirectory</span></span> |<span data-ttu-id="2d17e-206">이 매개 변수는 프로젝트의 이진 파일을 복사해 올 폴더를 PowerShell 스크립트에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-206">This parameter lets the PowerShell script know the folder from where the project’s binary files should be copied.</span></span> <span data-ttu-id="2d17e-207">이 값은 PowerShell 스크립트에서 사용하는 기본값보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-207">This value overrides the default value used by the PowerShell script.</span></span> <span data-ttu-id="2d17e-208">VS Team Services 사용을 위해 이 값을 -ArtifactStagingDirectory $(Build.StagingDirectory)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-208">For VS Team Services use, set the value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span></span> |
   
   <span data-ttu-id="2d17e-209">스크립트 인수 예는 다음과 같습니다(읽기 쉽도록 줄 구분).</span><span class="sxs-lookup"><span data-stu-id="2d17e-209">Here’s a script arguments example (line broken for readability):</span></span>
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   <span data-ttu-id="2d17e-210">완료되면 **스크립트 인수** 상자가 다음 목록과 유사하게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-210">When you’re finished, the **Script Arguments** box should resemble the following list:</span></span>
   
   ![스크립트 인수][11]
9. <span data-ttu-id="2d17e-212">Azure PowerShell 빌드 단계에 모든 필요한 항목을 추가한 후 **큐** 빌드 버튼을 선택하여 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-212">After you’ve added all the required items to the Azure PowerShell build step, choose the **Queue** build button to build the project.</span></span> <span data-ttu-id="2d17e-213">**빌드** 화면에 PowerShell 스크립트의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-213">The **Build** screen shows the output from the PowerShell script.</span></span>

### <a name="detailed-walkthrough-for-option-2"></a><span data-ttu-id="2d17e-214">옵션2에 대한 자세한 연습</span><span class="sxs-lookup"><span data-stu-id="2d17e-214">Detailed walkthrough for Option 2</span></span>
<span data-ttu-id="2d17e-215">다음 절차에서는 기본 제공 작업을 사용하여 VS Team Services에서 연속 배포를 구성하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-215">The following procedures walk you through the steps necessary to configure continuous deployment in VS Team Services using the built-in tasks.</span></span>

1. <span data-ttu-id="2d17e-216">VS Team Services 빌드 정의를 편집하여 두 가지 새로운 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-216">Edit your VS Team Services build definition to add two new build steps.</span></span> <span data-ttu-id="2d17e-217">**빌드 정의** 범주 아래에서 빌드 정의를 선택하고 **편집** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-217">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![빌드 정의 편집][12]
2. <span data-ttu-id="2d17e-219">**빌드 단계 추가...**를 사용하여 빌드 정의에 새 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-219">Add the new build steps to the build definition using the **Add build step…**</span></span> <span data-ttu-id="2d17e-220">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-220">button.</span></span>
   
   ![빌드 단계 추가][13]
3. <span data-ttu-id="2d17e-222">**배포** 작업 범주를 선택한 다음 **Azure File Copy** 작업을 선택하고 해당 항목의 **추가** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-222">Choose the **Deploy** task category, select the **Azure File Copy** task, and then choose its **Add** button.</span></span>
   
   ![Azure File Copy 작업 추가][14]
4. <span data-ttu-id="2d17e-224">**Azure 리소스 그룹 배포** 작업을 선택한 다음 해당 항목의 **추가** 단추를 선택한 후 **작업 카탈로그**를 **닫습니다**.</span><span class="sxs-lookup"><span data-stu-id="2d17e-224">Choose the **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** the **Task Catalog**.</span></span>
   
   ![Azure 리소스 그룹 배포 작업 추가][15]
5. <span data-ttu-id="2d17e-226">**Azure 파일 복사** 작업을 선택하고 해당 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-226">Choose the **Azure File Copy** task and fill in its values.</span></span>
   
   <span data-ttu-id="2d17e-227">이미 VS Team Services에 추가된 Azure 서비스 끝점이 있는 경우 **Azure 구독** 드롭다운 목록 상자에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-227">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="2d17e-228">구독이 없는 경우 VS Team Services에서 구독을 설정하는 방법에 대한 지침은 [옵션 1](#detailed-walkthrough-for-option-1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d17e-228">If you do not have a subscription, see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span></span>
   
   * <span data-ttu-id="2d17e-229">원본 - **$(Build.StagingDirectory)** 입력</span><span class="sxs-lookup"><span data-stu-id="2d17e-229">Source - enter **$(Build.StagingDirectory)**</span></span>
   * <span data-ttu-id="2d17e-230">Azure 연결 형식 - **Azure Resource Manager** 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-230">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="2d17e-231">Azure RM 구독 - **Azure 구독** 드롭다운 목록 상자에서 사용하려는 저장소 계정에 대한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-231">Azure RM Subscription - select the subscription for the storage account you want to use in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="2d17e-232">구독이 나타나지 않으면 **관리** 링크 옆에 있는 **새로 고침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-232">If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.</span></span>
   * <span data-ttu-id="2d17e-233">대상 형식 - **Azure Blob** 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-233">Destination Type - select **Azure Blob**</span></span>
   * <span data-ttu-id="2d17e-234">RM 저장소 계정 - 아티팩트 준비에 사용하려는 저장소 계정 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-234">RM Storage Account - select the storage account you would like to use for staging artifacts</span></span>
   * <span data-ttu-id="2d17e-235">컨테이너 이름 - 준비에 사용하려는 컨테이너의 이름을 입력합니다. 유효한 모든 컨테이너 이름을 사용할 수 있지만 이 빌드 정의의 전용 컨테이너 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-235">Container Name - enter the name of the container you would like to use for staging; it can be any valid container name, but use one dedicated to this build definition</span></span>
   
   <span data-ttu-id="2d17e-236">출력 값:</span><span class="sxs-lookup"><span data-stu-id="2d17e-236">For the output values:</span></span>
   
   * <span data-ttu-id="2d17e-237">저장소 컨테이너 URI - **artifactsLocation** 입력</span><span class="sxs-lookup"><span data-stu-id="2d17e-237">Storage Container URI - enter **artifactsLocation**</span></span>
   * <span data-ttu-id="2d17e-238">저장소 컨테이너 SAS 토큰 - **artifactsLocationSasToken** 입력</span><span class="sxs-lookup"><span data-stu-id="2d17e-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span></span>
   
   ![Azure File Copy 작업 구성][16]
6. <span data-ttu-id="2d17e-240">**Azure 리소스 그룹 배포** 빌드 단계를 선택하고 해당 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-240">Choose the **Azure Resource Group Deployment** build step and then fill in its values.</span></span>
   
   * <span data-ttu-id="2d17e-241">Azure 연결 형식 - **Azure Resource Manager** 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-241">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="2d17e-242">Azure RM 구독 - **Azure 구독** 드롭다운 목록 상자에서 배포에 대한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-242">Azure RM Subscription - select the subscription for deployment in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="2d17e-243">일반적으로 이전 단계에서 사용한 것과 동일한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-243">This will usually be the same subscription used in the previous step</span></span>
   * <span data-ttu-id="2d17e-244">작업 - **리소스 그룹 만들기 또는 업데이트** 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-244">Action - select **Create or Update Resource Group**</span></span>
   * <span data-ttu-id="2d17e-245">리소스 그룹 - 리소스 그룹을 선택하거나 배포에 대한 새 리소스 그룹의 이름 입력</span><span class="sxs-lookup"><span data-stu-id="2d17e-245">Resource Group - select a resource group or enter the name of a new resource group for the deployment</span></span>
   * <span data-ttu-id="2d17e-246">위치 - 리소스 그룹의 위치 선택</span><span class="sxs-lookup"><span data-stu-id="2d17e-246">Location - select the location for the resource group</span></span>
   * <span data-ttu-id="2d17e-247">템플릿 - 앞에 **$(Build.StagingDirectory)**를 추가하여 배포될 템플릿의 경로 및 이름 입력(예: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**)</span><span class="sxs-lookup"><span data-stu-id="2d17e-247">Template - enter the path and name of the template to be deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span></span>
   * <span data-ttu-id="2d17e-248">템플릿 매개 변수 - 앞에 **$(Build.StagingDirectory)**를 추가하여 사용될 매개 변수의 경로 및 이름 입력(예: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**)</span><span class="sxs-lookup"><span data-stu-id="2d17e-248">Template Parameters - enter the path and name of the parameters to be used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span></span>
   * <span data-ttu-id="2d17e-249">템플릿 매개 변수 재정의 - 다음 코드를 입력하거나 복사하여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-249">Override Template Parameters - enter or copy and paste the following code:</span></span>
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Azure 리소스 그룹 배포 작업 구성][17]
7. <span data-ttu-id="2d17e-251">모든 필요한 항목을 추가한 후 빌드 정의를 저장하고 위쪽에서 **새 빌드 큐 대기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d17e-251">After you’ve added all the required items, save the build definition and choose **Queue new build** at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d17e-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d17e-252">Next steps</span></span>
<span data-ttu-id="2d17e-253">Azure Resource Manager 및 Azure 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](azure-resource-manager/resource-group-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d17e-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) to learn more about Azure Resource Manager and Azure resource groups.</span></span>

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
