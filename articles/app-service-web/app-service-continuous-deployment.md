---
title: "Azure App Service에 연속 배포 | Microsoft Docs"
description: "Azure 앱 서비스에 연속 배포를 활성화하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 7d978e623aaff25a9400090bd3ac18ed560d2ebf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a><span data-ttu-id="9a0e9-103">Azure 앱 서비스에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="9a0e9-103">Continuous Deployment to Azure App Service</span></span>
<span data-ttu-id="9a0e9-104">이 자습서에서는 [Azure 앱 서비스] 앱에 대한 연속 배포 워크플로를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-104">This tutorial shows you how to configure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="9a0e9-105">BitBucket, GitHub 및 [VSTS(Visual Studio Team Services)](https://www.visualstudio.com/team-services/)와 App Service 통합을 통해 Azure가 이러한 서비스 중 하나에 게시한 프로젝트에서 최신 업데이트를 가져오는 연속 배포 워크플로를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in the most recent updates from your project published to one of these services.</span></span> <span data-ttu-id="9a0e9-106">연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="9a0e9-107">Azure Portal에 의해 나열되지 않은 클라우드 저장소에서 수동으로 연속 배포를 구성하는 방법을 확인하려면(예: [GitLab](https://gitlab.com/)), [수동 단계를 사용하여 연속 배포 설정](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-107">To find out how to configure continuous deployment manually from a cloud repository not listed by the Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="9a0e9-108"><a name="overview"></a>연속 배포 활성화</span><span class="sxs-lookup"><span data-stu-id="9a0e9-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="9a0e9-109">연속 배포를 활성화하려면</span><span class="sxs-lookup"><span data-stu-id="9a0e9-109">To enable continuous deployment,</span></span>

