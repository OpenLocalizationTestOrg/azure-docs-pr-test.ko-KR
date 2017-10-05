---
title: "Azure Functions에 대한 연속 배포 | Microsoft 문서"
description: "Azure 앱 서비스의 연속 배포 기능을 사용하여 Azure Functions를 게시합니다."
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
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="9d8f9-103">Azure Functions에 대한 연속 배포</span><span class="sxs-lookup"><span data-stu-id="9d8f9-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="9d8f9-104">Azure Functions를 사용하면 App Service 연속 통합을 사용하여 함수 앱을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="9d8f9-105">Functions는 BitBucket, Dropbox, GitHub 및 VSTS(Visual Studio Team Services)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="9d8f9-106">따라서 Azure에사 이러한 통합된 서비스 트리거 배포 중 하나를 사용하여 함수 코드가 업데이트된 워크플로를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="9d8f9-107">Azure Functions를 처음 접하는 경우 [Azure 함수 개요](functions-overview.md)로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="9d8f9-108">연속 배포는 여러 개의 빈번한 작성자가 통합되는 프로젝트에 적합한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="9d8f9-109">또한 함수 코드에서 소스 제어를 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="9d8f9-110">현재 지원되는 배포 원본은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="9d8f9-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="9d8f9-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="9d8f9-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="9d8f9-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="9d8f9-113">외부 리포지토리(Git 또는 Mercurial)</span><span class="sxs-lookup"><span data-stu-id="9d8f9-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="9d8f9-114">Git 로컬 리포지토리</span><span class="sxs-lookup"><span data-stu-id="9d8f9-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="9d8f9-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="9d8f9-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="9d8f9-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="9d8f9-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="9d8f9-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9d8f9-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="9d8f9-118">배포는 함수 앱별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="9d8f9-119">연속 배포가 활성화된 후 포털에서 함수 코드에 대한 액세스는 *읽기 전용*으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="9d8f9-120">연속 배포 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9d8f9-120">Continuous deployment requirements</span></span>

