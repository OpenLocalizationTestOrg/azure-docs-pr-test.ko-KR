---
title: "Azure 기능에 대 한 aaaContinuous 배포 | Microsoft Docs"
description: "Azure 앱 서비스 toopublish의 연속 배포 기능이 Azure 기능을 사용 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="924fb-103">Azure Functions에 대한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="924fb-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="924fb-104">Azure 기능 사용 하면 쉽게 toodeploy 앱 서비스 연속 통합을 사용 하 여 함수 앱.</span><span class="sxs-lookup"><span data-stu-id="924fb-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="924fb-105">Functions는 BitBucket, Dropbox, GitHub 및 VSTS(Visual Studio Team Services)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="924fb-106">이렇게 하면 이러한 통합된 서비스 트리거 배포 tooAzure 중 하나를 사용 하 여 워크플로 함수의 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="924fb-107">로 시작 하는 새로운 tooAzure 함수 인 경우 [Azure 함수 개요](functions-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="924fb-108">연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="924fb-109">또한 함수 코드에서 소스 제어를 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="924fb-110">배포 원본 hello는 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="924fb-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="924fb-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="924fb-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="924fb-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="924fb-113">외부 리포지토리(Git 또는 Mercurial)</span><span class="sxs-lookup"><span data-stu-id="924fb-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="924fb-114">Git 로컬 리포지토리</span><span class="sxs-lookup"><span data-stu-id="924fb-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="924fb-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="924fb-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="924fb-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="924fb-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="924fb-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="924fb-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="924fb-118">배포는 함수 앱별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="924fb-119">Hello 포털에 액세스 toofunction 코드 너무 설정 연속 배포를 사용 하도록 설정한 후*읽기 전용*합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="924fb-120">연속 배포 요구 사항</span><span class="sxs-lookup"><span data-stu-id="924fb-120">Continuous deployment requirements</span></span>