1. <span data-ttu-id="9a0e9-110">연속 배포에 사용될 리포지토리에 앱 콘텐츠를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-110">Publish your app content to the repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="9a0e9-111">이러한 서비스에 프로젝트를 게시하는 것에 대한 자세한 내용은 [리포지토리 만들기(GitHub)], [리포지토리 만들기(BitBucket)] 및 [VSTS 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-111">For more information on publishing your project to these services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="9a0e9-112">앱의 메뉴 블레이드에 있는 [Azure 포털]에서 **앱 배포 > 배포 옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-112">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="9a0e9-113">**원본 선택**을 클릭한 다음 배포 원본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-113">Click **Choose Source**, then select the deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="9a0e9-114">앱 서비스 배포를 위한 VSTS 계정을 구성하려면 이 [자습서](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-114">To configure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="9a0e9-115">권한 부여 워크플로를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-115">Complete the authorization workflow.</span></span>
4. <span data-ttu-id="9a0e9-116">**배포 원본** 블레이드에서 배포할 프로젝트 및 분기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-116">In the **Deployment source** blade, choose the project and branch to deploy from.</span></span> <span data-ttu-id="9a0e9-117">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="9a0e9-118">GitHub 또는 BitBucket에서 지속적으로 배포할 수 있도록 하면 공용 및 개인 프로젝트가 둘 다 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="9a0e9-119">앱 서비스는 선택한 저장소와의 연결을 만들고 지정한 분기에서 파일을 가져오고 앱 서비스 앱에 대한 리포지토리의 복제본을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-119">App Service creates an association with the selected repository, pulls in the files from the specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="9a0e9-120">Azure 포털에서 VSTS 연속 배포를 구성할 때 통합은 App Service [Kudu 배포 엔진](https://github.com/projectkudu/kudu/wiki)을 사용하며 여기서는 모든 `git push`를 통해 빌드 및 배포 작업을 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-120">When you configure VSTS continuous deployment from the Azure portal, the integration uses the App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="9a0e9-121">VSTS에서 연속 배포를 별도로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-121">You do not need to separately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="9a0e9-122">이 프로세스를 완료한 후에는 **배포 옵션** 앱 블레이드에서 배포가 성공했음을 나타내는 활성 배포를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-122">After this process completes, the **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="9a0e9-123">앱이 성공적으로 배포되었는지 확인하려면 Azure 포털에서 앱의 블레이드 맨 위에 있는 **URL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-123">To verify the app is successfully deployed, click the **URL** at the top of the app's blade in the Azure portal.</span></span>
6. <span data-ttu-id="9a0e9-124">사용자가 선택한 리포지토리에서 지속적으로 배포되는지 확인하려면, 리포지토리에 대한 변경을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-124">To verify that continuous deployment is occurring from the repository of your choice, push a change to the repository.</span></span> <span data-ttu-id="9a0e9-125">리포지토리에 푸시한 직후 변경 내용이 반영되도록 앱을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-125">Your app should update to reflect the changes shortly after the push to the repository completes.</span></span> <span data-ttu-id="9a0e9-126">앱의 **배포 옵션** 블레이드에서 업데이트를 가져왔는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-126">You can verify that it has pulled in the update in the **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="9a0e9-127"><a name="VSsolution"></a>Visual Studio 솔루션의 연속 배포</span><span class="sxs-lookup"><span data-stu-id="9a0e9-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="9a0e9-128">Azure 앱 서비스에 Visual Studio 솔루션을 푸시하는 것은 간단한 index.html 파일을 푸시하는 것만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-128">Pushing a Visual Studio solution to Azure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="9a0e9-129">앱 서비스 배포 프로세스는 NuGet 종속성 복원 및 응용 프로그램 이진 파일 생성 등의 모든 세부 정보를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-129">The App Service deployment process streamlines all the details, including restoring NuGet dependencies and building the application binaries.</span></span> <span data-ttu-id="9a0e9-130">Git 리포지토리에서 코드를 유지 관리하는 소스 제어 모범 사례만 따르면 나머지는 앱 서비스 배포에서 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-130">You can follow the source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of the rest.</span></span>

<span data-ttu-id="9a0e9-131">솔루션과 리포지토리를 다음과 같이 구성한 경우 Visual Studio 솔루션을 앱 서비스에 푸시하는 단계는 [이전 섹션](#overview)과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-131">The steps for pushing your Visual Studio solution to App Service are the same as in the [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="9a0e9-132">Visual Studio 원본 제어 옵션을 사용하여 아래 이미지와 같은 `.gitignore` 파일을 생성하거나 이 [.gitignore 샘플](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)과 유사한 콘텐츠로 리포지토리 루트에 `.gitignore` 파일을 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-132">Use the Visual Studio source control option to generate a `.gitignore` file such as the image below or manually add a `.gitignore` file in your repository root with content similar to this [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="9a0e9-133">전체 솔루션의 디렉터리 트리를 리포지토리에 추가하고 .sln 파일을 리포지토리 루트에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-133">Add the entire solution's directory tree to your repository, with the .sln file in the repository root.</span></span>

<span data-ttu-id="9a0e9-134">설명된 대로 리포지토리를 설정하고, 온라인 Git 리포지토리 중 하나에서 연속 게시에 대해 Azure에서 앱을 구성한 후에는 Visual Studio에서 ASP.NET 응용 프로그램을 로컬로 개발하고 온라인 Git 리포지토리에 변경 내용을 푸시하여 코드를 지속적으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of the online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes to your online Git repository.</span></span>

## <span data-ttu-id="9a0e9-135"><a name="disableCD"></a>지속적 배포 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="9a0e9-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="9a0e9-136">지속적 배포를 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="9a0e9-136">To disable continuous deployment,</span></span>

1. <span data-ttu-id="9a0e9-137">앱의 메뉴 블레이드에 있는 [Azure 포털]에서 **앱 배포 > 배포 옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-137">In your app's menu blade in the [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="9a0e9-138">그런 다음 **배포 옵션** 블레이드에서 **연결 끊기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-138">Then click **Disconnect** in the **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="9a0e9-139">확인 메시지에서 **예**를 클릭한 후 다른 원본의 게시를 설정하려면 앱의 블레이드로 돌아가서 **앱 배포 > 배포 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-139">After answering **Yes** to the confirmation message, you can return to your app's blade and click **APP DEPLOYMENT > Deployment options** if you would like to set up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9a0e9-140">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9a0e9-140">Additional Resources</span></span>
* [<span data-ttu-id="9a0e9-141">연속 배포의 일반 문제를 조사하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a0e9-141">How to investigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="9a0e9-142">[Azure용 PowerShell 사용 방법]</span><span class="sxs-lookup"><span data-stu-id="9a0e9-142">[How to use PowerShell for Azure]</span></span>
* <span data-ttu-id="9a0e9-143">[Mac 및 Linux용 Azure 명령줄 도구를 사용하는 방법]</span><span class="sxs-lookup"><span data-stu-id="9a0e9-143">[How to use the Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="9a0e9-144">[Git 설명서]</span><span class="sxs-lookup"><span data-stu-id="9a0e9-144">[Git documentation]</span></span>
* [<span data-ttu-id="9a0e9-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="9a0e9-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* <span data-ttu-id="9a0e9-146">[Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)(Azure를 사용하여 ASP.NET 4 앱을 배포할 CI/CD 파이프라인을 자동으로 생성)</span><span class="sxs-lookup"><span data-stu-id="9a0e9-146">[Use Azure to automatically generate a CI/CD pipeline to deploy an ASP.NET 4 app](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)</span></span>

> [!NOTE]
> <span data-ttu-id="9a0e9-147">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-147">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9a0e9-148">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a0e9-148">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="9a0e9-149">[Azure 앱 서비스]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="9a0e9-149">[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/</span></span>
<span data-ttu-id="9a0e9-150">[Azure 포털]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="9a0e9-150">[Azure portal]: https://portal.azure.com</span></span>
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="9a0e9-151">[Azure용 PowerShell 사용 방법]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="9a0e9-151">[How to use PowerShell for Azure]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="9a0e9-152">[Mac 및 Linux용 Azure 명령줄 도구를 사용하는 방법]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="9a0e9-152">[How to use the Azure Command-Line Tools for Mac and Linux]:../cli-install-nodejs.md</span></span>
<span data-ttu-id="9a0e9-153">[Git 설명서]: http://git-scm.com/documentation</span><span class="sxs-lookup"><span data-stu-id="9a0e9-153">[Git Documentation]: http://git-scm.com/documentation</span></span>

<span data-ttu-id="9a0e9-154">[리포지토리 만들기(GitHub)]: https://help.github.com/articles/create-a-repo</span><span class="sxs-lookup"><span data-stu-id="9a0e9-154">[Create a repo (GitHub)]: https://help.github.com/articles/create-a-repo</span></span>
<span data-ttu-id="9a0e9-155">[리포지토리 만들기(BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span><span class="sxs-lookup"><span data-stu-id="9a0e9-155">[Create a repo (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo</span></span>
<span data-ttu-id="9a0e9-156">[VSTS 시작]: https://www.visualstudio.com/docs/vsts-tfs-overview</span><span class="sxs-lookup"><span data-stu-id="9a0e9-156">[Get started with VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview</span></span>
