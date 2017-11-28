---
title: "Azure에서 Bottle로 aaaPython 웹 앱"
description: "Toorunning Azure 앱 서비스 웹 앱에서 Python 웹 응용 프로그램을 소개 하는 자습서입니다."
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
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="3e2f4-103">Azure에서 Bottle을 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2f4-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="3e2f4-104">이 자습서에서는 Azure 앱 서비스 웹 앱에서 Python 실행 tooget을 시작 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="3e2f4-105">웹앱은 제한된 무료 호스팅 및 신속한 배포 기능을 제공하며, Python을 사용할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="3e2f4-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="3e2f4-106">응용 프로그램 증가, toopaid 호스팅 전환할 수 있습니다 및 모든와 통합할 수 있습니다 때 hello 다른 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="3e2f4-107">Hello Bottle 웹 프레임 워크를 사용 하 여 웹 앱을 만들 (참조에 대 한이 자습서의 대체 버전 [Django](web-sites-python-create-deploy-django-app.md) 및 [플라스](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="3e2f4-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="3e2f4-108">Hello 웹 응용 프로그램 hello Azure Marketplace에서에서, Git 배포 설정 만들고 hello 로컬 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="3e2f4-109">그런 다음는 hello 웹 응용 프로그램을 로컬로 실행, 변경, 커밋 너무 푸시[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="3e2f4-110">자습서에서는 어떻게 hello toodo Windows 또는 Mac/Linux에서이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="3e2f4-111">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3e2f4-112">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3e2f4-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e2f4-113">Prerequisites</span></span>
* <span data-ttu-id="3e2f4-114">Windows, Mac 또는 Linux</span><span class="sxs-lookup"><span data-stu-id="3e2f4-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="3e2f4-115">Python 2.7 또는 3.4</span><span class="sxs-lookup"><span data-stu-id="3e2f4-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="3e2f4-116">setuptools, pip, virtualenv(Python 2.7 전용)</span><span class="sxs-lookup"><span data-stu-id="3e2f4-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="3e2f4-117">Git</span><span class="sxs-lookup"><span data-stu-id="3e2f4-117">Git</span></span>
* <span data-ttu-id="3e2f4-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio](PTVS) - 참고: 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="3e2f4-119">**참고**: 현재 Python 프로젝트에서는 TFS 게시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="3e2f4-120">Windows</span><span class="sxs-lookup"><span data-stu-id="3e2f4-120">Windows</span></span>
<span data-ttu-id="3e2f4-121">Python 2.7 또는 3.4(32비트)를 아직 설치하지 않은 경우 웹 플랫폼 설치 관리자를 사용하여 [Azure SDK for Python 2.7] 또는 [Azure SDK for Python 3.4]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="3e2f4-122">이 Python, setuptools, pip, virtualenv 등의 (32 비트 Python hello Azure 호스트 컴퓨터에 설치 된 항목은) hello 32 비트 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="3e2f4-123">또는 [python.org]에서 Python을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="3e2f4-124">Git의 경우 [Windows용 Git] 또는 [Windows용 GitHub]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="3e2f4-125">Visual Studio를 사용 하는 경우 통합 hello Git 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="3e2f4-126">또한 [Python Tools 2.2 for Visual Studio]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="3e2f4-127">이 속성은 선택적 있는 경우 [Visual Studio]hello를 포함 하 여 가능한 Visual Studio Community 2013 또는 Visual Studio Express 2013 for Web 차례로 이렇게 하면 한 훌륭한 인 Python IDE 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="3e2f4-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="3e2f4-128">Mac/Linux</span></span>
<span data-ttu-id="3e2f4-129">Python 및 Git를 이미 설치했어야 하지만 Python 버전은 2.7 또는 3.4여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="3e2f4-130">Hello Azure 포털에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2f4-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="3e2f4-131">hello 앱을 만드는 첫 번째 단계는 hello 통해 toocreate hello 웹 앱 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="3e2f4-132">Hello Azure 포털에 로그인 하 고 hello 클릭 **새로** hello 왼쪽된 하단에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="3e2f4-133">Hello 검색 상자에 "python"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="3e2f4-134">Hello 검색 결과에서 선택 **Bottle**, 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="3e2f4-135">Hello 새 Bottle 같은 앱에 대 한 새 앱 서비스 계획을 만들고 새 리소스 그룹을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="3e2f4-136">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="3e2f4-137">Hello 지침에 따라 새로 만든된 웹 앱에 대 한 Git 게시를 구성 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="3e2f4-138">응용 프로그램 개요</span><span class="sxs-lookup"><span data-stu-id="3e2f4-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="3e2f4-139">Git 리포지토리 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="3e2f4-139">Git repository contents</span></span>
<span data-ttu-id="3e2f4-140">Hello 다음 섹션에서 복제 hello 초기 Git 리포지토리에 있습니다 hello 파일의 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="3e2f4-141">Hello 응용 프로그램에 대 한 주 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-141">Main sources for hello application.</span></span> <span data-ttu-id="3e2f4-142">마스터 레이아웃과 함께 3페이지(index, about, contact)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="3e2f4-143">정적 콘텐츠와 스크립트에는 bootstrap, jquery, modernizr 및 respond가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="3e2f4-144">로컬 개발 서버 지원.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-144">Local development server support.</span></span> <span data-ttu-id="3e2f4-145">로컬이 toorun hello 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="3e2f4-146">[Python Tools for Visual Studio]에서 사용되는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="3e2f4-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="3e2f4-147">가상 환경용 IIS 프록시 및 PTVS 원격 디버깅 지원</span><span class="sxs-lookup"><span data-stu-id="3e2f4-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="3e2f4-148">이 응용 프로그램에 필요한 외부 패키지.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-148">External packages needed by this application.</span></span> <span data-ttu-id="3e2f4-149">hello 배포 스크립트에는이 파일에 나열 된 설치 hello 패키지 pip 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="3e2f4-150">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-150">IIS configuration files.</span></span> <span data-ttu-id="3e2f4-151">hello 배포 스크립트는 hello 적절 한 web.x.y.config 사용 되 고 web.config로 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="3e2f4-152">선택적 파일 - 배포 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3e2f4-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="3e2f4-153">선택적 파일 - Python 런타임</span><span class="sxs-lookup"><span data-stu-id="3e2f4-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="3e2f4-154">서버의 추가 파일</span><span class="sxs-lookup"><span data-stu-id="3e2f4-154">Additional files on server</span></span>
<span data-ttu-id="3e2f4-155">일부 파일 hello 서버에 존재 하지만 toohello git 리포지토리를 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="3e2f4-156">Hello 배포 스크립트에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="3e2f4-157">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-157">IIS configuration file.</span></span> <span data-ttu-id="3e2f4-158">모든 배포에서 web.x.y.config를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="3e2f4-159">Python 가상 환경.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-159">Python virtual environment.</span></span> <span data-ttu-id="3e2f4-160">호환 되는 가상 환경 hello 웹 응용 프로그램에 존재 하지 않는 경우 배포 중에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="3e2f4-161">Requirements.txt에 나열 된 패키지를 설치 하는 pip는 pip는 hello 패키지가 이미 설치 되어 있는 경우 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="3e2f4-162">hello 다음 3 설명 어떻게 hello로 tooproceed 웹 3 다양 한 환경에서 응용 프로그램 개발:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="3e2f4-163">Windows, Python Tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="3e2f4-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="3e2f4-164">Windows, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="3e2f4-164">Windows, with command line</span></span>
* <span data-ttu-id="3e2f4-165">Mac/Linux, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="3e2f4-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="3e2f4-166">웹앱 배포 - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e2f4-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="3e2f4-167">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="3e2f4-167">Clone hello repository</span></span>
<span data-ttu-id="3e2f4-168">첫째, hello Azure 포털에서 제공 하는 hello url를 사용 하 여 hello 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="3e2f4-169">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="3e2f4-170">Hello 저장소의 hello 루트에 포함 된 hello 솔루션 파일 (.sln)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="3e2f4-171">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2f4-171">Create virtual environment</span></span>
<span data-ttu-id="3e2f4-172">이제 로컬 개발을 위한 가상 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="3e2f4-173">**Python Environments**를 마우스 오른쪽 단추로 클릭하고 **Add Virtual Environment...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="3e2f4-174">Hello 환경의 hello 이름 인지 확인 `env`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="3e2f4-175">Hello 기본 인터프리터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-175">Select hello base interpreter.</span></span> <span data-ttu-id="3e2f4-176">Toouse hello 동일한 버전의 웹 앱에 대해 선택 된 Python 있는지 확인 (runtime.txt 또는 hello **응용 프로그램 설정** hello Azure 포털에서에서 웹 응용 프로그램의 블레이드)입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="3e2f4-177">Hello 옵션 toodownload 및 설치 패키지 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="3e2f4-178">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-178">Click **Create**.</span></span> <span data-ttu-id="3e2f4-179">이 hello 가상 환경을 만들고 requirements.txt에 나열 된 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="3e2f4-180">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="3e2f4-180">Run using development server</span></span>
<span data-ttu-id="3e2f4-181">디버깅, 키를 눌러 F5 toostart 및 웹 브라우저가 자동으로 toohello 페이지가 열립니다 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="3e2f4-182">Hello 소스, 사용 하 여 hello 조사식 창에서 중단점을 설정할 수 있습니다. Hello 참조 [Python Tools for Visual Studio 설명서] 대 한 자세한 내용은 hello 다양 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="3e2f4-183">변경 작업</span><span class="sxs-lookup"><span data-stu-id="3e2f4-183">Make changes</span></span>
<span data-ttu-id="3e2f4-184">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="3e2f4-185">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="3e2f4-186">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3e2f4-186">Install more packages</span></span>
<span data-ttu-id="3e2f4-187">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="3e2f4-188">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-188">You can install additional packages using pip.</span></span> <span data-ttu-id="3e2f4-189">선택 및 hello 가상 환경에서 tooinstall 패키지를 마우스 오른쪽 단추로 클릭 **Python 패키지 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="3e2f4-190">예를 들어 tooinstall hello 액세스할 수 있도록 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스를 입력 하는 Python 용 Azure SDK `azure`:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="3e2f4-191">Hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **requirements.txt 생성** tooupdate requirements.txt 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="3e2f4-192">그런 다음 커밋 hello toorequirements.txt toohello Git 리포지토리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="3e2f4-193">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3e2f4-193">Deploy tooAzure</span></span>
<span data-ttu-id="3e2f4-194">해당 배포를 tootrigger 클릭 **동기화** 또는 **푸시**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="3e2f4-195">Sync는 밀어넣기와 끌어오기를 둘 다 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="3e2f4-196">hello 첫 번째 배포 된 가상 환경, 설치 패키지 등 생성 될 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="3e2f4-197">Visual Studio hello 배포의 진행 상황 hello 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="3e2f4-198">Tooreview hello 출력을 원하는 경우에 hello 섹션을 참조 [문제 해결-배포](#troubleshooting-deployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="3e2f4-199">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="3e2f4-200">웹앱 배포 - Windows - 명령줄</span><span class="sxs-lookup"><span data-stu-id="3e2f4-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="3e2f4-201">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="3e2f4-201">Clone hello repository</span></span>
<span data-ttu-id="3e2f4-202">첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="3e2f4-203">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="3e2f4-204">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2f4-204">Create virtual environment</span></span>
<span data-ttu-id="3e2f4-205">개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="3e2f4-206">Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="3e2f4-207">Toouse hello 동일한 버전의 hello Azure 포털에서에서 웹 응용 프로그램에 대 한 응용 프로그램 설정 블레이드에서 runtime.txt 또는 hello) (에서 웹 응용 프로그램에 대해 선택 된 Python 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="3e2f4-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="3e2f4-208">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="3e2f4-209">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="3e2f4-210">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-210">Install any external packages required by your application.</span></span> <span data-ttu-id="3e2f4-211">가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="3e2f4-212">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="3e2f4-212">Run using development server</span></span>
<span data-ttu-id="3e2f4-213">Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="3e2f4-214">hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="3e2f4-215">그런 다음 웹 브라우저 toothat URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="3e2f4-216">변경 작업</span><span class="sxs-lookup"><span data-stu-id="3e2f4-216">Make changes</span></span>
<span data-ttu-id="3e2f4-217">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="3e2f4-218">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="3e2f4-219">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3e2f4-219">Install more packages</span></span>
<span data-ttu-id="3e2f4-220">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="3e2f4-221">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-221">You can install additional packages using pip.</span></span> <span data-ttu-id="3e2f4-222">예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="3e2f4-223">Tooupdate requirements.txt 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="3e2f4-224">Hello 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="3e2f4-225">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3e2f4-225">Deploy tooAzure</span></span>
<span data-ttu-id="3e2f4-226">배포 tootrigger 푸시 hello tooAzure를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="3e2f4-227">가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="3e2f4-228">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="3e2f4-229">웹앱 배포 - Mac/Linux - 명령줄</span><span class="sxs-lookup"><span data-stu-id="3e2f4-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="3e2f4-230">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="3e2f4-230">Clone hello repository</span></span>
<span data-ttu-id="3e2f4-231">첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="3e2f4-232">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="3e2f4-233">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2f4-233">Create virtual environment</span></span>
<span data-ttu-id="3e2f4-234">개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="3e2f4-235">Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="3e2f4-236">Toouse hello 동일한 버전의 hello Azure 포털에서에서 웹 응용 프로그램의 응용 프로그램 설정 블레이드에서 runtime.txt 또는 hello) (에서 웹 응용 프로그램에 대해 선택 된 Python 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="3e2f4-237">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="3e2f4-238">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="3e2f4-239">또는 pyvenv env</span><span class="sxs-lookup"><span data-stu-id="3e2f4-239">or pyvenv env</span></span>

<span data-ttu-id="3e2f4-240">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-240">Install any external packages required by your application.</span></span> <span data-ttu-id="3e2f4-241">가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="3e2f4-242">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="3e2f4-242">Run using development server</span></span>
<span data-ttu-id="3e2f4-243">Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="3e2f4-244">hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="3e2f4-245">그런 다음 웹 브라우저 toothat URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="3e2f4-246">변경 작업</span><span class="sxs-lookup"><span data-stu-id="3e2f4-246">Make changes</span></span>
<span data-ttu-id="3e2f4-247">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="3e2f4-248">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="3e2f4-249">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3e2f4-249">Install more packages</span></span>
<span data-ttu-id="3e2f4-250">응용 프로그램에 Python 및 Bottle 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="3e2f4-251">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-251">You can install additional packages using pip.</span></span> <span data-ttu-id="3e2f4-252">예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="3e2f4-253">Tooupdate requirements.txt 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="3e2f4-254">Hello 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="3e2f4-255">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="3e2f4-255">Deploy tooAzure</span></span>
<span data-ttu-id="3e2f4-256">배포 tootrigger 푸시 hello tooAzure를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="3e2f4-257">가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="3e2f4-258">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="3e2f4-259">문제 해결 - 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="3e2f4-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="3e2f4-260">문제 해결 - 가상 환경</span><span class="sxs-lookup"><span data-stu-id="3e2f4-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="3e2f4-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e2f4-261">Next Steps</span></span>
<span data-ttu-id="3e2f4-262">Visual Studio에 대 한 이러한 링크 toolearn Bottle 및 Python Tools에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2f4-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="3e2f4-263">[Bottle 설명서]</span><span class="sxs-lookup"><span data-stu-id="3e2f4-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="3e2f4-264">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="3e2f4-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="3e2f4-265">Azure 테이블 저장소 및 MongoDB에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="3e2f4-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="3e2f4-266">[Azure의 Bottle 및 MongoDB와 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3e2f4-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="3e2f4-267">[Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="3e2f4-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="3e2f4-268">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="3e2f4-268">What's changed</span></span>
* <span data-ttu-id="3e2f4-269">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3e2f4-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Azure의 Bottle 및 MongoDB와 Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Azure의 Bottle 및 Azure 테이블 저장소와 Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Windows용 Git]: http://msysgit.github.io/
[Windows용 GitHub]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs 
[Bottle 설명서]: http://bottlepy.org/docs/dev/index.html