<span data-ttu-id="924fb-121">연속 배포를 설정 하기 전에 hello 배포 원본에 구성 된 배포 소스와 함수 코드 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="924fb-122">지정 된 함수 앱 배포의 각 함수 hello 디렉터리 이름을 hello 함수 hello 이름을 인 명명 된 하위 디렉터리에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="924fb-123">연속 배포 설정</span><span class="sxs-lookup"><span data-stu-id="924fb-123">Set up continuous deployment</span></span>
<span data-ttu-id="924fb-124">이 절차 tooconfigure 연속 배포를 사용 하 여 기존 함수 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="924fb-125">다음 단계에서는 GitHub 리포지토리와의 통합을 보여 주지만 Visual Studio Team Services 또는 기타 배포 서비스에도 유사한 단계가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="924fb-126">Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="924fb-128">그런 다음 hello **배포** 블레이드 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="924fb-130">Hello에 **배포 원본을** 블레이드에서 클릭 **선택 소스**선택한 배포 원본에 대 한 hello 정보를 입력 한 다음을 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![배포 원본 선택](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="924fb-132">연속 배포를 구성한 후에 모든 파일 변경 내용 배포 원본에는 복사 toohello 함수 앱을 전체 사이트 배포 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="924fb-133">hello 원본 파일을 업데이트할 때 hello 사이트를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="924fb-134">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="924fb-134">Deployment options</span></span>

<span data-ttu-id="924fb-135">hello 다음은 몇 가지 일반적인 배포 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="924fb-136">스테이징 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="924fb-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="924fb-137">기존 함수 toocontinuous 배포 이동</span><span class="sxs-lookup"><span data-stu-id="924fb-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="924fb-138">스테이징 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="924fb-138">Create a staging deployment</span></span>

<span data-ttu-id="924fb-139">함수 앱은 배포 슬롯을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="924fb-140">그러나 연속 통합을 사용하여 별도 스테이징 및 프로덕션 배포를 계속 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="924fb-141">프로세스 tooconfigure hello 및 스테이징 배포를 다루는 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="924fb-142">Hello 프로덕션 코드 및 준비에 대 한 구독에서 두 개의 기능 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="924fb-143">아직 없는 경우 배포 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="924fb-144">이 예제에서는 [GitHub]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="924fb-145">단계를 완료 하는 hello 이전 프로덕션 함수 앱에 대 한 **연속 배포 설정** 및 집합 hello 배포 분기 toohello 마스터 분기 GitHub 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![배포 분기 선택](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="924fb-147">함수 앱을 준비 하는 hello에 대 한이 단계를 반복 하지만 GitHub 리포지토리에 있는 대신 분기를 준비 하는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="924fb-148">배포 원본이 분기를 지원하지 않는 경우 다른 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="924fb-149">분기 또는 폴더를 준비 하는 hello에 업데이트 tooyour 코드를 확인 한 후 hello 스테이징 배포에에서 이러한 변경 내용이 반영 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="924fb-150">테스트를 마친 후 hello 마스터 분기에 병합 hello 준비 분기에서 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="924fb-151">이 병합 toohello 프로덕션 함수 응용 프로그램을 배포를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="924fb-152">배포 소스 분기를 지원 하지 않으면 hello 준비 폴더의에서 hello 파일로 hello 프로덕션 폴더에 hello 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="924fb-153">기존 함수 toocontinuous 배포 이동</span><span class="sxs-lookup"><span data-stu-id="924fb-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="924fb-154">기존 함수를 만들고 필요한 toodownload hello 포털에서 유지 관리 하는 경우 위에서 설명한 것 처럼 연속 배포를 설정 하려면 먼저 FTP 또는 hello 로컬 Git 리포지토리를 사용 하 여 코드 파일 함수 기존 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="924fb-155">이렇게 하려면 hello에 응용 프로그램 서비스 설정을 함수 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="924fb-156">파일을 다운로드 한 후 선택한 tooyour 연속 배포 원본을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="924fb-157">연속 통합을 구성 하면 더 이상 됩니다 수 tooedit hello 함수 포털에서 소스 파일.</span><span class="sxs-lookup"><span data-stu-id="924fb-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="924fb-158">방법: 배포 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="924fb-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="924fb-159">방법: FTP를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="924fb-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="924fb-160">방법: hello 로컬 Git 리포지토리를 사용 하 여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="924fb-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="924fb-161">방법: 배포 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="924fb-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="924fb-162">FTP 또는 로컬 Git 리포지토리를 사용 하 여 함수 앱에서 파일을 다운로드할 수 있습니다, 전에 자격 증명 tooaccess hello 사이트를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="924fb-163">자격 증명 hello 함수 앱 수준에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="924fb-164">Hello Azure 포털에서에서 tooset 배포 자격 증명 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="924fb-165">Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![로컬 배포 자격 증명 설정](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="924fb-167">사용자 이름 및 암호를 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="924fb-168">이제 이러한 자격 증명 tooaccess 함수 앱 FTP 또는 hello의 기본 제공 Git 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="924fb-169">방법: FTP를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="924fb-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="924fb-170">Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **속성**, 다음에 대 한 hello 값을 복사 **P/배포 사용자**, **FTP 호스트 이름**, 및 **FTPS 호스트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="924fb-171">**P/배포 사용자** hello 응용 프로그램 이름, tooprovide hello FTP 서버에 대 한 적절 한 컨텍스트를 포함 하 여 hello 포털에 표시 된 대로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![배포 정보 가져오기](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="924fb-173">FTP 클라이언트에서 수집한 tooconnect tooyour 앱 hello 연결 정보를 사용 하 고 함수에 대 한 hello 소스 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="924fb-174">방법: 로컬 Git 리포지토리를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="924fb-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="924fb-175">Hello 함수 앱에서 [Azure 포털](https://portal.azure.com), 클릭 **플랫폼 기능** 및 **배포 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="924fb-177">그런 다음 hello **배포** 블레이드 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="924fb-179">Hello에 **배포 원본을** 블레이드에서 클릭 **로컬 Git 리포지토리** 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="924fb-180">**플랫폼 기능**, 클릭 **속성** Git URL의 hello 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="924fb-182">인식 Git 명령 프롬프트 또는 임의의 Git 도구를 사용 하 여 로컬 컴퓨터의 hello 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="924fb-183">hello Git 복제 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="924fb-184">다음 예제는 hello와 같이 로컬 컴퓨터에 함수 앱 toohello 복제본에서 파일을 인출:</span><span class="sxs-lookup"><span data-stu-id="924fb-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="924fb-185">요청된 경우 [구성된 배포 자격 증명](#credentials)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="924fb-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
