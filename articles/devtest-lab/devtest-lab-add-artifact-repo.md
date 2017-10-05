---
title: "Azure DevTest Labs의 랩에 Git 리포지토리 추가 | Microsoft Docs"
description: "Azure DevTest Labs에서 사용자 지정 아티팩트 원본용 GitHub 또는 Visual Studio Team Services Git 리포지토리 추가"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 053f92a65f9ae29154d471fd22ee842620b4f273
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates"></a><span data-ttu-id="435e4-103">사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 저장할 Git 리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="435e4-103">Add a Git repository to store custom artifacts and Azure Resource Manager templates</span></span>

<span data-ttu-id="435e4-104">랩에서 VM의 [사용자 지정 아티팩트를 만들거나](devtest-lab-artifact-author.md) [Azure Resource Manager 템플릿을 사용하여 사용자 지정 테스트 환경을 만들려는](devtest-lab-create-environment-from-arm.md) 경우 팀이 만드는 아티팩트 또는 Azure Resource Manager 템플릿을 포함할 개인 Git 리포지토리도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-104">If you want to [create custom artifacts](devtest-lab-artifact-author.md) for the VMs in your lab, or [use Azure Resource Manager templates to create a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository to include the artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="435e4-105">리포지토리는 [GitHub](https://github.com) 또는 [VSTS(Visual Studio Team Services)](https://visualstudio.com)에서 호스팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-105">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="435e4-106">Microsoft는 그대로 배포하거나 랩에 맞게 사용자 지정할 수 있는 [아티팩트의 Github 리포지토리](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="435e4-107">아티팩트를 사용자 지정하거나 만들 경우 공용 리포지토리에 저장할 수 없으며 개인 리포지토리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-107">When you customize or create an artifact, you cannot store them in the public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="435e4-108">VM을 만들 경우 Azure Resource Manager 템플릿을 저장하고 원할 경우 사용자 지정한 다음 나중에 추가 VM을 손쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-108">When you create a VM, you can save the Azure Resource Manager template, customize it if you want, and then use it later to easily create more VMs.</span></span> <span data-ttu-id="435e4-109">사용자 지정 Azure Resource Manager 템플릿을 저장할 개인 리포지토리를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-109">You must create your own private repository to store your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="435e4-110">GitHub 리포지토리를 만드는 방법을 알아보려면 [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435e4-110">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="435e4-111">Git 리포지토리를 사용하여 Team Services 프로젝트를 만드는 방법을 알아보려면 [Visual Studio Team Services에 연결](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="435e4-111">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="435e4-112">다음 스크린샷에서는 아티팩트가 포함된 리포지토리가 GitHub에서 어떻게 표시되는지 보여 주는 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-112">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![GitHub 아티팩트 리포지토리 샘플](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a><span data-ttu-id="435e4-114">리포지토리 정보 및 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="435e4-114">Get the repository information and credentials</span></span>
<span data-ttu-id="435e4-115">랩에 리포지토리를 추가하려면 먼저 리포지토리에서 특정 정보를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-115">To add a repository to your lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="435e4-116">다음 섹션에서는 GitHub 및 Visual Studio Team Services에서 호스트되는 리포지토리에 대해 이러한 정보를 가져오는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-116">The following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="435e4-117">GitHub 리포지토리 복제 URL 및 개인 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="435e4-117">Get the GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="435e4-118">GitHub 리포지토리 복제 URL 및 개인 액세스 토큰을 가져오려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="435e4-118">To get the GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="435e4-119">아티팩트 또는 Azure Resource Manager 템플릿 정의를 포함하는 GitHub 리포지토리의 홈 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-119">Browse to the home page of the GitHub repository that contains the artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="435e4-120">**복제 또는 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="435e4-121">이 단추를 선택하여 **HTTPS 복제 URL** 을 클립보드에 복사하고 나중에 사용할 수 있게 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-121">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span></span>
4. <span data-ttu-id="435e4-122">GitHub의 오른쪽 위에서 프로필 이미지를 탭하고 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-122">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="435e4-123">왼쪽의 **개인 설정** 메뉴에서 **개인 액세스 토큰**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-123">In the **Personal settings** menu on the left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="435e4-124">**Generate new token**(새 토큰 생성)을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="435e4-125">**새 개인 액세스 토큰** 페이지에서 **토큰 설명**을 입력하고 **범위 선택**에서 기본 항목을 수락한 다음 **토큰 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-125">On the **New personal access token** page, enter a **Token description**, accept the default items in the **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="435e4-126">나중에 필요하므로 생성한 토큰을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-126">Save the generated token as you need it later.</span></span>
9. <span data-ttu-id="435e4-127">이제 GitHub를 닫아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="435e4-128">[리포지토리에 랩 연결](#connect-your-lab-to-the-repository) 섹션을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-128">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="435e4-129">Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="435e4-129">Get the Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="435e4-130">Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰을 가져오려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="435e4-130">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="435e4-131">팀 컬렉션의 홈페이지(예: `https://contoso-web-team.visualstudio.com`)를 연 다음 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-131">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="435e4-132">프로젝트 홈 페이지에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-132">On the project home page, select **Code**.</span></span>
3. <span data-ttu-id="435e4-133">복제 URL을 보려면 프로젝트 **코드** 페이지에서 **복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-133">To view the clone URL, on the project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="435e4-134">이 자습서의 뒷부분에서 필요하므로 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-134">Save the URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="435e4-135">개인 액세스 토큰을 만들려면 사용자 계정 드롭다운 메뉴에서 **내 프로필** 을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-135">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span></span>
6. <span data-ttu-id="435e4-136">프로필 정보 페이지에서 **보안**을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-136">On the profile information page, select **Security**.</span></span>
7. <span data-ttu-id="435e4-137">**보안** 탭에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-137">On the **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="435e4-138">**개인 액세스 토큰 만들기** 페이지에서</span><span class="sxs-lookup"><span data-stu-id="435e4-138">In the **Create a personal access token** page:</span></span>

   * <span data-ttu-id="435e4-139">토큰에 대한 **설명** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-139">Enter a **Description** for the token.</span></span>
   * <span data-ttu-id="435e4-140">**다음 기간 내에 만료** 목록에서 **180일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-140">Select **180 days** from the **Expires In** list.</span></span>
   * <span data-ttu-id="435e4-141">**계정** 목록에서 **액세스 가능한 모든 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-141">Choose **All accessible accounts** from the **Accounts** list.</span></span>
   * <span data-ttu-id="435e4-142">**모든 범위** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-142">Choose the **All scopes** option.</span></span>
   * <span data-ttu-id="435e4-143">**토큰 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="435e4-144">완료되면 새 토큰이 **개인 액세스 토큰** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-144">When finished, the new token appears in the **Personal Access Tokens** list.</span></span> <span data-ttu-id="435e4-145">**토큰 복사**를 선택하고 나중에 사용할 수 있게 토큰 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-145">Select **Copy Token**, and then save the token value for later use.</span></span>
10. <span data-ttu-id="435e4-146">[리포지토리에 랩 연결](#connect-your-lab-to-the-repository) 섹션을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-146">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-to-the-repository"></a><span data-ttu-id="435e4-147">랩을 리포지토리에 연결</span><span class="sxs-lookup"><span data-stu-id="435e4-147">Connect your lab to the repository</span></span>
1. <span data-ttu-id="435e4-148">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-148">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="435e4-149">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-149">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="435e4-150">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-150">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="435e4-151">왼쪽 패널에서 **구성 및 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-151">On the left panel, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="435e4-152">랩의 **구성 및 정책** 영역에서 **리포지토리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-152">On the lab's **Configuration and policies** area, select **Repositories**.</span></span>
6. <span data-ttu-id="435e4-153">**리포지토리** 영역에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-153">On the **Repositories** area, select **+ Add**.</span></span>

    ![리포지토리 추가 버튼](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="435e4-155">두 번째 **리포지토리** 페이지에서 다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-155">On the second **Repositories** page, specify the following information:</span></span>

   * <span data-ttu-id="435e4-156">**이름** - 리포지토리의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-156">**Name** - Enter a name for the repository.</span></span>
   * <span data-ttu-id="435e4-157">**Git 복제 URL** - 이전에 GitHub 또는 Visual Studio Team Services에서 복사한 Git HTTPS 복제 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-157">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="435e4-158">**분기** - 정의를 가져올 분기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-158">**Branch** - Enter the branch to get your definitions.</span></span>
   * <span data-ttu-id="435e4-159">**개인 액세스 토큰** - 이전에 GitHub 또는 Visual Studio Team Services에서 가져온 개인 액세스 토큰을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-159">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="435e4-160">**폴더 경로** - 아티팩트 또는 Azure Resource Manager 템플릿 정의가 포함된 복제 URL에 상대적인 폴더 경로를 하나 이상 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-160">**Folder Paths** - Enter at least one folder path relative to the clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="435e4-161">하위 디렉터리를 지정하는 경우 폴더 경로에 슬래시를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-161">When specifying a subdirectory, make sure to include the forward slash in the folder path.</span></span>

     ![리포지토리 영역](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="435e4-163">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="435e4-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="435e4-164">Next steps</span></span>
<span data-ttu-id="435e4-165">개인 Git 리포지토리를 만든 후 필요에 따라 다음 중 하나 또는 둘 다를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-165">After you have created your private Git repository, you can do one or both of the following, depending on your needs:</span></span>
* <span data-ttu-id="435e4-166">[사용자 지정 아티팩트](devtest-lab-artifact-author.md)를 저장합니다. 저장한 아티팩트는 나중에 새 VM을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later to create new VMs.</span></span>
* <span data-ttu-id="435e4-167">[Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스를 만든](devtest-lab-create-environment-from-arm.md) 다음 개인 리포지토리에 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store the templates in your private repo.</span></span>

<span data-ttu-id="435e4-168">VM을 만드는 경우 Git 리포지토리에 아티팩트 또는 템플릿이 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-168">When you create a VM, you can verify that the artifacts or templates are added to your Git repository.</span></span> <span data-ttu-id="435e4-169">추가된 아티팩트 또는 템플릿은 목록에서 즉시 사용할 수 있으며 원본이 지정된 열에 개인 리포지토리의 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="435e4-169">They are available immediately in the list of artifacts or templates, with the name of your private repo shown in the column that specifies the source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="435e4-170">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="435e4-170">Related blog posts</span></span>
* [<span data-ttu-id="435e4-171">Azure DevTest Labs에서 실패한 아티팩트 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="435e4-171">How to troubleshoot failing Artifacts in Azure DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="435e4-172">Azure DevTest Labs에서 리소스 관리자 템플릿을 사용하여 기존 AD 도메인에 VM 가입</span><span class="sxs-lookup"><span data-stu-id="435e4-172">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
