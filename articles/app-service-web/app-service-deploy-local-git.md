---
title: "Azure 앱 서비스에 로컬 Git 배포"
description: "Azure 앱 서비스에 로컬 Git 배포를 사용하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="8cbed-103">Azure 앱 서비스에 로컬 Git 배포</span><span class="sxs-lookup"><span data-stu-id="8cbed-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="8cbed-104">이 자습서에서는 로컬 컴퓨터의 Git 리포지토리에서 [Azure 앱 서비스] 에 앱을 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="8cbed-105">앱 서비스는 **Azure 포털** 의 [로컬 Git]배포 옵션을 통해 이 접근 방식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="8cbed-106">이 문서에 설명되어 있는 대부분의 Git 명령은 [여기](app-service-web-get-started.md)에 설명된 대로 [Azure 명령줄 인터페이스]를 사용하여 앱 서비스 앱을 만드는 경우 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cbed-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8cbed-107">Prerequisites</span></span>
<span data-ttu-id="8cbed-108">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="8cbed-109">Git.</span><span class="sxs-lookup"><span data-stu-id="8cbed-109">Git.</span></span> <span data-ttu-id="8cbed-110">[여기](http://www.git-scm.com/downloads)에서 설치 이진 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="8cbed-111">Git에 대한 기본 지식.</span><span class="sxs-lookup"><span data-stu-id="8cbed-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="8cbed-112">Microsoft Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="8cbed-112">A Microsoft Azure account.</span></span> <span data-ttu-id="8cbed-113">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="8cbed-114">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 평가](https://azure.microsoft.com/try/app-service/)로 이동합니다. App Service에서 단기 스타터 앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="8cbed-115">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="8cbed-116"><a name="Step1"></a>1단계: 로컬 리포지토리 만들기</span><span class="sxs-lookup"><span data-stu-id="8cbed-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="8cbed-117">다음 작업을 수행하여 새 Git 리포지토리를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="8cbed-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="8cbed-118">**GitBash** (Windows) 또는 **Bash** (Unix Shell)와 같은 명령줄 도구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="8cbed-119">OS X 시스템에서는 **터미널** 응용 프로그램을 통해 명령줄에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="8cbed-120">배포할 콘텐츠가 있는 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="8cbed-121">다음 명령을 사용하여 새 Git 리포지토리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="8cbed-122"><a name="Step2"></a>2단계: 콘텐츠 커밋</span><span class="sxs-lookup"><span data-stu-id="8cbed-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="8cbed-123">앱 서비스는 다양한 프로그래밍 언어로 만들어진 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="8cbed-124">리포지토리에 콘텐츠가 이미 포함된 경우 이 항목을 건너뛰고 아래의 항목 2로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="8cbed-125">리포지토리에 콘텐츠가 포함되어 있지 않은 경우 다음과 같이 정적 .html 파일로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="8cbed-126">텍스트 편집기를 사용하여 Git 리포지토리의 루트에 **index.html** 이라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="8cbed-127">index.html 파일 내용으로 *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="8cbed-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="8cbed-128">명령줄에서 Git 리포지토리의 루트 아래에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="8cbed-129">다음 명령을 사용하여 리포지토리에 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="8cbed-130">그리고 나서 다음 명령을 사용하여 리포지토리에 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="8cbed-131"><a name="Step3"></a>3단계: App Service 앱 리포지토리 사용</span><span class="sxs-lookup"><span data-stu-id="8cbed-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="8cbed-132">앱 서비스 앱에서 Git 리포지토리를 사용할 수 있도록 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="8cbed-133">[로컬 Git]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="8cbed-134">App Service의 앱 블레이드에서 **설정 > 배포 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="8cbed-135">**원본 선택**을 클릭한 다음 **로컬 Git 리포지토리**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![로컬 Git 리포지토리](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="8cbed-137">Azure에서 리포지토리를 처음 설정하는 경우 로그인 자격 증명을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="8cbed-138">이를 사용하여 Azure 리포지토리에 로그인하고 로컬 Git 리포지토리에서 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="8cbed-139">앱의 블레이드에서 **설정> 배포 자격 증명**을 클릭한 다음 배포 사용자 이름 및 암호를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="8cbed-140">완료되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="8cbed-141"><a name="Step4"></a>4단계: 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="8cbed-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="8cbed-142">로컬 Git를 사용하여 앱을 앱 서비스에 게시하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="8cbed-143">Azure Portal의 앱 블레이드에서 **Git URL**에 대한 **설정 > 속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="8cbed-144">**Git URL** 은 로컬 리포지토리로부터 배포할 원격 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="8cbed-145">다음 단계에서 이 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="8cbed-146">명령줄을 사용하여 로컬 Git 리포지토리의 루트에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="8cbed-147">`git remote` 를 사용하여 1단계의 **Git URL** 에 나열된 원격 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="8cbed-148">명령은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="8cbed-149">**remote** 명령은 명명된 참조를 원격 리포지토리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="8cbed-150">이 경우 웹 앱의 리포지토리용으로 'azure'라는 이름의 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="8cbed-151">방금 만든 새 **azure** 원격을 사용하여 앱 서비스에 콘텐츠를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="8cbed-152">Azure 포털에서 앱으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="8cbed-153">가장 최근 푸시의 로그 항목이 **배포** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="8cbed-154">앱 블레이드의 위쪽에서 **찾아보기** 단추를 클릭하여 콘텐츠가 배포되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="8cbed-155"><a name="Step5"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="8cbed-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="8cbed-156">다음은 Git를 사용하여 Azure에서 앱 서비스 앱을 게시할 때 주로 발생하는 문제 또는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="8cbed-157">**증상**: '[siteURL]'에 액세스할 수 없음: [scmAddress]에 연결하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="8cbed-158">**원인**: 이 오류는 앱이 가동 및 실행되지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="8cbed-159">**해결 방법**: Azure 포털에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="8cbed-160">앱이 실행되지 않으면 Git 배포가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="8cbed-161">**증상**: 'hostname' 호스트를 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="8cbed-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="8cbed-162">**원인**: 이 오류는 'azure' 원격을 만들 때 입력한 주소 정보가 올바르지 않을 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="8cbed-163">**해결 방법**: `git remote -v` 명령을 사용하여 모든 원격을 관련 URL과 함께 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="8cbed-164">'azure' 원격의 URL이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="8cbed-165">필요한 경우 제거하고 올바른 URL을 사용하여 이 원격을 다시 만드세요.</span><span class="sxs-lookup"><span data-stu-id="8cbed-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="8cbed-166">**증상**: 공통 참조 없음 및 지정하지 않음; 아무것도 안 함.</span><span class="sxs-lookup"><span data-stu-id="8cbed-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="8cbed-167">'마스터'와 같은 분기를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="8cbed-168">**원인**: 이 오류는 git push 작업을 수행할 때 분기를 지정하지 않은 경우 및 Git에서 사용하는 push.default 값을 설정하지 않은 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="8cbed-169">**해결 방법**: 마스터 분기를 지정하고 push 작업을 다시 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="8cbed-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="8cbed-170">예:</span><span class="sxs-lookup"><span data-stu-id="8cbed-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="8cbed-171">**증상**: src refspec [branchname]이 전혀 일치하지 않음</span><span class="sxs-lookup"><span data-stu-id="8cbed-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="8cbed-172">**원인**: 이 오류는 'azure' 원격의 마스터가 아닌 다른 분기에 푸시하려는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="8cbed-173">**해결 방법**: 마스터 분기를 지정하고 push 작업을 다시 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="8cbed-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="8cbed-174">예:</span><span class="sxs-lookup"><span data-stu-id="8cbed-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="8cbed-175">**증상**: RPC 실패; 결과=22, HTTP 코드 = 502.</span><span class="sxs-lookup"><span data-stu-id="8cbed-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="8cbed-176">**원인**: 이 오류는 HTTPS를 통해 큰 git 리포지토리를 푸시하려고 시도하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="8cbed-177">**해결 방법**: 더 큰 postBuffer를 만들도록 로컬 컴퓨터에서 git 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="8cbed-178">**증상**: 오류 - 변경 내용이 원격 리포지토리에 커밋되었으나 웹앱이 업데이트되지 않음</span><span class="sxs-lookup"><span data-stu-id="8cbed-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="8cbed-179">**원인**: 이 오류는 추가 필수 모듈을 지정하는 package.json 파일이 포함된 Node.js 앱을 배포하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="8cbed-180">**해결 방법**: 'npm ERR!'을 포함하는 추가 메시지를</span><span class="sxs-lookup"><span data-stu-id="8cbed-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="8cbed-181">이 오류 이전에 기록해야 합니다. 이러한 메시지는 오류 원인에 대한 추가 내용을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="8cbed-182">다음은 이 오류 및 해당 'npm ERR!' 메시지의 알려진 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbed-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="8cbed-183">메시지:</span><span class="sxs-lookup"><span data-stu-id="8cbed-183">message:</span></span>

* <span data-ttu-id="8cbed-184">**잘못된 package.json 파일**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="8cbed-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="8cbed-185">종속성을 읽을 수 없음</span><span class="sxs-lookup"><span data-stu-id="8cbed-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="8cbed-186">**Windows용 바이너리 배포가 없는 네이티브 모듈**:</span><span class="sxs-lookup"><span data-stu-id="8cbed-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="8cbed-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="8cbed-187">npm ERR!</span></span> <span data-ttu-id="8cbed-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="8cbed-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="8cbed-189">또는</span><span class="sxs-lookup"><span data-stu-id="8cbed-189">OR</span></span>
  * <span data-ttu-id="8cbed-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="8cbed-190">npm ERR!</span></span> <span data-ttu-id="8cbed-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="8cbed-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8cbed-192">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8cbed-192">Additional Resources</span></span>
* [<span data-ttu-id="8cbed-193">Git 설명서</span><span class="sxs-lookup"><span data-stu-id="8cbed-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="8cbed-194">프로젝트 Kudu 설명서</span><span class="sxs-lookup"><span data-stu-id="8cbed-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="8cbed-195">Azure 앱 서비스에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="8cbed-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="8cbed-196">Azure용 PowerShell 사용 방법</span><span class="sxs-lookup"><span data-stu-id="8cbed-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="8cbed-197">Azure 명령줄 인터페이스를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cbed-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="8cbed-198">[Azure 앱 서비스]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="8cbed-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="8cbed-199">[로컬 Git]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8cbed-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="8cbed-200">[Azure 명령줄 인터페이스]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="8cbed-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
