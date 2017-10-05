---
title: "Azure에서 Bottle을 사용하는 Python 웹앱"
description: "Azure 앱 서비스 웹앱에서 Python 웹앱을 실행하는 방법을 소개하는 자습서입니다."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="d14da-103">Azure에서 Bottle을 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d14da-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="d14da-104">이 자습서에서는 Azure 앱 서비스 웹앱에서 Python을 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="d14da-105">웹앱은 제한된 무료 호스팅 및 신속한 배포 기능을 제공하며, Python을 사용할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="d14da-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="d14da-106">앱이 증가하면 유료 호스팅으로 전환하여 다른 모든 Azure 서비스와 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="d14da-107">먼저 Bottle 웹 프레임워크([Django](web-sites-python-create-deploy-django-app.md) 및 [Flask](web-sites-python-create-deploy-flask-app.md)는 이 자습서의 다른 버전 참조)를 사용하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="d14da-108">Azure 마켓플레이스에서 웹앱을 만들고, Git 배포를 설치하고, 리포지토리를 로컬로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="d14da-109">그런 다음 웹앱을 로컬로 실행하고, 변경한 다음, 이를 커밋하여 [Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d14da-110">이 자습서에서는 Windows 또는 Mac/Linux에서 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="d14da-111">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d14da-112">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d14da-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d14da-113">Prerequisites</span></span>
* <span data-ttu-id="d14da-114">Windows, Mac 또는 Linux</span><span class="sxs-lookup"><span data-stu-id="d14da-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="d14da-115">Python 2.7 또는 3.4</span><span class="sxs-lookup"><span data-stu-id="d14da-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="d14da-116">setuptools, pip, virtualenv(Python 2.7 전용)</span><span class="sxs-lookup"><span data-stu-id="d14da-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="d14da-117">Git</span><span class="sxs-lookup"><span data-stu-id="d14da-117">Git</span></span>
* <span data-ttu-id="d14da-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio](PTVS) - 참고: 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="d14da-119">**참고**: 현재 Python 프로젝트에서는 TFS 게시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="d14da-120">Windows</span><span class="sxs-lookup"><span data-stu-id="d14da-120">Windows</span></span>
<span data-ttu-id="d14da-121">Python 2.7 또는 3.4(32비트)를 아직 설치하지 않은 경우 웹 플랫폼 설치 관리자를 사용하여 [Azure SDK for Python 2.7] 또는 [Azure SDK for Python 3.4]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="d14da-122">그러면 32비트 버전의 Python, setuptools, pip, virtualenv 등(32비트 Python은 Azure 호스트 컴퓨터에 설치되는 버전)이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="d14da-123">또는 [python.org]에서 Python을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="d14da-124">Git의 경우 [Windows용 Git] 또는 [Windows용 GitHub]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="d14da-125">Visual Studio를 사용하는 경우 통합 Git 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="d14da-126">또한 [Python Tools 2.2 for Visual Studio]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="d14da-127">이는 선택 사항이지만 [Visual Studio](무료 Visual Studio Community 2013 또는 Visual Studio Express 2013 for Web 포함)가 있으면 Python IDE가 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="d14da-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="d14da-128">Mac/Linux</span></span>
<span data-ttu-id="d14da-129">Python 및 Git를 이미 설치했어야 하지만 Python 버전은 2.7 또는 3.4여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="d14da-130">Azure 포털에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d14da-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="d14da-131">앱을 만드는 첫 번째 단계는 [Azure 포털](https://portal.azure.com)을 통해 웹앱을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="d14da-132">Azure 포털에 로그인하여 왼쪽 아래에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="d14da-133">검색 상자에 "python"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="d14da-134">검색 결과에서 선택 **Bottle**을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="d14da-135">새 Bottle 앱을 구성(예: 새 앱 서비스 계획 만들기)하고 해당 앱의 새 리소스 그룹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="d14da-136">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="d14da-137">[Azure 앱 서비스에 로컬 Git 배포](app-service-deploy-local-git.md)의 지침에 따라 새로 만든 웹앱에 대한 Git 게시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="d14da-138">응용 프로그램 개요</span><span class="sxs-lookup"><span data-stu-id="d14da-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="d14da-139">Git 리포지토리 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="d14da-139">Git repository contents</span></span>
<span data-ttu-id="d14da-140">다음은 초기 Git 리포지토리에 표시되는 파일의 개요입니다(다음 섹션에서 복제).</span><span class="sxs-lookup"><span data-stu-id="d14da-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="d14da-141">응용 프로그램의 기본 소스.</span><span class="sxs-lookup"><span data-stu-id="d14da-141">Main sources for the application.</span></span> <span data-ttu-id="d14da-142">마스터 레이아웃과 함께 3페이지(index, about, contact)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="d14da-143">정적 콘텐츠와 스크립트에는 bootstrap, jquery, modernizr 및 respond가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="d14da-144">로컬 개발 서버 지원.</span><span class="sxs-lookup"><span data-stu-id="d14da-144">Local development server support.</span></span> <span data-ttu-id="d14da-145">이를 사용하여 응용 프로그램을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="d14da-146">[Python Tools for Visual Studio]에서 사용되는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="d14da-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="d14da-147">가상 환경용 IIS 프록시 및 PTVS 원격 디버깅 지원</span><span class="sxs-lookup"><span data-stu-id="d14da-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="d14da-148">이 응용 프로그램에 필요한 외부 패키지.</span><span class="sxs-lookup"><span data-stu-id="d14da-148">External packages needed by this application.</span></span> <span data-ttu-id="d14da-149">배포 스크립트는 이 파일에 나열된 패키지를 pip 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="d14da-150">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="d14da-150">IIS configuration files.</span></span> <span data-ttu-id="d14da-151">배포 스크립트에서는 적절한 web.x.y.config를 사용하며 이를 web.config로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="d14da-152">선택적 파일 - 배포 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d14da-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="d14da-153">선택적 파일 - Python 런타임</span><span class="sxs-lookup"><span data-stu-id="d14da-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="d14da-154">서버의 추가 파일</span><span class="sxs-lookup"><span data-stu-id="d14da-154">Additional files on server</span></span>
<span data-ttu-id="d14da-155">일부 파일은 서버에 있지만 git 리포지토리에 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="d14da-156">이러한 파일은 배포 스크립트를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="d14da-157">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="d14da-157">IIS configuration file.</span></span> <span data-ttu-id="d14da-158">모든 배포에서 web.x.y.config를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="d14da-159">Python 가상 환경.</span><span class="sxs-lookup"><span data-stu-id="d14da-159">Python virtual environment.</span></span> <span data-ttu-id="d14da-160">호환되는 가상 환경이 웹앱에 없는 경우 배포 중에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="d14da-161">requirements.txt에 나열된 패키지가 pip 설치되지만 패키지가 이미 설치된 경우에는 pip에서 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="d14da-162">다음 세 개의 섹션에서는 세 가지 환경에서 웹앱 배포를 계속 진행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="d14da-163">Windows, Python Tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="d14da-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="d14da-164">Windows, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="d14da-164">Windows, with command line</span></span>
* <span data-ttu-id="d14da-165">Mac/Linux, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="d14da-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="d14da-166">웹앱 배포 - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d14da-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="d14da-167">리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="d14da-167">Clone the repository</span></span>
<span data-ttu-id="d14da-168">먼저 Azure 포털에서 제공된 URL을 사용하여 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="d14da-169">자세한 내용은 [Azure 앱 서비스에 로컬 Git 배포](app-service-deploy-local-git.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d14da-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="d14da-170">리포지토리의 루트에 포함된 솔루션 파일(.sln)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="d14da-171">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="d14da-171">Create virtual environment</span></span>
<span data-ttu-id="d14da-172">이제 로컬 개발을 위한 가상 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="d14da-173">**Python Environments**를 마우스 오른쪽 단추로 클릭하고 **Add Virtual Environment...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="d14da-174">환경 이름이 `env`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="d14da-175">기본 해석기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-175">Select the base interpreter.</span></span> <span data-ttu-id="d14da-176">웹앱에 대해 선택(runtime.txt 또는 Azure 포털에서 웹앱의 **응용 프로그램 설정** 블레이드를 통해)된 Python의 동일한 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="d14da-177">패키지를 다운로드하여 설치하는 옵션이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="d14da-178">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-178">Click **Create**.</span></span> <span data-ttu-id="d14da-179">가상 환경이 만들어지고 requirements.txt에 나열된 종속성이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="d14da-180">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="d14da-180">Run using development server</span></span>
<span data-ttu-id="d14da-181">F5 키를 눌러 디버깅을 시작하면 웹 브라우저에서 로컬로 실행되는 페이지가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="d14da-182">원본에서 중단점을 설정하고, 조사식 창을 사용하는 등의 작업을 수행할 수 있습니다. 여러 기능에 대한 자세한 내용은 [Python Tools for Visual Studio 설명서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d14da-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="d14da-183">변경 작업</span><span class="sxs-lookup"><span data-stu-id="d14da-183">Make changes</span></span>
<span data-ttu-id="d14da-184">이제 응용 프로그램 소스 및/또는 템플릿을 변경하여 실험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="d14da-185">변경 내용을 테스트한 후 Git 리포지토리에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="d14da-186">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d14da-186">Install more packages</span></span>
<span data-ttu-id="d14da-187">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d14da-188">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-188">You can install additional packages using pip.</span></span> <span data-ttu-id="d14da-189">패키지를 설치하려면 가상 환경을 마우스 오른쪽 단추로 클릭하고 **Install Python Package**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="d14da-190">예를 들어 Azure 저장소, 서비스 버스 및 기타 Azure 서비스에 대한 액세스를 제공하는 Azure SDK for Python을 설치하려면 `azure`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="d14da-191">가상 환경을 마우스 오른쪽 단추로 클릭하고 **Generate requirements.txt** 를 선택하여 requirements.txt를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="d14da-192">그런 다음 requirements.txt의 변경 내용을 Git 리포지토리에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="d14da-193">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="d14da-193">Deploy to Azure</span></span>
<span data-ttu-id="d14da-194">배포를 트리거하려면 **Sync** 또는 **Push**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="d14da-195">Sync는 밀어넣기와 끌어오기를 둘 다 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="d14da-196">첫 배포에서는 가상 환경 만들기, 패키지 설치 등의 작업이 수행되므로 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="d14da-197">Visual Studio에는 배포 진행률이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="d14da-198">출력을 검토하려면 [문제 해결 - 배포](#troubleshooting-deployment)섹션을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="d14da-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="d14da-199">Azure URL로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="d14da-200">웹앱 배포 - Windows - 명령줄</span><span class="sxs-lookup"><span data-stu-id="d14da-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="d14da-201">리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="d14da-201">Clone the repository</span></span>
<span data-ttu-id="d14da-202">먼저 Azure 포털에서 제공된 URL을 사용하여 리포지토리를 복제하고 Azure 리포지토리를 원격으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="d14da-203">자세한 내용은 [Azure 앱 서비스에 로컬 Git 배포](app-service-deploy-local-git.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d14da-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d14da-204">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="d14da-204">Create virtual environment</span></span>
<span data-ttu-id="d14da-205">개발을 위해 새 가상 환경을 만듭니다(리포지토리에 추가 안 함).</span><span class="sxs-lookup"><span data-stu-id="d14da-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="d14da-206">Python의 가상 환경은 재할당할 수 없으므로 응용 프로그램에서 작업하는 모든 개발자가 각자 로컬로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="d14da-207">웹앱에 대해 선택(runtime.txt 또는 Azure 포털에서 웹앱에 대한 응용 프로그램 설정 블레이드를 통해)된 Python의 동일한 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="d14da-208">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="d14da-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="d14da-209">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="d14da-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="d14da-210">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-210">Install any external packages required by your application.</span></span> <span data-ttu-id="d14da-211">리포지토리의 루트에 있는 requirements.txt 파일을 사용하여 가상 환경에 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d14da-212">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="d14da-212">Run using development server</span></span>
<span data-ttu-id="d14da-213">다음 명령을 사용하여 개발 서버에서 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="d14da-214">콘솔에 서버에서 수신 대기하는 URL 및 포트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="d14da-215">그러면 이 URL로 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d14da-216">변경 작업</span><span class="sxs-lookup"><span data-stu-id="d14da-216">Make changes</span></span>
<span data-ttu-id="d14da-217">이제 응용 프로그램 소스 및/또는 템플릿을 변경하여 실험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="d14da-218">변경 내용을 테스트한 후 Git 리포지토리에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d14da-219">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d14da-219">Install more packages</span></span>
<span data-ttu-id="d14da-220">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d14da-221">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-221">You can install additional packages using pip.</span></span> <span data-ttu-id="d14da-222">예를 들어 Azure 저장소, 서비스 버스 및 기타 Azure 서비스에 대한 액세스를 제공하는 Azure SDK for Python을 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="d14da-223">requirements.txt를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="d14da-224">변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="d14da-225">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="d14da-225">Deploy to Azure</span></span>
<span data-ttu-id="d14da-226">배포를 트리거하려면 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="d14da-227">가상 환경 생성, 패키지 설치, web.config 생성 등 배포 스크립트의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d14da-228">Azure URL로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="d14da-229">웹앱 배포 - Mac/Linux - 명령줄</span><span class="sxs-lookup"><span data-stu-id="d14da-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="d14da-230">리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="d14da-230">Clone the repository</span></span>
<span data-ttu-id="d14da-231">먼저 Azure 포털에서 제공된 URL을 사용하여 리포지토리를 복제하고 Azure 리포지토리를 원격으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="d14da-232">자세한 내용은 [Azure 앱 서비스에 로컬 Git 배포](app-service-deploy-local-git.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d14da-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="d14da-233">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="d14da-233">Create virtual environment</span></span>
<span data-ttu-id="d14da-234">개발을 위해 새 가상 환경을 만듭니다(리포지토리에 추가 안 함).</span><span class="sxs-lookup"><span data-stu-id="d14da-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="d14da-235">Python의 가상 환경은 재할당할 수 없으므로 응용 프로그램에서 작업하는 모든 개발자가 각자 로컬로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="d14da-236">웹앱에 대해 선택(runtime.txt 또는 Azure 포털에서 웹앱의 응용 프로그램 설정 블레이드를 통해)된 Python의 동일한 버전을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="d14da-237">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="d14da-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="d14da-238">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="d14da-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="d14da-239">또는 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="d14da-239">or pyvenv env</span></span>

<span data-ttu-id="d14da-240">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-240">Install any external packages required by your application.</span></span> <span data-ttu-id="d14da-241">리포지토리의 루트에 있는 requirements.txt 파일을 사용하여 가상 환경에 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="d14da-242">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="d14da-242">Run using development server</span></span>
<span data-ttu-id="d14da-243">다음 명령을 사용하여 개발 서버에서 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="d14da-244">콘솔에 서버에서 수신 대기하는 URL 및 포트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="d14da-245">그러면 이 URL로 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="d14da-246">변경 작업</span><span class="sxs-lookup"><span data-stu-id="d14da-246">Make changes</span></span>
<span data-ttu-id="d14da-247">이제 응용 프로그램 소스 및/또는 템플릿을 변경하여 실험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="d14da-248">변경 내용을 테스트한 후 Git 리포지토리에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="d14da-249">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d14da-249">Install more packages</span></span>
<span data-ttu-id="d14da-250">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="d14da-251">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-251">You can install additional packages using pip.</span></span> <span data-ttu-id="d14da-252">예를 들어 Azure 저장소, 서비스 버스 및 기타 Azure 서비스에 대한 액세스를 제공하는 Azure SDK for Python을 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="d14da-253">requirements.txt를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="d14da-254">변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="d14da-255">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="d14da-255">Deploy to Azure</span></span>
<span data-ttu-id="d14da-256">배포를 트리거하려면 변경 내용을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="d14da-257">가상 환경 생성, 패키지 설치, web.config 생성 등 배포 스크립트의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="d14da-258">Azure URL로 이동하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d14da-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="d14da-259">문제 해결 - 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="d14da-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="d14da-260">문제 해결 - 가상 환경</span><span class="sxs-lookup"><span data-stu-id="d14da-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="d14da-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d14da-261">Next Steps</span></span>
<span data-ttu-id="d14da-262">Bottle 및 Python Tools for Visual Studio에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d14da-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="d14da-263">[Bottle 설명서]</span><span class="sxs-lookup"><span data-stu-id="d14da-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="d14da-264">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="d14da-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="d14da-265">Azure 테이블 저장소 및 MongoDB에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d14da-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="d14da-266">[Azure의 Bottle 및 MongoDB와 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d14da-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="d14da-267">[Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="d14da-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d14da-268">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="d14da-268">What's changed</span></span>
* <span data-ttu-id="d14da-269">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d14da-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="d14da-270">[Azure의 Bottle 및 MongoDB와 Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="d14da-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="d14da-271">[Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="d14da-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="d14da-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="d14da-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="d14da-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="d14da-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="d14da-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="d14da-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="d14da-275">[Windows용 Git]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="d14da-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="d14da-276">[Windows용 GitHub]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="d14da-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="d14da-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="d14da-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="d14da-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="d14da-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="d14da-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="d14da-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="d14da-280">[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="d14da-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="d14da-281">[Bottle 설명서]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="d14da-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

