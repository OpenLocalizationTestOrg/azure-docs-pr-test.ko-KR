---
title: "aaaCreate 다중 VM 환경 및 Azure 리소스 관리자 템플릿 사용 하 여 PaaS 리소스 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 다중 VM 환경 및 Azure 리소스 관리자 템플릿에서 DevTest Labs Azure에서에서 PaaS 리소스"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a><span data-ttu-id="c818a-103">Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="c818a-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>

<span data-ttu-id="c818a-104">hello [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooeasily를 사용 하면 [만들고 추가 VM tooa 랩](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-104">hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you tooeasily [create and add a VM tooa lab](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm).</span></span> <span data-ttu-id="c818a-105">이 포털은 한 번에 하나씩 VM을 만드는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-105">This works well for creating one VM at a time.</span></span> <span data-ttu-id="c818a-106">그러나 hello 환경에서 여러 Vm가 포함 된 경우 각 VM에 toobe 개별적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-106">However, if hello environment contains multiple VMs, each VM has toobe individually created.</span></span> <span data-ttu-id="c818a-107">예: 다층 계층 웹 응용 프로그램 또는 SharePoint 팜의 시나리오의 경우는 메커니즘은 한 번에 여러 Vm hello 생성에 필요한 tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed tooallow for hello creation of multiple VMs in a single step.</span></span> <span data-ttu-id="c818a-108">Azure 리소스 관리자 템플릿을 사용 하 여 이제 hello 인프라 및 Azure 솔루션의 구성을 정의할 수 있으며 반복적으로 일관 된 상태에서 여러 Vm을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-108">By using Azure Resource Manager templates, you can now define hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span> <span data-ttu-id="c818a-109">이 기능은 hello를 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-109">This feature provides hello following benefits:</span></span>

- <span data-ttu-id="c818a-110">Azure Resource Manager 템플릿은 소스 제어 리포지토리(GitHub 또는 Team Services Git)에서 직접 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span></span>
- <span data-ttu-id="c818a-111">사용자에 게는 Azure 리소스 관리자 템플릿을 hello와 다른 형식 수 있는 작업으로 Azure 포털에서에서 선택 하 여 환경을 만들 수 구성 되 면 [VM 자료](./devtest-lab-comparing-vm-base-image-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from hello Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span></span>
- <span data-ttu-id="c818a-112">또한 tooIaaS Vm에에서 Azure 리소스 관리자 템플릿을 환경에 azure PaaS 리소스를 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition tooIaaS VMs.</span></span>
- <span data-ttu-id="c818a-113">또한 tooindividual 밑의 다른 형식에 의해 만들어진 Vm의에서 hello 랩에서 환경의 hello 비용을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-113">hello cost of environments can be tracked in hello lab in addition tooindividual VMs created by other types of bases.</span></span>
- <span data-ttu-id="c818a-114">PaaS 리소스 만들어집니다 및 비용 관리;에 표시 됩니다. 그러나 VM 자동 종료 tooPaaS 리소스 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-114">PaaS resources are created and will appear in cost tracking; however, VM auto shutdown does not apply tooPaaS resources.</span></span>
- <span data-ttu-id="c818a-115">사용자가 단일 랩 Vm에 대 한 것 같은 VM 정책 제어 환경에 대 한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-115">Users have hello same VM policy control for environments as they have for single-lab VMs.</span></span>

<span data-ttu-id="c818a-116">에 대 한 자세한 hello 많은 [리소스 관리자 템플릿을 사용의 이점](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, 업데이트 또는 단일 작업에서 랩 리소스를 모두 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-116">Learn more about hello many [benefits of using Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, update, or delete all of your lab resources in a single operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c818a-117">를 사용 하면 리소스 관리자 템플릿을 별로 toocreate로 더 많은 랩 Vm 있는 경우 몇 가지 차이점 tookeep 염두에서 다중 Vm 또는 단일 Vm을 만들거나</span><span class="sxs-lookup"><span data-stu-id="c818a-117">When you use a Resource Manager template as a basis toocreate more lab VMs, there are some differences tookeep in mind whether you are creating Multi-VMs or single-VMs.</span></span> <span data-ttu-id="c818a-118">가상 컴퓨터의 Azure Resource Manager 템플릿 사용은 이러한 차이점을 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-118">Use a virtual machine's Azure Resource Manager template explains these differences in greater detail.</span></span>
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a><span data-ttu-id="c818a-119">Azure Resource Manager 템플릿 리포지토리 구성</span><span class="sxs-lookup"><span data-stu-id="c818a-119">Configure Azure Resource Manager template repositories</span></span>

<span data-ttu-id="c818a-120">Hello 중 하나로 된 인프라로 코드 및 코드와 구성, 환경 템플릿 모범 사례를 소스 제어에서 관리 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-120">As one of hello best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span></span> <span data-ttu-id="c818a-121">Azure DevTest Labs에서는 이 사례를 따르고 GitHub 또는 VSTS Git 리포지토리에서 직접 Azure Resource Manager 템플릿을 모두 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-121">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span></span> <span data-ttu-id="c818a-122">결과적으로, 리소스 관리자 템플릿은 hello 테스트 환경 toohello 프로덕션 환경에서 hello 전체 릴리스 주기에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-122">As a result, Resource Manager templates can be used across hello entire release cycle, from hello test environment toohello production environment.</span></span>

<span data-ttu-id="c818a-123">두 가지가 규칙 toofollow tooorganize의 Azure 리소스 관리자 템플릿을 저장소에서:</span><span class="sxs-lookup"><span data-stu-id="c818a-123">There are a couple of rules toofollow tooorganize your Azure Resource Manager templates in a repository:</span></span>

- <span data-ttu-id="c818a-124">hello 마스터 템플릿 파일 이름을 지정 해야 `azuredeploy.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-124">hello master template file must be named `azuredeploy.json`.</span></span> 

    ![주요 Azure Resource Manager 템플릿 파일](./media/devtest-lab-create-environment-from-arm/master-template.png)

- <span data-ttu-id="c818a-126">매개 변수 파일에 정의 된 toouse 매개 변수 값을 원하는 hello 매개 변수 파일 이름을 지정 해야 `azuredeploy.parameters.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-126">If you want toouse parameter values defined in a parameter file, hello parameter file must be named `azuredeploy.parameters.json`.</span></span>
- <span data-ttu-id="c818a-127">Hello 매개 변수를 사용할 수 `_artifactsLocation` 및 `_artifactsLocationSasToken` tooconstruct hello parametersLink URI 값을 DevTest Labs tooautomatically 관리할 수 있도록 서식 파일을 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-127">You can use hello parameters `_artifactsLocation` and `_artifactsLocationSasToken` tooconstruct hello parametersLink URI value, allowing DevTest Labs tooautomatically manage nested templates.</span></span> <span data-ttu-id="c818a-128">자세한 내용은 [Azure DevTest Labs에서 테스트 환경에 대해 더 쉽게 중첩된 Resource Manager 템플릿 배포를 만드는 방법](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c818a-128">See [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) for more information.</span></span>
- <span data-ttu-id="c818a-129">메타 데이터 정의 toospecify hello 템플릿 표시 이름 및 설명을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-129">Metadata can be defined toospecify hello template display name and description.</span></span> <span data-ttu-id="c818a-130">이 메타데이터는 `metadata.json`이라는 파일에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-130">This metadata must be in a file named `metadata.json`.</span></span> <span data-ttu-id="c818a-131">hello 다음 예제에서는 메타 데이터 파일에서는 toospecify hello 이름 및 설명을 표시 하는 방법을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-131">hello following example metadata file illustrates how toospecify hello display name and description:</span></span> 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

<span data-ttu-id="c818a-132">hello 다음 단계를 안내해 hello Azure 포털을 사용 하 여 저장소 tooyour 랩을 추가 하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-132">hello following steps guide you through adding a repository tooyour lab using hello Azure portal.</span></span> 

1. <span data-ttu-id="c818a-133">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-133">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="c818a-134">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-134">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="c818a-135">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-135">From hello list of labs, select hello desired lab.</span></span>   
1. <span data-ttu-id="c818a-136">Hello 랩 블레이드에서 선택 **구성 및 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-136">On hello lab's blade, select **Configuration and Policies**.</span></span>

    ![구성 및 정책](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. <span data-ttu-id="c818a-138">Hello에서 **구성 및 정책** 설정 목록 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-138">From hello **Configuration and Policies** settings list, select **Repositories**.</span></span> <span data-ttu-id="c818a-139">hello **저장소** 블레이드에 toohello 랩 추가 된 hello 저장소를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-139">hello **Repositories** blade lists hello repositories that have been added toohello lab.</span></span> <span data-ttu-id="c818a-140">라는 리포지토리 `Public Repo` 모든 랩에 대 한 자동으로 생성 되 고 toohello 연결 [DevTest Labs GitHub 리포지토리](https://github.com/Azure/azure-devtestlab) 사용에 대 한 여러 VM 아티팩트를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-140">A repository named `Public Repo` is automatically generated for all labs, and connects toohello [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span></span>

    ![공용 리포지토리](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. <span data-ttu-id="c818a-142">선택 **추가 +** tooadd Azure 리소스 관리자 템플릿 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-142">Select **Add+** tooadd your Azure Resource Manager template repository.</span></span>
1. <span data-ttu-id="c818a-143">둘째 hello 때 **저장소** 블레이드에서 열립니다 hello 필요한 정보를 다음과 같이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-143">When hello second **Repositories** blade opens, enter hello necessary information as follows:</span></span>
    - <span data-ttu-id="c818a-144">**이름** -hello 랩에서 사용 되는 hello 리포지토리 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-144">**Name** - Enter hello repository name that is used in hello lab.</span></span>
    - <span data-ttu-id="c818a-145">**Git 복제 URL** -GitHub 또는 Visual Studio Team Services hello GIT HTTPS 클론 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-145">**Git clone URL** - Enter hello GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span></span>  
    - <span data-ttu-id="c818a-146">**분기** -hello 분기 이름 tooaccess Azure 리소스 관리자 템플릿 정의 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-146">**Branch** - Enter hello branch name tooaccess your Azure Resource Manager template definitions.</span></span> 
    - <span data-ttu-id="c818a-147">**개인용 액세스 토큰** -hello 개인용 액세스 토큰은 사용 toosecurely 저장소에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-147">**Personal access token** - hello personal access token is used toosecurely access your repository.</span></span> <span data-ttu-id="c818a-148">Visual Studio Team Services에서 토큰 선택 tooget  **&lt;YourName >> 내 프로필 > 보안 > 공용 액세스 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-148">tooget your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span></span> <span data-ttu-id="c818a-149">GitHub에서 토큰 뒤에 선택 하 여 아바타를 선택 tooget **설정 > 공용 액세스 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-149">tooget your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span></span> 
    - <span data-ttu-id="c818a-150">**폴더 경로** -슬래시-/-로 시작 하는 hello 폴더 경로 입력 hello 두 입력된 필드 중 하나를 사용 하 여 하 고 상대 tooyour Git clone URI tooeither 아티팩트 정의 됩니다 (첫 번째 입력된 필드) 또는 Azure 리소스 관리자 템플릿 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-150">**Folder paths** - Using one of hello two input fields, enter hello folder path that starts with a forward slash - / - and is relative tooyour Git clone URI tooeither your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span></span>   
    
        ![공용 리포지토리](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. <span data-ttu-id="c818a-152">모든 필수 hello 필드를 입력 하 고 hello 유효성 검사를 통과, 선택할 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-152">Once all hello required fields are entered and pass hello validation, select **Save**.</span></span>

<span data-ttu-id="c818a-153">hello 다음 섹션에서 Azure 리소스 관리자 템플릿을 환경을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-153">hello next section will walk you through creating environments from an Azure Resource Manager template.</span></span>

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a><span data-ttu-id="c818a-154">Azure Resource Manager 템플릿에서 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="c818a-154">Create an environment from an Azure Resource Manager template</span></span>

<span data-ttu-id="c818a-155">Hello 랩에서 Azure 리소스 관리자 템플릿 리포지토리를 구성한 후 랩 사용자가 Azure 포털을 사용 하 여 단계를 수행 하는 hello로 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-155">Once an Azure Resource Manager template repository has been configured in hello lab, your lab users can create an environment using Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="c818a-156">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-156">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="c818a-157">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-157">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="c818a-158">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-158">From hello list of labs, select hello desired lab.</span></span>   
1. <span data-ttu-id="c818a-159">Hello 랩 블레이드에서 선택 **추가 +**합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-159">On hello lab's blade, select **Add+**.</span></span>
1. <span data-ttu-id="c818a-160">hello **기본 선택** 블레이드 첫 번째로 나열 hello Azure 리소스 관리자 템플릿으로 사용할 수는 hello 기본 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-160">hello **Choose a base** blade displays hello base images you can use with hello Azure Resource Manager templates listed first.</span></span> <span data-ttu-id="c818a-161">Select hello Azure 리소스 관리자 템플릿을 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-161">Select hello desired Azure Resource Manager template.</span></span>

    ![기본 선택](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. <span data-ttu-id="c818a-163">Hello에 **추가** 블레이드에서 hello 입력 **환경 이름** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-163">On hello **Add** blade, enter hello **Environment name** value.</span></span> <span data-ttu-id="c818a-164">hello 환경 이름은 이란 hello 랩에서 표시 tooyour 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-164">hello environment name is what is displayed tooyour users in hello lab.</span></span> <span data-ttu-id="c818a-165">hello 나머지 입력된 필드 hello Azure 리소스 관리자 서식 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-165">hello remaining input fields are defined in hello Azure Resource Manager template.</span></span> <span data-ttu-id="c818a-166">Hello 템플릿이나 hello에 기본값이 정의 된 경우 `azuredeploy.parameter.json` 파일이 있는지, 해당 입력된 필드에 기본값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-166">If default values are defined in hello template or hello `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span></span> <span data-ttu-id="c818a-167">형식의 매개 변수로 *보안 문자열*, hello 랩에 저장 된 hello 암호를 사용할 수 있습니다 [개인 비밀 저장소](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-167">For parameters of type *secure string*, you can use hello secrets stored in hello lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span></span>

    ![추가 블레이드](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > <span data-ttu-id="c818a-169">지정된 경우에도 빈 값으로 표시되는 몇 가지 매개 변수 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-169">There are several parameter values that - even if specified - are displayed as empty values.</span></span> <span data-ttu-id="c818a-170">따라서 이러한 값 tooparameters Azure Resource Manager 템플릿에 할당 하는 사용자, DevTest Labs 표시 되지 않습니다 hello 값이 있습니다. 대신 값을 보여 주는 hello 랩 필요한 tooenter 빈 입력된 필드 hello 환경을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="c818a-170">Therefore, if users assign those values tooparameters in an Azure Resource Manager template, DevTest Labs does not display hello values; instead showing blank input fields where hello lab users need tooenter a value when creating hello environment.</span></span>
    > 
    > - <span data-ttu-id="c818a-171">GEN-UNIQUE</span><span class="sxs-lookup"><span data-stu-id="c818a-171">GEN-UNIQUE</span></span>
    > - <span data-ttu-id="c818a-172">GEN-UNIQUE-[N]</span><span class="sxs-lookup"><span data-stu-id="c818a-172">GEN-UNIQUE-[N]</span></span>
    > - <span data-ttu-id="c818a-173">GEN-SSH-PUB-KEY</span><span class="sxs-lookup"><span data-stu-id="c818a-173">GEN-SSH-PUB-KEY</span></span>
    > - <span data-ttu-id="c818a-174">GEN-PASSWORD</span><span class="sxs-lookup"><span data-stu-id="c818a-174">GEN-PASSWORD</span></span> 
 
1. <span data-ttu-id="c818a-175">선택 **추가** toocreate hello 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-175">Select **Add** toocreate hello environment.</span></span> <span data-ttu-id="c818a-176">hello 환경을 즉시 hello에 표시 하는 hello 상태와 함께 프로 비전을 시작할 **내 가상 컴퓨터** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-176">hello environment starts provisioning immediately with hello status displaying in hello **My virtual machines** list.</span></span> <span data-ttu-id="c818a-177">새 리소스 그룹이 자동으로 생성 됩니다 hello 랩 tooprovision hello Azure Resource Manager 템플릿에 정의 된 모든 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-177">A new resource group is automatically created by hello lab tooprovision all hello resources defined in hello Azure Resource Manager template.</span></span>
1. <span data-ttu-id="c818a-178">Hello 환경 만들어지면 hello에 hello 환경을 선택 **내 가상 컴퓨터** tooopen hello 리소스 그룹 블레이드를 나열 하 고 모든 hello 환경에서 사용자를 프로 비전 하는 hello 리소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-178">Once hello environment is created, select hello environment in hello **My virtual machines** list tooopen hello resource group blade and browse all of hello resources provisioned in hello environment.</span></span>
    
    ![내 가상 컴퓨터 목록](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   <span data-ttu-id="c818a-180">Hello 환경에서 프로 비전 되는 Vm의 hello 환경 tooview 정당한 hello 목록을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-180">You can also expand hello environment tooview just hello list of VMs that are provisioned in hello environment.</span></span>
    
    ![내 가상 컴퓨터 목록](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. <span data-ttu-id="c818a-182">Hello 환경 tooview hello 사용 가능한 작업-아티팩트를 연결 하 고 데이터 디스크, 변경 자동 종료 시간 등을 적용 하는 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-182">Click any of hello environments tooview hello available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span></span>

    ![환경 작업](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a><span data-ttu-id="c818a-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c818a-184">Next steps</span></span>
* <span data-ttu-id="c818a-185">VM을 만든 후 toohello VM을 선택 하 여 연결할 수 있습니다 **연결** hello VM 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-185">Once a VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="c818a-186">보기 및 hello에 hello 환경을 선택 하 여 환경에서 리소스를 관리할 **내 가상 컴퓨터** 랩의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c818a-186">View and manage resources in an environment by selecting hello environment in hello **My virtual machines** list in your lab.</span></span> 
* <span data-ttu-id="c818a-187">Hello 탐색 [Azure 빠른 시작 템플릿 갤러리에서 Azure 리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates)</span><span class="sxs-lookup"><span data-stu-id="c818a-187">Explore hello [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span></span>
