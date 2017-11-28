---
title: "웹 응용 프로그램에 액세스 Linux aaaIntroduction tooAzure | Microsoft Docs"
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
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="2a6dc-104">소개 tooAzure Linux에서 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2a6dc-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="2a6dc-105">개요</span><span class="sxs-lookup"><span data-stu-id="2a6dc-105">Overview</span></span>
<span data-ttu-id="2a6dc-106">고객 스택 되는 응용 프로그램에 대 한 기본적으로 Linux에서 Linux toohost 웹 앱에 웹 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="2a6dc-107">hello 다음 섹션에는 현재 지원 되는 hello 응용 프로그램 스택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="2a6dc-108">기능</span><span class="sxs-lookup"><span data-stu-id="2a6dc-108">Features</span></span>
<span data-ttu-id="2a6dc-109">현재 웹 응용 프로그램에 액세스 Linux 응용 프로그램 스택 다음 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="2a6dc-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="2a6dc-110">Node.js</span></span>
    * <span data-ttu-id="2a6dc-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-111">4.4</span></span>
    * <span data-ttu-id="2a6dc-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-112">4.5</span></span>
    * <span data-ttu-id="2a6dc-113">6.2</span><span class="sxs-lookup"><span data-stu-id="2a6dc-113">6.2</span></span>
    * <span data-ttu-id="2a6dc-114">6.6</span><span class="sxs-lookup"><span data-stu-id="2a6dc-114">6.6</span></span>
    * <span data-ttu-id="2a6dc-115">6.9</span><span class="sxs-lookup"><span data-stu-id="2a6dc-115">6.9</span></span>
    * <span data-ttu-id="2a6dc-116">6.10</span><span class="sxs-lookup"><span data-stu-id="2a6dc-116">6.10</span></span>
    * <span data-ttu-id="2a6dc-117">6.11</span><span class="sxs-lookup"><span data-stu-id="2a6dc-117">6.11</span></span>
    * <span data-ttu-id="2a6dc-118">8.0</span><span class="sxs-lookup"><span data-stu-id="2a6dc-118">8.0</span></span>
    * <span data-ttu-id="2a6dc-119">8.1</span><span class="sxs-lookup"><span data-stu-id="2a6dc-119">8.1</span></span>
* <span data-ttu-id="2a6dc-120">PHP</span><span class="sxs-lookup"><span data-stu-id="2a6dc-120">PHP</span></span>
    * <span data-ttu-id="2a6dc-121">5.6</span><span class="sxs-lookup"><span data-stu-id="2a6dc-121">5.6</span></span>
    * <span data-ttu-id="2a6dc-122">7.0</span><span class="sxs-lookup"><span data-stu-id="2a6dc-122">7.0</span></span>
* <span data-ttu-id="2a6dc-123">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2a6dc-123">.Net Core</span></span>
    * <span data-ttu-id="2a6dc-124">1.0</span><span class="sxs-lookup"><span data-stu-id="2a6dc-124">1.0</span></span>
    * <span data-ttu-id="2a6dc-125">1.1</span><span class="sxs-lookup"><span data-stu-id="2a6dc-125">1.1</span></span>
* <span data-ttu-id="2a6dc-126">루비</span><span class="sxs-lookup"><span data-stu-id="2a6dc-126">Ruby</span></span>
    * <span data-ttu-id="2a6dc-127">2.3</span><span class="sxs-lookup"><span data-stu-id="2a6dc-127">2.3</span></span>

<span data-ttu-id="2a6dc-128">고객은 다음을 사용하여 해당 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="2a6dc-129">FTP</span><span class="sxs-lookup"><span data-stu-id="2a6dc-129">FTP</span></span>
* <span data-ttu-id="2a6dc-130">로컬 Git</span><span class="sxs-lookup"><span data-stu-id="2a6dc-130">Local Git</span></span>
* <span data-ttu-id="2a6dc-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="2a6dc-131">GitHub</span></span>
* <span data-ttu-id="2a6dc-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="2a6dc-132">Bitbucket</span></span>

<span data-ttu-id="2a6dc-133">응용 프로그램 크기 조정:</span><span class="sxs-lookup"><span data-stu-id="2a6dc-133">For application scaling:</span></span>

* <span data-ttu-id="2a6dc-134">고객 웹 앱 및 축소 하 여 확장할 수 해당 앱 서비스 계획의 hello 계층을 변경</span><span class="sxs-lookup"><span data-stu-id="2a6dc-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="2a6dc-135">고객 응용 프로그램을 확장 하 고 자신의 SKU의 hello 범위 내에서 여러 응용 프로그램 인스턴스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="2a6dc-136">에 대 한 Kudu hello 기본 기능 중 일부:</span><span class="sxs-lookup"><span data-stu-id="2a6dc-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="2a6dc-137">환경</span><span class="sxs-lookup"><span data-stu-id="2a6dc-137">Environments</span></span>
* <span data-ttu-id="2a6dc-138">배포</span><span class="sxs-lookup"><span data-stu-id="2a6dc-138">Deployments</span></span>
* <span data-ttu-id="2a6dc-139">기본 콘솔</span><span class="sxs-lookup"><span data-stu-id="2a6dc-139">Basic console</span></span>
* <span data-ttu-id="2a6dc-140">SSH</span><span class="sxs-lookup"><span data-stu-id="2a6dc-140">SSH</span></span>

