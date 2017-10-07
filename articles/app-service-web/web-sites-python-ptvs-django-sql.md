---
title: "aaaDjango 및 Python Tools 2.2 for Visual Studio를 사용 하 여 Azure에서 SQL 데이터베이스"
description: "어떻게 toouse hello Python Tools toocreate Visual Studio에 대 한 SQL 데이터베이스 인스턴스의 데이터를 저장 하는 Django 웹 앱 학습과 tooAzure 앱 서비스 웹 앱을 배포 합니다."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="00eee-103">Azure의 Django 및 SQL 데이터베이스와 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00eee-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="00eee-104">이 자습서에서는 [Python Tools for Visual Studio] toocreate 단순 hello PTVS 샘플 템플릿 중 하나를 사용 하 여 웹 앱을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="00eee-105">이 자습서는 [비디오](https://www.youtube.com/watch?v=ZwcoGcIeHF4)로도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="00eee-106">Toouse SQL 데이터베이스 호스팅 방법 Azure에서, 어떻게 tooconfigure hello 웹 응용 프로그램 toouse SQL 데이터베이스 및 어떻게 toopublish hello 웹 응용 프로그램 너무 알아봅니다 म[Azure 앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="00eee-107">Hello 참조 [Python 개발자 센터] Bottle를 사용 하 여 ptvs Azure 앱 서비스 웹 앱의 개발을 설명 하는 다른 문서 플라스 및 Django 웹 프레임 워크에서 Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="00eee-108">개발 하는 경우 hello 단계는 유사 하지만이 문서에서는 앱 서비스, [Azure 클라우드 서비스]합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00eee-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00eee-109">Prerequisites</span></span>
* <span data-ttu-id="00eee-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="00eee-110">Visual Studio 2015</span></span>
* <span data-ttu-id="00eee-111">[Python 2.7 32비트]</span><span class="sxs-lookup"><span data-stu-id="00eee-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="00eee-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="00eee-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="00eee-113">[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]</span><span class="sxs-lookup"><span data-stu-id="00eee-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="00eee-114">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="00eee-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="00eee-115">Django 1.9 이상</span><span class="sxs-lookup"><span data-stu-id="00eee-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="00eee-116">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="00eee-117">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="00eee-118">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="00eee-118">Create hello Project</span></span>
<span data-ttu-id="00eee-119">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="00eee-120">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="00eee-121">sqlite를 사용하여 로컬 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="00eee-122">그런 다음 hello 웹 응용 프로그램을 로컬로 실행할 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="00eee-123">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="00eee-124">프로젝트 템플릿 hello에서 hello [VSIX Visual Studio 샘플에 대 한 Python Tools 2.2] 아래에서 사용할 수 있는 **Python**, **샘플**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="00eee-125">선택 **설문 Django 웹 프로젝트** 확인 toocreate hello 프로젝트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="00eee-127">외부 패키지 입력 정보 요청된 tooinstall 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="00eee-128">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-128">Select **Install into a virtual environment**.</span></span>

     ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="00eee-130">선택 **Python 2.7** hello 기본 해석기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="00eee-132">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="00eee-133">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="00eee-134">Django 관리 콘솔 열리며 hello 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="00eee-135">Hello 프롬프트 toocreate 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="00eee-136">Hello 응용 프로그램 키를 눌러 작동 하는지 확인 <kbd>F5</kbd>합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="00eee-137">클릭 **로그인** hello hello 위쪽 탐색 모음에서.</span><span class="sxs-lookup"><span data-stu-id="00eee-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="00eee-139">Hello 데이터베이스를 동기화 할 때 만든 hello 사용자에 대 한 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="00eee-141">**Create Sample Polls**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-141">Click **Create Sample Polls**.</span></span>

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="00eee-143">poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-143">Click on a poll and vote.</span></span>

      ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="00eee-145">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00eee-145">Create a SQL Database</span></span>
<span data-ttu-id="00eee-146">Hello 데이터베이스에 대 한 Azure SQL 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="00eee-147">다음 단계에 따라 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="00eee-148">Hello에 로그인 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="00eee-149">Hello hello 탐색 창 아래쪽에 있는 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="00eee-150">**데이터 + 저장소** > **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="00eee-151">구성 선택 hello에 대 한 적절 한 위치 및 새 리소스 그룹을 만들어 새 SQL 데이터베이스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="00eee-152">Hello SQL 데이터베이스를 만든 후 클릭 **Visual Studio에서 열기** hello 데이터베이스 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="00eee-153">**방화벽 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="00eee-154">Hello에 **방화벽 설정** 블레이드를 사용 하 여 방화벽 규칙을 추가할 **시작 IP** 및 **끝 IP** toohello 개발 컴퓨터의 공용 IP 주소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="00eee-155">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-155">Click **Save**.</span></span>

   <span data-ttu-id="00eee-156">이렇게 하면 개발 컴퓨터에서 연결 toohello 데이터베이스 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="00eee-157">Hello 데이터베이스 블레이드를 다시 클릭 **속성**, 클릭 **데이터베이스 연결 문자열 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="00eee-158">hello 복사 단추 tooput hello 값을 사용 하 여 **ADO.NET** hello 클립보드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="00eee-159">Hello 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="00eee-159">Configure hello Project</span></span>
<span data-ttu-id="00eee-160">이 섹션에서는 방금 만든 웹 응용 프로그램 toouse hello SQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="00eee-161">에서는도 Django와 추가 Python 패키지 필요한 toouse SQL 데이터베이스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="00eee-162">그런 다음 hello 웹 응용 프로그램을 로컬로 실행할 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="00eee-163">Visual Studio에서 열고 **settings.py**, hello에서 *ProjectName* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="00eee-164">일시적으로 hello 연결 문자열 hello 편집기에 붙여 넣으십시오.</span><span class="sxs-lookup"><span data-stu-id="00eee-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="00eee-165">hello 연결 문자열은이 형식:</span><span class="sxs-lookup"><span data-stu-id="00eee-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="00eee-166">hello 정의 편집 `DATABASES` 위의 toouse hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="00eee-167">솔루션 탐색기에서 아래 **Python 환경**hello 가상 환경에서 마우스 오른쪽 단추로 클릭 하 고 선택 **Python 패키지 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="00eee-168">Hello 패키지 설치 `pyodbc` 를 사용 하 여 **pip**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="00eee-170">Hello 패키지 설치 `django-pyodbc-azure` 를 사용 하 여 **pip**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python 패키지 설치 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="00eee-172">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **Python**를 선택한 후 **Django 마이그레이션할**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="00eee-173">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="00eee-174">그러면 hello 이전 섹션에서 만든 hello SQL 데이터베이스에 대 한 hello 테이블 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="00eee-175">Hello 프롬프트 toocreate toomatch hello 사용자 hello 첫 번째 섹션에서 만든 hello sqlite 데이터베이스에 없는 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="00eee-176">Hello 응용 프로그램을 실행 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-176">Run hello application with `F5`.</span></span> <span data-ttu-id="00eee-177">사용 하 여 만든 설문 **샘플 설문 만들** 투표 제출한 hello 데이터 hello SQL 데이터베이스에 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="00eee-178">Hello 웹 응용 프로그램 tooAzure 앱 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="00eee-179">hello Azure.NET SDK 웹 웹 응용 프로그램 tooAzure 앱 서비스 웹 앱을 쉽게 toodeploy를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="00eee-180">**솔루션 탐색기**hello 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="00eee-182">**Microsoft Azure 웹앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="00eee-183">클릭 **새로** toocreate 새 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="00eee-184">Hello 필드 뒤에 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="00eee-185">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="00eee-185">**Web App name**</span></span>
   * <span data-ttu-id="00eee-186">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="00eee-186">**App Service plan**</span></span>
   * <span data-ttu-id="00eee-187">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="00eee-187">**Resource group**</span></span>
   * <span data-ttu-id="00eee-188">**지역**</span><span class="sxs-lookup"><span data-stu-id="00eee-188">**Region**</span></span>
   * <span data-ttu-id="00eee-189">둡니다 **데이터베이스 서버** 도**데이터베이스가 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="00eee-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="00eee-190">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="00eee-191">웹 브라우저가 toohello 게시 된 웹 응용 프로그램을 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="00eee-192">Hello를 사용 하 여 예상 대로 hello 웹 응용 프로그램 작업을 참조 해야 **SQL** Azure에서 호스팅되는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="00eee-193">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-193">Congratulations!</span></span>

     ![웹 브라우저](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="00eee-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00eee-195">Next steps</span></span>
<span data-ttu-id="00eee-196">Visual Studio, Django 및 SQL 데이터베이스에 대 한 Python Tools에 대 한 자세한 이러한 링크 toolearn를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00eee-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="00eee-197">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="00eee-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="00eee-198">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="00eee-198">[Web Projects]</span></span>
  * <span data-ttu-id="00eee-199">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="00eee-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="00eee-200">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="00eee-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="00eee-201">[Django 설명서]</span><span class="sxs-lookup"><span data-stu-id="00eee-201">[Django Documentation]</span></span>
* <span data-ttu-id="00eee-202">[SQL 데이터베이스]</span><span class="sxs-lookup"><span data-stu-id="00eee-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="00eee-203">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="00eee-203">What's changed</span></span>
* <span data-ttu-id="00eee-204">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="00eee-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure 포털]: https://portal.azure.com
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[VSIX Visual Studio 샘플에 대 한 Python Tools 2.2]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32비트]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python Tools for Visual Studio 설명서]: http://aka.ms/ptvsdocs
[Microsoft Azure의 원격 디버깅]: http://go.microsoft.com/fwlink/?LinkId=624026
[웹 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624027
[클라우드 서비스 프로젝트]: http://go.microsoft.com/fwlink/?LinkId=624028
[Django 설명서]: https://www.djangoproject.com/
[SQL 데이터베이스]: /documentation/services/sql-database/
