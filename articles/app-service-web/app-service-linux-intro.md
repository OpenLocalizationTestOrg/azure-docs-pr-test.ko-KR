---
title: "Linux의 Azure Web App 소개 | Microsoft Docs"
description: "Linux의 Azure Web App에 대해 자세히 알아봅니다."
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="2bf68-104">Linux의 Azure Web App 소개</span><span class="sxs-lookup"><span data-stu-id="2bf68-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="2bf68-105">개요</span><span class="sxs-lookup"><span data-stu-id="2bf68-105">Overview</span></span>
<span data-ttu-id="2bf68-106">고객은 지원되는 응용 프로그램 스택에 대해 Linux의 웹앱을 사용하여 Linux에서 웹앱을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="2bf68-107">다음 섹션에는 현재 지원되는 응용 프로그램 스택이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="2bf68-108">기능</span><span class="sxs-lookup"><span data-stu-id="2bf68-108">Features</span></span>
<span data-ttu-id="2bf68-109">Linux의 웹앱은 Service는 현재 다음과 같은 응용 프로그램 스택을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="2bf68-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="2bf68-110">Node.js</span></span>
    * <span data-ttu-id="2bf68-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="2bf68-111">4.4</span></span>
    * <span data-ttu-id="2bf68-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="2bf68-112">4.5</span></span>
    * <span data-ttu-id="2bf68-113">6.2</span><span class="sxs-lookup"><span data-stu-id="2bf68-113">6.2</span></span>
    * <span data-ttu-id="2bf68-114">6.6</span><span class="sxs-lookup"><span data-stu-id="2bf68-114">6.6</span></span>
    * <span data-ttu-id="2bf68-115">6.9</span><span class="sxs-lookup"><span data-stu-id="2bf68-115">6.9</span></span>
    * <span data-ttu-id="2bf68-116">6.10</span><span class="sxs-lookup"><span data-stu-id="2bf68-116">6.10</span></span>
    * <span data-ttu-id="2bf68-117">6.11</span><span class="sxs-lookup"><span data-stu-id="2bf68-117">6.11</span></span>
    * <span data-ttu-id="2bf68-118">8.0</span><span class="sxs-lookup"><span data-stu-id="2bf68-118">8.0</span></span>
    * <span data-ttu-id="2bf68-119">8.1</span><span class="sxs-lookup"><span data-stu-id="2bf68-119">8.1</span></span>
* <span data-ttu-id="2bf68-120">PHP</span><span class="sxs-lookup"><span data-stu-id="2bf68-120">PHP</span></span>
    * <span data-ttu-id="2bf68-121">5.6</span><span class="sxs-lookup"><span data-stu-id="2bf68-121">5.6</span></span>
    * <span data-ttu-id="2bf68-122">7.0</span><span class="sxs-lookup"><span data-stu-id="2bf68-122">7.0</span></span>
* <span data-ttu-id="2bf68-123">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2bf68-123">.Net Core</span></span>
    * <span data-ttu-id="2bf68-124">1.0</span><span class="sxs-lookup"><span data-stu-id="2bf68-124">1.0</span></span>
    * <span data-ttu-id="2bf68-125">1.1</span><span class="sxs-lookup"><span data-stu-id="2bf68-125">1.1</span></span>
* <span data-ttu-id="2bf68-126">루비</span><span class="sxs-lookup"><span data-stu-id="2bf68-126">Ruby</span></span>
    * <span data-ttu-id="2bf68-127">2.3</span><span class="sxs-lookup"><span data-stu-id="2bf68-127">2.3</span></span>

<span data-ttu-id="2bf68-128">고객은 다음을 사용하여 해당 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="2bf68-129">FTP</span><span class="sxs-lookup"><span data-stu-id="2bf68-129">FTP</span></span>
* <span data-ttu-id="2bf68-130">로컬 Git</span><span class="sxs-lookup"><span data-stu-id="2bf68-130">Local Git</span></span>
* <span data-ttu-id="2bf68-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="2bf68-131">GitHub</span></span>
* <span data-ttu-id="2bf68-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="2bf68-132">Bitbucket</span></span>

<span data-ttu-id="2bf68-133">응용 프로그램 크기 조정:</span><span class="sxs-lookup"><span data-stu-id="2bf68-133">For application scaling:</span></span>

* <span data-ttu-id="2bf68-134">고객은 App Service 계획의 계층을 변경하여 웹앱을 확장 및 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="2bf68-135">고객은 자신의 SKU 범위 내에서 응용 프로그램을 규모 확장하고 여러 앱 인스턴스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="2bf68-136">Kudu의 경우 일부 기본 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="2bf68-137">환경</span><span class="sxs-lookup"><span data-stu-id="2bf68-137">Environments</span></span>
* <span data-ttu-id="2bf68-138">배포</span><span class="sxs-lookup"><span data-stu-id="2bf68-138">Deployments</span></span>
* <span data-ttu-id="2bf68-139">기본 콘솔</span><span class="sxs-lookup"><span data-stu-id="2bf68-139">Basic console</span></span>
* <span data-ttu-id="2bf68-140">SSH</span><span class="sxs-lookup"><span data-stu-id="2bf68-140">SSH</span></span>

