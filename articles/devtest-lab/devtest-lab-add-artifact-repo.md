---
title: "Azure DevTest Labs에서 Git 리포지토리 tooa 랩 aaaAdd | Microsoft Docs"
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
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a><span data-ttu-id="f2044-103">Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="f2044-103">Add a Git repository toostore custom artifacts and Azure Resource Manager templates</span></span>

<span data-ttu-id="f2044-104">너무 하려는 경우[사용자 지정 아티팩트를 만들](devtest-lab-artifact-author.md) 랩에서 Vm hello에 대 한 또는 [Azure 리소스 관리자 템플릿 toocreate 사용자 지정 테스트 환경을 사용 하 여](devtest-lab-create-environment-from-arm.md), 개인 Git 리포지토리에 tooinclude도 추가 해야 hello 아티팩트 또는 팀에서 Azure 리소스 관리자 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-104">If you want too[create custom artifacts](devtest-lab-artifact-author.md) for hello VMs in your lab, or [use Azure Resource Manager templates toocreate a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository tooinclude hello artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="f2044-105">hello 저장소에 호스팅될 수 [GitHub](https://github.com) 또는 [VSTS Visual Studio Team Services ()](https://visualstudio.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-105">hello repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="f2044-106">Microsoft는 그대로 배포하거나 랩에 맞게 사용자 지정할 수 있는 [아티팩트의 Github 리포지토리](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts)를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="f2044-107">를 사용자 지정 하거나 아티팩트를 만들 때 hello 공용 저장소에 저장할 수 없습니다-개인 리포지토리에 직접 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-107">When you customize or create an artifact, you cannot store them in hello public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="f2044-108">Hello Azure 리소스 관리자 템플릿을 저장, 한 다음 사용 하 여 사용자 지정할 수는 VM을 만들 때 나중 tooeasily 더 많은 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-108">When you create a VM, you can save hello Azure Resource Manager template, customize it if you want, and then use it later tooeasily create more VMs.</span></span> <span data-ttu-id="f2044-109">사용자 고유의 개인 리포지토리에 toostore 지정 Azure 리소스 관리자 템플릿을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-109">You must create your own private repository toostore your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="f2044-110">toocreate GitHub 리포지토리를 확인 하려면 어떻게 toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-110">toolearn how toocreate a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="f2044-111">toocreate Git 리포지토리를 포함 하는 Team Services 프로젝트를 확인 하려면 어떻게 toolearn [tooVisual Studio Team Services 연결](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-111">toolearn how toocreate a Team Services project with a Git Repository, see [Connect tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="f2044-112">hello 다음 스크린 샷에서의 예가 나와 아티팩트가 포함 된 저장소 GitHub에서 표시 되는 방식을:</span><span class="sxs-lookup"><span data-stu-id="f2044-112">hello following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![GitHub 아티팩트 리포지토리 샘플](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a><span data-ttu-id="f2044-114">Hello 저장소 정보 및 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2044-114">Get hello repository information and credentials</span></span>
<span data-ttu-id="f2044-115">리포지토리 tooyour 랩 tooadd 먼저 가져와야 특정 정보 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-115">tooadd a repository tooyour lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="f2044-116">다음 섹션 hello GitHub 및 Visual Studio Team Services에서 호스트 되는 저장소에 대 한이 정보를 가져오는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-116">hello following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="f2044-117">Hello GitHub 리포지토리 복제 URL 및 개인용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2044-117">Get hello GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="f2044-118">tooget hello GitHub 리포지토리 복제 URL 및 개인 액세스 토큰에는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f2044-118">tooget hello GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="f2044-119">Hello 아티팩트 또는 Azure 리소스 관리자 템플릿 정의 포함 하는 hello GitHub 리포지토리의 toohello 홈 페이지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-119">Browse toohello home page of hello GitHub repository that contains hello artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="f2044-120">**복제 또는 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="f2044-121">선택 hello 단추 toocopy hello **복제 url을 HTTPS** toohello 클립보드 하 고 나중에 사용할 hello URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-121">Select hello button toocopy hello **HTTPS clone url** toohello clipboard, and save hello URL for later use.</span></span>
4. <span data-ttu-id="f2044-122">GitHub의 hello 오른쪽 위 모서리에 hello 프로필 이미지를 선택 하 고 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-122">Select hello profile image in hello upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="f2044-123">Hello에 **개인 설정** 메뉴 hello 왼쪽에서 선택 **개인용 액세스 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-123">In hello **Personal settings** menu on hello left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="f2044-124">**Generate new token**(새 토큰 생성)을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="f2044-125">Hello에 **새 개인용 액세스 토큰** 페이지에서 입력 한 **설명 토큰**, hello에서 hello 기본 항목을 수락 **범위를 선택**, 선택한 후 **생성 토큰**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-125">On hello **New personal access token** page, enter a **Token description**, accept hello default items in hello **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="f2044-126">나중에 필요에 따라 생성 된 hello 토큰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-126">Save hello generated token as you need it later.</span></span>
9. <span data-ttu-id="f2044-127">이제 GitHub를 닫아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="f2044-128">Toohello 계속 [랩 toohello 리포지토리에 연결](#connect-your-lab-to-the-repository) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f2044-128">Continue toohello [Connect your lab toohello repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="f2044-129">Hello Visual Studio Team Services 리포지토리 복제 URL 및 개인용 액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2044-129">Get hello Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="f2044-130">tooget hello Visual Studio Team Services 리포지토리 복제 URL 및 개인 액세스 토큰에는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f2044-130">tooget hello Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="f2044-131">열기 hello 홈 페이지의 팀 컬렉션 (예를 들어 `https://contoso-web-team.visualstudio.com`)을 선택한 다음 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-131">Open hello home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="f2044-132">Hello 프로젝트 홈 페이지에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-132">On hello project home page, select **Code**.</span></span>
3. <span data-ttu-id="f2044-133">hello 프로젝트, tooview hello 클론 URL **코드** 페이지에서 **복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-133">tooview hello clone URL, on hello project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="f2044-134">이 자습서의 뒷부분에 나오는 필요에 따라 hello URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-134">Save hello URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="f2044-135">개인 액세스 토큰 toocreate 선택 **내 프로필** hello 사용자 계정 드롭 다운 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-135">toocreate a Personal Access Token, select **My profile** from hello user account drop-down menu.</span></span>
6. <span data-ttu-id="f2044-136">Hello 프로필 정보 페이지에서 선택 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-136">On hello profile information page, select **Security**.</span></span>
7. <span data-ttu-id="f2044-137">Hello에 **보안** 탭에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-137">On hello **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="f2044-138">Hello에 **개인용 액세스 토큰을 만듭니다.** 페이지:</span><span class="sxs-lookup"><span data-stu-id="f2044-138">In hello **Create a personal access token** page:</span></span>

   * <span data-ttu-id="f2044-139">입력 한 **설명** hello 토큰에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-139">Enter a **Description** for hello token.</span></span>
   * <span data-ttu-id="f2044-140">선택 **180 일** hello에서 **만료에** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-140">Select **180 days** from hello **Expires In** list.</span></span>
   * <span data-ttu-id="f2044-141">선택 **액세스할 수 있는 모든 계정을** hello에서 **계정** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-141">Choose **All accessible accounts** from hello **Accounts** list.</span></span>
   * <span data-ttu-id="f2044-142">Hello 선택 **모든 범위** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-142">Choose hello **All scopes** option.</span></span>
   * <span data-ttu-id="f2044-143">**토큰 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="f2044-144">완료 되 면 hello 새 토큰 나타납니다 hello **개인 액세스 토큰** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-144">When finished, hello new token appears in hello **Personal Access Tokens** list.</span></span> <span data-ttu-id="f2044-145">선택 **토큰 복사**, 한 다음 나중에 사용할 hello 토큰 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-145">Select **Copy Token**, and then save hello token value for later use.</span></span>
10. <span data-ttu-id="f2044-146">Toohello 계속 [랩 toohello 리포지토리에 연결](#connect-your-lab-to-the-repository) 섹션.</span><span class="sxs-lookup"><span data-stu-id="f2044-146">Continue toohello [Connect your lab toohello repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-toohello-repository"></a><span data-ttu-id="f2044-147">랩 toohello 리포지토리에 연결</span><span class="sxs-lookup"><span data-stu-id="f2044-147">Connect your lab toohello repository</span></span>
1. <span data-ttu-id="f2044-148">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-148">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f2044-149">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-149">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f2044-150">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-150">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="f2044-151">왼쪽된 패널의 hello 선택 **구성 및 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-151">On hello left panel, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="f2044-152">Hello 랩에 **구성 및 정책** 영역에서 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-152">On hello lab's **Configuration and policies** area, select **Repositories**.</span></span>
6. <span data-ttu-id="f2044-153">Hello에 **저장소** 영역에서 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-153">On hello **Repositories** area, select **+ Add**.</span></span>

    ![리포지토리 추가 버튼](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="f2044-155">Hello에 두 번째 **저장소** 페이지 hello 다음 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-155">On hello second **Repositories** page, specify hello following information:</span></span>

   * <span data-ttu-id="f2044-156">**이름** -hello 저장소에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-156">**Name** - Enter a name for hello repository.</span></span>
   * <span data-ttu-id="f2044-157">**Git 복제 Url** -GitHub 또는 Visual Studio Team Services에서 앞에서 복사한 hello Git HTTPS 클론 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-157">**Git Clone Url** - Enter hello Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="f2044-158">**분기** -hello 분기 tooget 정의를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-158">**Branch** - Enter hello branch tooget your definitions.</span></span>
   * <span data-ttu-id="f2044-159">**개인용 액세스 토큰** -GitHub 또는 Visual Studio Team Services에서 이전에 얻은 hello 개인용 액세스 토큰을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-159">**Personal Access Token** - Enter hello personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="f2044-160">**폴더 경로** -프로그램 아티팩트 또는 Azure 리소스 관리자 템플릿 정의가 포함 된 하나 이상의 폴더에 경로 상대 toohello 클론 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-160">**Folder Paths** - Enter at least one folder path relative toohello clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="f2044-161">하위 디렉터리를 지정할 때는 hello 폴더 경로에 있는지 tooinclude hello 슬래시를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-161">When specifying a subdirectory, make sure tooinclude hello forward slash in hello folder path.</span></span>

     ![리포지토리 영역](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="f2044-163">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2044-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2044-164">Next steps</span></span>
<span data-ttu-id="f2044-165">개인 Git 리포지토리를 만든 후 필요에 따라 hello 다음 중 하나 또는 모두를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-165">After you have created your private Git repository, you can do one or both of hello following, depending on your needs:</span></span>
* <span data-ttu-id="f2044-166">저장소 프로그램 [사용자 지정 아티팩트](devtest-lab-artifact-author.md)이며 이후 toocreate를 사용할 수 있습니다 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later toocreate new VMs.</span></span>
* <span data-ttu-id="f2044-167">[Azure 리소스 관리자 템플릿으로 환경 다중 VM 및 PaaS 리소스 만들기](devtest-lab-create-environment-from-arm.md) 다음 개인 리 포에 hello 서식 파일을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store hello templates in your private repo.</span></span>

<span data-ttu-id="f2044-168">VM을 만들 때 hello 아티팩트 또는 템플릿 / tooyour Git 리포지토리에 추가 된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-168">When you create a VM, you can verify that hello artifacts or templates are added tooyour Git repository.</span></span> <span data-ttu-id="f2044-169">즉시 hello 또는 목록에서 아티팩트 템플릿 hello 소스를 지정 하는 hello 열에 표시 된 사용자의 개인 리포지토리의 hello 이름으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2044-169">They are available immediately in hello list of artifacts or templates, with hello name of your private repo shown in hello column that specifies hello source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="f2044-170">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="f2044-170">Related blog posts</span></span>
* [<span data-ttu-id="f2044-171">어떻게 tootroubleshoot Azure DevTest Labs의 아티팩트를 실패</span><span class="sxs-lookup"><span data-stu-id="f2044-171">How tootroubleshoot failing Artifacts in Azure DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="f2044-172">VM tooexisting Azure DevTest Labs에서 리소스 관리자 템플릿을 사용 하는 AD 도메인 가입</span><span class="sxs-lookup"><span data-stu-id="f2044-172">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
