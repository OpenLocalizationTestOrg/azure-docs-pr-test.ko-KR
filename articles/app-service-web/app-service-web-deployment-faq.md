---
title: "Azure 웹 앱에 대 한 Faq aaaDeployment | Microsoft Docs"
description: "Azure 앱 서비스의 hello 웹 응용 프로그램 기능에 대 한 배포에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a><span data-ttu-id="8e11e-103">Azure의 Web Apps에 대한 배포 FAQ</span><span class="sxs-lookup"><span data-stu-id="8e11e-103">Deployment FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="8e11e-104">이 문서는 질문과 대답 (Faq) 배포 문제에 대 한 hello에 대 한 답변 toofrequently [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-104">This article has answers toofrequently asked questions (FAQs) about deployment issues for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a><span data-ttu-id="8e11e-105">App Service Web Apps를 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-105">I am just getting started with App Service web apps.</span></span> <span data-ttu-id="8e11e-106">내 코드를 어떻게 게시할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-106">How do I publish my code?</span></span>

<span data-ttu-id="8e11e-107">다음은 웹앱 코드를 게시할 수 있는 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-107">Here are some options for publishing your web app code:</span></span>

*   <span data-ttu-id="8e11e-108">Visual Studio를 사용하여 배포.</span><span class="sxs-lookup"><span data-stu-id="8e11e-108">Deploy by using Visual Studio.</span></span> <span data-ttu-id="8e11e-109">Hello Visual Studio 솔루션을 구현할 경우 hello 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-109">If you have hello Visual Studio solution, right-click hello web application project, and then select **Publish**.</span></span>
*   <span data-ttu-id="8e11e-110">FTP 클라이언트를 사용하여 배포.</span><span class="sxs-lookup"><span data-stu-id="8e11e-110">Deploy by using an FTP client.</span></span> <span data-ttu-id="8e11e-111">Hello Azure 포털에서에서 다운로드 hello 게시 hello 웹 앱에 대 한 프로필 되도록 toodeploy 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-111">In hello Azure portal, download hello publish profile for hello web app that you want toodeploy your code to.</span></span> <span data-ttu-id="8e11e-112">그런 다음 hello 파일 too\site\wwwroot 업로드 hello를 사용 하 여 동일한 게시 프로필 FTP 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-112">Then, upload hello files too\site\wwwroot by using hello same publish profile FTP credentials.</span></span>

