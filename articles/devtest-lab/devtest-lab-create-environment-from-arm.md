---
title: "Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 Azure DevTest Labs에 다중 VM 환경 및 PaaS 리소스를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4e1aae6c041e4572e7e2281203f969e7649e1480
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a><span data-ttu-id="bcf29-103">Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="bcf29-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>

<span data-ttu-id="bcf29-104">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)을 사용하면 쉽게 [랩에 VM을 만들고 추가](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-104">The [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you to easily [create and add a VM to a lab](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm).</span></span> <span data-ttu-id="bcf29-105">이 포털은 한 번에 하나씩 VM을 만드는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-105">This works well for creating one VM at a time.</span></span> <span data-ttu-id="bcf29-106">그러나 환경에서 여러 VM을 포함하는 경우 각 VM을 개별적으로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-106">However, if the environment contains multiple VMs, each VM has to be individually created.</span></span> <span data-ttu-id="bcf29-107">다중 계층 웹앱 또는 SharePoint 팜과 같은 시나리오의 경우 한 번에 여러 VM을 만들 수 있는 메커니즘이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed to allow for the creation of multiple VMs in a single step.</span></span> <span data-ttu-id="bcf29-108">Azure Resource Manager 템플릿을 사용하면 Azure 솔루션의 인프라와 구성을 정의하고 여러 VM을 일관된 상태로 반복적으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-108">By using Azure Resource Manager templates, you can now define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span> <span data-ttu-id="bcf29-109">이 기능은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-109">This feature provides the following benefits:</span></span>

- <span data-ttu-id="bcf29-110">Azure Resource Manager 템플릿은 소스 제어 리포지토리(GitHub 또는 Team Services Git)에서 직접 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span></span>
- <span data-ttu-id="bcf29-111">일단 구성되면 사용자가 Azure Portal에서 다른 유형의 [VM 자료](./devtest-lab-comparing-vm-base-image-types.md)를 처리할 수 있는 것처럼 Azure Resource Manager 템플릿을 선택하여 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from the Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span></span>
- <span data-ttu-id="bcf29-112">Azure Resource Manager 템플릿과 IaaS VM의 환경에서 Azure PaaS 리소스를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition to IaaS VMs.</span></span>
- <span data-ttu-id="bcf29-113">다른 유형의 자료로 만든 개별 VM 외에도 랩에서 환경의 비용을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-113">The cost of environments can be tracked in the lab in addition to individual VMs created by other types of bases.</span></span>
- <span data-ttu-id="bcf29-114">PaaS 리소스가 만들어지고 비용 추적에 표시되지만 VM 자동 종료는 PaaS 리소스에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-114">PaaS resources are created and will appear in cost tracking; however, VM auto shutdown does not apply to PaaS resources.</span></span>
- <span data-ttu-id="bcf29-115">사용자가 단일 랩 VM 환경과 동일한 VM 정책을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-115">Users have the same VM policy control for environments as they have for single-lab VMs.</span></span>

<span data-ttu-id="bcf29-116">단일 작업에서 모든 랩 리소스를 배포, 업데이트 또는 삭제하는 데 많은 [Resource Manager 템플릿 사용의 이점](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-116">Learn more about the many [benefits of using Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) to deploy, update, or delete all of your lab resources in a single operation.</span></span>

> [!NOTE]
> <span data-ttu-id="bcf29-117">더 많은 랩 VM을 만드는 기준으로 Resource Manager 템플릿을 사용하는 경우 다중 VM 또는 단일 VM을 만드는지 염두에 둘 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-117">When you use a Resource Manager template as a basis to create more lab VMs, there are some differences to keep in mind whether you are creating Multi-VMs or single-VMs.</span></span> <span data-ttu-id="bcf29-118">가상 컴퓨터의 Azure Resource Manager 템플릿 사용은 이러한 차이점을 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-118">Use a virtual machine's Azure Resource Manager template explains these differences in greater detail.</span></span>
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a><span data-ttu-id="bcf29-119">Azure Resource Manager 템플릿 리포지토리 구성</span><span class="sxs-lookup"><span data-stu-id="bcf29-119">Configure Azure Resource Manager template repositories</span></span>

<span data-ttu-id="bcf29-120">코드 기반 인프라와 코드 기반 구성을 사용하는 모범 사례 중 하나인 환경 템플릿은 소스 제어에서 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-120">As one of the best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span></span> <span data-ttu-id="bcf29-121">Azure DevTest Labs에서는 이 사례를 따르고 GitHub 또는 VSTS Git 리포지토리에서 직접 Azure Resource Manager 템플릿을 모두 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-121">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span></span> <span data-ttu-id="bcf29-122">결과적으로, Resource Manager 템플릿은 테스트 환경에서 프로덕션 환경까지 전체 릴리스 주기에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-122">As a result, Resource Manager templates can be used across the entire release cycle, from the test environment to the production environment.</span></span>

<span data-ttu-id="bcf29-123">리포지토리에 Azure Resource Manager 템플릿을 구성하는 따라야 할 몇 가지 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-123">There are a couple of rules to follow to organize your Azure Resource Manager templates in a repository:</span></span>

- <span data-ttu-id="bcf29-124">마스터 템플릿 파일의 이름은 `azuredeploy.json`으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-124">The master template file must be named `azuredeploy.json`.</span></span> 

    ![주요 Azure Resource Manager 템플릿 파일](./media/devtest-lab-create-environment-from-arm/master-template.png)

- <span data-ttu-id="bcf29-126">매개 변수 파일에 정의한 매개 변수 값을 사용하려면 매개 변수 파일의 이름을 `azuredeploy.parameters.json`으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-126">If you want to use parameter values defined in a parameter file, the parameter file must be named `azuredeploy.parameters.json`.</span></span>
- <span data-ttu-id="bcf29-127">DevTest Labs에서 중첩된 템플릿을 자동으로 관리할 수 있도록 매개 변수 `_artifactsLocation` 및 `_artifactsLocationSasToken`을 사용하여 parametersLink URI 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-127">You can use the parameters `_artifactsLocation` and `_artifactsLocationSasToken` to construct the parametersLink URI value, allowing DevTest Labs to automatically manage nested templates.</span></span> <span data-ttu-id="bcf29-128">자세한 내용은 [Azure DevTest Labs에서 테스트 환경에 대해 더 쉽게 중첩된 Resource Manager 템플릿 배포를 만드는 방법](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bcf29-128">See [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) for more information.</span></span>
- <span data-ttu-id="bcf29-129">템플릿 표시 이름과 설명을 지정하기 위해 메타데이터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-129">Metadata can be defined to specify the template display name and description.</span></span> <span data-ttu-id="bcf29-130">이 메타데이터는 `metadata.json`이라는 파일에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-130">This metadata must be in a file named `metadata.json`.</span></span> <span data-ttu-id="bcf29-131">다음 예제 메타데이터 파일에서는 표시 이름과 설명을 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-131">The following example metadata file illustrates how to specify the display name and description:</span></span> 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of the template>"
 
}
```

<span data-ttu-id="bcf29-132">다음 단계는 Azure Portal을 사용하여 랩에 리포지토리를 추가하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-132">The following steps guide you through adding a repository to your lab using the Azure portal.</span></span> 

1. <span data-ttu-id="bcf29-133">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-133">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bcf29-134">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-134">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="bcf29-135">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-135">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="bcf29-136">랩의 블레이드에서 **구성 및 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-136">On the lab's blade, select **Configuration and Policies**.</span></span>

    ![구성 및 정책](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. <span data-ttu-id="bcf29-138">**구성 및 정책** 설정 목록에서 **리포지토리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-138">From the **Configuration and Policies** settings list, select **Repositories**.</span></span> <span data-ttu-id="bcf29-139">**리포지토리** 블레이드에서 랩에 추가된 리포지토리를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-139">The **Repositories** blade lists the repositories that have been added to the lab.</span></span> <span data-ttu-id="bcf29-140">모든 랩에 대해 `Public Repo`라는 리포지토리가 자동으로 생성되고 사용할 여러 VM 아티팩트를 포함하고 있는 [DevTest Labs GitHub 리포지토리](https://github.com/Azure/azure-devtestlab)에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-140">A repository named `Public Repo` is automatically generated for all labs, and connects to the [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span></span>

    ![공용 리포지토리](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. <span data-ttu-id="bcf29-142">**추가+**를 선택하여 Azure Resource Manager 템플릿 리포지토리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-142">Select **Add+** to add your Azure Resource Manager template repository.</span></span>
1. <span data-ttu-id="bcf29-143">두 번째 **리포지토리** 블레이드가 열리면 다음과 같이 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-143">When the second **Repositories** blade opens, enter the necessary information as follows:</span></span>
    - <span data-ttu-id="bcf29-144">**이름** - 랩에서 사용되는 리포지토리 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-144">**Name** - Enter the repository name that is used in the lab.</span></span>
    - <span data-ttu-id="bcf29-145">**Git 복제 URL** - GitHub 또는 Visual Studio Team Services의 GIT HTTPS 복제 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-145">**Git clone URL** - Enter the GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span></span>  
    - <span data-ttu-id="bcf29-146">**분기** - Azure Resource Manager 템플릿 정의에 액세스하기 위한 분기 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-146">**Branch** - Enter the branch name to access your Azure Resource Manager template definitions.</span></span> 
    - <span data-ttu-id="bcf29-147">**개인 액세스 토큰** - 개인 액세스 토큰은 리포지토리에 안전하게 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-147">**Personal access token** - The personal access token is used to securely access your repository.</span></span> <span data-ttu-id="bcf29-148">Visual Studio Team Services에서 토큰을 가져오려면 **&lt;YourName>> 내 프로필> 보안> 공용 액세스 토큰**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-148">To get your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span></span> <span data-ttu-id="bcf29-149">GitHub에서 토큰을 가져오려면 **설정 > 공용 액세스 토큰**을 선택한 다음 아바타를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-149">To get your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span></span> 
    - <span data-ttu-id="bcf29-150">**폴더 경로** - 두 입력 필드 중 하나를 사용하여 슬래시(/)로 시작하는 폴더 경로를 입력합니다. 이 경로는 아티팩트 정의(첫 번째 입력 필드) 또는 Azure Resource Manager 템플릿 정의에 대한 Git 복제 URI의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-150">**Folder paths** - Using one of the two input fields, enter the folder path that starts with a forward slash - / - and is relative to your Git clone URI to either your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span></span>   
    
        ![공용 리포지토리](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. <span data-ttu-id="bcf29-152">필수 필드를 모두 입력하고 유효성 검사를 통과하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-152">Once all the required fields are entered and pass the validation, select **Save**.</span></span>

<span data-ttu-id="bcf29-153">다음 섹션에서는 Azure Resource Manager 템플릿에서 환경을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-153">The next section will walk you through creating environments from an Azure Resource Manager template.</span></span>

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a><span data-ttu-id="bcf29-154">Azure Resource Manager 템플릿에서 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="bcf29-154">Create an environment from an Azure Resource Manager template</span></span>

<span data-ttu-id="bcf29-155">랩에 Azure Resource Manager 템플릿 리포지토리를 구성한 후에 랩 사용자는 Azure Portal을 사용하여 다음 단계에 따라 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-155">Once an Azure Resource Manager template repository has been configured in the lab, your lab users can create an environment using Azure portal with the following steps:</span></span>

1. <span data-ttu-id="bcf29-156">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-156">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bcf29-157">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-157">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="bcf29-158">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-158">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="bcf29-159">랩의 블레이드에서 **추가+**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-159">On the lab's blade, select **Add+**.</span></span>
1. <span data-ttu-id="bcf29-160">**기본 선택** 블레이드에는 먼저 나열된 Azure Resource Manager 템플릿에서 사용할 수 있는 기본 이미지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-160">The **Choose a base** blade displays the base images you can use with the Azure Resource Manager templates listed first.</span></span> <span data-ttu-id="bcf29-161">원하는 Azure Resource Manager 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-161">Select the desired Azure Resource Manager template.</span></span>

    ![기본 선택](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. <span data-ttu-id="bcf29-163">**추가** 블레이드에서 **환경 이름** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-163">On the **Add** blade, enter the **Environment name** value.</span></span> <span data-ttu-id="bcf29-164">환경 이름은 랩에서 사용자에게 표시되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-164">The environment name is what is displayed to your users in the lab.</span></span> <span data-ttu-id="bcf29-165">나머지 입력 필드는 Azure Resource Manager 템플릿에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-165">The remaining input fields are defined in the Azure Resource Manager template.</span></span> <span data-ttu-id="bcf29-166">기본값이 템플릿에 정의되어 있거나 `azuredeploy.parameter.json` 파일이 있으면 해당 입력 필드에 기본값이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-166">If default values are defined in the template or the `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span></span> <span data-ttu-id="bcf29-167">*보안 문자열* 형식의 매개 변수에는 랩의 [개인 비밀 저장소](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)에 저장된 비밀을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-167">For parameters of type *secure string*, you can use the secrets stored in the lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span></span>

    ![추가 블레이드](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > <span data-ttu-id="bcf29-169">지정된 경우에도 빈 값으로 표시되는 몇 가지 매개 변수 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-169">There are several parameter values that - even if specified - are displayed as empty values.</span></span> <span data-ttu-id="bcf29-170">따라서 사용자가 Azure Resource Manager 템플릿의 매개 변수에 해당 값을 할당하면 DevTest Labs에서는 값을 표시하지 않는 대신 랩 사용자가 환경을 만들 때 값을 입력해야 하는 입력 필드를 빈 상태로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-170">Therefore, if users assign those values to parameters in an Azure Resource Manager template, DevTest Labs does not display the values; instead showing blank input fields where the lab users need to enter a value when creating the environment.</span></span>
    > 
    > - <span data-ttu-id="bcf29-171">GEN-UNIQUE</span><span class="sxs-lookup"><span data-stu-id="bcf29-171">GEN-UNIQUE</span></span>
    > - <span data-ttu-id="bcf29-172">GEN-UNIQUE-[N]</span><span class="sxs-lookup"><span data-stu-id="bcf29-172">GEN-UNIQUE-[N]</span></span>
    > - <span data-ttu-id="bcf29-173">GEN-SSH-PUB-KEY</span><span class="sxs-lookup"><span data-stu-id="bcf29-173">GEN-SSH-PUB-KEY</span></span>
    > - <span data-ttu-id="bcf29-174">GEN-PASSWORD</span><span class="sxs-lookup"><span data-stu-id="bcf29-174">GEN-PASSWORD</span></span> 
 
1. <span data-ttu-id="bcf29-175">**추가**를 선택하여 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-175">Select **Add** to create the environment.</span></span> <span data-ttu-id="bcf29-176">환경에서는 **내 가상 컴퓨터** 목록에 상태를 표시하는 즉시 프로비전을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-176">The environment starts provisioning immediately with the status displaying in the **My virtual machines** list.</span></span> <span data-ttu-id="bcf29-177">Azure Resource Manager 템플릿에 정의된 모든 리소스를 프로비전하기 위해 랩에서 새 리소스 그룹을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-177">A new resource group is automatically created by the lab to provision all the resources defined in the Azure Resource Manager template.</span></span>
1. <span data-ttu-id="bcf29-178">환경이 만들어지면 **내 가상 컴퓨터** 목록에서 환경을 선택하여 리소스 그룹 블레이드를 열고 환경에 프로비전된 모든 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-178">Once the environment is created, select the environment in the **My virtual machines** list to open the resource group blade and browse all of the resources provisioned in the environment.</span></span>
    
    ![내 가상 컴퓨터 목록](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   <span data-ttu-id="bcf29-180">또한 환경을 확장하여 환경에서 프로비전되는 VM의 목록만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-180">You can also expand the environment to view just the list of VMs that are provisioned in the environment.</span></span>
    
    ![내 가상 컴퓨터 목록](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. <span data-ttu-id="bcf29-182">환경을 클릭하여 아티팩트 적용, 데이터 디스크 연결, 자동 종료 시간 변경 등과 같은 사용 가능한 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-182">Click any of the environments to view the available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span></span>

    ![환경 작업](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a><span data-ttu-id="bcf29-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcf29-184">Next steps</span></span>
* <span data-ttu-id="bcf29-185">VM을 만든 후에는 해당 VM의 블레이드에서 **연결** 을 선택하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-185">Once a VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="bcf29-186">랩의 **내 가상 컴퓨터** 목록에서 환경을 선택하여 환경에서 리소스를 보고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-186">View and manage resources in an environment by selecting the environment in the **My virtual machines** list in your lab.</span></span> 
* <span data-ttu-id="bcf29-187">[Azure 빠른 시작 템플릿 갤러리의 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates)(영문)을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="bcf29-187">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span></span>
