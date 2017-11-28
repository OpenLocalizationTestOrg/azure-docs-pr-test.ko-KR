---
title: "Azure에서 Django로 aaaCreating 웹 앱"
description: "Toorunning Azure 앱 서비스 웹 앱에서 Python 웹 응용 프로그램을 소개 하는 자습서입니다."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="7863a-103">Azure에서 Django를 사용하여 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="7863a-104">이 자습서에서는 tooget 시작 Python을 실행 하는 방법을 설명 [Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="7863a-105">웹앱은 제한된 무료 호스팅 및 신속한 배포 기능을 제공하며, Python을 사용할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="7863a-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="7863a-106">응용 프로그램 증가, toopaid 호스팅 전환할 수 있습니다 및 모든와 통합할 수 있습니다 때 hello 다른 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="7863a-107">Hello Django 웹 프레임 워크를 사용 하 여 응용 프로그램을 만들 됩니다 (참조에 대 한이 자습서의 대체 버전 [플라스](web-sites-python-create-deploy-flask-app.md) 및 [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="7863a-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="7863a-108">Hello 웹 응용 프로그램 hello Azure Marketplace에서에서, Git 배포 설정 만들고 hello 로컬 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="7863a-109">다음은 hello 응용 프로그램을 로컬로 실행, 변경, 커밋 하 고 tooAzure 푸시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="7863a-110">자습서에서는 어떻게 hello toodo Windows 또는 Mac/Linux에서이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="7863a-111">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7863a-112">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7863a-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7863a-113">Prerequisites</span></span>
* <span data-ttu-id="7863a-114">Windows, Mac 또는 Linux</span><span class="sxs-lookup"><span data-stu-id="7863a-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="7863a-115">Python 2.7 또는 3.4</span><span class="sxs-lookup"><span data-stu-id="7863a-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="7863a-116">setuptools, pip, virtualenv(Python 2.7 전용)</span><span class="sxs-lookup"><span data-stu-id="7863a-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="7863a-117">Git</span><span class="sxs-lookup"><span data-stu-id="7863a-117">Git</span></span>
* <span data-ttu-id="7863a-118">[Python Tools for Visual Studio][Python Tools for Visual Studio](PTVS) - 참고: 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="7863a-119">**참고**: 현재 Python 프로젝트에서는 TFS 게시를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="7863a-120">Windows</span><span class="sxs-lookup"><span data-stu-id="7863a-120">Windows</span></span>
<span data-ttu-id="7863a-121">Python 2.7 또는 3.4(32비트)를 아직 설치하지 않은 경우 웹 플랫폼 설치 관리자를 사용하여 [Azure SDK for Python 2.7] 또는 [Azure SDK for Python 3.4]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="7863a-122">이 Python, setuptools, pip, virtualenv 등의 (32 비트 Python hello Azure 호스트 컴퓨터에 설치 된 항목은) hello 32 비트 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="7863a-123">또는 [python.org]에서 Python을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="7863a-124">Git의 경우 [Windows용 Git] 또는 [Windows용 GitHub]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="7863a-125">Visual Studio를 사용 하는 경우 통합 hello Git 지원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="7863a-126">또한 [Python Tools 2.2 for Visual Studio]를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="7863a-127">이 속성은 선택적 있는 경우 [Visual Studio]hello를 포함 하 여 가능한 Visual Studio Community 2013 또는 Visual Studio Express 2013 for Web 차례로 이렇게 하면 한 훌륭한 인 Python IDE 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="7863a-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7863a-128">Mac/Linux</span></span>
<span data-ttu-id="7863a-129">Python 및 Git를 이미 설치했어야 하지만 Python 버전은 2.7 또는 3.4여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="7863a-130">포털에서 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-130">Web App Creation on Portal</span></span>
<span data-ttu-id="7863a-131">hello 앱을 만드는 첫 번째 단계는 hello 통해 toocreate hello 웹 앱 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="7863a-132">Hello Azure 포털에 로그인 하 고 hello 클릭 **새로** hello 왼쪽된 하단에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="7863a-133">Hello 검색 상자에 "python"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="7863a-134">Hello 검색 결과에서 선택 **Django** (PTVS에서 게시)를 클릭 한 다음 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="7863a-135">Hello 새 Django 같은 앱에 대 한 새 앱 서비스 계획을 만들고 새 리소스 그룹을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="7863a-136">그런 다음에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="7863a-137">Hello 지침에 따라 새로 만든된 웹 앱에 대 한 Git 게시를 구성 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="7863a-138">응용 프로그램 개요</span><span class="sxs-lookup"><span data-stu-id="7863a-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="7863a-139">Git 리포지토리 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="7863a-139">Git repository contents</span></span>
<span data-ttu-id="7863a-140">Hello 다음 섹션에서 복제 hello 초기 Git 리포지토리에 있습니다 hello 파일의 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="7863a-141">Hello 응용 프로그램에 대 한 주 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-141">Main sources for hello application.</span></span> <span data-ttu-id="7863a-142">마스터 레이아웃과 함께 3페이지(index, about, contact)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="7863a-143">정적 콘텐츠와 스크립트에는 bootstrap, jquery, modernizr 및 respond가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="7863a-144">로컬 관리 및 개발 서버 지원.</span><span class="sxs-lookup"><span data-stu-id="7863a-144">Local management and development server support.</span></span> <span data-ttu-id="7863a-145">ऍ प ् toorun hello 로컬로, 등 hello 데이터베이스를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="7863a-146">기본 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="7863a-146">Default database.</span></span> <span data-ttu-id="7863a-147">Hello 응용 프로그램 toorun에 대 한 hello 필요한 테이블을 포함 하지만 (hello 데이터베이스 toocreate 사용자 동기화) 사용자가 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="7863a-148">[Python Tools for Visual Studio]에서 사용되는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="7863a-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="7863a-149">가상 환경용 IIS 프록시 및 PTVS 원격 디버깅 지원</span><span class="sxs-lookup"><span data-stu-id="7863a-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="7863a-150">이 응용 프로그램에 필요한 외부 패키지.</span><span class="sxs-lookup"><span data-stu-id="7863a-150">External packages needed by this application.</span></span> <span data-ttu-id="7863a-151">hello 배포 스크립트에는이 파일에 나열 된 설치 hello 패키지 pip 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="7863a-152">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="7863a-152">IIS configuration files.</span></span> <span data-ttu-id="7863a-153">hello 배포 스크립트는 hello 적절 한 web.x.y.config 사용 되 고 web.config로 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="7863a-154">선택적 파일 - 배포 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="7863a-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="7863a-155">선택적 파일 - Python 런타임</span><span class="sxs-lookup"><span data-stu-id="7863a-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="7863a-156">서버의 추가 파일</span><span class="sxs-lookup"><span data-stu-id="7863a-156">Additional files on server</span></span>
<span data-ttu-id="7863a-157">일부 파일 hello 서버에 존재 하지만 toohello git 리포지토리를 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="7863a-158">Hello 배포 스크립트에 의해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="7863a-159">IIS 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="7863a-159">IIS configuration file.</span></span> <span data-ttu-id="7863a-160">모든 배포에서 web.x.y.config를 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="7863a-161">Python 가상 환경.</span><span class="sxs-lookup"><span data-stu-id="7863a-161">Python virtual environment.</span></span> <span data-ttu-id="7863a-162">호환 되는 가상 환경 hello 웹 응용 프로그램에 존재 하지 않는 경우 배포 중에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="7863a-163">Requirements.txt에 나열 된 패키지를 설치 하는 pip는 pip는 hello 패키지가 이미 설치 되어 있는 경우 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="7863a-164">hello 다음 3 설명 어떻게 hello로 tooproceed 웹 3 다양 한 환경에서 응용 프로그램 개발:</span><span class="sxs-lookup"><span data-stu-id="7863a-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="7863a-165">Windows, Python Tools for Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="7863a-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="7863a-166">Windows, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="7863a-166">Windows, with command line</span></span>
* <span data-ttu-id="7863a-167">Mac/Linux, 명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="7863a-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="7863a-168">웹앱 배포 - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7863a-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="7863a-169">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="7863a-169">Clone hello repository</span></span>
<span data-ttu-id="7863a-170">첫째, hello Azure 포털에서 제공 하는 hello URL를 사용 하 여 hello 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="7863a-171">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="7863a-172">Hello 저장소의 hello 루트에 포함 된 hello 솔루션 파일 (.sln)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="7863a-173">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-173">Create virtual environment</span></span>
<span data-ttu-id="7863a-174">이제 로컬 개발을 위한 가상 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="7863a-175">**Python Environments**를 마우스 오른쪽 단추로 클릭하고 **Add Virtual Environment...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="7863a-176">Hello 환경의 hello 이름 인지 확인 `env`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="7863a-177">Hello 기본 인터프리터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-177">Select hello base interpreter.</span></span> <span data-ttu-id="7863a-178">Toouse hello 동일한 버전의 웹 앱에 대해 선택 된 Python 있는지 확인 (runtime.txt 또는 hello **응용 프로그램 설정** hello Azure 포털에서에서 웹 응용 프로그램의 블레이드)입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="7863a-179">Hello 옵션 toodownload 및 설치 패키지 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="7863a-180">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-180">Click **Create**.</span></span> <span data-ttu-id="7863a-181">이 hello 가상 환경을 만들고 requirements.txt에 나열 된 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="7863a-182">superuser 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-182">Create a superuser</span></span>
<span data-ttu-id="7863a-183">hello 응용 프로그램에 포함 된 hello 데이터베이스에 정의 된 모든 superuser를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="7863a-184">순서 toouse hello 로그인 기능 hello 응용 프로그램 또는 hello Django 관리 인터페이스에서에서 (tooenable 결정 한 경우 해당), toocreate superuser 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="7863a-185">명령줄을 실행이 hello에서 프로젝트 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="7863a-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="7863a-186">Hello 프롬프트 tooset hello 사용자 이름, 암호 등을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="7863a-187">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="7863a-187">Run using development server</span></span>
<span data-ttu-id="7863a-188">디버깅, 키를 눌러 F5 toostart 및 웹 브라우저가 자동으로 toohello 페이지가 열립니다 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="7863a-189">Hello 소스, 사용 하 여 hello 조사식 창에서 중단점을 설정할 수 있습니다. Hello 참조 [Python Tools for Visual Studio 설명서] 대 한 자세한 내용은 hello 다양 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="7863a-190">변경 작업</span><span class="sxs-lookup"><span data-stu-id="7863a-190">Make changes</span></span>
<span data-ttu-id="7863a-191">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="7863a-192">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="7863a-193">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="7863a-193">Install more packages</span></span>
<span data-ttu-id="7863a-194">응용 프로그램에 Python 및 Django 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="7863a-195">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-195">You can install additional packages using pip.</span></span> <span data-ttu-id="7863a-196">선택 및 hello 가상 환경에서 tooinstall 패키지를 마우스 오른쪽 단추로 클릭 **Python 패키지 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="7863a-197">예를 들어 tooinstall hello 액세스할 수 있도록 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스를 입력 하는 Python 용 Azure SDK `azure`:</span><span class="sxs-lookup"><span data-stu-id="7863a-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="7863a-198">Hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **requirements.txt 생성** tooupdate requirements.txt 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="7863a-199">그런 다음 커밋 hello toorequirements.txt toohello Git 리포지토리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="7863a-200">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="7863a-200">Deploy tooAzure</span></span>
<span data-ttu-id="7863a-201">해당 배포를 tootrigger 클릭 **동기화** 또는 **푸시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="7863a-202">Sync는 밀어넣기와 끌어오기를 둘 다 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="7863a-203">hello 첫 번째 배포 된 가상 환경, 설치 패키지 등 생성 될 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="7863a-204">Visual Studio hello 배포의 진행 상황 hello 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="7863a-205">Tooreview hello 출력을 원하는 경우에 hello 섹션을 참조 [문제 해결-배포](#troubleshooting-deployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="7863a-206">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="7863a-207">웹앱 배포 - Windows - 명령줄</span><span class="sxs-lookup"><span data-stu-id="7863a-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="7863a-208">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="7863a-208">Clone hello repository</span></span>
<span data-ttu-id="7863a-209">첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="7863a-210">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="7863a-211">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-211">Create virtual environment</span></span>
<span data-ttu-id="7863a-212">개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="7863a-213">Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.</span><span class="sxs-lookup"><span data-stu-id="7863a-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="7863a-214">Toouse hello 동일한 버전의 hello Azure 포털에서에서 웹 응용 프로그램의 응용 프로그램 설정 블레이드에서 runtime.txt 또는 hello) (에서 웹 응용 프로그램에 대해 선택 된 Python 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="7863a-215">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="7863a-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="7863a-216">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="7863a-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="7863a-217">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-217">Install any external packages required by your application.</span></span> <span data-ttu-id="7863a-218">가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="7863a-219">superuser 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-219">Create a superuser</span></span>
<span data-ttu-id="7863a-220">hello 응용 프로그램에 포함 된 hello 데이터베이스에 정의 된 모든 superuser를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="7863a-221">순서 toouse hello 로그인 기능 hello 응용 프로그램 또는 hello Django 관리 인터페이스에서에서 (tooenable 결정 한 경우 해당), toocreate superuser 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="7863a-222">명령줄을 실행이 hello에서 프로젝트 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="7863a-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="7863a-223">Hello 프롬프트 tooset hello 사용자 이름, 암호 등을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="7863a-224">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="7863a-224">Run using development server</span></span>
<span data-ttu-id="7863a-225">Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="7863a-226">hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:</span><span class="sxs-lookup"><span data-stu-id="7863a-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="7863a-227">그런 다음 웹 브라우저 toothat URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="7863a-228">변경 작업</span><span class="sxs-lookup"><span data-stu-id="7863a-228">Make changes</span></span>
<span data-ttu-id="7863a-229">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="7863a-230">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="7863a-231">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="7863a-231">Install more packages</span></span>
<span data-ttu-id="7863a-232">응용 프로그램에 Python 및 Django 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="7863a-233">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-233">You can install additional packages using pip.</span></span> <span data-ttu-id="7863a-234">예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:</span><span class="sxs-lookup"><span data-stu-id="7863a-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="7863a-235">Tooupdate requirements.txt 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="7863a-236">Hello 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="7863a-237">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="7863a-237">Deploy tooAzure</span></span>
<span data-ttu-id="7863a-238">배포 tootrigger 푸시 hello tooAzure를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="7863a-239">가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="7863a-240">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="7863a-241">웹앱 배포 - Mac/Linux - 명령줄</span><span class="sxs-lookup"><span data-stu-id="7863a-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="7863a-242">Hello 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="7863a-242">Clone hello repository</span></span>
<span data-ttu-id="7863a-243">첫째, hello Azure 포털에서 제공 하는 hello URL을 사용 하 여 hello 리포지토리를 복제 하 고 원격으로 hello Azure 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="7863a-244">자세한 내용은 참조 [로컬 Git 배포 tooAzure 앱 서비스](app-service-deploy-local-git.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="7863a-245">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-245">Create virtual environment</span></span>
<span data-ttu-id="7863a-246">개발 목적으로 (추가 하지 않아도 toohello 저장소)에 대 한 새 가상 환경이 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="7863a-247">Python에서 가상 환경을 위치 변경이 가능한, 되지 않으므로 hello 응용 프로그램에서 작업 하는 모든 개발자는 자체적으로 만드는 로컬로.</span><span class="sxs-lookup"><span data-stu-id="7863a-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="7863a-248">Toouse hello 동일한 버전의 hello Azure 포털에서에서 웹 응용 프로그램의 응용 프로그램 설정 블레이드에서 runtime.txt 또는 hello) (에서 웹 응용 프로그램에 대해 선택 된 Python 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="7863a-249">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="7863a-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="7863a-250">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="7863a-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="7863a-251">또는</span><span class="sxs-lookup"><span data-stu-id="7863a-251">or</span></span>

    pyvenv env

<span data-ttu-id="7863a-252">응용 프로그램에 필요한 모든 외부 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-252">Install any external packages required by your application.</span></span> <span data-ttu-id="7863a-253">가상 환경에서 hello 리포지토리 tooinstall hello 패키지의 hello 루트를 hello requirements.txt 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="7863a-254">superuser 만들기</span><span class="sxs-lookup"><span data-stu-id="7863a-254">Create a superuser</span></span>
<span data-ttu-id="7863a-255">hello 응용 프로그램에 포함 된 hello 데이터베이스에 정의 된 모든 superuser를 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="7863a-256">순서 toouse hello 로그인 기능 hello 응용 프로그램 또는 hello Django 관리 인터페이스에서에서 (tooenable 결정 한 경우 해당), toocreate superuser 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="7863a-257">명령줄을 실행이 hello에서 프로젝트 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="7863a-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="7863a-258">Hello 프롬프트 tooset hello 사용자 이름, 암호 등을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="7863a-259">개발 서버를 사용하여 실행</span><span class="sxs-lookup"><span data-stu-id="7863a-259">Run using development server</span></span>
<span data-ttu-id="7863a-260">Hello 응용 프로그램 개발 서버에서 다음 명령을 hello로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="7863a-261">hello 콘솔 hello URL이 표시 됩니다 및를 수신 대기 포트 hello 서버:</span><span class="sxs-lookup"><span data-stu-id="7863a-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="7863a-262">그런 다음 웹 브라우저 toothat URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="7863a-263">변경 작업</span><span class="sxs-lookup"><span data-stu-id="7863a-263">Make changes</span></span>
<span data-ttu-id="7863a-264">이제 변경 내용이 toohello 응용 프로그램 소스 및/또는 서식 파일을 만들어서 해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="7863a-265">변경 내용을 테스트 한 후 toohello Git 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="7863a-266">추가 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="7863a-266">Install more packages</span></span>
<span data-ttu-id="7863a-267">응용 프로그램에 Python 및 Django 이외의 종속성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="7863a-268">pip를 사용하여 추가 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-268">You can install additional packages using pip.</span></span> <span data-ttu-id="7863a-269">예를 들어 tooinstall hello을 제공 하는 Python 용 Azure SDK 액세스 tooAzure 저장소, 서비스 버스 및 기타 Azure 서비스 유형:</span><span class="sxs-lookup"><span data-stu-id="7863a-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="7863a-270">Tooupdate requirements.txt 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="7863a-271">Hello 변경 내용을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="7863a-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="7863a-272">TooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="7863a-272">Deploy tooAzure</span></span>
<span data-ttu-id="7863a-273">배포 tootrigger 푸시 hello tooAzure를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="7863a-274">가상 환경 만들기, 패키지를 설치 web.config의 생성을 포함 하 여 hello 배포 스크립트의 hello 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="7863a-275">Toohello Azure URL tooview 변경 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="7863a-276">문제 해결 - 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="7863a-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="7863a-277">문제 해결 - 가상 환경</span><span class="sxs-lookup"><span data-stu-id="7863a-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="7863a-278">문제 해결 - 정적 파일</span><span class="sxs-lookup"><span data-stu-id="7863a-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="7863a-279">Django 개념이 hello 정적 파일을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="7863a-280">이 모든 hello 정적 파일에서 원래 위치를 가져오며 tooa 단일 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="7863a-281">이 응용 프로그램에 대 한 복사 되며 너무`/static`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="7863a-282">이 작업은 정적 파일이 다른 Django ‘앱’에서 가져온 파일일 수 있기 때문에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="7863a-283">예를 들어 hello Django 관리 인터페이스에서 정적 파일 hello hello 가상 환경에서 Django 라이브러리 하위 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="7863a-284">이 응용 프로그램에서 정의된 정적 파일은 `/app/static`에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="7863a-285">추가 Django ‘앱’을 사용할 경우 정적 파일을 여러 위치에 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="7863a-286">Hello 응용 프로그램, 디버그 모드에서 실행할 때는 hello 응용 프로그램의 원래 위치에서 hello 정적 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="7863a-287">Hello 응용 프로그램, 릴리스 모드에서 실행할 때는 hello 응용 프로그램 않습니다 **하지** hello 정적 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="7863a-288">hello hello 웹 서버 tooserve hello 파일의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="7863a-289">IIS에서 hello 정적 파일에서이 응용 프로그램에 대 한 처리 `/static`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="7863a-290">이전에 수집 hello 배포 스크립트를 지우는 부분의 파일로 hello 컬렉션 정적 파일을 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="7863a-291">즉, hello 컬렉션 배포 속도가 약간 느려지는 모든 배포에서 발생 하지만 되도록 조정 사용 되지 않는 파일 사용할 수 있는 잠재적인 보안 문제를 피할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="7863a-292">Django 응용 프로그램에 대 한 정적 파일의 tooskip 컬렉션 하려면:</span><span class="sxs-lookup"><span data-stu-id="7863a-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="7863a-293">그런 다음이 필요 합니다 toodo hello 컬렉션 수동으로 로컬 컴퓨터에서.</span><span class="sxs-lookup"><span data-stu-id="7863a-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="7863a-294">다음 hello 제거 `\static` 폴더에서 `.gitignore` toohello Git 리포지토리를 추가 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="7863a-295">문제 해결 - 설정</span><span class="sxs-lookup"><span data-stu-id="7863a-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="7863a-296">Hello 응용 프로그램에 대 한 다양 한 설정을 변경할 수 있습니다 `DjangoWebProject/settings.py`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="7863a-297">개발자의 편의를 위해 디버그 모드가 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="7863a-298">좋은 부작용 중 하나는 수 수 toosee 이미지 및 다른 정적 콘텐츠 toocollect 정적 파일 필요 없이 로컬에서 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7863a-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="7863a-299">toodisable 디버그 모드:</span><span class="sxs-lookup"><span data-stu-id="7863a-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="7863a-300">디버그 비활성화 되 면 hello에 대 한 값 `ALLOWED_HOSTS` 요구 toobe tooinclude hello Azure 호스트 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="7863a-301">예:</span><span class="sxs-lookup"><span data-stu-id="7863a-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="7863a-302">또는 tooenable 모든:</span><span class="sxs-lookup"><span data-stu-id="7863a-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="7863a-303">실제로 수도 있습니다 toodo 간에 전환 하는 데 더 복잡 한 toodeal 디버그 하 고 가져오는 hello 호스트 이름 및 모드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="7863a-304">Hello Azure 포털을 통해 환경 변수를 설정할 수 **구성** 페이지 hello **앱 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="7863a-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="7863a-305">이 hello 소스 (연결 문자열, 암호 등)에서 tooappear 원하지 않을 수 있습니다 또는 Azure와 로컬 컴퓨터 간에 다르게 tooset 원하는 값을 설정 하기 위한 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="7863a-306">`settings.py`를 사용 하 여 hello 환경 변수를 쿼리할 수 있습니다 `os.getenv`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="7863a-307">데이터베이스 사용</span><span class="sxs-lookup"><span data-stu-id="7863a-307">Using a Database</span></span>
<span data-ttu-id="7863a-308">hello 응용 프로그램에 포함 되어 있는 hello 데이터베이스가 sqlite 데이터베이스가입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="7863a-309">설치 하지 않아도 거의 해야 하므로 개발을 위한 편리 하 고 유용한 기본 데이터베이스 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="7863a-310">hello 데이터베이스 hello 프로젝트 폴더의 hello db.sqlite3 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="7863a-311">Azure는 Django 응용 프로그램에서 쉽게 toouse 데이터베이스 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="7863a-312">사용 하 여에 대 한 자습서 [SQL 데이터베이스] 및 [MySQL] Django 응용 프로그램에서 단계를 보여 줍니다 hello 필요한 toocreate hello 데이터베이스 서비스의 hello 데이터베이스 설정을 변경 `DjangoWebProject/settings.py`, 및 hello 라이브러리 tooinstall이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="7863a-313">물론, toomanage 고유한 데이터베이스 서버를 선호 하는 경우 Azure에서 실행 되는 Windows 또는 Linux 가상 컴퓨터를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="7863a-314">Django 관리 인터페이스</span><span class="sxs-lookup"><span data-stu-id="7863a-314">Django Admin Interface</span></span>
<span data-ttu-id="7863a-315">모델 작성을 시작 하면 일부 데이터를 사용 하 여 toopopulate hello 데이터베이스를 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="7863a-316">쉽게 toodo 추가 하 고 콘텐츠를 대화형으로 편집는 toouse hello Django 관리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="7863a-317">관리 인터페이스를 hello에 대 한 hello 코드 hello 응용 프로그램 소스에 주석으로 처리 하지만 것 ('관리'에 대 한 검색) 쉽게 사용할 수 있도록 명확 하 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="7863a-318">활성화 된 후 hello 데이터베이스를 동기화, hello 응용 프로그램을 실행 하 고 탐색 너무`/admin`합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7863a-319">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7863a-319">Next Steps</span></span>
<span data-ttu-id="7863a-320">Visual Studio에 대 한 이러한 링크 toolearn Django 및 Python Tools에 대 한 자세한를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="7863a-321">[Django 설명서]</span><span class="sxs-lookup"><span data-stu-id="7863a-321">[Django Documentation]</span></span>
* <span data-ttu-id="7863a-322">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="7863a-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="7863a-323">SQL 데이터베이스 및 MySQL 사용에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7863a-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="7863a-324">[Azure의 Django 및 MySQL과 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7863a-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="7863a-325">[Azure의 Django 및 SQL 데이터베이스와 Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7863a-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="7863a-326">자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7863a-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="7863a-327">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="7863a-327">What's changed</span></span>
* <span data-ttu-id="7863a-328">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7863a-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Azure의 Django 및 MySQL과 Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Azure의 Django 및 SQL 데이터베이스와 Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL 데이터베이스]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Django 설명서]: https://www.djangoproject.com/