<span data-ttu-id="2a6dc-141">devops:</span><span class="sxs-lookup"><span data-stu-id="2a6dc-141">For devops:</span></span>

* <span data-ttu-id="2a6dc-142">스테이징 환경</span><span class="sxs-lookup"><span data-stu-id="2a6dc-142">Staging environments</span></span>
* <span data-ttu-id="2a6dc-143">ACR 및 DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="2a6dc-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="2a6dc-144">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2a6dc-144">Limitations</span></span>
<span data-ttu-id="2a6dc-145">hello Azure 포털 현재 Linux에서 웹 앱에 대 한 작동 하는 유일한 기능을 표시 하거나 숨깁니다 hello rest 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="2a6dc-146">더 많은 기능을 사용 하도록 설정 하는 대로 hello 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="2a6dc-147">가상 네트워크 통합, Azure Active Directory/타사 인증 또는 Kudu 사이트 확장 등의 일부 기능은 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="2a6dc-148">이러한 기능을 사용할 수 되 면이 문서 및 블로그 hello 변경에 대 한 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="2a6dc-149">이 공개 미리 보기가 현재 hello 다음 영역에서에서 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="2a6dc-150">미국 서부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-150">West US</span></span>
* <span data-ttu-id="2a6dc-151">미국 동부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-151">East US</span></span>
* <span data-ttu-id="2a6dc-152">서유럽</span><span class="sxs-lookup"><span data-stu-id="2a6dc-152">West Europe</span></span>
* <span data-ttu-id="2a6dc-153">북유럽</span><span class="sxs-lookup"><span data-stu-id="2a6dc-153">North Europe</span></span>
* <span data-ttu-id="2a6dc-154">미국 중남부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-154">South Central US</span></span>
* <span data-ttu-id="2a6dc-155">미국 중북부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-155">North Central US</span></span>
* <span data-ttu-id="2a6dc-156">동남아시아</span><span class="sxs-lookup"><span data-stu-id="2a6dc-156">Southeast Asia</span></span>
* <span data-ttu-id="2a6dc-157">동아시아</span><span class="sxs-lookup"><span data-stu-id="2a6dc-157">East Asia</span></span>
* <span data-ttu-id="2a6dc-158">오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-158">Australia East</span></span>
* <span data-ttu-id="2a6dc-159">일본 동부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-159">Japan East</span></span>
* <span data-ttu-id="2a6dc-160">브라질 남부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-160">Brazil South</span></span>
* <span data-ttu-id="2a6dc-161">인도 남부</span><span class="sxs-lookup"><span data-stu-id="2a6dc-161">South India</span></span>

<span data-ttu-id="2a6dc-162">웹 앱 linux hello 전용된 앱 서비스 계획에서만 지원 됩니다 및 무료 또는 공유 계층에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="2a6dc-163">또한 일반 및 Linux 웹앱에 대한 App Service 계획은 상호 배타적이므로 비 Linux App Service 계획에서 Linux 웹앱을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="2a6dc-164">웹 앱이 Linux hello에서 비 Linux 웹 앱을 포함 하지 않는 리소스 그룹에 만들어야 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2a6dc-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2a6dc-165">Troubleshooting</span></span> ##

<span data-ttu-id="2a6dc-166">응용 프로그램 toostart 못하거나 toocheck hello 로깅 응용 프로그램에서 원하는 Docker가 hello LogFiles 디렉터리에 로그인 하는 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="2a6dc-167">SCM 사이트 또는 FTP를 통해 이 디렉터리에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="2a6dc-168">toolog hello `stdout` 및 `stderr` tooenable 사용자 컨테이너에서 필요한 **Docker 컨테이너 로깅** 아래 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![로깅 사용][2]

![Kudu tooview Docker 로그를 사용 하 여][1]

<span data-ttu-id="2a6dc-171">hello SCM 사이트에 액세스할 수 있습니다 **고급 도구** hello에 **개발 도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a6dc-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a6dc-172">Next steps</span></span>
<span data-ttu-id="2a6dc-173">다음 링크 tooget linux 응용 프로그램 서비스를 시작 하는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="2a6dc-174">[당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a6dc-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="2a6dc-175">Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법</span><span class="sxs-lookup"><span data-stu-id="2a6dc-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="2a6dc-176">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="2a6dc-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2a6dc-177">Linux의 Azure App Service Web App에서 .NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="2a6dc-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="2a6dc-178">Linux의 Azure App Service Web App에서 Ruby 사용</span><span class="sxs-lookup"><span data-stu-id="2a6dc-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="2a6dc-179">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="2a6dc-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="2a6dc-180">Linux의 Azure Web App에 대한 SSH 지원</span><span class="sxs-lookup"><span data-stu-id="2a6dc-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="2a6dc-181">Azure App Service에서 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="2a6dc-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="2a6dc-182">Linux에서 Azure Web App을 사용한 Docker 허브 연속 배포</span><span class="sxs-lookup"><span data-stu-id="2a6dc-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png