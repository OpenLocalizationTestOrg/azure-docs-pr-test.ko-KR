---
title: "Azure의 Django 및 MySQL과 Python Tools 2.2 for Visual Studio"
description: "Python Tools for Visual Studio를 사용하여 MySQL 데이터베이스 인스턴스에 데이터를 저장하고 Azure 앱 서비스 웹앱에 배포할 수 있는 Django 웹앱을 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="721ba-103">Azure의 Django 및 MySQL과 Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="721ba-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="721ba-104">이 자습서에서는 PTVS 샘플 템플릿 중 하나를 사용하여 간단한 설문 조사 웹앱을 만들기 위해 [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="721ba-105">Azure에서 호스트된 MySQL 서비스를 사용하는 방법, MySQL을 사용하도록 웹앱을 구성하는 방법 및 [Azure 앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)에 웹앱을 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="721ba-106">이 자습서에 포함된 정보는 다음 비디오에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="721ba-107">[PTVS 2.1: MySQL을 사용하는 Django 앱][video]</span><span class="sxs-lookup"><span data-stu-id="721ba-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="721ba-108">Bottle, Flask 및 Django 웹 프레임워크, Azure 테이블 저장소, MySQL 및 SQL 데이터베이스 서비스를 사용하여 PTVS로 Azure 앱 서비스 웹앱을 개발하는 내용을 다루는 추가 문서에 대해서는 [Python 개발자 센터] 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="721ba-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="721ba-109">이 문서는 앱 서비스를 중점적으로 다루지만 포함된 단계는 [Azure 클라우드 서비스]를 개발할 때와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="721ba-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="721ba-110">Prerequisites</span></span>
* <span data-ttu-id="721ba-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="721ba-111">Visual Studio 2015</span></span>
* <span data-ttu-id="721ba-112">[Python 2.7 32비트] 또는 [Python 3.4 32비트]</span><span class="sxs-lookup"><span data-stu-id="721ba-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="721ba-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="721ba-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="721ba-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="721ba-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="721ba-115">[Azure SDK Tools for VS 2015]</span><span class="sxs-lookup"><span data-stu-id="721ba-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="721ba-116">Django 1.9 이상</span><span class="sxs-lookup"><span data-stu-id="721ba-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="721ba-117">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="721ba-118">신용 카드 및 약정은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="721ba-119">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="721ba-119">Create the Project</span></span>
<span data-ttu-id="721ba-120">이 섹션에서는 샘플 템플릿을 사용하여 Visual Studio 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="721ba-121">가상 환경을 만들고 필요한 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="721ba-122">sqlite를 사용하여 로컬 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="721ba-123">그런 후 응용 프로그램을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="721ba-124">Visual Studio에서 **파일**, **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="721ba-125">[Python Tools 2.2 for Visual Studio Samples VSIX]의 프로젝트 템플릿은 **Python**, **샘플**에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="721ba-126">**Polls Django Web Project** 를 선택하고 확인을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![새 프로젝트 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="721ba-128">외부 패키지를 설치할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="721ba-129">**가상 환경에 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-129">Select **Install into a virtual environment**.</span></span>
   
    ![외부 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="721ba-131">기본 해석기로 **Python 2.7** 또는 **Python 3.4**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![가상 환경 추가 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="721ba-133">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **Python**을 선택한 다음 **Django Migrate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="721ba-134">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="721ba-135">Django 관리 콘솔이 열리고 프로젝트 폴더에 sqlite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="721ba-136">프롬프트에 따라 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="721ba-137">`F5`키를 눌러 응용 프로그램이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="721ba-138">위쪽의 탐색 모음에서 **로그인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Django 탐색 모음](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="721ba-140">데이터베이스를 동기화할 때 만든 사용자의 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![로그인 형식](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="721ba-142">**Create Sample Polls**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="721ba-144">poll and vote를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-144">Click on a poll and vote.</span></span>
    
     ![샘플 설문 조사 투표](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="721ba-146">MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="721ba-146">Create a MySQL Database</span></span>
<span data-ttu-id="721ba-147">데이터베이스에 대해 Azure에서 ClearDB MySQL 호스트 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="721ba-148">또는 Azure에서 실행되는 자체의 가상 컴퓨터를 만든 다음 MySQL을 직접 설치하고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="721ba-149">다음 단계에 따라 무료로 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="721ba-150">[Azure 포털]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="721ba-151">탐색 창 맨 위에서 **새로 만들기**를 클릭한 다음 **데이터 + 저장소**를 클릭한 다음 **MySQL 데이터베이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="721ba-152">새 리소스 그룹을 만들어 새 MySQL 데이터베이스를 구성하고 적절한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="721ba-153">MySQL 데이터베이스를 만든 후 데이터베이스 블레이드에서 **속성** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="721ba-154">복사 단추를 사용하여 **CONNECTION STRING** 값을 클립보드에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="721ba-155">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="721ba-155">Configure the Project</span></span>
<span data-ttu-id="721ba-156">이 섹션에서는 방금 만든 MySQL 데이터베이스를 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="721ba-157">Django에서 MySQL 데이터베이스를 사용하는 데 필요한 추가 Python 패키지도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="721ba-158">그런 다음 웹앱을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="721ba-159">Visual Studio에서 **ProjectName**폴더의 *settings.py* 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="721ba-160">일시적으로 연결 문자열을 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="721ba-161">연결 문자열은 다음 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="721ba-162">MySQL을 사용하도록 기본 데이터베이스 **ENGINE**을 변경하고 **CONNECTIONSTRING**에서 **NAME**, **USER**, **PASSWORD** 및 **HOST** 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="721ba-163">솔루션 탐색기의 **Python Environments**에서 가상 환경을 마우스 오른쪽 단추로 클릭하고 **Install Python Package**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="721ba-164">**pip**를 사용하여 패키지 `mysqlclient`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![설치 패키지 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="721ba-166">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **Python**을 선택한 다음 **Django Migrate**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="721ba-167">그런 다음 **Django Create Superuser**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="721ba-168">이렇게 하면 이전 섹션에서 만든 MySQL 데이터베이스에 대한 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="721ba-169">프롬프트에 따라 사용자를 만듭니다. 이 사용자가 이 문서의 첫 번째 섹션에서 만든 sqlite 데이터베이스의 사용자와 일치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="721ba-170">`F5`키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-170">Run the application with `F5`.</span></span> <span data-ttu-id="721ba-171">**Create Sample Polls** 를 사용하여 만든 설문 조사와 투표를 통해 제출된 데이터는 MySQL 데이터베이스에서 serialize됩니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="721ba-172">Azure 앱 서비스에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="721ba-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="721ba-173">Azure .NET SDK를 통해 Azure 앱 서비스에 웹앱을 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="721ba-174">**솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![웹 게시 대화 상자](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="721ba-176">**Microsoft Azure 앱 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="721ba-177">**새로 만들기** 를 클릭하여 새 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="721ba-178">다음 필드에 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="721ba-179">**웹앱 이름**</span><span class="sxs-lookup"><span data-stu-id="721ba-179">**Web App name**</span></span>
   * <span data-ttu-id="721ba-180">**앱 서비스 계획**</span><span class="sxs-lookup"><span data-stu-id="721ba-180">**App Service plan**</span></span>
   * <span data-ttu-id="721ba-181">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="721ba-181">**Resource group**</span></span>
   * <span data-ttu-id="721ba-182">**지역**</span><span class="sxs-lookup"><span data-stu-id="721ba-182">**Region**</span></span>
   * <span data-ttu-id="721ba-183">**데이터베이스 서버**를 **데이터베이스 없음**으로 그대로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="721ba-184">다른 모든 기본값을 그대로 적용하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="721ba-185">웹 브라우저가 자동으로 게시된 웹앱으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="721ba-186">Azure에 호스트된 **MySQL** 데이터베이스를 사용하여 예상한 대로 웹앱이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![웹 브라우저](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="721ba-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-188">Congratulations!</span></span> <span data-ttu-id="721ba-189">Azure에 MySQL 기반 웹앱을 성공적으로 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="721ba-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="721ba-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="721ba-190">Next steps</span></span>
<span data-ttu-id="721ba-191">Python Tools for Visual Studio, Django 및 MySQL에 대해 자세히 알아보려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="721ba-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="721ba-192">[Python Tools for Visual Studio 설명서]</span><span class="sxs-lookup"><span data-stu-id="721ba-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="721ba-193">[웹 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="721ba-193">[Web Projects]</span></span>
  * <span data-ttu-id="721ba-194">[클라우드 서비스 프로젝트]</span><span class="sxs-lookup"><span data-stu-id="721ba-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="721ba-195">[Microsoft Azure의 원격 디버깅]</span><span class="sxs-lookup"><span data-stu-id="721ba-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="721ba-196">[Django 설명서]</span><span class="sxs-lookup"><span data-stu-id="721ba-196">[Django Documentation]</span></span>
* <span data-ttu-id="721ba-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="721ba-197">[MySQL]</span></span>

<span data-ttu-id="721ba-198">자세한 내용은 [Python 개발자 센터](/develop/python/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="721ba-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python 개발자 센터]: /develop/python/
[Azure 클라우드 서비스]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure 포털]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
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