<span data-ttu-id="8e11e-113">자세한 내용은 참조 [프로그램 응용 프로그램 tooApp 서비스 배포](web-sites-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-113">For more information, see [Deploy your app tooApp Service](web-sites-deploy.md).</span></span>

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a><span data-ttu-id="8e11e-114">Visual Studio에서 toodeploy 려 할 때 오류 메시지가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-114">I see an error message when I try toodeploy from Visual Studio.</span></span> <span data-ttu-id="8e11e-115">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-115">How do I resolve this?</span></span>

<span data-ttu-id="8e11e-116">Hello 메시지의 뒤에 표시 되 면 사용할 수 있습니다 hello SDK의 이전 버전: "리소스 그룹 'YourResourceGroup'에서 'YourResourceName' 리소스에 대 한 배포 중 오류가 발생 했습니다: MissingRegistrationForLocation: hello 구독에 등록 되지 않습니다 hello의 리소스 종류가 '구성 요소' hello 위치 ' 중앙 미국 '.</span><span class="sxs-lookup"><span data-stu-id="8e11e-116">If you see hello following message, you might be using an older version of hello SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: hello subscription is not registered for hello resource type 'components' in hello location 'Central US'.</span></span> <span data-ttu-id="8e11e-117">다시 등록 하십시오 순서 toohave 액세스 toothis 위치에이 공급자에 대 한. "</span><span class="sxs-lookup"><span data-stu-id="8e11e-117">Please re-register for this provider in order toohave access toothis location.”</span></span> 

<span data-ttu-id="8e11e-118">tooresolve이 오류, 업그레이드 toohello [최신 SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-118">tooresolve this error, upgrade toohello [latest SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8e11e-119">이 메시지가 나타나는 경우 최신 SDK hello 있는, 지원 요청을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-119">If you see this message and you have hello latest SDK, submit a support request.</span></span>

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a><span data-ttu-id="8e11e-120">Visual Studio tooApp 서비스에서에서 ASP.NET 응용 프로그램를 어떻게 배포 합니까?</span><span class="sxs-lookup"><span data-stu-id="8e11e-120">How do I deploy an ASP.NET application from Visual Studio tooApp Service?</span></span>
<a id="deployasp"></a>

<span data-ttu-id="8e11e-121">hello 자습서 [5 분 후에 Azure에서 첫 번째 ASP.NET 웹 앱 만들기](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) toodeploy ASP.NET Visual Studio 2015를 사용 하 여 앱 서비스에서 응용 프로그램 tooa 웹 앱에 웹 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-121">hello tutorial [Create your first ASP.NET web app in Azure in five minutes](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) shows you how toodeploy an ASP.NET web application tooa web app in App Service by using Visual Studio 2015.</span></span>

## <a name="what-are-hello-different-types-of-deployment-credentials"></a><span data-ttu-id="8e11e-122">배포 자격 증명의 hello 다른 유형은 무엇 인가요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-122">What are hello different types of deployment credentials?</span></span>

<span data-ttu-id="8e11e-123">App Service에서는 로컬 Git 배포 및 FTP/S 배포에 대한 두 가지 형식의 자격 증명을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span></span> <span data-ttu-id="8e11e-124">방법에 대 한 자세한 내용은 tooconfigure 배포 자격 증명 참조 [응용 프로그램 서비스에 대 한 배포 자격 증명을 구성](app-service-deployment-credentials.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-124">For more information about how tooconfigure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span></span>

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a><span data-ttu-id="8e11e-125">앱 서비스 웹 응용 프로그램의 hello 파일 또는 디렉터리 구조는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8e11e-125">What is hello file or directory structure of my App Service web app?</span></span>

<span data-ttu-id="8e11e-126">앱 서비스 앱의 hello 파일 구조에 대 한 정보를 참조 하십시오. [Azure에서 파일 구조](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-126">For information about hello file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span></span>

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a><span data-ttu-id="8e11e-127">어떻게 해결할 수 있습니까 "FTP 오류 550-여기 않습니다 hello 디스크 공간이 부족" 려 할 때 tooFTP 내 파일?</span><span class="sxs-lookup"><span data-stu-id="8e11e-127">How do I resolve "FTP Error 550 - There is not enough space on hello disk" when I try tooFTP my files?</span></span>

<span data-ttu-id="8e11e-128">이 메시지가 표시 될 웹 앱에 대 한 hello 서비스 계획의 디스크 할당량에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-128">If you see this message, it's likely that you are running into a disk quota in hello service plan for your web app.</span></span> <span data-ttu-id="8e11e-129">디스크 공간 요구 사항에 따라 tooa 더 높은 서비스 계층을 tooscale를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-129">You might need tooscale up tooa higher service tier based on your disk space needs.</span></span> <span data-ttu-id="8e11e-130">가격 계획 및 리소스 제한에 대한 자세한 내용은 [App Service 가격](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e11e-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a><span data-ttu-id="8e11e-131">내 App Service 웹앱에 대한 지속적인 배포를 설정하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-131">How do I set up continuous deployment for my App Service web app?</span></span>

<span data-ttu-id="8e11e-132">Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox 및 기타 Git 리포지토리를 포함한 여러 리소스에서 지속적인 배포를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-132">You can set up continuous deployment from several resources, including Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span></span> <span data-ttu-id="8e11e-133">이러한 옵션은 hello 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-133">These options are available in hello portal.</span></span> <span data-ttu-id="8e11e-134">[연속 배포 tooApp 서비스](app-service-continuous-deployment.md) 설명 하는 것이 도움이 자습서가 어떻게 tooset 연속 배포를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-134">[Continuous deployment tooApp Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how tooset up continuous deployment.</span></span>

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a><span data-ttu-id="8e11e-135">GitHub 및 Bitbucket의 지속적인 배포 관련 문제를 해결하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span></span>

<span data-ttu-id="8e11e-136">GitHub 또는 Bitbucket의 지속적인 배포 관련 문제를 조사하는 방법에 대한 자세한 내용은 [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)(지속적인 배포 조사)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e11e-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span></span>

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a><span data-ttu-id="8e11e-137">FTP 사이트를 toomy 및 코드를 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-137">I can't FTP toomy site and publish my code.</span></span> <span data-ttu-id="8e11e-138">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-138">How do I resolve this?</span></span>

<span data-ttu-id="8e11e-139">FTP tooresolve 문제:</span><span class="sxs-lookup"><span data-stu-id="8e11e-139">tooresolve FTP issues:</span></span>

1. <span data-ttu-id="8e11e-140">Hello 올바른 호스트 이름 및 자격 증명을 입력 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-140">Verify that you are entering hello correct host name and credentials.</span></span> <span data-ttu-id="8e11e-141">다른 형식의 자격 증명에 대 한 자세한 내용은 toouse, 참조 및 [배포 자격 증명](https://github.com/projectkudu/kudu/wiki/Deployment-credentials)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-141">For detailed information about different types of credentials and how toouse them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span></span>
2. <span data-ttu-id="8e11e-142">Hello FTP 포트가 방화벽에 의해 차단 되지 않은 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-142">Verify that hello FTP ports are not blocked by a firewall.</span></span> <span data-ttu-id="8e11e-143">hello 포트에는 이러한 설정을 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-143">hello ports should have these settings:</span></span>
    * <span data-ttu-id="8e11e-144">FTP 제어 연결 포트: 21</span><span class="sxs-lookup"><span data-stu-id="8e11e-144">FTP control connection port: 21</span></span>
    * <span data-ttu-id="8e11e-145">FTP 데이터 연결 포트: 989, 10001-10300</span><span class="sxs-lookup"><span data-stu-id="8e11e-145">FTP data connection port: 989, 10001-10300</span></span>

## <a name="how-do-i-publish-my-code-tooapp-service"></a><span data-ttu-id="8e11e-146">내 코드 tooApp 서비스 게시 방법</span><span class="sxs-lookup"><span data-stu-id="8e11e-146">How do I publish my code tooApp Service?</span></span>

<span data-ttu-id="8e11e-147">hello Azure 빠른 시작은 설계 된 toohelp hello 배포 스택 및 선택한 방법을 사용 하 여 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-147">hello Azure Quickstart is designed toohelp you deploy your app by using hello deployment stack and method of your choice.</span></span> <span data-ttu-id="8e11e-148">hello Azure 포털에에서 대 한 빠른 시작, toouse hello 너무 이동**설정** > **앱 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-148">toouse hello Quickstart, in hello Azure portal, go too**Settings** > **App Deployment**.</span></span>

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a><span data-ttu-id="8e11e-149">이유 내 앱 때로는 후가 다시 시작 서비스 배포 tooApp?</span><span class="sxs-lookup"><span data-stu-id="8e11e-149">Why does my app sometimes restart after deployment tooApp Service?</span></span>

<span data-ttu-id="8e11e-150">응용 프로그램 배포를 다시 시작 될 수 있습니다 hello 상황에 대 한 toolearn 참조 [런타임 문제 및 배포](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts")합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-150">toolearn about hello circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span></span> <span data-ttu-id="8e11e-151">앱 서비스는 hello 문서에 설명 된 대로 파일 toohello wwwroot 폴더를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-151">As hello article describes, App Service deploys files toohello wwwroot folder.</span></span> <span data-ttu-id="8e11e-152">앱을 직접 다시 시작하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-152">It never directly restarts your app.</span></span>

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a><span data-ttu-id="8e11e-153">App Service에 Visual Studio Team Services 코드를 통합하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="8e11e-153">How do I integrate Visual Studio Team Services code with App Service?</span></span>

<span data-ttu-id="8e11e-154">Visual Studio Team Services에서 지속적인 배포를 사용할 수 있는 다음과 같은 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-154">You have two options for using continuous deployment with Visual Studio Team Services:</span></span>

*   <span data-ttu-id="8e11e-155">Git 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-155">Use a Git project.</span></span> <span data-ttu-id="8e11e-156">해당 리포지토리에 대 한 hello 배포 옵션을 사용 하 여 응용 프로그램 서비스를 통해 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-156">Connect via App Service by using hello deployment options for that repo.</span></span>
*   <span data-ttu-id="8e11e-157">TFVC(Team Foundation Version Control) 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-157">Use a Team Foundation Version Control (TFVC) project.</span></span> <span data-ttu-id="8e11e-158">응용 프로그램 서비스에 대 한 hello 빌드 에이전트를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-158">Deploy by using hello build agent for App Service.</span></span>

<span data-ttu-id="8e11e-159">이러한 두 가지 옵션에 대한 연속 코드 배포는 기존 개발자 워크플로 및 체크 인 절차에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span></span> <span data-ttu-id="8e11e-160">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e11e-160">For more information, see these articles:</span></span> 

*   [<span data-ttu-id="8e11e-161">사용자 앱 tooan Azure 웹 사이트의 연속 배포를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-161">Implement continuous deployment of your app tooan Azure website</span></span>](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [<span data-ttu-id="8e11e-162">Tooa 웹 응용 프로그램을 배포할 수 있도록 Visual Studio Team Services 계정을 설정합니다</span><span class="sxs-lookup"><span data-stu-id="8e11e-162">Set up a Visual Studio Team Services account so it can deploy tooa web app</span></span>](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a><span data-ttu-id="8e11e-163">FTP 또는 FTPS toodeploy 내 앱 tooApp 서비스도 사용 방법</span><span class="sxs-lookup"><span data-stu-id="8e11e-163">How do I use FTP or FTPS toodeploy my app tooApp Service?</span></span>

<span data-ttu-id="8e11e-164">FTP 또는 FTPS toodeploy 사용에 대 한 내용은 웹 앱 tooApp 서비스 참조 [FTP/S를 사용 하 여 사용자 앱 tooApp 서비스 배포](app-service-deploy-ftp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e11e-164">For information about using FTP or FTPS toodeploy your web app tooApp Service, see [Deploy your app tooApp Service by using FTP/S](app-service-deploy-ftp.md).</span></span>
