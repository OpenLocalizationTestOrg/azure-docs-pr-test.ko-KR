---
title: "aaaFlighting 배포 (베타)에서 테스트 Azure 앱 서비스"
description: "응용 프로그램 또는 베타의 새로운 기능 tooflight이 종단 간 자습서에서 업데이트를 테스트 하는 방법을 알아봅니다. 연속 게시, 슬롯, 트래픽 라우팅 및 Application Insights 통합과 같은 앱 서비스 기능을 함께 소개합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="2e49a-104">Azure 앱 서비스에서 Flighting 배포(베타 테스트)</span><span class="sxs-lookup"><span data-stu-id="2e49a-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="2e49a-105">이 자습서에서는 어떻게 toodo *플 라이팅 배포* 통합 하 여 hello의 다양 한 기능 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 및 [Azure Application Insights](/services/application-insights/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-105">This tutorial shows you how toodo *flighting deployments* by integrating hello various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="2e49a-106">*Flighting* 은 제한된 수의 실제 고객으로 새로운 기능 또는 변경의 유효성을 검사하는 배포 프로세스이며 프로덕션 시나리오의 주요 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="2e49a-107">김 윤 식 toobeta는 테스트 및 "처리 중 통제 된 테스트" 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-107">It is akin toobeta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="2e49a-108">웹 서비스를 제공하는 많은 대기업이 이 방법을 사용하여 [민첩한 개발](https://en.wikipedia.org/wiki/Agile_software_development)이라는 해당 연습에서 앱 업데이트의 초기 유효성 검사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="2e49a-109">Azure 앱 서비스 하면 지속적인 게시로 프로덕션에서 toointegrate 테스트 하 고 Application Insights tooimplement hello 동일한 DevOps 시나리오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-109">Azure App Service enables you toointegrate test in production with continous publishing and Application Insights tooimplement hello same DevOps scenario.</span></span> <span data-ttu-id="2e49a-110">이 방법의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="2e49a-111">**실제 피드백을 얻을 *전에* 업데이트가 릴리스된 tooproduction** -hello 놓으면으로 피드백을 얻는 것 피드백 해제 하기 전에 취소만 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-111">**Gain real feedback *before* updates are released tooproduction** - hello only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="2e49a-112">초기 hello 제품 수명 주기에서 사용자가 원하는 실제 사용자 트래픽 및 동작을 사용 하 여 업데이트를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-112">You can test updates with real user traffic and behaviors as early as you desire in hello product life cycle.</span></span>
* <span data-ttu-id="2e49a-113">**[연속 테스트 기반 개발(CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development) 향상** - Application Insights를 사용하여 연속 통합 및 계측으로 프로덕션에서 테스트를 통합하여 사용자 유효성 검사가 제품 수명 주기에서 초기에 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="2e49a-114">수동 테스트 실행에 시간 투자를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="2e49a-115">**테스트 워크플로 최적화** -연속 모니터링 계측으로 프로덕션에서 테스트를 자동화 하 여 수행할 수 있습니다 잠재적으로 단일 프로세스에서 테스트의 다양 한 종류의 hello 목표와 같은 [통합](https://en.wikipedia.org/wiki/Integration_testing), [회귀](https://en.wikipedia.org/wiki/Regression_testing), [유용성](https://en.wikipedia.org/wiki/Usability_testing), 내게 필요한 옵션, 지역화, [성능](https://en.wikipedia.org/wiki/Software_performance_testing), [보안](https://en.wikipedia.org/wiki/Security_testing), 및 [ 승인](https://en.wikipedia.org/wiki/Acceptance_testing)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish hello goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="2e49a-116">Flighting 배포는 라이브 트래픽의 라우팅에 국한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="2e49a-117">이러한 배포는 예기치 않은 버그, 성능 저하, 사용자 환경 문제 인지 여부를 최대한 빨리 toogain 통찰력을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-117">In such a deployment you want toogain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="2e49a-118">실제 고객을 상대한다는 점을 기억하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="2e49a-119">따라서 toodo 것 바로, 있어야를 설정한 후에 플 라이팅 배포 toogather 하면 필요한 순서 toomake 결정을 내릴된 다음 단계에 대 한 모든 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-119">So toodo it right, you must make sure that you have set up your flighting deployment toogather all hello data you need in order toomake an informed decision for your next step.</span></span> <span data-ttu-id="2e49a-120">이 자습서에서는 New Relic 또는 시나리오에 적합 한 기타 기술 있지만 Application Insights를 사용 하 여 toocollect 데이터 사용 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-120">This tutorial shows you how toocollect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2e49a-121">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="2e49a-121">What you will do</span></span>
<span data-ttu-id="2e49a-122">이 자습서에서는 살펴보겠습니다 어떻게 toobring 프로덕션에서 응용 프로그램 서비스 응용 프로그램 시나리오 함께 tootest 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="2e49a-122">In this tutorial, you will learn how toobring hello following scenarios together tootest your App Service app in production:</span></span>

* <span data-ttu-id="2e49a-123">[프로덕션 트래픽을 라우팅할](app-service-web-test-in-production-get-start.md) tooyour 베타 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2e49a-123">[Route production traffic](app-service-web-test-in-production-get-start.md) tooyour beta app</span></span>
* <span data-ttu-id="2e49a-124">[응용 프로그램을 계측할](../application-insights/app-insights-web-track-usage.md) tooobtain 유용한 메트릭</span><span class="sxs-lookup"><span data-stu-id="2e49a-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) tooobtain useful metrics</span></span>
* <span data-ttu-id="2e49a-125">연속 베타 앱 배포 및 라이브 앱 메트릭 추적</span><span class="sxs-lookup"><span data-stu-id="2e49a-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="2e49a-126">Hello 프로덕션 앱 및 코드 어떻게 변경 되는지 hello 베타 앱 toosee 간의 비교 메트릭 tooresults 변환</span><span class="sxs-lookup"><span data-stu-id="2e49a-126">Compare metrics between hello production app and hello beta app toosee how code changes translate tooresults</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="2e49a-127">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="2e49a-127">What you will need</span></span>
* <span data-ttu-id="2e49a-128">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="2e49a-128">An Azure account</span></span>
* <span data-ttu-id="2e49a-129">[GitHub](https://github.com/) 계정</span><span class="sxs-lookup"><span data-stu-id="2e49a-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="2e49a-130">Visual Studio 2015-hello를 다운로드할 수 있습니다 [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-130">Visual Studio 2015 - you can download hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="2e49a-131">Git 셸 (설치 된 [Windows 용 GitHub](https://windows.github.com/))-이 통해 있습니다 toorun hello 두 hello Git 및 PowerShell 명령 동일한 세션</span><span class="sxs-lookup"><span data-stu-id="2e49a-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you toorun both hello Git and PowerShell commands in hello same session</span></span>
* <span data-ttu-id="2e49a-132">최신 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) 비트</span><span class="sxs-lookup"><span data-stu-id="2e49a-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="2e49a-133">기본적으로 hello 다음 이해:</span><span class="sxs-lookup"><span data-stu-id="2e49a-133">Basic understanding of hello following:</span></span>
  * <span data-ttu-id="2e49a-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 템플릿 배포([Azure에서 예측 가능하도록 복잡한 응용 프로그램 배포](app-service-deploy-complex-application-predictably.md) 참조)</span><span class="sxs-lookup"><span data-stu-id="2e49a-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="2e49a-135">Git</span><span class="sxs-lookup"><span data-stu-id="2e49a-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="2e49a-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e49a-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="2e49a-137">이 자습서는 Azure 계정 toocomplete 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-137">You need an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="2e49a-138">할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/) -크레딧을 얻게 Azure 서비스를 유료 아웃 tootry 사용할 수 있으며 모두 사용 하는 후에 hello 계정 등에 사용 가능한 웹 응용 프로그램 등의 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="2e49a-139">[Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) 할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="2e49a-140">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-140">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2e49a-141">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="2e49a-142">프로덕션 웹앱 설치</span><span class="sxs-lookup"><span data-stu-id="2e49a-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="2e49a-143">이 자습서에 사용 된 hello 스크립트 GitHub 리포지토리에서 지속적인 게시를 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-143">hello script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="2e49a-144">이렇게 하려면 GitHub 자격 증명 Azure에 이미 저장 되어, hello 웹 앱에 대 한 소스 제어 설정 tooconfigure 시도할 때 스크립팅된 hello 배포 그렇지 않으면 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-144">This requires that your GitHub credentials are already stored in Azure, otherwise hello scripted deployment will fail when attempting tooconfigure source control settings for hello web apps.</span></span>
>
> <span data-ttu-id="2e49a-145">azure에서 자격 증명에 GitHub toostore hello에 웹 앱 만들기 [Azure 포털](https://portal.azure.com/) 및 [GitHub 배포 구성](app-service-continuous-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-145">toostore your GitHub credentials in Azure, create a web app in hello [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="2e49a-146">하기만 하면 toodo 한 번이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-146">You only need toodo this once.</span></span>
>
>

<span data-ttu-id="2e49a-147">일반적인 DevOps 시나리오에서는 Azure에서 동시에 실행 하는 응용 프로그램 하 고 지속적인 게시를 통해 변경 내용을 tooit toomake 하려는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want toomake changes tooit through continuous publishing.</span></span> <span data-ttu-id="2e49a-148">이 시나리오에서는 tooproduction가 개발 하 고 테스트 하는 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-148">In this scenario, you will deploy tooproduction a template that you have developed and tested.</span></span>

1. <span data-ttu-id="2e49a-149">사용자 고유의 분기의 hello 만들기 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-149">Create your own fork of hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="2e49a-150">분기를 만드는 방법에 대한 자세한 내용은 [리포지토리 분기](https://help.github.com/articles/fork-a-repo/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e49a-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="2e49a-151">사용자의 포크를 생성하면, 브라우저에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="2e49a-152">Git 셸 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-152">Open a Git Shell session.</span></span> <span data-ttu-id="2e49a-153">Git 셸이 없는 경우 [Windows용 GitHub](https://windows.github.com/) 를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="2e49a-154">Hello 다음 명령을 실행 하 여 포크의 로컬 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-154">Create a local clone of your fork by executing hello following command:</span></span>

     <span data-ttu-id="2e49a-155">git clone https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="2e49a-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="2e49a-156">로컬 복제본을 사용 하는 후 너무 이동*&lt;repository_root >*\ARMTemplates, 및 실행된 hello deploy.ps1 같이 고유한 접미사와 함께 아래 스크립트:</span><span class="sxs-lookup"><span data-stu-id="2e49a-156">Once you have your local clone, navigate too*&lt;repository_root>*\ARMTemplates, and run hello deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="2e49a-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span><span class="sxs-lookup"><span data-stu-id="2e49a-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="2e49a-158">대화 상자가 나타나면 원하는 hello 사용자 이름 및 데이터베이스 액세스에 대 한 암호에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-158">When prompted, type in hello desired username and password for database access.</span></span> <span data-ttu-id="2e49a-159">Toospecify 필요 하므로 데이터베이스 자격 증명 기억 다시 때 업데이트 hello 리소스 그룹에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-159">Remember your database credentials because you will need toospecify them again when updating hello resource group.</span></span>

   <span data-ttu-id="2e49a-160">다양 한 Azure 리소스의 진행 상태를 프로 비전 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-160">You should see hello provisioning progress of various Azure resources.</span></span> <span data-ttu-id="2e49a-161">배포가 완료 되 면 hello 스크립트 hello 브라우저에서 응용 프로그램 hello 실행과 친숙 한 경고음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-161">When deployment completes, hello script will launch hello application in hello browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="2e49a-162">Git 셸 세션으로 돌아가서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="2e49a-163">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="2e49a-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="2e49a-164">Hello 스크립트 작업을 마치면 toobrowse toohello 프런트 엔드의 주소 돌아가서 (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello 응용 프로그램을 프로덕션 환경에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-164">When hello script finishes, go back toobrowse toohello frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) toosee hello application running in production.</span></span>
8. <span data-ttu-id="2e49a-165">Hello에 로그인 [Azure 포털](https://portal.azure.com/) 무엇이 확인 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-165">Log into hello [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="2e49a-166">Hello에 수 toosee 두 웹 응용 프로그램 수 같은 리소스 그룹, hello 사용 하 여 `Api` hello 이름에서 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-166">You should be able toosee two web apps in hello same resource group, one with hello `Api` suffix in hello name.</span></span> <span data-ttu-id="2e49a-167">Hello 리소스 그룹 보기를 보면 하는 경우 hello SQL 데이터베이스 및 서버, 앱 서비스 계획 hello 및 hello 웹 앱에 대 한 스테이징 슬롯 hello도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-167">If you look at hello resource group view, you will also see hello SQL Database and server, hello App Service plan, and hello staging slots for hello web apps.</span></span> <span data-ttu-id="2e49a-168">Hello 다양 한 리소스를 탐색 하 고 비교를 사용 하 여  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 서식 파일에 구성 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-168">Browse through hello different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json toosee how they are configured in hello template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="2e49a-169">Hello 프로덕션 응용 프로그램을 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-169">You have set up hello production app.</span></span>  <span data-ttu-id="2e49a-170">이제 유용성 hello 앱에 대 한 나쁘지 피드백 나타나는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-170">Now, let's imagine that you receive feedback that usability is poor for hello app.</span></span> <span data-ttu-id="2e49a-171">따라서 tooinvestigate를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-171">So you decide tooinvestigate.</span></span> <span data-ttu-id="2e49a-172">거 tooinstrument 앱 toogive 피드백 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-172">You're going tooinstrument your app toogive you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="2e49a-173">조사: 모니터링/메트릭에 대한 클라이언트 앱 계측</span><span class="sxs-lookup"><span data-stu-id="2e49a-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="2e49a-174">Visual Studio에서 *&lt;repository_root>*\src\MultiChannelToDo.sln을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="2e49a-175">솔루션 > **솔루션에 대한 NuGet 패키지 관리** > **복원**을 마우스 오른쪽 단추로 클릭하여 모든 NuGet 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="2e49a-176">마우스 오른쪽 단추로 클릭 **MultiChannelToDo.Web** > **Application Insights 원격 분석 추가** > **설정 구성** > 리소스 그룹 변경 tooToDoApp*&lt;your_suffix >* > **Application Insights 추가 tooProject**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
4. <span data-ttu-id="2e49a-177">Hello Azure 포털에서에서 hello에 대 한 hello 블레이드를 엽니다 **MultiChannelToDo.Web** Application Insight 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-177">In hello Azure Portal, open hello blade for hello **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="2e49a-178">Hello 그런 다음 **응용 프로그램 상태** 부, 클릭 **toocollect 브라우저 페이지에서 데이터를 로드 하는 방법에 대해 알아봅니다** > 코드를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-178">Then in hello **Application health** part, click **Learn how toocollect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="2e49a-179">Hello JS 계측 코드를 너무 복사 추가*&lt;repository_root >*hello 닫는 직전 \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-179">Add hello copied JS instrumentation code too*&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before hello closing `<heading>` tag.</span></span> <span data-ttu-id="2e49a-180">Application Insight 리소스의 hello 고유 계측 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-180">It should contain hello unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="2e49a-181">Hello 본문의 코드 toohello 맨 아래에 다음을 추가 하 여 사용자 지정 이벤트 tooApplication Insights 마우스 클릭에 대 한 보내기:</span><span class="sxs-lookup"><span data-stu-id="2e49a-181">Send custom events tooApplication Insights for mouse clicks by adding hello following code toohello bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="2e49a-182">이 JavaScript 코드 조각을 hello 웹 응용 프로그램에서 사용자가 클릭할 때마다 사용자 지정 이벤트 tooApplication 통찰력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-182">This JavaScript snippet sends a custom event tooApplication Insights every time a user clicks anywhere in hello web app.</span></span>
7. <span data-ttu-id="2e49a-183">Git 셸에서 커밋하고 GitHub에서 변경 내용을 tooyour 포크 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-183">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="2e49a-184">다음 클라이언트 toorefresh 브라우저에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-184">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="2e49a-185">배포 된 hello 앱 변경 내용 tooproduction를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-185">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="2e49a-186">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="2e49a-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="2e49a-187">사용자가 구성한 toohello Application Insights 리소스를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-187">Browse toohello Application Insights resource that you configured.</span></span> <span data-ttu-id="2e49a-188">사용자 지정 이벤트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="2e49a-189">사용자 지정 이벤트에 대한 메트릭이 보이지 않으면 몇 분 기다렸다가 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="2e49a-190">아래와 같은 차트를 본다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="2e49a-191">및 그 아래의 이벤트 표 형태 hello:</span><span class="sxs-lookup"><span data-stu-id="2e49a-191">And hello event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="2e49a-192">Hello tooyour ToDoApp 응용 프로그램 코드에 따라, **단추** toohello 전송 단추와 hello 이벤트는 해당 **입력** 이벤트 해당 toohello 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-192">According tooyour ToDoApp application code, hello **BUTTON** event corresponds toohello submit button, and hello **INPUT** event corresponds toohello textbox.</span></span> <span data-ttu-id="2e49a-193">지금까지는 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-193">So far, things make sense.</span></span> <span data-ttu-id="2e49a-194">그러나 것 같습니다.는 충분 한 크기가 클릭 및 매우 몇 번의 클릭 hello 할 일 항목에는 (hello **LI** 이벤트).</span><span class="sxs-lookup"><span data-stu-id="2e49a-194">However, it looks like there's a good amount of clicks and very few clicks on hello to-do items (hello **LI** events).</span></span>

<span data-ttu-id="2e49a-195">이 하면 폼 hello의 어느 부분이 UI는 클릭 가능한 아니며 hello 목록 항목 및 해당 아이콘에 가져가면 hello 커서 텍스트 선택에 대 한 스타일 지정 하기 때문에 일부 사용자가 프로그램 가설 혼동 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-195">Based on this, you form your hypothesis that some users are confused which part of hello UI is clickable and it is because hello cursor is styled for text selection when it hovers on hello list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="2e49a-196">부자연스러운 예제일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-196">This might be a contrived example.</span></span> <span data-ttu-id="2e49a-197">그럼에도 불구 하 고 진행 중인 toomake 개선 tooyour 응용 프로그램 하 고 라이브 고객 으로부터 플 라이팅 배포 tooget 유용성 피드백을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-197">Nevertheless, you're going toomake an improvement tooyour app, and then perform a flighting deployment tooget usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="2e49a-198">모니터링/메트릭에 대한 서버 앱 계측</span><span class="sxs-lookup"><span data-stu-id="2e49a-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="2e49a-199">이 자습서에서 설명 하는 hello 시나리오 hello 클라이언트 앱만 처리 하므로 탄젠트입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-199">This is a tangent since hello scenario demonstrated in this tutorial only deals with hello client app.</span></span> <span data-ttu-id="2e49a-200">그러나 완결성에 대 한 hello 서버 쪽 앱을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-200">However, for completeness you will set up hello server-side app.</span></span>

1. <span data-ttu-id="2e49a-201">마우스 오른쪽 단추로 클릭 **MultiChannelToDo** > **Application Insights 원격 분석 추가** > **설정 구성** > 리소스 그룹 변경 tooToDoApp*&lt;your_suffix >* > **Application Insights 추가 tooProject**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group tooToDoApp*&lt;your_suffix>* > **Add Application Insights tooProject**.</span></span>
2. <span data-ttu-id="2e49a-202">Git 셸에서 커밋하고 GitHub에서 변경 내용을 tooyour 포크 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-202">In Git Shell, commit and push your changes tooyour fork in GitHub.</span></span> <span data-ttu-id="2e49a-203">다음 클라이언트 toorefresh 브라우저에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-203">Then, wait for clients toorefresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="2e49a-204">배포 된 hello 앱 변경 내용 tooproduction를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-204">Swap hello deployed app changes tooproduction:</span></span>

     <span data-ttu-id="2e49a-205">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="2e49a-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="2e49a-206">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a><span data-ttu-id="2e49a-207">슬롯 관련 태그 tooyour 클라이언트 응용 프로그램 메트릭을 추가 조사 하십시오:</span><span class="sxs-lookup"><span data-stu-id="2e49a-207">Investigate: Add slot-specific tags tooyour client app metrics</span></span>
<span data-ttu-id="2e49a-208">이 섹션에서는 구성한 hello 다양 한 배포 슬롯 toosend 슬롯 관련 원격 분석 toohello 같은 Application Insights 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-208">In this section, you will configure hello different deployment slots toosend slot-specific telemetry toohello same Application Insights resource.</span></span> <span data-ttu-id="2e49a-209">이러한 방식으로 원격 분석을 비교할 수 있습니다 다른 슬롯 (배포 환경) tooeasily 트래픽만 간에 데이터 앱 변경 내용 hello 효과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) tooeasily see hello effect of your app changes.</span></span> <span data-ttu-id="2e49a-210">At hello 동일한 시간을 계속할 수 있도록 toomonitor 프로덕션 응용 프로그램 필요에 따라 hello 나머지에서 hello 프로덕션 트래픽을 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-210">At hello same time, you can separate hello production traffic from hello rest so you can continue toomonitor your production app as needed.</span></span>

<span data-ttu-id="2e49a-211">클라이언트 동작에 데이터를 수집 하는 이후 [원격 분석 이니셜라이저 tooyour JavaScript 코드를 추가](../application-insights/app-insights-api-filtering-sampling.md) index.cshtml에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-211">Since you're gathering data on client behavior, you will [add a telemetry initializer tooyour JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="2e49a-212">서버 쪽 성능 tootest 하려는 경우 예를 들어 할 수 있는 마찬가지로 서버 코드에서 (참조 [사용자 지정 이벤트 및 메트릭을 대 한 Application Insights API](../application-insights/app-insights-api-custom-events-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-212">If you want tootest server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="2e49a-213">먼저 추가 하는 hello 코드 있게 되었습니다 hello 두 `//` 아래에 메모 hello JavaScript 블록 toohello를 추가한 `<heading>` 이전 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-213">First, add hello code bewteen hello two `//` comments below in hello JavaScript block that you added toohello `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="2e49a-214">이 이니셜라이저 코드는 hello `appInsights` 개체 tooadd hello 라는 사용자 지정 속성 `Environment` tooevery 부분의 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-214">This initializer code causes hello `appInsights` object tooadd hello a custom property called `Environment` tooevery piece of telemetry it sends.</span></span>
2. <span data-ttu-id="2e49a-215">다음으로 Azure에서 웹앱에 대해 이 사용자 지정 속성을 [슬롯 설정](web-sites-staged-publishing.md#AboutConfiguration) 에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="2e49a-216">toodo 명령을 Git 셸 세션에서 다음 실행된이, hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-216">toodo this, run hello following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="2e49a-217">프로젝트의 Web.config hello 이미 정의 되어 hello `environment` 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-217">hello Web.config in your project already defines hello `environment` app setting.</span></span> <span data-ttu-id="2e49a-218">이 설정을 사용 하 여 hello 응용 프로그램을 로컬로 테스트할 때 하면 메트릭이 태그로 지정 될 `VS Debugger`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-218">With this setting, when you test hello app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="2e49a-219">그러나 변경 내용을 tooAzure 푸시할 때 Azure는 고 hello를 사용 하 여 `environment` 사항과 대신 hello 웹 앱의 구성에서 설정 하는 응용 프로그램으로 태그 처리 될 `Production`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-219">However, when you push your changes tooAzure, Azure will find and use hello `environment` app setting in hello web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="2e49a-220">커밋 및 GitHub에서 코드 변경 내용을 tooyour 포크 강제 하 고 사용자가 toouse hello 새 앱 (toorefresh hello 브라우저 필요) 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-220">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="2e49a-221">Application Insights에서 새 속성 tooshow hello에 대 한 약 15 분을 차지 `MultiChannelToDo.Web` 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-221">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. <span data-ttu-id="2e49a-222">이제 toohello 이동 **사용자 지정 이벤트** 블레이드를 다시 및 필터에 메트릭 hello `Environment=Production`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-222">Now, go toohello **Custom events** blade again and filter hello metrics on `Environment=Production`.</span></span> <span data-ttu-id="2e49a-223">이 필터와 hello 새 사용자 지정 이벤트를 모두 hello 프로덕션에서 슬롯 수 toosee 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-223">You should now be able toosee all hello new custom events in hello production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="2e49a-224">Hello 클릭 **즐겨찾기** 단추 toosave hello 현재 메트릭 탐색기 설정을 toosomething 같은 **사용자 지정 이벤트: 프로덕션**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-224">Click hello **Favorites** button toosave hello current Metrics Explorer settings toosomething like **Custom events: Production**.</span></span> <span data-ttu-id="2e49a-225">나중에 이 뷰 및 배포 슬롯 뷰를 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="2e49a-226">더욱 강력한 분석의 경우 [Power BI로 Application Insights 리소스 통합](../application-insights/app-insights-export-power-bi.md)을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a><span data-ttu-id="2e49a-227">슬롯 관련 태그 tooyour 서버 응용 프로그램 메트릭 추가</span><span class="sxs-lookup"><span data-stu-id="2e49a-227">Add slot-specific tags tooyour server app metrics</span></span>
<span data-ttu-id="2e49a-228">다시 완결성에 대 한 hello 서버 쪽 앱을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-228">Again, for completeness you will set up hello server-side app.</span></span> <span data-ttu-id="2e49a-229">JavaScript 계측는 hello 클라이언트 앱에서는 달리 hello 서버 응용 프로그램에 대 한 슬롯 관련 태그.NET 코드를 계측 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-229">Unlike hello client app which is instrumented in JavaScript, slot-specific tags for hello server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="2e49a-230">*&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="2e49a-231">닫는 중괄호 네임 스페이스 hello 직전 아래 hello 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-231">Add hello code block below, just before hello closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="2e49a-232">Hello를 추가 하 여 hello 이름 확인 오류를 해결 `using` hello 파일의 시작 부분 toohello 아래 문:</span><span class="sxs-lookup"><span data-stu-id="2e49a-232">Correct hello name resolution errors by adding hello `using` statements below toohello beginning of hello file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="2e49a-233">Hello hello toohello 맨 아래에 코드 추가 `Application_Start()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="2e49a-233">Add hello code below toohello beginning of hello `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="2e49a-234">커밋 및 GitHub에서 코드 변경 내용을 tooyour 포크 강제 하 고 사용자가 toouse hello 새 앱 (toorefresh hello 브라우저 필요) 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-234">Commit and push your code changes tooyour fork on GitHub, and then wait for your users toouse hello new app (need toorefresh hello browser).</span></span> <span data-ttu-id="2e49a-235">Application Insights에서 새 속성 tooshow hello에 대 한 약 15 분을 차지 `MultiChannelToDo` 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-235">It takes about 15 minutes for hello new property tooshow up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="2e49a-236">업데이트: 베타 분기 설정</span><span class="sxs-lookup"><span data-stu-id="2e49a-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="2e49a-237">열기  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json 및 찾기 hello `appsettings` 리소스 (검색할 `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="2e49a-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find hello `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="2e49a-238">각 슬롯에 하나 씩 4개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="2e49a-239">각 `appsettings` 리소스에 추가 `"environment": "[parameters('slotName')]"` 앱 toohello 끝 설정 hello `properties` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting toohello end of hello `properties` array.</span></span> <span data-ttu-id="2e49a-240">쉼표 tooend hello 이전 줄 것을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-240">Don't forget tooend hello previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="2e49a-241">Hello 방금 추가한 `environment` hello 템플릿에서 tooall hello 슬롯을 설정 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-241">You have just added hello `environment` app setting tooall hello slots in hello template.</span></span>
3. <span data-ttu-id="2e49a-242">동일한 파일 hello 하 hello `slotconfignames` 리소스 (검색할 `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="2e49a-242">In hello same file, find hello `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="2e49a-243">각 앱에 하나 씩 2개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="2e49a-244">각 `slotconfignames` 리소스를 추가 `"environment"` hello toohello 끝 `appSettingNames` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-244">For each `slotconfignames` resource, add `"environment"` toohello end of hello `appSettingNames` array.</span></span> <span data-ttu-id="2e49a-245">쉼표 tooend hello 이전 줄 것을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-245">Don't forget tooend hello previous line with a comma.</span></span>

    <span data-ttu-id="2e49a-246">Hello 방금 변경한 `environment` 두 앱에 대 한 응용 프로그램 설정 스틱 tooits 제품의 배포 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-246">You have just made hello `environment` app setting stick tooits respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="2e49a-247">Git 셸 세션에서 다음 실행된 hello로 명령을 hello 동일한 리소스 그룹 접미사 이전에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-247">In your Git Shell session, run hello following commands with hello same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="2e49a-248">메시지가 지정 이전과 같은 SQL 데이터베이스 자격 증명 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-248">When prompted, specify hello same SQL database credentials as before.</span></span> <span data-ttu-id="2e49a-249">그런 다음 tooupdate hello 리소스 그룹으로 형식 때 요청 `Y`, 다음 `ENTER`합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-249">Then, when asked tooupdate hello resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="2e49a-250">Hello 스크립트 완료, hello 원본 리소스 그룹에 모든 리소스는 유지 되지만 "beta" 라는 새 슬롯은 내에 만든 hello로 동일 되 면 hello 시작 부분에서 만든 hello "스테이징" 슬롯으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-250">Once hello script finishes, all your resources in hello original resource group are retained, but a new slot named "beta" is created in it with hello same configuration as hello "Staging" slot that was created in hello beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2e49a-251">이 방법으로 서로 다른 배포 환경에서 hello 메서드 간에 차이가 있는 [Azure 앱 서비스와 Agile 소프트웨어 개발](app-service-agile-software-development.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-251">This method of creating different deployment environments is different from hello method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="2e49a-252">여기에서 배포 슬롯을 사용하여 배포 환경을 만든 반면 저기서는 리소스 그룹을 사용하여 배포 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="2e49a-253">배포 환경 리소스 그룹으로 관리 하면 tookeep hello 프로덕션 환경 off-limits toodevelopers, 아니라 슬롯을 쉽게 수행할 수 있는 프로덕션 환경에서 테스트 하는 쉬운 toodo 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-253">Managing deployment environments with resource groups enables you tookeep hello production environment off-limits toodevelopers, but it's not easy toodo testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="2e49a-254">또한 원하는 경우 실행하여 알파 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="2e49a-255">이 자습서에서는 베타 앱을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-toohello-beta-app"></a><span data-ttu-id="2e49a-256">업데이트: 업데이트 toohello 베타 앱 푸시</span><span class="sxs-lookup"><span data-stu-id="2e49a-256">Update: Push your updates toohello beta app</span></span>
<span data-ttu-id="2e49a-257">원하는 tooimprove tooyour 응용 프로그램을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-257">Back tooyour app that you want tooimprove.</span></span>

1. <span data-ttu-id="2e49a-258">베타 분기에서 지금 여러분이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="2e49a-259"> *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, 찾기 hello `<li>` 태그를 지정 하 고 hello 추가 `style="cursor:pointer"` 특성을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find hello `<li>` tag and add hello `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="2e49a-260">커밋하고 tooAzure 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="2e49a-260">commit and push tooAzure.</span></span>
4. <span data-ttu-id="2e49a-261">Hello 변경 이제에 반영 되도록 hello 베타 슬롯 toohttp://todoapp 이동 하 여 확인*&lt;your_suffix >*-beta.azurewebsites.net/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-261">Verify that hello change is now reflected in hello beta slot by navigating toohttp://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="2e49a-262">Hello 변경 아직 브라우저 tooget hello 새 javascript 코드를 새로 고치려면 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-262">If you don't see hello change yet, refresh your browser tooget hello new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="2e49a-263">Hello 베타 슬롯에서 실행 되는 변경 내용을가지고 준비 tooperform 플 라이팅 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-263">Now that you have your change running in hello beta slot, you are ready tooperform a flighting deployment.</span></span>

## <a name="validate-route-traffic-toohello-beta-app"></a><span data-ttu-id="2e49a-264">유효성 검사: 경로 트래픽 toohello 베타 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2e49a-264">Validate: Route traffic toohello beta app</span></span>
<span data-ttu-id="2e49a-265">이 섹션에서는 트래픽 toohello 베타 응용 프로그램을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-265">In this section, you will route traffic toohello beta app.</span></span> <span data-ttu-id="2e49a-266">데모의 명확성을 위해 tooroute hello 사용자 트래픽 tooit의 상당 부분이 겠 군요.</span><span class="sxs-lookup"><span data-stu-id="2e49a-266">For sake of clarity of demonstration, you're going tooroute a significant portion of hello user traffic tooit.</span></span> <span data-ttu-id="2e49a-267">실제로 hello 소통량 원하는 tooroute 상황에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-267">In reality, hello amount of traffic you want tooroute will depend on your specific situation.</span></span> <span data-ttu-id="2e49a-268">예를 들어, microsoft.com의 hello 규모에 사이트가 있는 경우 순서 toogain 유용한 데이터의 총 트래픽의 1% 보다 작은 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-268">For example, if your site is at hello scale of microsoft.com, then you may need less than one percent of your total traffic in order toogain useful data.</span></span>

1. <span data-ttu-id="2e49a-269">Git 셸 세션에서 실행 명령을 tooroute 다음 hello hello 프로덕션 트래픽 toohello 베타 슬롯의 절반 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-269">In your Git Shell session, run hello following commands tooroute half of hello production traffic toohello beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="2e49a-270">hello `ReroutePercentage=50` 속성 지정 hello 프로덕션 트래픽의 50% 라우트된 toohello 베타 앱의 URL (hello로 지정 된 `ActionHostName` 속성).</span><span class="sxs-lookup"><span data-stu-id="2e49a-270">hello `ReroutePercentage=50` property specifies that 50% of hello production traffic will be routed toohello beta app's URL (specified by hello `ActionHostName` property).</span></span>
2. <span data-ttu-id="2e49a-271">이제 toohttp://ToDoApp 이동*&lt;your_suffix >*. azurewebsites.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-271">Now navigate toohttp://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="2e49a-272">hello 트래픽의 50%를 리디렉션된 toohello 베타 슬롯 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-272">50% of hello traffic should now be redirected toohello beta slot.</span></span>
3. <span data-ttu-id="2e49a-273">Application Insights 리소스에서 hello 메트릭을 기준으로 필터링 환경 = "beta"입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-273">In your Application Insights resource, filter hello metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="2e49a-274">다른 즐겨찾기로이 필터링 된 보기를 저장 하는 경우 프로덕션 및 베타 뷰 간의 hello 메트릭 탐색기 보기 쉽게 전환할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-274">If you save this filtered view as another favorite, then you can easily flip hello metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="2e49a-275">다음과 유사한 toohello 다음을 참조 하는 Application Insights에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-275">Suppose in Application Insights you see something similar toohello following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="2e49a-276">뿐만 아니라이 표시 hello에 대 한 많은 자세한 클릭 된다고 `<li>` 태그 toobe의 클릭 급증 하기 때문에 결과적으로 하지만 `<li>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-276">Not only is this showing that there are many more clicks on hello `<li>` tags, but there seems toobe a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="2e49a-277">다음 사용자를 새 hello 가져 왔어 있는지을 완료할 수 있습니다 `<li>` 태그 클릭할 수 및는 이제 hello 응용 프로그램의 모든 이전에 완료 된 작업의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-277">You can then conclude that people have discovered hello new `<li>` tags are clickable and are now clearing all their previously-completed tasks in hello app.</span></span>

<span data-ttu-id="2e49a-278">플 라이팅 배포의 hello 데이터에 따라 새 UI를 프로덕션에 대 한 준비가 되었는지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-278">Based on hello data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="2e49a-279">바로 사용: 새 코드를 프로덕션으로 이동</span><span class="sxs-lookup"><span data-stu-id="2e49a-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="2e49a-280">사용자는 이제 준비 toomove 업데이트 tooproduction 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-280">You're now ready toomove your update tooproduction.</span></span> <span data-ttu-id="2e49a-281">유용은 이제는 업데이트의 유효성을 이미 알고 있는 *전에* tooproduction 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-281">What's great is that now you know that your update has already been validated *before* it is pushed tooproduction.</span></span> <span data-ttu-id="2e49a-282">이제 안심하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="2e49a-283">클라이언트 응용 프로그램 업데이트 toohello AngularJS를 보낸 후 hello 클라이언트 쪽 코드만 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-283">Since you made an update toohello AngularJS client app, you only validated hello client-side code.</span></span> <span data-ttu-id="2e49a-284">Toomake 변경 toohello 백 엔드 웹 API 앱 인 경우 쉽고 마찬가지로 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-284">If you were toomake changes toohello back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="2e49a-285">Git 셸에서 hello 다음 명령을 실행 하 여 hello 트래픽 라우팅 규칙을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-285">In Git Shell, remove hello traffic routing rule by running hello following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="2e49a-286">Hello Git 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-286">Run hello Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="2e49a-287">몇 분 정도 hello에 대 한 새로운 배포 toobe toohello 슬롯을 코딩 한 다음 시작 http://ToDoApp 기다리세요*&lt;your_suffix >*-hello 스테이징에서 새 업데이트 hello staging.azurewebsites.net tooverify 준비 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-287">Wait for a few minutes for hello new code toobe deployed toohello staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net tooverify that hello new update is warmed up in hello staging slot.</span></span> <span data-ttu-id="2e49a-288">분기의 마스터 분기는 해당 hello 연결 toohello 준비 기억 응용 프로그램의 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-288">Remember that hello your fork's master branch is linked toohello staging slot of your app.</span></span>
4. <span data-ttu-id="2e49a-289">이제 프로덕션 환경으로 슬롯을 준비 하는 hello를 교체</span><span class="sxs-lookup"><span data-stu-id="2e49a-289">Now, swap hello staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="2e49a-290">요약</span><span class="sxs-lookup"><span data-stu-id="2e49a-290">Summary</span></span>
<span data-ttu-id="2e49a-291">Azure 앱 서비스 쉽게 소규모 toomedium 기업 tootest에 대 한 고객 지향 앱 프로덕션 환경에서 어떤 큰 기업에서 일반적으로 수행 되 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-291">Azure App Service makes it easy for small- toomedium-sized businesses tootest their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="2e49a-292">다행히이 자습서가 제공한 hello toobring 함께 응용 프로그램 서비스 및 Application Insights toomake 가능한 플 라이팅 배포 및 기타 테스트 프로덕션 시나리오 DevOps 세계에 필요한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="2e49a-292">Hopefully, this tutorial has given you hello knowledge you need toobring together App Service and Application Insights toomake possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="2e49a-293">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2e49a-293">More resources</span></span>
* [<span data-ttu-id="2e49a-294">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="2e49a-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="2e49a-295">Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="2e49a-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="2e49a-296">Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포</span><span class="sxs-lookup"><span data-stu-id="2e49a-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="2e49a-297">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="2e49a-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="2e49a-298">JSONLint-hello JSON 유효성 검사기</span><span class="sxs-lookup"><span data-stu-id="2e49a-298">JSONLint - hello JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="2e49a-299">Git 분기-기본 분기 및 병합</span><span class="sxs-lookup"><span data-stu-id="2e49a-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="2e49a-300">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e49a-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2e49a-301">프로젝트 Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="2e49a-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