<span data-ttu-id="9d8f9-121">연속 배포를 설정하기 전에 구성된 배포 원본 및 배포 원본에 함수 코드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="9d8f9-122">지정된 함수 앱 배포에서 각 함수는 명명된 하위 디렉터리에 있으며, 여기서 디렉터리 이름은 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="9d8f9-123">연속 배포 설정</span><span class="sxs-lookup"><span data-stu-id="9d8f9-123">Set up continuous deployment</span></span>
<span data-ttu-id="9d8f9-124">다음 절차를 사용하여 기존 함수 앱에 대한 연속 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="9d8f9-125">다음 단계에서는 GitHub 리포지토리와의 통합을 보여 주지만 Visual Studio Team Services 또는 기타 배포 서비스에도 유사한 단계가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="9d8f9-126">[Azure Portal](https://portal.azure.com)의 함수 앱에서 **플랫폼 기능** 및 **배포 옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="9d8f9-128">그런 다음 **배포** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="9d8f9-130">**배포 원본** 블레이드에서 **원본 선택**을 클릭한 다음 선택한 배포 원본에 대한 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![배포 원본 선택](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="9d8f9-132">연속 배포가 구성된 후 배포 원본의 모든 파일 변경 내용이 함수 앱으로 복사되고 전체 사이트 배포가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="9d8f9-133">원본의 파일이 업데이트될 때 사이트가 다시 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="9d8f9-134">배포 옵션</span><span class="sxs-lookup"><span data-stu-id="9d8f9-134">Deployment options</span></span>

<span data-ttu-id="9d8f9-135">다음은 몇 가지 일반적인 배포 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="9d8f9-136">스테이징 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="9d8f9-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="9d8f9-137">기존 함수를 연속 배포로 이동</span><span class="sxs-lookup"><span data-stu-id="9d8f9-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="9d8f9-138">스테이징 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="9d8f9-138">Create a staging deployment</span></span>

<span data-ttu-id="9d8f9-139">함수 앱은 배포 슬롯을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="9d8f9-140">그러나 연속 통합을 사용하여 별도 스테이징 및 프로덕션 배포를 계속 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="9d8f9-141">구성할 프로세스 및 스테이징 배포 작업은 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="9d8f9-142">구독에서 프로덕션 코드와 스테이징에 대한 두 개의 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="9d8f9-143">아직 없는 경우 배포 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="9d8f9-144">이 예제에서는 [GitHub]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="9d8f9-145">프로덕션 함수 앱의 경우 **연속 배포 설정**에서 앞의 단계를 완료하고 GitHub 리포지토리의 마스터 분기에 배포 분기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![배포 분기 선택](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="9d8f9-147">스테이징 함수 앱에 대해 이 단계를 반복하지만 GitHub 리포지토리 대신 스테이징 분기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="9d8f9-148">배포 원본이 분기를 지원하지 않는 경우 다른 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="9d8f9-149">스테이징 분기 또는 폴더에서 코드를 업데이트한 후 스테이징 배포에 이러한 변경 내용이 반영되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="9d8f9-150">테스트 후 스테이징 분기의 변경 내용을 마스터 분기로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="9d8f9-151">이렇게 병합하면 프로덕션 함수 앱으로 트리거 배포가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="9d8f9-152">배포 원본이 분기를 지원하지 않는 경우 스테이징 폴더의 파일로 프로덕션 폴더의 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="9d8f9-153">기존 함수를 연속 배포로 이동</span><span class="sxs-lookup"><span data-stu-id="9d8f9-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="9d8f9-154">포털에서 만들고 유지 관리하는 기존 함수가 있는 경우 위에서 설명한 대로 연속 배포를 설정하려면 먼저 FTP 또는 로컬 Git 리포지토리를 사용하여 기존 함수 코드 파일을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="9d8f9-155">함수 앱에 대한 앱 서비스 설정에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="9d8f9-156">파일을 다운로드한 후 선택한 연속 배포 원본에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="9d8f9-157">연속 통합을 구성한 후 함수 포털에서 원본 파일을 더 이상 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="9d8f9-158">방법: 배포 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="9d8f9-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="9d8f9-159">방법: FTP를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d8f9-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="9d8f9-160">방법: 로컬 Git 리포지토리를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d8f9-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="9d8f9-161">방법: 배포 자격 증명 구성</span><span class="sxs-lookup"><span data-stu-id="9d8f9-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="9d8f9-162">FTP 또는 로컬 Git 리포지토리가 있는 함수 앱에서 파일을 다운로드하려면 먼저 사이트에 액세스할 수 있도록 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="9d8f9-163">자격 증명은 함수 앱 수준에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="9d8f9-164">다음 단계를 사용하여 Azure Portal에서 배포 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="9d8f9-165">[Azure Portal](https://portal.azure.com)의 함수 앱에서 **플랫폼 기능** 및 **배포 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![로컬 배포 자격 증명 설정](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="9d8f9-167">사용자 이름 및 암호를 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="9d8f9-168">이제 해당 자격 증명을 사용하여 FTP 또는 기본 제공 Git 리포지토리에서 함수 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="9d8f9-169">방법: FTP를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d8f9-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="9d8f9-170">[Azure Portal](https://portal.azure.com)의 함수 앱에서 **플랫폼 기능**을 클릭하고 **속성**을 클릭한 다음 **FTP/배포 사용자**, **FTP 호스트 이름** 및 **FTPS 호스트 이름** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="9d8f9-171">FTP 서버에 적절한 컨텍스트를 제공하기 위해 앱 이름을 포함하여 포털에서 표시한 대로 **FTP/배포 사용자**를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![배포 정보 가져오기](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="9d8f9-173">FTP 클라이언트에서 수집한 연결 정보를 사용하여 앱에 연결하고 함수에 대한 원본 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="9d8f9-174">방법: 로컬 Git 리포지토리를 사용하여 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d8f9-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="9d8f9-175">[Azure Portal](https://portal.azure.com)의 함수 앱에서 **플랫폼 기능** 및 **배포 옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="9d8f9-177">그런 다음 **배포** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![연속 배포 설정](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="9d8f9-179">**배포 원본** 블레이드에서 **로컬 Git 리포지토리**를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="9d8f9-180">**플랫폼 기능**에서 **속성**을 클릭하고 Git URL의 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![연속 배포 설정](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="9d8f9-182">Git 인식 명령 프롬프트 또는 즐겨 찾는 Git 도구를 사용하여 로컬 컴퓨터에서 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="9d8f9-183">Git 복제 명령은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="9d8f9-184">다음 예제와 같이 함수 앱의 파일을 로컬 컴퓨터의 복제로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="9d8f9-185">요청된 경우 [구성된 배포 자격 증명](#credentials)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8f9-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="9d8f9-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="9d8f9-186">[GitHub]: https://github.com/</span></span>
