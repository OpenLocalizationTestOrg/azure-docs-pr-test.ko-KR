---
title: "Git 배포 tooAzure aaaLocal 앱 서비스"
description: "자세한 내용은 방법 tooenable 로컬 Git 배포 tooAzure 앱 서비스입니다."
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
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="536c8-103">로컬 Git 배포 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="536c8-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="536c8-104">이 자습서에서는 어떻게 toodeploy 앱 너무[Azure 앱 서비스] 로컬 컴퓨터의 Git 리포지토리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="536c8-105">앱 서비스는 hello로이 방법을 지원 합니다. **로컬 Git** hello에 대 한 배포 옵션 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="536c8-106">Hello를 사용 하 여 앱 서비스 앱을 만드는 경우 자동으로 수행 됩니다이 문서에서 설명 하는 hello Git 명령 중 많은 [Azure 명령줄 인터페이스] 설명 된 대로 [여기](app-service-web-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="536c8-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="536c8-107">Prerequisites</span></span>
<span data-ttu-id="536c8-108">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="536c8-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="536c8-109">Git.</span><span class="sxs-lookup"><span data-stu-id="536c8-109">Git.</span></span> <span data-ttu-id="536c8-110">Hello 설치 이진 파일을 다운로드할 수 있습니다 [여기](http://www.git-scm.com/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="536c8-111">Git에 대한 기본 지식.</span><span class="sxs-lookup"><span data-stu-id="536c8-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="536c8-112">Microsoft Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="536c8-112">A Microsoft Azure account.</span></span> <span data-ttu-id="536c8-113">계정이 없는 경우 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial)하거나 [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="536c8-114">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 앱 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="536c8-115">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="536c8-116"><a name="Step1"></a>1단계: 로컬 리포지토리 만들기</span><span class="sxs-lookup"><span data-stu-id="536c8-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="536c8-117">Hello 작업 toocreate 새 Git 리포지토리를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="536c8-118">**GitBash** (Windows) 또는 **Bash** (Unix Shell)와 같은 명령줄 도구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="536c8-119">OS X 시스템에서 명령줄 hello hello를 통해 액세스할 수 있습니다 **터미널** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="536c8-120">Hello 콘텐츠 toodeploy 찾을 수 없는 toohello 디렉터리를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="536c8-121">Hello 다음 명령 tooinitialize 새 Git 리포지토리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="536c8-122"><a name="Step2"></a>2단계: 콘텐츠 커밋</span><span class="sxs-lookup"><span data-stu-id="536c8-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="536c8-123">앱 서비스는 다양한 프로그래밍 언어로 만들어진 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="536c8-124">리포지토리에 이미 콘텐츠 skip을 포함 하는 경우이 가리킨 toopoint 아래 2 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="536c8-125">리포지토리에 콘텐츠가 포함되어 있지 않은 경우 다음과 같이 정적 .html 파일로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="536c8-126">라는 새 파일을 텍스트 편집기를 사용 하 여 만들 **index.html** hello Git 리포지토리 루트 hello에</span><span class="sxs-lookup"><span data-stu-id="536c8-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="536c8-127">Hello hello index.html에 대 한 hello 콘텐츠 파일을 저장 하는 대로 텍스트를 다음 추가: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="536c8-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="536c8-128">Hello 명령줄에서 Git 리포지토리의 루트 hello 하위 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="536c8-129">다음 명령은 tooadd 파일 tooyour 저장소 다음 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="536c8-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="536c8-130">다음으로, 다음 명령을 hello를 사용 하 여 hello 변경 toohello 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="536c8-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="536c8-131"><a name="Step3"></a>3 단계: 앱 서비스 앱 저장소 hello 설정</span><span class="sxs-lookup"><span data-stu-id="536c8-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="536c8-132">Hello 단계 tooenable 앱 서비스 앱에 대 한 Git 리포지토리를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="536c8-133">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="536c8-134">App Service의 앱 블레이드에서 **설정 > 배포 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="536c8-135">**원본 선택**을 클릭한 다음 **로컬 Git 리포지토리**를 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![로컬 Git 리포지토리](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="536c8-137">Azure에서 리포지토리를 첫 번째 시간 설정을 인 경우에 대 한 toocreate 로그인 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="536c8-138">사용 합니다 해당 hello Azure 저장소에 toolog 및 푸시 변경 내용을 로컬 Git 리포지토리에서.</span><span class="sxs-lookup"><span data-stu-id="536c8-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="536c8-139">앱의 블레이드에서 **설정> 배포 자격 증명**을 클릭한 다음 배포 사용자 이름 및 암호를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="536c8-140">완료되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="536c8-141"><a name="Step4"></a>4단계: 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="536c8-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="536c8-142">다음 단계 toopublish hello 사용자 앱 tooApp 로컬 Git를 사용 하 여 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="536c8-143">Hello Azure 포털에서에서 앱의 블레이드에서 클릭 **설정 > 속성** hello에 대 한 **Git URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="536c8-144">**Git URL** hello 원격 참조 toodeploy toofrom 로컬 리포지토리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="536c8-145">단계를 수행 하는 hello에이 URL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="536c8-146">Hello 명령줄을 사용 하 여, 로컬 Git 리포지토리의 hello 루트에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="536c8-147">사용 하 여 `git remote` tooadd hello 원격 참조에 나열 된 **Git URL** 1 단계에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="536c8-148">명령 비슷한 toohello 다음 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="536c8-149">hello **원격** 명령은 명명 된 참조 tooa 원격 리포지토리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="536c8-150">이 경우 웹 앱의 리포지토리용으로 'azure'라는 이름의 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="536c8-151">서비스 사용자 콘텐츠 tooApp 푸시 새 hello를 사용 하 여 **azure** 원격 방금 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="536c8-152">Hello Azure 포털에서에서 tooyour 응용 프로그램을 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="536c8-153">Hello 빌드되고 가장 최근의 푸시의 로그 항목을 표시 해야 **배포** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="536c8-154">Hello 클릭 **찾아보기** hello 앱 블레이드 tooverify hello 콘텐츠 hello 위쪽에 단추를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="536c8-155"><a name="Step5"></a>문제 해결</span><span class="sxs-lookup"><span data-stu-id="536c8-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="536c8-156">hello 다음은 오류 또는 Azure에서 Git toopublish tooan 앱 서비스 앱을 사용 하는 경우 일반적으로 발생 하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="536c8-157">**증상**: 수 없습니다. '[siteURL]' tooaccess: 너무 tooconnect 실패 했습니다 [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="536c8-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="536c8-158">**원인**: hello 앱이 실행 하는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="536c8-159">**해결 방법**: hello Azure 포털에서에서 hello 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="536c8-160">Git 배포 hello 응용 프로그램을 실행 하지 않는 한 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="536c8-161">**증상**: 'hostname' 호스트를 확인할 수 없음</span><span class="sxs-lookup"><span data-stu-id="536c8-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="536c8-162">**원인**:이 오류가 발생할 수 있습니다 hello 주소 정보를 만들 때 입력 하는 경우 원격 ' azure' hello 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="536c8-163">**해상도**: 사용 하 여 hello `git remote -v` toolist hello 연결 된 URL 따라 모든 원격 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="536c8-164">원격 ' azure' hello에 대 한 hello URL이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="536c8-165">필요에 따라 제거 하 고이 원격 hello 올바른 URL을 사용 하 여 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="536c8-166">**증상**: 공통 참조 없음 및 지정하지 않음; 아무것도 안 함.</span><span class="sxs-lookup"><span data-stu-id="536c8-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="536c8-167">'마스터'와 같은 분기를 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="536c8-168">**원인**: git 푸시 작업을 수행할 때 분기를 지정 및 하지 설정 값을 가질 hello push.default Git에서 사용 하지 않는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="536c8-169">**해결 방법**: hello 마스터 분기 지정 hello 푸시 작업을 다시 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="536c8-170">예:</span><span class="sxs-lookup"><span data-stu-id="536c8-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="536c8-171">**증상**: src refspec [branchname]이 전혀 일치하지 않음</span><span class="sxs-lookup"><span data-stu-id="536c8-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="536c8-172">**원인**: hello 'azure' 원격에서 마스터 이외의 toopush tooa 분기 하려는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="536c8-173">**해결 방법**: hello 마스터 분기 지정 hello 푸시 작업을 다시 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="536c8-174">예:</span><span class="sxs-lookup"><span data-stu-id="536c8-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="536c8-175">**증상**: RPC 실패; 결과=22, HTTP 코드 = 502.</span><span class="sxs-lookup"><span data-stu-id="536c8-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="536c8-176">**원인**: HTTPS를 통해 toopush 큰 git 리포지토리를 시도 하는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="536c8-177">**해결 방법**: hello 로컬 컴퓨터 toomake hello 전위 큰에 hello git 구성 변경</span><span class="sxs-lookup"><span data-stu-id="536c8-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="536c8-178">**증상**: 오류-변경 내용이 커밋된 tooremote 저장소 하지만 웹 앱 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="536c8-179">**원인**: 이 오류는 추가 필수 모듈을 지정하는 package.json 파일이 포함된 Node.js 앱을 배포하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="536c8-180">**해결 방법**: 'npm ERR!'을 포함하는 추가 메시지를</span><span class="sxs-lookup"><span data-stu-id="536c8-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="536c8-181">기록 된 이전 toothis 오류 수준이 며 hello 실패 시 추가 컨텍스트를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="536c8-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="536c8-182">hello 다음이 오류의 원인은 알려진을 해당 'ERR npm!' hello</span><span class="sxs-lookup"><span data-stu-id="536c8-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="536c8-183">메시지:</span><span class="sxs-lookup"><span data-stu-id="536c8-183">message:</span></span>

* <span data-ttu-id="536c8-184">**잘못된 package.json 파일**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="536c8-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="536c8-185">종속성을 읽을 수 없음</span><span class="sxs-lookup"><span data-stu-id="536c8-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="536c8-186">**Windows용 바이너리 배포가 없는 네이티브 모듈**:</span><span class="sxs-lookup"><span data-stu-id="536c8-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="536c8-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="536c8-187">npm ERR!</span></span> <span data-ttu-id="536c8-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="536c8-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="536c8-189">또는</span><span class="sxs-lookup"><span data-stu-id="536c8-189">OR</span></span>
  * <span data-ttu-id="536c8-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="536c8-190">npm ERR!</span></span> <span data-ttu-id="536c8-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="536c8-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="536c8-192">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="536c8-192">Additional Resources</span></span>
* [<span data-ttu-id="536c8-193">Git 설명서</span><span class="sxs-lookup"><span data-stu-id="536c8-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="536c8-194">프로젝트 Kudu 설명서</span><span class="sxs-lookup"><span data-stu-id="536c8-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="536c8-195">연속 배포 tooAzure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="536c8-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="536c8-196">어떻게 toouse Azure에 대 한 PowerShell</span><span class="sxs-lookup"><span data-stu-id="536c8-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="536c8-197">어떻게 toouse hello Azure 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="536c8-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure 앱 서비스]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure 포털]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure 명령줄 인터페이스]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
