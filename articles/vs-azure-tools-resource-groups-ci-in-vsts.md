---
title: "Azure 리소스 그룹 프로젝트를 사용 하 여 VS Team Services에서 aaaContinuous 통합 | Microsoft Docs"
description: "Visual Studio에서 Azure 리소스 그룹 배포를 사용 하 여 Visual Studio Team Services에서 연속 통합을 tooset 프로젝션 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a><span data-ttu-id="b6675-103">Azure 리소스 그룹 배포 프로젝트를 사용하여 Visual Studio Team Services에서 연속 통합</span><span class="sxs-lookup"><span data-stu-id="b6675-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span></span>
<span data-ttu-id="b6675-104">다양 한 단계에서 작업을 수행 Azure 템플릿 toodeploy: 빌드, 테스트, 복사 tooAzure ("준비" 라고도 함) 및 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-104">toodeploy an Azure template, you perform tasks in various stages: Build, Test, Copy tooAzure (also called "Staging"), and Deploy Template.</span></span> <span data-ttu-id="b6675-105">두 가지 방법으로 toodeploy 템플릿 tooVisual Studio Team Services (VS Team Services) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-105">There are two different ways toodeploy templates tooVisual Studio Team Services (VS Team Services).</span></span> <span data-ttu-id="b6675-106">두 방법 모두 hello 동일한 결과 제공 하므로 hello 워크플로 가장 잘 맞는 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-106">Both methods provide hello same results, so choose hello one that best fits your workflow.</span></span>

1. <span data-ttu-id="b6675-107">Hello Azure 리소스 그룹 배포 프로젝트 (deploy-azureresourcegroup.ps1 스크립트로)에 포함 된 hello PowerShell 스크립트를 실행 하는 단일 단계 tooyour 빌드 정의 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-107">Add a single step tooyour build definition that runs hello PowerShell script that’s included in hello Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span></span> <span data-ttu-id="b6675-108">hello 스크립트 아티팩트를 복사한 다음 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-108">hello script copies artifacts and then deploys hello template.</span></span>
2. <span data-ttu-id="b6675-109">각각 단계 작업을 수행하는 여러 VS Team Services 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-109">Add multiple VS Team Services build steps, each one performing a stage task.</span></span>

<span data-ttu-id="b6675-110">이 문서에서는 두 옵션 모두를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-110">This article demonstrates both options.</span></span> <span data-ttu-id="b6675-111">hello 첫 번째 옵션 이점이 hello Visual Studio에서 개발자가 동일한 스크립트를 사용 하는 hello를 사용 하 고 hello 수명 주기 전체에서 일관성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-111">hello first option has hello advantage of using hello same script used by developers in Visual Studio and providing consistency throughout hello lifecycle.</span></span> <span data-ttu-id="b6675-112">hello 두 번째 옵션은 편리 하 게 대체 toohello 기본 제공 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-112">hello second option offers a convenient alternative toohello built-in script.</span></span> <span data-ttu-id="b6675-113">두 절차에서는 이미 VS Team Services에 Visual Studio 배포 프로젝트를 체크인했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span></span>

## <a name="copy-artifacts-tooazure"></a><span data-ttu-id="b6675-114">아티팩트 tooAzure 복사</span><span class="sxs-lookup"><span data-stu-id="b6675-114">Copy artifacts tooAzure</span></span>
<span data-ttu-id="b6675-115">템플릿 배포에 필요한 모든 아티팩트가 있으면 hello 시나리오에 관계 없이 Azure 리소스 관리자 액세스 toothem를 부여 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-115">Regardless of hello scenario, if you have any artifacts that are needed for template deployment, you must give Azure Resource Manager access toothem.</span></span> <span data-ttu-id="b6675-116">이러한 아티팩트에는 다음과 같은 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-116">These artifacts can include files such as:</span></span>

* <span data-ttu-id="b6675-117">중첩된 템플릿</span><span class="sxs-lookup"><span data-stu-id="b6675-117">Nested templates</span></span>
* <span data-ttu-id="b6675-118">구성 스크립트 및 DSC 스크립트 </span><span class="sxs-lookup"><span data-stu-id="b6675-118">Configuration scripts and DSC scripts</span></span>
* <span data-ttu-id="b6675-119">응용 프로그램 이진 파일</span><span class="sxs-lookup"><span data-stu-id="b6675-119">Application binaries</span></span>

