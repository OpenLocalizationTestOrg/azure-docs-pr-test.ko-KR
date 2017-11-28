---
title: "aaaDjango 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 MySQL"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 MySQL 데이터베이스 인스턴스의 데이터를 저장 하는 Django 웹 앱 학습과 tooAzure 앱 서비스 웹 앱을 배포 합니다."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="f550c-103">Azure의 Django 및 MySQL과 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f550c-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="f550c-104">이 자습서를 사용 하 여 [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="f550c-105">에 대해 배워 봅니다 toouse MySQL 서비스 호스팅 방법 Azure에서, 어떻게 tooconfigure hello 웹 앱 toouse MySQL 어떻게 toopublish hello 웹 응용 프로그램 너무[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="f550c-106">이 자습서에 포함 된 hello 정보 비디오를 따라 hello에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="f550c-107">[PTVS 2.1: MySQL을 사용하는 Django 앱][video]</span><span class="sxs-lookup"><span data-stu-id="f550c-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="f550c-108">Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크에서 Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="f550c-109">개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f550c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f550c-110">Prerequisites</span></span>
* <span data-ttu-id="f550c-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f550c-111">Visual Studio 2015</span></span>
* <span data-ttu-id="f550c-112">[Python 2.7 32비트] 또는 [Python 3.4 32비트]</span><span class="sxs-lookup"><span data-stu-id="f550c-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="f550c-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f550c-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="f550c-114">[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]</span><span class="sxs-lookup"><span data-stu-id="f550c-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="f550c-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="f550c-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="f550c-116">Django 1.9 이상</span><span class="sxs-lookup"><span data-stu-id="f550c-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="f550c-117">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f550c-118">신용 카드 및 약정은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="f550c-119">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="f550c-119">Create hello Project</span></span>
<span data-ttu-id="f550c-120">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="f550c-121">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="f550c-122">sqlite를 사용하여 로컬 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="f550c-123">다음 hello 응용 프로그램을 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="f550c-124">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="f550c-125">프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="f550c-126">선택 **설문 Django 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="f550c-128">외부 패키지 입력 정보 요청된 tooinstall 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="f550c-129">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-129">Select **Install into a virtual environment**.</span></span>
   
    ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="f550c-131">선택 **Python 2.7** 또는 **Python 3.4** hello 기본 해석기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="f550c-133">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="f550c-134">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="f550c-135">Django 관리 콘솔 열리며 hello 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="f550c-136">Hello 프롬프트 toocreate 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="f550c-137">Hello 응용 프로그램 키를 눌러 작동 하는지 확인 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="f550c-138">클릭 **로그인** hello hello 위쪽 탐색 모음에서.</span><span class="sxs-lookup"><span data-stu-id="f550c-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Django 탐색 모음](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="f550c-140">Hello 데이터베이스를 동기화 할 때 만든 hello 사용자에 대 한 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![로그인 형식](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="f550c-142">**Create Sample Polls**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="f550c-144">poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-144">Click on a poll and vote.</span></span>
    
     ![샘플 설문 조사 투표](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="f550c-146">MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f550c-146">Create a MySQL Database</span></span>
<span data-ttu-id="f550c-147">Hello 데이터베이스에서는 Azure에서 호스팅된 ClearDB MySQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="f550c-148">또는 Azure에서 실행되는 자체의 가상 컴퓨터를 만든 다음 MySQL을 직접 설치하고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="f550c-149">다음 단계에 따라 무료로 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="f550c-150">Toohello 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="f550c-151">Hello hello 탐색 창의 위쪽에 클릭 **새로**, 클릭 **데이터 + 저장소**, 클릭 하 고 **MySQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="f550c-152">새 리소스 그룹을 만들어 hello 새 MySQL 데이터베이스를 구성 하 고 hello에 대 한 적절 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="f550c-153">Hello MySQL 데이터베이스를 만든 후 클릭 **속성** hello 데이터베이스 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="f550c-154">hello 복사 단추 tooput hello 값을 사용 하 여 **연결 문자열** hello 클립보드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="f550c-155">Hello 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="f550c-155">Configure hello Project</span></span>
<span data-ttu-id="f550c-156">이 섹션에서는 방금 만든 웹 응용 프로그램 toouse hello MySQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="f550c-157">또한 Django와 추가 Python 패키지 필요한 toouse MySQL 데이터베이스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="f550c-158">다음 hello 웹 응용 프로그램을 로컬로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="f550c-159">Visual Studio에서 열고 **settings.py**, hello에서 *ProjectName* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="f550c-160">일시적으로 hello 연결 문자열 hello 편집기에 붙여 넣으십시오.</span><span class="sxs-lookup"><span data-stu-id="f550c-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="f550c-161">hello 연결 문자열은이 형식:</span><span class="sxs-lookup"><span data-stu-id="f550c-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="f550c-162">Hello 기본 데이터베이스 변경 **엔진** 집합과, MySQL, toouse hello에 대 한 값 **이름**, **사용자**, **암호** 및  **호스트** hello에서 **CONNECTIONSTRING**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="f550c-163">솔루션 탐색기에서 아래 **Python 환경**hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **Python 패키지 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="f550c-164">Hello 패키지 설치 `mysqlclient` 를 사용 하 여 **pip**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![설치 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="f550c-166">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="f550c-167">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="f550c-168">그러면 hello 이전 섹션에서 만든 hello MySQL 데이터베이스에 대 한 hello 테이블 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="f550c-169">Hello 프롬프트 toocreate toomatch hello 사용자 hello이 문서의 첫 번째 섹션에서 만든 hello sqlite 데이터베이스에 없는 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="f550c-170">Hello 응용 프로그램을 실행 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-170">Run hello application with `F5`.</span></span> <span data-ttu-id="f550c-171">사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터 hello MySQL 데이터베이스에 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="f550c-172">Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="f550c-173">Azure.NET SDK hello 쉽게 toodeploy 웹 앱 tooAzure 앱 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="f550c-174">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="f550c-176">**Microsoft Azure 앱 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="f550c-177">클릭 **새로** toocreate 새 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="f550c-178">Hello 필드 뒤에 입력 하 고 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="f550c-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="f550c-179">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="f550c-179">**Web App name**</span></span>
   * <span data-ttu-id="f550c-180">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="f550c-180">**App Service plan**</span></span>
   * <span data-ttu-id="f550c-181">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="f550c-181">**Resource group**</span></span>
   * <span data-ttu-id="f550c-182">**지역**</span><span class="sxs-lookup"><span data-stu-id="f550c-182">**Region**</span></span>
   * <span data-ttu-id="f550c-183">둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="f550c-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="f550c-184">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="f550c-185">웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="f550c-186">Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **MySQL** Azure에서 호스팅되는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![웹 브라우저](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="f550c-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-188">Congratulations!</span></span> <span data-ttu-id="f550c-189">MySQL 기반 웹 응용 프로그램 tooAzure를 게시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f550c-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f550c-190">Next steps</span></span>
<span data-ttu-id="f550c-191">Visual Studio, Django 및 MySQL Python Tools에 대 한 자세한 링크 toolearn 이러한 방식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="f550c-192">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="f550c-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="f550c-193">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="f550c-193">[Web Projects]</span></span>
  * <span data-ttu-id="f550c-194">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="f550c-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="f550c-195">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="f550c-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="f550c-196">[Django 설명서]</span><span class="sxs-lookup"><span data-stu-id="f550c-196">[Django Documentation]</span></span>
* <span data-ttu-id="f550c-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="f550c-197">[MySQL]</span></span>

<span data-ttu-id="f550c-198">자세한 내용은 참조 hello [Python 개발자 센터](/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f550c-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure 포털]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32비트]: http://go.microsoft.com/fwlink/?LinkId=517191
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 설명서]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
