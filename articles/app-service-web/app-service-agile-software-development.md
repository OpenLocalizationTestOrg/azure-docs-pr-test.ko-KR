---
title: "Azure 앱 서비스와 aaaAgile 소프트웨어 개발"
description: "자세한 내용은 방법 toocreate 확장성이 뛰어난 복잡 한 응용 프로그램 Azure 앱 서비스와 agile 소프트웨어 개발을 지 원하는 방식으로 합니다."
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
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a><span data-ttu-id="2e7da-103">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="2e7da-103">Agile software development with Azure App Service</span></span>
<span data-ttu-id="2e7da-104">이 자습서에서는 살펴보겠습니다 방법을 toocreate 확장성이 뛰어난 복잡 한 응용 프로그램을 [Azure 앱 서비스](/azure/app-service/) 지 원하는 방식으로 [agile 소프트웨어 개발](https://en.wikipedia.org/wiki/Agile_software_development)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-104">In this tutorial, you will learn how toocreate high-scale complex applications with [Azure App Service](/azure/app-service/) in a way that supports [agile software development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="2e7da-105">이미 알고 있다고 너무 어떻게 가정[Azure에 예측 가능한 방식으로 복잡 한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-105">It assumes that you already know how too[deploy complex applications predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="2e7da-106">Agile 방법론의 성공적인 구현의 hello 방식에서 기술 프로세스의 제한 사항을 위반 독립 종종 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-106">Limitations in technical processes can often stand in hello way of successful implementation of agile methodologies.</span></span> <span data-ttu-id="2e7da-107">Azure 앱 서비스와 같은 기능과 함께 [지속적인 게시](app-service-continuous-deployment.md), [스테이징 환경의](web-sites-staged-publishing.md) (슬롯) 및 [모니터링](web-sites-monitor.md)hello 오케스트레이션과 현명 하 게 결합 하는 경우 및 배포의 관리 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md), agile 소프트웨어 개발 수용 개발자를 위한 가장 좋은 방법의 일부일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-107">Azure App Service with features such as [continuous publishing](app-service-continuous-deployment.md), [staging environments](web-sites-staged-publishing.md) (slots), and [monitoring](web-sites-monitor.md), when coupled wisely with hello orchestration and management of deployment in [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), can be part of a great solution for developers who embrace agile software development.</span></span>

<span data-ttu-id="2e7da-108">hello 다음 표는 민첩 한 개발와 관련 된 요구 사항의 짧은 목록을 방법과 Azure 서비스를 사용 하 고 각 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-108">hello following table is a short list of requirements associated with agile development, and how Azure services enable each of them.</span></span>

| <span data-ttu-id="2e7da-109">요구 사항</span><span class="sxs-lookup"><span data-stu-id="2e7da-109">Requirement</span></span> | <span data-ttu-id="2e7da-110">Azure 사용할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="2e7da-110">How Azure enables</span></span> |
| --- | --- |
| <span data-ttu-id="2e7da-111">-모든 커밋을 사용하여 구축</span><span class="sxs-lookup"><span data-stu-id="2e7da-111">- Build with every commit</span></span><br><span data-ttu-id="2e7da-112">- 빠르게 자동적으로 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-112">- Build automatically and fast</span></span> |<span data-ttu-id="2e7da-113">지속적인 배포를 구성할 때, Azure 앱 서비스는 개발 분기점에 따라 실시간 구축 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-113">When configured with continuous deployment, Azure App Service can function as live-running builds based on a dev branch.</span></span> <span data-ttu-id="2e7da-114">코드 toohello 분기 푸시됩니다, 될 때마다 자동으로 빌드된 한는 실시간 Azure 에서입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-114">Every time code is pushed toohello branch, it is automatically built and running live in Azure.</span></span> |
| <span data-ttu-id="2e7da-115">- 자체-테스트 빌드 구축하기</span><span class="sxs-lookup"><span data-stu-id="2e7da-115">- Make builds self-testing</span></span> |<span data-ttu-id="2e7da-116">테스트, 웹 테스트 등 로드할 하시기 바랍니다 hello Azure 리소스 관리자 템플릿을 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-116">Load tests, web tests, etc., can be deployed with hello Azure Resource Manager template.</span></span> |
| <span data-ttu-id="2e7da-117">- 프로덕션 환경의 클론에 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-117">- Perform tests in a clone of production environment</span></span> |<span data-ttu-id="2e7da-118">Azure 리소스 관리자 템플릿 hello Azure 프로덕션 환경 (응용 프로그램 설정, 연결 문자열 템플릿, 배율, 등 포함) 신속 하 고 예측 가능한 방식으로 테스트를 위해 사용 되는 toocreate 복제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-118">Azure Resource Manager templates can be used toocreate clones of hello Azure production environment (including app settings, connection string templates, scaling, etc.) for testing quickly and predictably.</span></span> |
| <span data-ttu-id="2e7da-119">-최근 구축 결과를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-119">- View result of latest build easily</span></span> |<span data-ttu-id="2e7da-120">리포지토리에서 지속적인 배포 tooAzure 변경 내용을 커밋한 후에 즉시 라이브 응용 프로그램에서 새 코드를 테스트할 수를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-120">Continuous deployment tooAzure from a repository means that you can test new code in a live application immediately after you commit your changes.</span></span> |
| <span data-ttu-id="2e7da-121">-커밋 주 분기 toohello 매일</span><span class="sxs-lookup"><span data-stu-id="2e7da-121">- Commit toohello main branch every day</span></span><br><span data-ttu-id="2e7da-122">-배포를 자동화하기</span><span class="sxs-lookup"><span data-stu-id="2e7da-122">- Automate deployment</span></span> |<span data-ttu-id="2e7da-123">연속 통합 저장소의 main 분기와 프로덕션 응용 프로그램의 모든 커밋/병합 toohello main 분기 tooproduction를 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-123">Continuous integration of a production application with a repository’s main branch automatically deploys every commit/merge toohello main branch tooproduction.</span></span> |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="2e7da-124">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="2e7da-124">What you will do</span></span>
<span data-ttu-id="2e7da-125">순서 toopublish 새 변경 내용 toohello에서 일반적인 작업 테스트 단계 프로덕션 개발 과정을 안내 합니다 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 두 구성 되는 샘플 응용 프로그램 [웹 앱](/services/app-service/web/), 하나의 프론트 엔드 (FE) 및 웹 API 백 엔드 (BE) 되 고 다른 hello 및 [SQL 데이터베이스](/services/sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-125">You will walk through a typical dev-test-stage-production workflow in order toopublish new changes toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) sample application, which consists of two [web apps](/services/app-service/web/), one being a frontend (FE) and hello other being a Web API backend (BE), and a [SQL database](/services/sql-database/).</span></span> <span data-ttu-id="2e7da-126">배포 아키텍처를 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-126">You will work with hello following deployment architecture:</span></span>

![](./media/app-service-agile-software-development/what-1-architecture.png)

<span data-ttu-id="2e7da-127">단어로 tooput hello 그림:</span><span class="sxs-lookup"><span data-stu-id="2e7da-127">tooput hello picture into words:</span></span>

* <span data-ttu-id="2e7da-128">hello 배포 아키텍처는 세 가지 서로 다른 환경으로 구분 됩니다 (또는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md) Azure에서)를 각각 고유의 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [배율](web-sites-scale.md) 설정 및 SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-128">hello deployment architecture is separated into three distinct environments (or [resource groups](../azure-resource-manager/resource-group-overview.md) in Azure), each with its own [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [scaling](web-sites-scale.md) settings, and SQL database.</span></span> 
* <span data-ttu-id="2e7da-129">각 환경을 별도로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-129">Each environment can be managed separately.</span></span> <span data-ttu-id="2e7da-130">서로 다른 구독에도 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-130">They can even exist in different subscriptions.</span></span>
* <span data-ttu-id="2e7da-131">스테이징 및 프로덕션 hello의 두 슬롯으로 구현 됩니다 동일한 앱 서비스 앱.</span><span class="sxs-lookup"><span data-stu-id="2e7da-131">Staging and production are implemented as two slots of hello same App Service app.</span></span> <span data-ttu-id="2e7da-132">hello 마스터 분기 슬롯 hello로 연속 통합에 대 한 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-132">hello master branch is set up for continuous integration with hello staging slot.</span></span>
* <span data-ttu-id="2e7da-133">커밋 toomaster 분기 hello 슬롯 (프로덕션 데이터를 사용)에서 확인 되며, 준비 응용 프로그램은 hello 프로덕션 슬롯으로 교환 된 hello 확인 [중단 시간 없이](web-sites-staged-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-133">When a commit toomaster branch is verified on hello staging slot (with production data), hello verified staging app is swapped into hello production slot [with no downtime](web-sites-staged-publishing.md).</span></span>

<span data-ttu-id="2e7da-134">hello 프로덕션 및 스테이징 환경 템플릿에 의해 정의 됩니다 hello에 [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-134">hello production and staging environment is defined by hello template at [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).</span></span>

<span data-ttu-id="2e7da-135">hello 개발 및 테스트 환경에서 hello 템플릿에서 정의 [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-135">hello dev and test environments are defined by hello template at [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).</span></span>

<span data-ttu-id="2e7da-136">또한 toohello 테스트 분기를 dev 분기 hello toohello 마스터 분기 (따라서 toospeak 품질에서 이동)에서 이동 하는 코드와 함께 hello 일반적인 분기 전략을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-136">You will also use hello typical branching strategy, with code moving from hello dev branch up toohello test branch, then toohello master branch (moving up in quality, so toospeak).</span></span>

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a><span data-ttu-id="2e7da-137">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="2e7da-137">What you need</span></span>
* <span data-ttu-id="2e7da-138">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="2e7da-138">An Azure account</span></span>
* <span data-ttu-id="2e7da-139">[GitHub](https://github.com/) 계정</span><span class="sxs-lookup"><span data-stu-id="2e7da-139">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="2e7da-140">Git 셸 (설치 된 [Windows 용 GitHub](https://windows.github.com/))-동일한 hello에 사용 하도록 설정 하면 toorun 둘 다 hello Git 및 PowerShell 명령을 세션</span><span class="sxs-lookup"><span data-stu-id="2e7da-140">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - enables you toorun both hello Git and PowerShell commands in hello same session</span></span> 
* <span data-ttu-id="2e7da-141">최신 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 비트</span><span class="sxs-lookup"><span data-stu-id="2e7da-141">Latest [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) bits</span></span>
* <span data-ttu-id="2e7da-142">기본적으로 도구 다음 hello 이해:</span><span class="sxs-lookup"><span data-stu-id="2e7da-142">Basic understanding of hello following tools:</span></span>
  * <span data-ttu-id="2e7da-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 템플릿 배포([Azure에서 예측 가능하도록 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md) 참조)</span><span class="sxs-lookup"><span data-stu-id="2e7da-143">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (also see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="2e7da-144">Git</span><span class="sxs-lookup"><span data-stu-id="2e7da-144">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="2e7da-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e7da-145">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="2e7da-146">이 자습서는 Azure 계정 toocomplete 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-146">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="2e7da-147">할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/) -크레딧을 얻게 Azure 서비스를 유료 아웃 tootry 사용할 수 있으며 모두 사용 하는 후에 hello 계정 등에 사용 가능한 웹 응용 프로그램 등의 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-147">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="2e7da-148">[Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-148">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> <span data-ttu-id="2e7da-149">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-149">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2e7da-150">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-150">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="set-up-your-production-environment"></a><span data-ttu-id="2e7da-151">프로덕션 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-151">Set up your production environment</span></span>
> [!NOTE]
> <span data-ttu-id="2e7da-152">이 자습서에 자동으로 사용 하는 hello 스크립트 GitHub 리포지토리에서 지속적인 게시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-152">hello script used in this tutorial automatically configures continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="2e7da-153">GitHub 자격 증명 Azure에 이미 저장 되어, hello 웹 앱에 대 한 소스 제어 설정 tooconfigure 시도할 때 hello 배포 실패를 스크립팅 하는 그렇지 않은 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-153">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment fails when attempting tooconfigure source control settings for hello web apps.</span></span> 
> 
> <span data-ttu-id="2e7da-154">azure에서 자격 증명에 GitHub toostore hello에 웹 앱 만들기 [Azure 포털](https://portal.azure.com/) 및 [GitHub 배포 구성](app-service-continuous-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-154">toostore your GitHub credentials in Azure, create a web app in hello [Azure portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="2e7da-155">하기만 하면 toodo 한 번이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-155">You only need toodo this once.</span></span> 
> 
> 

<span data-ttu-id="2e7da-156">일반적인 DevOps 시나리오에서는 Azure에서 동시에 실행 하는 응용 프로그램 하 고 지속적인 게시를 통해 변경 내용을 tooit toomake 하려는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-156">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="2e7da-157">이 시나리오에서는 사용자에 게 템플릿이 있습니다 개발, 테스트 및 사용 되는 toodeploy hello 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-157">In this scenario, you have a template that you developed, tested, and used toodeploy hello production environment.</span></span> <span data-ttu-id="2e7da-158">이 섹션에서는 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-158">You will set it up in this section.</span></span>

1. <span data-ttu-id="2e7da-159">사용자 고유의 분기의 hello 만들기 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-159">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="2e7da-160">분기를 만드는 방법에 대한 자세한 내용은 [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e7da-160">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="2e7da-161">사용자의 포크를 생성하면, 브라우저에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-161">Once your fork is created, you can see it in your browser.</span></span>
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="2e7da-162">Git 셸 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-162">Open a Git Shell session.</span></span> <span data-ttu-id="2e7da-163">Git 셸이 없는 경우 [Windows용 GitHub](https://windows.github.com/) 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-163">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="2e7da-164">Hello 다음 명령을 실행 하 여 포크의 로컬 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-164">Create a local clone of your fork by executing hello following command:</span></span>

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. <span data-ttu-id="2e7da-165">로컬 복제본을 사용 하는 후 너무 이동*&lt;repository_root >*\ARMTemplates, 및 실행된 hello deploy.ps1 다음과 같이 스크립트:</span><span class="sxs-lookup"><span data-stu-id="2e7da-165">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script as follows:</span></span>
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. <span data-ttu-id="2e7da-166">대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-166">When prompted, type in hello desired username and password for database access.</span></span>
   
   <span data-ttu-id="2e7da-167">다양 한 Azure 리소스의 진행 상태를 프로 비전 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-167">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="2e7da-168">배포가 완료 되 면 hello 스크립트 hello 브라우저에서 hello 응용 프로그램을 시작 하 고 친숙 한 경고음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-168">When deployment completes, hello script launches hello application in hello browser and give you a friendly beep.</span></span>
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > <span data-ttu-id="2e7da-169">살펴보기  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee 어떻게 고유 Id 사용 하 여 리소스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-169">Take a look at *&lt;repository_root>*\ARMTemplates\Deploy.ps1, toosee how it generates resources with unique IDs.</span></span> <span data-ttu-id="2e7da-170">Hello 동일한 접근 방식을 toocreate의 복제를 사용할 수 있습니다 충돌 하는 리소스 이름에 대 한 걱정 없이 동일한 배포 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-170">You can use hello same approach toocreate clones of hello same deployment without worrying about conflicting resource names.</span></span>
   > 
   > 
6. <span data-ttu-id="2e7da-171">Git 셸 세션으로 돌아가서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-171">Back in your Git Shell session, run:</span></span>
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. <span data-ttu-id="2e7da-172">Hello 스크립트 작업을 마치면 toobrowse toohello 프런트 엔드의 주소 돌아가서 (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello 응용 프로그램을 프로덕션 환경에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-172">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="2e7da-173">Toohello 로그인 [Azure 포털](https://portal.azure.com/) 무엇이 확인 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-173">Log in toohello [Azure portal](https://portal.azure.com/) and take a look at what’s created.</span></span>
   
   <span data-ttu-id="2e7da-174">Hello에 수 toosee 두 웹 응용 프로그램 수 같은 리소스 그룹, hello 사용 하 여 `Api` hello 이름에서 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-174">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="2e7da-175">Hello 리소스 그룹 보기를 보면 hello SQL 데이터베이스 및 서버, 앱 서비스 계획 hello 및 hello 웹 앱에 대 한 스테이징 슬롯 hello도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-175">If you look at hello resource group view, you also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="2e7da-176">Hello 다양 한 리소스를 탐색 하 고 비교를 사용 하 여  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 서식 파일에 구성 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-176">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

<span data-ttu-id="2e7da-177">이제 설정한 hello 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-177">You have now set up hello production environment.</span></span> <span data-ttu-id="2e7da-178">다음으로 새 업데이트 toohello 응용 프로그램 시작과 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-178">Next, you will kick off a new update toohello application.</span></span>

## <a name="create-dev-and-test-branches"></a><span data-ttu-id="2e7da-179">Dev를 생성하고 분기점을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-179">Create dev and test branches</span></span>
<span data-ttu-id="2e7da-180">Azure에서 프로덕션 환경에서 실행 되는 복잡 한 응용 프로그램을가지고 agile 방법론에 따라 업데이트 tooyour 응용 프로그램을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-180">Now that you have a complex application running in production in Azure, you will make an update tooyour application in accordance with agile methodology.</span></span> <span data-ttu-id="2e7da-181">이 섹션에서는 hello toomake hello 필요한 업데이트 해야 하는 개발 및 테스트 분기를 만들 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-181">In this section, you will create hello dev and test branches that you will need toomake hello required updates.</span></span>

1. <span data-ttu-id="2e7da-182">먼저 hello 테스트 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-182">Create hello test environment first.</span></span> <span data-ttu-id="2e7da-183">Git 셸 세션에서 실행된 hello 다음 명령을 호출 하는 새 분기에 대 한 toocreate hello 환경을 **NewUpdate**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-183">In your Git Shell session, run hello following commands toocreate hello environment for a new branch called **NewUpdate**.</span></span> 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. <span data-ttu-id="2e7da-184">대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-184">When prompted, type in hello desired username and password for database access.</span></span> 
   
   <span data-ttu-id="2e7da-185">배포가 완료 되 면 hello 스크립트 hello 브라우저에서 hello 응용 프로그램을 시작 하 고 친숙 한 경고음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-185">When deployment completes, hello script launches hello application in hello browser and give you a friendly beep.</span></span> <span data-ttu-id="2e7da-186">이제 자체 테스트 환경이 포함된 새로운 분기점이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-186">You now have a new branch with its own test environment.</span></span> <span data-ttu-id="2e7da-187">이 테스트 환경에 대 한 몇 가지 순간 tooreview를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-187">Take a moment tooreview a few things about this test environment:</span></span>
   
   * <span data-ttu-id="2e7da-188">모든 Azure 구독에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-188">You can create it in any Azure subscription.</span></span> <span data-ttu-id="2e7da-189">즉, hello 프로덕션 환경과 테스트 환경에서 별도로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-189">That means hello production environment can be managed separately from your test environment.</span></span>
   * <span data-ttu-id="2e7da-190">테스트 환경을 라이브 Azure에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-190">Your test environment is running live in Azure.</span></span>
   * <span data-ttu-id="2e7da-191">테스트 환경에 스테이징 슬롯 hello 및 hello 배율 설정을 제외 하 고 동일한 toohello 프로덕션 환경이입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-191">Your test environment is identical toohello production environment, except for hello staging slots and hello scaling settings.</span></span> <span data-ttu-id="2e7da-192">알고 있는 ProdandStage.json와 Dev.json 간의 유일한 차이점 hello 되기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-192">You know it because they are hello only differences between ProdandStage.json and Dev.json.</span></span>
   * <span data-ttu-id="2e7da-193">다른 가격 계층(예: **무료**)으로 자체 앱 서비스 계획에서 테스트 환경을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-193">You can manage your test environment in its own App Service plan, with a different price tier (such as **Free**).</span></span>
   * <span data-ttu-id="2e7da-194">이 테스트 환경을 삭제 작업은을 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-194">Deleting this test environment is as simple as deleting hello resource group.</span></span> <span data-ttu-id="2e7da-195">방법을 배울 toodo이 [나중](#delete)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-195">You will find out how toodo this [later](#delete).</span></span>
3. <span data-ttu-id="2e7da-196">다음 명령을 실행 하 여 dev 분기 hello toocreate 참조.</span><span class="sxs-lookup"><span data-stu-id="2e7da-196">Go on toocreate a dev branch by running hello following commands:</span></span>
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. <span data-ttu-id="2e7da-197">대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-197">When prompted, type in hello desired username and password for database access.</span></span> 
   
   <span data-ttu-id="2e7da-198">순간 tooreview이 개발 환경에 대 한 몇 가지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-198">Take a moment tooreview a few things about this dev environment:</span></span> 
   
   * <span data-ttu-id="2e7da-199">배포 되어 서 hello를 사용 하 여 개발 환경에 구성 동일한 toohello 테스트 환경에 같은 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2e7da-199">Your dev environment has a configuration identical toohello test environment because it’s deployed using hello same template.</span></span>
   * <span data-ttu-id="2e7da-200">Hello 개발자의 Azure 구독에서 별도로 관리 하는 hello 테스트 환경 toobe 두면 각 개발 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-200">Each dev environment can be created in hello developer’s own Azure subscription, leaving hello test environment toobe separately managed.</span></span>
   * <span data-ttu-id="2e7da-201">개발 환경이 Azure에서 실시간 작동 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-201">Your dev environment is running live in Azure.</span></span>
   * <span data-ttu-id="2e7da-202">환경은 hello dev를 삭제 하기만 하면 hello 리소스 그룹을 삭제 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-202">Deleting hello dev environment is as simple as deleting hello resource group.</span></span> <span data-ttu-id="2e7da-203">방법을 배울 toodo이 [나중](#delete)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-203">You will find out how toodo this [later](#delete).</span></span>

> [!NOTE]
> <span data-ttu-id="2e7da-204">여러 개발자가 hello 새 업데이트에서 작업을 사용 하는 경우 각 사람 쉽게 만들 수 있는 분기와 전용된 개발 환경을 단계를 수행 하는 hello로:</span><span class="sxs-lookup"><span data-stu-id="2e7da-204">When you have multiple developers working on hello new update, each of them can easily create a branch and dedicated dev environment with hello following steps:</span></span>
> 
> 1. <span data-ttu-id="2e7da-205">GitHub에서 자신의 hello 리포지토리 분기를 만듭니다 (참조 [는 리포지토리를 분기](https://help.github.com/articles/fork-a-repo/)).</span><span class="sxs-lookup"><span data-stu-id="2e7da-205">Create their own fork of hello repository in GitHub (see [Fork a Repo](https://help.github.com/articles/fork-a-repo/)).</span></span>
> 2. <span data-ttu-id="2e7da-206">로컬 컴퓨터에서 복제 hello 분기</span><span class="sxs-lookup"><span data-stu-id="2e7da-206">Clone hello fork on their local machine</span></span>
> 3. <span data-ttu-id="2e7da-207">Hello 실행 동일 명령 toocreate 자신의 dev 분기와 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-207">Run hello same commands toocreate their own dev branch and environment.</span></span>
> 
> 

<span data-ttu-id="2e7da-208">완료되면, GitHub 포크는 세 개의 분기가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-208">When you’re done, your GitHub fork should have three branches:</span></span>

![](./media/app-service-agile-software-development/test-1-github-view.png)

<span data-ttu-id="2e7da-209">3 개의 별도 리소스 그룹에서 6개의 웹앱(한 그룹에 2개의 응용 프로그램)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-209">And you should have six web apps (three sets of two) in three separate resource groups:</span></span>

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> <span data-ttu-id="2e7da-210">ProdandStage.json 지정 hello 프로덕션 환경 toouse hello **표준** 가격 책정 계층 hello 프로덕션 응용 프로그램의 확장성에 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-210">ProdandStage.json specifies hello production environment toouse hello **Standard** pricing tier, which is appropriate for scalability of hello production application.</span></span>
> 
> 

## <a name="build-and-test-every-commit"></a><span data-ttu-id="2e7da-211">모든 커밋을 구축하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-211">Build and test every commit</span></span>
<span data-ttu-id="2e7da-212">템플릿 파일 ProdAndStage.json hello 및 Dev.json 이미 hello 소스 제어 매개 변수를 지정 hello 웹 응용 프로그램에 지속적인 게시를 설정 하는 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-212">hello template files ProdAndStage.json and Dev.json already specify hello source control parameters, which by default sets up continuous publishing for hello web app.</span></span> <span data-ttu-id="2e7da-213">따라서 모든 커밋 toohello GitHub 분기 로부터 자동 배포 tooAzure를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-213">Therefore, every commit toohello GitHub branch triggers an automatic deployment tooAzure from that branch.</span></span> <span data-ttu-id="2e7da-214">이제 설치 작업을 하는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-214">Let’s see how your setup works now.</span></span>

1. <span data-ttu-id="2e7da-215">Hello 로컬 저장소의 hello Dev 분기에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-215">Make sure that you’re in hello Dev branch of hello local repository.</span></span> <span data-ttu-id="2e7da-216">toodo 다음 명령을 Git 셸에서이, 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="2e7da-216">toodo this, run hello following command in Git Shell:</span></span>
   
        git checkout Dev
2. <span data-ttu-id="2e7da-217">Hello 코드 toouse 변경 하 여 변경 toohello 앱의 UI 계층을 만들 [부트스트랩](http://getbootstrap.com/components/) 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-217">Make a change toohello app’s UI layer by changing hello code toouse [Bootstrap](http://getbootstrap.com/components/) lists.</span></span> <span data-ttu-id="2e7da-218">열기  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml 고 강조 표시 된 변경 hello:</span><span class="sxs-lookup"><span data-stu-id="2e7da-218">Open *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml and make hello following highlighted change:</span></span>
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > <span data-ttu-id="2e7da-219">읽을 수 없는 경우에 위 그림 hello:</span><span class="sxs-lookup"><span data-stu-id="2e7da-219">If you can't read hello preceding image:</span></span> 
    > 
    > * <span data-ttu-id="2e7da-220">18 줄에서 변경 `check-list` 너무`list-group`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-220">In line 18, change `check-list` too`list-group`.</span></span>
    > * <span data-ttu-id="2e7da-221">19 줄에서 변경 `class="check-list-item"` 너무`class="list-group-item"`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-221">In line 19, change `class="check-list-item"` too`class="list-group-item"`.</span></span>
    > 
    > 
3. <span data-ttu-id="2e7da-222">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-222">Save hello change.</span></span> <span data-ttu-id="2e7da-223">다시 Git 셸에서 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-223">Back in Git Shell, run hello following commands:</span></span>
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   <span data-ttu-id="2e7da-224">Git 유사한 너무 "확인" 코드에서 TFS와 같은 다른 소스 제어 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-224">These git commands are similar too"checking in your code" in another source control system like TFS.</span></span> <span data-ttu-id="2e7da-225">실행 하는 경우 `git push`, hello 새 커밋에는 다음 다시 작성 hello hello 개발 환경에서 응용 프로그램 tooreflect hello 변경 하는 자동 코드 푸시 tooAzure 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-225">When you run `git push`, hello new commit triggers an automatic code push tooAzure, which then rebuilds hello application tooreflect hello change in hello dev environment.</span></span>
4. <span data-ttu-id="2e7da-226">이 코드 푸시 tooyour 개발 환경 발생 했음을 tooverify tooyour 개발 환경 웹 응용 프로그램 페이지를 이동 하 고 hello 확인 **배포** 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-226">tooverify that this code push tooyour dev environment has occurred, go tooyour dev environment’s web app page and look at hello **Deployment** part.</span></span> <span data-ttu-id="2e7da-227">최신 커밋 있는 메시지 수 toosee 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-227">You should be able toosee your latest commit message there.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. <span data-ttu-id="2e7da-228">여기에서 클릭 **찾아보기** toosee hello Azure의 hello 라이브 응용 프로그램에 새로운 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-228">From there, click **Browse** toosee hello new change in hello live application in Azure.</span></span>
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   <span data-ttu-id="2e7da-229">최소 변경 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-229">It's a minor change toohello application.</span></span> <span data-ttu-id="2e7da-230">그러나 새 변경 내용 tooa 복잡 한 웹 응용 프로그램 시간 대부분에 의도 하지 않은 및 원치 않는 부작용입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-230">However, many times new changes tooa complex web application have unintended and undesirable side effects.</span></span> <span data-ttu-id="2e7da-231">수 tooeasily 테스트 되 고 모든 커밋과 라이브 빌드에 사용 하면 toocatch 있습니다 이러한 문제 고객에 게 표시 되기 전에.</span><span class="sxs-lookup"><span data-stu-id="2e7da-231">Being able tooeasily test every commit in live builds enables you toocatch these issues before your customers see them.</span></span>

<span data-ttu-id="2e7da-232">지금까지 hello 인식 방법을 잘 알고 있어야 hello에 개발자는 **NewUpdate** 프로젝트를 빌드하고 수 있습니다를 직접 위한 개발 환경을 만들려면 다음 모든 커밋과 모든 빌드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-232">By now, you should be comfortable with hello realization that, as a developer on hello **NewUpdate** project, you can create a dev environment for yourself, then build every commit and test every build.</span></span>

## <a name="merge-code-into-test-environment"></a><span data-ttu-id="2e7da-233">테스트 환경에 코드를 병합</span><span class="sxs-lookup"><span data-stu-id="2e7da-233">Merge code into test environment</span></span>
<span data-ttu-id="2e7da-234">을 사용 하는 준비 toopush tooNewUpdate 분기를 Dev에서 코드를 분기는 hello 표준 git 프로세스:</span><span class="sxs-lookup"><span data-stu-id="2e7da-234">When you’re ready toopush your code from Dev branch up tooNewUpdate branch, it’s hello standard git process:</span></span>

1. <span data-ttu-id="2e7da-235">다른 개발자가 만든 커밋이 같은 github를 hello Dev 분기에 모든 새 커밋이 tooNewUpdate를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-235">Merge any new commits tooNewUpdate into hello Dev branch in GitHub, such as commits created by other developers.</span></span> <span data-ttu-id="2e7da-236">GitHub에 대 한 모든 새 커밋을 코드 푸시 및 hello 개발 환경에서 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-236">Any new commit on GitHub triggers a code push and build in hello dev environment.</span></span> <span data-ttu-id="2e7da-237">그런 다음 Dev 분기의 코드로 hello 최신 비트로 NewUpdate 분기에서 여전히 작동 하는지을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-237">You can then make sure your code in Dev branch still works with hello latest bits from NewUpdate branch.</span></span>
2. <span data-ttu-id="2e7da-238">개발 분기의 모든 새 커밋을 GitHub의 새 업데이트 브랜치로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-238">Merge all your new commits from Dev branch into NewUpdate branch on GitHub.</span></span> <span data-ttu-id="2e7da-239">이 동작은 코드 푸시 및 hello 테스트 환경에서 빌드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-239">This action triggers a code push and build in hello test environment.</span></span> 

<span data-ttu-id="2e7da-240">Note 다시 연속 배포는 이미 이러한 git 분기를 설정 하기 때문에 실행 통합 같은 다른 작업을 모두 빌드 tootake 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-240">Note again that because continuous deployment is already set up with these git branches, you don’t need tootake any other action like running integration builds.</span></span> <span data-ttu-id="2e7da-241">Git를 사용 하 여 tooperform 표준 소스 제어 사례를 제공 하기만 하 고 Azure 사용자에 대 한 모든 hello 빌드 프로세스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-241">You simply need tooperform standard source control practices using git, and Azure performs all hello build processes for you.</span></span>

<span data-ttu-id="2e7da-242">이제 코드를 너무 푸시 보겠습니다**NewUpdate** 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-242">Now, let’s push your code too**NewUpdate** branch.</span></span> <span data-ttu-id="2e7da-243">Git 셸에서 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-243">In Git Shell, run hello following commands:</span></span>

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

<span data-ttu-id="2e7da-244">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-244">That’s it!</span></span> 

<span data-ttu-id="2e7da-245">이동 toohello 웹 응용 프로그램 페이지에 대 한 테스트 환경 toosee (NewUpdate 분기에 병합) 새 커밋 이제 푸시 toohello 테스트 환경.</span><span class="sxs-lookup"><span data-stu-id="2e7da-245">Go toohello web app page for your test environment toosee your new commit (merged into NewUpdate branch) now pushed toohello test environment.</span></span> <span data-ttu-id="2e7da-246">클릭 **찾아보기** 스타일 변경 hello toosee Azure 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-246">Then, click **Browse** toosee that hello style change is now running live in Azure.</span></span>

## <a name="deploy-update-tooproduction"></a><span data-ttu-id="2e7da-247">업데이트 tooproduction 배포</span><span class="sxs-lookup"><span data-stu-id="2e7da-247">Deploy update tooproduction</span></span>
<span data-ttu-id="2e7da-248">코드 toohello 푸시 스테이징 및 프로덕션 환경까지 이미 작업 한 내용을 코드 toohello 테스트 환경 푸시되는 방법과 다르지 않습니다 느끼지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-248">Pushing code toohello staging and production environment should feel no different than what you’ve already done when you pushed code toohello test environment.</span></span> <span data-ttu-id="2e7da-249">매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-249">It's really that simple.</span></span> 

<span data-ttu-id="2e7da-250">Git 셸에서 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-250">In Git Shell, run hello following commands:</span></span>

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

<span data-ttu-id="2e7da-251">ProdandStage.json에 hello 스테이징 및 프로덕션 환경이 설정 된 hello 방식을 기준으로 새 코드 toohello 푸시됩니다 **준비** 슬롯 없습니다 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-251">Remember that based on hello way hello staging and production environment is set up in ProdandStage.json, your new code is pushed toohello **Staging** slot and is running there.</span></span> <span data-ttu-id="2e7da-252">따라서 toohello 스테이징 슬롯의 URL을 탐색 하는 경우에 hello 여기서 실행 되는 새 코드를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-252">So if you navigate toohello staging slot’s URL, you see hello new code running there.</span></span> <span data-ttu-id="2e7da-253">toodo Git 셸에서 cmdlet을 다음이 실행된 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-253">toodo this, run hello following cmdlet in Git Shell.</span></span>

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

<span data-ttu-id="2e7da-254">Hello 슬롯의 hello 업데이트를 확인 한 후 남았습니다 toodo tooswap 파일인 hello 하는 이제 및 프로덕션 환경에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-254">And now, after you’ve verified hello update in hello staging slot, hello only thing left toodo is tooswap it into production.</span></span> <span data-ttu-id="2e7da-255">Git 셸에서 hello 다음 명령을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-255">In Git Shell, just run hello following commands:</span></span>

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

<span data-ttu-id="2e7da-256">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-256">Congratulations!</span></span> <span data-ttu-id="2e7da-257">새 업데이트 tooyour 프로덕션 웹 응용 프로그램을 성공적으로 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-257">You’ve successfully published a new update tooyour production web application.</span></span> <span data-ttu-id="2e7da-258">게다가 쉽게 개발과 테스트 환경을 생성하고, 모든 커밋을 구축하고 테스트함으로써 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-258">What’s more is that did it by easily creating dev and test environments, and building and testing every commit.</span></span> <span data-ttu-id="2e7da-259">이들은 agile 소프트웨어 개발의 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-259">These are crucial building blocks for agile software development.</span></span>

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a><span data-ttu-id="2e7da-260">개발 환경과 테스트 환경 삭제</span><span class="sxs-lookup"><span data-stu-id="2e7da-260">Delete dev and test environments</span></span>
<span data-ttu-id="2e7da-261">되기 쉬운 toodelete 프로그램 개발의 의도적으로 설계 하 고 테스트 환경 toobe 자체 포함 된 리소스 그룹 때문에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-261">Because you have purposely architected your dev and test environments toobe self-contained resource groups, it is easy toodelete them.</span></span> <span data-ttu-id="2e7da-262">toodelete hello hello GitHub 분기와 Azure 아티팩트를 모두이 자습서에서 만든 것 hello 셸에서 Git 명령을 다음 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-262">toodelete hello ones you created in this tutorial, both hello GitHub branches and Azure artifacts, just run hello following commands in Git Shell:</span></span>

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a><span data-ttu-id="2e7da-263">요약</span><span class="sxs-lookup"><span data-stu-id="2e7da-263">Summary</span></span>
<span data-ttu-id="2e7da-264">Agile 소프트웨어 개발에는 응용 프로그램 플랫폼으로 Azure tooadopt 하려는 대부분의 회사은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-264">Agile software development is a must-have for many companies who want tooadopt Azure as their application platform.</span></span> <span data-ttu-id="2e7da-265">이 자습서에서는 어떻게 toocreate와 정확 하 게 아래로 또는 옆의 복제본 삭제 hello 프로덕션 환경으로 복잡 한 응용 프로그램에도 쉽게 알아 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-265">In this tutorial, you have learned how toocreate and tear down exact replicas or near replicas of hello production environment with ease, even for complex applications.</span></span> <span data-ttu-id="2e7da-266">이 기능은 toocreate 개발 처리 하는 tooleverage 방법 또한 배웠습니다 빌드하고 Azure의 단일 커밋 모든 테스트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-266">You have also learned how tooleverage this ability toocreate a development process that can build and test every single commit in Azure.</span></span> <span data-ttu-id="2e7da-267">이 자습서에서는 다행 스럽게도 살펴보았습니다 사용 하는 방법을 가장 함께 toocreate Azure 앱 서비스 및 Azure 리소스 관리자는 DevOps 솔루션 tooagile 방법론 빈도가 낮은입니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-267">This tutorial has hopefully shown you how you can best use Azure App Service and Azure Resource Manager together toocreate a DevOps solution that caters tooagile methodologies.</span></span> <span data-ttu-id="2e7da-268">다음으로 [프로덕션에서 테스트](app-service-web-test-in-production-get-start.md)와 고급 DevOps 기술을 수행하여 시나리오를 계속 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e7da-268">Next, you can build on this scenario by performing advanced DevOps techniques such as [testing in production](app-service-web-test-in-production-get-start.md).</span></span> <span data-ttu-id="2e7da-269">일반적인 프로덕션 시나리오 테스트의 경우 [Azure 앱 서비스에서 Flighting 배포(베타 테스트)](app-service-web-test-in-production-controlled-test-flight.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e7da-269">For a common testing-in-production scenario, see [Flighting deployment (beta testing) in Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).</span></span>

## <a name="more-resources"></a><span data-ttu-id="2e7da-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2e7da-270">More resources</span></span>
* [<span data-ttu-id="2e7da-271">Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포</span><span class="sxs-lookup"><span data-stu-id="2e7da-271">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="2e7da-272">Agile 개발 연습에서: 현대화 개발 주기의 팁과 트릭</span><span class="sxs-lookup"><span data-stu-id="2e7da-272">Agile Development in Practice: Tips and Tricks for Modernized Development Cycle</span></span>](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [<span data-ttu-id="2e7da-273">리소스 관리자 템플릿을 사용하여 Azure 웹앱의 고급 배포 전략</span><span class="sxs-lookup"><span data-stu-id="2e7da-273">Advanced deployment strategies for Azure Web Apps using Resource Manager templates</span></span>](http://channel9.msdn.com/Events/Build/2015/2-620)
* [<span data-ttu-id="2e7da-274">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="2e7da-274">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="2e7da-275">JSONLint-hello JSON 유효성 검사기</span><span class="sxs-lookup"><span data-stu-id="2e7da-275">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="2e7da-276">ARMClient – 게시 toosite GitHub 설정</span><span class="sxs-lookup"><span data-stu-id="2e7da-276">ARMClient – Set up GitHub publishing toosite</span></span>](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [<span data-ttu-id="2e7da-277">Git 분기-기본 분기 및 병합</span><span class="sxs-lookup"><span data-stu-id="2e7da-277">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="2e7da-278">David Ebbo의 블로그</span><span class="sxs-lookup"><span data-stu-id="2e7da-278">David Ebbo’s Blog</span></span>](http://blog.davidebbo.com/)
* [<span data-ttu-id="2e7da-279">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e7da-279">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2e7da-280">Azure 플랫폼간 명령줄 도구</span><span class="sxs-lookup"><span data-stu-id="2e7da-280">Azure Cross-Platform Command-Line Tools</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="2e7da-281">Azure AD에서 사용자 만들기 또는 편집</span><span class="sxs-lookup"><span data-stu-id="2e7da-281">Create or edit users in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [<span data-ttu-id="2e7da-282">프로젝트 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="2e7da-282">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)

