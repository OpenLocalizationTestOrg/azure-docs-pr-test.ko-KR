---
title: "Azure Web Apps에 대한 배포 FAQ | Microsoft Docs"
description: "Azure App Service Web Apps 기능의 배포에 대한 질문과 대답을 확인합니다."
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
ms.openlocfilehash: 69f8c50f7f5889b75544deca19c54268fbf5eca7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a><span data-ttu-id="b702e-103">Azure의 Web Apps에 대한 배포 FAQ</span><span class="sxs-lookup"><span data-stu-id="b702e-103">Deployment FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="b702e-104">이 문서에는 [Azure App Service의 Web Apps 기능](https://azure.microsoft.com/services/app-service/web/) 관련 배포 문제에 대한 FAQ(질문과 대답)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-104">This article has answers to frequently asked questions (FAQs) about deployment issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a><span data-ttu-id="b702e-105">App Service Web Apps를 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-105">I am just getting started with App Service web apps.</span></span> <span data-ttu-id="b702e-106">내 코드를 어떻게 게시할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-106">How do I publish my code?</span></span>

<span data-ttu-id="b702e-107">다음은 웹앱 코드를 게시할 수 있는 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-107">Here are some options for publishing your web app code:</span></span>

*   <span data-ttu-id="b702e-108">Visual Studio를 사용하여 배포.</span><span class="sxs-lookup"><span data-stu-id="b702e-108">Deploy by using Visual Studio.</span></span> <span data-ttu-id="b702e-109">Visual Studio 솔루션이 있는 경우 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭하고 나서 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-109">If you have the Visual Studio solution, right-click the web application project, and then select **Publish**.</span></span>
*   <span data-ttu-id="b702e-110">FTP 클라이언트를 사용하여 배포.</span><span class="sxs-lookup"><span data-stu-id="b702e-110">Deploy by using an FTP client.</span></span> <span data-ttu-id="b702e-111">Azure Portal에서 코드를 배포할 웹앱에 대한 게시 프로필을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-111">In the Azure portal, download the publish profile for the web app that you want to deploy your code to.</span></span> <span data-ttu-id="b702e-112">그다음에 동일한 게시 프로필 FTP 자격 증명을 사용하여 \site\wwwroot에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-112">Then, upload the files to \site\wwwroot by using the same publish profile FTP credentials.</span></span>

<span data-ttu-id="b702e-113">자세한 내용은 [App Service에 앱 배포](web-sites-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-113">For more information, see [Deploy your app to App Service](web-sites-deploy.md).</span></span>

## <a name="i-see-an-error-message-when-i-try-to-deploy-from-visual-studio-how-do-i-resolve-this"></a><span data-ttu-id="b702e-114">Visual Studio에서 배포하려고 할 때 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-114">I see an error message when I try to deploy from Visual Studio.</span></span> <span data-ttu-id="b702e-115">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-115">How do I resolve this?</span></span>

<span data-ttu-id="b702e-116">다음 메시지가 표시되면 SDK의 이전 버전을 사용하고 있을 수 있습니다. “리소스 그룹 ‘YourResourceGroup’의 ‘YourResourceName’ 리소스에 대한 배포에서 오류가 발생했습니다. MissingRegistrationForLocation: 구독이 ‘Central US’ 위치의 ‘components’ 리소스 형식에 대해 등록되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-116">If you see the following message, you might be using an older version of the SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: The subscription is not registered for the resource type 'components' in the location 'Central US'.</span></span> <span data-ttu-id="b702e-117">이 리소스 형식에 액세스할 수 있는 권한을 가지려면 이 공급자에 대해 다시 등록하세요.”</span><span class="sxs-lookup"><span data-stu-id="b702e-117">Please re-register for this provider in order to have access to this location.”</span></span> 

<span data-ttu-id="b702e-118">이 오류를 해결하려면 [최신 SDK](https://azure.microsoft.com/downloads/)로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-118">To resolve this error, upgrade to the [latest SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="b702e-119">이 메시지가 표시되고 최신 SDK가 있으면 지원 요청을 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-119">If you see this message and you have the latest SDK, submit a support request.</span></span>

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-to-app-service"></a><span data-ttu-id="b702e-120">Visual Studio에서 App Service로 ASP.NET 응용 프로그램을 배포하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-120">How do I deploy an ASP.NET application from Visual Studio to App Service?</span></span>
<a id="deployasp"></a>

<span data-ttu-id="b702e-121">[Azure에서 ASP.NET 웹앱 만들기](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) 자습서에서는 Visual Studio 2015를 사용하여 ASP.NET 웹 응용 프로그램을 Azure App Service의 웹앱에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-121">The tutorial [Create your first ASP.NET web app in Azure in five minutes](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) shows you how to deploy an ASP.NET web application to a web app in App Service by using Visual Studio 2015.</span></span>

## <a name="what-are-the-different-types-of-deployment-credentials"></a><span data-ttu-id="b702e-122">배포 자격 증명 형식에는 무엇이 있나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-122">What are the different types of deployment credentials?</span></span>

<span data-ttu-id="b702e-123">App Service에서는 로컬 Git 배포 및 FTP/S 배포에 대한 두 가지 형식의 자격 증명을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span></span> <span data-ttu-id="b702e-124">배포 자격 증명을 구성하는 방법에 대한 자세한 내용은 [App Service에 대한 배포 자격 증명 구성](app-service-deployment-credentials.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-124">For more information about how to configure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span></span>

## <a name="what-is-the-file-or-directory-structure-of-my-app-service-web-app"></a><span data-ttu-id="b702e-125">내 App Service 웹앱의 파일 또는 디렉터리 구조는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b702e-125">What is the file or directory structure of my App Service web app?</span></span>

<span data-ttu-id="b702e-126">App Service 앱의 파일 구조에 대한 자세한 내용은 [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)(Azure의 파일 구조)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-126">For information about the file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span></span>

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-the-disk-when-i-try-to-ftp-my-files"></a><span data-ttu-id="b702e-127">내 파일을 FTP하려고 할 때 “FTP 오류 550 - 디스크 공간이 부족합니다.” 메시지가 표시되면 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-127">How do I resolve "FTP Error 550 - There is not enough space on the disk" when I try to FTP my files?</span></span>

<span data-ttu-id="b702e-128">이 메시지가 표시되면 웹앱에 대한 서비스 계획에서 디스크 할당량에 도달한 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-128">If you see this message, it's likely that you are running into a disk quota in the service plan for your web app.</span></span> <span data-ttu-id="b702e-129">필요한 디스크 공간에 따라 상위 서비스 계층으로 확장해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-129">You might need to scale up to a higher service tier based on your disk space needs.</span></span> <span data-ttu-id="b702e-130">가격 계획 및 리소스 제한에 대한 자세한 내용은 [App Service 가격](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a><span data-ttu-id="b702e-131">내 App Service 웹앱에 대한 지속적인 배포를 설정하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-131">How do I set up continuous deployment for my App Service web app?</span></span>

<span data-ttu-id="b702e-132">Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox 및 기타 Git 리포지토리를 포함한 여러 리소스에서 지속적인 배포를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-132">You can set up continuous deployment from several resources, including Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span></span> <span data-ttu-id="b702e-133">이러한 옵션은 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-133">These options are available in the portal.</span></span> <span data-ttu-id="b702e-134">[App Service에 대한 지속적인 배포](app-service-continuous-deployment.md)는 지속적인 배포를 설정하는 방법을 설명하는 유용한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-134">[Continuous deployment to App Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how to set up continuous deployment.</span></span>

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a><span data-ttu-id="b702e-135">GitHub 및 Bitbucket의 지속적인 배포 관련 문제를 해결하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span></span>

<span data-ttu-id="b702e-136">GitHub 또는 Bitbucket의 지속적인 배포 관련 문제를 조사하는 방법에 대한 자세한 내용은 [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)(지속적인 배포 조사)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span></span>

## <a name="i-cant-ftp-to-my-site-and-publish-my-code-how-do-i-resolve-this"></a><span data-ttu-id="b702e-137">내 사이트에 FTP하고 내 코드를 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-137">I can't FTP to my site and publish my code.</span></span> <span data-ttu-id="b702e-138">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-138">How do I resolve this?</span></span>

<span data-ttu-id="b702e-139">FTP 문제를 해결하려면:</span><span class="sxs-lookup"><span data-stu-id="b702e-139">To resolve FTP issues:</span></span>

1. <span data-ttu-id="b702e-140">올바른 호스트 이름 및 자격 증명을 입력하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-140">Verify that you are entering the correct host name and credentials.</span></span> <span data-ttu-id="b702e-141">다양한 자격 증명 형식 및 이러한 자격 증명을 사용하는 방법에 대한 자세한 내용은 [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials)(배포 자격 증명)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-141">For detailed information about different types of credentials and how to use them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span></span>
2. <span data-ttu-id="b702e-142">FTP 포트가 방화벽으로 차단되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-142">Verify that the FTP ports are not blocked by a firewall.</span></span> <span data-ttu-id="b702e-143">포트에는 다음 설정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-143">The ports should have these settings:</span></span>
    * <span data-ttu-id="b702e-144">FTP 제어 연결 포트: 21</span><span class="sxs-lookup"><span data-stu-id="b702e-144">FTP control connection port: 21</span></span>
    * <span data-ttu-id="b702e-145">FTP 데이터 연결 포트: 989, 10001-10300</span><span class="sxs-lookup"><span data-stu-id="b702e-145">FTP data connection port: 989, 10001-10300</span></span>

## <a name="how-do-i-publish-my-code-to-app-service"></a><span data-ttu-id="b702e-146">App Service에 내 코드를 게시하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-146">How do I publish my code to App Service?</span></span>

<span data-ttu-id="b702e-147">Azure 빠른 시작은 선택한 배포 스택 및 방법을 사용하여 앱을 배포할 수 있도록 디자인되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-147">The Azure Quickstart is designed to help you deploy your app by using the deployment stack and method of your choice.</span></span> <span data-ttu-id="b702e-148">빠른 시작을 사용하려면 Azure Portal에서 **설정** > **앱 배포**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-148">To use the Quickstart, in the Azure portal, go to **Settings** > **App Deployment**.</span></span>

## <a name="why-does-my-app-sometimes-restart-after-deployment-to-app-service"></a><span data-ttu-id="b702e-149">App Service에 배포한 후 때때로 앱이 다시 시작되지 않는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b702e-149">Why does my app sometimes restart after deployment to App Service?</span></span>

<span data-ttu-id="b702e-150">응용 프로그램 배포 후 다시 시작되는 경우를 알아보려면 [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts")(배포 및 런타임 문제)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-150">To learn about the circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span></span> <span data-ttu-id="b702e-151">문서에서 설명하는 대로 App Service는 파일을 wwwroot 폴더에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-151">As the article describes, App Service deploys files to the wwwroot folder.</span></span> <span data-ttu-id="b702e-152">앱을 직접 다시 시작하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-152">It never directly restarts your app.</span></span>

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a><span data-ttu-id="b702e-153">App Service에 Visual Studio Team Services 코드를 통합하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-153">How do I integrate Visual Studio Team Services code with App Service?</span></span>

<span data-ttu-id="b702e-154">Visual Studio Team Services에서 지속적인 배포를 사용할 수 있는 다음과 같은 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-154">You have two options for using continuous deployment with Visual Studio Team Services:</span></span>

*   <span data-ttu-id="b702e-155">Git 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-155">Use a Git project.</span></span> <span data-ttu-id="b702e-156">해당 리포지토리에 대한 배포 옵션을 사용하여 App Service를 통해 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-156">Connect via App Service by using the deployment options for that repo.</span></span>
*   <span data-ttu-id="b702e-157">TFVC(Team Foundation Version Control) 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-157">Use a Team Foundation Version Control (TFVC) project.</span></span> <span data-ttu-id="b702e-158">App Service에 대한 빌드 에이전트를 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-158">Deploy by using the build agent for App Service.</span></span>

<span data-ttu-id="b702e-159">이러한 두 가지 옵션에 대한 연속 코드 배포는 기존 개발자 워크플로 및 체크 인 절차에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="b702e-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span></span> <span data-ttu-id="b702e-160">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-160">For more information, see these articles:</span></span> 

*   <span data-ttu-id="b702e-161">[Implement continuous deployment of your app to an Azure website](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)(Azure 웹 사이트에 대한 앱 지속적인 배포 구현)</span><span class="sxs-lookup"><span data-stu-id="b702e-161">[Implement continuous deployment of your app to an Azure website](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)</span></span>
*   <span data-ttu-id="b702e-162">[Set up a Visual Studio Team Services account so it can deploy to a web app](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)(웹앱에 배포할 수 있도록 Visual Studio Team Services 계정 설정)</span><span class="sxs-lookup"><span data-stu-id="b702e-162">[Set up a Visual Studio Team Services account so it can deploy to a web app](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)</span></span>

## <a name="how-do-i-use-ftp-or-ftps-to-deploy-my-app-to-app-service"></a><span data-ttu-id="b702e-163">FTP 또는 FTPS를 사용하여 App Service에 내 앱을 배포하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b702e-163">How do I use FTP or FTPS to deploy my app to App Service?</span></span>

<span data-ttu-id="b702e-164">FTP 또는 FTPS를 사용하여 App Service에 웹앱을 배포하는 방법에 대한 자세한 내용은 [FTP/S를 사용하여 App Service에 앱 배포](app-service-deploy-ftp.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b702e-164">For information about using FTP or FTPS to deploy your web app to App Service, see [Deploy your app to App Service by using FTP/S](app-service-deploy-ftp.md).</span></span>