<span data-ttu-id="2bf68-141">devops:</span><span class="sxs-lookup"><span data-stu-id="2bf68-141">For devops:</span></span>

* <span data-ttu-id="2bf68-142">스테이징 환경</span><span class="sxs-lookup"><span data-stu-id="2bf68-142">Staging environments</span></span>
* <span data-ttu-id="2bf68-143">ACR 및 DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="2bf68-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="2bf68-144">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2bf68-144">Limitations</span></span>
<span data-ttu-id="2bf68-145">Azure Portal에는 Linux의 웹앱에 대해 작동하는 기능만 표시되고 나머지는 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="2bf68-146">더 많은 기능이 사용 가능해지면 포털에 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="2bf68-147">가상 네트워크 통합, Azure Active Directory/타사 인증 또는 Kudu 사이트 확장 등의 일부 기능은 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="2bf68-148">이러한 기능이 사용 가능해지면 설명서와 블로그에 변경 내용이 업데이트될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="2bf68-149">이 공개 미리 보기는 현재 다음 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="2bf68-150">미국 서부</span><span class="sxs-lookup"><span data-stu-id="2bf68-150">West US</span></span>
* <span data-ttu-id="2bf68-151">미국 동부</span><span class="sxs-lookup"><span data-stu-id="2bf68-151">East US</span></span>
* <span data-ttu-id="2bf68-152">서유럽</span><span class="sxs-lookup"><span data-stu-id="2bf68-152">West Europe</span></span>
* <span data-ttu-id="2bf68-153">북유럽</span><span class="sxs-lookup"><span data-stu-id="2bf68-153">North Europe</span></span>
* <span data-ttu-id="2bf68-154">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="2bf68-154">South Central US</span></span>
* <span data-ttu-id="2bf68-155">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="2bf68-155">North Central US</span></span>
* <span data-ttu-id="2bf68-156">동남아시아</span><span class="sxs-lookup"><span data-stu-id="2bf68-156">Southeast Asia</span></span>
* <span data-ttu-id="2bf68-157">동아시아</span><span class="sxs-lookup"><span data-stu-id="2bf68-157">East Asia</span></span>
* <span data-ttu-id="2bf68-158">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="2bf68-158">Australia East</span></span>
* <span data-ttu-id="2bf68-159">일본 동부</span><span class="sxs-lookup"><span data-stu-id="2bf68-159">Japan East</span></span>
* <span data-ttu-id="2bf68-160">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="2bf68-160">Brazil South</span></span>
* <span data-ttu-id="2bf68-161">인도 남부</span><span class="sxs-lookup"><span data-stu-id="2bf68-161">South India</span></span>

<span data-ttu-id="2bf68-162">Linux의 Web Apps는 전용 App Service 계획에서만 지원되며 무료 또는 공유 계층은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="2bf68-163">또한 일반 및 Linux 웹앱에 대한 App Service 계획은 상호 배타적이므로 비 Linux App Service 계획에서 Linux 웹앱을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="2bf68-164">Linux의 Web Apps는 동일한 지역에 비 Linux 웹앱을 포함하지 않는 리소스 그룹에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2bf68-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2bf68-165">Troubleshooting</span></span> ##

<span data-ttu-id="2bf68-166">응용 프로그램이 시작되지 못하거나 앱에서 로깅을 확인하려는 경우 LogFiles 디렉터리에서 Docker 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="2bf68-167">SCM 사이트 또는 FTP를 통해 이 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="2bf68-168">컨테이너에서 `stdout` 및 `stderr`을 로그하려면 **진단 로그** 아래에서 **Docker 컨테이너 로깅**을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![로깅 사용][2]

![Kudu를 사용하여 Docker 로그 보기][1]

<span data-ttu-id="2bf68-171">**고급 도구**의 **개발 도구** 메뉴에서 SCM 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bf68-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2bf68-172">Next steps</span></span>
<span data-ttu-id="2bf68-173">Linux에서 App Service를 시작하려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bf68-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="2bf68-174">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bf68-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="2bf68-175">Linux에서 Azure Web App에 대한 사용자 지정 Docker 이미지를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="2bf68-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="2bf68-176">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="2bf68-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2bf68-177">Linux의 Azure App Service Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="2bf68-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="2bf68-178">Linux의 Azure App Service Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="2bf68-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="2bf68-179">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="2bf68-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="2bf68-180">Linux의 Azure Web App에 대한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="2bf68-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="2bf68-181">Azure App Service에서 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="2bf68-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="2bf68-182">Linux에서 Azure Web App을 사용한 Docker 허브 연속 배포</span><span class="sxs-lookup"><span data-stu-id="2bf68-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png