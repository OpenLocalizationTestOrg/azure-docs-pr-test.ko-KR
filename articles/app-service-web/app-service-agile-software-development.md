---
title: "Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발"
description: "agile 소프트웨어 개발을 지원하는 Azure 앱 서비스를 사용하여 고확장성 복합 응용 프로그램을 만드는 법을 배웁니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a><span data-ttu-id="f2c44-103">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="f2c44-103">Agile software development with Azure App Service</span></span>
<span data-ttu-id="f2c44-104">이 자습서에서는 [agile 소프트웨어 개발](https://en.wikipedia.org/wiki/Agile_software_development)을 지원하는 [Azure App Service](/azure/app-service/)를 사용하여 고확장성 복합 응용 프로그램을 만드는 법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-104">In this tutorial, you will learn how to create high-scale complex applications with [Azure App Service](/azure/app-service/) in a way that supports [agile software development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="f2c44-105">여기서는 사용자가 [Azure에서 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md)방법을 이미 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-105">It assumes that you already know how to [deploy complex applications predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="f2c44-106">Agile 방법론의 성공적인 구현을 기술적인 과정의 제약이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-106">Limitations in technical processes can often stand in the way of successful implementation of agile methodologies.</span></span> <span data-ttu-id="f2c44-107">Azure App Service를 [지속적인 게시](app-service-continuous-deployment.md), [스테이징 환경](web-sites-staged-publishing.md)(슬롯) 및 [모니터링](web-sites-monitor.md)과 같은 기능을 조합과 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)의 배포 관리와 잘 결합하면 Agile 소프트웨어 개발자에게 훌륭한 솔루션의 일부가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-107">Azure App Service with features such as [continuous publishing](app-service-continuous-deployment.md), [staging environments](web-sites-staged-publishing.md) (slots), and [monitoring](web-sites-monitor.md), when coupled wisely with the orchestration and management of deployment in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), can be part of a great solution for developers who embrace agile software development.</span></span>

<span data-ttu-id="f2c44-108">다음 표는 Agile 개발과 연관된 요구 사항의 최종 목록과, Azure 서비스가 이것들을 어떻게 사용 가능하게 만드는지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-108">The following table is a short list of requirements associated with agile development, and how Azure services enable each of them.</span></span>

| <span data-ttu-id="f2c44-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="f2c44-109">Requirement</span></span> | <span data-ttu-id="f2c44-110">Azure 사용할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="f2c44-110">How Azure enables</span></span> |
| --- | --- |
| <span data-ttu-id="f2c44-111">-모든 커밋을 사용하여 구축</span><span class="sxs-lookup"><span data-stu-id="f2c44-111">- Build with every commit</span></span><br><span data-ttu-id="f2c44-112">- 빠르게 자동적으로 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-112">- Build automatically and fast</span></span> |<span data-ttu-id="f2c44-113">지속적인 배포를 구성할 때, Azure 앱 서비스는 개발 분기점에 따라 실시간 구축 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-113">When configured with continuous deployment, Azure App Service can function as live-running builds based on a dev branch.</span></span> <span data-ttu-id="f2c44-114">모든 시간 코드는 분기점에 푸시되고, 자동적으로 Azure에서 구축하고 실시간으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-114">Every time code is pushed to the branch, it is automatically built and running live in Azure.</span></span> |
| <span data-ttu-id="f2c44-115">- 자체-테스트 빌드 구축하기</span><span class="sxs-lookup"><span data-stu-id="f2c44-115">- Make builds self-testing</span></span> |<span data-ttu-id="f2c44-116">Azure 리소스 관리자 템플릿으로 배포 된 테스트, 웹 테스트 등을 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-116">Load tests, web tests, etc., can be deployed with the Azure Resource Manager template.</span></span> |
| <span data-ttu-id="f2c44-117">- 프로덕션 환경의 클론에 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-117">- Perform tests in a clone of production environment</span></span> |<span data-ttu-id="f2c44-118">Azure 리소스 관리자 템플릿은 신속하고 예측 가능한 테스트를 위해 Azure 프로덕션 환경 (앱 설정, 연결 문자열 템플릿, 크기 조정 등 포함)의 클론을 만들 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-118">Azure Resource Manager templates can be used to create clones of the Azure production environment (including app settings, connection string templates, scaling, etc.) for testing quickly and predictably.</span></span> |
| <span data-ttu-id="f2c44-119">-최근 구축 결과를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-119">- View result of latest build easily</span></span> |<span data-ttu-id="f2c44-120">리포지토리에서 Azure로의 지속적인 배포는 변경 사항 을 커밋한 즉시 실시간 응용 프로그램에서 테스트 할 수 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-120">Continuous deployment to Azure from a repository means that you can test new code in a live application immediately after you commit your changes.</span></span> |
| <span data-ttu-id="f2c44-121">-매일 주 분기점에 커밋하기</span><span class="sxs-lookup"><span data-stu-id="f2c44-121">- Commit to the main branch every day</span></span><br><span data-ttu-id="f2c44-122">-배포를 자동화하기</span><span class="sxs-lookup"><span data-stu-id="f2c44-122">- Automate deployment</span></span> |<span data-ttu-id="f2c44-123">프로덕션 응용 프로그램과 저장소의 주 분기점의 지속적인 통합은 모든 커밋/병합은 프로덕션의 주 분기점으로 자동적으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-123">Continuous integration of a production application with a repository’s main branch automatically deploys every commit/merge to the main branch to production.</span></span> |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="f2c44-124">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="f2c44-124">What you will do</span></span>
<span data-ttu-id="f2c44-125">사용자는 Web API backend(BE), Frontend(FE)이 두 개의 [웹앱](/services/app-service/web/)과 [SQL Database](/services/sql-database/)로 구성된 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 샘플 응용 프로그램의 새로운 변경 사항을 게시하기 위해 전형적인 개발 테스트 단계 프로덕션 워크플로에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-125">You will walk through a typical dev-test-stage-production workflow in order to publish new changes to the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) sample application, which consists of two [web apps](/services/app-service/web/), one being a frontend (FE) and the other being a Web API backend (BE), and a [SQL database](/services/sql-database/).</span></span> <span data-ttu-id="f2c44-126">다음과 같은 배포 아키텍처를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-126">You will work with the following deployment architecture:</span></span>

![](./media/app-service-agile-software-development/what-1-architecture.png)

<span data-ttu-id="f2c44-127">단어에 그림을 넣으려면:</span><span class="sxs-lookup"><span data-stu-id="f2c44-127">To put the picture into words:</span></span>

* <span data-ttu-id="f2c44-128">배포 아키텍처는 3가지 환경(또는 Azure의 [리소스 그룹](../azure-resource-manager/resource-group-overview.md))으로 구분됩니다. 각각은 개별적인 [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [크기 조정](web-sites-scale.md) 설정, SQL Database가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-128">The deployment architecture is separated into three distinct environments (or [resource groups](../azure-resource-manager/resource-group-overview.md) in Azure), each with its own [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [scaling](web-sites-scale.md) settings, and SQL database.</span></span> 
* <span data-ttu-id="f2c44-129">각 환경을 별도로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-129">Each environment can be managed separately.</span></span> <span data-ttu-id="f2c44-130">서로 다른 구독에도 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-130">They can even exist in different subscriptions.</span></span>
* <span data-ttu-id="f2c44-131">스테이징과 프로덕션은 같은 앱 서비스 앱의 두 슬롯으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-131">Staging and production are implemented as two slots of the same App Service app.</span></span> <span data-ttu-id="f2c44-132">마스터 분기점은 스테이징 슬롯의 연속 통합을 위한 장치 조정입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-132">The master branch is set up for continuous integration with the staging slot.</span></span>
* <span data-ttu-id="f2c44-133">마스터 분기점으로의 커밋이 (프로덕션 데이터를 사용하여) 스테이징 슬롯에서 확인될 때 확인된 스테이징 앱은 [가동 중지 시간 없이](web-sites-staged-publishing.md)프로덕션 슬롯으로 교체됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-133">When a commit to master branch is verified on the staging slot (with production data), the verified staging app is swapped into the production slot [with no downtime](web-sites-staged-publishing.md).</span></span>

<span data-ttu-id="f2c44-134">프로덕션 및 스테이징 환경은 [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json)의 템플릿에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-134">The production and staging environment is defined by the template at [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).</span></span>

<span data-ttu-id="f2c44-135">개발 및 테스트 환경은 [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json)의 템플릿으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-135">The dev and test environments are defined by the template at [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).</span></span>

<span data-ttu-id="f2c44-136">또한 사용자는 개발 분기점에서 테스트 분기점까지, 그리고 마스터 분기점까지 코드 이동하는 일반적인 분기 전략을 사용합니다(예: 질의 향상).</span><span class="sxs-lookup"><span data-stu-id="f2c44-136">You will also use the typical branching strategy, with code moving from the dev branch up to the test branch, then to the master branch (moving up in quality, so to speak).</span></span>

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a><span data-ttu-id="f2c44-137">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="f2c44-137">What you need</span></span>
* <span data-ttu-id="f2c44-138">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f2c44-138">An Azure account</span></span>
* <span data-ttu-id="f2c44-139">[GitHub](https://github.com/) 계정</span><span class="sxs-lookup"><span data-stu-id="f2c44-139">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="f2c44-140">Git 셸(설치된 [Windows용 GitHub](https://windows.github.com/)) - 동일한 세션에서 Git와 PowerShell 명령을 실행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-140">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - enables you to run both the Git and PowerShell commands in the same session</span></span> 
* <span data-ttu-id="f2c44-141">최신 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 비트</span><span class="sxs-lookup"><span data-stu-id="f2c44-141">Latest [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits</span></span>
* <span data-ttu-id="f2c44-142">다음 도구의 기본적인 이해:</span><span class="sxs-lookup"><span data-stu-id="f2c44-142">Basic understanding of the following tools:</span></span>
  * <span data-ttu-id="f2c44-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 템플릿 배포([Azure에서 예측 가능하도록 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md) 참조)</span><span class="sxs-lookup"><span data-stu-id="f2c44-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (also see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="f2c44-144">Git</span><span class="sxs-lookup"><span data-stu-id="f2c44-144">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="f2c44-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2c44-145">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="f2c44-146">이 자습서를 완료하려면 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-146">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="f2c44-147">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/) 할 수 있음 - 유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 되며 크레딧을 모두 사용한 후에도 계정을 유지하고 웹앱과 같은 무료 Azure 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-147">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="f2c44-148">[Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-148">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> <span data-ttu-id="f2c44-149">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-149">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f2c44-150">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-150">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="set-up-your-production-environment"></a><span data-ttu-id="f2c44-151">프로덕션 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-151">Set up your production environment</span></span>
> [!NOTE]
> <span data-ttu-id="f2c44-152">이 자습서에서 사용되는 스크립트는 GitHub 리포지토리에서 지속적으로 게시되도록 자동적으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-152">The script used in this tutorial automatically configures continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="f2c44-153">Azure에 이미 저장되어 있는 GitHub 자격 증명이 필요하고 그렇지 않으면 웹앱에 소스 제어 설정을 구성하도록 시도할 때 스크립트된 배포에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-153">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment fails when attempting to configure source control settings for the web apps.</span></span> 
> 
> <span data-ttu-id="f2c44-154">Azure에서 GitHub 자격 증명을 저장하려면 [Azure Portal](https://portal.azure.com/)에서 웹앱을 생성하고 [GitHub 배포를 구성](app-service-continuous-deployment.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-154">To store your GitHub credentials in Azure, create a web app in the [Azure portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f2c44-155">이 작업은 한 번만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-155">You only need to do this once.</span></span> 
> 
> 

<span data-ttu-id="f2c44-156">일반적인 DevOps 시나리오에서, 사용자는  Azure에서 실시간으로 실행되는 응용 프로그램을 갖게 되며, 지속적인 게시를 통해 원하는 부분을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-156">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="f2c44-157">이 시나리오에서는 개발, 테스트 및 프로덕션 환경에 배포하는 데 사용하는 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-157">In this scenario, you have a template that you developed, tested, and used to deploy the production environment.</span></span> <span data-ttu-id="f2c44-158">이 섹션에서는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-158">You will set it up in this section.</span></span>

1. <span data-ttu-id="f2c44-159">[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 저장소에서 사용자 고유 포크를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-159">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="f2c44-160">분기를 만드는 방법에 대한 자세한 내용은 [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-160">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="f2c44-161">사용자의 포크를 생성하면, 브라우저에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-161">Once your fork is created, you can see it in your browser.</span></span>
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="f2c44-162">Git 셸 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-162">Open a Git Shell session.</span></span> <span data-ttu-id="f2c44-163">Git 셸이 없는 경우 [Windows용 GitHub](https://windows.github.com/) 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-163">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="f2c44-164">다음 명령을 실행하여 사용자 포크의 로컬 클론을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-164">Create a local clone of your fork by executing the following command:</span></span>

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. <span data-ttu-id="f2c44-165">로컬 클론을 만든 후 *&lt;repository_root>*\ARMTemplates으로 이동하여 다음과 같이 deploy.ps1 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-165">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script as follows:</span></span>
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. <span data-ttu-id="f2c44-166">메시지가 표시되면 데이터베이스 액세스에 대한 원하는 사용자이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-166">When prompted, type in the desired username and password for database access.</span></span>
   
   <span data-ttu-id="f2c44-167">다양한 Azure 리소스의 프로비전 진행 상태가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-167">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="f2c44-168">배포가 완료되면, 스크립트가 브라우저에서 응용 프로그램을 시작되고, 친숙한 소리가 납니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-168">When deployment completes, the script launches the application in the browser and give you a friendly beep.</span></span>
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > <span data-ttu-id="f2c44-169">고유 ID를 사용한 리소스 제공 방법을 알아보려면 *&lt;repository_root>*\ARMTemplates\Deploy.ps1을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-169">Take a look at *&lt;repository_root>*\ARMTemplates\Deploy.ps1, to see how it generates resources with unique IDs.</span></span> <span data-ttu-id="f2c44-170">충돌하는 리소스 이름에 대해 걱정하지 않고 동일한 배포의 클론을 만들려면 동일한 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-170">You can use the same approach to create clones of the same deployment without worrying about conflicting resource names.</span></span>
   > 
   > 
6. <span data-ttu-id="f2c44-171">Git 셸 세션으로 돌아가서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-171">Back in your Git Shell session, run:</span></span>
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. <span data-ttu-id="f2c44-172">스크립트가 완료되면 프런트 엔드의 주소(http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/)로 돌아가서 프로덕션에서 응용 프로그램이 실행되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-172">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="f2c44-173">[Azure Portal](https://portal.azure.com/)에 로그인하고 생성된 항목을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-173">Log in to the [Azure portal](https://portal.azure.com/) and take a look at what’s created.</span></span>
   
   <span data-ttu-id="f2c44-174">같은 리소스 그룹에서 두 개의 웹앱이 나타나야 하며, 하나는 이름에 `Api` 접미사가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-174">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="f2c44-175">리소스 그룹 보기를 보면 SQL Database 및 서버, App Service 계획 및 웹앱에 대한 스테이징 슬롯도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-175">If you look at the resource group view, you also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="f2c44-176">*&lt;repository_root>*\ARMTemplates\ProdAndStage.json을 사용하여 다른 리소스를 통해 검색 및 비교하여 템플릿에서 어떻게 구성되는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-176">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

<span data-ttu-id="f2c44-177">이제 프로덕션 환경을 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-177">You have now set up the production environment.</span></span> <span data-ttu-id="f2c44-178">다음으로, 응용 프로그램에 대한 새 업데이트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-178">Next, you will kick off a new update to the application.</span></span>

## <a name="create-dev-and-test-branches"></a><span data-ttu-id="f2c44-179">Dev를 생성하고 분기점을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-179">Create dev and test branches</span></span>
<span data-ttu-id="f2c44-180">이제 Azure의 프로덕션 내에서 실행되는 복합 응용 프로그램을 갖게 되었으므로,  agile방법론에 따라 사용자의 응용 프로그램의 업데이트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-180">Now that you have a complex application running in production in Azure, you will make an update to your application in accordance with agile methodology.</span></span> <span data-ttu-id="f2c44-181">이 섹션에서는 업데이트 요구 사항을 만드는 데 필요한 분기점을 테스트하고 dev를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-181">In this section, you will create the dev and test branches that you will need to make the required updates.</span></span>

1. <span data-ttu-id="f2c44-182">먼저 테스트 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-182">Create the test environment first.</span></span> <span data-ttu-id="f2c44-183">Git 셸 세션에서 다음 명령을 실행하여 **NewUpdate**라는 새로운 분기에 대한 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-183">In your Git Shell session, run the following commands to create the environment for a new branch called **NewUpdate**.</span></span> 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. <span data-ttu-id="f2c44-184">메시지가 표시되면 데이터베이스 액세스에 대한 원하는 사용자이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-184">When prompted, type in the desired username and password for database access.</span></span> 
   
   <span data-ttu-id="f2c44-185">배포가 완료되면, 스크립트가 브라우저에서 응용 프로그램을 시작되고, 친숙한 소리가 납니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-185">When deployment completes, the script launches the application in the browser and give you a friendly beep.</span></span> <span data-ttu-id="f2c44-186">이제 자체 테스트 환경이 포함된 새로운 분기점이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-186">You now have a new branch with its own test environment.</span></span> <span data-ttu-id="f2c44-187">잠시 테스트환경에 관한 몇 가지 사항을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-187">Take a moment to review a few things about this test environment:</span></span>
   
   * <span data-ttu-id="f2c44-188">모든 Azure 구독에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-188">You can create it in any Azure subscription.</span></span> <span data-ttu-id="f2c44-189">즉, 테스트 환경에서 프로덕션 환경을 별도로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-189">That means the production environment can be managed separately from your test environment.</span></span>
   * <span data-ttu-id="f2c44-190">테스트 환경을 라이브 Azure에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-190">Your test environment is running live in Azure.</span></span>
   * <span data-ttu-id="f2c44-191">테스트 환경은 스테이징 슬롯 및 크기 조정 설정을 제외하고 프로덕션 환경과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-191">Your test environment is identical to the production environment, except for the staging slots and the scaling settings.</span></span> <span data-ttu-id="f2c44-192">ProdandStage.json과 Dev.json 간의 유일한 차이점이므로 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-192">You know it because they are the only differences between ProdandStage.json and Dev.json.</span></span>
   * <span data-ttu-id="f2c44-193">다른 가격 계층(예: **무료**)으로 자체 앱 서비스 계획에서 테스트 환경을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-193">You can manage your test environment in its own App Service plan, with a different price tier (such as **Free**).</span></span>
   * <span data-ttu-id="f2c44-194">테스트 환경을 삭제하는 것은 리소스 그룹을 삭제하는 것 만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-194">Deleting this test environment is as simple as deleting the resource group.</span></span> <span data-ttu-id="f2c44-195">이 작업을 수행하는 방법은 [나중에](#delete)살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-195">You will find out how to do this [later](#delete).</span></span>
3. <span data-ttu-id="f2c44-196">다음 명령을 실행하여 개발 분기점 생성으로 넘어갑니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-196">Go on to create a dev branch by running the following commands:</span></span>
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. <span data-ttu-id="f2c44-197">메시지가 표시되면 데이터베이스 액세스에 대한 원하는 사용자이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-197">When prompted, type in the desired username and password for database access.</span></span> 
   
   <span data-ttu-id="f2c44-198">잠시 개발 환경에 관한 몇가지 사항을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-198">Take a moment to review a few things about this dev environment:</span></span> 
   
   * <span data-ttu-id="f2c44-199">개발 환경은 테스트 환경과 같은 템플릿을 사용하여 배포되었으므로 구성이 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-199">Your dev environment has a configuration identical to the test environment because it’s deployed using the same template.</span></span>
   * <span data-ttu-id="f2c44-200">각 개발 환경은 개발자의 Azure 구독에서 생성 가능하며, 별도로 관리하는 테스트 환경을 남겨둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-200">Each dev environment can be created in the developer’s own Azure subscription, leaving the test environment to be separately managed.</span></span>
   * <span data-ttu-id="f2c44-201">개발 환경이 Azure에서 실시간 작동 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-201">Your dev environment is running live in Azure.</span></span>
   * <span data-ttu-id="f2c44-202">개발 환경을 삭제하는 것은 리소스 그룹을 삭제하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-202">Deleting the dev environment is as simple as deleting the resource group.</span></span> <span data-ttu-id="f2c44-203">이 작업을 수행하는 방법은 [나중에](#delete)살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-203">You will find out how to do this [later](#delete).</span></span>

> [!NOTE]
> <span data-ttu-id="f2c44-204">여러 개발자가 새로운 업데이트를 개발할 때, 각각의 개발자들은 다음 단계에서 쉽게 분기 및 전용 개발 환경을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-204">When you have multiple developers working on the new update, each of them can easily create a branch and dedicated dev environment with the following steps:</span></span>
> 
> 1. <span data-ttu-id="f2c44-205">GitHub에서 리포지토리의 고유한 분기를 만듭니다( [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)참조).</span><span class="sxs-lookup"><span data-stu-id="f2c44-205">Create their own fork of the repository in GitHub (see [Fork a Repo](https://help.github.com/articles/fork-a-repo/)).</span></span>
> 2. <span data-ttu-id="f2c44-206">자신의 로컬 컴퓨터에서 포크를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-206">Clone the fork on their local machine</span></span>
> 3. <span data-ttu-id="f2c44-207">자신의 개발 포크 및 환경을 만들려면 동일한 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-207">Run the same commands to create their own dev branch and environment.</span></span>
> 
> 

<span data-ttu-id="f2c44-208">완료되면, GitHub 포크는 세 개의 분기가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-208">When you’re done, your GitHub fork should have three branches:</span></span>

![](./media/app-service-agile-software-development/test-1-github-view.png)

<span data-ttu-id="f2c44-209">3 개의 별도 리소스 그룹에서 6개의 웹앱(한 그룹에 2개의 응용 프로그램)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-209">And you should have six web apps (three sets of two) in three separate resource groups:</span></span>

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> <span data-ttu-id="f2c44-210">ProdandStage.json은 프로덕션 응용 프로그램의 확장성에 적합한 **표준** 가격 책정 계층을 사용하기 위한 프로덕션 환경을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-210">ProdandStage.json specifies the production environment to use the **Standard** pricing tier, which is appropriate for scalability of the production application.</span></span>
> 
> 

## <a name="build-and-test-every-commit"></a><span data-ttu-id="f2c44-211">모든 커밋을 구축하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-211">Build and test every commit</span></span>
<span data-ttu-id="f2c44-212">ProdAndStage.json 및 Dev.json 템플릿 파일은 웹앱에 대한 연속 게시 설정 기본값인 소스 제어 매개 변수를 이미 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-212">The template files ProdAndStage.json and Dev.json already specify the source control parameters, which by default sets up continuous publishing for the web app.</span></span> <span data-ttu-id="f2c44-213">따라서, GitHub분기의 모든 커밋은 해당 분기에서 Azure로 자동 배포를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-213">Therefore, every commit to the GitHub branch triggers an automatic deployment to Azure from that branch.</span></span> <span data-ttu-id="f2c44-214">이제 설치 작업을 하는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-214">Let’s see how your setup works now.</span></span>

1. <span data-ttu-id="f2c44-215">사용자가 로컬 저장소의 개발 분기에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-215">Make sure that you’re in the Dev branch of the local repository.</span></span> <span data-ttu-id="f2c44-216">이렇게 하려면 Git 셸에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-216">To do this, run the following command in Git Shell:</span></span>
   
        git checkout Dev
2. <span data-ttu-id="f2c44-217">[부트스트랩](http://getbootstrap.com/components/) 목록을 사용하도록 코드를 변경하여 앱의 UI 계층을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-217">Make a change to the app’s UI layer by changing the code to use [Bootstrap](http://getbootstrap.com/components/) lists.</span></span> <span data-ttu-id="f2c44-218">*&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml을 열고 다음과 같이 강조 표시된 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-218">Open *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml and make the following highlighted change:</span></span>
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > <span data-ttu-id="f2c44-219">이전 이미지가 나타나지 않으면:</span><span class="sxs-lookup"><span data-stu-id="f2c44-219">If you can't read the preceding image:</span></span> 
    > 
    > * <span data-ttu-id="f2c44-220">18번 줄에서 `check-list`를 `list-group`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-220">In line 18, change `check-list` to `list-group`.</span></span>
    > * <span data-ttu-id="f2c44-221">19 번 줄에서 `class="check-list-item"`을 `class="list-group-item"`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-221">In line 19, change `class="check-list-item"` to `class="list-group-item"`.</span></span>
    > 
    > 
3. <span data-ttu-id="f2c44-222">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-222">Save the change.</span></span> <span data-ttu-id="f2c44-223">Git 셸로 돌아가서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-223">Back in Git Shell, run the following commands:</span></span>
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   <span data-ttu-id="f2c44-224">이러한 git 명령은 TFS와 같은 다른 소스 제어 시스템의 ‘사용자 코드에서 확인”과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-224">These git commands are similar to "checking in your code" in another source control system like TFS.</span></span> <span data-ttu-id="f2c44-225">`git push`를 실행하는 경우 새로운 커밋은 Azure로 자동 코드 푸시를 트리거한 다음 개발 환경의 변경 사항을 반영하기 위해 해당 응용 프로그램을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-225">When you run `git push`, the new commit triggers an automatic code push to Azure, which then rebuilds the application to reflect the change in the dev environment.</span></span>
4. <span data-ttu-id="f2c44-226">개발 환경에서 코드 푸시가 나타나는지 확인하려면 개발 환경의 웹앱 페이지에서 **배포** 부분을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-226">To verify that this code push to your dev environment has occurred, go to your dev environment’s web app page and look at the **Deployment** part.</span></span> <span data-ttu-id="f2c44-227">그곳에서 최신 커밋 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-227">You should be able to see your latest commit message there.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. <span data-ttu-id="f2c44-228">여기서 **찾아보기** 를 클릭하여 Azure의 라이브 응용 프로그램의 새로운 변경 사항을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-228">From there, click **Browse** to see the new change in the live application in Azure.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   <span data-ttu-id="f2c44-229">응용 프로그램의 사소한 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-229">It's a minor change to the application.</span></span> <span data-ttu-id="f2c44-230">그러나, 복잡한 웹 응용 프로그램의 많은 새로운 변경 사항들은 의도하지 않고 원하지 않는 부작용을 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-230">However, many times new changes to a complex web application have unintended and undesirable side effects.</span></span> <span data-ttu-id="f2c44-231">라이브 빌드에서 모든 커밋을 쉽게 테스트 하여 이러한 문제들을 고객이 먼저 발견하기 전에 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-231">Being able to easily test every commit in live builds enables you to catch these issues before your customers see them.</span></span>

<span data-ttu-id="f2c44-232">이제 **NewUpdate** 프로젝트의 개발자로서 개발 환경을 만든 후 모든 커밋을 빌드하고 모든 빌드를 테스트할 수 있다는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-232">By now, you should be comfortable with the realization that, as a developer on the **NewUpdate** project, you can create a dev environment for yourself, then build every commit and test every build.</span></span>

## <a name="merge-code-into-test-environment"></a><span data-ttu-id="f2c44-233">테스트 환경에 코드를 병합</span><span class="sxs-lookup"><span data-stu-id="f2c44-233">Merge code into test environment</span></span>
<span data-ttu-id="f2c44-234">개발 환경 분기에서 새 업데이트 분기까지 코드 푸시가 준비된 경우는 표준 git 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-234">When you’re ready to push your code from Dev branch up to NewUpdate branch, it’s the standard git process:</span></span>

1. <span data-ttu-id="f2c44-235">새 업데이트의 모든 커밋을 GitHub의 개발 분기에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-235">Merge any new commits to NewUpdate into the Dev branch in GitHub, such as commits created by other developers.</span></span> <span data-ttu-id="f2c44-236">(예: 다른 개발자가 만든 커밋) GitHub의 모든 커밋을 개발 환경 안에서 코드 푸시하고 구축하는 데 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-236">Any new commit on GitHub triggers a code push and build in the dev environment.</span></span> <span data-ttu-id="f2c44-237">그리고 나서, 사용자는 개발분기의 코드가 새 업데이트 분기의 최신 비트와 여전히 작동 되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-237">You can then make sure your code in Dev branch still works with the latest bits from NewUpdate branch.</span></span>
2. <span data-ttu-id="f2c44-238">개발 분기의 모든 새 커밋을 GitHub의 새 업데이트 브랜치로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-238">Merge all your new commits from Dev branch into NewUpdate branch on GitHub.</span></span> <span data-ttu-id="f2c44-239">이 작업은 테스트 환경의 코드 푸시와 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-239">This action triggers a code push and build in the test environment.</span></span> 

<span data-ttu-id="f2c44-240">지속적인 배포를 이미 git 분기와 같이 설치했기 때문에 사용자는 통합 빌드 실행과 같은 다른 어떤 작업도 할 필요가 없다는 것을 다시 한번 명심하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-240">Note again that because continuous deployment is already set up with these git branches, you don’t need to take any other action like running integration builds.</span></span> <span data-ttu-id="f2c44-241">사용자는 단순히 git를 사용하여 표준 소스 제어 사례를 수행하고, Azure는 사용자를 위해 모든 구축 프로세스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-241">You simply need to perform standard source control practices using git, and Azure performs all the build processes for you.</span></span>

<span data-ttu-id="f2c44-242">이제 **NewUpdate** 분기에 사용자의 코드를 푸시해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-242">Now, let’s push your code to **NewUpdate** branch.</span></span> <span data-ttu-id="f2c44-243">Git 셸에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-243">In Git Shell, run the following commands:</span></span>

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

<span data-ttu-id="f2c44-244">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-244">That’s it!</span></span> 

<span data-ttu-id="f2c44-245">이제 테스트 환경에 푸시된 새 커밋(NewUpdate 분기에 병합)을 보려면 테스트 환경에 대한 웹앱 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-245">Go to the web app page for your test environment to see your new commit (merged into NewUpdate branch) now pushed to the test environment.</span></span> <span data-ttu-id="f2c44-246">**찾아보기** 를 클릭하여 스타일 변경을 볼 수 있으면 Azure에서 실시간으로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-246">Then, click **Browse** to see that the style change is now running live in Azure.</span></span>

## <a name="deploy-update-to-production"></a><span data-ttu-id="f2c44-247">프로덕션에 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="f2c44-247">Deploy update to production</span></span>
<span data-ttu-id="f2c44-248">코드를 스테이징 및 프로덕션 환경에 푸시하는 것은 이미 작업했던 테스트환경에 코드를 푸시하는 것과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-248">Pushing code to the staging and production environment should feel no different than what you’ve already done when you pushed code to the test environment.</span></span> <span data-ttu-id="f2c44-249">매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-249">It's really that simple.</span></span> 

<span data-ttu-id="f2c44-250">Git 셸에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-250">In Git Shell, run the following commands:</span></span>

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

<span data-ttu-id="f2c44-251">ProdandStage.json에서 스테이징 및 프로덕션 환경이 설정된 방식에 따라 새 코드가 **스테이징** 슬롯으로 푸시되고 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-251">Remember that based on the way the staging and production environment is set up in ProdandStage.json, your new code is pushed to the **Staging** slot and is running there.</span></span> <span data-ttu-id="f2c44-252">스테이징 슬롯의 URL로 이동하면 여기서 실행 되는 새 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-252">So if you navigate to the staging slot’s URL, you see the new code running there.</span></span> <span data-ttu-id="f2c44-253">이렇게 하려면 Git 셸에서 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-253">To do this, run the following cmdlet in Git Shell.</span></span>

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

<span data-ttu-id="f2c44-254">스테이징 슬롯에서 업데이트를 확인 후, 남은 것은 이것을 프로덕션으로 교체하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-254">And now, after you’ve verified the update in the staging slot, the only thing left to do is to swap it into production.</span></span> <span data-ttu-id="f2c44-255">Git 셸에서 바로 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-255">In Git Shell, just run the following commands:</span></span>

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

<span data-ttu-id="f2c44-256">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-256">Congratulations!</span></span> <span data-ttu-id="f2c44-257">프로덕션 웹 응용 프로그램에 새 업데이트를 성공적으로 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-257">You’ve successfully published a new update to your production web application.</span></span> <span data-ttu-id="f2c44-258">게다가 쉽게 개발과 테스트 환경을 생성하고, 모든 커밋을 구축하고 테스트함으로써 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-258">What’s more is that did it by easily creating dev and test environments, and building and testing every commit.</span></span> <span data-ttu-id="f2c44-259">이들은 agile 소프트웨어 개발의 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-259">These are crucial building blocks for agile software development.</span></span>

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a><span data-ttu-id="f2c44-260">개발 환경과 테스트 환경 삭제</span><span class="sxs-lookup"><span data-stu-id="f2c44-260">Delete dev and test environments</span></span>
<span data-ttu-id="f2c44-261">사용자가 의도적으로 자체 포함된 리소스 그룹으로 개발 환경과 테스트 환경을 설계했기 때문에 삭제하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-261">Because you have purposely architected your dev and test environments to be self-contained resource groups, it is easy to delete them.</span></span> <span data-ttu-id="f2c44-262">이 자습서에서 만든 GitHub 분기와 Azure 결과물 둘 중에 하나를 지우려먼, Git 셸에서 다음 명령을 실행하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-262">To delete the ones you created in this tutorial, both the GitHub branches and Azure artifacts, just run the following commands in Git Shell:</span></span>

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a><span data-ttu-id="f2c44-263">요약</span><span class="sxs-lookup"><span data-stu-id="f2c44-263">Summary</span></span>
<span data-ttu-id="f2c44-264">Agile 소프트웨어 개발은 Azure를 응용 프로그램 플랫폼으로 채택하려는 대부분의 회사에게 필수품입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-264">Agile software development is a must-have for many companies who want to adopt Azure as their application platform.</span></span> <span data-ttu-id="f2c44-265">이 자습서에서는, 프로덕션 환경, 심지어 복잡한 응용 프로그램의 정확하거나 비슷한 복제본을 쉽게 만들고 분리하는 방법에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-265">In this tutorial, you have learned how to create and tear down exact replicas or near replicas of the production environment with ease, even for complex applications.</span></span> <span data-ttu-id="f2c44-266">또한, Azure에서 모든 단일 커밋을 구축하고 테스트하는 개발 프로세스를 생성하는 기능을 활용하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-266">You have also learned how to leverage this ability to create a development process that can build and test every single commit in Azure.</span></span> <span data-ttu-id="f2c44-267">이 자습서는 사용자가 Azure 앱 서비스와 Azure 리소스 관리자를 함께 사용하여 agile 방법론에 부합하는 DevOps 솔루션을 제공하는 최상의 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-267">This tutorial has hopefully shown you how you can best use Azure App Service and Azure Resource Manager together to create a DevOps solution that caters to agile methodologies.</span></span> <span data-ttu-id="f2c44-268">다음으로 [프로덕션에서 테스트](app-service-web-test-in-production-get-start.md)와 고급 DevOps 기술을 수행하여 시나리오를 계속 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c44-268">Next, you can build on this scenario by performing advanced DevOps techniques such as [testing in production](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="f2c44-269">일반적인 프로덕션 시나리오 테스트의 경우 [Azure 앱 서비스에서 Flighting 배포(베타 테스트)](app-service-web-test-in-production-controlled-test-flight.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2c44-269">For a common testing-in-production scenario, see [Flighting deployment (beta testing) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).</span></span>

## <a name="more-resources"></a><span data-ttu-id="f2c44-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f2c44-270">More resources</span></span>
* [<span data-ttu-id="f2c44-271">Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포</span><span class="sxs-lookup"><span data-stu-id="f2c44-271">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="f2c44-272">Agile 개발 연습에서: 현대화 개발 주기의 팁과 트릭</span><span class="sxs-lookup"><span data-stu-id="f2c44-272">Agile Development in Practice: Tips and Tricks for Modernized Development Cycle</span></span>](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [<span data-ttu-id="f2c44-273">리소스 관리자 템플릿을 사용하여 Azure 웹앱의 고급 배포 전략</span><span class="sxs-lookup"><span data-stu-id="f2c44-273">Advanced deployment strategies for Azure Web Apps using Resource Manager templates</span></span>](http://channel9.msdn.com/Events/Build/2015/2-620)
* [<span data-ttu-id="f2c44-274">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="f2c44-274">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="f2c44-275">JSONLint-JSON 유효성 검사기</span><span class="sxs-lookup"><span data-stu-id="f2c44-275">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="f2c44-276">ARMClient – 사이트로 GitHub 게시를 설정</span><span class="sxs-lookup"><span data-stu-id="f2c44-276">ARMClient – Set up GitHub publishing to site</span></span>](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [<span data-ttu-id="f2c44-277">Git 분기-기본 분기 및 병합</span><span class="sxs-lookup"><span data-stu-id="f2c44-277">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="f2c44-278">David Ebbo의 블로그</span><span class="sxs-lookup"><span data-stu-id="f2c44-278">David Ebbo’s Blog</span></span>](http://blog.davidebbo.com/)
* [<span data-ttu-id="f2c44-279">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2c44-279">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="f2c44-280">Azure 플랫폼간 명령줄 도구</span><span class="sxs-lookup"><span data-stu-id="f2c44-280">Azure Cross-Platform Command-Line Tools</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="f2c44-281">Azure AD에서 사용자 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="f2c44-281">Create or edit users in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [<span data-ttu-id="f2c44-282">프로젝트 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="f2c44-282">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)