### <a name="nested-templates-and-configuration-scripts"></a><span data-ttu-id="b6675-120">중첩된 템플릿 및 구성 스크립트</span><span class="sxs-lookup"><span data-stu-id="b6675-120">Nested Templates and Configuration Scripts</span></span>
<span data-ttu-id="b6675-121">Visual Studio에서 제공 하는 hello 서식 파일을 사용 하는 경우 (또는 Visual Studio 코드 조각을 사용 하 여 빌드한) hello PowerShell 스크립트 뿐만 아니라 hello 아티팩트를 준비, 다양 한 배포에 대 한 hello 리소스에 대 한 hello URI에서 매개 변수화도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-121">When you use hello templates provided by Visual Studio (or built with Visual Studio snippets), hello PowerShell script not only stages hello artifacts, it also parameterizes hello URI for hello resources for different deployments.</span></span> <span data-ttu-id="b6675-122">hello 스크립트 그런 다음 Azure의 hello 아티팩트 tooa 보안 컨테이너를 복사, 해당 컨테이너에 대 한 SaS 토큰을 만드는 데 및 toohello 템플릿 배포에 대 한 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-122">hello script then copies hello artifacts tooa secure container in Azure, creates a SaS token for that container, and then passes that information on toohello template deployment.</span></span> <span data-ttu-id="b6675-123">참조 [템플릿 배포를 만드는](https://msdn.microsoft.com/library/azure/dn790564.aspx) 중첩 템플릿에서 toolearn에 더 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn more about nested templates.</span></span>  <span data-ttu-id="b6675-124">VS Team Services의 작업을 사용할 경우 템플릿 배포에 대 한 hello 적절 한 작업을 선택 하 고 필요한 경우 단계 toohello 템플릿 배포를 준비 하는 hello에서 매개 변수 값을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-124">When using tasks in VS Team Services, you must select hello appropriate tasks for your template deployment and if necessary, pass parameter values from hello staging step toohello template deployment.</span></span>

## <a name="set-up-continuous-deployment-in-vs-team-services"></a><span data-ttu-id="b6675-125">VS Team Services에서 연속 배포 설정</span><span class="sxs-lookup"><span data-stu-id="b6675-125">Set up continuous deployment in VS Team Services</span></span>
<span data-ttu-id="b6675-126">tooupdate 해야 toocall VS Team Services에서 PowerShell 스크립트를 hello, 빌드 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-126">toocall hello PowerShell script in VS Team Services, you need tooupdate your build definition.</span></span> <span data-ttu-id="b6675-127">간단히 말해서 hello 단계는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-127">In brief, hello steps are:</span></span> 

1. <span data-ttu-id="b6675-128">Hello 빌드 정의 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-128">Edit hello build definition.</span></span>
2. <span data-ttu-id="b6675-129">VS Team Services에서 Azure 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-129">Set up Azure authorization in VS Team Services.</span></span>
3. <span data-ttu-id="b6675-130">Hello Azure 리소스 그룹 배포 프로젝트에서 hello PowerShell 스크립트를 참조 하는 Azure PowerShell 빌드 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-130">Add an Azure PowerShell build step that references hello PowerShell script in hello Azure Resource Group deployment project.</span></span>
4. <span data-ttu-id="b6675-131">Hello의 hello 값 설정 *-ArtifactsStagingDirectory* VS Team Services에서 빌드한 프로젝트와 toowork 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-131">Set hello value of hello *-ArtifactsStagingDirectory* parameter toowork with a project built in VS Team Services.</span></span>

### <a name="detailed-walkthrough-for-option-1"></a><span data-ttu-id="b6675-132">옵션1에 대한 자세한 연습</span><span class="sxs-lookup"><span data-stu-id="b6675-132">Detailed walkthrough for Option 1</span></span>
<span data-ttu-id="b6675-133">hello 다음 절차에 관한 hello 단계 필요한 tooconfigure hello PowerShell 스크립트 프로젝트에서 실행 되는 단일 작업을 사용 하 여 VS Team Services에서 연속 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-133">hello following procedures walk you through hello steps necessary tooconfigure continuous deployment in VS Team Services using a single task that runs hello PowerShell script in your project.</span></span> 

1. <span data-ttu-id="b6675-134">VS Team Services 빌드 정의를 편집하고 Azure PowerShell 빌드 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span></span> <span data-ttu-id="b6675-135">Hello에서 hello 빌드 정의 선택 **빌드 정의** 범주 hello 선택 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-135">Choose hello build definition under hello **Build definitions** category and then choose hello **Edit** link.</span></span>
   
   ![빌드 정의 편집][0]
2. <span data-ttu-id="b6675-137">새로 추가 **Azure PowerShell** 빌드 단계 toohello 빌드 정의 선택한 후 hello **빌드 단계 추가 중...**</span><span class="sxs-lookup"><span data-stu-id="b6675-137">Add a new **Azure PowerShell** build step toohello build definition and then choose hello **Add build step…**</span></span> <span data-ttu-id="b6675-138">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-138">button.</span></span>
   
   ![빌드 단계 추가][1]
3. <span data-ttu-id="b6675-140">Hello 선택 **배포 작업** 범주, 선택 hello **Azure PowerShell** 의 작업을 선택한 후 해당 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-140">Choose hello **Deploy task** category, select hello **Azure PowerShell** task, and then choose its **Add** button.</span></span>
   
   ![작업 추가][2]
4. <span data-ttu-id="b6675-142">Hello 선택 **Azure PowerShell** 빌드 단계 및 해당 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-142">Choose hello **Azure PowerShell** build step and then fill in its values.</span></span>
   
   1. <span data-ttu-id="b6675-143">Azure 서비스 끝점 추가 tooVS Team Services 이미 있는 경우, hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자와 skip toohello 다음 섹션.</span><span class="sxs-lookup"><span data-stu-id="b6675-143">If you already have an Azure service endpoint added tooVS Team Services, choose hello subscription in hello **Azure Subscription** drop-down list box and then skip toohello next section.</span></span> 
      
      <span data-ttu-id="b6675-144">VS Team Services에서 Azure 서비스 끝점을 없다면 tooadd 하나 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-144">If you don’t have an Azure service endpoint in VS Team Services, you need tooadd one.</span></span> <span data-ttu-id="b6675-145">이 하위 섹션에서는 hello 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-145">This subsection takes you through hello process.</span></span> <span data-ttu-id="b6675-146">Azure 계정에서 Microsoft 계정 (예: Hotmail)를 사용 하는 경우 서비스 사용자 인증 hello 단계 tooget 다음 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-146">If your Azure account uses a Microsoft account (such as Hotmail), you must take hello following steps tooget a Service Principal authentication.</span></span>
   2. <span data-ttu-id="b6675-147">Hello 선택 **관리** 다음 toohello 연결 **Azure 구독** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-147">Choose hello **Manage** link next toohello **Azure Subscription** drop-down list box.</span></span>
      
      ![Azure 구독 관리][3]
   3. <span data-ttu-id="b6675-149">선택 **Azure** hello에 **새 서비스 끝점** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-149">Choose **Azure** in hello **New Service Endpoint** drop-down list box.</span></span>
      
      ![새 서비스 끝점][4]
   4. <span data-ttu-id="b6675-151">Hello에 **Azure 구독 추가** 대화 상자, 선택 hello **서비스 사용자** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-151">In hello **Add Azure Subscription** dialog box, select hello **Service Principal** option.</span></span>
      
      ![서비스 주체 옵션][5]
   5. <span data-ttu-id="b6675-153">추가 Azure 구독 정보 toohello **Azure 구독 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b6675-153">Add your Azure subscription information toohello **Add Azure Subscription** dialog box.</span></span> <span data-ttu-id="b6675-154">다음 항목 tooprovide hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-154">You need tooprovide hello following items:</span></span>
      
      * <span data-ttu-id="b6675-155">구독 ID</span><span class="sxs-lookup"><span data-stu-id="b6675-155">Subscription Id</span></span>
      * <span data-ttu-id="b6675-156">구독 이름</span><span class="sxs-lookup"><span data-stu-id="b6675-156">Subscription Name</span></span>
      * <span data-ttu-id="b6675-157">서비스 주체 ID</span><span class="sxs-lookup"><span data-stu-id="b6675-157">Service Principal Id</span></span>
      * <span data-ttu-id="b6675-158">서비스 주체 키</span><span class="sxs-lookup"><span data-stu-id="b6675-158">Service Principal Key</span></span>
      * <span data-ttu-id="b6675-159">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="b6675-159">Tenant Id</span></span>
   6. <span data-ttu-id="b6675-160">선택한 toohello의 이름을 추가 **구독** 이름 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-160">Add a name of your choice toohello **Subscription** name box.</span></span> <span data-ttu-id="b6675-161">이 값 표시 hello의 뒷부분에 나오는 **Azure 구독** VS Team Services에서 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-161">This value appears later in hello **Azure Subscription** drop-down list in VS Team Services.</span></span> 
   7. <span data-ttu-id="b6675-162">Azure 구독 ID를 모르는 경우 다음 명령을 tooretrieve hello 중 하나를 사용할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-162">If you don’t know your Azure subscription ID, you can use one of hello following commands tooretrieve it.</span></span>
      
      <span data-ttu-id="b6675-163">PowerShell 스크립트의 경우 </span><span class="sxs-lookup"><span data-stu-id="b6675-163">For PowerShell scripts, use:</span></span>
      
      `Get-AzureRmSubscription`
      
      <span data-ttu-id="b6675-164">Azure CLI의 경우 </span><span class="sxs-lookup"><span data-stu-id="b6675-164">For Azure CLI, use:</span></span>
      
      `azure account show`
   8. <span data-ttu-id="b6675-165">서비스 보안 주체 ID를 서비스 사용자 키 및 테 넌 트 ID tooget hello 절차에 따라 [만드는 Active Directory 응용 프로그램 및 서비스 사용자 포털을 사용 하 여](resource-group-create-service-principal-portal.md) 또는 [인 서비스 사용자를 인증 합니다. Azure 리소스 관리자](resource-group-authenticate-service-principal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-165">tooget a Service Principal ID, Service Principal Key, and Tenant ID, follow hello procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span></span>
   9. <span data-ttu-id="b6675-166">서비스 사용자 ID, 서비스 사용자 키 및 테 넌 트 ID 값 toohello 추가 hello **Azure 구독 추가** 대화 상자를 선택한 후 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-166">Add hello Service Principal ID, Service Principal Key, and Tenant ID values toohello **Add Azure Subscription** dialog box and then choose hello **OK** button.</span></span>
      
      <span data-ttu-id="b6675-167">Azure PowerShell 스크립트는 유효한 서비스 사용자 toouse toorun hello를 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-167">You now have a valid Service Principal toouse toorun hello Azure PowerShell script.</span></span>
5. <span data-ttu-id="b6675-168">Hello 빌드 정의 편집 하 고 hello 선택 **Azure PowerShell** 빌드 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-168">Edit hello build definition and choose hello **Azure PowerShell** build step.</span></span> <span data-ttu-id="b6675-169">Hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-169">Select hello subscription in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="b6675-170">(Hello 구독 표시 되지 않으면 hello 선택 **새로 고침** 단추 다음 hello **관리** 링크 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b6675-170">(If hello subscription doesn't appear, choose hello **Refresh** button next hello **Manage** link.)</span></span> 
   
   ![Azure PowerShell 빌드 작업 구성][8]
6. <span data-ttu-id="b6675-172">경로 toohello deploy-azureresourcegroup.ps1 스크립트로 PowerShell 스크립트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-172">Provide a path toohello Deploy-AzureResourceGroup.ps1 PowerShell script.</span></span> <span data-ttu-id="b6675-173">toodo이 hello 줄임표 (...) 단추 다음 toohello 선택 **스크립트 경로** 상자에서 hello에서 deploy-azureresourcegroup.ps1 스크립트로 PowerShell 스크립트를 toohello 이동 **스크립트** 프로젝트의 폴더 선택 선택한 후 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-173">toodo this, choose hello ellipsis (…) button next toohello **Script Path** box, navigate toohello Deploy-AzureResourceGroup.ps1 PowerShell script in hello **Scripts** folder of your project, select it, and then choose hello **OK** button.</span></span>    
   
   ![경로 선택 tooscript][9]
7. <span data-ttu-id="b6675-175">Hello 스크립트를 선택한 후 hello 경로 toohello 스크립트 hello Build.StagingDirectory에서에서 실행 될 수 있도록 업데이트 (동일한 디렉터리 hello 하 *ArtifactsLocation* 로 설정).</span><span class="sxs-lookup"><span data-stu-id="b6675-175">After you select hello script, update hello path toohello script so that it’s run from hello Build.StagingDirectory (hello same directory that *ArtifactsLocation* is set to).</span></span> <span data-ttu-id="b6675-176">"$(Build.StagingDirectory)/" toohello 경로의 시작 부분 hello 스크립트 추가 하 여 수행할 수 있습니다입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-176">You can do this by adding “$(Build.StagingDirectory)/” toohello beginning of hello script path.</span></span>
   
    ![경로 tooscript 편집][10]
8. <span data-ttu-id="b6675-178">Hello에 **스크립트 인수** 상자 hello 매개 변수 (한 줄으로) 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-178">In hello **Script Arguments** box, enter hello following parameters (in a single line).</span></span> <span data-ttu-id="b6675-179">Visual Studio에서 hello 스크립트를 실행할 때 VS 사용 하 여 hello에 대 한 매개 변수를 hello 하는 방법을 확인할 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="b6675-179">When you run hello script in Visual Studio, you can see how VS uses hello parameters in hello **Output** window.</span></span> <span data-ttu-id="b6675-180">빌드 단계에서 hello 매개 변수 값을 설정 하기 위한 시작 지점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-180">You can use this as a starting point for setting hello parameter values in your build step.</span></span>
   
   | <span data-ttu-id="b6675-181">매개 변수</span><span class="sxs-lookup"><span data-stu-id="b6675-181">Parameter</span></span> | <span data-ttu-id="b6675-182">설명</span><span class="sxs-lookup"><span data-stu-id="b6675-182">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b6675-183">-ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="b6675-183">-ResourceGroupLocation</span></span> |<span data-ttu-id="b6675-184">지리적 위치 값 hello 리소스 그룹은 같이 hello **eastus** 또는 **' 미국 동부 '**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-184">hello geo-location value where hello resource group is located, such as **eastus** or **'East US'**.</span></span> <span data-ttu-id="b6675-185">(Hello 이름에 공백이 있는 경우 작은따옴표로 추가 합니다.) 자세한 내용은 [Azure 지역](https://azure.microsoft.com/en-us/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6675-185">(Add single quotes if there's a space in hello name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span></span> |
   | <span data-ttu-id="b6675-186">-ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b6675-186">-ResourceGroupName</span></span> |<span data-ttu-id="b6675-187">이 배포에 사용 되는 hello 리소스 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-187">hello name of hello resource group used for this deployment.</span></span> |
   | <span data-ttu-id="b6675-188">-UploadArtifacts</span><span class="sxs-lookup"><span data-stu-id="b6675-188">-UploadArtifacts</span></span> |<span data-ttu-id="b6675-189">이 매개 변수 있는 경우 toobe 해야 하는 아티팩트 업로드 지정 tooAzure hello 로컬 시스템에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-189">This parameter, when present, specifies that artifacts that need toobe uploaded tooAzure from hello local system.</span></span> <span data-ttu-id="b6675-190">필요할 때만 tooset이이 스위치 템플릿 배포 추가 아티팩트 (예: 구성 스크립트 또는 중첩 된 템플릿도) hello PowerShell 스크립트를 사용 하 여 toostage 한다는 것을 요구 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b6675-190">You only need tooset this switch if your template deployment requires extra artifacts that you want toostage using hello PowerShell script (such as configuration scripts or nested templates).</span></span> |
   | <span data-ttu-id="b6675-191">-StorageAccountName</span><span class="sxs-lookup"><span data-stu-id="b6675-191">-StorageAccountName</span></span> |<span data-ttu-id="b6675-192">이 배포에 대 한 toostage 아티팩트를 사용 하는 hello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-192">hello name of hello storage account used toostage artifacts for this deployment.</span></span> <span data-ttu-id="b6675-193">이 매개 변수는 배포에 대한 아티팩트를 준비하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-193">This parameter is only used if you are staging artifacts for deployment.</span></span> <span data-ttu-id="b6675-194">이 매개 변수가 제공 되는 경우에 새 저장소 계정은 hello 스크립트는 이전 배포 하는 동안 생성 되지 않은 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-194">If this parameter is supplied, a new storage account is created if hello script has not created one during a previous deployment.</span></span> <span data-ttu-id="b6675-195">Hello 매개 변수를 지정 하는 경우 hello 저장소 계정은 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-195">If hello parameter is specified, hello storage account must already exist.</span></span> |
   | <span data-ttu-id="b6675-196">-StorageAccountResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b6675-196">-StorageAccountResourceGroupName</span></span> |<span data-ttu-id="b6675-197">hello 저장소 계정과 연결 된 hello 리소스 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-197">hello name of hello resource group associated with hello storage account.</span></span> <span data-ttu-id="b6675-198">이 매개 변수는 hello StorageAccountName 매개 변수에 대 한 값을 제공 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-198">This parameter is required only if you provide a value for hello StorageAccountName parameter.</span></span> |
   | <span data-ttu-id="b6675-199">-TemplateFile</span><span class="sxs-lookup"><span data-stu-id="b6675-199">-TemplateFile</span></span> |<span data-ttu-id="b6675-200">hello toohello 템플릿 파일 경로 hello Azure 리소스 그룹 배포 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b6675-200">hello path toohello template file in hello Azure Resource Group deployment project.</span></span> <span data-ttu-id="b6675-201">tooenhance 유연성을는 hello 절대 경로가 아닌 PowerShell 스크립트의 상대 toohello 위치는이 매개 변수에 대 한 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-201">tooenhance flexibility, use a path for this parameter that is relative toohello location of hello PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="b6675-202">-TemplateParametersFile</span><span class="sxs-lookup"><span data-stu-id="b6675-202">-TemplateParametersFile</span></span> |<span data-ttu-id="b6675-203">hello toohello 매개 변수 파일 경로 hello Azure 리소스 그룹 배포 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b6675-203">hello path toohello parameters file in hello Azure Resource Group deployment project.</span></span> <span data-ttu-id="b6675-204">tooenhance 유연성을는 hello 절대 경로가 아닌 PowerShell 스크립트의 상대 toohello 위치는이 매개 변수에 대 한 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-204">tooenhance flexibility, use a path for this parameter that is relative toohello location of hello PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="b6675-205">-ArtifactStagingDirectory</span><span class="sxs-lookup"><span data-stu-id="b6675-205">-ArtifactStagingDirectory</span></span> |<span data-ttu-id="b6675-206">이 매개 변수는 hello PowerShell 스크립트를에서 hello 프로젝트의 이진 파일을 복사할 hello 폴더를 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-206">This parameter lets hello PowerShell script know hello folder from where hello project’s binary files should be copied.</span></span> <span data-ttu-id="b6675-207">이 값 hello PowerShell 스크립트에서 사용 하는 hello 기본값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-207">This value overrides hello default value used by hello PowerShell script.</span></span> <span data-ttu-id="b6675-208">VS Team Services에 사용 하 여 hello 값으로 설정:-ArtifactStagingDirectory $(Build.StagingDirectory)</span><span class="sxs-lookup"><span data-stu-id="b6675-208">For VS Team Services use, set hello value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span></span> |
   
   <span data-ttu-id="b6675-209">스크립트 인수 예는 다음과 같습니다(읽기 쉽도록 줄 구분).</span><span class="sxs-lookup"><span data-stu-id="b6675-209">Here’s a script arguments example (line broken for readability):</span></span>
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   <span data-ttu-id="b6675-210">완료 되 면 hello **스크립트 인수** 상자 목록 다음 hello와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-210">When you’re finished, hello **Script Arguments** box should resemble hello following list:</span></span>
   
   ![스크립트 인수][11]
9. <span data-ttu-id="b6675-212">Azure PowerShell 빌드 단계 항목을 필요한 대로 toohello hello 모두 추가한 후 선택 hello **큐** 단추 toobuild hello 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-212">After you’ve added all hello required items toohello Azure PowerShell build step, choose hello **Queue** build button toobuild hello project.</span></span> <span data-ttu-id="b6675-213">hello **빌드** 화면 hello PowerShell 스크립트의에서 출력을 hello를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-213">hello **Build** screen shows hello output from hello PowerShell script.</span></span>

### <a name="detailed-walkthrough-for-option-2"></a><span data-ttu-id="b6675-214">옵션2에 대한 자세한 연습</span><span class="sxs-lookup"><span data-stu-id="b6675-214">Detailed walkthrough for Option 2</span></span>
<span data-ttu-id="b6675-215">hello 다음 절차에 관한 hello 단계 필요한 tooconfigure hello 제공 되는 작업을 사용 하 여 VS Team Services에서 연속 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-215">hello following procedures walk you through hello steps necessary tooconfigure continuous deployment in VS Team Services using hello built-in tasks.</span></span>

1. <span data-ttu-id="b6675-216">VS Team Services 빌드 정의 tooadd 두 개의 새 빌드 단계를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-216">Edit your VS Team Services build definition tooadd two new build steps.</span></span> <span data-ttu-id="b6675-217">Hello에서 hello 빌드 정의 선택 **빌드 정의** 범주 hello 선택 **편집** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-217">Choose hello build definition under hello **Build definitions** category and then choose hello **Edit** link.</span></span>
   
   ![빌드 정의 편집][12]
2. <span data-ttu-id="b6675-219">추가 hello 새 빌드 단계 hello를 사용 하 여 toohello 빌드 정의 **빌드 단계 추가 중...**</span><span class="sxs-lookup"><span data-stu-id="b6675-219">Add hello new build steps toohello build definition using hello **Add build step…**</span></span> <span data-ttu-id="b6675-220">단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-220">button.</span></span>
   
   ![빌드 단계 추가][13]
3. <span data-ttu-id="b6675-222">Hello 선택 **배포** 작업 범주, 선택 hello **Azure 파일 복사** 의 작업을 선택한 후 해당 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-222">Choose hello **Deploy** task category, select hello **Azure File Copy** task, and then choose its **Add** button.</span></span>
   
   ![Azure File Copy 작업 추가][14]
4. <span data-ttu-id="b6675-224">Hello 선택 **Azure 리소스 그룹 배포** 의 작업을 다음 선택 해당 **추가** 단추 차례로 **닫기** hello **작업 카탈로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-224">Choose hello **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** hello **Task Catalog**.</span></span>
   
   ![Azure 리소스 그룹 배포 작업 추가][15]
5. <span data-ttu-id="b6675-226">Hello 선택 **Azure 파일 복사** 작업 및 해당 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-226">Choose hello **Azure File Copy** task and fill in its values.</span></span>
   
   <span data-ttu-id="b6675-227">Azure 서비스 끝점 추가 tooVS Team Services 이미 있는 경우, hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-227">If you already have an Azure service endpoint added tooVS Team Services, choose hello subscription in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="b6675-228">구독이 없는 경우 VS Team Services에서 구독을 설정하는 방법에 대한 지침은 [옵션 1](#detailed-walkthrough-for-option-1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6675-228">If you do not have a subscription, see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span></span>
   
   * <span data-ttu-id="b6675-229">원본 - **$(Build.StagingDirectory)** 입력</span><span class="sxs-lookup"><span data-stu-id="b6675-229">Source - enter **$(Build.StagingDirectory)**</span></span>
   * <span data-ttu-id="b6675-230">Azure 연결 형식 - **Azure Resource Manager** 선택</span><span class="sxs-lookup"><span data-stu-id="b6675-230">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="b6675-231">Azure RM 구독-toouse hello에 원하는 hello 저장소 계정에 대 한 선택 hello 구독 **Azure 구독** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-231">Azure RM Subscription - select hello subscription for hello storage account you want toouse in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="b6675-232">Hello 구독 표시 되지 않으면 hello 선택 **새로 고침** 단추 다음 hello **관리** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-232">If hello subscription doesn't appear, choose hello **Refresh** button next hello **Manage** link.</span></span>
   * <span data-ttu-id="b6675-233">대상 형식 - **Azure Blob** 선택</span><span class="sxs-lookup"><span data-stu-id="b6675-233">Destination Type - select **Azure Blob**</span></span>
   * <span data-ttu-id="b6675-234">RM 저장소 계정-선택 hello 저장소 계정이 toouse 아티팩트를 준비 하 시겠습니까</span><span class="sxs-lookup"><span data-stu-id="b6675-234">RM Storage Account - select hello storage account you would like toouse for staging artifacts</span></span>
   * <span data-ttu-id="b6675-235">컨테이너 이름-hello 이름을 입력 hello 컨테이너의 원하는 toouse 준비;에 대 한 모든 올바른 컨테이너 이름이 될 수 있지만 하나의 전용된 toothis 빌드 정의 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b6675-235">Container Name - enter hello name of hello container you would like toouse for staging; it can be any valid container name, but use one dedicated toothis build definition</span></span>
   
   <span data-ttu-id="b6675-236">Hello 출력 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-236">For hello output values:</span></span>
   
   * <span data-ttu-id="b6675-237">저장소 컨테이너 URI - **artifactsLocation** 입력</span><span class="sxs-lookup"><span data-stu-id="b6675-237">Storage Container URI - enter **artifactsLocation**</span></span>
   * <span data-ttu-id="b6675-238">저장소 컨테이너 SAS 토큰 - **artifactsLocationSasToken** 입력</span><span class="sxs-lookup"><span data-stu-id="b6675-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span></span>
   
   ![Azure File Copy 작업 구성][16]
6. <span data-ttu-id="b6675-240">Hello 선택 **Azure 리소스 그룹 배포** 빌드 단계 및 해당 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-240">Choose hello **Azure Resource Group Deployment** build step and then fill in its values.</span></span>
   
   * <span data-ttu-id="b6675-241">Azure 연결 형식 - **Azure Resource Manager** 선택</span><span class="sxs-lookup"><span data-stu-id="b6675-241">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="b6675-242">Azure RM 구독-hello에 대 한 배포에 대 한 선택 hello 구독 **Azure 구독** 드롭다운 목록 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-242">Azure RM Subscription - select hello subscription for deployment in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="b6675-243">동일한 구독에 사용 되는 hello hello 이전 단계에서 일반적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-243">This will usually be hello same subscription used in hello previous step</span></span>
   * <span data-ttu-id="b6675-244">작업 - **리소스 그룹 만들기 또는 업데이트** 선택</span><span class="sxs-lookup"><span data-stu-id="b6675-244">Action - select **Create or Update Resource Group**</span></span>
   * <span data-ttu-id="b6675-245">리소스 그룹-리소스 그룹 이름 선택 또는 입력 hello 새 리소스 그룹의 hello 배포에 대 한</span><span class="sxs-lookup"><span data-stu-id="b6675-245">Resource Group - select a resource group or enter hello name of a new resource group for hello deployment</span></span>
   * <span data-ttu-id="b6675-246">위치-hello 리소스 그룹에 대 한 선택 hello 위치</span><span class="sxs-lookup"><span data-stu-id="b6675-246">Location - select hello location for hello resource group</span></span>
   * <span data-ttu-id="b6675-247">템플릿의 경우-hello 템플릿 배포 toobe 앞의 hello 경로 이름을 입력 **$(Build.StagingDirectory)**예를 들면: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span><span class="sxs-lookup"><span data-stu-id="b6675-247">Template - enter hello path and name of hello template toobe deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span></span>
   * <span data-ttu-id="b6675-248">템플릿 매개 변수-입력을 사용 하는 hello 매개 변수 toobe의 hello 경로 이름 앞에 추가 **$(Build.StagingDirectory)**예를 들면: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span><span class="sxs-lookup"><span data-stu-id="b6675-248">Template Parameters - enter hello path and name of hello parameters toobe used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span></span>
   * <span data-ttu-id="b6675-249">템플릿 매개 변수 재정의-입력 하거나 복사 하 코드 다음 hello를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-249">Override Template Parameters - enter or copy and paste hello following code:</span></span>
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Azure 리소스 그룹 배포 작업 구성][17]
7. <span data-ttu-id="b6675-251">모든 필요한 hello 항목을 추가한 후 hello 빌드 정의 저장 하 고 선택 **새 빌드 큐 대기** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-251">After you’ve added all hello required items, save hello build definition and choose **Queue new build** at hello top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6675-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6675-252">Next steps</span></span>
<span data-ttu-id="b6675-253">읽기 [Azure 리소스 관리자 개요](azure-resource-manager/resource-group-overview.md) toolearn Azure 리소스 관리자 및 Azure 리소스 그룹에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6675-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) toolearn more about Azure Resource Manager and Azure resource groups.</span></span>

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
